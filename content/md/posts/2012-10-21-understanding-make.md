

{:author "admin", :title "Understanding `make`", :date "2012-10-21 11:52:28", :publish-date "Sun, 21 Oct 2012 11:52:28 +0000"}



<!-- content below -->

I'm working with node more as I develop a few projects in my spare time, and I've just come across the node community's habit of using `Makefiles` to automate tasks in their project.

I've played with Python, PHP, and Ruby over the last few years, but in that time I've barely used MakeFiles at all, so after a fee initial hiccups, I was pleased to find them pretty straightforward to work with. 

Here's a trivial makefile I'm using on a project:

    test:	
    	./node_modules/.bin/mocha \
    	--reporter dot

    test-watch:	
    	./node_modules/.bin/mocha \
    	--reporter list \
    	--watch

    .PHONY: test

With this, I can type `make` on the project root. and it'll run the tests on the project, without me needing to think about what kinds of options I need to set beforehand to make sure I'm using the right test tools, or getting the right output to understand what the test results are telling me and so on.

In the case above, I've got a basic make test, and I've also got a `test-watch` task defined here, to give me constant feedback when making changes to the codebase to see if I've broken anything. I've also changed the output to be a bit more readable, for when I'm looking over it.

In both cases, I've just defined the task name, then on the following lines, written the shell commands to execute.

### A few gotchas

Well, it *should* be that easy, right?

#### A strange fetish of tabs

When I first copied and pasted a makefile to try running it, I had this cryptic response though - 

    Makefile:2: *** missing separator.  Stop.

    "Makefile", line 2: Need an operator
    Fatal errors encountered -- cannot continue

The trick here, is to make sure after defining the task on online, you HAVE to use tabs to indent the subsequent shell commands, or `make` throws a fit like above. Life is too short to work out why, so it's best to just roll your eyes, accept it, then move on.

#### How does `make` know what to call when you type `make` and what is this PHONY japery?

This threw me initially when I was trying to understand the syntax, but I think I've got a handle on it now. 

By default, if you type `make`, it will look for the first task it can run in the `Makefile`, in this case `test`. However, because make was originally a build tool for managing dependencies when building projects, `make` will only run if there isn't a file or directory with the same name as it in the current working directory, because it assumes you want to be building a file and output something called 'test'.

If there is a something there in your propect with that name, then you'll get a response like so:

    12:23pm $ make
      make: `test' is up to date.
      
What the `PHONY` line does, is tell `make` not to care if there are directories or files called `test` in the project structure, and just to run the task anyway. 

Without the `PHONY` line, your `test` task will never run if there's a directory called `test` lying around.

And there you have it. You should know enough now to write your own make tasks. Off you go then.

### Helpful links

[This piece here helped me get my head round phony](http://makepp.sourceforge.net/1.18/t_phony.html), and [this one here](http://www.cs.usask.ca/staff/oster/makefiles.html) gave me a handy background too. Finally, the [mocha testing library](http://visionmedia.github.com/mocha/) was the reason I decided to try to learn this in the first place, and an nice example of it being used in a javascript project.

