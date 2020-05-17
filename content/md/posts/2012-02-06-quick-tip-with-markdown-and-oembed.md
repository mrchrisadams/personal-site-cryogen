

{:author "admin", :title "Quick tip with Markdown and oEmbed", :date "2012-02-06 23:14:09", :publish-date "Mon, 06 Feb 2012 23:14:09 +0000"}



<!-- content below -->

I write nearly all of the posts on this post in Markdown - it's a nice midway point between plain text, which readable but very limited, and full on html, which is powerful, but comparatively horrible to read.

However, I could never workout how to embed media in Wordpress blog if the content is being passed through a Markdown filter.

Normally, you should be able to just add a direct link to the video, and it should be replaced with a video element rendered inline, but as soon as the Markdown filter gets involved things aren't so simple.

### The solution as ever is embarrassingly simple

Not _as_ simple, but still pretty simple it turns out, once you decide to [actually look through the docs](http://codex.wordpress.org/Embeds "Embeds &laquo; WordPress Codex"). The trick is to use a shortcode, like so, showing this demo of Ubuntu's new HUD for their forthcoming OS release in April:

<pre>

  [embed]http://link.to.youtu.be/v=w_WW-DHqR3c[/embed]

</pre>

And it works fine!

See?   

[embed]http://www.youtube.com/watch?feature=player_embedded&v=w_WW-DHqR3c[/embed]


