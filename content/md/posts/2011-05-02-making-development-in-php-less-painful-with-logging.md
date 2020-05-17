

{:author "admin", :title "Making development in PHP less painful with logging", :date "2011-05-02 11:15:20", :publish-date "Mon, 02 May 2011 11:15:20 +0000"}



<!-- content below -->

I've been looking for a nicer way to handle logging when developing with php than simply hitting F5 all the time and this approach here, if you're spending more than 30 mins writing something is a silly approach to debugging.

<pre lang='php'>

  <pre> 
  $value = do_somestuff_with_code();
  
  var_dump($value);
  </pre>

</pre>

For a start, it assumes that we'll only ever access this code directly through a browser, and also, it means we can't see what was happening up to and around any kind of important event (like an silly error bringing down a your site) has occured, once it's left your machine.

These seem to be the options available that I've found:

### [Klogger][] - the lightest option

[KLogger][] is refreshingly simple - it's a tiny PHP class, that simply logs to a file, in a straightforward fashion. No browser integration, or logging to remote servers, (which we don't really need most of the time).

Here's what the code looks like:

<pre lang='php'>

    $log = new KLogger ( "log.txt" , KLogger::INFO );
    $log->LogInfo("Returned a million search results");	//Prints to the log file
    $log->LogFATAL("Oh dear.");				//Prints to the log file
    $log->LogDebug("x = 5");					//Prints nothing due to priority setting

</pre>

This will log the first two mesages to a file, but because we created the logging class using `KLogger::INFO` as our second param, we've set the logging level to be slightly less verbose than if we had set up using the `KLogger::DEBUG`.

### PHPConsole - chrome output of errors instead of a file.

If you don't want to log to files, you may want to try out [PHPConsole][], a plugin for chrome that lets you output messages to the chrome console, instead of clogging up your displayed page with debug code.

<pre lang='php'>

    require_once('PhpConsole.php');
    PhpConsole::start();

    // test
    debug('test message');
    debug('SELECT * FROM users', 'sql');
    unkownFunction($unkownVar);
</pre>

This doesn't log to a file, so if you want anything more persistent, so you may want to look at the companion class for `PHPConsole`, [Lagger][].

### Lagger - more fully featured than PHPConsole.

The PHP console also works with [Lagger][], another logging library that sounds very powerful, but left like way more code than I actually need.

For example, look at how much setup code we have here in the example - I'm sure load of it is useful, but before I've even started, I'm having to understand what an `EVENTSPACE` is, and start configuring it all:

<pre lang='php'>

    define('LAGGER_BASE_DIR', '../library/');
    function autoloadLaggerClasses($class) {
            if(strpos($class, 'Lagger_') === 0) {
                    require_once (LAGGER_BASE_DIR . str_replace('_', '/', $class) . '.php');
            }
    }
    spl_autoload_register('autoloadLaggerClasses');
    $laggerES = new Lagger_Eventspace();
    $debug = new Lagger_Handler_Debug($laggerES);
    $errors = new Lagger_Handler_Errors($laggerES);
    $exceptions = new Lagger_Handler_Exceptions($laggerES);

    $chromeConsole = new Lagger_Action_ChromeConsole();
    $debug->addAction($chromeConsole);
    $errors->addAction($chromeConsole);
    $exceptions->addAction($chromeConsole);

    function debug($message, $tags = null) {
            $GLOBALS['debug']->handle($message, $tags);
    }

    // test
    debug('debug message', 'some,test,tags');
    echo $unkownVar;
    unkownFunction();
</pre>


If I'm writing this much setup code, I might as well go the whole way and start using the logging tools provided by PEAR, the closest thing in PHP that I can find to Rubygems. Which brings me to...

### PEAR Log

Once you've got past the hassle of installing PEAR on your system properly (it felt like way more faff than I expected the first time when setting up PHPUnit), using PEAR Logger seems nice enough, and refreshingly, it feels like it's been written with a decent knowledge of concepts like the Singleton and Factory Patterns. The examples and documentation are fantastic, and out of the box it can also log to firebug. I haven't looked into logging to chrome yet, but [this post here suggests it can][wppearlog].

Here's some sample code for Pear Log, taken from [Irakli Nadareishvili's][] blog post about using it with Drupal.

<pre lang='php'>

    require_once 'Log.php';
    // use a lenient permission mask, and format entries accordingly
    $logconf = array('mode' => 0775, 'timeFormat' => '%X %x');

    // make sure only single log instance can ever exist, and output it
    // to '/tmp/pear.log', passing in the log configuration object
    $logger = &Log::singleton('file', '/tmp/pear.log', 'ident', $logconf);

    global $logger; //once per scope e.g. once per function body.

    $logger->log ( "LOREM IPSUM TESTS. DO NOT TOUCH");

    // print_r equivalent, to pretty print an object
    $drw = new Drawing();
    $logger->log ( var_export ($drw,true) );

</pre>

Interestingly, you can also create custom handlers for Pear Log, which would allow talking to a centralised error monitoring service like Hoptoad.

### Summary

I'd definitely recommend using a logging library over just dumping stuff onto a screen if you can help it - if you're new to logging, try out [Klogger][].

If you find yourself needing something larger, and you're prepared to spend a few minutes setting up PEAR (which you'd need for PHPUnit anyway), I'd recommand using PEAR Log - it's got a nice API, lots of other libraries are setup to use it already, and the documentation makes it easy to get started with.

[PHPConsole]: http://code.google.com/p/php-console/
[Lagger]: http://code.google.com/p/lagger/
[Klogger]: http://codefury.net/projects/klogger
[[Irakli Nadareishvili's]: http://www.freshblurbs.com/drupal-debugging-pear-logging
[wppearlog]: http://www.turingtarpit.com/2009/05/wordpress-logger-a-plugin-to-display-php-log-messages-in-safari-and-firefox/#wptoc_0_0_2


