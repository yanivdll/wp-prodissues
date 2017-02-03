---
ID: 83
post_title: >
  Should I Keep Using Pelican Or Move To
  WordPress
author: Yaniv
post_date: 2016-01-18 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/01/should-i-keep-using-pelican-or-move-to-wordpress.html
published: true
---
<p> I'm currently using <a href="http://docs.getpelican.com/en/3.6.3/">Pelican</a> to power this site. Pelican is a static site generator (SSG) that takes markdown files as an input and generate html pages as an output; no database, no server-side logic; just simple, static HTML. </p>

<p> When I created this blog, using Wordpress or Tumblr wasn't an option, simply because every geeky blogger I follow wrote about how much those platforms suck, and how using SSG to run their blog were the best move they have ever made. I chose Pelican<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>, because of its popularity and because it is written in Python. </p>

<!--more-->

<p> Recently, though, I've started to question my decision. I found that I spend more time on site administration than on  writing. Tinkering with the plumbing of the site meant that I have less time to write. And since getting more productive with my writing is a <a href="http://prodissues.com/2015/12/thinking-with-words.html">personal goals</a>, I've started to play with the idea of switching to Wordpress. </p>

<p> The first thing that I've learned was that moving <i>from</i> SSG <i>to</i> Wordpress meant swimming against the current. It isn't the cool thing to do. Yet. As such, no one writes about it, except for Martin, who shares in his post <a href="http://ronn-bundgaard.dk/blog/the-static-site-generator-pelican-vs-wordpress/#comment-14937">"The Static Site Generator Pelican VS WordPress"</a><sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup> many of the pains I'll be discussing here in a moment. </p>

<p> With that, here's is my assessment of what I like and dislike about Pelican, and what I expect to get (or not) from Wordpress. I hope this will help me make up my mind, and get clearer on what should be my next steps. </p>

<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">Things that I like about Pelican</h2>
<div class="outline-text-2" id="text-orgheadline1">
<ul class="org-ul">
<li><b><b>The coding experience</b></b> - I'm not a full time developer. Building this site helps me maintain <i>some</i> level of coding proficiency.</li>
<li><b><b>Writing in markdown</b></b> - when writing a post, I can focus on the content and not on the format and styling.</li>
<li><b><b>No database and no server side logic</b></b> - pages load faster, and my site is supposed to be more secure (since everything is static, there is almost no way to hack it).</li>
<li><b><b>Absolute control</b></b> - the entire site is encapsulated in one <a href="https://github.com/yanivdll/prodissues">git repository</a> that includes the content and the HTML template. It means that moving to another hosting or SSG is easy.</li>
<li><b><b>Cost</b></b> - running a static site is almost free. All I have to pay for is the domain name (~13$/year) and the Amazon S3 storage (~0.5$/month).</li>
</ul>
</div>
</div>

<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Things that I don't like</h2>
<div class="outline-text-2" id="text-orgheadline2">
<ul class="org-ul">
<li><b><b>Generating the HTML pages is slow</b></b> - every time I'm adding a new post, or editing an existing one, I have to regenerate the site. This process takes time, and gets longer as I accumulate more and more posts. Pankaj More put it nicely in his article <a href="http://blog.pankajmore.in/static-site-generators-focus-on-the-wrong-thing">Static Site Generators Focus On The Wrong Thing</a>.</li>

<li><b><b>Too much friction</b></b> - no matter how automated my process is, it's still cumbersome. Just take a look at all the touch-points in my publishing workflow:</li>
</ul>

<div class="figure"> <p><img src="http://media.prodissues.com/images/2016/01/posting-workflow-with-pelican.png" alt="posting-workflow-with-pelican.png" /> </p> </div>

<ul class="org-ul">
<li><b><b>No mobile support</b></b> - since Pelican runs on the desktop, I have no way to write a post on my iPhone and publish it directly to my blog. This adds friction to my writing workflow, and hinders me from writing more spontaneously.</li>

<li><b><b>Maintenance and site administration</b></b> - I'm getting tired of running 2 terminals at all times, just to regenerate the site and keep a development server live.</li>

<li><b><b>Slow iterations</b></b> - adding new functionality, improving existing one, or making some UI changes takes a lot of time. Again, this is valuable time that I prefer spending on writing.</li>

<li><b><b>Flaky org-mode integration</b></b> - I write most of my posts in <a href="http://orgmode.org/">Org-mode</a>, using Emacs. Pelican and org-mode doesn't work very well together. While there's a plugin for Pelican that reads org files(org_reader), it relies on my Emacs configuration. And since I'm experimenting with Emacs a lot, this plugin constantly breaks. And when that's happens, most of my posts (those that are in org-mode), won't be generated, and disappeared from the site.</li>
</ul>

<div class="figure"> <p><img src="http://media.prodissues.com/images/2016/01/error-make-html.png" alt="error-make-html.png" /> </p> <p><span class="figure-number">Figure 2:</span> Working with org and Pelican isn't a smooth sail</p> </div>

<p> And when it comes to Wordpress, here are the goods and the bad: </p>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">The Goods</h2>
<div class="outline-text-2" id="text-orgheadline3">
<ul class="org-ul">
<li><b><b>The writing experience</b></b> - starting, writing and publishing a new post is frictionless.</li>

<li><b><b>Functionality</b></b> - comments, search, categories and tags filtering, social functionality, and advanced post status management, are all part of the platform.</li>

<li><b><b>Native commenting system</b></b> - if you'll read <a href="http://prodissues.com/2015/11/adding-a-commenting-system.html">this post</a>, you'll find that I'm not a big fan of disqus. Using the native Wordpress commenting system is a big plus for me.</li>

<li><b><b>One dashboard</b></b> - I use google analytics to monitor trafic, and disqus dashboard to manage comments. I like the idea of getting all this information in one place. Additionally, I currently don't have a way to manage posts and drafts, since they are just files in a folder. Having a dashboard where I can take a glimpse and see how my site looks like is another benefit.</li>

<li><b><b>Community</b></b> - I'm getting warmer to the idea of being part of the Wordpress community; of following, and being followed by, other interesting bloggers, and having my posts discoverable across the Wordpress ecosystem.</li>
</ul>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Concerns</h2>
<div class="outline-text-2" id="text-orgheadline4">
<ul class="org-ul">
<li><b><b>Lack of control</b></b> - that's my biggest concern. When I <a href="http://prodissues.com/2015/06/why-i-decided-to-move-away-from-evernote.html">left Evernote</a>, I've decided that I'll never use proprietary formats; that I will keep my information in plain text. I didn't want my data to be reliant on a company that can go bust, or mess up with my it. I'm not sure this is the case with Wordpress, because people seem to not have issues exporting their blogs and moving elsewhere, and because it's open source. So there will always be a way to gain control over my data if needed. But still, having a black box that I know not how it operates is bothering.</li>

<li><b><b>Complexity</b></b> - I won't be able to wrap my site with a bunch of markdown files.</li>

<li><b><b>Cost</b></b> - Wordpress will cost much more, regardless if I use Wordpress.com for hosting, or going the wp-admin route.</li>

<li>Performance - not high on my priority, at least for now, but still, this is one of the main issues people mention when talking about their decision to switch from Wordpress to static sites.</li>
</ul>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-2">
<h2 id="orgheadline5">Conclusion</h2>
<div class="outline-text-2" id="text-orgheadline5">
<p> As I'm writing this post, my gut feeling tells me that I've already made a decision, and that I use this post as a way to rationalize the decision to myself. <b><b>I'm going to migrate my blog to Wordpress</b></b>. </p>

<p> I'll do it gradually, though, and make a "cut-off" only when I'm sure the benefits out-weight the drawbacks. I've already opened a blog in Wordpress. It uses the default settings and URL (<a href="http://yanivgilad.wordpress.com/">yanivgilad.wordpress.com</a>). I will start pushing there everything I post<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup> some stuff there, including new posts that I push to pelican, to play around with the system, and see how it feels. </p>
</div>
</div>

<div id="outline-container-orgheadline6" class="outline-2">
<h2 id="orgheadline6">Updates</h2>
<div class="outline-text-2" id="text-orgheadline6">
<ol class="org-ol">
<li>Fixed the issue.</li>
<li>Pelican refuses to generate this post. There's probably something wrong with the org-reader plugin, or my Emacs config... but that's an example for the friction and site administration work I'm trying to avoid.</li>
</ol>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> For a list of almost every SSG available, check out <a href="https://www.staticgen.com/">StaticGen</a>. </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> Martin, by the way, decided to move to Wordpress. </p></div></div>

<div class="footdef"><sup><a id="fn.3" class="footnum" href="#fnr.3">3</a></sup> <div class="footpara"><p class="footpara"> I installed <a href="https://github.com/punchagan/org2blog/">org2blog</a> in my Emacs, and plan to use it to push my org-mode based posts to Wordpress. </p></div></div>


</div>
</div>