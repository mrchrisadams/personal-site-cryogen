

{:author "admin", :title "My latest reason for wanting to scoop IE7's eyes out with a sharpened spoon.", :date "2009-01-09 19:13:02", :publish-date "Fri, 09 Jan 2009 19:13:02 +0000"}



<!-- content below -->

When we're developing for the web, adapting for Interet Explorer is an unavoidable pain that we have to deal with.

But it's rare to find a problem that rears its ugly head in Internet Explorer 7, but not its much maligned predecessor Internet Explorer 6. We're trained by experience to expect IE7 to know better, albeit only slightly.

However,  I recently learnt that this isn't always the case; IE 7 throws its toys out the pram if you dare set a width on the on the main html element on a page like so:
<pre><span style="font-family: Georgia; line-height: 19px; white-space: normal; ">&lt;</span>html&gt;</pre>
<pre></pre>
<pre>&lt;style type="text/css" media="screen"&gt;</pre>
<pre>html{</pre>
<pre>width:700px;</pre>
<pre>margin: 0 auto;</pre>
<pre>background:#444;</pre>
<pre>}</pre>
<span> </span>
<pre><span style="font-family: Georgia; line-height: 19px; white-space: normal; ">b</span>ody{</pre>
<pre>width:650px;</pre>
<pre>margin: 0 auto;</pre>
<pre>background:#eee;</pre>
<pre>padding:18px;</pre>
<pre>}</pre>
<span> </span>
<pre><span style="font-family: Georgia; line-height: 19px; white-space: normal; ">#</span>wrapper{</pre>
<pre>width:550px;</pre>
<pre>margin: 0 auto;</pre>
<pre>background:#435434;</pre>
<pre>padding:18px;</pre>
<pre>}</pre>
<span> </span>
<pre><span style="font-family: Georgia; line-height: 19px; white-space: normal; ">&lt;</span>/style&gt;</pre>
<pre></pre>
<pre>&lt;body&gt;</pre>
<pre> &lt;div id="wrapper"&gt;</pre>
<pre><span style="white-space:pre"> </span>Yammer yammer</pre>
<pre> &lt;/div&gt;</pre>
<pre>&lt;/body&gt;</pre>
<pre>&lt;/html&gt;</pre>
 

Do this, and you'll find your layout clings to the leftmost side of the browser window in IE7, for no good reason.

But look at it in IE6, Opera, Safari or Firefox, and you'll see a series of boxes in the centre of the screen, behaving properly.

It's really rather frustrating.

I've put also put this into a test page <a title="IE7 layout bug" href="http://chrisadams.me.uk/examples/ie7-centre-layout/">here</a>, as a sanity check for myself, and also to see if IE8 displays the same asinine behaviour.

I can't get back the time it took to work out this bug, the best I can hope for that this post saves time for another developer.

Such is life.

