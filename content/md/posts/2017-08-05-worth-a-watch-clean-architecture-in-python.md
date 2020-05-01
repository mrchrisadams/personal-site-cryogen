

{:author "mrchrisadams", :title "Worth a watch - Clean Architecture in Python", :date "2017-08-05 19:33:15", :publish-date "Sat, 05 Aug 2017 19:33:15 +0000"}



<!-- content below -->

<em>I'm experimenting with ways to start posting regularly here, and one way I think might work is to share a link each week to a talk, or video I've watched, and why I found it worth watching. As of summer 2017, Python is my primary coding language, and this talk by Brandon Rhodes from 2014 was a lovely find. I'll explain why in this post.</em>

&nbsp;

https://www.youtube.com/watch?v=DJtef410XaM

<h4>Why you might watch it</h4>

If you've ever written any code in python that pulls data from a database, or external web service, it's easy to get bogged down in long messy chunks of code, that end up being difficult to test, or take a long time for the tests to run.

Sadly, this often acts as a disincentive against writing tests, which means you end up writing few tests, and end up with buggier code than you want.

This talk gives a nice round up of the strategies specific to Python 3 you might use to manage this (like <a href="https://docs.python.org/3/library/unittest.mock.html">the built-in mock library</a>), as well as referring to more common techniques used in other languages like dependency injection, in Brandon's typical affable, easy to understand fashion.

He also gives a nice round introduction to ideas put forward by other programmers, like what <a href="https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell">Gary Bernhardt refers to as <em>imperative shell, functional core</em></a>, in his talk<em> <a href="https://www.destroyallsoftware.com/talks/boundaries">Boundaries (also worth a look).</a></em>

If you don't want to spend 45 minutes watching the vid, the general recommendation is that where possible, it's better not to hide IO, (where you talk to a database or API), but instead decouple it as much from the rest of your code as possible, so you can decompose the rest of your code into pure functions which accept and return data - this makes it easier to write fast, easy to understand tests.

The added benefit of this is that because you are able to understand the what data is going into and out of each function, you're able to test edge cases in these smaller functions, rather than relying on large expensive, slow tests that rely on lots of set up and tear down to create the necessary state you need just to test a single operation on a small subset of the data being set up. I've worked on a couple of projects in the last 12 months that had this problem, and in both cases, it was a real drain on productivity, as well, as being a real pain to work around.

The final key takeaway I took was what he referred to as having <em>consistent levels of abstraction </em>from the 'top' to the 'bottom' a program - having code that does crunchy IO wrangling mixed in with code that expresses business logic make it difficult to read, but just hiding the IO in a function then continuing to have low levels details in business logic isn't much better, as you're still mentally switching gears as you read. Better to wrap some of the business logic in well named functions too, so you're operating at the same level of abstraction in the code, and at a glance you can read the intent.

TLDR: if you're writing code in python regularly, and succinctly presents a lot of good ideas from other programming communities, and how they apply when coding in Python - I think it's worth 45 minutes of your time, and it'll almost definitely save that much time in waiting for slow tests inside a month…

&nbsp;

