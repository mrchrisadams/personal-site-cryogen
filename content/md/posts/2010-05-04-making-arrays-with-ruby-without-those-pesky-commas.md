

{:author "admin", :title "Making arrays with ruby, without those pesky commas", :date "2010-05-04 13:22:23", :publish-date "Tue, 04 May 2010 13:22:23 +0000"}



<!-- content below -->

The most common way to create an array in Ruby is do this:

<pre lang="ruby">
my_shiny_new_array = ["tom", "dick", "harry", "jonah", "percy", "jermaine"]
</pre>

Thanks to its perly origins though, you also have a more idiomatic way to do this in Ruby, like so:

<pre lang="ruby">
%w(tom dick harry jonah percy jermaine)
</pre>

Because Ruby has such a flexible syntax, it's easy to forget that when you use some of it's more magical tricks like wrapping a series of words in  `%w()` to create an array, you're really calling a method called `%w`, and passing in the the strings as params like any other method.

This trick works with other delimiting characters too, using `{}` or `[]` like below gives the same result.

<pre lang="ruby" >
# all these create an array in the same way
%w(tom dick harry jonah percy jermaine)
%w[tom dick harry jonah percy jermaine]
%w{tom dick harry jonah percy jermaine}
</pre>

_This post has been updated since I managed to forgot to wrap the strings in quotes, and it was pointed out by a commenter (thanks Jakub!)_



