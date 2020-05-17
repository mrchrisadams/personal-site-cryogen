

{:author "admin", :title "Going beyond typing cap deploy", :date "2010-05-05 22:08:05", :publish-date "Wed, 05 May 2010 22:08:05 +0000"}



<!-- content below -->

I mentioned earlier that if you don't use [Capistrano][] too much, you might not be aware it's designed in such a way that it can be called happily from within Ruby code as well as being called on the command line.

In fact, the snippets below from the [rdoc pages for the project](http://rdoc.info/projects/jamis/capistrano "rdoc.info :: capistrano"), given idea of what's going on under the hood, when you call `cap deploy`.

Here's the command when we call it straight from the command line, within a capified project:

<pre lang="bash">
`cap deploy update_code -vvvv` 
</pre>

Now here's the same command, wrapped with a very lightweight ruby sprinkling of ruby, that wouldn't need us to supply any command line arguments ourselves.

<pre lang="ruby">
require 'capistrano/cli'
  Capistrano::CLI.parse(%w(-vvvv -r config/deploy update_code)).execute!
</pre>

There's a whole lot of clever stuff happening when the `capistrano/cli.rb` is called, like instantiating a configuration object that stores the arguments for parsing, and serves as a base for other methods, tasks and even full-on recipes to be attached to. 

The snippet above is roughly equivalent to the code below, if we wanted to be explicit bout what how we wanted things to be done.

<pre lang="ruby">
  require 'capistrano'
  require 'capistrano/cli'
  config = Capistrano::Configuration.new
  config.logger_level = Capistrano::Logger::TRACE
  config.set(:password) { Capistrano::CLI.password_prompt }
  config.load "config/deploy"
  config.update_code
</pre>

While writing this post, I consulted the [Capistrano][] docs on [rdoc.info](http://rdoc.info/ "rdoc.info") repeatedly, and I think at long last, I'm starting to see the appeal of [Yard](http://yardoc.org/ "YARD 0.5.4 - The Longest") for documentation now. Now to find a fun little project to actually try it out on...


[Capistrano]: www.capify.org "Capistrano"

