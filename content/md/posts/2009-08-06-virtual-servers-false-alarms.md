

{:author "admin", :title "Virtual servers and false alarms", :date "2009-08-06 00:22:59", :publish-date "Thu, 06 Aug 2009 00:22:59 +0000"}



<!-- content below -->

When you start looking after virtual machines instead of buying shared hosting, you very quickly realise how important RAM is to making a server run properly.

I'm using a machine with a fairly heft chunk of free memory, but recently when shelling into the box to check memory usage I've have some pretty scary stats that look like I've hardly got any memory left at all:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/08/stemcaa1-—-ssh-—-bash-—-top.png"><img class="alignnone size-large wp-image-191" title="stemcaa1- ~ — ssh — bash — top" src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2009/08/stemcaa1-—-ssh-—-bash-—-top-1024x653.png" alt="stemcaa1- ~ — ssh — bash — top" width="655" height="418" /></a>

<strong>No cause for concern</strong>

I was understandably a bit confused when I first saw this, and contacted support at Memset, and I'm pretty satisfied with their answer.
<blockquote>This is actually the way Linux handles memory management - it's rather complicated. As long as your swap isn't very high, you're not actually using that much memory. This link sum's it quite well:
<a style="color: #2a5db0;" href="http://www.linuxvox.com/linux-articles/memory-and-swap/2-how-much-free-memory-does-my-linux-server-really-have" target="_blank">http://www.linuxvox.com/linux-articles/memory-and-swap/2-how-much-free-memory-does-my-linux-server-really-have</a></blockquote>
By default the Linux Kernel is designed to use as much free ram as possible when it can, and then release as and when it's needed by other apps.

Panic over.

