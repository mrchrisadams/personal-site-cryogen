

{:author "admin", :title "Vim and line height", :date "2011-03-12 00:25:50", :publish-date "Sat, 12 Mar 2011 00:25:50 +0000"}



<!-- content below -->

I've switched to using MacVim lately as my editor, partly because I work on servers a fair amount in my job, and partly because well... lots of other people who are better programmers than me are generally singing it's praises, and the mix of Mac like UI polish, and power offered by Vim is an appealing combo  for me.

One little thing tweak I'd recommend though if you're coming from Textmate, is to increase the default line-height when reading text. By default, I've found the to be squished together too tightly for my liking, making it less readable than I'm used to.

### Fixable with two words (and one number)

Thankfully it's quite easy to fix: I found [this thread on the Mac Vim mailing list](http://vim.1045645.n5.nabble.com/How-do-I-change-the-line-height-td1217884.html) which had a few tips on using the `set linespace` command in Vim. Just type in:

<pre lang='vim'>

 set linespace=2

</pre>

...and once again, staring at text should become relatively easy on the eye again.

And of course, with this being , the next step is to put this setting into your dotfiles, and whichever computer you end up using, you'll only ever be a `git clone` away from having your settings just like how you're used to. Huzzah!

