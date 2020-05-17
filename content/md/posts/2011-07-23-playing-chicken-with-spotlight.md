

{:author "admin", :title "Playing chicken with spotlight on a fanless macbook", :date "2011-07-23 21:59:24", :publish-date "Sat, 23 Jul 2011 21:59:24 +0000"}



<!-- content below -->

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/07/Screen-shot-2011-07-23-at-22.37.06.png">
</a>So, last week, when working on the laptop at home, I heard the last thing you want to hear on a laptop - a nasty crunchy whirring grinding noise coming from inside the macbook, that sounded like the hard drive diving a horrible, rotating circular death.

Not what you want to hear, when you haven't backed up for a couple of weeks.

Fast forward a week, and a new replacement disk later, and it turns out the problem area was a mangled fan.

Cue me feeling rather sheepish about the replacement 256 Gb SSD I just ordered.

### Solid state black macbook.

Right now, I'm my macbook is damn near silent - the are no whirring spindles, and crucially, with no fan, there are no moving parts to make any other noises.

However, until that replacement fan arrives, using this computer has taken on a comical element, where I need to work with `top` open in a window, and an eye on the CPU temp at all times, to kill CPU hungry processes, before they cook the laptop.

One real killer here is spotlight; before I had caught it the first time, it was well on it's way to monstering both cores on the macbook, taking the internal temperature to more than 90C (!) before I shut the machine down to stop any damage occurring.

Even renicing it to give the process a lower priority didn't help (I'm not sure why, one for another day's research).

Since then, I've found a handy one liner here, to stop automatic indexing, which I'm sharing here in case anyone finds themselves in a similarly ridiculous condition.

### How to kill the Spotlight Index before it kills your macbook

Run this command in a terminal, and spotlight will no longer index content on your mac:
<pre lang="bash">sudo mdutil -a -i off</pre>
Once you've fit a replacement fan inside your machine, you can switch it back on with this incantation below:
<pre lang="bash">sudo mdutil -a -i on</pre>
### That fan can't arrive quick enough

Just to state the obvious - what I'm doing here is very risky, and probably quite stupid, without early warning software like Bjango's istat pro.

This provides more stats than I could ever want about the internals of my machine, and that, combined with constantly open terminal, means that I can usually `kill -9` runaway processes before they cook this laptop. Below are a few screengrabs of the temp stats iStat pro gives you from the menu bar, along with an example of the difference in CPU usage before and after killing the spotlight indexer:

&nbsp;

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/07/too-hot.png"><img class="alignleft" title="too hot" src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/07/too-hot.png" alt="" width="252" height="667" /></a>

&nbsp;

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/07/phew.png"><img title="phew" src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2011/07/phew.png" alt="" width="188" height="566" /></a>

&nbsp;

&nbsp;

&nbsp;

Let's hope this isn't the last blog post on this macbook - it's been going strong since 2008 now, and I've grown pretty attached to it...

