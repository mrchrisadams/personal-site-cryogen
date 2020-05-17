

{:author "admin", :title "Tea, Arduino and Dynamic Demand", :date "2009-04-24 23:35:41", :publish-date "Fri, 24 Apr 2009 23:35:41 +0000"}



<!-- content below -->

It’s the next HomeCamp tomorrow. And in a spectacular feat of bad calendaring, I’ve managed to organise the <a title="The Letter Lounge (letterlounge) on Twitter" href="http://twitter.com/letterlounge">Letter Lounge</a> to take place on the day I’ve been looking forward to for the last few months are coming away from the initial HomeCamp, utterly inspired by what I saw there. 

So to make up for not being able to attend, the least I can do is finally get round to writing about the Tealight, a fun, Homecampy little project <a href="http://jimmyg.org/">James Gardner</a> and I built one evening in the Hub recently.

We did it partly to learn about the Arduino platform, and partly to explore how to make something as complex as demand response intelligible to people who don’t think about this for a living, and well here it is, in all it’s janky, low budget hackish glory:

<object width="400" height="300"> <param name="flashvars" value="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Fdaggi%2Fsets%2F72157617196235135%2Fshow%2F&page_show_back_url=%2Fphotos%2Fdaggi%2Fsets%2F72157617196235135%2F&set_id=72157617196235135&jump_to="></param> <param name="movie" value="http://www.flickr.com/apps/slideshow/show.swf?v=70933"></param> <param name="allowFullScreen" value="true"></param><embed type="application/x-shockwave-flash" src="http://www.flickr.com/apps/slideshow/show.swf?v=70933" allowFullScreen="true" flashvars="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Fdaggi%2Fsets%2F72157617196235135%2Fshow%2F&page_show_back_url=%2Fphotos%2Fdaggi%2Fsets%2F72157617196235135%2F&set_id=72157617196235135&jump_to=" width="400" height="300"></embed></object>

This green orb constantly polls the national power grid to see how it’s keeping up with demand from everyone watching The Apprentice, and subsequently whether your next cuppa will be a particularly carbon intensive one.

If there’s spare capacity on the grid, the tealight will glows green, it’s basically saying:
<blockquote>‘Go ahead! Make some tea! Knock yourself out!’</blockquote>
If there isn’t, the colour shifts to red, saying:
<blockquote>“Now’s not the best time for that cuppa, give it a little while.”</blockquote>
The main idea here is that you can glance at the globe from across an office or co-working space, to get an idea about whether making that cup of tea is a good idea right now, without having to think too hard about it.

Think of it as national grid load balancing, using people, and hot beverages.

<h3 id="how_we_made_this">How we made this</h3>
This is thing is almost embarrassingly simple.

On the software side, we’re basically polling the api for caniturniton.com a website which scrapes the national grid for power usage data every minute or so, and depending on if the figure returned is higher or lower than the baseline of 50hz, we call a function to tell the BlinkM to change the colour of it’s LED accordingly.

Here’s the shopping list of hardware we used:
<ul>
	<li><a title="Arduino - ArduinoBoardDiecimila" href="http://arduino.cc/en/Main/ArduinoBoardDiecimila">Arduino Diecimila</a></li>
	<li><a title="Arduino Ethernet Shield from Cool Components" href="http://www.coolcomponents.co.uk/catalog/product_info.php?products_id=232">Arduino Ethernet</a></li>
	<li><a title="BlinkM - I2C Controlled RGB LED from Cool Components" href="http://www.coolcomponents.co.uk/catalog/product_info.php?products_id=132">Blink-M light</a></li>
	<li>A lampshade from B &amp; Q</li>
</ul>
The fact that we could even make this, with me generally not being big on writing in any languages that feel like C, and with James being almost completely new to the platform is a testament to how lego-like the Arduino ecosystem is getting now.

When we take the shade off the lamp, it’s quite a bit easier to see how it all works:

<a title="Tealight working without the globe by chris.d.adams, on Flickr" href="http://www.flickr.com/photos/daggi/3472190903/"><img src="http://farm4.static.flickr.com/3657/3472190903_a004dcaf5d.jpg" alt="Tealight working without the globe" width="500" height="333" /></a>

The orange cable is a ethernet cable, and the grey one is the usb power, running off a spare iPod I had lying around.

The code has largely been a messy cut and paste job spliced from number of sources, but mostly from this <a title="Arduino Forum - Parse XML to Extract Weather Data from Web" href="http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1231812230">thread in the arduino forums</a>, and the string parsing code example <a title="string to float - Page 2 - C" href="http://www.daniweb.com/forums/showthread.php?p=640773">is from a post by Jeff Tanner here on the daniweb forums</a>.

This isn’t really big enough to be considered a project on github, so I’m just chucking a gist up for now:

<script src="http://gist.github.com/101553.js"></script>

<h3 id="isn8217t_this_massively_oversimplifying_and_trivialising_the_whole_concept_of_demand_smoothing">Isn&#8217;t this massively oversimplifying and trivialising the whole concept of demand smoothing?</h3>

<p>You could argue so, yes. </p>

<p>But placing it in a relatively high traffic co-working space, full of people working in totally unrelated fields is a great opportunity to speak to them about the ideas inspiring this little toy, and get lots of interesting feedback, and see how best to communicate on issues related to climate change and how massively energy intensive our life styles are.</p>

<h3 id="but_why_tea">But why tea?</h3>

<p>A number of reasons:</p>

<ul>
<li><p>they provide a recognisable power spike for comparing against national averages, and also for graphing against national load averages too. It makes it easier to see if behaviour is changing.</p></li>
<li><p>there&#8217;s a pattern to making hot beverages at work, but it&#8217;s pretty easy to timeshift it, without getting into emotive issues like calling people utter carbon bastards for flying to Spain on holiday.</p></li>
<li><p>it&#8217;s a usefully mundane , which makes explaining why changing behaviour here could work to smooth out demand on the national grid, meaning the oldest, dirtiest power stations don&#8217;t need to be powered up just so everyone can have a cup of tea at the same time.</p></li>
<li><p>because a good pun is its own reword.</p></li>
</ul>

This builds on ideas and hacks developed by <a href="http://knolleary.net">Nick O'Leary</a> at IBM, <a href="http://www.torchbox.com/">Tom Dyson at Torchbox</a> <a href="http://www.joeshort.net/">Joe Short from Demand Logic</a>, and presented at the last Homecamp. I really wish I was going, but I have a day of letter writing ahead of me instead for Saturday. 

Which after this weekend, will be the subject of another post.

