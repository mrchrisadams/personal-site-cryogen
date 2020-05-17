

{:author "admin", :title "The quickest way into Wordpress when you're locked out.", :date "2010-06-09 13:39:55", :publish-date "Wed, 09 Jun 2010 13:39:55 +0000"}



<!-- content below -->

I love Wordpress as a platform for building sites.

But no matter how many times I see it, I don't think I'll ever get used to having this snippet available to me if I get locked out of a Wordpress install :

<pre lang="php">
  <?php wp_set_password('new_admin_password',1); 
// this changes the password for user with an id of 1 (i.e. the admin)  ?>
</pre>

Surely it shouldn't be that easy to get root on a Wordpress site?

Ladies and gentlemen, _this_ is why you should always sequester access on a database, so each app has it's own db user. If a charmless bad guy DOES gain access, they can only reck _one_ Wordpress site database, _not all of them_.

