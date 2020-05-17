

{:author "admin", :title "Migrating from synchronous rails, to async node - part one of a three part guide", :date "2012-10-28 16:55:31", :publish-date "Sun, 28 Oct 2012 16:55:31 +0000"}



<!-- content below -->

In my spare time, I've recently been working with a few codebases that either are written in, or use enough code written in nodejs, that make me keen to have some kind of testing framework in place to help put the same kinds of safety nets in place that I'm used to working with on Chef, Sinatra or Rails projects.

After losing a couple of weekends looking into BDD style development with node, and getting my head around asynchronous coding concepts, I think I've settled on an approach that feels enough like Rspec to feel comfortable enough to use for future server-side js development.

It's way too much for a single post, so I'll be sharing the first of a three part series of posts here, to help other Ruby developers used to synchronous development with [Rspec][] adjust to asynchronous development using [Mocha][], the closest thing I can find to it in node-land right now.

In this post I'll cover how [Mocha][] syntax compares to [Rspec][], then the next post I'll cover implementing the code to pass these Mocha tests. In the third post, I'll touch on how to keep asynchronous code halfway manageable in node, and avoid getting stuck in callback hell.

### How we do it in Ruby

I'm going to use a side project I've been hacking on for a few months, to show how I'd add a new class to wrap calls around a persistence layer to provide a degree of encapsulation, abstracting away the database technology from external interface for the class.

In this case, with my User class, I want to have a method that finds me a user, stored as a hash in Redis, keyed on the mac address of the laptop or iphone they're using.

The tests I'd write might look a bit like this pseudocode here:

    describe 'User' do

      before(:each) do 
        redis = Redis.new
        # create an entry in redis with the key "99:aa:44:33:01:3r", 
        # and the hash below
        redis.hmset("99:aa:44:33:01:3r", {
          :username    => "mrchrisadams",
          :name        => "Chris"
          :email       => "wave@chrisadams.me.uk",
          :mac_address => "99:aa:44:33:01:3r"
        })
      end

      it 'fetches the user object' do 
        u = User.new
        c = u.find_by_mac('99:aa:44:33:01:3r')
        c.name.should be('mrchrisadams')
      end

    end

I use the `before` block to store a hash inside redis, setting a few extra values on it, and then later on, in the `it 'fetches the user object'` block, I create an instance of my `User` class, and call the `find_by_mac` method to fetch me the hash I just stored in Redis.

The implemntation code in Ruby, might look like this:

    class User do

      def initialize
        @db = Redis.new
      end
  
      def find_by_mac(mac)
        @db.hgetall(mac) 
      end

    end

So far so good. This is synchronous code, and feels comfortable, and is easy enough to work with.

### Doing this in node

_For future reference, the [completed mocha test code is here on github][1], and the [completed implementation code is here too][2]._

Now, lets try to take the same approach in node, to see how different this looks, but also to see what we need to be aware of when learning to think in asynchronous terms. 

So, lets be good developers and try to write out test code first, in Mocha. I'll paste the lot, then go through the interesting bits piece by piece.

    describe('User', function() {
      describe('#findByDevice', function() {

        beforeEach(function(done) {

          db.hmset("mrchrisadams", {
            name: "Chris Adams",
            username: "mrchrisadams",
            devices: ["00:1e:c2:a4:d3:5e"],
            email_address: "wave@chrisadams.me.uk"
          }, done);

        })


        it('should fetch the user for that mac', function(done) {
          var user = new User();
          user.findByDevice('00:1e:c2:a4:d3:5e', function(err, res) {
            if (err) {
              console.log(err)
            } else {
              res.username.should.be.ok
              res.username.should.equal('mrchrisadams')
              done()
            }
          }); // find by device
        }) // should fetch the user for that mac
      })
    })

So first of all, much of the syntax is looks quite like Rspec. We have nested `describe` and `it` blocks, and even the assertion syntax is familiar, with nice, readable `should`s, `be`s and `equal`s all around.

However, there are a few important additions here that we need, to allow for the asynchronous nature of node.

First of all, lets look at the `beforeEach` function:

    beforeEach(function(done) {

      db.hmset("mrchrisadams", {
        name: "Chris Adams",
        // object vars edited out for brevity
      }, done);
    })

In this case, we're making a call to db, an instance of `node-redis` a popular redis client library for node, that is completely asynchronous.

If we tried using the bog-standard `beforeEach` function like this, when working with an asynchronous library (not the lack of `done`), it would look like the code below:

      beforeEach(function() {
        db.hmset("mrchrisadams", {
          name: "Chris Adams",
          // object vars edited out for brevity
        });
      })

Had we done this, node would have zipped to the `beforeEach` function, started it, then returned straight away, racing ahead trying to run the tests below it, without waiting for our Redis setup steps to be finished. 

Now Redis is fast, but you can't rely on that to make sure your tests are set up before you run them, and this code would have given us at best unpredictable results, but more likely, fails across the board.

#### `done` to the rescue

Here's how we do it when working asynchronously with [Mocha][].

    beforeEach(function(done) {

      db.hmset("mrchrisadams", {
        name: "Chris Adams",
        // object vars edited out for brevity
      }, done);
    })
    
The difference this time round is that we're passing in `done`, a function that exists to stop the tests running until our Redis setup steps are finished, and we're in a state for testing.

We have to take this approach too for the tests itself, in our `it` function:

    it('should fetch the user for that mac', function(done) {
      var user = new User();
      user.findByDevice('00:1e:c2:a4:d3:5e', function(err, res) {
        if (err) {
          // do something to recover
        } else {
          res.username.should.be.ok
          res.username.should.equal('mrchrisadams')
          done()
        }
      }); // close findByDevice
    }) // close should fetch the user for that mac

Here, we're doing something very different to the ruby approach of storing returned values from methods in variables, then testing the value of those.

#### Our first real exposure to "continuation-passing style"

Look at this line in paticular: 

    user.findByDevice('00:1e:c2:a4:d3:5e', function(err, res)
    
Understanding this here for me was the key to getting my head around this initially very alien syntax. If you're having trouble with the shift from sync to async, the closest thing in typical sync ruby code might be something like this line, where you set the varibale `res` then use it for testing assertions against:

    res = user.findByDevice('00:1e:c2:a4:d3:5e)
    res.should be_okay

Now there's two important things here to remember when working with node:

1) Because we're working asynchronously, we only want to run out assertions once we know we have the values back from the call we just made
2) We are working with javascript, passing functions around to execute the code inside them at a later date, both common, and necessary.

So, our solution to the asynchronous problem, is to pass in a _function with the assertions we care about inside it_, as a parameter to our `findByDevice` call on the user object.

So, what we're saying here is: "go fetch the results of `findByDevice`, with the paramters `00:1e:c2:a4:d3:5e`, and here's the function I'd like you to execute when you're done, please":

      user.findByDevice('00:1e:c2:a4:d3:5e', function(err, res) {
        if (err) {
          // do something to recover
        } else {
          res.username.should.be.ok
          res.username.should.equal('mrchrisadams')
          done()
        }
      })

You might be confused by the two parameters `err`, and `res`. 

There is a generally accepted convention when coding asynchronously in node, to make it possible to pass the result from one callback to another. Passing in a function which itself has the parameters `error`, and `result` (or some variaton on the name, like `err`, and `res`) as the last argument going into a method call is idiomatic node javascript now, and is often referred to as the continuation-passing style. 

It's crucial to understand it, because you won't get far without it.

#### Where does `done()` fit into this?

You might notice a call to `done()` on the last line of the function we're passing in, after the assertions. 

[Mocha][], when you pass in `done` to a testing block, doesn't know when the test finished, so will wait for `done()` to be called, before deciding if that particular `it` block has failed or passed.

### Now onto the implementation in node

So we've run thorugh how [Mocha][] works now, and how it compares to [Rspec][], and we've seen how we rely on anonymous functions to run our assertions on the results of asynchronous functions.  

(As an aside, anonymous functions are simply functions with no name -  just the keyword, parameters, the code to execute them. They looks like `function(err, res) { // do stuff }`, instead of `function hasSomeName(err, res) { // do stuff }` ).

It's worth re-reading the above, until you're really comfortable with the concepts, as the next section, implementation is unfortunately pretty messy.

<!-- links -->
[1]: https://github.com/mrchrisadams/herenow/blob/users/test/herenow/users.js
[2]:(https://github.com/mrchrisadams/herenow/blob/users/herenow/db/user.js
[Mocha]: http://visionmedia.github.com/mocha/
[Rspec]: http://rspec.info/


