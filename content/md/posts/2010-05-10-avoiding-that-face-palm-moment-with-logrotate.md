

{:author "admin", :title "Avoiding that Face Palm moment with Logrotate", :date "2010-05-10 22:08:33", :publish-date "Mon, 10 May 2010 22:08:33 +0000"}



<!-- content below -->

A runaway log file brought down on a previously built Rails app I was involved in building recently, and the solution to the problem here is so simple and easy to implement that a) I feel like a total dunce for not having this setup here in the first place b) it's almost churlish not to list it here, for reference for someone else, in the hope that it saves them feeling this stupid themselves in the future, (oh, and keeps the site they're working on up...).

If you're not using Rail's own to rotate the log files it generates, it really is good idea to make sure any log files it _does_ make are being rotated, to make sure you don't get caught out when that innocuous seeming `development.log` file from a few months back goes live ends up bringing down your site because it's since grown from a 6k file to a 7 gigiabyte one, and eaten all the space on your server.

Making sure this doesn't happen is a pretty simple process:

- Find where the offending logfiles are eating up all your disk space.
- Create a new [logrotate][] entry pointing to them.
- Trigger the [logrotate][] daemon to test it
- Relax and get on with your life
 
Okay lets run through this in more detail.

#### Find the offending logfiles

The first step here is to find where the logs are being created. This here is the cause of the problem on a lot of boxes running Rails apps, because if you're using Capistrano to deploy an app, and you're using a stock Passenger config then your logs will end up in somewhere that the [logrotate][] daemon, the program that dutifully goes around compressing and sorting logfiles on your server, won't know where to look for by default.

Normally, you can expect to find these quietly ballooning log files somewhere like `/home/deploy/app/shared/log/`, or `/rails/deploy/appname.production/shared/log/`.

#### Create the new logrotate entry

Now that we know where the logs are that keep eating space, we can tell [logrotate][] about them, to make sure they won't grow too large. Create a text file named `railsapp` (or whatever makes the most sense to you) in `/etc/logrotate.d/`, the default place to leave instructions for [logrotate][] to follow:

<pre lang="bash">

/home/deploy/app/shared/log/*.log {
  daily
  missingok
  rotate 30
  compress
  delaycompress
  sharedscripts
  postrotate
    touch /home/deploy/app/current/tmp/restart.txt
  endscript
}

</pre>

Looking at that line by line:

- `daily` calls this script daily 
- `missingok` means it's okay if we're missing some log files, we'll still work without stopping
- `rotate 30` means keep the last 30 days of logs
- `compress` yup, compress the logs (using gzip by default)
- `delaycompress` means "wait til the next day before compressing this file, just incase there are still be processes writing to this logfile"
- `sharedscripts` means only call the next `postrotate` script once for all the files that match the pattern above, instead of restarting for each file
- `postrotate` ... `endscript` - this script here fires after a rotate, to restart the passenger server, so that future processes log to the fresh, empty logfile

If you want to learn more, this article by [Jesse Andrews on how he uses it][1]  is an absolute gem.

#### Trigger the logrotate daemon

Now that we have a [logrotate][] entry, lets check it if works now rather than going to bed and finding out we had mistyped the path, by *forcing* a log rotate with this command (note the `-f` flag):

<pre lang="bash">
logrotate -f /etc/logrotate.d/railsapp
</pre>


#### Get on with your life

If that's worked, then huzzah! That should be one less thing to worry about when looking after a webapp - though the usual "do some real homework before putting absolute faith in and deploying on a production system" disclaimers apply. As ever with Linux, be sure to [read the man pages][2] before use.



_*nb.* While it's true that Rails is actually smart enough to rotate its own logs if you remember to configure it to behave this way, learning how to use [logrotate][] like this means we can use this on other apps too, without being too tied to a particular framework. Handy when you need it for a Merb, Sinatra, Django, or even Node.js project_


<!-- Links -->
[logrotate]: http://gd.tuwien.ac.at/linuxcommand.org/man_pages/logrotate8.html "logrotate"
[1]: http://overstimulate.com/articles/logrotate-rails-passenger "Log Rotation for Phusion Passenger | overstimulate"
[2]: http://gd.tuwien.ac.at/linuxcommand.org/man_pages/logrotate8.html "logrotate"

