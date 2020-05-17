

{:author "admin", :title "How to update Boxen on your mac with changes from upstream", :date "2014-06-08 16:44:29", :publish-date "Sun, 08 Jun 2014 16:44:29 +0000"}



<!-- content below -->

I use Boxen to manage which development software is on my mac, which can be useful to keep track of changes. It's also handy for staying familiar with puppet when you're not working with it directly at work.

The downside to keeping a machine under config management is that you can't always just run `brew install shiny_new_software_package` when you need to get a new version of Ruby installed or something similar, as Boxen tends to use a few nonstandard defaults.

It's also worth pulling in the latest upstream updates to the Boxen repo from time to time, to make sure you're benefiting from fixes and upgrades made there.

AS much for my future self as anyone else, here's a guide on upgrading your version of Boxen you've checked out an installed onto your own mac with updates from the upstream repo.

### Add an upstream for the official boxen repo

```
cd ~/src/our-boxen
$ git remote add upstream https://github.com/boxen/our-boxen.git
```

### Get upstream updates

Then we’re going to fetch the stuff from the upstream repository:

```
$ git fetch upstream
```

### Merge in upstream changes

Now we’re going to merge the updated repository with our own:

```
$ git checkout master
$ git merge upstream/master
```

### Resolve conflicts, and run boxen to update machine

After this, you'll usually need to clear up any conflicts in your puppet file. In my case, some packages I had added over the last few months, like [Go][], or [PhantomJS][] were now in the default list of Puppet modules that comes with Github. I had to remove the extra mentions of these in the Puppetfile, so it only declared a dependency on them once.

After this, you should be to rm the now out-of-date `Puppetfile.lock`, and run `boxen`, to a) generate a new Puppetfile.lock and also install all the new bits of software declared in the Puppet manifests you use to manage your mac.

This [guide by Graham Gilbert][updating boxen] was incredibly helpful in working through these steps myself today. Thanks Graham!

[PhantomJS]: http://phantomjs.org/
[Go]: http://golang.org/
[updating boxen]: http://grahamgilbert.com/blog/2014/04/04/updating-boxen/


