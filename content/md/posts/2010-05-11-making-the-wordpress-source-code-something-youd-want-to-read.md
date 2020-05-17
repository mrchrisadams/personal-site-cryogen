

{:author "admin", :title "Making the Wordpress source code something you'd want to read", :date "2010-05-11 23:13:38", :publish-date "Tue, 11 May 2010 23:13:38 +0000"}



<!-- content below -->

If you develop with [Wordpress][] at all, you're likely to spend a fair chunk of your time wading through source code, and poring over the [Wordpress Codex][2] when something isn't working the way you expected, or when you're coding new features.

If you're working with Ruby and (assuming the projects you're working on has some documentation in the first place), tools like [RailsAPI][] or [rdoc.info][] have made browsing source code, and getting an idea of how various classes or objects make up project a fairly simple process now. 

Thing is, moving from there to [Drupal][], with its insistence on not having any useful examples in its documentation, or [Wordpress][], where the surrounding Codex docs are great, but where the source code less as easy to browse, has always felt clunky by comparison.

Thankfully, [Harry](http://twitter.com/harrym) and [Tom](http://twitter.com/holizz) at the [Dextrous Web](http://dextrousweb.com/lab-notes/ "Lab Notes :: The Dextrous Web") have worked out a clever hack that makes using the docs on [Wordpress][]'s just as nice an experience as it is on a normal ruby project, by passing all source code through [Doxygen][], then passing _that_ through the same all singing, all dancing , autocompletin' sdoc templates as used on RailsAPI, giving us all the slickness we'd come to associate with a well written Ruby project, but on a workhorse platform like [Wordpress][].

Here's how to to get your own [browsable docs like these][1], local to your machine for speedy offline reference.
 
#### Install Doxygen 

[Doxygen][] is a tool you can use to generate actual documentation the comments in [Wordpress][]'s existing code base. If you're on a mac, and using macports, you can install it like so (you may need to sudo install these, depending on how your system is set up):

<pre lang="bash">
# if you're on a mac...
port install Doxygen #if you're using macports
port install Doxygen #if you're using homebrew

# or if you're using linux ...
yum install Doxygen #if you're using a CentoOS/Redhat 
apt-get install Doxygen #if you're using a Debian/Ubuntu 
</pre>

#### Fetch the Wordpress source code.

We need to pull down this code so when we call the next step we have everything we need to create the documentation, then pass it through sdoc to create the docs.

<pre lang="bash">

git clone git://github.com/dxw/wordpressapi.git
cd wordpressapi
gem install wpdoc
git clone git://github.com/dxw/geshi.git
git clone git://github.com/dxw/[Wordpress][].git
ln -s wordpress/wp-includes
ruby update_codex.rb

</pre>

#### Generate your own docs

This step takes a long time (as in more than half an hour on my black new macbook) , and uses a fair old chunk of CPU power too, so don't be alarmed if this seems to take longer than you're used to.

<pre lang="bash">
ruby doxydoc.rb
</pre>


#### Bookmark the document index page 

The docs you're after will be created in the `docs/` directory in the wordpressapi project; you'll find the index page at `docs/` , presenting a page of all the classes that make up [Wordpress][], with an autocomplete listing of every class, method and file used in the project, with links to the source code on [github.com][], locally, and where relevant, to the [Wordpress Codex][3].

#### Browse the source 

Have a quick browse - you also have keyboard shortcuts for navigating around the code, you'll I guarantee that the easier access to the source code will help you learn something new about using [Wordpress][], without even trying, and be navigating through the the guts of the [Wordpress][] source like a pro in no time.



<!-- links -->
[RailsAPI]: http://railsapi.com/ "Rails Searchable API Doc"
[rdoc.info]: http://rdoc.info "rdoc.info"
[1]: http://wpdocs.labs.thedextrousweb.com/ "WordPress API"
[2]: http://codex.wordpress.com/ "Wordpress Codex"
[WordPress]: wordpress.org "Wordpress Main Site"
[Doxygen]: http://www.stack.nl/~dimitri/doxygen/ "Source code documentation generator tool"
[Drupal]: http://drupal.org/ "Drupal"
[github.com]: http://github.com "Secure source code hosting and collaborative development - GitHub"

