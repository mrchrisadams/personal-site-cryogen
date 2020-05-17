

{:author "admin", :title "Setting environments with Rails: how Rake and Capistrano differ", :date "2009-07-30 16:38:37", :publish-date "Thu, 30 Jul 2009 16:38:37 +0000"}



<!-- content below -->

I keep forgetting this when I'm developing with Rails, and while it's not massively hard to find, it IS annoying to keep looking up, so scribbling it here should commit it slightly more fully to memory

If you want to make sure stuff happens in a certain environment with Rake, you need to make sure you set the environment before you call the command. You'll do this when setting up a database for testing.
<pre># Drop the test database</pre>
<pre>RAILS_ENV=test rake db:drop</pre>
<pre># Clear database and reset schema to restart</pre>
<pre>RAILS_ENV=test rake db:reset</pre>
<pre># Recreate the staging database, but only migrate it to version 3</pre>
<pre>RAILS_ENV=staging rake db:reset VERSION=3</pre>
However, If you're using Capistrano, and multistage environments (and you really should, it makes live, way, way better) you'll need to set it after calling the command initial, but before you pass the argument like so:
<pre># deploy an app the beta environment</pre>
<pre>cap beta deploy</pre>
<pre># setup the staging environment before deployment</pre>
<pre>cap staging deploy:setup</pre>
Rake comes first, and cap comes second.

