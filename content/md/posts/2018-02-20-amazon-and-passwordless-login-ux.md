

{:author "mrchrisadams", :title "Amazon and passwordless login UX", :date "2018-02-20 13:05:37", :publish-date "Tue, 20 Feb 2018 13:05:37 +0000"}



<!-- content below -->

I signed into the German Amazon Retail site, today, and I saw a new sign-in flow. Being a UX nerd, I took photos and immediately took to twitter.

Here's what I saw.

<h3>Look! Only one thing being requested!</h3>

The first change is that like Google, and Eventbrite, they only ask for one thing per page now.

This roughly translates as 'login' , and 'email address or phone number', then 'continue'/

<img class="alignnone size-full wp-image-2852" src="https://mrchrisadamsblog.files.wordpress.com/2018/02/screen-shot-2018-02-20-at-13-24-20.png" alt="Screen Shot 2018-02-20 at 13.24.20" width="1088" height="894" />

<h3>Next! No password requested!</h3>

<img class="alignnone size-full wp-image-2853" src="https://mrchrisadamsblog.files.wordpress.com/2018/02/screen-shot-2018-02-20-at-13-24-47.png" alt="Screen Shot 2018-02-20 at 13.24.47.png" width="1088" height="894" />

Sometimes you might get the option to sign in with a password, but Amazon is also testing this as way in, where they send an email with a one-time-use login code to your email address instead of asking for your password. This is good, as most of us have terrible password hygiene (not <em>you </em>obviously though<em> -</em> I know <em>you</em> use a password manager, but the chances you have family members who don't, and also use the Amazon website)<em>. </em>

<h3>A one time code, sent to your email, instead of a password</h3>

<img class="alignnone size-full wp-image-2854" src="https://mrchrisadamsblog.files.wordpress.com/2018/02/screen-shot-2018-02-20-at-13-25-00.png" alt="Screen Shot 2018-02-20 at 13.25.00.png" width="903" height="596" />

What you get sent to your address is this - the one time code, and some reassuring copy about taking your security seriously. Interestingly though - there's <em>no link to click to get to Amazon at all</em>. This feels like a good anti-phishing pattern.

I'm happy sharing a one time code in a screenshot here, because well… it's a one time code - you can only use it once. You might be able to social engineer access if you called Amazon, and said this code wasn't working, but the solution I hope they would give would be to tell me to generate a new code, or go through some escalated process to prove who I was.

<h2>Why I like this</h2>

As I mentioned before, most of us are terrible at managing passwords, so moving us away from relying on terrible passwords as a default as feels like a win.

<h2>Things I wish it did - chunking</h2>

<img class="alignnone size-full wp-image-2855" src="https://mrchrisadamsblog.files.wordpress.com/2018/02/screenshot_20180220-135056.png" alt="Screenshot_20180220-135056.png" width="1080" height="1920" />

I don't understand why these services don't chunk numbers longer than 3 digits to make them easier to read, or type in.

As an example, Google Authenticator does this chunking trick, and I think it makes it easier to read the numbers.

Well… it's not just me that thinks it makes it easier - this is not a new technique, and there is a <a href="https://www.interaction-design.org/literature/book/the-glossary-of-human-computer-interaction/chunking">paper from 1956 that explains how it helps with human computer interaction.</a> There's also some recent, <a href="https://www.nngroup.com/articles/chunking/">good advice on when and how to apply chunking from the Neilsen Norman group.</a> It's not a new idea, and there are peer reviewed academic papers to help justify using the technique.

<h3>How many people are getting this?</h3>

I'm curious if this is a widespread experiment - if you see it too, and have opinions on it, let me know.

Also, I'm considering writing a piece about the common pitfalls when implementing passwordless logins, based on my own experience over the last few months. If I get say… 15 faves/likes, it'll justify me writing a more in-depth article, as it turns out there are quite a few non-obvious pitfalls along the way.

https://twitter.com/mrchrisadams/status/965914733772771328

&nbsp;

&nbsp;

&nbsp;

&nbsp;

