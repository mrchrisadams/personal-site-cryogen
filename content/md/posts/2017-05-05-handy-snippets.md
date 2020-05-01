

{:author "mrchrisadams", :title "Handy snippets - Python without the .pyc cruft", :date "2017-05-05 22:28:27", :publish-date "Fri, 05 May 2017 22:28:27 +0000"}



<!-- content below -->

<em>I maintain a huge workflowy file of snippets and tricks and, I suspect some of them will be handy for others to use too. I'm going to sharing them regularly, when I'm not sure what to write, mainly to keep the habit of blogging, until it comes naturally.</em>

Part of my professional life, involves me writing a fair amount of python code. When you write python, you end up creating lots of files ending with <code>.py</code>, but when you <em>run</em> the code, you end up with compiled python files, sending in <code>pyc</code>.

If you don't want loads of <code>pyc</code> files crufting up your workspace, and you're workignon the command line, there's a handy little environment variable you can set in your shell, to banish those ugly files once and for good. Run this command before working (or better yet, make it run whenever you open a terminal window):

[code lang="bash"]

export PYTHONDONTWRITEBYTECODE=1

[/code]

See, isn't that better?

I picked up this gem from the <a href="http://docs.python-guide.org/en/latest/writing/gotchas/#bytecode-pyc-files-everywhere">Hitchhiker's Guide to Python</a>, a free, opinionated book from Kenneth Reitz about good practices with working with Python. Reading it will almost certainly improve your python - I know mine is better as a result of spending some looking over it.

