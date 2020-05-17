

{:author "admin", :title "Looking for a green host - concluding the search", :date "2009-07-08 10:34:52", :publish-date "Wed, 08 Jul 2009 10:34:52 +0000"}



<!-- content below -->

I think I can finally stop searching for a decent green host who does virtual servers,now that I've found <a title="Memset" href="http://memset.com">Memset</a>.

I was after a host based in the EU, who specialised in virtual servers, had experience with open source software, were environmentally sound, and affordable - I've gone the why's of this in more detail in previous posts.

This post will outline how why I ended up choosing Memset, and list a few other honourable mentions from other companies who might also fit the bill if you're looking for similar things to me in hosting.

<strong>They're based in the UK</strong>

Having servers in the UK generally takes an element of uncertainty out of hosting - and while I'm hardly going to drive all the way down to Reading to look at a couple of boxes, seeing an accolade from a UK publication about their service carries much more weight with me than one from a US mag I've never heard of.

<strong>They do virtual machines and they've been doing it for long time:</strong>

Memset have been doing VM's since before it became cool, and their choice of Xen, an open source platform for the virtualisation, ticks the opensource geek tickbox for me.

<strong>They're affordable </strong>

Of the companies, in the UK, Memset seemed to offer the best combination of price and service I could find. In fact their new pricing even looks aggresive when you compare them to US based operators like <a href="http://www.linode.com/">Linode</a> and <a title="Slicehost" href="http://www.slicehost.com/">Slicehost</a>. £9.99 for a VPS with 512mb of ram (the main resource I'm interested in) is extremely respectable, and when I did need to upgrade ram on a VPS recently they did it in about 15 minutes after me asking them.

<strong>They're about as green as I could find in the UK</strong>

They don't use renewable energy to power their data centres, but apparently this is down to there not actually being enough in the UK to meet demand at all - I put out a few emails asking around, and was contacted directly by the <a title="Kate Craig Wood's blog" href="http://www.katescomment.com/">Kate Craig-Wood</a>, the Memset MD, who provided me with detailed answers to the questions I had. She explained her reasons for choosing conventional energy, telling me that hosting providers in the UK that claim they use renewable will only end up sourcing a fraction of their power from these sources.

This seems in keeping with what I could find myself - the only place in the UK that I could find that runs on renewable power offers virtual private servers is Smartbunker, who've stopped offering VPS's to concentrate on bigger clients instead.

So if you can't run on renewable energy, you can at least go for efficiency, and that's what they've been done. At the moment, a widely accepted figure for measuring datacentre efficiency is <a title="Definition of PUE" href="http://searchdatacenter.techtarget.com/sDefinition/0,,sid80_gci1307933,00.html">PUE - Power Usage Effectiveness</a>, and is measured by comparing the power being going into a datacentre to how much is used by the computers themselves. The closer to one this figure gets the better.

If you have a PUE of 2 for example for every watt used by the computers, another watt is spent on keeping the data centre cool and power going to the servers themselves. <a href="http://www.google.com/corporate/green/datacenters/measuring.html">Google's own pages </a>cite a PUE of 1.9 as the direction that most datacentres are heading towards for 2011, although they're already way ahead of this with figures of 1.1-1.4 as their average. 

Memset tell me they hit a PUE of around 1.3, and they offset any emissions left over through the <a title="The Carbon Neutral Company" href="http://www.carbonneutral.com/">carbon neutral company</a>, one of largest, most well known (and also one of the most expensive) companies selling offsets.

<strong>Other options</strong> 

Two other UK based hosts who look interesting if you're after UK virtual private servers are <a title="Bytemark" href="http://www.bytemark.co.uk/">Bytemark</a> and <a href="http://www.brightbox.co.uk/">Brightbox</a>. Both are more expensive; with Brightbox you're partly paying for their staff's expertise with Rails, and the fact that they integrate tightly with <a href="http://www.fiveruns.com/">FiveRuns</a>, a monitoring tool to help you see where the performance bottlenecks are in your apps. They also offset the their companies carbon with ClimateCare, another UK company.

Bytemark is the host I used before Memset. They've been extremely attentive to any requests I've had, and were able to answer all the questions I had about their datacentres, other than bizarrely their PUE. They're also well known for being friendly to open source development. I'd happily recommend them as an alternative to Memset if you're not crazy about storing all your eggs in one basket.

