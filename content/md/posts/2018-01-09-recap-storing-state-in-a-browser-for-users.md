

{:author "mrchrisadams", :title "Recap - storing state in a browser for users", :date "2018-01-09 23:34:25", :publish-date "Tue, 09 Jan 2018 23:34:25 +0000"}



<!-- content below -->

I've been working on some static sites recently, and I needed to show some content to someone, but allow it to be dismissed easily, and then stay dismissed. This is much a note to future me as anyone else, but hopefully it'll be helpful to some other soul on the net.

<h3>Doing this with frameworks like django or rails</h3>

When I'm working with a full dynamic site, how you do this is usually hidden from you using a handy data structure in the language that your framework is written in.

For example, in django you often have a handy session object available, which works like a dictionary you can get and set data on. Let's say you have a blog, and you want to set some state on the user, to mark that they've commented on on a post you've written.

In some view code handling a get request, you might set a value on the session like so:

<pre><span class="n">request</span><span class="o">.</span><span class="n">session</span><span class="p">[</span><span class="s1">'has_commented'</span><span class="p">]</span> <span class="o">=</span> <span class="kc">True</span></pre>

Then, later on you could check for this by calling <code>get</code> on the session object:

<pre><span class="k">if</span> <span class="n">request</span><span class="o">.</span><span class="n">session</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="s1">'has_commented'</span><span class="p">,</span> <span class="kc">False</span><span class="p">):</span>
        <span class="k">return</span> <span class="n">HttpResponse</span><span class="p">(</span><span class="s2">"You've already commented."</span><span class="p">)</span></pre>

Python also has a native cookie library that does a similar job, of storing state on a client browser, and sparing you the gory details.

This is very handy, but when when you're working with a static site, you don't have the server there to wrap all of it in some tasty syntactic sugar.

If like me, you've had it abstracted away from you most of the time, it might be useful to know your options.

<h3>Your options if you need to do it yourself</h3>

<h4>If you want to keep data on the client</h4>

Right now, if you want to store state <em>just</em> on the client you have two popular options: local storage, and session storage. In both cases you use javascript to write values, with an api that looks a bit like so:

<pre class="brush: js line-numbers  language-js"><code class=" language-js"><span class="token comment">// Save data to sessionStorage</span>
sessionStorage<span class="token punctuation">.</span><span class="token function">setItem</span><span class="token punctuation">(</span><span class="token string">'key'</span><span class="token punctuation">,</span> <span class="token string">'value'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Get saved data from sessionStorage</span>
<span class="token keyword">var</span> data <span class="token operator">=</span> sessionStorage<span class="token punctuation">.</span><span class="token function">getItem</span><span class="token punctuation">(</span><span class="token string">'key'</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>

The main difference between localstorage and session storage is that <strong>session storage</strong> is automatically expired at the when you close a tab. By comparison, <strong>local storage</strong> persists, so you can visit a page, set some data, close it, and assuming you haven't set a super short expiry date, access it again the following day  from the same browser.

You can't access this from a server though it never leaves the browser.

<h4>If you want to be able to access the data on the server</h4>

If you <em>do</em> want data to persist for more than one session, <em>and</em> you want to be able to read this information on the server side (like the example the django example above), then cookies are a better fit. They work at the HTTP level, so they're really sent as extra headers when you send HTTP requests to a server somewhere. <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies">Mozilla's docs are fantastic</a> if you want to learn more about what's really happening under the hood.

You might want to have a similar API to the session and local storage APIs, to keep them easy to remember, so you can use javasscript to set data on a user's client browser like so:

<pre><span class="pl-smi">// set a value as cookie
docCookies</span>.<span class="pl-c1">setItem</span>(name, value)

// get saved value from the cookies
<span class="pl-smi">docCookies</span>.<span class="pl-c1">getItem</span>(name)</pre>

If you want this, then you want to look at the nice <a href="https://github.com/madmurphy/cookies.js">cookies.js</a> library, that wraps it up in some nice synatactic sugar, and save you remember esoteric invokations, just to set some basic data on a client.

Just remember, you can't set much data with cookies compared local storage or session storage.

Obviously if you're sending data back and forth between a browser and server, there are privacy implications and in the EU, you should to inform users how you're using cookies, to get consent before you start tracking your users. Again the <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies">MDN docs are a good concise starting point,</a> if you need a reminder.

&nbsp;

&nbsp;

