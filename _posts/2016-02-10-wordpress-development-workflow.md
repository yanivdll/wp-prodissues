---
ID: 300
post_title: My WordPress Development Workflow
author: Yaniv
post_date: 2016-02-10 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/02/wordpress-development-workflow.html
published: true
---
<p> I currently use a child-theme for this site<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>, its parent being <a href="https://wordpress.org/themes/twentysixteen/">twentysixteen</a>. I  keep modifying this theme on my local machine and push updates to my live site. But in parallel, I want to start building a completely new theme, based on the starting <a href="http://underscores.me/">_s</a> theme. I'm uncomfortable developing this new theme within the same local environment; I want, instead, to create a playground where I can experiment, knowing it's completely isolated from my production environment. </p>

<!--more-->

<p> With that goal in mind, I installed a second instance of WordPress on my local machine, and now I have 3 environments - production(that's where my live site reside), staging and development. </p>

<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Running two WordPress instances on the same machine</h2>
<div class="outline-text-2" id="text-orgheadline2">
</div><div id="outline-container-orgheadline1" class="outline-3">
<h3 id="orgheadline1">Folder structure</h3>
<div class="outline-text-3" id="text-orgheadline1">
<p> Initially, I had WordPress installed in a folder called <code>wordpress</code>. To prepare for the second install, I created the following hierarchy: </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/wp-folders.png" alt="wp-folders.png" /> </p> </div>

<p> I moved the content of my original WordPress to the <code>/prodissues-staging</code> folder. I then had to go to <a href="https://www.mamp.info/en/">MAMP</a> and change the "Document Root" setting, to point to the new location, so that when I visit <code>localhost:8888</code>, I still land on my site. </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/mamp-prodissues-staging.png" alt="mamp-prodissues-staging.png" /> </p> </div>

<p> Next, I downloaded WordPress to the <code>prodissues-dev</code> folder. To start the installation process, I had to go back to MAMP and change the "Document Root" to point to that folder: </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/mamp-prodissues-dev.png" alt="mamp-prodissues-dev.png" /> </p> </div>

<p> At that point I was ready to install WordPress in my development environment. This is the same process as installing WordPress for the first time, including the creation of a new database<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup> . To refresh your memory on how to do it, here's WordPress <a href="https://codex.wordpress.org/Installing_WordPress#Famous_5-Minute_Install">"Famous 5-Minute Install"</a> guide. </p>
</div>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">Switching between environments</h2>
<div class="outline-text-2" id="text-orgheadline3">
<p> I now had two WordPress installations on my local machine (and one hosted). Switching from one to the other is as simple as changing the "Document Root" in MAMP, as was shown above. </p>

<p> What left to be done is to define a workflow that will help me keeping the different environments fresh, while making sure the live site (i.e. production environment) is safe from what's going on in the development environment. </p>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Development workflow</h2>
<div class="outline-text-2" id="text-orgheadline4">
<p> I now have 3 WordPress environments: </p>

<ul class="org-ul">
<li>Production (hosted)</li>
<li>Staging (local)</li>
<li>Development (local)</li>
</ul>

<p> My plan is to make sure that staging is always in sync with production. I'll build my new theme in the development environment, and push it to staging when it's ready. If everything works fine in staging (which is, again, almost identical to the live site) then I'll push the new theme to production. </p>

<p> Here's a sketch that illustrates the separation and interaction among the 3 environments: </p>

<div class="figure"> <p><img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/wp-environments.jpeg" alt="wp-environments.jpeg" /> </p> </div>

<p> And here's the logic behind this architecture: </p>

<ul class="org-ul">
<li>The most important resource that I would like to protect is the production database, since it holds the content of my blog. I might be missing something here, but I see no reason to ever override it with a version of the database from other environments. Therefore, the production database can only be pulled to the staging or development environemnts<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>.</li>
<li>I shouldn't push files from development directly to production. I should move them instead to staging. This will protect my live site from un-tested or broken code.</li>
<li>Staging is where new code is tested. From there it can be pushed only one way - to production via ftp. Again, there's no upload of the database to production.</li>
</ul>

<p> This one-way streets architecture should give me the peace of mind to build and breaking stuff, knowing that whatever I do won't affect the other 2 sane environments. </p>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-2">
<h2 id="orgheadline5">Open question:</h2>
<div class="outline-text-2" id="text-orgheadline5">
<ul class="org-ul">
<li>Is there any reason that I haven't thought of to push database from staging to production?</li>
</ul>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> Feel free fork it on GitHub - <a href="https://github.com/yanivdll/twentysixteen-child">https://github.com/yanivdll/twentysixteen-child</a> </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> With one exception - the name of the new database should be unique. I called mine <code>prodissues-dev</code>. </p></div></div>

<div class="footdef"><sup><a id="fn.3" class="footnum" href="#fnr.3">3</a></sup> <div class="footpara"><p class="footpara"> I use <a href="https://github.com/wp-sync-db/wp-sync-db">wp-sync-db</a> to pull the database and files from production to dev and staging. </p></div></div>


</div>
</div>