

{:author "mrchrisadams", :title "Debugging in python with pdb and dropping into a 'proper' session", :date "2018-07-30 17:47:16", :publish-date "Mon, 30 Jul 2018 17:47:16 +0000"}



<!-- content below -->

If you code in python, there's a reasonably high chance you've heard of dropping into a debugger with something like pdb, or if you prefer ipython, ipdb.

It's a really, really handy skill, and if you haven't done this before, this 40 minute video gives a good overview of how it can help you:

https://www.youtube.com/watch?v=lnlZGhnULn4

<h3>But what if I want to do stuff on more than one line?</h3>

One nice thing about the debugger like this is that it puts you in a REPL like environment, where you can see what the values of various variables are, and call functions to see what they returned values might be.

The thing is, if you want to use a loop, or an if/then construct, you'll get a stroppy message like so, when you try to break onto the next line:

<pre>for obj in collection_of_objects:
*** SyntaxError: unexpected EOF while parsing<code></code></pre>

This isn't great - if you're trying to investigate why code is working the way it's working, having some basic features normally offered  by the language makes life much easier - part of the point of dropping into a debugger in the first place is to use the language you've written code in to understand the what's going on in the code better.

<h3>Oh, interact - <em>that's</em> what it's for</h3>

This is where <strong><em><a href="https://docs.python.org/3/library/pdb.html#pdbcommand-interact">interact</a> </em></strong>comes in. if you're in a pdb session, you can type <code>interact</code>, and  you'll end up in a <em>proper</em> python session where you have all the abilities you'd have with a regular python prompt, like loops, if/thens and so on.

Once you're done, hit <code>ctrl+d</code> and you'll end up back in the debugging session you were in when you first started with pdb.

<em>I've been programming python professionally since 2008, and I discovered this today. Oh well, better late than never, right?
</em>

