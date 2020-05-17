

{:author "admin", :title "Quick note working with child themes and Wordpress", :date "2011-05-02 21:27:28", :publish-date "Mon, 02 May 2011 21:27:28 +0000"}



<!-- content below -->


Continuing my adventures in the world of Wordpress theming today, I stumbled across a minor gotcha when working with Child Themes and writing code using functions.

When you're using [Dimas Begunoff][]'s WPAlchemy framework for making metaboxes, the code examples refer to creating a sample meta box like so:

<pre lang="php">

  $custom_metabox = new WPAlchemy_MetaBox(array
  (
    'id' => '_custom_meta', // underscore prefix hides fields from the custom fields area
    'title' => 'My Custom Meta',
    'template' => TEMPLATEPATH . '/custom/simple_meta.php',
  ));

</pre>

This won't work with child themes, because the TEMPLATEPATH will be pointing to the template path of the parent theme. As all your code is (or should be...) in the child theme, you won't be able to get to the template.

### You need STYLESHEETPATH 

If you're using a child theme, you'll need to use a different constant instead, called `STYLESHEETPATH`, which rather confusingly gives you the equivalent path, for the child theme:

<pre lang="php">

  $custom_metabox = new WPAlchemy_MetaBox(array
  (
    'id' => '_custom_meta', // underscore prefix hides fields from the custom fields area
    'title' => 'My Custom Meta',
    'template' => STYLESHEETPATH . '/custom/simple_meta.php',
  ));

</pre>



Found via [nabble][].


<!-- links -->
[nabble]: http://old.nabble.com/Re%3A-TEMPLATEPATH-in-child-themes-p23527283.html "Nabble"
[Dimas Begunoff]: http://www.farinspace.com/wpalchemy-metabox/ "Dimas' meta-box"


