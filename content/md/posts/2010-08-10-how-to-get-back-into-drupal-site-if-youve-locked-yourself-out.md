

{:author "admin", :title "How to get back into Drupal site if you've locked yourself out", :date "2010-08-10 23:35:29", :publish-date "Tue, 10 Aug 2010 23:35:29 +0000"}



<!-- content below -->

A few posts back, I shared a one liner to get you back into a Wordpress site if you manage to lock yourself out, and forget your database password.

Assuming you've access to the command line and drush, you can pull a similar trick with Drupal, by typing the following query in:

<pre lang='bash'>
    drush sql-query "update users set pass=md5('NEWPASSWORD') where uid = 1;"
</pre>

### What's happening here?

The first thing we're doing is calling drush sql-query, a sub-command of drush.

If you haven't used Drush yet, you really, really should. It totally transforms how you work with Drupal, by making the kinds of tasks you had to do manually through the website possible from a commandline, which means yes, you can get up to all kinds of handy scripting shenanigans.

As you might expect drush sql-query lets you pass a single arbitrary query to the database described in your site's settings file, without you needing to fish the credentials out yourself. Here's our query too now:

<pre lang='mysql'>
 update users set pass=md5('NEWPASSWORD') where uid = 1;  
</pre>

In short, we're _updating_ the _users_ table in the Drupal database, by _setting_ the _pass_word value for the the first user id (_where uid=1_), to a _md5 hash_ of the phrase _NEWPASSWORD_.

If you don't haves access to drush, nor the command line, but you still can change a file over SFTP, you can to the same by adding a snippet like this on to the site:

<pre lang='php'>
  $doh_forgot_my_password = db_query("update users set pass=md5('NEWPASSWORD') where uid = 1;");
</pre>

Of course you really should be paramaterizing this like so:

<pre lang='php'>
  $doh_forgot_my_password = db_query("update users set pass=md5('%s') where uid = %d;", array("NEWPASSWORD", "1") );
</pre>

But this given the fact that this snippet should only existing in a template for 15-20 seconds _at the most_ you'd probably be forgiven for taking the short cut...

