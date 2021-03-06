

{:author "mrchrisadams", :title "So, we ended up at a democracy themed hackday thing", :date "2017-09-04 09:06:20", :publish-date "Mon, 04 Sep 2017 09:06:20 +0000"}



<!-- content below -->

<em>Earlier in August I wrote a post about the BPB, a German institute focussed on promoting democracy, and <span style="font-weight:400;">WhoTargetsMe, a project to bring more transparency to election campaign advertising on Facebook. </span>After sharing the post online, I had a few people contact me about forming a group to work at an Democracy is Everything, a hackathon at Factory Berlin, in Mitte in Berlin.</em>

<em>Here's how we got on, and some notes for other people thinking extending a project at a hackday like this in future…</em>

I've been going to hackdays and hackathons since 2007, (although to be fair, <em>much</em> less frequently after I entered my thirties, five years ago…), and the format has usually been something along the lines of:

<ol>
    <li>think up a project, usually at the hackday, or maybe a little bit before it starts</li>
    <li>meet people, see who you can imagine building something with</li>
    <li>work out who is supposed to be doing what</li>
    <li>realise how little of what you've doing will fit into the time available and update plan</li>
    <li>build much less than you thought, and think how to present it</li>
    <li>present it</li>
    <li>curse self at missing key points in in the minute or two you have to present it</li>
</ol>

This one was different a in few interesting ways:

<h4>Wait, I need to apply?</h4>

<span style="font-weight:400;">While I’ve seen a few events where you pay to go to an event like this (which I think is at best pretty cheeky if you have sponsors), this is the first event I’ve been to where you needed to apply to go, and have an idea beforehand.</span>

<span style="font-weight:400;">While this makes an event less approachable for individuals and takes the focus away from meeting new people, it had some interesting effects. It forced me think more about what could be done in the time available, and what the ideal makeup of a team to do this might be, in a way I haven’t had to before.</span>

<h4>Extending a existing project</h4>

<span style="font-weight:400;">This is also the first time I’ve worked on an extending an existing project, rather than try to come up with a new one, and also one where I hadn’t ever met the most visible project author.</span>

<span style="font-weight:400;">This added another new dynamic: whatever you think you can do in the time available, you need to have some idea of how useful it would be to the maintainers of the project if you want it to last beyond the hackday. I’ll touch on this later.</span>

<h2>What we did</h2>

If you're not familiar with <a href="http://whotargets.me">whotargets.me</a>, it's a browser extension that counts the political ads in your Facebook feed, and based on this information, gives you some charts and analysis about how different political parties target you to for your vote during an election. <span style="font-weight:400;">By using it, you help build a dataset of how political parties are using the Facebook platform to advertise voters. This dataset can then be used to help inform public discourse, and eventually policy. </span>

Here's how the site looked before the hackday:

[caption id="attachment_media-22" align="alignnone" width="3030"]<img class="alignnone size-full wp-image-2116" src="https://mrchrisadamsblog.files.wordpress.com/2017/09/screen-shot-2017-08-26-at-15-12-27.png" alt="Screen Shot 2017-08-26 at 15.12.27.png" width="3030" height="1978" /> What am I downloading, and what does it do?[/caption]

<span style="font-weight:400;">This wasn’t immediately obvious when you first visited the page though – you were prompted to download a browser extension without understanding what it was really going to do. Germany is known for different attitudes to personal data to the UK, and this seemed a big turn off to a number of Germans we showed it to, so we had a couple of main goals for the hackday:</span>

<ol>
    <li>Make it work in Germany</li>
    <li>Make it clearer what it does</li>
</ol>

I'll explore these in more detail below:

<h3>Making it work in Germany</h3>

<span style="font-weight:400;">WhoTargetsMe originally comes from the UK, which has a much more centralised tradition of campaigning than Germany – a nice example of this is the story where a conservative campaigner told me how Tory MPs are essentially barred from even retweeting without central HQ’s permission. I think this is also an artefact of how election financing in the UK places hard limits on online spending in local campaigning, but in in 2016 at least, doesn’t really have limits on national campaigns.</span>

<span style="font-weight:400;">This centralisation is different to Germany, partly because Germany is split into a series of Länder (it’s not totally accurate, but it can help to think of them as states), but also because there are comparatively more parties and decentralised campaigning as a result. Fortunately for us though, in Germany online campaigning with Facebook is less established, so it’s not unreasonable to think that campaigning will start out similarly centralised at first, because that’s where the expertise and budget to run a campaign might be in the main parties.</span>

<span style="font-weight:400;">In the long run through, it’s likely that as campaigning digitally becomes more commonplace, you’d have many, many more advertisers to keep track of – I know in Kreuzberg/Friedrichshain where I live, at least one party in this area is already  experimenting with Facebook ads like this.  To this end, we did a fair amount of research in the group for this, and found a load of useful datasets to help with matching ads to politicians and parties, but we didn’t pursue this further during the weekend event for time reasons.</span>

<span style="font-weight:400;">I’ll explore this in a future post, which I’ll link to when it’s online, as I think it has an impact on projects like this in the long run.</span>

<h3>Making it clearer what it does</h3>

<span style="font-weight:400;">If you look at the whotargets.me front page for Germany or for the UK, you’ll see more info on what the whotargets.me browser extension is, and what it does – I’ve taken a screenshot below (the actual wording from the hackday has been tweaked a bit, but the general idea is the same):</span>

<img class="alignnone size-full wp-image-2207" src="https://mrchrisadamsblog.files.wordpress.com/2017/09/screen-shot-2017-09-02-at-23-14-15.png" alt="Screen Shot 2017-09-02 at 23.14.15.png" width="1694" height="1474" />

<h4>Getting a different point of view</h4>

<span style="font-weight:400;">The screenshot above is clearly a different style to the previous look for the site with the black and white photo of the Reichstag (the German equivalent to the House of Parliament).  In using illustrations like this instead, we were trying to capture some of the mood of democracy being a messy process driven by ultimately by people, rather than faceless institutions, and make the project feel more approachable than before.</span>

<img class="alignnone size-full wp-image-2241" src="https://mrchrisadamsblog.files.wordpress.com/2017/09/screen-shot-2017-09-03-at-19-34-41.png" alt="Screen Shot 2017-09-03 at 19.34.41.png" width="2794" height="1504" />

<span style="font-weight:400;">These are largely thanks to the illustrator on our team, <a href="http://www.judithcarnaby.com/">Judith Carnaby</a>, who was introduced to me by <a href="http://alicero.se">Alice Rose</a>, who helped tidy up the copy and some of the React code in the plugin itself. The two of them being much more comfortable in German than me, and us having a native German speaker in <a href="https://twitter.com/krasch_io">Katarina Rasch</a> really helped here.</span>

<h4>Explaining how the data is used</h4>

In Germany, people tend to be a bit more wary about how data that might identify them is used than the UK - it's not clear how it's used, they often will flat out refuse to use a service. So, we also ended up writing some more about how it works once we had a chance to speak to <a href="https://twitter.com/LouisKnightWebb">Louis Knight-Webb</a> (one of the co-founders of the project) over slack at the hackday.

<span style="font-weight:400;">There’s few more details being finalised, but that this info should be available on the main site soon, with some helpful diagrams – in the meantime, this should be visible in tweaks to copy throughout the app that should make it clearer what is happening with adverts, and what data is used in them.</span>

<h3>If you want to extend a project at a hackday like this in future</h3>

<span style="font-weight:400;">First of all, it is possible, and all in all, I feel it worked out pretty well – I’d totally do this again, rather than try to re-invent the wheel. There’s a few things worth bearing in mind though.</span>

<h4>Access to at least one member of the original team is important</h4>

<span style="font-weight:400;">I had about 3 hours of skype calls with Louis before starting the hackday to understand the existing project, and we spent quite some time talking about was realistic to attempt in the time we had. We cut back a lot of scope in these calls, and without them I’m pretty sure we’d have wasted a lot of time trying things that we’d realise only later weren’t feasible.</span>

<span style="font-weight:400;">During the hackday itself, we had a slack channel open which Louis was in, which also helped massively – at one point on the Friday night, we realised were going in pretty different directions to the rest of the how the project was communicated, and catching it comparatively early saved some awkward moments the following day.</span>

<span style="font-weight:400;">Louis made himself very available, but if I was doing this again, I’d probably sort out some pre-agreed time slots to answer questions, as being on call over a weekend might not be everyone’s idea of fun…</span>

<h4>Typical hackday style rules about pitching change</h4>

<span style="font-weight:400;">If you’ve been to any hackday style event, it’s common to see “Pitch-Driven Development”, where you might start with a what you aim to present, then work backwards, only building the bits that will be in a presentation. Doing this in theory saves time spend on login systems, proper backends, and so on, in favour of visible features, that increase the chances of your presentation impressing judges and winning. The implication here is that if you don’t win, your effort was more or less wasted, and it has no life beyond the hackday.</span>

<span style="font-weight:400;">In our case, we had a real working product that we were trying to adapt to a new region, so even if we didn’t catch the eye of the judges, it would still need to be useful, so this didn’t apply in the same way.</span>

<span style="font-weight:400;">At the same time, part of the value of events like this is the coverage for a project if your team DOES win, and the doors it opens to help meet people who can help the project later. So, if you make it all about your contribution to a project than the project itself, you run the risk of everyone you present it to missing the bigger picture.</span>

<span style="font-weight:400;">Finally, there’s the ethical aspect – misrepresenting what you actually achieved during an event when there’s at least some expectation of it being a fair competition isn’t cool, and will almost definitely come back to bite you.</span>

<h5>Videos over presentations in future?</h5>

<span style="font-weight:400;">Quite late in the day, we realised that the visible changes to the site may not be all that easy to show during the ridiculously short two minute window we had for presenting, so we ended up with some frantic last minute changes to what we showed off.</span>

<span style="font-weight:400;">If we were to do this again, and if we were confident we could show a video, I’d probably rely on putting together a video of what we had made for our two minute slot, rather than put together a short lived presentation for the judges. If we did this, we’d be able to make more use of it after as support material in blogposts too.</span>

<h3>Worth a spending a weekend</h3>

<span style="font-weight:400;">In the end, I’m pretty happy with what we got together during the Friday and Saturday we had, and it was a lovely surprise to come third place.</span>

Big thanks to Alice, Judith, Kat, Nick, Louis, Brian, and the rest of the whoTargets.me team 👍🏽

[caption id="attachment_2356" align="alignnone" width="1600"]<img class="alignnone size-full wp-image-2356" src="https://mrchrisadamsblog.files.wordpress.com/2017/09/img_20170826_185904.jpg" alt="IMG_20170826_185904" width="1600" height="1200" /> Triumphant faces - some of us even picked up some useful swag out of this hackday…[/caption]

<h3>How you can find out more about Who Targets Me</h3>

If you're in Germany and you've read this, I think you should visit <a href="http://whotargets.me">whotargets.me,</a> and try installing it on your browser to help us build a decent dataset to add some transparency to how political ads are used in elections.

If you're technically inclined, the <a href="http://github.com/whotargetsme">code repo for the browser extensions is on github.</a>

There's an <a href="https://whotargets.me/en/targets-deutschland-updates-germany/">official write up on the whotargets me blog</a>, added by Louis.

If you read German, <a href="https://www.buzzfeed.com/darkads">this microsite on Buzzfeed about WhoTargets.me and Dark Ads</a> (these political ads this project was all about) is also a good resource.

If you're in Berlin and want to chat to one of us, I live in Berlin, but Louis is in town all of this month, and probably the best person to speak to about the project  - he's <a href="https://twitter.com/LouisKnightWebb">@LouisKnightWebb</a> on twitter.

&nbsp;

&nbsp;

&nbsp;

