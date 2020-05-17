

{:author "admin", :title "Fixing old gits", :date "2009-07-25 20:03:12", :publish-date "Sat, 25 Jul 2009 20:03:12 +0000"}



<!-- content below -->

I've been working a project that used a very old git repo, and when I tried to run commit, I was greeted with this particular gem, over and over:
<pre><code>
Git: You have some suspicious patch lines…
(endless whining about whitespace and tabs and other petty crap
</code></pre>
This gets pretty tiresome, but fortunately, it's quite easy to fix. You can either run <code>git commit</code> with the <code>--noverify</code> flag, or for a more permanent fix, take by taking out the executable bit on the pre-commit hook like so:
<pre><code>
cd .git/hooks/ # go to the directory where the git hooks are
chmod -x pre-commit #metaphorically speaking, take a crow bar its kneecaps
</code></pre>
Mercifully, this little feat of silicon skullduggery is already done for you in more recent git versions, so you needn't dirty your hands.

Thanks <a href="http://robwilkerson.org/2008/09/12/ignore-gits-suspicious-patch-lines/">Rob Wilkerson's</a>, and <a href="http://danklassen.com/wordpress/2008/12/git-you-have-some-suspicious-patch-lines/">Dan Klassen</a> for this particular gem.

