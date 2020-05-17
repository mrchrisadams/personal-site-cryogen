

{:author "admin", :title "How to set up a debugger with mod_rails/Passenger", :date "2009-04-28 09:47:32", :publish-date "Tue, 28 Apr 2009 09:47:32 +0000"}



<!-- content below -->

Anyone who's worked on the web will know easy it is to end up constantly refreshing pages to see if the content delivered from say, a database driven site is the indeed content you want to show. 

This is one approach, and while simple to understand, there are often other approaches available to this. 

One example is using the ruby debugger, and break points in your code to inspect and control what is happening at each step, to see what variables are available.

This, combined with the more traditional tools for debugging a view using `@object.inspect` or `debug(@object)` methods make fixing bugs less of a pain.

As many of us transition from using Mongrel as our server to Passenger, we find ourselves missing this useful tool. This post outlines one way to setup a debugger for Passenger.

### Putting a debugger back in Passenger

Before people started using Passenger for handling rails requests, using the ruby debugger was simply a case of adding `debugger` statements in the code, and then starting the Mongrel or Webrick with `script/server --debugger`.

When the code hit a `debugger` statement, the console would drop into an interactive debugger, and all would be well with the world.

Passenger currently doesn't allow an easy way to use the debugger straight out of the box, so we'll have to make a few changes to the code in our own environments, and use a gem called ruby-debug if we want this behaviour again.

### Add ruby-debug

We're actually using a gem called ruby debug - this gives us a powerful remote debugger, to inspect code - it does load of other interesting things, but in this case we're only interested in a subset of the features here. 

<pre lang="bash">

`sudo gem install ruby-debug`

</pre>

### Add code to use ruby debug when you hit a debugger statement

Just like how we restart Passenger using the touch tmp/restart.txt file, the nicest way I've found to switch on the debugger comes from the ominously titled [duck_punching](http://duckpunching.com/passenger-mod_rails-for-development-now-with-debugger "duck_punching Passenger (mod_rails) for development. Now with debugger!") weblog. It involves adding a `rake` task to create a `debug.txt` text file, and adding a snippet of code to your development.rb config file:

<pre lang="ruby">

    if File.exists?(File.join(RAILS_ROOT,'tmp', 'debug.txt'))
      require 'ruby-debug'
      Debugger.wait_connection = true
      Debugger.start_remote
      File.delete(File.join(RAILS_ROOT,'tmp', 'debug.txt'))
    end
</pre>

This snippet checks for the existence of a debug.txt in the `tmp` directory of the main Rails directory, and if it's there, it opens a connection to connect to for debugging.

And here's there restart task for rake:

<pre lang="ruby">
    desc "Restarts passenger if in debug mode"
    task :restart do
      system("touch tmp/restart.txt")
      system("touch tmp/debug.txt") if ENV["DEBUG"] == 'true'
    end
</pre>

To run in debug mode, you just pass the constant DEBUG in while calling the rake task like so:

<pre lang="ruby">
    rake restart DEBUG=true
</pre>

### Sprinkle in your debugger statements

We can now add the `debugger` statements where we want the breakpoints in our code for us to inspect. 

### Open a rdebug session

Now we can finally open our ruby debug session, using the -c switch to start our client connection.

<pre lang="ruby">
    rdebug -c

</pre>

Because we're connecting to the same machine as we're running rails on, it defaults to localhost, but we can connect to other remote machines too.

### Gotcha - Remember to reboot!

Once you've finished your command line debugging session, and exited the debugger, you won't be able to start a new sessions without calling the `rake:restart` command with the `DEBUG=true` values.

Now that you have this set up, take a look at this [Railscast by Ryan Bates](http://railscasts.com/episodes/54-debugging-with-ruby-debug "Railscasts - Debugging with ruby-debug") or this one by [Brian Donovan](http://brian.maybeyoureinsane.net/blog/2007/05/07/ruby-debug-basics-screencast/ "Local Insanity - Ruby Debug Basics [screencast]") to get an idea of just how useful the ruby debugger is. 

Patrick Lenz has another [really helpful article](http://www.sitepoint.com/article/debug-rails-app-ruby-debug/ "Debug Your Rails App With ruby-debug [Ruby &amp; Rails]") that goes in depth with the commands available to you during a debug session - I found it incredibly useful, and I can't recommend it highly enough.

