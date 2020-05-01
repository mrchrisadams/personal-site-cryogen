

{:author "mrchrisadams", :title "Book review: Time is Money - The business Value of Web Performance", :date "2018-01-08 00:18:56", :publish-date "Mon, 08 Jan 2018 00:18:56 +0000"}



<!-- content below -->

Since discovering how significant the  energy impact of moving data over networks is for the <a href="https://www.planetfriendlyweb.org/">Planet Friendly Web Guide</a>, I've found myself reading more and more about web performance optimisation (WPO). Last week I ordered Tammy Evert's book, <em><a href="https://tammyeverts.wordpress.com/2016/06/06/woohoo-my-book-is-out/">Time is Money - the Business Value of Web Performance</a>. It arrived on Saturday morning, and I had finished it by the afternoon. Here's a quick review.</em>

<strong>TLDR: </strong>I really like it. It's a short book to give you ammo to help win arguments about web performance, in a language product managers and other people who don't code will understand.

You might be able to explain <em>what</em> you would do if you had the time and budget to work on performance on a site or app you're responsible for. This book help you explain <em>why </em>someone should allocate the time and budget to let you make it happen.

<strong>Longer version: </strong>I really like it. It does what a published book does well, compared to a blog post or website, which is provide a concise argument, in ways that hopefully won't feel dated within months of being published, and save you sifting through the entire internet to find the information to arrive at the similar conclusion yourself.

<h3>How we perceive performance</h3>

It begins with a brief primer on why speed and responsiveness (in the HCI, not mobile friendly sense) feel intuitively <em>right, </em>and how regardless of technology, there are a few universal laws around how quickly an application ought to respond, to user input to allow them to feel productive and maintain a state of flow. When I say universal, it might as well be she references literature from as far back as 60's,on human computer interaction.

<h3><strong>Why a business would care about performance</strong></h3>

The next section presents a useful way to think about speed, in ways that a business or project sponsor will otherwise be able to understand - if you've ever read about WPO, you'll probably be familiar with the familiar quotes about speed increasing conversion rates in e-commerce. But Tammy presents few other ways to sell it, from benchmarking against competitors with various monitoring tools, to brand perception, where the people would respond to the same sites, with the same copy, and same design, but see the all of them as lower quality when when presented over a slower connection, to comparing the impact of slow sites of the impact of downtime on a business.

I had never thought of selling it in this way, but it's a really elegant way to think about it - and it's totally compatible with how we might reasonably think about risk in business.

You might think about risk in these terms:

<strong>risk</strong> = <strong>severity of consequences</strong> x <strong>likelihood of it happening</strong>

Some risks have severe consequences. Having a site go down for example, means it can't raise donations, complete purchases, or find the information they need. It (hopefully) doesn't happen very often, but because it's so severe, we dedicate resources to avoiding downtime, like on-call rotas, building redundancy into our systems and so on.

While a slow site may not be as dramatic as a site going down, degrading performance to the point that people stop using it, or go to a competitor has similar effect - it stops making money, or letting people meet their needs. And worse, a slow site is not a one-off event - if it's continually happening, then the cumulative effect of users abandoning tasks over a longer period can be <em>greater</em> than a more dramatic, but shorter period of downtime.

This section, introduced me to a catchy term, <em>the performance poverty line - </em>the slower site is, the more conversions tend to drop off, until, at around 6 seconds, they're barely even happen compared to further up the scale.

If you don't work in e-commerce, but if you work in an organisation where you have internal customers, the chapter following it shows how to think about it in terms of productivity gains, from sites working properly, or reduced bills on infrastructure.

<h3><strong>The how of performance</strong></h3>

I'll say again - this is not a technical book, but the book does provide a good grounding on the principles of performance - the differences between latency and bandwidth, and how different parts of the infrastructure of the net affect performance, and what things like a content delivery network are and why they matter, and the different kinds of monitoring available these days  - synthetic and real user monitoring (RUM) performance measurement . This section is very accessible - if someone knows what HTML is, then they should be able to get through it easily, while still covering a lot of ground.

There's some useful guidance on how you might target your performance efforts too, like which parts of a user journey tend to make the most sense to optimize first to see results.

<h3>The future of performance</h3>

The book rounds off with a few words about the future. There are a few new APIs in browsers to make measuring performance in terms that are more useful to us than simply tracking how long an entire page took to load, and it covers those, and there's some further thoughts what where the function of tracking performance fits in an organisation.

Before I read this book, I hadn't really heard of a role called a <em>digital performance manager, </em>and from what I read, it feels like a cross between a very focused product manager, and the kind of data scientist who gets their kicks from <a href="https://discuss.httparchive.org/">running analysis on the HTTP Archive with Big Query</a> (as an aside, this sounds quite fun - I'd love to hear if this actually is your job).

<h3>Who should buy this book</h3>

It feels like there are two clear audiences for this book:

<ol>
    <li>People into WPO who want to know how to sell it to others.</li>
    <li>People the first group would like to sell it to</li>
</ol>

<strong>People into WPO who want to know how to sell it to others.</strong> If this is you and you're working in a job where you want to start doing this, then it'll probably cost you as much in billable time to read this review, go to amazon, read some more reviews and buy the book, as the book itself costs to buy, and start making a case at work. What are you waiting for?

<strong>The other audience, seems to be the people who the first group would want to give this book to</strong> - either because someone has given it to them to read, to understand what they're continually going on about, or because they don't code, but think there might be something in this performance thing. It feels like this is the <em>real</em> audience for the book, and the writing is light, and easy to read quickly for this reason.

If you don't code as primary way of making money, but you work with developers, it's a good complement to the following short books, for understanding other aspects of working on or managing a digital product:

<ol>
    <li><a href="https://abookapart.com/products/the-elements-of-content-strategy">Erin Kissane's Elements of Content Strategy,</a> (for content strategy and UX)</li>
    <li><a href="https://leanpub.com/agiletoolbox-visualizationexamples">Jimmy Janlen's Toolbox for the Agile Coach</a> (for sharing and planning agile work better in co-located environments)</li>
    <li><a href="https://www.amazon.co.uk/Badass-Making-Awesome-Kathy-Sierra/dp/1491919019">Kathy Sierra's Badass </a>(making users feel productive and effective when using your products).</li>
</ol>

In case you forgot - I really like it.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

