

{:author "admin", :title "Discovering the jQuery data method", :date "2010-09-19 22:44:50", :publish-date "Sun, 19 Sep 2010 22:44:50 +0000"}



<!-- content below -->

Every now and then you come across a trick in web development, or a particular method in a library's API that makes you wonder how you bumbled along without it, and totally changes how you work in future.

That happened today foe me when I discovered the `data()` method in jQuery. 

In short, it lets you attach arbitrary data to elements you've referring to in the DOM, without resorting to gruesome hacks like coming up with bogus `rel=foo` attributes to store data relating to specific dom elements.

For example lets say we have an list of people below in unordered list

<pre lang='html' line='1'>
    
    <ul class="fave_streetfighters">
        <li id"ryu">Ryu</li>
        <li id"ken">Ken</li>
        <li id"chunli">Chunli</li>
        <li id"zangief">Zangief</li>
    </ul>

</pre>

Now lets say I have some some data here I want to add to these characters, freshly delivered by an ajax call:

<pre lang='javascript' line='1'>
    
    data = [
        {   "name":"Ryu",
            "sex":"male",
            "super_move":"hoofing great fireball",
            "likes":"pyjamas"
        },
        { 
            "name":"Ken",
            "sex":"male",
            "super_move":"big fiery jumping uppercut",
            "likes":"being arrogant"
        },
        { 
            "name":"Chunli",
            "sex":"female",
            "super_move":"hundred foot kick",
            "likes":"spiky bracelets"
        },
        {
            "name":"Zangief",
            "sex":"male",
            "super_move":"spinning pile driver",
            "likes":"tight red pants"
        }
    ]
</pre>

Instead of embedding this data in each list item by faffing around with weird classnames, or made up attributes like this, which messes the DOM up something horrible:

<pre lang='javascript' line='0'>
    $('li#ryu').attr('made_up_attribute_for_super_move', data[0].super_move);
    $('li#ryu').attr('made_up_attribute_for_likes', data[0].likes);
</pre>

... the cleaner way to add this data to the corresponding element is so use the `data{}` method like so:

<pre lang='javascript' line='0'>
    $('li#ryu').data('profileInfo', data[0]);
</pre>

This lets me associate the two, and fetch the data in future easily, with a related `data()` call:

<pre lang='javascript' line='0'>
    var cowardly_finishing_move = $('li#ryu').data('profileInfo').super_move;
    // returns "hoofing great fireball"'
</pre>

jQuery internally uses this `data()` method, which makes it extremely fast, and it's been in the API for ages, but it's something that's easy to overlook if you don't see it in use in someone else's code, or read the API yourself.

Or, if like me, you didn't read this [excellent post here by Marc Grabanski](http://marcgrabanski.com/articles/5-tips-for-better-jquery-code "5 Tips for Better jQuery Code") back in 2008.

Oh well, better late than never, right?

