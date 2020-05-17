

{:author "admin", :title "The ForkBomb Tattoo", :date "2010-05-23 19:18:12", :publish-date "Sun, 23 May 2010 19:18:12 +0000"}



<!-- content below -->

This doesn't count for much, but I think this is one of the cleverest, geekiest, most elegant tattoos I've ever seen. Carving an <a href="http://www.flickr.com/groups/apple_tattoo/pool/">Apple</a>, <a href="http://www.readwriteweb.com/archives/the_30_best_and_worst_web_tech_tattoos.php">Cisco</a> or <a href="http://www.flickr.com/photos/bigmoontattoo/2514998242/">Nike Logo</a> onto your body? That's really quite sad. But this is something different:

<a href="http://www.flickr.com/photos/silveiraneto/4033340711/"><img class="alignnone" title="Fork Bomb" src="http://farm3.static.flickr.com/2422/4033340711_543ef81df0_b.jpg" alt="" width="354" height="614" /></a>

### Why do I like it?

#### I think it's about as attractive as a code type tattoo is going to get

The proportions are well balanced, and there's a nice visual rhythm in there - this is largely down to the choice Bitstream Sans Mono, the typeface used for this. This typeface is a well loved font in programmer circles, who spend hours staring at monospace fonts - a lovely touch.

#### It's actually executable code

This particular incantation has its own story too - this cryptic combination of symbols is a working example of a *forkbomb*, and was presented as a piece of open source art back in 2002, by<a href="http://en.wikipedia.org/wiki/Jaromil"> Denis Jaromil Rojo</a>, an Italian Rastafarian developer and media activist now residing in Amsterdam. A forkbomb is a piece of self replicating code that when called, start forking itself relentlessly, until it  consumes all the resources on a computer system, rendering it unusable.

For the terminally curious, here's how it works:
<pre lang="bash">

:()      # define ':' -- whenever we say ':', do this:
{        # beginning of what to do when we say ':'
    :    # load another copy of the ':' function into memory...
    |    # ...and pipe its output to...
    :    # ...another copy of ':' function, which has to be loaded into memory
         # (therefore, ':|:' simply gets two copies of ':' loaded whenever ':' is called)
    &amp;    # disown the functions -- if the first ':' is killed,
         #     all of the functions that it has started should NOT be auto-killed
}        # end of what to do when we say ':'
;        # Having defined ':', we should now...
:        # ...call ':', initiating a chain-reaction: each ':' will start two more.
</pre>

More on <a href="http://en.wikipedia.org/wiki/Fork_bomb">Forkbombs</a> here.

