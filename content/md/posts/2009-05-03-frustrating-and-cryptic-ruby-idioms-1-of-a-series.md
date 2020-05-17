

{:author "admin", :title "Frustrating and Cryptic Ruby Idioms (#1 of a series)", :date "2009-05-03 07:33:58", :publish-date "Sun, 03 May 2009 07:33:58 +0000"}



<!-- content below -->

I keep coming across these FACRI's (Frustrating and Cryptic Ruby Idioms) in my work, so I'm jotting them here in the hope that I'll remember them better in future.

#### Ruby idioms

Ruby is a wonderful, if somewhat slow and memory hungry language, with an incredibly flexible and expressive syntax. However this flexibility leads to the creation of idioms that initially look totally opaque, if you don't know what to look for.

##### Case in point: the object{:&amp;method} idiom

If you want to take an array called names , want to create a new array by running a text manipulation on every member of that array, a terse, but readable way to do this would be:

result = names.map { |name| name.upcase }

The intent is pretty clear here, and what happens programatically is also very readable. Another way to do this though is write it like:

result = names.map {&amp;:upcase}

Something called type coercion is occurring here; you normally pass the `map` method a `Proc` object to execute, with a placeholder name for each iteration, and the code to run and return. However because you're not passing a Proc object here, Ruby tries to convert it on the fly into a Proc object using a method called `to_proc`:

def to_proc
proc { |obj, *args| obj.send(self, *args) }
end

So in this case, it's passing in `names`, and the method in the `*args` is `upcase`. I wasn't familiar with the `send` method here either, so the [documentation for it from ruby core](http://www.ruby-doc.org/core/classes/Object.html#M000335 "Class: Object.send") may help here:

class Klass
def hello(*args)
"Hello " + args.join(' ')
end
end
k = Klass.new
k.send :hello, "gentle", "readers" #=&gt; "Hello gentle readers"

##### An expensive idiom, by rockstars, for rockstars.

Th end result of all these examples is a saving of about 12 characters, at the expense of readability, and a huge performance hit as each member in names of passed around and type coerced like there's no tomorrow.

If you're a coding savant, the elegance of this will probably make you weep tears of syntactic joy, and the clever brevity of this isn't lost on me.

However, coming to this, without too much knowledge of the Ruby extensions project, or [someone to talk you through what's happening](http://pragdave.pragprog.com/pragdave/2005/11/symbolto_proc.html "PragDave: Symbol#to_proc") is likely to be a frustrating experience.

Hope fully this will save time for someone else in future.

