---
ID: 140
post_title: Moving to WordPress
author: Yaniv
post_date: 2016-01-26 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/01/moving-to-wordpress.html
published: true
---
<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/pelican-to-wordpress.png" alt="pelican-to-wordpress.png" /> </p> </div>

<p> That was quick. </p>

<p> Couple of weeks ago I wrote about thinking to <a href="http://prodissues.com/2016/01/should-i-keep-using-pelican-or-move-to-wordpress.html">move my blog to Wordpress</a>. Since then, I've used Wordpress<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> in conjunction with my static blog, and published posts to both sites. This experiment helped me to reaffirm the pros and cons of using Wordpress, especially the part about concentrating on writing rather than site administration. During those two weeks I posted more, and became comfortable working with, and in, Wordpress. </p>

<p> When I realized that I started to publish first to my dummy Wordpress blog, and then reluctantly to my static blog, I made the decision to switch. Yesterday I completed the migration. </p>

<p> Following is the checklist I've used to manage the migration. It helped me going through the process with no downtime, and no prodissues :-) </p>

<!--more-->

<div id="outline-container-orgheadline1" class="outline-4">
<h4 id="orgheadline1">Decide between hosted an self-hosted</h4>
<div class="outline-text-4" id="text-orgheadline1">
<p> Initially I wanted to keep it as simple as possible, by paying for the basic plan on <a href="https://store.wordpress.com/plans/">Wordpress.com</a>. I wanted to avoide technical setup. Eventually, though, I went the self-hosting route for one simple reason - I wanted to keep the same URL format I had with the static site, but Worpress.com doesn't let you define the permalink format. </p>
</div>
</div>

<div id="outline-container-orgheadline2" class="outline-4">
<h4 id="orgheadline2">Select a hosting provider</h4>
<div class="outline-text-4" id="text-orgheadline2">
<p> There are tons of comparisons between every possible hosting provider, enough to get me confused about the pricing and the different features. Since my site is small and simple, and without a lot of traffic, I decided to take the economical route, and go with a shared hosting service. I then narrowed the list to Godaddy and Bluehost, and finally decided on Bluehost<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>, mainly because it's <a href="https://wordpress.org/hosting/">endorsed by Wordpress</a>. </p>
</div>
</div>


<div id="outline-container-orgheadline3" class="outline-4">
<h4 id="orgheadline3">Local installation of WP</h4>
<div class="outline-text-4" id="text-orgheadline3">
<p> Wordpress famous claim for 5 minute installation isn't a cliche. I just had to follow <a href="https://codex.wordpress.org/Installing_WordPress_Locally_on_Your_Mac_With_MAMP">this guide</a>. </p>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-4">
<h4 id="orgheadline4">Import all of my posts to the local install</h4>
<div class="outline-text-4" id="text-orgheadline4">
<p> My plan to export and import an RSS feed from my static blog to Wordpress didn't work. WordPress RSS importer didn't recognize my Pelican generated RSS feed, so I had to spend some time researching for an alternative. </p>

<p> My posts are written in one of two formats - markdown or <a href="http://orgmode.org/">org-mode</a>. Migrating the org-mode based posts was easy, using Emacs' <a href="https://github.com/punchagan/org2blog/">org2blog</a> package. Pushing the markdown files was a little trickier. Eventually, with the help of <a href="http://emacs.stackexchange.com/q/5465/10150">this stack-overflow answer</a>, I converted those markdown posts into org-mode, using pandoc. I had to make a little bit of cleaning<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup> to the output, but overall that process wasn't too complicated. </p>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-4">
<h4 id="orgheadline5">Connect to Bluehost</h4>
<div class="outline-text-4" id="text-orgheadline5">
<p> Now that I had my local installation of Wordpress up and running with all my posts, it was time to set Wordpress on Bluehost. </p>

<p> Logging-in to my Bluehost panel for the first time was intimidating. The endless list of tools got me thinking that I might end up doing even more site administration work than I did before. I hoped, though, that this will be the case only during the initial setup<sup><a id="fnr.4" class="footref" href="#fn.4">4</a></sup>, and that I will not have to log in to that panel again after I deploy my site. </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/bluehost-cpanel.png" alt="bluehost-cpanel.png" /> </p> <p><span class="figure-number">Figure 2:</span> The cPanel - lots of tools, though I had to use only few to get my site live</p> </div>
</div>
</div>

<div id="outline-container-orgheadline6" class="outline-4">
<h4 id="orgheadline6">Connect to WP with a temporary URL</h4>
<div class="outline-text-4" id="text-orgheadline6">
<p> When I signed up with Bluehost, I got an email with a list of temporal IPs and ftp configuration. This way I could set up my Wordpress blog before having to point my domain to it. At first, I wasn't able to access my temporary URL, even after reading <a href="http://www.expression-web-tips.com/accessing-bluehost-domains-from-a-temporary-web-address/">this detailed article</a>. It probably took time for the URL to be activated and link to my account, because I was able to access it eventually (after couple of hours) without doing anything special. </p>

<p> As soon as I connected to the temporary URL, a Wordpress installation process started, and 5 minutes later I had Wordpress installed on my production environment. Exciting! </p>

<p> The first thing I've noticed when logging in to my fresh self-hosted Wordpress was this gaudy green icon - the Mojo market place. I didn't know what Mojo is, and didn't care to know. I just wanted it out of my dashboard. Googling it, I <a href="https://wordpress.org/support/topic/how-do-i-remove-mojo-marketplace-from-admin-header">found</a> that it's just a plugin that can be removed. Removed it I had.<sup><a id="fnr.5" class="footref" href="#fn.5">5</a></sup>. </p>
</div>
</div>

<div id="outline-container-orgheadline7" class="outline-4">
<h4 id="orgheadline7">Set FTP access</h4>
<div class="outline-text-4" id="text-orgheadline7">
<p> With a little hand holding from the Bluehost support team, I was able to connect to my temporary URL via ftp. Here's the FileZilla configuration I had to set: </p>

<div class="figure"> <p><img src="http://media.prodissues.com/images/2016/01/filezilla-setup.png" alt="filezilla-setup.png" /> </p> <p><span class="figure-number">Figure 3:</span> My FileZilla Configuration - note the non-default Encryption type</p> </div>

<p> FTP connection will be useful later on, when I'll need to push my local environment and database to production. </p>
</div>
</div>

<div id="outline-container-orgheadline8" class="outline-4">
<h4 id="orgheadline8">Themes that I like</h4>
<div class="outline-text-4" id="text-orgheadline8">
<p> Back to my localhost Wordpress, I need to chose a theme, and get ready to push everything to Bluehost. Here's the list of themes I liked: </p>

<ul class="org-ul">
<li><a href="https://theme.wordpress.com/themes/big-brother/">Big brother</a></li>
<li><a href="https://theme.wordpress.com/themes/big-brother/">Twenty twelve</a> - I don't like the font though.</li>
<li><a href="http://p2theme.com/">P2</a></li>
<li><a href="https://theme.wordpress.com/themes/everyday/">Everyday</a> (75$)</li>
<li><a href="https://wordpress.org/themes/twentysixteen/">Twenty Sixteen</a> (that's the one I chose.)</li>
</ul>
</div>
</div>

<div id="outline-container-orgheadline9" class="outline-4">
<h4 id="orgheadline9">Import the local installation to the hosting service</h4>
<div class="outline-text-4" id="text-orgheadline9">
<p> I used <a href="https://www.bluehost.com/blog/wordpress-2/faq-how-do-i-move-my-wordpress-website-to-bluehost-1787/">Bluehost's excellent guide</a> for that. At first, I messed things up by not following it step-by-step - I pushed my local database before copying my local Wordpress installation and overriding that on the host. As a result I had to run the Wordpress installation on Bluehost again. Not a big deal, but a reminder about the complexity behind the scene... </p>
</div>
</div>

<div id="outline-container-orgheadline10" class="outline-4">
<h4 id="orgheadline10">Set the permalink format</h4>
<div class="outline-text-4" id="text-orgheadline10">
<p> My blog is up and running on a temporary URL. This post for example was accessible with the following URL (not anymore, though): </p>

<p> <code>http://69.195.124.143/~prodissu/2016/02/moving-to-wordpress.html</code> </p>

<p> I now had to make sure that my URLs are formatted correctly. That was easily done within the wp-admin. The setting is under setting-&gt;permalink. </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/wp-admin-set-permalink.png" alt="wp-admin-set-permalink.png" /> </p> <p><span class="figure-number">Figure 4:</span> Setting the permalink format</p> </div>

<p> Now I had to make sure that when I switch to Wordpress, all of my existing posts will maintain the same URL. So, I run through a sample of posts, replaced the temporary part of the URL (the <code>http://69.195.124.143/~prodissu/</code> in the example above), which led to the Wordpress installation, with my domain name. Doing so I've expected to land on the same post on my static, and still live, site. When I made sure this is the case, I was ready for the final part - the cut-off. </p>
</div>
</div>

<div id="outline-container-orgheadline11" class="outline-4">
<h4 id="orgheadline11">Figure how to transfer my domain</h4>
<div class="outline-text-4" id="text-orgheadline11">
<p> My domain registrar is Godaddy, and my static site was running on AWS S3. To move my domain to link to Bluehost instead of AWS, I had to change the configuration of the nameservers on Godaddy. <a href="https://my.bluehost.com/cgi/help/432">Here's a guide</a> for how to do that. </p>

<p> One small consideration at that point - I have a bucket on S3 dedicated to all the media file I use in posts. I wanted to keep this bucket and not move those media files into the Wordpress database. Just in case I change my mind again, and decide to switch back to static blog at some point. I also kind of wanted to keep that neat workflow I created to <a href="http://prodissues.com/2016/01/uploading-images-to-amazon-s3.html">upload media files to S3</a>... </p>

<p> To maintain that bucket and sub-domain, I had to <a href="https://my.bluehost.com/cgi/help/559#add">define a CNAME</a>, now on the Bluehost console. </p>

<p> With that, my site is up and running on Wordpress. Hooray! </p>

<p> There's only one open task left: </p>
</div>
</div>

<div id="outline-container-orgheadline12" class="outline-4">
<h4 id="orgheadline12">Import the disqus comments</h4>
<div class="outline-text-4" id="text-orgheadline12">
<p> I exported the comments from disqus, but didn't find a way to import them into Wordpress. </p>
</div>
</div>


<div id="outline-container-orgheadline13" class="outline-2">
<h2 id="orgheadline13">Helpful links:</h2>
<div class="outline-text-2" id="text-orgheadline13">
<ul class="org-ul">
<li><a href="https://codex.wordpress.org/Installing_WordPress_Locally_on_Your_Mac_With_MAMP">Installing Wordpress Locally on Your Mac With MAMP</a></li>
<li><a href="http://www.expression-web-tips.com/accessing-bluehost-domains-from-a-temporary-web-address/">Accessing Bluehost Domains and ftp from a Temporary Web Address</a></li>
<li><a href="https://my.bluehost.com/cgi/help/wordpress_url">Using Your Temporary URL with Wordpress</a></li>
<li><a href="https://www.bluehost.com/blog/wordpress-2/faq-how-do-i-move-my-wordpress-website-to-bluehost-1787/">How Do I Transfer My Wordpress Website To Bluehost?</a></li>
</ul>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> First, I created a blog in Wordpress.com. Then I installed Wordpress on my local machine. </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> So far I'm happy with Bluehost. I had to chat with their support twice, once to help me with connecting to the ftp, and then to white-list my IP for remote publishing. Support was prompt and helpful in both cases. </p></div></div>

<div class="footdef"><sup><a id="fn.3" class="footnum" href="#fnr.3">3</a></sup> <div class="footpara"><p class="footpara"> I had to add the headers to the org file and fix some of the footnotes' references. </p></div></div>

<div class="footdef"><sup><a id="fn.4" class="footnum" href="#fnr.4">4</a></sup> <div class="footpara"><p class="footpara"> It's probably too early to answer this question, but since making the cut-off, I didn't have to log in to the cPanel. </p></div></div>

<div class="footdef"><sup><a id="fn.5" class="footnum" href="#fnr.5">5</a></sup> <div class="footpara"><p class="footpara"> I removed it so quickly, that I didn't even take a screen shot to include here. </p></div></div>


</div>
</div>