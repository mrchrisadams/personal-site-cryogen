

{:author "admin", :title "RVM and Textmate in harmony", :date "2010-05-21 07:14:51", :publish-date "Fri, 21 May 2010 07:14:51 +0000"}



<!-- content below -->

One side effect of Ruby's popularity is the proliferation of ruby interpreters that can now execute ruby code, which is generally seen as a good thing, as a sign of a healthy community. However, keeping track of all these versions of Ruby, especially when testing gets harder as each new version of Ruby is released, so to help alleviate this problem [Wayne E. Seguin][] released Ruby Version Manager, or [RVM][] to it's friends last year. 

[RVM][] does some clever voodoo with symbolic links and suchlike on your box to let you switch between versions of Ruby very easily on the command line simply by typing `RVM use ruby-version` when you want to use a particular flavour of Ruby. So If I wanted to run MacRuby instead of the usual version of Ruby 1.8.7 that uses the MRI Interpreter, I'd simply check what versions of Ruby I had installed on my box like so :

<pre lang="bash">

chrisadams@edam[/usr/local/Library]
[7:52]:rvm list

   jruby-1.4.0 [ [x86_64-java] ]
   macruby-nightly [ ]
   ree-1.8.7-2010.01 [ ]
=> ruby-1.8.7-tv1_8_7_249 [ x86_64 ]
=> (default) ruby-1.8.7-tv1_8_7_249 [ x86_64 ]
   system [ x86_64 i386 ppc ]

</pre>

And then say which Ruby I want to use for the rest of the session I have open:

<pre lang="bash">
[7:52]:rvm use macruby-nightly

  Now using macruby nightly

</pre>

And if I wanted to switch back, I'd just type

<pre lang="bash">
chrisadams@edam[/usr/local/Library]
[7:54]:rvm use default        

Now using default ruby.

</pre>

This is extremely handy, except if you're using Textmate, which by default, will happily use a version of Ruby that pays no attention to your version switching japery, making testing and development rather less fun.

Fortunately, there are now some tools to make [RVM][] work with everyone's favourite mac only OS X editor now. Here's how to to make the two work together easily:

First of all tell [RVM][] to setup your symlink:

<pre lang="bash">
    rvm 1.8.7 --symlink textmate
</pre>

Now, you'll need to tell Textmate to use this version of Ruby instead by a) setting a shell variable, and then forcing Textmate to use this Ruby instead, by moving the `Builder` class, that normally sets up it's Ruby shell environment:

Here's where you should set your shell variable in Textmate:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/05/20100521-x7b3hw4i2r4xqd1kgyeg2hxijd.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/05/20100521-x7b3hw4i2r4xqd1kgyeg2hxijd-300x272.png" alt="" title="20100521-x7b3hw4i2r4xqd1kgyeg2hxijd" width="300" height="272" class="alignnone size-medium wp-image-294" /></a>

Once you have that, swap out the `Builder` as mentioned before, then restart Textmate.

<pre lang="bash">
    cd /Applications/TextMate.app/Contents/SharedSupport/Support/lib/ ; mv Builder.rb Builder.rb.backup
</pre>

And that should be about it. You can easily test that this worked in Textmate by opening a new file containing only the following code snippet:

<pre lang="ruby">
    puts RUBY_DESCRIPTION
</pre>

... then either saving the file with a `.rb` extension, or set the syntax colouring for Ruby, then hitting command + 

If it worked, you should see something like this:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/05/Running-“test.rb”….png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2010/05/Running-“test.rb”…-300x271.png" alt="" title="Running “test.rb”…" width="300" height="271" class="alignnone size-medium wp-image-293" /></a>

If not, don't despair - there's lots of useful docs on the [RVM][] site itself, and the irc channel, #[RVM][] is full of wonderfully helpful types.

Now go, armed with this knowledge and make Textmate and [RVM][] to play nicely together again.


<!-- links -->

[Wayne E. Seguin]: http://www.workingwithrails.com/recommendation/for/person/7192-wayne-e-seguin
[RVM]: http://rvm.beginrescueend.com/integration/textmate/

