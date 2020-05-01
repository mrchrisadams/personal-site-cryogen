

{:author "mrchrisadams", :title "Planet friendly web development with Python - a transcript", :date "2017-06-10 12:26:54", :publish-date "Sat, 10 Jun 2017 12:26:54 +0000"}



<!-- content below -->

<em>Over the last few months, I've spoken at a few conferences and meet-ups around Europe about what I'm calling the "Planet-Friendly Design" or "Planet-Friendly Web Development", to a mixture of UX focussed audiences, and developers. The slide decks I have used for each <a href="https://speakerdeck.com/mrchrisadams">conference are available online at speakerdeck</a> (mainly because I've been updating decks and what I say each time). </em>

<em>Somewhat inspired by Ana Balica's transcript post of <a href="http://ana-balica.github.io/2017/05/28/humanizing-among-coders/">from her keynote for Pycon CZ last year</a> , and <a href="http://idlewords.com/talks/web_design_first_100_years.htm">Maciej Cegłowski long form talk/essay hybrid pages</a>, I'm also experimenting with putting the talk on my blog here, to make it easier to digest. I'll add the video once it's online.</em>

<em>Here we go…</em>

<h2>Planet Friendly Web Development with Python</h2>

<hr />

<img class=" size-medium wp-image-1395 alignnone" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-001.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.001" width="300" height="169" />

<hr />

<img class=" size-medium wp-image-1399 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-002.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.002" width="300" height="169" />

<p class="p1"><span class="s1">Hello. My name is Chris Adams.</span></p>

<p class="p1"><span class="s1">I started out working with Django in 2008, but over the last ten years I’ve also worked as a designer, a sysadmin, a product manager, a UX consultant, and and a user researcher, on various environmentally minded projects and startups. I currently live and work in Berlin, I booked a train down with <a href="http://loco2.com">Loco2</a>, and I’m working with <a href="http://thermondo.de">Thermondo</a> in Germany.</span></p>

<p class="p1"><span class="s1">Over this time, I’ve been thinking a fair amount about how what we do as developers relates to the wider discussion about the environment and climate change taking place.
</span></p>

<p class="p1"><span class="s1">My aim today is to provide you with some context for how what we do fits into this wider picture, and share a mental model for thinking about building apps with this in mind, along with some examples of how this relates to your work.</span></p>

<hr />

<img class=" size-medium wp-image-1402 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-003.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.003" width="300" height="169" />

<p class="p1"><span class="s1">I'll be mentioning carbon dioxide a few times today, so I’m going to start with a quick reminder on the greenhouse effect. Here’s more or less how it works:
</span></p>

<p class="p1"><span class="s1">Sunlight hits earth.</span></p>

<p class="p1"><span class="s1">When energy from the sun hits Earth, some of it ends up warming the planet, and some bounces back off into space. What's special about Earth though is that it has large enough quantities of certain gases within the atmosphere, primarily CO2, to bounce some of the energy back to Earth again.</span></p>

<p class="p1"><span class="s1">This energy warms up the planet, so we refer to these gases as greenhouse gases, and the phenomenon as the greenhouse effect.</span></p>

<p class="p1"><span class="s1">So, this greenhouse effect has been very useful to us. It's made life possible in the first place.</span></p>

<p class="p1"><span class="s1">Over the last 100 years or so, largely as a result of human activity, we’ve ended up with greater levels of greenhouse gases, and in particular CO2, in the atmosphere.</span></p>

<p class="p1"><span class="s1">More CO2 results in a more powerful greenhouse effect, resulting in more energy in the system, and a warmer world.</span></p>

<hr />

<img class=" size-medium wp-image-1404 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-004.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.004" width="300" height="169" />

<p class="p1"><span class="s1">While warmer world sounds nice, it turns out that the reality is less nice.</span></p>

<p class="p1"><span class="s1">The reality is more extreme weather events, more drought, more destruction to vital ecosystems we rely on, and in general, problems of the kind that scientists describe as existential threats, and ones that can only really be solved by collective action.</span></p>

<p class="p1"><span class="s1">So, since the mid-nineties, we (and by we, I mean the countries making up the United Nations) have been meeting every year for a series of huge, long meetings, to agree on what to do about this, the aforementioned existential threat to our civilisation.</span></p>

<p class="p1"><span class="s1">And finally, after 21 goes at getting it right, in 2015 in Paris - more or less everyone agreed that we definitely want to limit climate change, and we also want to aim for to less than 2 degrees of global warming in total.</span></p>

<p class="p1"><span class="s1">This effectively created a ceiling on the total amount of greenhouse gases we can emit as a planet - a carbon budget, so if we want to stay inside this budget, our emissions need to go a bit like this (short video of showing the emissions drop off from Bret Viktor's essay <a href="http://worrydream.com/ClimateChange/"> What can a technologist do about climate change? A personal view)</a></span></p>

<hr />

<img class=" size-medium wp-image-1407 alignnone" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-005.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.005" width="300" height="169" />

<p class="p1"><span class="s1">Getting an agreement like the one in Paris was quite impressive, but what’s even more amazing, is that people are actually following through with the agreement, and changing how their economies work.</span></p>

<p class="p1"><span class="s1">According to the <a href="http://www.iea.org/newsroom/news/2017/march/iea-finds-co2-emissions-flat-for-third-straight-year-even-as-global-economy-grew.html">International Energy Agency</a>, 2017 is the third year where global emissions didn't increase, but the global economy still grew.</span></p>

<p class="p1"><span class="s1">So, we’re seeing a decoupling of economic growth from emissions - and we can now point to this happening in America and China, the two biggest emitters as they move away from coal, while their economies continue to grow.</span></p>

<hr />

<img class=" size-medium wp-image-1411 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-006.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.006" width="300" height="169" />

<p class="p1"><span class="s1">That said though, before we start feeling too proud of ourselves, we do need a sense of perspective.</span></p>

<p class="p1"><span class="s1">Because it’s taken this long to reach a turning point, as a civilisation, we need to reduce our emissions much more aggressively than a few years ago if we want to stay within 2 degrees. The blue line here shows what we needed to do in 1995, and the red line onwards shows how much faster emissions need to fall now as a result of our inaction.</span></p>

<span class="s1">Okay, so we have established that:</span>

<ol>
    <li class="p1"><span class="s1">we can change our economies</span></li>
    <li class="p1"><span class="s1">we have a lot of work to do</span></li>
    <li class="p1"><span class="s1">we need to do it fast</span></li>
</ol>

<p class="p1"><span class="s1">Where do we start?</span></p>

<em>(image is from Robbie Andrew's blogpost <a href="http://folk.uio.no/roberan/t/global_mitigation_curves.shtml">It's getting harder and harder to limit ourselves to 2°C</a>)</em>

<hr />

<img class=" size-medium wp-image-1414 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-007.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.007" width="300" height="169" />

<p class="p1"><span class="s1"><a href="http://www.ecofys.com/files/files/asn-ecofys-2013-world-ghg-emissions-flow-chart-2010.pdf">This Sankey diagram from 2010</a> shows a rough breakdown of global emissions by sector and gas. The bit on the left shows the key sources of emissions, the middle bit shows emissions by sector responsible for them, and the bit on the right shows which gases are responsible for the Greenhouse effect.</span></p>

<p class="p1"><span class="s1">Agriculture is about 7%, and road transport is about 10%, like deforestation (filed euphemistically as “land use change” here), and energy generation is about 13%.</span></p>

<p class="p1"><span class="s1">Flying, which is one we hear a lot about only shows up as a between 1 and 2 percent of global emissions. IT doesn’t even show up - it’s just lumped in with the other categories.</span></p>

<p class="p1"><span class="s1">And this is a key thing when talking about climate change and the environment, if you woke up tomorrow and thought "I HAVE to do something important about climate change" you wouldn't <b>start</b> with changing how you design your websites.</span></p>

<p class="p1"><span class="s1">There are important discussions to have about our diets, (i.e. how much meat we eat, how keep homes warm or cool, how we travel around the world by car or fly, and so on).</span></p>

<p class="p1"><span class="s1">However, I’m not here to talk about that, as it’s far beyond the scope of the time I have. Instead, I’m here to talk about our impact when we build things online.</span></p>

<hr />

<img class=" size-medium wp-image-1417 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-008.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.008" width="300" height="169" />

<p class="p1"><span class="s1"><a href="https://www.slideshare.net/greentouch-org/intro-to-green-touch">This deck</a>, citing the Climate Groups <i>Smart 2020</i> report shows IT at around 2% of planetary CO2 emissions in 2007 - about the same as aviation.</span></p>

<p class="p1"><span class="s1">Remember how much power generation (i.e. electricity) contributed to emissions in the last graph? Well, as an industry, we’re getting pretty power hungry. I live in Germany, currently the 4th largest economy on Earth. Deutsche Telekom is the 3rd largest consumer of electricity in the country.</span></p>

<p class="p1"><span class="s1">And in three years time, as an industry, we’re predicted to be responsible for twice the emissions as aviation.</span></p>

<p class="p1"><span class="s1">So we may have started as a small part of emissions, but we're growing fast. And as web developers, while we might not have direct control over deforestation, we do have rather more control over how we might use data centres and infrastructure for shipping our bits to our users.</span></p>

<hr />

<img class=" size-medium wp-image-1420 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-009.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.009" width="300" height="169" />

<p class="p1"><span class="s1">As I said before, I’ve been trying to come up with a mental model to help me take this stuff into account when I’m building sites or apps, and I’m going to share it with you today.</span></p>

<p class="p1"><span class="s1">And I’m doing it because I think there’s a lot of overlap between what’s good environmentally, and what’s good practice for building digital products and services.</span></p>

<p class="p1"><span class="s1">I also think that if you want to bring about the change we need, framing it in positive terms, like being awesome at your profession is a better approach than trying to shame people into action.</span></p>

<hr />

<img class=" size-medium wp-image-1422 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-010.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.010" width="300" height="169" />

<p class="p1"><span class="s1">So, I’ve grouped this mental model into three main areas: <strong>Your Platform</strong>, <strong>Your Packets</strong>, and <strong>Your Process</strong>, drawing on existing communities of practice, that don’t always speak to each other:</span></p>

<p class="p1"><span class="s1">For <b>Your Platform</b>, we borrow ideas from software engineering, and technical architecture, and the devops movement.</span></p>

<p class="p1"><span class="s1">For <b>Your Packets </b>we borrow ideas from Web Performance Optimisation.</span></p>

<p class="p1"><span class="s1">For <b>Your Process</b> - we borrow ideas from the Lean UX movement, and continuous delivery, but there isn't really time today to cover it in much depth. There’s a link to a 45 minute talk I gave in November at the end of this deck though.</span></p>

<hr />

<img class=" size-medium wp-image-1425 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-011.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.011" width="300" height="169" />

<p class="p1"><span class="s1">When it comes to servers you control you can think of two things to think about. who your providers are, and how you provision your computing power.</span></p>

&nbsp;

&nbsp;

<hr />

<img class=" size-medium wp-image-1427 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-012.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.012" width="300" height="169" />

<p class="p1"><span class="s1">The first part covers how the electricity powering your servers is generated. This is probably where you have the most direct control.</span></p>

&nbsp;

&nbsp;

<hr />

<img class=" size-medium wp-image-1429 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-013.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.013" width="300" height="169" />

<p class="p1"><span class="s1">A few years back, if you wanted to run your apps on green power, you’d either need to run them in Iceland where almost everything runs on clean geothermal power, or with a number  of small providers either who weren’t too reliable, or had limited product offerings. You’re less likely to make a trade-off between ‘green’ and ‘effective’ these days, and in Europe at least, the two real cloud giants, Amazon and Google claim to run on renewable energy, or be working towards it. So if you’re using these, and you’re running servers in Europe, you’ve already made a decision that reduces the carbon footprint of your app, considerably.</span></p>

<hr />

<img class=" size-medium wp-image-1431 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-014.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.014" width="300" height="169" />

<p class="p1"><span class="s1">If you’re not, there are other things that determine how much CO2 is emitted on behalf of your app. Specifically how efficiently you use the capacity you’ve paid for, from your provider.</span></p>

&nbsp;

<hr />

<img class=" size-medium wp-image-1433 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-015.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.015" width="300" height="169" />

<p class="p1"><span class="s1">This graph from the <a href="http://CEET - http://www.ceet.unimelb.edu.au/publications">CEET report "power of the wireless cloud"</a> here for example shows the typical usage patterns of traffic across the internet in a given area over the day. We’re all asleep, then we start work, then we go home and watch netflix.</span></p>

<p class="p1"><span class="s1">For many of us, we’re so used to paying for compute by the month, that we don’t really think too much about how the capacity we’ve reserved matches up to when our users are awake - we often just think about making sure there’s always enough headroom (reserved capacity) to meet the top end of traffic we expect.</span></p>

<hr />

<img class=" size-medium wp-image-1435 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-016.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.016" width="300" height="169" />

<p class="p1"><span class="s1">But if we’re thinking about the environmental impact of this unused computing capacity, then I think that’s a missed opportunity - it feels a little bit like leaving the office lights on at work when you go home.</span></p>

<p class="p1"><span class="s1">For the longest time, because provisioning servers has been slow and a hassle, it has made sense to just leave the lights on, because the cost of managing this outweighs any savings you might make.</span></p>

(quote from <a href="https://read.acloud.guru/evolution-of-business-logic-from-monoliths-through-microservices-to-functions-ff464b95a44d">Adrian Cockrofts' medium piece Evolution of Business Logic from Monoliths through Microservices, to Functions</a>)

<hr />

<p class="p1"><img class=" size-medium wp-image-1436 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-017.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.017" width="300" height="169" /></p>

<p class="p1"><span class="s1">But as we’ve started to use services more than servers, this has changed. When we shift to use PaaS, we trade a higher unit cost of compute for the greater ease of management of these resources. If we’re looking at this through our planet friendly web lens, we might care about scaling down during periods of low use, so we burn less compute, and therefore less CO2.</span></p>

<p class="p1"><span class="s1">Increasingly you can do this automatically in response to heuristics about load and response time, but if that sounds a bit like voodoo to you, you can also just do it on a timer, by looking at previous usage patterns. I’ll touch on this later.</span></p>

<hr />

<img class=" size-medium wp-image-1439 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-018.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.018" width="300" height="169" />

<p class="p1"><span class="s1">There are other models though. When you pay per response like with FaaS, you don’t really pay for reserved capacity in the same way at all. This changes how you think about redundancy and failover (you aren’t paying to have redundant servers in some high availability configuration anymore), and scaling, versioning of APIs… all kinds of things.</span></p>

<hr />

<img class=" size-medium wp-image-1441 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-019.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.019" width="300" height="169" />

<p class="p1"><span class="s1">Instead you pay per 100 milliseconds you spend serving a request, and you pay for the RAM you use. So, if you can improve code to servicing the same request twice as fast, you see the cost halve.</span></p>

<p class="p1"><span class="s1">Similarly, if you can serve the same request in half the memory footprint, you’ve halved it again.</span></p>

<p class="p1"><span class="s1">In many cases, less CPU burned means less money spent and also means less CO2 released.</span></p>

<p class="p1"><span class="s1">Into performance optimisation? Check you out captain planet, you’ll go far, in this new world!</span></p>

<em>(Quote from <a href="https://gojko.net/2016/08/27/serverless.html">https://gojko.net/2016/08/27/serverless.html</a>)</em>

<hr />

<img class=" size-medium wp-image-1443 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-020.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.020" width="300" height="169" />

<p class="p1"><span class="s1">So, you might be wondering why this talk is feeling like a talk about optimisation, rather than the environment. This is what I mean by there being a lot of overlap between things that reduce how much CO2 we emit into the atmosphere, and good engineering practices.</span></p>

<p class="p1"><span class="s1">Google and Amazon don’t necessarily care about saving energy because they’re warm fuzzy companies. They do it because it’s good business sense, and they work at a scale where the incentives to save energy are proportionally greater, and can use more sophisticated techniques. In the example above, Google bought Deepmind an AI company, for hundreds of millions of dollars, then deployed the AI to work out the most efficient way to save electricity in their datacentres. This reduced the amount of CO2 emitted, but also saved them a huge amount of money.</span></p>

<p class="p1"><span class="s1">So, planet friendly can be wallet friendly -</span></p>

<hr />

<img class=" size-medium wp-image-1445 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-021.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.021" width="300" height="169" />

<p class="p1"><span class="s1">The choices in this table outline some of your options, for platforms, services, or libraries, that you might want to look into if any of this has caught your attention so far.</span></p>

&nbsp;

&nbsp;

<hr />

<img class=" size-medium wp-image-1448 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-022.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.022" width="300" height="169" />

<p class="p1"><span class="s1">So, we’ve covered servers you have control over, and how using green energy, and using your compute resources effectively has an effect on how much CO2 you emit. </span></p>

<p class="p1"><span class="s1">You typically need to send data to your users though - if the previous section was <b><i>Your Platform</i></b>, think go this as <b><i>Your Packets.</i></b></span></p>

<p class="p1"><span class="s1">When a request leaves your servers, you don’t have much control over how it routes through the web to reach a user.</span></p>

<p class="p1"><span class="s1">This is a feature of the internet, and is usually a good thing.</span></p>

<hr />

<img class=" size-medium wp-image-1450 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-023.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.023" width="300" height="169" />

<p class="p1"><span class="s1">However, you don’t have control over how green the rest of the<i> </i>infrastructure you rely on is. So, sending data can result in wildly differing amounts of CO2 emissions too, depending on where those servers are.</span></p>

<p class="p1"><span class="s1">This map shows how green the electricity is around Europe, based on what kind of power is used to generate it. The further from green the colour is the more CO2 intensive the energy is.</span></p>

<p class="p1"><span class="s1">You can see that France is geeen because it's full of nukes.</span></p>

<p class="p1"><span class="s1">The Scandinavian states are green because they have lots of hydro power.</span></p>

<p class="p1"><span class="s1">Germany is brown because while it has lots of solar, it also has lots of coal.</span></p>

<p class="p1"><span class="s1">And Poland has loads of coal, so it’s really dirty power.</span></p>

<hr />

<img class=" size-medium wp-image-1452 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-024.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.024" width="300" height="169" />

<p class="p1"><span class="s1">We’ve covered how the energy mix in a country is likely to affect our impact. As this quote from a recent Center for Energy Efficient Telecommunications report suggests, the type of connection used also affects the CO2 emissions of sending data.</span></p>

<p class="p1"><span class="s1">The recent switch to 4G has meant that while we get data faster, it’s also much more energy intensive. This means our CO2 emissions increase here, as a greater amount of our traffic moves to mobile.</span></p>

<hr />

<img class=" size-medium wp-image-1454 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-025.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.025" width="300" height="169" />

<p class="p1"><span class="s1">This graph from the Center for Energy Efficient Telecommunications shows predicted growth in energy usage back in 2012, and the impact of switching to 4G.</span></p>

<p class="p1"><span class="s1">Even in the best case scenario, this showed at least 3x increase in power usage - for mobile - 4G transmission alone is larger than ALL the energy use from a three years earlier.</span></p>

<hr />

<img class=" size-medium wp-image-1456 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-026.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.026" width="300" height="169" />

<p class="p1"><span class="s1">Compounded by this, we can see an obesity crisis in webpage size. There’s a clear direction of travel here - ever larger pages, sent over more energy intensive connections - and it’s pretty much the opposite of what we’d want from a CO2 emissions perspective.</span></p>

<p class="p1"><span class="s1">I’m trying avoid being too ‘doom and gloom’ here, but folks - the average webpage is bigger than the game Doom was when it was first release now.</span></p>

<p class="p1"><span class="s1">So, what can we do?</span></p>

<hr />

<img class=" size-medium wp-image-1459 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-027.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.027" width="300" height="169" />

<p class="p1"><span class="s1">One technique the web performance community has used to help fight this bloat, has been the use of performance budgets in designs. While the goal here is a better user experience and a fast loading site, it also turns out to be pretty planet-friendly too, as it reduces the amount of data being sent, and therefore energy used, and therefore CO2 being chucked into the atmosphere.</span></p>

<hr />

<img class=" size-medium wp-image-1461 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-028.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.028" width="300" height="169" />

<p class="p1"><span class="s1">Whats also cool is that just like how we have continuous integration to check our tests work, you’re now seeing tools like Speedcurve, or CalibreApp, that work like Continous Integration on for page and performance budgets on key pages on your production site. So we have a tool to guard against this now.</span></p>

<p class="p1"><span class="s1">What’s more these allow for lots of other clever uses. For example, I know that U-switch, a uk energy switching company, used this to benchmark their site against competitors, but also to get their home page down to around 600k in size, and there are many, many studies correlating increased web performance and sales from amazon, easy and so on.</span></p>

<p class="p1"><span class="s1">If you want an open source option, I suggest you look at <a href="http://sitespeed.io"><span class="s2">sitespeed.io</span></a> too.</span></p>

<hr />

<img class=" size-medium wp-image-1463 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-029.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.029" width="300" height="169" />

<p class="p1"><span class="s1">When we’re talking about the packets of data you send, I’ve found it useful to think of your packets in terms lossy changes you might make, and lossless changes.</span></p>

<p class="p1"><span class="s1">We often make ‘lossy’ trade-offs in what we send to people - you deliberately reduce image quality and dimensions, or omit unused code, to deliver a faster loading, better user experience.</span></p>

<p class="p1"><span class="s1">For example, when a user gets sent lots of stuff they won’t use, or appreciate in a web page now, it’s a waste. They might just want a nice dropdown menu, but they get masses of javascript and a whole bootstrap’s worth of CSS, regardless of whether they want it or not. Why do this when we can just send the css and js we need? There’s loads of interesting work going on in this area, which I’ll refer to in more detail in a bit.
</span></p>

<hr />

<img class=" size-medium wp-image-1465 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-030.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.030" width="300" height="169" />

<p class="p1"><span class="s1">If the previous idea is lossy, you might think of another category, where compression and caching fit in, as a more ‘lossless’ approach.</span></p>

<p class="p1"><span class="s1">When I gzip or minify files, I don’t lose information, or remove functionality, but amount of data sent is smaller. And when I’m use caching or a CDN, by choosing to not send data you already have, I still end up with less data to deliver, without losing information.</span></p>

<hr />

<img class=" size-medium wp-image-1468 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-031.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.031" width="300" height="169" />

<p class="p1"><span class="s1">So, we've looked at two ways how we affect the environmental impact of sending packets to our users. Coincidentally, they almost always result in a better user experience, as pages end up loading faster, and we often end up with us, and our users paying less for bandwidth.</span></p>

<p class="p1"><span class="s1">If there is one takeaway I really want you to take from this talk, it’s this: making a site work better for the planet is pretty much the SAME THING as making it work better for users. So, the chances are, many of you in this room have already spent years becoming black belts in planet-friendly web-ninjutsu. Hear that Neo? You already know kung fu.
</span></p>

<hr />

<img class=" size-medium wp-image-1470 alignleft" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-032.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.032" width="300" height="169" />

<p class="p1"><span class="s1">Remember those scary graphs I mentioned at the beginning of this talk, and how basically every industry needs to change if we want to stand a chance at staying inside that planetary budget of 2 degrees? As professional developers, we’ll need to know what those changes look like inside our industry too - especially given that IT is being seen as one of the best tools we have for building a greener, more sustainable future.</span></p>

<p class="p1"><span class="s1">I aimed in this talk to give you a better understanding about where what we do as developers fits into the global picture, and how some of the stuff you might already be doing has an effect on the environmental impact of the sites and apps you create.</span></p>

<p class="p1"><span class="s1">
So I hope in your day to day jobs, you’ll see how things <i>you already know how to do </i>can help make the sites you build more planet-friendly, as well as cost less, and provide a better user experience. You might do it because you feel strongly about the environment like me, but you might do it because you like looking awesome in front of your boss. The key thing as developers we don’t really need to choose - for us they’re the same thing!</span></p>

<p class="p1"><span class="s1">So, I’ll end this talk by with a quote from one of my favourite childhood cartoons - the power is yours.</span></p>

<hr />

<img class="alignnone size-medium wp-image-1472" src="https://mrchrisadamsblog.files.wordpress.com/2017/06/2017-06-09-planet-friendly-web-development-with-python-pics-033.jpeg?w=300" alt="2017-06-09 Planet Friendly Web Development with Python - pics.033" width="300" height="169" />

<em>Okay, that was it. When I gave this talk at Djangocon, there were about 300-350 people in the audience. Pycon Italia was closer to 70, and I believe Pycon Czech  had about 100.</em>

<em>I'm tempted to just be done with it and create a proper talk page for this, as while Wordpress is easy to use, for getting something out the door, if I'm writing about this subject, it would be good to y'know, practice what I'm preaching more, and use some of the techniques I refer to in the talk.</em>

<i>If you have questions, feel free to drop me a line of leave a question in the comments (I'll help me think through the ideas better), and I'll try to address it below.</i>

&nbsp;

