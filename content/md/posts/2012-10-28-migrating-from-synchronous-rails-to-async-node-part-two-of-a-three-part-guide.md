

{:author "admin", :title "Migrating from synchronous rails, to async node – part two of a three part guide", :date "2012-10-28 17:02:44", :publish-date "Sun, 28 Oct 2012 17:02:44 +0000"}



<!-- content below -->

This is the second of the three part series covering how to migrate from developing synchronously with Rails and [Rspec][], to asynchronously with Node, and [Mocha]. It picks up from the previous post, introducing Mocha syntax, and asynchronous testing.

We covered before how we'd implement a class with instance methods in Ruby in the previous post. 

Here's the simplified psuedo-code, for comparison to some coming javascript:

    class User do

      def initialize
        @db = Redis.new
      end
  
      def find_by_mac(mac)
        @db.hgetall(mac) 
      end

    end

It looks a bit different when working with asynchronous javascript code.

#### What implementation in node looks like

Because javascript doesn't have a class system, if we want something that acts a bit like a class, the idiomatic approach is to use functions, and use a bit of boilerplate code to make it easier to identify the function in stacktraces or logging when developing.

In javascript, instead of defining class methods or instance methods like we do with Ruby, we'd use `prototype` to inject new methods into the `User` function, so they're available to all instances of the `User` function in the system.

This chunk of code below is roughly analagous to declaring a `User` class in Ruby, mixing in methods from an `EventEmitter` module and giving it a `to_s` method, so there's a readable string returned when you try to log the class, or print it:
 
    function User() {
      if(false === (this instanceof User)) {
        return new User();
      }
      events.EventEmitter.call(this);
    }
    sys.inherits(User, events.EventEmitter);

    User.prototype.toString = function() {
      return "User"
    }

One thing - because we can rely on `User.prototype.toString` returning a value instantaneously, we can treat it as synchronous code, without thinking about callbacks, and using return the way we would in other languages.

#### Writing asynchronous functions

However, when we're working with asynchronous functions, things are different, and so far, we've only covered calling them, not defining them.

Here's a simplified version of an asynchronous function in use in the `User` function. 

We have defined a function on the prototype of `User`, accepting two parameters: 

  * `device_mac` - a String we use as our key when fetching a hash with Redis 
  * `callback` - the function we want to pass into `findByDevice` for later execution when Redis gives us our hash to execute operations on when it's done.
  
In line with convention, our function `callback` itself takes two parameters, `err` and `res`. In our case, `res` is the hash given to us by Redis, if all is well, and `err` is what we get if something goes wrong with Redis when it's fetching our hash for us.

    User.prototype.findByDevice = function(device_mac, callback) {
      db.hgetall(device_mac, function (err, res) {
        callback(null, res);
      })
    })

#### Checking this against our test code

It might be helpful to show these side by side, to put the implemented function on `User`, next to the function we're passing with our test to see what it is we're passing into `findByDevice`:

Our implemented function:

    User.prototype.findByDevice = function(device_mac, callback) {
      db.hgetall(device_mac, function (err, res) {
        callback(err, res);
      })
    })

The test:

    user.findByDevice('00:1e:c2:a4:d3:5e', function(err, res) {
      if (err) {
        // do something to recover
      } else {
        res.username.should.be.ok
        res.username.should.equal('mrchrisadams')
        done()
      }
    })
    
When we have the value from Redis, `callback(err, res)` is executing the function below, with our `res.username.should.be.ok` type assertions.


### When you need to call async functions from async functions

Once you've got your head around passing functions for asynchronous code, you'll often find yourself working with multiple asynchronous functions, that you need to control the order of, so that data is passed from one to the other, to give you the result you want.

Here's the first actual implementation of the `findByDevice` function I ended up using in the project I'm working on. 

We still pass in the `callback` function as our final parameter, but in order to return the value we want, we end up nesting a second call to `db.hgetall` inside the anonymous function we pass into our first call of `db.hgetall`, then use `callback(err, user)` to execute the function passed into `findByDevice`, and pass the results along to the code initially calling `user.findByDevice`.

      User.prototype.findByDevice = function(device_mac, callback) {

        db.hgetall(device_mac, function (err, device) {
          if (err) { console.log(err) }
          else {
            if (device.hasOwnProperty('mac')) { 
              db.hgetall(device.owner, function (err, user) {
                if (err) { console.log(err)}
                else{
                  callback(err , user)
                }
              });
            }
          }
        });
      }
      
### Avoiding callback hell.

Even with just two asynchronous function calls, this isn't very readable. 

Also, it seems that nearly every second developer on the planet playing with node has written their own callback handling library to make this easier to read and more maintainable. 

In fact, there's a bewildering number of libraries out there that claim to make this problem much easier to understand. 

In the next post, I'll introduce `async.js` a well documented library I've found fairly straightforward to work with, to help mitigate against callback hell.

<!--  -->
[Mocha]: http://visionmedia.github.com/mocha/
[Rspec]: http://rspec.info/

