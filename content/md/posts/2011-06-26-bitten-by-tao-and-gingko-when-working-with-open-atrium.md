

{:author "admin", :title "Bitten by Tao and Gingko when working with Open Atrium", :date "2011-06-26 01:07:52", :publish-date "Sun, 26 Jun 2011 01:07:52 +0000"}



<!-- content below -->

One problem when working with a subtheme of a subtheme, like when you're working with Open Atrium is that if you're not careful, it's easy to spend loads of time looking in the wrong theme wondering why your preprocess functions aren't working.

The solution here is to always go back to the README.txt file on the first parent theme, (in this case Tao), and make sure you understand what's happening there, and that you can eliminate that one from any debugging you may have to do.

#### Read the README already

In particular, I ended up spending ages today wondering why I couldn't pass in a classname for a template for some predefined css styles to be recognised by it, until working my way back up the theme ancestry, I finally came across the Tao readme.md file:

> The `$vars['attr']` variable is the standard way for adding any HTML attribute to the major containing element of the corresponding template. The
> `drupal_attributes($attr)` is used in each template to render attributes. For example, to add a class to a node, you would add the following to your
> subtheme's node preprocessor:
> 
>     $vars['attr']['class'] .= ' myclass';
> 

Obvious in hindsight, but different from bolstering the usual $body_class string used in many other themes.


