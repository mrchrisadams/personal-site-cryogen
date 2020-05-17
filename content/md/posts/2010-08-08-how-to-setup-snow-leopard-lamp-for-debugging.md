

{:author "admin", :title "How to setup Snow Leopard for LAMP development and debugging", :date "2010-08-08 19:00:23", :publish-date "Sun, 08 Aug 2010 19:00:23 +0000"}



<!-- content below -->

Over this weekend,  I've been looking at ways to make it easier for me to work with PHP, largely because I've been using it more and more at work, and I've felt spoilt by the tools available when using Ruby, like the [ruby debugger], or when playing with Django or Twisted, python's own interactive [pdb debugger][], so I decided to give [MacGDBp][] a try.

It's pretty handy - it allows you to step your code when things break, giving you an idea of what exactly is happening, under the hood, or letting you understand the actual a request takes through your code.

I'm not using MAMP, because where possible, I'm trying to minimise duplication of software on the my computer, and previously I've confused myself something horrible with trying to keep track of multiple instances of MySQL and Apache before, so if you're not using MAMP, following these instructions should help get you set up with a decent debugging tool, on Snow Leopard, and along the way get a fairly maintainable lamp stack, if you're not enamoured with MAMP.

#### Get PHP 5.2

This isn't strictly necessary, but right now, I've found PHP 5.2 to be less hassle when developing than 5.3, and for time being, Drupal and Wordpress to be standardising on it first before moving to the newer version, which means I am too.

The best instructions I've found to do this are here [PHP 5.2 for compatibility with Drupal][1], and provide a good introduction to the amazing Homebrew, which you really should be using instead of Macports or Fink, if you're not already.

Lets get the hard commandline work out of the way first.

#### Setup PEAR to complement Homebrew's PHP 5.2

Just like how we have pip or easy_install with Python, CPAN for Perl, and Rubygems for Ruby, with PHP, we have PECL, and PEAR. PEAR is repository of PHP classes, like PHP Unit for unit testing, whereas PECL is a repository for C extensions like APC or Memcache, that help with performance, and caching, or link to other programs.

By default we do have PEAR and PECL installed, but in keeping with Homebrew's example of storing stuff in `/usr/local/` to avoid needless sudo'ing we're going to use our own versions of PEAR, using this handy one liner. What's happening here is that we're using curl to fetch the data at http://pear.php.net/go-pear, and then streaming it into the php command:
<pre lang="bash">    curl http://pear.php.net/go-pear | sudo php</pre>
We'll be presented with some text, once we've entered our admin password, along the lines of:
<pre lang="text">  Welcome to go-pear!

  Go-pear will install the 'pear' command and all the files needed by
  it.  This command is your tool for PEAR installation and maintenance.

  Go-pear also lets you download and install the following optional PEAR
  packages: PEAR_Frontend_Web-beta, PEAR_Frontend_Gtk2, MDB2.

  If you wish to abort, press Control-C now, or press Enter to continue: 

  HTTP proxy (http://user:password@proxy.myhost.com:port), or Enter for none::</pre>
We probably don't need a proxy, so you can just hit enter, at which point we'll be asked the following:
<pre lang="text">  Below is a suggested file layout for your new PEAR installation.  To
  change individual locations, type the number in front of the
  directory.  Type 'all' to change all of them or simply press Enter to
  accept these locations.

   1. Installation prefix ($prefix) : .
   2. Temporary files directory     : $prefix/temp
   3. Binaries directory            : $prefix/bin
   4. PHP code directory ($php_dir) : $prefix/PEAR
   5. Documentation base directory  : $php_dir/docs
   6. Data base directory           : $php_dir/data
   7. Tests base directory          : $php_dir/tests

  1-7, 'all' or Enter to continue:</pre>
We want to change the installation prefix, to make sure we're putting this stuff into `/usr/local` - I found that I had to do this explicitly, because the default value for `$prefix`, ended up with me getting build errors.

Once we've added this, we'll get a load of text flying past as PEAR is built, and end up with some text saying something like:
<pre lang="text">    WARNING!  The include_path defined in the currently used php.ini does not
    contain the PEAR PHP directory you just specified:

    If the specified directory is also not in the include_path used by
    your scripts, you will have problems getting any PEAR packages working.

    Would you like to alter php.ini ? [Y/n] :</pre>
Why _yes_, we _would_ like this added. This will add this snippet to your `php.ini` file:
<pre lang="text">    ;***** Added by go-pear
    include_path=".:/usr/local/PEAR"
    ;*****</pre>
One important thing here - now that you have this, make sure your PEAR

Now, any thing you add to pear will be available in future, so installing PHP Unit for unit testing is as simple as calling this on the commandline (note):
<pre lang="bash">  pear install phpunit/PHPUnit</pre>
In a similar fashion to Rubygems, these libraries of classes are available by calling `require_once` as if you were in the path `/usr/local/PEAR`, so to pull in PHP Unit, you just type:
<pre lang="bash">  require_once 'PHPUnit/Framework.php';</pre>
#### Setup PECL with PHP 5.2

Now that we have PEAR setup, we should spend a it of time on making PECL simple to administer without sudo. All I needed to do here was check that everything in `/usr/local/Cellar/php52/` belonged to my normal user account, by calling:
<pre lang="bash">    sudo chown -R /usr/local/Cellar/php52/</pre>
This does away with the need to compile things as root, and makes installing extensions like Memcache, Mongodb, APC, as simple as:
<pre lang="bash">    pecl install apc</pre>
If you find yourself having trouble here, you may want to check the permissions on any extra directories created during the PECL installation process - I had a couple of issues because some extensions had been installed as root earlier when following [Hunter Ford's instructions at Cupcake with Sprinkles][2], which stopped my user account being able to install into the nested directory structure, because my account was trying to put files into directories owned by root.

#### Fetch Xdebug ####

If we didn't need xdebug, this would be all we needed, but sadly things aren't as simple as that. If we try calling something like `pecl install xdebug`, we DO get a version of debug installed, but it's not quite what we need, and doesn't seem to do anything useful. If we want this to work with [MacGDBp][], we need to install the version compiled by the chaps at [Active state from their Remote Debugging page][3], that's designed to work with their own IDE, but also other tools. Once we've downloaded the tar file, we need to choose the correct version,

And then copy it to where the other extensions are:
<pre lang="bash">    cp xdebug /usr/local/Cellar/php52/5.2.13/lib/php/extensions/xdebug.so</pre>
And make the relevant changes in our `php.ini` file for them, to point to the xdebug shared object (that's the `.so` suffix on extensions), and provide a few defaults as directed on the [MacGDBp help page][4]:
<pre lang="ini">  ; Adding xdebug
  zend_extension=/usr/local/Cellar/php52/5.2.13/lib/php/extensions/xdebug.so
  xdebug.remote_enable=1
  xdebug.remote_autostart=1
  xdebug.remote_host=localhost
  xdebug.remote_port=9000</pre>
In short we're telling xdebug to switch on by default, and and listen on localhost:9000 for any clients that want to connect to it when we want to inspect what's happening with code.

#### Finally turning on MacGDBp

Still with me? Good. At long last, we can finally start looking through code in our debugger. Fire up MacGDBp, and when you run your next PHP script, you should get to see something like this pic pilfered from Particle Tree's own post on this subject:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/08/particle-tree-macgdbp.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/08/particle-tree-macgdbp.png" alt="" title="particle-tree-macgdbp" width="655" class="alignright size-full wp-image-364" /></a>

There's far more to this, but in general the key to using the debugger is knowing how to set breakpoints, and remembering that your choices in the blue buttons are (from left to right)

* stepping _into_ functions to see what's happening as a request is passed from function to function
* stepping _out_ when you no longer need to see what's happening in a particular function
* ...and stepping _past_ a particular function, without needing to look into its working at all

The green button is a fast-forward button, to take you to the next breakpoint you might have in the code, and the green power button is analogous to a power button, to refresh a connection to the debugger. You really, really should look into [this post here by Tim Sabat at Particle Tree][5], and this one here by [Matt Butcher, at TechnoSophos][6].

#### Debugging without MacGDBp

Of course, you don't need to use MacGDBp all the time, In most cases, just having a stack trace will help find the source of the error. Once you've got xdebug setup, you _should_ get a handy track trace whenever you throw an error - if not, be sure to make sure you have the display errors setting set to 'on' in your php.ini setting (it should be around line 370 in your file, normally):
<pre lang="ini">    display_errors = On</pre>
By the time you've followed these steps, you should have an easier to main installation of the LAMP stack, with a simple way to install extra PHP libraries and C extensions, a couple much more effective ways to debug than simply typing `echo $variable` everywhere, and an ideal environment to get on with hacking on Drupal, Wordpress and any other PHP code in future.

#### Phew!

This guide is largely a synthesis of earlier blog posts about this subject by [Justin Hileman][7], [Matt Butcher][6], [Tim Sabat][5], [Hunter Ford][2], and [Boris Gordon][1], I'd recommend subscribing to their blogs, as they _definitely_ know more about PHP than I do, and they're a great source of handy info.

If there's anything that isn't clear, please let me know, so I can improve this guide - I don't want anyone else to have to blunder through working out all this themselves in future, as working all this out has taken, far, far longer than I'd like, and well, it seems churlish not to share now that I've got a setup that seems fairly stable.

Now, time to actually do something useful with it...



[1]: http://boztek.net/blog/2009/10/07/install-lamp-stack-source-mac-os-x-106-snow-leopard-using-homebrew "Install LAMP stack from source on Mac OS X 10.6 Snow Leopard using Homebrew | boztek"
[2]: http://www.cupcakewithsprinkles.com/setting-up-apache-php-python-mysql-on-mac-os-x-snow-leopard-10-6/#comments "Setting Up Apache-PHP-Python-MySQL on Mac OS X Snow Leopard 10.6 |  Cupcake With Sprinkles"
[3]: http://aspn.activestate.com/ASPN/Downloads/Komodo/RemoteDebugging
[4]: http://www.bluestatic.org/software/macgdbp/help.php "MacGDBp - Help - Blue Static"
[5]: http://particletree.com/notebook/silence-the-echo-with-macgdbp/ "Particletree  » Silence The Echo with MacGDBp"
[6]: http://technosophos.com/content/debugging-your-php-code-xdebug-mamp-textmate-and-macgdbp-support "Debugging your PHP Code: XDebug on MAMP with TextMate and MacGDBp Support | TechnoSophos"
[7]: http://justinhileman.info/articles/building-a-lamp-development-environment-on-snow-leopard "Building a LAMP development environment on Snow Leopard | justin hileman dot info"
[ruby debugger]: http://railscasts.com/episodes/54-debugging-with-ruby-debug "Railscasts - Debugging with ruby-debug"
[pdb debugger]: http://aymanh.com/python-debugging-techniques "Python Debugging Techniques | Ayman Hourieh"
[MacGDBp]: http://www.bluestatic.org/software/macgdbp/ "MacGDBp - Blue Static"

