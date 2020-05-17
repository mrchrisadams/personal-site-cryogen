

{:author "admin", :title "How to fix a Wordpress site when the database corrupts on you.", :date "2010-05-16 23:43:47", :publish-date "Sun, 16 May 2010 23:43:47 +0000"}



<!-- content below -->

Phew!

... and as soon as I say this, the database powering this site corrupts on me - charming!

For one awful moment I thought I had lost everything (I hadn't set up a regular mysql backup task for this blog), but thankfully, bringing this blog back from the dead was surprisingly straight forward.

Here's what happened, and what I did to fix it.

Yesterday when writing a post about how there's a mobile missing tariff that should exist but doesn't, when I posted, [Wordpress](http://wordpress.org "WordPress &#8250; Blog Tool and Publishing Platform") would accept my post; those pretty git spinners just kept spinning on the text page.

I didn't think too much of it, at the time, as I was heading out to meet James to work on some top sekrit project, based around [node.js](http://nodejs.org/ "node.js"), [mongodb](http://www.mongodb.org/ "MongoDB"), and doing something strange yet hopefully useful with wifi, so I just saved it locally on my mac, and headed out on my bike.

This evening though, I tried again, and I had the same error. "Ah," I thought, "maybe I just need to restart the database on this box - it's been going for ages anyway". So I ssh'd into the server running the system, and called the usual [CentOS](http://centos.org/ "www.centos.org - The Community ENTerprise Operating System") restart command

<pre lang="bash">
  service mysql restart
</pre>

This took nearly two minutes to stop, then spat out this response when restarting:

<pre lang="bash">
[chris@stemcaa2 ~]# service mysql restart
Shutting down MySQL........................................[  OK  ].......
Starting MySQL.........................................................................................................................................................................................................................................../sbin/service: line 66: 27651 Terminated              env -i LANG="$LANG" PATH="$PATH" TERM="$TERM" "${SERVICEDIR}/${SERVICE}" ${OPTIONS}
</pre>

Okay, slight panic now - lets check the disk, to see if there's space for the database to write, with `df -h`

<pre lang="bash">

[chris@stemcaa2 ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda1             9.9G  9.4G     0 100% /
tmpfs                 129M     0  129M   0% /dev/shm
/usr/tmpDSK           485M   11M  449M   3% /tmp

</pre>

Ah, that's not good. Disk space is like oxygen for servers, and without it, things break quickly.

The quickest way to make some breathing space fast is to clear the `yum` cache, like so:

<pre lang="bash">
yum clean headers packages
</pre>

Okay, lets try restart again:

<pre lang="bash">
[chris@stemcaa2 ~]# service mysql restart
Shutting down MySQL.                                       [  OK  ]
Starting MySQL.                                            [  OK  ]
</pre>

Sweet! It worked! But hang on... now wordpress isn't showing any posts! This _really_ isn't good.

So lets check the database;

<pre lang="mysql">
[root@stemcaa2 ~]# mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 5.0.90-community MySQL Community Edition (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema | 
| antia_wordpress    | 
| chris_wordpress    | 
| cphulkd            | 
| deadonim_wordpress | 
| dov_wordpress      | 
| eximstats          | 
| horde              | 
| leechprotect       | 
| modsec             | 
| mysql              | 
| roundcube          | 
+--------------------+
12 rows in set (0.16 sec)

</pre>


Okay the database is there. What about the tables though?

<pre lang="mysql">

Database changed
mysql> show tables;
+---------------------------+
| Tables_in_chris_wordpress |
+---------------------------+
| wp_ak_twitter             | 
| wp_commentmeta            | 
| wp_comments               | 
| wp_links                  | 
| wp_options                | 
| wp_postmeta               | 
| wp_posts                  | 
| wp_term_relationships     | 
| wp_term_taxonomy          | 
| wp_terms                  | 
| wp_usermeta               | 
| wp_users                  | 
+---------------------------+
12 rows in set (0.00 sec)

</pre>

Hmm.. they're there too. Maybe the tables?

<pre lang="mysql">

mysql> select * from wp_posts
    -> ;
ERROR 145 (HY000): Table './chris_wordpress/wp_posts' is marked as crashed and should be repaired

</pre>

*Uh-oh.* I think this is going to be ugly. And yet...

### The magic fix

...a quick check here on google gleaned the fix - MySQL's got a tool for just this occasion, and you call it like  `mysqlcheck broken_database` from the command line:

<pre lang="mysql">
[root@stemcaa2 ~]# mysqlcheck chris_wordpress
chris_wordpress.wp_ak_twitter                      OK
chris_wordpress.wp_commentmeta                     OK
chris_wordpress.wp_comments                        OK
chris_wordpress.wp_links                           OK
chris_wordpress.wp_options                         OK
chris_wordpress.wp_postmeta                        OK
chris_wordpress.wp_posts
warning  : Table is marked as crashed
error    : Size of datafile is: 745472         Should be: 745692
error    : Corrupt
chris_wordpress.wp_term_relationships              OK
chris_wordpress.wp_term_taxonomy                   OK
chris_wordpress.wp_terms                           OK
chris_wordpress.wp_usermeta                        OK
chris_wordpress.wp_users                           OK

</pre>
The fix was trivial from here - just pass in an `auto-repair` flag:

<pre lang="mysql">

[root@stemcaa2 ~]# mysqlcheck chris_wordpress --auto-repair
chris_wordpress.wp_ak_twitter                      OK
chris_wordpress.wp_commentmeta                     OK
chris_wordpress.wp_comments                        OK
chris_wordpress.wp_links                           OK
chris_wordpress.wp_options                         OK
chris_wordpress.wp_postmeta                        OK
chris_wordpress.wp_posts
warning  : Table is marked as crashed
error    : Size of datafile is: 745472         Should be: 745692
error    : Corrupt
chris_wordpress.wp_term_relationships              OK
chris_wordpress.wp_term_taxonomy                   OK
chris_wordpress.wp_terms                           OK
chris_wordpress.wp_usermeta                        OK
chris_wordpress.wp_users                           OK

Repairing tables
chris_wordpress.wp_posts
info     : Found block that points outside data file at 742932
status   : OK

</pre>

And then all was well again! Why can't technology always be this easy to fix?  A huge, huge heartfelt thanks goes to [Felipe Cruz](http://www.felipecruz.com/ "Felipe's Blog - Technology Articles &amp; know how") for adding [such simple instructions on his site](http://www.felipecruz.com/repair-mysql-database.php "Ways to repair MYSQL Databases") explaining how to use that insanely handy `mysqlcheck` command.

<!-- links -->
[Wordpress]: http://wordpress.org


