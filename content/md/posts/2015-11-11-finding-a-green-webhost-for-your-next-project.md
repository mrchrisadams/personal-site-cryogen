

{:author "admin", :title "Finding a green webhost for your next project", :date "2015-11-11 10:44:28", :publish-date "Wed, 11 Nov 2015 10:44:28 +0000"}



<!-- content below -->

<em>I've had a few people ask me online about the cleanest host for running your services online is. My recommendations are below.</em>

I should start first saying that like most questions related to quantifying CO2 emissions, the more you look into it, the complexity you uncover.

As such, the recommendations below will be incomplete, but if you're in the UK, they're at least some starting point. I'm looking for people who would be up for compiling a guide for this:

<strong>If you want to keep data inside the UK - use Memset</strong>

Memset have been banging the low CO2 emissions computing drum for a while now since 2006 at least, and are priced fairly competitively with other UK providers.
<ul>
	<li>Memset and their green credentials: <a href="http://www.memset.com/about-us/green-it/">http://www.memset.com/about-us/green-it/</a></li>
	<li>Memset's products and pricing: <a href="http://www.memset.com/solutions/">http://www.memset.com/solutions/</a></li>
	<li>Their CEO writes about this <a href="https://www.katescomment.com/category/environment/">semi-regularly about the subject</a> with some actual figures for energy use of servers and so on: <a href="https://www.katescomment.com/category/environment/">https://www.katescomment.com/category/environment/</a></li>
</ul>
<em>I use them for my personal hosting, and I've used them for client hosting before.</em>

<strong>If you want to use Amazons's Web services and stay in the Europe - use AWS Frankfurt</strong>
<blockquote>"Jeff Bezos is the internet's ultimate apex predator"</blockquote>
If you're expecting run a business with any kind of online component, you ignore Amazon at your peril, because the chances are high that they already carry out some processes that are part of your business model better and more cheaply than you, and they will destroy you if you try to compete with them on this front.

Fortunately, Amazon Web Services, offer a dizzying, and confusingly named range of these processes as services now  so you can pay them to take care of those parts, so you can focus on the parts that differentiate your offering.

For example, rather than being responsible for the management of a database for your data, you can use a hosted version like  Amazon's Relational Database Service (RDS) so you're not the one having to fix servers at 4am when something breaks, or their search engine service, so you're not managing a cluster or search servers yourself.

AWS's carbon footprint has traditionally been somewhat murky, with them being avid consumers of coal in north Virginia.

If you're in Europe, the new Frankfurt Data centre in Germany is apparently Carbon neutral, keeps your data inside the EU, and means you have access to many of the web services that you might rely on for a competitive advantage. Outside Europe,  AWS in North America's western region is based in Oregon, which relies on hydro power much more than coal, so using them is a good compromise.

<em>I'm increasingly using the Frankfurt Datacentre for client work, because AWS's services and libraries are so good.</em>
<ul>
	<li>Amazons's AWS sustainability pages - <a href="https://aws.amazon.com/about-aws/sustainable-energy/">https://aws.amazon.com/about-aws/sustainable-energy</a></li>
	<li>Amazon's AWS dizzying range of products - <a href="https://aws.amazon.com">https://aws.amazon.com</a></li>
	<li>AWS's product named translated into plain english - <a href="https://www.expeditedssl.com/aws-in-plain-english">https://www.expeditedssl.com/aws-in-plain-english</a></li>
</ul>
<strong>If you want to a greener cloud provider, you use some web services, but you're not so bothered about keeping inside Europe - use Google Cloud Platform
</strong>

Google have been long time leaders when it comes to the greening of cloud computing, and they have an increasingly wide range of web services that mean you're not managing your own search engines and so on if you use them.

However due to the way their networks work, I'm not sure if there's a away to ensure that data stored with them is kept inside the EU, which may make them unsuitable for your project.

<em>I've been using them for providing the compute and storage parts of a few projects,and some of kicking the tyres of their other services. If they offered a hosted PostGresSQL service, I would recommend them more highly, but otherwise I'm pretty happy with them.</em>
<ul>
	<li>Google Sustainability pages: <a href="https://www.google.com/green/bigpicture/">https://www.google.com/green/bigpicture/</a></li>
	<li>Google Cloud Platform products: <a href="https://cloud.google.com/">https://cloud.google.com/</a></li>
</ul>
<strong>Others?</strong>

I just dashed this post out now, in response to a tweet this so there are obviously glaring emissions. I'd like to find other people interested in this subject. - if you run a service, or use one, please leave a comment, and I'll update this post.

I intend to put together a free online guide about this subject, which some more structured justification of choosing one provider over another in the near future.

&nbsp;

