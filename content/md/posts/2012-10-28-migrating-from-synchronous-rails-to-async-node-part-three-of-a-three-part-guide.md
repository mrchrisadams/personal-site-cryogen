

{:author "admin", :title "Migrating from synchronous rails, to async node – part three of a three part guide", :date "2012-10-28 18:10:41", :publish-date "Sun, 28 Oct 2012 18:10:41 +0000"}



<!-- content below -->

In the last post, I implemented an asynchronous function that wrapped a call to Redis, using an existing node library, `node-redis`. 

The final implementation introduced nested asynchronous method calls, and the code ended up looking a bit like this, even after simplifying somewhat:

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

Now the code took this form, because we relied on the results of one asynchronous function to make the second one - if you take a second to imagine how hard to read this would look at four, five or six levels of nesting, you'll quickly understand why so many developers are writing their own callback management libraries to make this easier to work with.

### Introducing async.js

The one I've found most promising so far is `async.js`, a fairly comprehensive utility module that provides a number of different ways to ensure that asynchronous functions are either called in a specific order, or run in parallel, aggregating their results before allowing code to continue and so on.

In this case, I'll be focusing on the use of `waterfall`, a function in the `async` module that lets you pass in an array of functions to be called in order, passing the results of one to the next, until a final callback passes the final result on to the code initially calling the function `async` was called from within.

      User.prototype.findByDevice = function(device_mac, callback) {

        async.waterfall([

            // fetch our device first
            function(cb){
              db.hgetall(device_mac, function (err, res) {
                cb(null, res);
              })
            },

            // new we have our device, fetch the user
            function(device, cb){
              db.hgetall(device.owner, function (err, res) {
                cb(err, res);
              })
            }

            // return our user object
          ], function (err, user) {
            callback(err, user)
          });

      }
      
In our case, we have our function `findByDevice` on `User`, and we have passed an array containing our two asynchronous functions as the first argument to `async`, then passing a final anonymous function to return our user object.

To be more specific, just like the code above, we take our mac address string as the first parameter to `findByDevice`, and the function to execute as our second parameter, `callback`. 

We then make the asynchronous call to Redis to fetch a device object, passing in `cb` as our function to execute once Redis has given us our hash, to pass it to the next function in the array.

We then use the `owner` property of the device object passed into the second function, to make another call to fetch our user, again passing in `cb`, to execute once Redis has given us a user object, to pass to the final function.

Once we have the user object, we can pass it on to the code that called `findByDevice` with `callback(err, user)`, completing the asynchronous callback chain.

#### More than just waterfalls

Of course, just because we now know how to execute asynchronous functions in a set order, one after the other like we're used to doesn't mean we _should_ always do so. 

One of the advantages of node's asynchronous style is that it allows the [parallel execution][] of code, so the same operations could be applied to the an array of values at the same time, getting around bottlenecks, but then only passing on the results once all the operations have been completed.

Alternatively, this allows us to pop values onto [queues][], with set numbers of workers, to work through them, without needing a dedicated worker process like you would with in Rails for, when using [delayed_job][] or [resque][].

#### Doesn't all this seem like a lot of work though? The ruby you showed me first was much shorter, and easier to read

In a word, yes. 

Node isn't a magic bullet, and although it's popular, if you're doing a basic CRUD app, there are often very good reasons to choose Rails, Django over Node and Express. 

That being said, it pays to understand your options when choosing a particular technology to solve the problem facing you. Also, if you're a fan of behaviour driven development, it's good to know that such an approach is possible with this technology, and, once you've got your head around async programming, there's value in knowing that there some well developed tools to help you apply these techniques to both server-side, and client-side javascript.

If anything's not clear in this series, please let me know - I've sunk a good few hours into these posts now, to make it easier to understand async node development if you're used to sync ruby development, and I'd really like to know where I can improve these for future visitors.

<!-- links -->
[parallel execution]: https://github.com/caolan/async#parallel
[queues]: https://github.com/caolan/async#queueworker-concurrency
[delayed_job]: https://github.com/collectiveidea/delayed_job
[resque]: https://github.com/defunkt/resque

