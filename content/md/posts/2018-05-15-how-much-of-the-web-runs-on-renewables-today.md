

{:author "mrchrisadams", :title "How much of the web runs on renewables today?", :date "2018-05-15 11:49:27", :publish-date "Tue, 15 May 2018 11:49:27 +0000"}



<!-- content below -->

As part of the work I'm doing on the <a href="http://planetfriendlyweb.org/">Planet Friendly Web</a>, I'm trying to get access to data that I can base the guide on. In some cases this involves <em>creating</em> datasets from existing data. Here I share some findings from a dataset I generated along the way.

For example, to get a figure on how much of the web runs on renewable power, I started with a dataset of the top 1 million domains by traffic from Alexa.com, then run the list against the <a href="https://www.thegreenwebfoundation.org/green-web-feed/">Green Web Foundation's own API,</a> which maintains a list of which domains run on renewable power.

To do this, involves making something like 100k API requests, so I created a screenscraper to carry out the job, and take care of retries, failed requests and so on. You can see it <a href="https://github.com/productscience/pfw-top-mil">here on github</a>.

I've uploaded the <a href="https://datbase.org/view?query=8be6d29e63b010bb4240dc366e578e1f7f91e89a73062a7802c5b83d9cc793fe">dataset created to datbase</a>, partly as an experiment in making it available in a decentralised way, but also partly try out the workflow for publishing data.

So, now we have some data, let's see what we can do with it, right?

<h3>Doing some analysis and some interesting findings</h3>

I have an <a href="https://github.com/productscience/planet-friendly-web/blob/master/binder/how-much-web-renewable.ipynb">earlier exploration of the data in a notebook on github,</a> but when working with this data, I 'm bit embarrassed to say I forgot how to use the Dataframe filters to slice the data quickly.

So instead, I've used Open Refine. You could probably store this in a Google spreadsheet too, as 100k rows is big, not but <em>THAT</em> big.

<h4>Anyway, what do we see?</h4>

There's a few interesting findings just from faceting data like below in Openrefine,  and sorting by count along a few dimensions:

<img class="alignnone size-full wp-image-2979" src="https://mrchrisadamsblog.files.wordpress.com/2018/05/screen-shot-2018-05-15-at-12-07-36.png" alt="Screen Shot 2018-05-15 at 12.07.36.png" width="2466" height="1324" />

If you're not familiar with OpenRefine, I'll summarise what's visible in this view:

<ul>
    <li>Youtube.com is now more popular than google.com. Who knew?</li>
    <li>The top three websites in the world run on renewable power. Huzzah!</li>
    <li>Based on the greenweb foundation's data, around 7% of the web the most popular domains on the net run on renewable power.</li>
    <li>Hetzner AG, a German hosting company hosts more domains running on green power than Google does.</li>
    <li>Amazon doesn't appear here at all as a green provider.</li>
</ul>

After a slow start, I understood Amazon to be a HUGE player here, and while they have a nice shiny page <a href="https://aws.amazon.com/about-aws/sustainability/">showing off their windfarms and how much renewable power they use</a> , they also run a load of their servers on coal. That they don't appear may be an artefact of the Green Web Foundation going by an organisation's entire power mix, to decide whether a company is running on green power or not.

I think need to check with Rene at the Green Web Foundation to see.

<h4>Fancy playing too? Come hang out on slack</h4>

This shows some pretty superficial analysis, but there's already some interesting nuggets here.

If working with this data sounds interesting to you, let me know in the comments - I'm looking for collaborators on the Planet Friendly Web Guide.

Alternatively, <a href="https://join.slack.com/t/sustainableux/shared_invite/enQtMzY0MTQ0NjY5OTQxLWIyYmFhMTkxMjM3ZjMyMjFiYWIyY2JiN2VlMDQ5YWVhZWYwMjdiNzRhNzI0Y2Y2OWE1MGI2MjY2M2EzNzBmOGU">come hang out in the sustainableux.com slack channel</a>, where there's a nice little community growing around sustainable web design.

<strong>If you prefer email</strong>

It turns out there's a <a href="https://www.w3.org/community/sustyweb/">W3C Sustainable web design group</a>. Here's my <a href="https://lists.w3.org/Archives/Public/public-sustyweb/2018May/0011.html">post to the mailing list,</a> if you'd prefer to communicate there via email.

&nbsp;

&nbsp;

