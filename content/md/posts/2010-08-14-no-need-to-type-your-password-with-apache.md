

{:author "admin", :title "There's no need to type your password when you restart Apache, really...", :date "2010-08-14 23:08:13", :publish-date "Sat, 14 Aug 2010 23:08:13 +0000"}



<!-- content below -->

When you're developing with PHP on a mac, if you're not using MAMP, you'll often end up having to do a lot of manual restarts when you make changes to how you've set up Apache (assuming you haven't joined all the cool kids and moved onto Nginx yet...). This usually involves calling up a terminal window and typing in the usual Apache restart command on OS X:

<pre lang='bash'>
  sudo apachectl restart
</pre>

This isn't a really destructive command, and having to type in your admin password every time when doing this in development on your own computer gets old quickly. It's also error prone. Surely there's a better way?

Fortunately, when browsing the [Aegir OS X install documentation][1], I came across as handy fix to this problem. The Aegir hackers let Aegir handle server restarts in a fairly elegant fashion, by tweaking the `sudoers` file on your mac, which is basically a short list of who is allowed to do what on your machine. I've borrowed a few tricks, and adaprted them to use in my sudoers file here, and after showing it in full, I'll explain how it works.

Bear in mind, you can't edit the `sudoers` file directly - you need to use the `visudo` command, (this works as a precaution to stop this file getting screwed up by letting more than one person is edit it at a time for example). 

Also, to make things more complex, you need to edit this inside the terminal, to you may need to force this by typing `EDITOR='vim'` first

Okay, now that's out the way, lets look at that file:

<pre lang='ssh' line='1'>
  # Run as alias specification

  # User privilege specification
  root    ALL=(ALL) ALL
  %admin  ALL=(ALL) ALL

  # Uncomment to allow people in group wheel to run all commands
  # %wheel        ALL=(ALL) ALL

  # Same thing without a password
  # %wheel        ALL=(ALL) NOPASSWD: ALL
  %staff          ALL=(ALL) NOPASSWD: /usr/sbin/apachectl
  # Samples
  # %users  ALL=/sbin/mount /cdrom,/sbin/umount /cdrom
  # %users  localhost=/sbin/shutdown -h now
  
</pre>

Lets look at the first lines, with `root` and `%wheel`. If you're even bothering to read this, the chances are you know that `root` refers to the all powerful user that can do anything on a system, but you may not be familiar with the percent prefix on `%admin` nor the `ALL=(ALL) ALL`. The `%admin` basically means 'anyone in the admin group, but the `ALL=(ALL) ALL` is somewhat more cryptic. The rough translation goes like this though: 

> from _ALL_ terminals, let these users run _ALL_ commands and as _ALL_ of the users in the system. 

We see the same trick visible again with the `%wheel` group, but the line starting with `%staff` deserves more attention:

<pre lang='ssh'>
  %staff          ALL=(ALL) NOPASSWD: /usr/sbin/apachectl
</pre>

Translated, this means:

> for ALL members in the _staff group_, let them use ALL terminals, to run the command `/usr/sbin/apachectl` as ALL users (in particular, the root user) without needing a password (that's the NOPASSWD: bit).

This is the line that lets us run the familiar `sudo apachectl restart` without needing to constantly type our password credentials in. 

Which over the course of a year, will easily save you tons of typing over the year, and leave some time to skim the [`sudoers` man page][2], and suggest a similar trick here for others to try.

Over to you now...


[1]: http://geoffhankerson.com/node/109
[2]: http://www.gratisoft.us/sudo/sudoers.man.html

