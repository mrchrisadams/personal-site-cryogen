

{:author "admin", :title "How I am debugging Drupal Views ", :date "2010-09-12 10:42:16", :publish-date "Sun, 12 Sep 2010 10:42:16 +0000"}



<!-- content below -->

I've been working with Drupal a lot lately, and while there are lots of reasons to like it, ever now and then stumble across some ridiculously frustrating idiosyncrasy, that makes me want seriously consider working with the web professionally. I've documented the process of debugging a recent view that took about a day in total of head scratching, swearing, and general unhappiness, so I can refer to it in future, when I'm next battling with views, because I really don't ever want debugging to be this frustrating ever again. 

The most recent time suck on mine has been working out why one view provided by the heartbeat module, was outputting content totally differently to how the rest of the site was. Here's the html I'd normally expect to see:

<pre lang='html' line='1'>
  <a href="http://project.work.local/node/166">joe bloggs</a> has <a href="http://project.work.local/node/166">added the page Multimedia Gallery</a>
</pre>

Here's what was being generated.

<pre lang='html' line='1'>
  joebloggs [1] has added page Multimedia Gallery [2]. [1] http://project.work.local/users/joebloggs [2] http://project.work.local/node/166
</pre>

Chucking that string into google brought lead me to the drupal function `drupal_html_to_text`, which you'd normally use to sanitise text before emailing people, but this function didn't seem to directly crop up in either the views code, nor the heartbeat code.

Running a call to `ack` to look for any occurrences of this string didn't help - I'd normally expect to see this function somewhere, in the two modules, but that brought up nothing.

Even throwing an exception before the variable was generated didn't show me where the text was being changed.

There's no logging that I know of to let me trace a request from hitting the server to coming out the other end to see what functions are touching it.

I was stuck.

#### Why was this happening?

Eventually, I found out that I had the default input format set up wrong, which was the cause of all this pain. In this file here in the heartbeat module, `heartbeat/views/heartbeat_views.views.inc`, the view was reconstructing the output, basing it on what the default filter was, and handing it over to the `views_handler_field_markup` file for reformatting:

<pre lang='php' line='108'>

  // Heartbeat activity table
  $data['heartbeat_activity'] = array(

      // Table to join
      'table' => array(

        'group' => t('Heartbeat activity'),

        'base'  => array(
          'field' => 'message_id',
          'title' => t('Heartbeat activity messages'),
          'help'  => t("All activity logged by heartbeat"),
        ),
        /* 'join' => array(
          'heartbeat_messages' => array(
            'left_field' => 'message_id',
            'field' => 'message_id',
          ),
        ), */
      ),

  //  snip
  // pass content through the input filter before displaying it 
  'field' => array(
    'handler' => 'views_handler_field_markup',
    'format' => FILTER_FORMAT_DEFAULT,
  ),
  
</pre>

In this `views/handlers/views_handler_field_markup.inc`  file, the text was being reformatted using the render function:

<pre lang='php' line='28'>

  function render($values) {
    $value = $values->{$this->field_alias};
    $format = is_numeric($this->format) ? $this->format : $values->{$this->aliases['format']};
    if ($value) {
      return check_markup($value, $format, FALSE);
    }
  }
  
</pre>

... and herein lies the problem. My default format here was no longer _filtered html_, it was _messaging plain text_. If you see my defaults, you'll see why the links were being converted:

<IMAGE HERE>


### How to solve this problem ###

There are two ways you can solve this - 

1) You can change the default input format to allow links in the first pace. This keeps control in the database which works great for site builders who want to change content through the views UI.

2) You an override the template with code, and put it in source control.

#### Solving this in the database ####

In this case, our output finally ends up on our page via the default template `views-view-field.tpl.php` inside the views module which is visible below. The important variable to bear in mind here is `$output`, the result of all the prepocessing we define through the views UI, and whatever other part of Drupal decides to chime in in how it thinks the content should be rendered, like our input formatters.

<pre lang='php' line='1'>
  <?php
  // $Id: views-view-field.tpl.php,v 1.1 2008/05/16 22:22:32 merlinofchaos Exp $
   /**
    * This template is used to print a single field in a view. It is not
    * actually used in default Views, as this is registered as a theme
    * function which has better performance. For single overrides, the
    * template is perfectly okay.
    *
    * Variables available:
    * - $view: The view object
    * - $field: The field handler object that can process the input
    * - $row: The raw SQL result that can be used
    * - $output: The processed output that will normally be used.
    *
    * When fetching output from the $row, this construct should be used:
    * $data = $row->{$field->field_alias}
    *
    * The above will guarantee that you'll always get the correct data,
    * regardless of any changes in the aliasing that might happen if
    * the view is modified.
    */
  ?>

  <?php print $output; ?>
  
</pre>

After losing a day hunting down the source of this display issue, by spelunking through lot of Views and Activity contrib module code, countless blogposts and confusing views documentation, I think this is a terrible idea, especially if you're developing a website and you're already using source control, and you value consistency and simplicity.

#### Solving this in code ####

The other way to solve this problem is to use an overriding template that the views UI is considerate enough to suggest the name for when settig up a view in the first place, and also let it generate a handy view template too. The output presented should look something like this:

This text is rendered using the render format here in `views-view-field--heartbeat-activity--block-1--message.tpl.php`

<pre lang='php' line='1'>
  <?php
  // $Id: views-view-field.tpl.php,v 1.1 2008/05/16 22:22:32 merlinofchaos Exp $
   /**
    * This template is used to print a single field in a view. It is not
    * actually used in default Views, as this is registered as a theme
    * function which has better performance. For single overrides, the
    * template is perfectly okay.
    *
    * Variables available:
    * - $view: The view object
    * - $field: The field handler object that can process the input
    * - $row: The raw SQL result that can be used
    * - $output: The processed output that will normally be used.
    *
    * When fetching output from the $row, this construct should be used:
    * $data = $row->{$field->field_alias}
    *
    * The above will guarantee that you'll always get the correct data,
    * regardless of any changes in the aliasing that might happen if
    * the view is modified.
    */
  ?>

  <?php print $row->{$field->field_alias}; ?>
  
</pre>

The important change here now is that by default, we're not printing `$output` to the screen, but `$row->{$field->field_alias}`, which as the documentation tells us, is the content before it's been messed with by the input filters and such like. With direct control to the $row result, and its attributes, we finally have a degree of control over our layout, like we would be used to if using any other tool I'm more familiar with, like Rails, Django, or Wordpress.

The real watershed moment with this bug came when I gave up looking on Drupal.org, and used stack overflow to see if anyone else had had a similar problem, and following [links from an issue that looked very close to mine](http://stackoverflow.com/questions/3538505/views-is-stripping-tags-from-the-output "Views is stripping tags from the output - Stack Overflow").
 
Hopefully this will help someone else losing their hair when working on a drupal project, and help explain how this frustrating framework decides serve content to users using views.

This entire development process would be made so much easier if Drupal had an option to log the path through the framework a request takes, like how Rails does, so you can see which templates are being called, which queries are being made and so on. 

_Surely_ there's a way to do this do you can see what Drupal is actually doing under the hood, instead of making so many semi-educated guesses like I had to do here?




