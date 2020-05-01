

{:author "mrchrisadams", :title "How to rate limit punks with nginx", :date "2019-12-02 17:05:24", :publish-date "Mon, 02 Dec 2019 17:05:24 +0000"}



<!-- content below -->

<!-- wp:paragraph -->
<p>I do some ops work for the Green Web Foundation, and over the last few weeks we've been seeing nasty spikes </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code -->
<pre class="wp-block-syntaxhighlighter-code">limit_req_zone $binary_remote_addr zone=nopunks:10m rate=10r/s;</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>What does this mean? We start by calling <strong><code>limit_req_zone</code></strong>, to tell nginx we want to set up a zone where we rate limit requests on our server, telling it to use  <strong><code>$binary_remote_addr</code></strong>, or the binary representation of a connecting client's IP address to tell one requesting client from another. We want to be able to refer to this rate limiting zone, so we give it a name, <em>nopunks</em> <strong><code>zone=nopunks:10m</code></strong>, and we site aside 10 megabytes of space to keep track of all the possible IP addresses connecting.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This means we can keep track of something how much our poor API is being hammed, from around 160,000 different IP addresses - useful!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Finally we set a rate of requests that seems fair with <strong><code>rate=10r/s</code></strong>. This means we want an upper limit of 10 requests per second to apply to this zone.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>So, after writing this, we have a special zone, <em>nopunks</em>, that we can apply to any vhost or server we want with nginx.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Adding our zone to a site or API we want to protect</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Now we have that, let's apply this handy new <em>nopunks</em> zone, to a route in nginx. </p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code -->
<pre class="wp-block-syntaxhighlighter-code">location / {
      # apply the nopunks
      # allow a burst of up to 20 requests
      # in one go, with no delay
      limit_req zone=nopunks burst=20 nodelay;
      # tell the offending client they are being
      # rate limited - it's polite!
      limit_req_status=429;
      # try to serve file directly, fallback to index.php
      try_files $uri /index.php$is_args$args;
}</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>What we're doing here is applying the nopunks zone, and passing in a couple of extra incantations, to avoid a page loading too slowly.  We use <code>burst=20</code> to say:</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>we are cool with a burst of up to 20 requests, in one go before we stop accepting requests</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Thing is, this leaves us with a backlog of 20 requests, each taking 0.1 seconds to be served, so the whole set of requests will take 2 seconds. That's a pretty poor user experience. So, we can pass in <code>nodelay</code> - this adjusts our rate limiting to say this instead:</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>okay, you can send up to 20 requests, and we'll even let you send them as fast as you like, but if you send any more than that, we'll rate limit you</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Finally, by default, with nginx, when a site is rate limited it serves a rather dramatic 503 error, as if something very wrong had happened. Instead <code>limit_req_status=429</code> tells nginx to tell the connecting client to send a 429  <em>too many requests</em> status, so ideally, the person programming the offending HTTP client gets the message, and stops hammering the your API so hard.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>So there you have it</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This is a message mainly to my future self, next time I am looking after a server under attack. But with some luck, it'll make being DOS'd (unintentional or not) a less stressful experience for another soul on the internet.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Further reading</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The <a href="https://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req_status">nginx documentation</a> is pretty clear if you need to do this, with lots of helpful examples, and the <a href="https://www.nginx.com/blog/rate-limiting-nginx/#limit_req_status">guide on rate limiting on the Nginx website</a>  also was a godsend when I had do this today.</p>
<!-- /wp:paragraph -->

