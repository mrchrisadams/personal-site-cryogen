

{:author "mrchrisadams", :title "A quick summary of my understanding of software licensing and IP, when it comes to building digital products", :date "2019-03-04 13:21:45", :publish-date "Mon, 04 Mar 2019 13:21:45 +0000"}



<!-- content below -->

<!-- wp:paragraph -->
<p><em>If you want to build an open source product or service, or indeed open source an existing product, it's worth being aware of the key licenses, and in general what they do. In this post, I share how I see them.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><em>Before we go further - I'm not a lawyer. This is my rough understanding, as someone who writes code, makes product decisions, and has followed the industry for the last ten  years or so.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><em>Please consult an actual lawyer before making a decision, obvs.</em></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1>Intellectual property - licensing versus trademarks</h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Intellectual property comes in many, many flavours, depending on where in the world you are, but generally speaking, when thinking about software projects, it's helpful to think of copyright and ownership of code, as separate from discussions of design and trademarks.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It's useful to think of them separately, as they're about different questions - ownership of code is being allowed to make copies of a program, and use it in your own software, or make you pay for access to it.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Design and trademarks, as I understand them are more about stopping people passing off work as theirs, or using a name or design in a way that might confuse others with something made by you  or your organisation.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Because they solve different problems, it's useful to think of both if you'ore thikning about open up a project or the code within it</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Examples of trademarks in use</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>You'll often see an organisation licensing code itself under a relatively permissive license, but retaining control of a brand, by asserting ownership of a trademark, and only allowing distribution if you follow specific guidelines.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Examples</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>You can see this with Mozilla Firefox, or Wordpress, or The Django project.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>With Mozilla's Firefox, if you wanted to distribute the software and bundle a different search engine, you couldn't call it Mozilla Firefox, for a long time. For this reason, for a number of years, see Firefox in the Debian Linux operating system,  branded as <em>IceWeasel</em>. <a href="https://lwn.net/Articles/676799/">This explainer article here outlines why.</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You see the same with Wordpress. You can happily copy wordpress code, and use to host a website, but you need to follow certain guidelines to use the word "Wordpress" in your marketing or external comms. You can see <a href="https://wordpressfoundation.org/trademark-policy/">guidance directly from the Wordpress Foundation here. </a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You <em>also </em>see the same with the Django Project. If you want to put on an event and use the name "Django", you need to follow the <a href="https://www.djangoproject.com/trademarks/"> guidance on how you can use the name</a>. This doesn't stop you using the code to build totally new products.<br><br>With me so far? Trademark might helps you control how people talk about a project or product, but that's not the same as controlling how people are allowed to copy the code in a project.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For that, it's more common to talk about licensing, and licenses. I'll outline a few of the popular licenses you might see online:</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Examples of licensing in use</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>MIT/ FreeBSD / Apache</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>These are very permissive licenses used by software like <a href="https://github.com/django/django/blob/master/LICENSE">Django</a>, and <a href="https://github.com/rails/rails/blob/master/MIT-LICENSE">Ruby on Rails</a>, and <a href="https://github.com/go-redis/redis/blob/master/LICENSE">Redis</a> (<a href="https://redislabs.com/community/licenses/">although not all the code from Redis Labs is licensed this way</a>) </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can include software with these licenses into larger products, that you can sell as a something people pay to download, or pay to use.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Other people can do this too - so, so if you licensed your code under the MIT license, it would be legal for say… Google or Microsoft to copy the code and provide a service, making their improvements and not share anything back.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>An easy example of this would be how the big cloud providers have been able offer <a href="https://aws.amazon.com/elasticache/">Redis as as a hosted service for ages</a>, with needing to pay any money back to Redis Labs, the primary stewards of the software.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You might use these licenses when you want to increase the likelihood of people using your code, and building products on top of it. The risk you run is that they do not share back their changes, or they capture most of the value instead of you.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>GPL - General Public License</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>If you worry about the above, you might choose the General Public License. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>With this someone can run a hosted service, without sharing back their improvements. If you want multiple providers competing to offer your product, but you want to provide an incentive to do this (i.e keep the operational improvements so they can compete on providing a known, compatible product in a better way) , the GPL works here.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The GPL for example lets people use Wordpress and Drupal as hosted services, or indeed include them in services that build on them, without needing to pay a license fees or share back their changes to the original authors of the code.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For example, this lets <a href="https://wpengine.com/">WP Engine</a>, or <a href="https://pantheon.io/">Pantheon</a>, provide a specialised, managed hosting service without needing to share their code for the hosting platform back with you.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>What the GPL stops you doing is sell a proprietary, shrink-wrapped product based on the code, and then stop others from distributing it, by claiming copyright over the code.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This might feel a bit academic, but Wordpress themes are useful example of here.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It's not hard to find Wordpress themes that are licensed with the GPL, and making these themes available for download, where you are expected to pay something.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can still get the code freely if you search for it, or look on some torrent site, but if you're looking for a theme, it's often the support with implementation that you want, as much as the code itself, and trying to get in touch with the original creator and asking for help with a theme you picked up from a torrent is likely to not to go too well.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It's a bit counter intuitive at first, but <a href="https://kinsta.com/learn/wordpress-gpl/">this piece from wordpress host Linsta, is really helpful</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Some companies don't touch GPL licensed code at all. Apple doesn't let GPL code in the Apple store for example, largely because Apple's user license for the Apple store, stops you being allowed to copy an app you download and distribute to others, which violates the GPL.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The most common GPL license you'll typically see now is the <a href="https://github.com/WordPress/WordPress/blob/master/license.txt">GPL v3</a>, but <a href="https://github.com/WordPress/WordPress/blob/master/license.txt">Wordpress still uses the v2 version of the license</a>.<br></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>AGPL - the Afferro General Public License</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>You can think of the Afferro General Public License as like the GPL, in that you can't distribute a proprietary product based on GPL code and stop others copying it themselves, but <em>more so</em>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It goes further, by closing what's sometimes referred to as the hosting loophole, so by making the code available over the network, you need to make the source available too. For example, you probably couldn't run a hosted like Pantheon, or WP Engine, if WordPress was licensed with the AGPL, without making available all the secret sauce you use to run the platform really well<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The <a href="https://www.mongodb.com/blog/post/the-agpl">MongoDB server license used to be licensed under the AGPL</a> - and although I'm not a lawyer, I can see a scenario where this license would be one of the reasons that Amazon took a relatively long time to <a href="https://aws.amazon.com/blogs/aws/new-amazon-documentdb-with-mongodb-compatibility-fast-scalable-and-highly-available/">release DocumentDB, their hosted Mongo-DB compatible service</a>, when they've been able to provide hosted Redis, hosted Elasticsearch and hosted MySQL or Postgres services much earlier. Rather than using the code directly, they've had to make something <em>compatible with MongoDB, but without using any of that AGPL licensed code.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Like the GPL, some large companies have blanket bans on software using the AGPL. Google is an example.Using this license can mean that if you want to work with them, you'll need a different licensed option for your project.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A number of projects, like the Neo4J graph database were dual licensed for this reason - you could use it for free if you share back under the terms of the AGPL, but if you want to build something and <em>not</em> share, you'd need to pay for a commercial license.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can see other examples here in the <a href="https://libraries.io/pypi/searx">Searx open source search engine</a>, or <a href="https://github.com/viewflow/viewflow">Viewflow,</a> business process modelling software. You can use it freely available under the AGPL, but if you want a to make a proprietary product you'd need <a href="https://github.com/viewflow/viewflow#license">Viewflow Pro, a commercial licensed version of the same.</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>What people use instead of the AGPL</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Some organisations that used to rely on the AGPL to stop another provider rebadging their software and selling it as a hosted service, are increasingly licensing code under a different, permissive licenses, but applying extra licenses on opt of them.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can see this in the <a href="https://commonsclause.com/">Commons Clause</a> in the case of <a href="https://github.com/neo4j/neo4j">Neo4j,</a> or the <a href="https://www.mongodb.com/licensing/server-side-public-license">Server Side License with MongoDB.</a> Update: Neo4J dropped the commons clause. They just have GPL for the community version and a commercial license for the Enterprise version of their app.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="docs-internal-guid-0718f988-7fff-4a7a-86d7-c48f7832acf8"><strong>Further reading</strong></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>There's a few sites that can help here, to provide some plain English pointers on licensing your software.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>One is<a href="https://choosealicense.com/"> Choose a Licence from Github.</a> The other from FOSSA, does a similar job, is<a href="https://tldrlegal.com/"> TLDR Legal</a>, which gives readable summaries of many, many licenses.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Simon Wardley's thinking and commentary around how open source licensing can affect a product or service has been extremely useful for me too. This<a href="https://twitter.com/swardley/status/1076258902491258880"> thread here on twitter is illuminating</a>:<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This <a href="https://blog.gardeviance.org/2016/08/the-play-and-decision-to-act.html">piece from Simon Wardley outlines specific reasons to choose the GPL</a> as a tool to establish ecosystem around a new product or service, as well as the trade-offs involved.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This <a href="https://stratechery.com/2019/aws-mongodb-and-the-economic-realities-of-open-source/">post from Stratechery does a good job of spelling out the implications of the AGPL license</a> in the context of the interplay between MongoDB and AWS.<br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This <a href="https://twitter.com/mjasay/status/1039231443979751424?lang=en">thread on twitter on the shortcomings of the AGPL</a> for stopping 3d parties using it without contributing back</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><br></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><br></p>
<!-- /wp:paragraph -->

