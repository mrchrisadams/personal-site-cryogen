

{:author "admin", :title "There is life after the cloud", :date "2009-01-02 12:27:03", :publish-date "Fri, 02 Jan 2009 12:27:03 +0000"}



<!-- content below -->

This post is partly a reaction to getting slightly sick of the phrase '<a title="wikipedia cloud computing" href="http://en.wikipedia.org/wiki/Cloud_computing">cloud computing</a>' over the last few months.

I don't think that 'the cloud' is the be all and end all of computing, and I think there's some fascinating stuff happening at the edges of IT right now that shows the beginning of  swing back away from the idea of centralised computing as the best way to do IT.

If you look at the history of computing from halfway through the twentieth century to where we are now, you'll see evidence of an interesting oscillation between centralisation and decentralisation as a way to solve problems with computers.

In the 60's and 70's and computing was carried out, on huge centralised mainframes, whose processing cycles were shared by groups of users, using relatively simple terminals.

Through the 80's and 90's, the increasing power of computing at the edges of the network gave rise to prominence of the desktop PC, and the network became less important, relatively speaking.

Where computers were networked outside of academia, the most popular commonly used collaboration and groupware tools were properietary, and usually sold with accompanying hardware; the easiest example here is Microsoft Office's success on the desktop parlaying into the ubiquity of Microsoft Exchange for email, calendar sharing, sharing files, which in turn drove further sales of Office's suite and Windows licenses. Here the desktop is king, and any concessions to the existence of the internet are occurring terms that don't disrupt the continued dominance of the selling hardware and shrinkwrapped software.  

With the end of the nineties and the turn of the century however, the pendulum has started to swung back to centralisation, and as more and more computers have came online, more and more tasks are being performed through the web on centralised servers. You could argue we're at the apogee of this stage with the rise of cloud computing, where virtualised servers, instantiated on demand, are replacing the clusters of servers bought that and maintained in-house.

These virtualised servers exist physically in huge, energy guzzling datacentres aroudn the globe, in an echo of the centralisation of the early days of computing, though it's arrived late to the party, even Microsoft has an offering in this space, in the form of <a href="http://news.bbc.co.uk/1/hi/technology/7693993.stm">Azure</a>.

I think in 2009 though, we're going to see the pendulum start to slowly swing back towards decentralisation again, as the experience and utility we get from centralised services like Google Docs, Youtube, Twitter and Facebook, can be delivered by a system of federated websites and webservices, that don't assume a constant connection to the net, in order to function.

<strong>Evidence?</strong>

I'm saying this based on the trends that emerged in the tools that are being used to make the web now, compared to those a couple of years back. 

<strong>Subversion vs. Git</strong>

<a title="subversion" href="http://subversion.tigris.org/">Subversion</a> is a really powerful version control system that uses a centralised repository of changes that everyone working on a project subscribes to. There's all kinds of clever logic in place that helps merge changes from disparate users, and let people branch off their development to try out new approaches to solving computing problems with code. But as soon as you lose your connection to the internet, it's severely crippled; you lose the ability to make incremental changes, branch off new versions of code for experimentation. <a title="Git" href="http://git.or.cz/">Git</a> by comparison is another tool used to help manage source code, but has a few other advantages, like being designed with decentralisation in mind; this means that even if your umbilical to the central server managing the master copy of all changes  to the code is severed, you can still keep working and enjoy the safety net of version control, branching off code in new directions, and get back in sync once you do have a connection to the net again.

<strong>Twitter vs. Identica</strong>

<a title="Twitter" href="http://twitter.com">Twitter</a> is a centralised service that lets people update their friends and followers with a stream of microcontent through the course of the day. Managing this centrally is a huge technical challenge, and users have now become familiar with the failwhale, an arresting little illo often displayed on the twitter page when servers are overloaded. <a title="Identica" href="http://identi.ca/">Identica</a> is a federated approach to microcontent blogging, that doesn't try to manage everything centrally, but breaks down the problem into smaller chunks, with a particular identica server only managing a subset of the problem, and leaving the areas that don't immediately concern it to being someone else's problem. If part of the network goes down, your server will keep going, and until the health of the network is restored again.

<strong>Microsoft Passport vs. OpenID</strong>

Managing usernames and passwords is not something that humans naturally do well. Despite our best intentions, we normally either end up using the same password across many, many sites at once (which means if we lose one passwords, we're compromised everywhere), or simply forget our passwords all the time and end up having to jump through hoops all day long to do anything useful. One solution put forward by Microsoft to solve this was the <a title="Joel Spolsky on Passport" href="http://www.joelonsoftware.com/articles/fog0000000047.html">Microsoft Passport</a>; in short, your hotmail login would become your login to every supporting site under the sun. While this would have been convenient for end users, this was problematic on many, many levels as Microsoft's habit of abusing monopolies understandably made users and site owners uncomfortable with this idea.

<a title="37 signals on Open ID" href="http://www.37signals.com/openid/">OpenID</a> is designed to offer many of the same advantages of using a single username and password to sign into lots of sites, without as many security problems inherent with a centralised service like passport, by placing you as a user, in greater control of how your identity is managed, right up to the point that much like running a blog on your server, you can run your own openid server, precluding you from relying on a third party to grant or deny access to a site.

<strong>Blogger vs Wordpress</strong>

<a title="blogger" href="http://www.blogger.com/home">Blogger</a> is a centralised service for blogging. It works fine mostly, but if you want to change how it works, or you're not happy with all of it, there's not much you can do. Wordpress is a available as a hosted service on <a title="Wordpress.com" href="http://wordpress.com">wordpress.com</a>, but it also can be downloaded from <a title="Wordpress.org" href="http://wordpress.org">wordpress.org</a>, and setup on your own server, and modified as you see fit. If the central server stops, you can keep blogging on your own instance of Wordpress regardless.

<strong>MySQL - CouchDB
</strong>

<a title="MySQL" href="http://mysql.com">MySQL</a> might be a strange example here for centralisation versus deentralisation, as it's the database that drives many a open source app. Ultimately though, it's designed to be one big database, with one unique key per database than a network of databases loosely linked. Making it act like a federation of silos takes a lot of work to shard off databases and still keep performance reasonably high. <a title="CouchDB" href="http://couchdb.com">CouchDB</a> by comparison is designed to be replicated in many disparate places, and has a simiarly laid back approach to how data should be structured compared to an SQL styled database; rather than having one canonical app using one database, CouchDB looks like it's designed to allow multiple apps with multiple databases to share data very well without data conflicts. This is something that's much, much harder than it sounds.

<strong>Swinging back, or something totally different?</strong>

I'm painting with very broad strokes here in this description, but what I'm hoping to show here is that over the coming year, we're likely to see some of this trend towards decentralisation, and in particular federation, in the web.

