

{:author "admin", :title "How to use get Git, Things and Dropbox to work together ", :date "2011-01-16 23:16:29", :publish-date "Sun, 16 Jan 2011 23:16:29 +0000"}



<!-- content below -->

I've started using [Things][] as a way to keep track of [Things][] I've committed to doing, or _should_ be doing, and I'm a big fan: it syncs nicely with an iPhone, and it's full of loads of lovely UI touches, like automatically loading the url, or email message URI you're looking at into the notes section when making a new to do item, or providing well thought out keyboard short cuts, or simply having a "Today" mode designed let you set targets just for today, and forgot about the rest of your ever growing todo pile.

There's one shortcoming I've found though, and that's using [Things][] with more than one computer - it isn't supported by out of the box, and using [Dropbox][], my normal way of sharing content between two computers, doesn't play too nicely with [Things][] by default either.

However, on Cultured Code's own wiki there there some handy instructions for using Git to allow multiple instances of [Things][] to share a single tasks database, but setting up a remote git server just to share todo's across computers seems like a git of an overkill - instead, I've adopted them to work with [Dropbox][], using a simple directory to share repos, instead of using a whole separate server.

In this post, I'll outline, how to set this up for yourself. 

### What we're going to do here

This is a fairly lengthy post, so I'll outline what we're doing first:

a) setup an a Git Repo in [Dropbox][] that we push updates to.

b) Set up a clone of this repo on computer where the [Things][] todo database is normally stored, and track changes in there.

c) Setup something like a cronjob using OS X's equivalent, `launchctl` to commit the changes every half hour, and push them to the main Git repo on dropbox.

Of we go then...

#### Setting up our [Dropbox][] Git Repo

First of all, we setup our repository in [Dropbox][] like so:

<pre lang="bash">
  mkdir -p ~/Dropbox/Git-Repos/Things.git   
</pre>

It should look something like this in the finder:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/01/git-repos.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/01/git-repos.png" alt="" title="git-repos" width="670" height="327" class="alignright size-full wp-image-416" /></a>


Now we have a directory for our git repo, we need to initialise it, using a special flag, `--bare`. This creates a repo that's ready for us to push code to:

<pre lang="bash">
  cd Things.git
  git --bare init
</pre>

Congrats, that's step one done!

### Cloning the repo into we we put our Things

Now we have somewhere to push code to, lets start pushing code. We're going to into the directory where [Things][] data is stored, initialise a repo, and make our first commit:

<pre lang="bash">
  cd Library/Application\ Support/Cultured\ Code/Things
  git init
  git add .
  git commit -a -m "initial commit"
</pre>

Okay, we've made our repo for [Things][], but we still don't have a way of getting content to the [Dropbox][] repo, which is our canonical repo that we'd like to push code to. We need to tell git where the remote to push code to.

Normally with git, you'll push code to another server, but you can just as easily just push to another directory using git - this lets [Dropbox][] handle the hard work of giving us distributed backups, and making this repo available to other computers:

<pre lang="bash">
  git remote add dropbox ~/Dropbox/Git-Repos/Things.git
  git push dropbox master 
</pre>

Okay, so we've now created a central repo, we've created a local repo where we store our [Things][], and we've pushed our first chunk of code there too. Now we just need to automate this process, so we don't have to think about it in future.

### Making this run on autopilot

For this, we turn to `Launchd`, a tool on the mac to run commands automatically in the background, somewhat like a a newer version of cron. It's what starts all your programs on boot, but it's also used to run certain tasks at certain times of the day on a schedule.

What we're going to do here is use it to run a shell script every 30 minutes when the computer is awake, to commit the latest state of the file storing our [Things][] data locally, then push that changeset to the main repo on Dropbox. Paste this code into a file called `thingssync.sh`. 

<pre lang="bash">
  #!/bin/bash
  DATE=`date`
  REMOTE='dropbox'
  cd ~/Library/Application\ Support/Cultured\ Code/Things
  git pull $REMOTE master
  git commit -a -m "Auto Sync - $DATE"
  git push $REMOTE master
</pre>

The `git pull` line is there to keep this in sync with other instances of Things. The `git commit` line will aways give us a unique commit message, and the `git push`, makes sure we are pushing to the right branch.

Next, we need to breathe life into this script, by making it executable. We use a sometimes arcane unix command here, `chmod` (our `+x` part of the command gives it an executable bit, allowing it to be run by itself):

<pre lang="bash">
  chmod +x thingssync.sh   
</pre>

We need to put this newly enlivened script into a place where our `launchctl` daemons can actually access it, so let's put it into the user directory `usr/local/bin` - I tend to prefer this as a place for storing executable binaries than `/usr/bin`, because a) it means we don't have to start using `sudo` to make future changes, and b) it should be clearer that this isn't a core binary that would be clobbered by a software update from Apple.

<pre lang="bash">
  cp thingssync.sh /usr/local/bin/ 
</pre>

The final steps are creating a `launchctl` config file known as a property list, and putting it where the `launchctl` daemons normally look for config files, and then loading it in to `launchctl` to start running our cronjobs: 

First paste this code into the property list file (more commonly referred to as a `plist file`) called `com.$(hostname).ThingsSync.plist`:


<pre lang="xml">
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN"
  "http://www.apple.com/DTDs/PropertyList-1.0.dtd">

  <plist version="1.0">
    <dict>
      <key>Label</key>
      <string>com.twelvestone.ThingsSync</string>
      <key>Program</key>
      <string>/usr/bin//local/thingsync.sh</string>
      <key>RunAtLoad</key>
      <true />
      <key>StartInterval</key>
      <integer>1800</integer>
    </dict>
  </plist>

</pre>



Then put it into the directory set aside for loading plist files, `~/Library/LaunchAgents`:

<pre lang="bash">
  mkdir -p ~/Library/LaunchAgents
  cp com.$(hostname).ThingsSync.plist ~/LaunchAgents
</pre>

Our last step before we're finished, is to load the plist file in launchctl, so it knows of its existence, without use needing to reboot the machine:

<pre lang="bash">
  launchctl load ~/Library/LaunchAgents/com.$(hostname).ThingsSync.plist 
</pre>

Once this is done, we should now have our [Things][] data being committed and pushed using git, every 30 mins while the computer is awake. If we want another machine set up work with this, we can clone from the repo in dropbox, follow steps 2 and 3, and at last, have multi-mac sync using [Things][].


<!-- links -->

[Things]: http://culturedcode.com/things/
[Dropbox]: http://dropbox.com

