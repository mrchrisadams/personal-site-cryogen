

{:author "mrchrisadams", :title "Notes as I learn about tuning MySQL", :date "2019-07-04 20:45:01", :publish-date "Thu, 04 Jul 2019 20:45:01 +0000"}



<!-- content below -->

<!-- wp:paragraph -->
<p><em>I've been doing some work with MySQL again with the Green Web Foundation. This has involved working with relatively large sets of data, so to make some queries run faster, I've found myself looking at the settings it uses by default, and having to understand what queries are doing under the hood.</em> <em>These are some of my notes</em>, mainly for my future self.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Like earlier Postgres, earlier MySQL has smalll memory defaults</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>When I was last working with servers directly, and having to fiddle around with settings, I learned that early versions of Postgres has defaults to be really conservative about how much RAM the server would assume it could access on a machine.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is good news in terms of not eating up all your memory, but less good for actual performance, you'd often end up with RAM lying around unused, when it could be put to work making things run faster.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The story is similar with MySQL - if you're using a version of MySQL like 5.6 or earlier,and no one's been playing with the settings, you maybe using the default tiny amount of memory, and relying on reads or writes to disk, slowing everything down.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Different storage engines need different kinds of settings</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>One key difference between the two is that MySQL has the idea of swappable storage engines, where as with PostGres, you only have the one.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>What's more over the last 10 years or so, the old default storage engine for MySQL, MYISAM, given way to the more capable InnoDB storage engine.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is good if you have new projects, but less so for old ones. What's more, if you have some tables which use MYISAM, and some which use InnoDB, you now need to thinkg about two sets of settings to tweak.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I'll list the key settings in each case that I've found.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>MYISAM</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>key_buffer_size</strong> - MySQL relies on this setting to work out how much space it has to use for storing parts of table's indexes in memory to quickly find stuff. This isn't the full picture though - as this only covers <em>indexes</em>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If there's actual data that needs to be kept in cache, it relies on whatever the server operating system uses to cache files, to avoid reading from a disk. If you're using Linux, this means the disk caching that it uses by default to keep commonly used data in memory anyway. But this also means that you need to leave space for it. </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>InnoDB</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>innodb_buffer_pool_size</strong> - by comparison, InnoDB uses single setting to let you explicitly decide how much RAM you want to allocate as a buffer for indexes and data. This is likely the single most important thing to change if you're using primarily InnoDB tables. There's</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It also outlines why a mix of MYISAM and InnoDB tables can be a pain - you now have two sets of knobs to twiddle for performance, when it would be so much nicer to just have one set.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Global vs per-thread settings</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Like Postgres MySQL supports lots of clients reading or writing at the same time to a given database via a pool of <em>connections</em>. And in addition to setting global settings like <strong>innodb_buffer_pool_size</strong>, or <strong>key_buffer_size</strong>, you there are also per client settings - these decide how much memory might either be allocated for a client to have to available for various queries and so on.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In my use case, I'm needing to do a bunch of sorts, and groupings, which rely on creating temporary tables when working.  One important setting in this case is <strong>tmp_table_size</strong>, which decides how much memory is allocated for making temporary tables to speed these actions up (<a href="https://dev.mysql.com/doc/refman/5.7/en/internal-temporary-tables.html">see more in the docs</a>).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This piece from <a href="https://www.percona.com/blog/2006/05/17/mysql-server-memory-usage/">Percona's blog on MySQL memory usage</a>, even though it's 13 years old now was pretty helpful.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Understanding queries with EXPLAIN</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Just like Postgres, you can add EXPLAIN at the beginning of any queries to get a better understanding of what they'd be doing under the hood then the query runs.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://www.sitepoint.com/optimize-mysql-indexes-slow-queries-configuration/">This post from sitepoint explains how to use it</a> - it's nowhere near as comprehensive as Postgres's version of EXPLAIN, but it at least tells you how MySQL will try to find the rows you care about. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>Setting session level settings for a client</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>I mentioned before about per client settings, in addition to global settings.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>With MySQL, you can set things like <strong>read_buffer_size, sort_buffer_size, read_rnd_buffer_size,  tmp_table_size</strong>, but make them only apply for a given session - this is useful in the case of you having a loads of normal kinds of requests and queries you need to support, but there <em>also</em> being occasional jobs where you it would be really helpful to have much more memory available to make big sorts, and joins and so on.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For this, you can set it in  query, like so:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>SET SESSION sort_buffer_size = 4 * 1024 * 1024</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>At the end of the session it'll be unset, which is useful, as otherwise setting these values globally can overwhelm a server, when you have 300 requests suddenly using this massivelt greedy default.</p>
<!-- /wp:paragraph -->

