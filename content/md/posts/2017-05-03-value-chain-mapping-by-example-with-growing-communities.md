

{:author "chrisdaggimoh", :title "Value Chain Mapping by example with Growing Communities", :date "2017-05-03 09:20:30", :publish-date "Wed, 03 May 2017 09:20:30 +0000"}



<!-- content below -->

<em>Through my company Product Science, for the last three years I've been working with <a href="http://growingcommunities.org/">Growing Communities</a> a non-profit organisation set up in the 90s to get good, fairly traded, organic food to people in a neighbourhood, in an environmentally, socially, and financially sustainable way. </em><em>In the summer of 2015, during a strategy planning workshop together we used Simon Wardley's Value Mapping technique (often referred to as Wardley mapping) to help work out a strategy for a key part of the organisation's activity: their <a href="https://growingcommunities.org/organic-veg-scheme">weekly veg scheme</a>. With their permission, I'm sharing this write-up to help share examples of using Wardley maps in the wild, as a handy reference point for others.</em><!--more-->

<h2>Setting the scene</h2>

<img class="alignnone size-full wp-image-313" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/staff20photo20201520lowres20v2_0.jpg" alt="staff20photo20201520lowres20v2_0" width="480" height="319" />

Over 2014, I started working with Growing Communities, an NGO committed to making affordable, organic food available in Hackney, creating long term relationships with farmers around London, and creating jobs in the local neighbourhood. This short video below gives an idea of what they're about. They're a lovely bunch.

https://vimeo.com/114160087

<h3>That's nice. What does this have to do with mapping?</h3>

As mentioned in earlier (and in the video) Growing Communties runs a box scheme. A during a half day workshop, after running through a short deck introducing the concept, a handful of us had a go at mapping this out together, with some post-it notes, markers. It looked a bit like this:

<img class="alignnone size-full wp-image-336" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/img_0641.jpg" alt="IMG_0641" width="2592" height="1936" />

<h3>Tidying this up a bit</h3>

Tidied up it looks a bit more like this:

<img class="alignnone size-full wp-image-346" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/screen-shot-2017-05-01-at-00-12-04.png" alt="Screen Shot 2017-05-01 at 00.12.04" width="1119" height="867" />

At the top of this, we had a user need for "<em>ethical fresh veg</em>". To help meet this need, we relied on a) a <em>website</em> for people to see what's available, and place orders, b) a <em>veg bag</em> of produce, c) a <em>newsletter</em> we used to tell members what was in the bag this week, with some links to recipes, and d) for publicity and to help people pick up their bags, printed matter which we referred to as '<em>signage</em>'.

On order to deliver the veg bags, we also needed a way to deliver them (in this case, it was Maisie the Milkfloat who took care of <em>delivery</em>), as well as <em>fruit and veg</em> from the farms. Growing Communities isn't a box scheme - you pick it up from a specific place instead of having vans drop it off to you, so we needed somewhere for member s to pick up the bags of produce. In this map you can see this as <em>Cafes and Community spaces </em>on the map, some of which were rented (hence the <em>rented premises</em>).

The website was more than a brochureware site, there was a hand-rolled CRM of sorts in it depths, which also helped generate a <em>packing list </em>of  who had ordered product in a given week. This <em>packing list</em> is what staff use to work what product they should put into the bags to be delivered, but this <em>packing list </em>is also what is used to work out what to order each week, and also what to collect from customers via a <em>payment processing </em>system. Other staff would put the numbers of active customers each week into a custom <em>ordering spreadsheet</em>, and then use these numbers of people ordering in a given week, as a guideline for what kind of budget they had to spend on ordering product from <em>local farmers</em> and <em>wholesalers.</em>

From data recorded in a packing list each week, you could generate data for checking in an <em>accounting system, </em>and yes because there was a fairly complex website and a number of automated systems, we relied on some<em> servers </em>to run our programs on.

So that's our map, abridged.

<h3>Representing our own stack in this map</h3>

I referred to a few automated processes and a website in the previous section. While these were different activities, the reality was that a single monolithic Django application powered all of them, and to represent, this, I've shaded it it grey.

Building an app as a monolith when starting out tends to help you deliver features quickly, but over time, it becomes they can become harder to manage, and frequently, productivity when working on them drops off, as you end up managing an ever growing 'ball of mud'. This is compounded if you are running an application on a 'snowflake'-like server set up, which is the only working version of a given site.

Lots of the Growing Communities stack was custom, and had been built by a developer who was no really longer around to work on it, and when the this stack was built, lots of this <em>had </em>to be done a custom one-off work, because there were few suitable products to do some of these jobs for you.

<img class="alignnone size-full wp-image-395" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/screen-shot-2017-05-01-at-00-30-52.png" alt="Screen Shot 2017-05-01 at 00.30.52" width="1275" height="951" />

<h3>However, everything evolves</h3>

While a Wardley Map nice for giving a point in time snapshot of a service's of an organisation, being able to show movement over time is extremely useful for helping people in a room understand how common ways of carrying out an activity may change over time.

I've represented this in the map below - as I mentioned before, the shaded grey area represents a big ol', hard to change custom django application, and the arrows highlight areas of the value chain, where there are clear examples of evolution to a more well understood, commodity-like offering. I'll cover websites and delivery below in more detail to explain this in more detail:

<img class="alignnone size-full wp-image-425" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/screen-shot-2017-05-01-at-00-42-26.png" alt="Screen Shot 2017-05-01 at 00.42.26" width="1255" height="952" />

<h4>Evolution in websites</h4>

Over the last 5 years or so, it's safe to say building websites has become a more commonplace activity, and popular products, like Wordpress have grown to be much more capable, sophisticated and well understood.  If you compare the WordPress of 2008, to the WordPress of 2017, you'll see a much more powerful product, but also a vibrant ecosystem of hosting services, products built on top of it, and companies who provide development services, which means you have a wider range of suppliers to choose from.

Wordpress is one clear example we were thinking when making this map, but it's not the only one. There are a number of closed source and open source products available now if you want to get a website up, and you don't want to be tied to a single supplier.

<h4>Evolution in delivery</h4>

You can also see evolution in the delivery area, where I've added another arrow - just hiring hiring a car, or small van on a per hour basis has become much easier, and more commonplace thanks to companies like Zipcar and so on, This might not be as charming as Maisie the Milkfloat, but operationally, it's much simpler, and finding spare parts for milkfloats isn't getting any easier. Also utility like pricing means that you end up only paying for the time you're using it, and you're not committing for a long term either - good if a vehicle isn't in constant use all week, or the use patterns change.

&nbsp;

<h3>Sketching out a new world</h3>

So, we were able to use maps to sketch out our own value chain, and we were able to sue them to identify areas of evolution that we might want to take advantage of, when thinking strategically about our future.

In addition to using a map to talk about what changes have taken place, you can also use maps to describe a possible future shape of a value chain, and talk about the pros and cons of these different approaches.

<h4>If we were to start a new veg scheme tomorrow with no legacy infrastructure</h4>

If you were setting up a veg scheme tomorrow, and you already had years of experience running one, you might not build everything as a single monolithic system straight away. In general, I agree with <a href="https://www.martinfowler.com/bliki/MonolithFirst.html">Martin Fowler's advice that monoliths are good to start out with</a> when you're exploring a problem or building a first pass at something. Once you've identified the main jobs a system is doing, there is an argument for breaking this into smaller services, and letting specialised tools to specific jobs.

<h4>A sample map, without building a website CMS yourself</h4>

The map below, outlines one possible approach we considered. While some parts of running a weekly veg scheme, were unique to Growing Communities, other parts, like maintaining a website, and letting people sign up to the scheme weren't, and we explored having two separate systems - one well under product looking after a website like Wordpress or Drupal, and where the recurring billing, and specific delivery rules were needed, we'd continue to build this in-house.

This is why in the map below we no longer have the amorphous blob representing a huge, old do-everything django app, but instead we have two separate shaded regions to represent the two systems at work - one for the more commoditised, commonly understood CMS-powered website, and one for the more bespoke system handling billing, generating packing lists for customers and so on.

If you have a smaller system custom system, there's less code, and hopefully fewer concepts for a new developer or team to understand before they can be productive on, meaning that you're less dependent on a single supplier.

<img class="alignnone size-full wp-image-448" src="https://mrchrisadamsblog.files.wordpress.com/2017/04/screen-shot-2017-05-01-at-00-52-30.png" alt="Screen Shot 2017-05-01 at 00.52.30.png" width="1209" height="947" />

<h4>How the map informed the final strategy</h4>

If you go to the Growing Communities website, you'll see a website powered by the Drupal CMS put together by <a href="http://www.webfroth.co.uk/">an agency</a> that specialises in creating websites in Drupal. This speaks to <a href="http://boxmaster-systems.co.uk/">Boxmaster</a>, a commercial product designed specifically for organisations running veg box schemes.

This replaces a single hard-to-change, monolithic django application, which was appropriate for exploring the problem and building a service around, but was only really understood by two people, who were not core parts of the staff, nor were they working on building veg box schemes full time.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

