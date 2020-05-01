

{:author "mrchrisadams", :title "Writing up IotMark, part 2 of 2", :date "2018-03-13 14:14:22", :publish-date "Tue, 13 Mar 2018 14:14:22 +0000"}



<!-- content below -->

<em>I said on twitter that I'd do a write up of the Friday IoTMark workshop last week:</em>

https://twitter.com/mrchrisadams/status/972009776518381569

<em>I've had enough people fave it to give me a reason to write it, but over the weekend, I realised that giving context and backstory to the event took up more than 1500 words already. I've <a href="http://blog.chrisadams.me.uk/2018/03/13/writing-up-iotmark-like-i-said-i-would/">split that out into a separate post</a>,</em> so here's how the day went down and the key things I learned.

<h4>Much less than 60 people this time around</h4>

Previous events have been relatively large affairs, taking over entire venues, with breakout rooms, and culminating in a somewhat chaotic mob-editing of a google doc, to come up with either a bill of rights style document, or some kind of spec or set of principles to inform the creation of a certification mark for connected products.

https://twitter.com/mrchrisadams/status/214382405778276352?ref_src=twsrc%5Etfw&amp;ref_url=http%3A%2F%2Fstorify.com%2FPepeBorras%2Fopent-iot-assembly

This time round, there was a handful of people, in person, in a room for the whole day in central Mitte instead - albeit one with a nice view from the tenth floor, and a few people skyped in, in anm iPhone in a glass, to make them easier to hear.

<img class="alignnone size-full wp-image-2911" src="https://mrchrisadamsblog.files.wordpress.com/2018/03/dsc_0345.jpg" alt="DSC_0345.jpg" width="2992" height="2000" />

<h4>What we were going for</h4>

The goal of the day, as I understood it, was to get the ideas in the most recent document in better shape for being used as a basis for a certification mark.

This included:

<ol>
    <li>tidying up the language and trying to make it as accessible as possible without losing the substance of the initial document</li>
    <li>reconciling it with the <a href="https://github.com/openiotmark/iotmark-principles/issues">issues raised on github,</a> and feedback when presenting it at Mozfest in November 2017.</li>
</ol>

There was also a move to make the IoTMark something people and organisations of all sizes could realistically commit to adhering to - when setting up a certification mark can easily cost more than 40k USD, it makes sense make it something that actually could be adopted.

<h3>A bit like Energy Star, for IoT</h3>

<img class="alignnone size-full wp-image-2910" src="https://mrchrisadamsblog.files.wordpress.com/2018/03/dsc_0387.jpg" alt="DSC_0387.jpg" width="2992" height="2000" />

One strategy to follow if you want a diverse set of people to commit to a set of ideas, is to introduce levels of commitment, so you aren't asking for people to make a binary <em>all in/ all out </em>choice.

There was already some implicit sense of grading here in the normative language (a MUST  is non-negotiable, but a SHOULD for example, is not absolutely mandatory), so started with that, to come up with a rough set of three groupings.

I say groupings here, because it's <em>really, really hard</em> to have a single axis when discussing these products, that goes from, say, <em>bad</em> to <em>good</em>. It's much more complicated than that, and different people value different qualities - some people might value openness of software and hardware over the supply chain transparency, and some might treat being explicit about how personal data is used as more important than marketing to a specific group of people.

That said, one grouping <em>was</em> considered <em>a bare minimum - </em>something considered reasonable to expect <em>anyone</em> wanting a connected product that follows the principles to follow. It felt important to have something everyone could have as some shared values, before focusing on diverging areas.

<h3>Relating GDPR to IoT</h3>

The other thing that came out of the day was just how far reaching the GDPR is when it comes to thinking about about connected products, and why it made sense to think about it in the context of IoT.

It's a common refrain that the tech industry needs to improve when it comes to it's cavalier attitude to people's data - often deeply personal data secured in dangerously careless ways, and used in ways that definitely aren't in the interests of the consumer.

I also think it's safe to say that there is appetite for change, and well… from my perspective at least, GDPR feels like change for the tech industry in the same way that a giant asteroid might have represented change to wildlife around the end of the <a class="int-link" title="" href="https://www.wikiwand.com/en/Cretaceous">Cretaceous</a> period on Earth.

To be clear, this change isn't necessarily bad - asteroids can sometimes get rid of dinosaurs and make life easier for us humans, after all.

<strong>Why you might care about GDPR for IoT</strong>

I often point people to these <a href="https://digitalblog.coop.co.uk/2017/11/27/making-the-general-data-protection-regulation-easier-to-understand/">posters from the co-up to</a> help understand the ideas behind the GDPR, and why it's a big deal - for many consumers, <em>the ideas in the GDPR don't sound like unreasonable things to ask for,</em> especially when <a href="https://blog.mozilla.org/blog/2018/02/28/dear-mick-mulvaney-dont-let-equifax-off-easy/">there often seems to be no real penalty for bad behaviour, from lawmakers</a>.

https://twitter.com/jckfltchr/status/927863292923662336

<h4>Chaos Monkeys for your data pipeline, otherwise known as <em>Europeans</em></h4>

In addition, if you are building a connected product the the changes to <a href="https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/">privacy law are extraterritorial,</a> as in - if any citizens of EU member states end up in your data pipeline, or data is proceeded in the EU these laws still apply. I think <a href="https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/">Heather Burns, covers this really well in a recent piece</a> aimed at web developers, and much of it applies for IoT too:

<blockquote>In May of 2018, a major upgrade to Europe’s overarching data protection framework becomes enforceable. This will be followed by a companion piece of legislation pertaining to data in transit. The extraterritorial nature of these two frameworks — they protect the privacy rights of people in Europe regardless of where their data is collected — means that they will become the <em>de facto</em> standard for privacy around the world.</blockquote>

Enforcement may be another issue, but given that for 300 million people at least, the biggest changes to privacy law in 25 years are coming into effect this year, and will force changes anyway, ignoring it seemed short-sighted, as well as being against many of the ideas in original document.

<h4>Overlap between IoT principles and GDPR</h4>

I'll end this section with one thing that struck me - it's totally possible to build connected products that comply with the ideas of the GDPR, and there are very large companies doing exactly this. In fact, there's some great stuff by <a href="http://interconnected.org/home/2017/10/31/security_and_privacy">Matt Webb</a>, on how privacy can be a competitive advantage for IoT services that's worth reading if you're interested in this field.

He cites <a href="https://www.hoxtonanalytics.com/">Hoxton Analytics as a good example</a> - by building privacy into their product from the beginning, they could be deployed in places more invasive systems couldn't, helping them against competitors - there's a lot of FUD about GDPR, but it's also an opportunity to rethink the playing field, something lots of companies already invested in one way of working seem to miss.

<h4><span class="contentBold">R</span><span class="contentBold">F</span><span class="contentBold">C</span><span class="contentBold">s</span> <span class="contentBold">v</span><span class="contentBold">e</span><span class="contentBold">r</span><span class="contentBold">s</span><span class="contentBold">u</span><span class="contentBold">s</span> <span class="contentBold">p</span><span class="contentBold">r</span><span class="contentBold">i</span><span class="contentBold">n</span><span class="contentBold">c</span><span class="contentBold">i</span><span class="contentBold">p</span><span class="contentBold">l</span><span class="contentBold">e</span><span class="contentBold">s</span></h4>

Another thing that came up thing during the day, was the difference between a spec using specific normative language as described by the IETF, which you typically validate programmatically based on the MUSTs and SHOULDs, and a set of principles which tend to have more fuzzy edges, and are more open to interpretation.

It's relatively old now, there's some really great thinking in Lawrence Lessig's book Code, about different ways of enforcing behaviour, which I think is relevant.

I don't have the book handy, but <a href="http://www.zephoria.org/thoughts/archives/2011/08/05/design-social-norms.html">Danah Boyd's blog summarises</a> one of the key ideas nicely :

<blockquote>In his seminal book “Code”, Larry Lessig argued that social systems are regulated by four forces: 1) the market; 2) the law; 3) social norms; and 4) architecture or code.</blockquote>

I think it's easy to conflate these. When you're trying to bring about a specific kind of behaviour you want people to follow, it's worth thinking in these terms, so you don't try to make one force act as it's another.

<h4>Embodied thinking in physical space</h4>

<img class="alignnone size-full wp-image-2908" src="https://mrchrisadamsblog.files.wordpress.com/2018/03/dsc_0382.jpg" alt="DSC_0382" width="2992" height="2000" />

Finally, in the afternoon, after re-reading through the the principles as described in the original Open IoT documents, referring to the Github issues, and Mozilla versions, and deduping them, we spent a bunch of time finding ways to group these principles, to make it easier to follow a meaningful amount of them if you can't follow all of them.

If you have a load of people in a room, and you need to help build a shared understanding, one strategy to help people to this is use some physical token represent an idea, and let people use the physical space to communicate how ideas relate to each other.

Given we had spent a bunch of time already checking our understanding of the ideas in isolation, I found it useful to help communicate positions for people in the room to discuss more effectively.

The downside here when you are skyping people in, is that they're not able to move things around themselves - and by doing this, you're making a specific decision to favour collaboration in the room, over those who are remote. In most cases, I think this is the right call, as the alternative is often to collaborate at speed of the person with the lowest bandwidth connection, which reduces what you can get done in a limited amount of time.

I'd love to hear suggestions for finding a way around this - while you can use tools like <a href="http://realtimeboard.com/">realtimeboard</a> to create a whiteboard-like experience, you're still reducing the richness of your interactions in the room to what the software lets you do with a piece of backlit glass.

<h3>How to get involved in this in future</h3>

If you're interested in any of this, I'd suggest heading to the <a href="http://iotmark.org">iotmark website</a> - from there you can see the current version of the principles, join the slack workspace, or subscribe for <a href="http://eepurl.com/cWNLyv">updates over email</a>, or <a href="http://twitter.com/iot__mark">follow the IotMark on twitter</a>.

As ever, comments on this post are welcome, and if you prefer <a href="http://blog.chrisadams.me.uk/contact">you can contact me directly.</a>

&nbsp;

&nbsp;

&nbsp;

