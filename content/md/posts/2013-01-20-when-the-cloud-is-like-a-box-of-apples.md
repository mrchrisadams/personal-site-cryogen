

{:author "admin", :title "When the cloud is like a box of apples", :date "2013-01-20 14:51:48", :publish-date "Sun, 20 Jan 2013 14:51:48 +0000"}



<!-- content below -->

Last week, I gave a talk at LDNdevops, about the [steps that you can take as a devops engineer to make your cloud computing more planet friendly][1], and while I was there, watching Sam Pointer's talk about using Chef to manage thousands of virtual machines, I learn of an interesting side effect of Amazon providing abstract virtual machines through its compute cloud AWS, rather than selling actual servers.

### When you have a box of apples, some are going to be bad

Back when I used to work at Headshift, I remember having a conversation with a friend of mine, [Stu Calum][2] telling me how he had heard AWS being described as something like create of apples - Individually they're fine, but every once in a while you come across a bad apple[^1]. 

So whenever you're working out how you might build out infrastructure, you need to expect that one or more nodes will be will blink out of existence with little or no warning, on a more regular basis than that provided by more traditional colocation, or virtual private servers. 

### Not so much bad apples, as good, great, okay, bad and terrible apples

One thing that that really leapt out at me was how Sam in his talk mentioned how they use Chef to provide an audit of the 'quality' of their machines by benchmarking how well the difference virtual machine instances they have compare to the baseline in a graphical fashion.

They do this because while we as customers are buying "large", "small", "medium" and "extra large" virtual machines, we have no real idea what the actual hardware they run really is, or where the metal lies in a typical server lifecycle. So on one day you could be spinning up a load of aging servers, that are being sold as "medium" VM instances but are much slower than normal, but another day you might luck out and spin up some virtual machines running on superfast, shiny new hardware, giving you loads of free performance.

This graph they use helps them visualise the relative performance of the machines they're using, by comparing the area underneath the graph:

<a href="http://chrisadams.me.uk/wordpress/wp-content/uploads/2013/01/bang_for_buck.png"><img src="http://chrisadams.me.uk/wordpress/wp-content/uploads/2013/01/bang_for_buck.png" alt="bang_for_buck" width="800" height="600" class="alignnone size-full wp-image-861" /></a>


In a given corner if the area is large, they have a load of fast machines, and they're better off holding on to them. If the corner is smaller, it may be worth switching those VMs off, and spinning up some new ones to do the same job the old ones were doing, in the hope that [they give more bang for their buck][4].

There's more available in this [published paper on USENIX here][3], and if you find this interesting, you'd do well to follow [Sam Pointer's blog][6] - it's full of little gems like this.



[^1]: To give full credit, I think this description came from [Stephen Nelson Smith of Atalanta Systems][5],



[1]: http://lanyrd.com/2013/ldndevops-january/sccfwf
[2]: http://www.headshift.com/our-blog/author/stuart-cullum
[3]: https://www.usenix.org/system/files/conference/hotcloud12/hotcloud12-final40.pdf
[4]: http://blog.sam-pointer.com/2013/01/10/bang-for-your-buck-on-amazon-ec2
[5]: http://atalanta-systems.com/
[6]: http://blog.sam-pointer.com/

