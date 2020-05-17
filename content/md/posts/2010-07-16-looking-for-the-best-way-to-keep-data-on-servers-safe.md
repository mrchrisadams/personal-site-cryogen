

{:author "admin", :title "Looking for the best way to keep data on servers safe", :date "2010-07-16 23:33:42", :publish-date "Fri, 16 Jul 2010 23:33:42 +0000"}



<!-- content below -->

We know we should all be doing it, but most of us don't do it enough.

I put out a request today to my followers Twitter asking this question:

I've had the following services recommended to me by a number of fellow developers whose opinions I have a lot of respect for:

A couple of ex-Headshifters pointed me to [Duplicity][], a free tool that also looks very promising. Using it looks pretty straight forward.

<pre lang="bash">
    duplicity /home/my_directory scp://backup@other.host//usr/backup    
</pre>

A variant of it can be used to backup to Amazon S3 too, and [there's a helpful blog post to show how to do this here][1], if you use Ubuntu or OSX.

[Kalv][] recommended [Safe][], a clever Ruby gem by the Astrails crew that was originally designed to automate the backing up of Rails projects in a simple fashion.

One service that looks really interesting is though is Tarsnap, as recommended by [Jon Gilbrath][]. It's similarly simple to use, but takes care of the some of the more awkwards backup issues, and saves you having to setup your own S3 account.

<pre lang="bash">
  # Create an archive named "mybackup" containing /usr/home and /other/stuff:
  tarsnap -c -f mybackup /usr/home /other/stuff
</pre>

The developer, Colin Percival also has written quite extensively [about how it works on his own blog][2] - he's only making a few cents per gigabyte on providing this service for people, yet it still looks to be something viable for him to run - amazing.

It looks like it's almost exactly what I'm after - the only thing missing is the option to back up storage inside the EU. This requirement is mainly one coming from data protection concerns from previous clients, because rules for processing data and storing in in the EU are different to that in the US, but given the strength of encryption, I'm not sure how much of an issue this really is, these days.

I'd really appreciate some light shed on this actually - technology is moving so much faster than law these days, it's frustrating not being able to take advantage of these kinds of services.

Anyway that's what I've found. What do you use, and why?

[Duplicity]: http://duplicity.nongnu.org/ "duplicity: Main"
[Kalv]: http://twitter.com/kalv/status/18672139356
[Tarsnap]: http://www.tarsnap.com/index.html
[Safe]: [http://github.com/astrails/safe] "astrails's safe at master - GitHub"
[1]: http://blog.damontimm.com/how-to-automated-secure-encrypted-incremental-backups-amazon-s3-duplicity-os-x-or-ubuntu "How To: Automated Encrypted Incremental Backups on Amazon S3 with Duplicity (OS X or Ubuntu) &laquo;  damontimm.com"
[2]: http://www.daemonology.net/blog/2008-12-14-how-tarsnap-uses-aws.html "How Tarsnap uses Amazon Web Services"

