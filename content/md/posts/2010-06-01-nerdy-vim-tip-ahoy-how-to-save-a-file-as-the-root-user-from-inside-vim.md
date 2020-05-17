

{:author "admin", :title "Nerdy Vim tip ahoy! How to save a file as the root user from inside Vim", :date "2010-06-01 10:46:18", :publish-date "Tue, 01 Jun 2010 10:46:18 +0000"}



<!-- content below -->

At work, I'm always managing files while working on a remote server which invariably means I'm stuck using Vim or Vi, and finding out after I've made the my necessary changes to crucial config file,  I don't have the rights to actually save them - so I can see this tip by  [catonmat][] saving lots of time in future. Thank you internets!

If you're using Vim, and you find that you need to save a file as root, the normal commands like `:wq` won't work. Instead you'll need to call this command:

<pre lang="bash">
  :w !sudo tee %
</pre>

### Okay that's nice. What is it actually doing?

The above command is basically saying _call the write command, passing in `sudo tee %` as the argument_. Now `sudo` we should be fairly comfortable with by now, leaving us just puzzling over what `tee` and `%`  actually mean. Thankfully, it's not too complex.

The `tee` command takes the the standard input (which in this case is the contents of the file we're editing), and writes that into the filename referenced by `%` which is a vim shorthard for the current filename.

### Again, in English please

Sadly for these purposes, my first language for thinking in still English rather than Bash or Vim, so the only way I think I'll ever retain this particular gem is to think of this in the following terms:

> From within vim, take the contents of the file I'm editing, and as sudo, write it into the file I'm currently in, doing so as root.

One day this will all be second nature to me when I'm a _real_ programmer, but til then, I'll stick with Textmate - it's massively powerful, but when you come against these strange cases, it defers to OS X's much slicker handling of permissions issues.

<!-- links -->

[catonmat]: http://www.catonmat.net/blog/top-ten-one-liners-from-commandlinefu-explained/ "Top Ten One-Liners from CommandLineFu Explained - good coders code, great reuse"

