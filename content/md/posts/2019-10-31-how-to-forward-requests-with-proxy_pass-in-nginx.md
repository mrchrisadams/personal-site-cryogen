

{:author "mrchrisadams", :title "How to forward requests with proxy_pass in nginx", :date "2019-10-31 14:38:54", :publish-date "Thu, 31 Oct 2019 14:38:54 +0000"}



<!-- content below -->

<!-- wp:paragraph -->
<p>I've been doing some work of late with The Green Web Foundation, and recently we moved from using Gearman as a queue, to RabbitMQ instead.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>RabbitMQ has a management UI that makes it easier to tell what it's doing, and it also exposes this information at a specific port, (lets say 12345) in the form of a handy dashboard.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You might want to make this easy to see remotely, and if you already use Nginx as a webserver for serving files on the same machine, one thing you can do is serve this dashboard using nginx, using a handy directive called <em>proxy_pass</em>, and setting up an <em>upstream</em> provider, to send requests to another service.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Here's how it works.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>First all, set up a server</strong></p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code -->
<pre class="wp-block-syntaxhighlighter-code">server {
  # sample values
  listen 123.123.123.123:80;
  server_name dashboard.thegreenwebfoundation.org;
  # the directory to serve files from
  root  /var/www/dashboard.thegreenwebfoundation.org;


  location / {
        # try to serve file directly, fallback to index.php
        try_files $uri /index.html$is_args$args;
  }

}
</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Once you have a server, this should be serving files from the directory <code>/var/www/dashboard.thegreenwebfoundation.org</code>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This works for static files, but in the case of the RabbitMQ dashboard, we have the dashboard being served from a different port.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>One way to serve this content on a different port is to define it as an <em>upstream</em>, server, like so, so we can refer to it later:</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code -->
<pre class="wp-block-syntaxhighlighter-code">upstream rabbitmgmnt {
	server localhost:12345;
}</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p>Now we have defined a server listening on 12345, we need a way to send traffic along to this new upstream server. One way is to use the <code>location</code> directive like this - now, any requests sent to <code>dashboard.thegreenwebfoundation.org/rabbit</code> will not be sent along to the upstream rabbitmgnt server.</p>
<!-- /wp:paragraph -->

<!-- wp:syntaxhighlighter/code -->
<pre class="wp-block-syntaxhighlighter-code">location /rabbit/ {
        proxy_pass http://rabbitmgmnt/;
  }</pre>
<!-- /wp:syntaxhighlighter/code -->

<!-- wp:paragraph -->
<p><strong>Why is this useful?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is handy as it saves you needing to set up a whole new virtual host.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Note: I've abridged the code this example to keep the code easily readable, but you'd almost always serve this over HTTPS, and ideally, you'd try to reduce the possible IP addresses you've be able to access this endpoint over.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This post is one for my future self, when I forget how to use nginx again…</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Helpful links</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>RabbitMQ Management plugin - <a href="https://www.rabbitmq.com/management.html">https://www.rabbitmq.com/management.html</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Nginx proxy_pass info - <a href="http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass">http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Nginx upstream servers - <a href="http://nginx.org/en/docs/http/ngx_http_upstream_module.html#upstream">http://nginx.org/en/docs/http/ngx_http_upstream_module.html#upstream</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

