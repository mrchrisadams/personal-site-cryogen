

{:author "mrchrisadams", :title "How to search better with Atom", :date "2017-05-11 20:35:40", :publish-date "Thu, 11 May 2017 20:35:40 +0000"}



<!-- content below -->

<i>I've been using&nbsp;Atom as my text editor for&nbsp;longer than any other text editor now, after using Textmate, Sublime Text, and Vim for a couple of years each. In this post, I show a little tip I've discovered to help make searching more powerful.</i>

Using Atom?

I like using Atom as an editor.

It's free, open source, polished, under constant development in the open with a well funded team,&nbsp;and on the whole, I agree with <a href="https://al3x.net/2008/10/22/on-flight-to-old-text-editors.html">Alex Payne's post about the flight to old text editors</a> feeling like mis-step.

It's easy enough to start with, and can adapt to work well with many, many languages. It's what I'd recommend to most people learning to code too.

However, because it isn't a full IDE, you do need to know how to use the search tools to get the most from it.

<h3>Searching for things that match one pattern, but not another</h3>

As the wonderful <a href="http://flight-manual.atom.io/using-atom/sections/find-and-replace/">flight manual from Atom editor describes in more</a> detail, you can search in within files, and search within projects easily, by hitting <code>cmd+F</code>&nbsp;to search in a file, and <code>cmd+shift+F</code>&nbsp;to search across your project.

This is nice, and&nbsp;it's common to search for a pattern like <code>some_function</code>&nbsp; or some class like <code>Page</code> in your existing project.

This example here shows a personal site I used to run, searching for mentions of <code>Page</code>&nbsp;in an django project:

[caption width="1126" id="attachment_1034" align="alignnone"]<img class="alignnone size-full wp-image-1034" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/screen-shot-2017-05-11-at-22-13-25.png" alt="Screen Shot 2017-05-11 at 22.13.25.png" width="1126" height="634"> I'm getting all kinds of maches, including ones in files I don't want[/caption]

However, lets say you're working on an app, where you're sure you don't want to look in some kinds of files that also end in <code>.py</code>.&nbsp;This might be some migration files, which are written in python, but you know you won't want to look in them for code that controls how an application works right now. To filter out all the migration files, you can and a second <em>negated</em> pattern, by adding the bang/exclamation mark instead, like so:

[caption width="1126" id="attachment_1036" align="alignnone"]<img class="alignnone size-full wp-image-1036" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/screen-shot-2017-05-11-at-22-13-47.png" alt="Screen Shot 2017-05-11 at 22.13.47.png" width="1126" height="634"> That's more like it, no migration files in the search results. Huzzah![/caption]

This is, <em>really, really</em> handy when working with javascript projects, and huge <code>node_modules</code> directories. More here in this <a href="https://discuss.atom.io/t/a-way-to-exclude-folders-from-find-in-project/9861/9">forum thread on discuss.atom.io</a>.

<h3>Searching across files you normally want to ignore in a project</h3>

The other handy trick I've started using&nbsp;a fair amount of late, and especially since I started writing in javascript and python more is toggling the search behaviour between to ignore the files that you have told git to ignore with a <code>.gitignore</code> file, and including them when you're trying to understand where a given bit of code came from.

You can do this the quick and dirty way by opening up Atom's config file here:

<img class="alignnone size-full wp-image-1055" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/screen-shot-2017-05-11-at-22-25-08.png" alt="Screen Shot 2017-05-11 at 22.25.08.png" width="354" height="412">

And in the <code>config.cson</code>&nbsp;file that's presented ​to you, making sure you have this property set to either true or false:

[code lang="coffeescript"]

"*":
core:
excludeVcsIgnoredPaths: true
[/code]

If you have this set to true, you'll have faster searching of just the files and folders you have decided to ignore with your <code>gitignore</code> file. But if you <em>do</em>&nbsp;need to search for something in something like a <code>node_modules</code> folder in javascript, in a <code>virtual environment</code>&nbsp;in Python, you can toggle this by setting this value to true or false.

I only really discovered these this year, and it's not something I new how to do before, and I figured Atom others might find it useful too.

Hope it helps, and happy searching! If you use Atom, and there are any other gems like this, feel free to add a comment below.

&nbsp;

&nbsp;

