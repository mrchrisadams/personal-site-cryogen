

{:author "mrchrisadams", :title "How much CO2 can you save when you remove ad-tracking from news sites?", :date "2018-05-27 15:29:05", :publish-date "Sun, 27 May 2018 15:29:05 +0000"}



<!-- content below -->

<em>Now that GPDR has landed, we're seeing companies serving EU specific versions of their site to EU users, which in some cases, serve a user experience which is cleaner, simpler and faster loading.</em>

<em>Some are </em>much<em> smaller over the wire too. So, because moving data uses servers,and those servers use electricity, and that electricity usually comes from burning coal, I've had a go at doing some basic calculations to work out what the CO2 reductions might be if these became the norm.</em>

<em><strong>TLDR - </strong>For a site like USAtoday,</em> <em>it looks like running the 'GPDR-lite' version as the default would represent CO2 emissions savings equivalent to an entire European persons's annual carbon footprint, each month.</em>

<h3>How I arrive at these numbers</h3>

I need to stress right at the beginning - these figures I'm about to share are very rough, and I don't pretend that they're in any final, accurate form at all.

I'm hoping to share this to help get a better idea for how you might work out the CO2 emissions associated with transferring data in a more rigorous fashion,  but also because I think these emissions are worth discussing, and I can't find any numbers like this online yet.

<h3>First, our smaller site:</h3>

Let's take Hadley's tweet here - she's referring to a the EU specific version of the USA Today site, which is about 500kb, compared to the full size, ads and tracking site which weighs in at 5mb site instead:

https://twitter.com/hadleybeeman/status/1000435217109278721

What kind of energy footprint does this represent? Let's take a rough estimate of the total daily traffic <a href="https://www.easycounter.com/report/usatoday.com">for the USAToday from EasyCounter</a> (we could use Alexa if we wanted to pay for more accurate traffic results)

<img class="alignnone size-full wp-image-2990" src="https://mrchrisadamsblog.files.wordpress.com/2018/05/screen-shot-2018-05-27-at-16-45-50.png" alt="Screen Shot 2018-05-27 at 16.45.50.png" width="2130" height="1006" />

Looking here, we get 3.77 million daily page views.

So, if we wanted an <em>idea </em>of daily bandwidth, we might multiply page size by daily page views.

So, lets take a 5MB page, and multiply it 3.77 million times to represent the page views.

This gives us a figure, that, when we round it to the nearest one hundred gigabytes, is about <strong>18,400 gigabytes of data per day.</strong>

<h3>How much energy is that?</h3>

Now, it's been <em>really hard</em> to find reliable numbers to convert bandwidth to energy usage when I've looked before, but the <a href="http://www.koomey.com/post/165024508933">best freely available figures I've found are from work I found via Jonathan Koomey's blog</a>, where he shares something like this:

<em>This article derives criteria to identify accurate estimates over time and provides a new estimate of <strong>0.06 kWh/GB</strong> for 2015. By retroactively applying our criteria to existing studies, we were able to determine that the electricity intensity of data transmission (core and fixed-line access networks) has decreased by half approximately every 2 years since 2000 (for developed countries),</em>

So, this is semi-throwaway blog post and it's a Sunday, and so for the purposes of getting a ballpark figure, I'm going to cheat and just project forward two years to 2017, and say 2018 is close enough to 2017 for me to use <strong><em>0.03 kWh/GB</em>.</strong>

<h3>Okay, how much carbon dioxide is that?</h3>

For a ballpark figure like this, we'd take the total energy needed to transfer our 18,400 gigabytes per day, then multiply that by our 0.03 kilowatt hours per gigabyte, then multiply <em>that</em> by the CO2 emissions per kilowatt hour.

<h4>Let's get our CO2 per kilowatt hour figure so we can do this</h4>

In the US, where most of the USAToday audience is likely to be, a fair amount of coal is used to generate power, so when I was dumping some numbers into this jupyter notebook, I made a guesstimate figure of <strong>0.45 kilograms of CO2</strong> emitted per kilowatt hour of electricity generated.

After checking it against the <a href="https://emissionsindex.org">emissions index website to check against some actual numbers</a>, it turns out I was off, but not <em>that</em> far off.

Their figure is 432 kilograms per megawatt hour, which is about <strong>0.43 kilograms of CO2 per kilowatt</strong> <strong>hour</strong>.

<img class="alignnone size-full wp-image-2991" src="https://mrchrisadamsblog.files.wordpress.com/2018/05/screen-shot-2018-05-27-at-16-56-42.png" alt="Screen Shot 2018-05-27 at 16.56.42.png" width="1604" height="1238" />

I've been rounding at each stage here, to make it a bit easier to keep the numbers a bit easier to remember.

However, I'm going to pull the <a href="https://github.com/productscience/planet-friendly-web/blob/master/binder/co2-savings-usatoday-gdpr.ipynb">actual number from the jupyter notebook</a>, which when rounded again, gives us <strong>248.5kg of CO2 per day, or a little under 7.5 tonnes per month more or less.</strong>

<h3><strong>Translating this into something  more tangible</strong></h3>

If we had the lighter, GPDR friendly, ad-and-tracking-free version of the site as the norm, if we just looked at the bandwidth savings, then we'd be saving something like <a href="http://databank.worldbank.org/data/reports.aspx?source=2&amp;series=EN.ATM.CO2E.PC&amp;country=#">the annual carbon footprint of a typical European, according to the World Bank</a>, every month.

Or if you prefer, something like <a href="https://co2.myclimate.org/en/portfolios?calculation_id=1171584">a flight between New York and Chicago every day</a>.

If this is interesting to you, there's some more <a href="https://github.com/productscience/planet-friendly-web/blob/master/binder/co2-savings-usatoday-gdpr.ipynb">in this jupyter notebook on github.</a>

<h3>Plug time - the planet friendly web guide</h3>

I'm looking for people to work with and explore this kind of stuff with me.

Why?

Well, I work in tech, and it seems like loads of our existing tools, and practices can be re-purposed to bring about reductions in CO2 emissions in our industry AND make the digital products we create work better for our users.

If you design infra for services,where you source power, and how you provision your resources, to match your use (i.e. scaling) has an impact.

If you design clients, or apps, then how send data over the wire has an impact (i.e. WPO, et al).

If you design the business model, or how you get feedback from stakeholders, or how you travel to do all this, then decisions you make here have an impact too.

<h4>Let's chat</h4>

If this is interesting, please do get in touch, as I'm trying to:

<ol>
    <li>get a free, open source guide together around the subject at <a href="http://planetfriendlyweb.org/">planetfriendlyweb.org</a></li>
    <li>prototype a workshop (one remote, one in Berlin), to help organisations identify where they can make these reductions (and usually, save money or reduce waste along the way)</li>
</ol>

My <a href="https://blog.chrisadams.me.uk/contact/">contact page lists the usual ways to reach me</a>, and if the guide seems fun, <a href="http://planetfriendlyweb.org/contributing">there's a contributor page there too</a>. T

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

