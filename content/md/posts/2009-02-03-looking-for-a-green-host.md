

{:author "admin", :title "Looking for a green host.", :date "2009-02-03 22:45:32", :publish-date "Tue, 03 Feb 2009 22:45:32 +0000"}



<!-- content below -->

<span style="color: #0000ee; -webkit-text-decorations-in-effect: underline; text-decoration: underline;"><a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/02/renewable-energy.jpg"><img class="alignnone size-full wp-image-102" title="renewable-energy" src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/02/renewable-energy.jpg" alt="renewable-energy" width="520" height="348" /></a></span>

For the last two weeks, I’ve been looking for a good reliable, green, well priced hosting company that offers virtual servers in or around the UK, and it’s been largely a fruitless, frustrating endeavor. But in order to really explain why I’m doing this in the first place, it helps to give a summary of what kinds of hosting is available.
<h3 id="a_brief_primer_on_web_hosting">A brief primer on web hosting</h3>
Up until fairly recently, there were two main kinds of web hosting you could buy to put a website on: shared hosting, or dedicated servers.
<h4 id="shared_hosting">Shared Hosting</h4>
If you have your own personal website, the chances pretty high that you’re running on shared hosting.

When you bought shared hosting, what you did was effectively rent space on a computer that had loads of user accounts sharing it like, in the same way you might have a few different user accounts on a laptop that multiple people share. It’s a pretty cheap way of having use of a computer, but is has a few drawbacks, namely:
<ul>
	<li><h4>You can’t treat it like your computer</h4>

If some arbitrary IT security policy put on a computer by someone else has stopped you doing something you want to on a computer, you’ll know how frustrating this can be. In the days of simple html, this wasn’t so much of a problem; you just put html on a server, and that was about it. When you wanted to update the site, you would pay someone to write new code.

However, it’s understandable to want to update your own website these days, and this frequently involves putting software on the server itself, like <a title="WordPress; Blog Tool and Publishing Platform" href="http://wordpress.org/">Wordpress</a> or <a title="drupal.org | Community plumbing" href="http://drupal.org/">Drupal</a>, which dynamically create html to feed to browsers. It’s common to bump up against limits to stop you using more than your fair share of the server’s processing power, which usually results in your programs being killed off halfway through doing something, or your users’ unable to do more processor intensive things like attach large files.

Also, if you’re looking to something slightly non-standard, like use a new web framework like Django or Ruby on Rails, these limits will stop you dead in your tracks.
</li>

<li><h4>Everyone on the server shares the same limited resources.</h4>
Conversely with shared hosting, when <em>some other</em> bright spark decides to something slightly non-standard, like use a new web framework like <a title="Django | The Web framework for perfectionists with deadlines" href="http://www.djangoproject.com/">Django</a> or <a title="Ruby on Rails" href="http://rubyonrails.org/">Ruby on Rails</a>, when they crash their program it can bring down your website too. Not great.

Finally, if your host crams too many people onto a single server you end up with a ridiculously slow website, because you’re all fighting over the same resources. You’ll often have this on hosting offers than seem ridiculously cheap.

Fees for shared hosting tend tend to correlate with how many people are being crammed onto each server, how much space is being offered, and what kind of bandwidth the sites use up, starting at less than a pound, and scaling upto around £25 per month. Companies know for bring shared hosting providers are <a title="DreamHost Web Hosting" href="http://dreamhost.com">Dreamhost</a>,  <a title="1and1 Internet Ltd " href="http://1and1.co.uk">1and1.co.uk</a>, <a title="Web Hosting - Web Hosting Company UK - Fasthosts" href="http://fasthosts.co.uk">http://fasthosts.co.uk</a>
</li>
</ul>

<h4 id="dedicated_servers">Dedicated Servers</h4>
Dedicated, or private servers are servers that are totally dedicated for your use alone.

As you’d expect, they carry none of the problems that sharing have, but they’re usually much more expensive, and in many cases a pretty wasteful way of hosting a site unless you really need one. If you need one of these, you either can afford to pay someone to look after it for you, or you’ve been ripped off, or your website is so successful that there is nothing I could tell you that you don’t already know.

Prices for these start range from around £60, upwards.
<h4 id="the_third_way_the_wonders_of_the_vps">The third way - the wonders of the VPS</h4>
In the last few years, companies like <a title="Slicehost - VPS Hosting" href="http://www.slicehost.com/">Slicehost</a> and <a title="Linode.com - Xen VPS Hosting" href="http://www.linode.com/">Linode</a> have made a name form themselves by specialising in offering virtual private servers to customers. In a nutshell, a virtual private server offers you the benefits of control, and predictability of a dedicated server, but at a cost much closer to that of shared hosting.

When you rent a virtual private server, you share a physical server like with shared hosting, but each virtual machine runs in it’s own isolated sandbox, to stop what everyone gets upto on their machines affecting each other. This has a few advantages:
<ul>
	<li><h4>Predictability</h4>
That sandbox gives a reassuring degree of reliability, and fair minimum expectation of performance. Someone else being dugg or slasheddotted won’t affect your site.</li>
	<li><h4>Control</h4>
Because you have control over your environment, running slightly more exotic software like Rails or Django, or using a source control system like <a title="Git - Fast Version Control System" href="http://git-scm.com/">Git</a>, is much much simpler. While these can sometimes be done with shared hosting, any long running processes that might run in the background will usually be killed off on shared hosting.</li>
	<li><h4>Elasticity</h4>
Virtual machines are no longer physical machines, but simply digital containers talking to hardware in an abstract sense, they take on a protean nature, that means they can be copied, resized, backed up and generally fiddled with in ways that you can’t with physical machines. If your site gets popular, you can resize the the server to make it respond to increased demand, and conversely, in a datacentre full of virtual machines, throttling back energy usage when demand drops is also possible.</li>
	<li><h4>Portability</h4>
The same qualities that make virtual machines elastic, also make them portable, and this has me really interested right now; it helps with testing, as you can have a container on your local machine, but also helps safeguard against being locked into one hosting company if you’re not happy with what they offer and makes it easier to move hosts more easily. This makes it possible to allow website owners to choose hosts based on factors like customer service, or how sustainably they are run, rather than worrying about if they’ll install the right version of Perl for you.</li>
</ul>
The starting rate virtual machines is around the £15 mark, scaling up depending on how much power you need.
<h4 id="back_to_the_point_where_are_the_reliable_green_virtual_private_servers">Back to the point - where are the reliable green virtual private servers?</h4>
This post should have worked as halfway decent primer for explaining why virtual private servers are so desirable. In the next post, I’ll build on this to share the results of my trying to find a good green virtual hosting company in the UK, as I know I’m not the only one who’s looking around for this.

