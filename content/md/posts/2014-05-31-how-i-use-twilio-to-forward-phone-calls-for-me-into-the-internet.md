

{:author "admin", :title "How I use Twilio to forward phone calls for me into the internet", :date "2014-05-31 23:42:45", :publish-date "Sat, 31 May 2014 23:42:45 +0000"}



<!-- content below -->

As I've mentioned in previous posts, I am a new resident of Berlin, after living almost all of my life in London. Also, almost all my family is still in Blighty, as are almost all of the people I work with in my day job.

In a given day, I'll rely on [Google Hangouts](http://www.google.com/hangouts/), [Skype](skype.com), [IRC](irccloud.com), [Slack](https://slack.com/) and [Hipchat](http://hipchat.com/) to stay in touch, and conduct video and voicecalls on my ipad or laptop. When I need to call UK numbers, my easiest option is to use Skype to call, using SkypeOut (now simply referred to as "[Calls to mobiles and landlines](http://www.skype.com/en/features/call-phones-and-mobiles/)")

### Getting around unreliable connections

Sometimes however, you if you're somewhere with a poor upstream connection to the internet, the sound quality on voice calls like can become unacceptably poor.

This tends to happen more with Skype than Hangouts for me during the week, but is common enough to make using it at times, untenable.

If you don't have a landline where you are, then you're reduced to relying on a mobile phone to call another country, which is rarely a cheap way to call someone, nor for them to call you.

### Bouncing phone calls into the internet with Twilio

Recently, I tried to solve this problem with Twilio, and it's worked well enough so far to share here. At a glance, here the steps you need to take to do this:

1. Buy a UK number with Twilio
1. Register with Twilio to make international calls
1. Setup a forward inside Twilio to your local phone number
1. Receive phone calls on the UK number, and pick up on your German mobile

There is a cost to this - you pay a monthly fee to have a UK number, and you still need to foot the bill for forwarding the phone call to your mobile in your own country. However, this is usually cheaper making a single phone call of any length from a mobile to another country.

### Interested? Here's how to do it for yourself.

#### Buy a UK number

Once you're registered with Twilio, the first step is to buy a number, for the country you want to people to call:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2014/05/Twilio-User-Account-Phone-Numbers-Available-GB-Local.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2014/05/Twilio-User-Account-Phone-Numbers-Available-GB-Local-1024x621.png" alt="Twilio User - Account Phone Numbers Available GB Local" width="604" height="366" class="alignnone size-large wp-image-977" /></a>

#### Register for international calls

At this point, it's possible to forward calls people make to this number, to another number in the same country. If you try to forward a phone call to a phone number in another country, you'll end up with a failed call, and the twilio logs will show an `Warning: 13227 - Dial: No International Authorization` error.

You need to authorise international calls by filing a ticket - this part is a bit clunky, but your request is answered quickly. I file one evening, and had it approved the following morning.

#### Set up a forward to your local phone number

Assuming you've been able to activate international calls, the next step is to use the Twilio API itself to connect someone calling your UK twilio number to a phone of your choice.

To do this, I suppose you *could* write a simple Sinatra style webapp, that posts to relevant endpoints of Twilio's API, then deploy that to heroku for free.

An easier way to do this is, is to just use a [Twimlet](https://www.twilio.com/labs/twimlets), a pre-built PHP app, that uses the Twilio API to make a phone call to the number you set, when you fill in the details at the [Twilio Forward page](https://www.twilio.com/labs/twimlets/forward).

Your twimlet url generated should look something like the number below:

    # My real number has been replaced with xxx's in this example
    http://twimlets.com/forward?PhoneNumber=+49160xxxxxxxx&CallerId=+447974xxxxxx

You add it to your number listing when logged into Twilio, like so:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2014/05/Phone-Number-442033225777-Dashboard-Twilio.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2014/05/Phone-Number-442033225777-Dashboard-Twilio-1024x788.png" alt="Phone Number 442033225777 | Dashboard | Twilio" width="604" height="464" class="alignnone size-large wp-image-978" /></a>


#### Receive phone calls on the number, and pick up whereever you redirect it to

Now, when someone rings the number you registered with Twilio, it triggers a POST to the Twilio API endpoint responsible for starting a phone call, and connects the caller to the number you've specified to dail.

Because you're relying on a voice network, rather than unpredictable wifi, phone calls should have a more consistent sound quality, and it becomes much easier and cheaper for people to call you if they need to.

This whole exercise assumes the mobile you're forwarding calls to is in an area of reliable mobile coverage - but assuming a) you have that, b) there's no convenient bolt-on tariff for your phone contract and c) roaming and international calls are still unreasonably expensive, this seems to work fairly well so far.

So now you know.



