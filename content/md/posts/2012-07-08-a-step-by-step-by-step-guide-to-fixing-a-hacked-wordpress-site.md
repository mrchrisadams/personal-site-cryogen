

{:author "admin", :title "A step by step by step guide to fixing a hacked wordpress site", :date "2012-07-08 23:01:27", :publish-date "Sun, 08 Jul 2012 23:01:27 +0000"}



<!-- content below -->

I had to do a bit of server-side troubleshooting on Wordpress site recently, that had been hacked. It's not a popular site, and hardly gets any traffic, and was simple enough to fix, but it's worth noting the actions I had to take.

I'm trying to find a mental model that fits this process, to make it easier to remember what to do in future, so I figured I'd share my approach here:

### 1) Stop the bleeding 

In this case, the hack had been down to a malicious script being able to sign into the site, using the `admin` credentials, and a dictionary-attacking the password until the weak password was broken. A simple fix for this is to change the password to something stronger, and be change the name of the admin account, so it's no longer such a target for scripts.

Changing the password for an user account is pretty mundane, but changing the name of a user account is slightly more exotic.

Here's a handy mysql snippet for this, once you're logged in at the mysql shell:

<pre lang="sql">
    update wp_users set user_nicename='new.harder.to.hack.name' where user_nicename='admin';
    update wp_users set user_login='new.harder.to.hack.name' where user_login='admin';
</pre>

### 2) Clean the infection

Now you have this, it's worth looking for the culprit. In many cases, you'll see an unfamiliar php file in the `uploads` directory. It'll often have a url like this: `img_112.php`, and you might be able to see it in server logs as a request like this:

<pre>
    http://hackedsite.co.uk/wp-content/img_112.php?SOMESTRING_OF_PARAMETERS_
</pre>

Unless you have very good reasons to have executable php files in your upload diretories, it's best to remove any.
  
### 3) Keep it clean

Now that you've stopped further attacks, and removed any malicious scripts from within your site, it's a good time to lock down permissions on any files on your site. If you're running Wordpress under a virtual private server, the snippet below should work fine, if you run them from within the `wordpress directory`:

<pre lang="bash">
  find /path/to/your/wordpress/install/ -type f -exec chmod 644 {} \;
</pre>

If you're like me and can never remember the syntax for the `find` command, here's a sort of translation of what it means:

> starting within the directory "/path/to/your/wordpress/install/", start a *find*, looking only for results of the type file (shown by `-type f`). Then, for each result, execute the command (using the `-exec` flag) `chmod 644` on them, to restrict how the files can be modified on the server. 

Now that we've done files, we'll need to to the directories too:

<pre lang="bash">
  find /path/to/your/wordpress/install/ -type d -exec chmod 755 {} \;
</pre>

This is almost the same as the previous command except that a) we're only looking for directories (specified by the `-type d` flag), and we're allowing slightly more relaxed permissions, because we're dealing with directories instead files  (`chmod 755` versus `chmod 644`).

Once we've cleaned up permissions on our site, now we can turn to some plugins to help automate some of the drudgework of keeping a site sufficiently secure. I've found [WordPress File Monitor Plus][1] useful for detecting malicious changes to your site in future, and if you can see past the rather bombastic name, [Ultimate Security Checker][2], gives a number of simple steps you can follow to further harden up your site.

#### Is this even vaguely coherent? 

So there we have it - (hopefully) a simple enough explanation of how you might fix a site after it's been compromised by some opportunist or semi automated hacking scripts, and a useful way to to think about site in future.

#### Where to learn more

If you're interested in looking into this in more detail, right now this presentation below seems to the best one I can find about the subject. And as ever, [the Codex][3] is wealth of useful information

[embed]http://www.slideshare.net/williamsba/wordpress-security-1709496[/embed]

<!-- links -->

[1]: http://l3rady.com/projects/wordpress-file-monitor-plus/
[2]: (http://wordpress.org/extend/plugins/ultimate-security-checker/ "WordPress - Ultimate Security Checker WordPress - Plugins")
[3]: http://codex.wordpress.org/Hardening_WordPress

