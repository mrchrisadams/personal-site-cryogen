

{:author "mrchrisadams", :title "Dear Developer, go read \"Dear Developer\"", :date "2018-04-06 14:49:31", :publish-date "Fri, 06 Apr 2018 14:49:31 +0000"}



<!-- content below -->

<i>I've just finished reading through Charlie Owen's converted-webpage-from-a-talk thing, Dear Developer. It's funny, friendly and really captures the wonder of the web as a medium to work with. Without picking fights, it steers developers away from a lot of bad practices, and towards ones which are more empathetic, resilient and performant. In this post I share a few gems that stood out.</i>

<h3>The web as a resilient technology</h3>

If you've developer with the web much over the last few years, you can't help but notice a trend towards pages becoming brittle. I mean this in the sense that if there's an error in the javascript, or a resource like a javascript file doesn't load in time, the page is essentially unusable.

She shows a really nice example by using Firefox's DOM inspector to take a page apart, and have it still work. Here's the quote below, but the link to <a href="https://hyp.is/VMx0pjmlEeijpCfeEnpHBw/sonniesedge.co.uk/talks/dear-developer">the section via hypothesis of the page is here and shows the video:</a>

<blockquote>It is this flirty declarative nature makes HTML so incredibly robust. Just look at this video. It shows me pulling chunks out of the Amazon homepage as I browse it, while the page continues to run.

Let’s just stop and think about that, because we take it for granted. I’m pulling chunks of code out of a running computer application, AND IT IS STILL WORKING.

Just how… INCREDIBLE is that? Can you imagine pulling random chunks of code out of the memory of your iPhone or Windows laptop, and still expecting it to work? Of course not! But with HTML, it’s a given.</blockquote>

<h4>The pyramid of robustness</h4>

I really like the visual device, the Pyramid of Robustness she uses for this too

[caption id="attachment_2960" width="1920"]<img class="alignnone size-full wp-image-2960" src="https://mrchrisadamsblog.files.wordpress.com/2018/04/pyramid-of-robustness.jpeg" alt="Pyramid of robustness" width="1920" height="1080"> Pyramid of robustness[/caption]

It's a deft way of presenting the downsides of building assuming javascript is always working, and there being a fast enough connection to download all the resources on a page quickly:

[caption id="attachment_2961" width="1920"]<img class="alignnone size-full wp-image-2961" src="https://mrchrisadamsblog.files.wordpress.com/2018/04/pyramid-upside-down.jpeg" alt="The Pyramid of Robustness, upside down" width="1920" height="1080"> The Pyramid of Robustness, upside down[/caption]

There's a really good visual gag here that made me guffaw in the silent section of the coworking space I was in when I read it first. I won't spoil it for you.

<h3>Getting started with a11y and why it's important.</h3>

There's a nice part about getting started with accessibility or (a11y) to it's friends, and how to do this easily on a mac.

You just hit command+f5 to start voice-over, and you can start navigating content the same way someone who is partially sighted, or blind would.

It also covers <i>why </i>it's important. Accessibility is often mischaracterised as designing for blind people, and as a sighted person, it's often thought of as the key reason (I'm guilty of this in this section myself).

It's the right thing to do, but it's also worth thinking about this in terms of a design being resilient - people can be temporarily disabled when they injure themselves or even when they're just holding something in one arm, like a bag of shopping or a child. <a href="https://www.microsoft.com/en-us/design/inclusive">The persona Spectrum from Microsoft</a> is a good example of this.

[caption id="attachment_2962" width="1700"]<img class="alignnone size-full wp-image-2962" src="https://mrchrisadamsblog.files.wordpress.com/2018/04/screen-shot-2018-04-06-at-16-46-31.png" alt="Screen Shot 2018-04-06 at 16.46.31" width="1700" height="1416"> Microsoft's Persona Spectrum for inclusive design[/caption]

When it's presented like this, it reframes a11y as not being a question of charity or guilt, but being one of pragmatism and professionalism.

Framing it like this in terms of positive, intrinsic motivation makes it feel more likely to be adopted.

There's a nice quote from Theo Schlossnagle from Circonus that I feel captures this idea - he uses it in the context of hiring, but it's stayed with me ever since I heard it:

<blockquote>
<h4>I don't want programmers, I want professionals<i>.</i></h4>
</blockquote>

If we want to call ourselves software engineers and act like we're a grown-up profession, then we should hold ourselves to the standards engineers and other professions hold themselves to.

And that means to acknowledge the full range of contexts the products and services we create are used in.

<h3>Go take the time to read it</h3>

I'm when speaking to people who want to learn to code for the web, I think I'm going to point them to this as a thing to read for understanding why the web is magical.

If you haven't read it yourself yet, I <i>strongly </i>recommend checking it out.

See? It's even got a nice short url - <a href="https://sonniesedge.co.uk/talks/dear-developer">go read it now.</a>

<a href="https://sonniesedge.co.uk/talks/dear-developer">https://sonniesedge.co.uk/talks/dear-developer</a>

