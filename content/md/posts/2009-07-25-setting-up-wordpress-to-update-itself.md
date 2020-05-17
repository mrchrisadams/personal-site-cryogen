

{:author "admin", :title "Setting up wordpress to update itself", :date "2009-07-25 21:06:31", :publish-date "Sat, 25 Jul 2009 21:06:31 +0000"}



<!-- content below -->

Wordpress's auto update feature is incredibly handy.

However, not every webhost automatically has accounts setup to allow for this, and if click the promising looking auto-upgrade icon, you'll often be face with this screen here:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/07/Wordpress-auto-upload-fail-.jpg"><img class="alignnone size-medium wp-image-179" title="Wordpress - auto-upload fail" src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/07/Wordpress-auto-upload-fail--300x202.jpg" alt="Wordpress - auto-upload fail" width="300" height="202" /></a>

You get this screen when the folder containing wordpress belongs to the user, instead of the apache daemon; this is normally either <code>www-data</code> if you're using Ubuntu, or <code>nobody</code> if you're using Redhat Linux instead.

The simplest way to do this is to change the folders to be owned by the apache daemon instead, by using <code>chmod</code> like so:
<pre><code>
chown -R nobody wordpress
</code></pre>
Adding the <code>-R</code> flag makes the changing of ownership recursive through all the folders inside wordpress.

Job done.

This is outlined in more detail by <a title="Rob Spender on Wordpress permissions" href="http://robspencer.net/auto-update-wordpress-without-ftp/">Rob Spencer</a> on his own blog - really quite handy.

