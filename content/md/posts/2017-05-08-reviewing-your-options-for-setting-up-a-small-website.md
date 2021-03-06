

{:author "mrchrisadams", :title "Reviewing the options for setting up a small website, and ending up with WordPress", :date "2017-05-08 20:37:44", :publish-date "Mon, 08 May 2017 20:37:44 +0000"}



<!-- content below -->

<em>After spending a frankly depressing amount of time trying out various options, I've recently set up this blog, and a recent project blog, the <a href="https://awmug.org">Amateur Wardley Mapping User Group</a>, to run on Wordpress.com. For my future self to check as much as anyone else, I'll explain my reasons for doing.
</em>

I have a fair few friends who don't have a well established website, but want one, and aren't really sure where to start.

After a few years of running my own blog, on my own servers, I'm in a similar situation - at some point, I had had enough of logging into a CentOS box, that I set up in 2010, so I put all files on the box into some object storage bucket, as well as the entire machine image and pulled the plug. I put some placeholder site up, and promised myself I'd have a full site set up in a few weeks, on a fresh server, where I'm not responsible for keeping backups safe and so on.

<img class="alignnone size-full wp-image-979" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/screen-shot-2017-05-08-at-22-38-52.png" alt="Screen Shot 2017-05-08 at 22.38.52" width="832" height="481" />

<h3>More than 9 months later</h3>

That placeholder site is still up, but I've now set up this blog on WordPress.com, which I'm moving selected content over week by week. I'll probably keep the blog subdomain, and host the majority of written content there from now on.

Why?

<h3>Moving content around is a pain, but slightly less of pain with WP</h3>

I've carried out a number of content migrations in various, and without exception, migrating content has been a pain. Where possible, I now want any content I write to be in as common a format as possible, to avoid this pain in future.

WordPress now powers huge chunk of the internet, and there's value in being part of that ecosystem - WordPress's export format is pretty close to an industry standard for storing content now, and moving it around.

If you put content into WordPress, there are clear paths for getting it back out again, and into other systems, in a well-structured fashion.

<h3>I want to write more than tinker with my site</h3>

When you run your own WordPress site, it's easy to spend ages creating themes, looking around for plugins, and trying to work out how to make them all work nicely together, then invent all kind of convoluted workflows for keeping things in source control, and building weird deployment pipelines, for a perfect writing workflow, <em>rather than actually writing</em>.

By using WordPress.com, I still have the relative of freedom to leave, and move content away, but having someone else manage the user experience is quite liberating. Like with Tumblr or other tools, I'm not fiddling with settings so much, and when I've written on wordpress.com blogs before, I've been able to focus on communicating with others more.

Writing on Wordpress doesn't feel like it has quite the same focus on content as writing in <a href="http://medium.com/">Medium</a> does, but it's at least it's clear how <a href="https://automattic.com/">Automattic</a>, the company behind Wordpress.com makes money.

<h3>I think the Wordpress writing experience is going to continue to get better faster than other tools</h3>

On the subject of user experience, while writing in Wordpress isn't bad, there are other competitors that also offer a nice place to write online:

<img class="alignnone size-full wp-image-944" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/screen-shot-2017-05-08-at-22-19-29.png" alt="Screen Shot 2017-05-08 at 22.19.29" width="915" height="682" />

If you're looking for a polished open source CMS to run, <a href="http://wagtail.io/">Wagtail,</a> a Django app is the closest I've seen to combine Wordpress's ease of use, with some interesting thinking about structured blocks of content, expressed as Streamfields, and explained by Matt Westcott's article <a href="https://torchbox.com/blog/rich-text-fields-and-faster-horses/">Rich Text fields and Faster Horses.</a>

A few years ago, Poetica offered a really well thought through writing experience, that you could use inside wordpress itself as your editor.

<img class="alignnone size-full wp-image-946" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/banner-772x250.png" alt="banner-772x250" width="772" height="250" />

Elsewhere, for many of us, Google docs, has effectively become the de facto place where content is written before we paste it into a blog editor.

If you really like Markdown, and source control, and you tend not to use many images anyway, there are now many, many static sites generators now, promising an unhackable, fast site, like Pelican, Jekyll, Cryogen

Finally, I think Medum's writing experience is probably the most enjoyable one online right now. From writing, to asking for feedback on a draft, to seeing highlights and comments  on writing you've published, very much feels like the benchmark writing online will be judged against from now on.

I looked at all of these, setting them up, writing with them and trying publishing/deployment workflow.

I ended up with WordPress, partly because I wherever there was a strength one of the options had over it, I could see a decent response from the product team at Automattic.

<h4>Wordpress's responses to these threats</h4>

With my Product Manager hat on, seeing Automatic respond to these threats is fascinating:

<img class="alignnone size-full wp-image-954" src="https://mrchrisadamsblog.files.wordpress.com/2017/05/google-docs-for-wp-com.jpg" alt="google-docs-for-wp-com" width="640" height="400" />

<a href="https://apps.wordpress.com/google-docs/">Google Docs for Wordpress.com,</a> which lets you collaborate with others, then publish directly from Google Docs to a WordPress site feels like a pragmatic response to how people really write online. It also deftly provides an alternative right now for people clamour for the collaboration and commentary tools that Poetica and Medium offer.

Elsewhere, you can see experiments in editor UI by the Automattic on with <a href="https://github.com/WordPress/gutenberg">Project Gutenberg</a>  and <a href="http://intenseminimalism.com/2017/two-mental-models-to-design-wysiwyg-editors/">this post by Davide Casali,</a> about mental models for text editors give an idea of how the team are thinking about writing online in future.

On the speed / security front - having a fast hosted service, with a dedicated security team offers many of the upsides of static sites - in each case, you're less exposed to being hacked for different reasons, you're probably at less of a risk than if you ran it yourself. It's also cheap enough, to feel comprable to using a static site too. For me, the cost of Wordpress.com, on a personal plan offers many of the upsides of a static site (my own domain name, fast loading, no servers to worry about), at price point that is pretty easy to swallow.

So those are my reasons. Let's see if I can stick to them and actually keep getting posts our the door in 2017…

