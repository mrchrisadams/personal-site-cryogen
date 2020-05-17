

{:author "admin", :title "Tar is not zip", :date "2010-05-17 01:40:54", :publish-date "Mon, 17 May 2010 01:40:54 +0000"}



<!-- content below -->

Today, I had to package up some code that was residing on a remote server that I had ssh access to, to send to someone who was probably on a windows box.

This meant I had to use the `zip` tool, which I can never remember how to use, hence this memory jogging post.

Now if someone's using a Mac or is on Linux, the normal command line approach to to tar up a directory to send to someone goes like this:

<pre lang="bash">
tar -cvzf my_tarfile.tar.gz a_directory_to_tar and_otherone_here
</pre>

We're calling `tar` here, with the -create _(c)_, file _(f)_, compress _(z)_ oh, and the verbose _(f)_, flag. Think of that string like saying to the computer: "create the tarfile `my_tarfile` putting it into a file we just created, verbosely, while compressing it, from `a_directory_to_tar` and `and_otherone_here`".

As commands go, the order feels a bit weird at first, but you get the hang eventually.

#### Where zip is different

Using `zip` isn't too different really, but it you need to remember to tell it to zip recursively (why is this not default behaviour?). If we call command:

<pre lang="bash">
zip archive a_directory_to_tar and_otherone_here
</pre>

We'll end up with an rather useless empty file called `archive.zip`. We need to pass in the recursive flag
<pre lang="bash">
zip -r archive a_directory_to_tar and_otherone_here
</pre>

There's also no need to add the `.zip` file extension - this is added for you as a courtesy. Well, after that ridiculous non-recursive default shenanigans, frankly that's the least it could do...

Anyway, there you have it. The differences you between them if you don't want to dive into the manpages just to package up a folder for somebody, or look at this [linux.about.com](http://linux.about.com/od/commands/a/blcmdl1_zipx.htm "Example uses of the Linux Command zip").


