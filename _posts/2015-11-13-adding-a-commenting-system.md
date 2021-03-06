---
ID: 44
post_title: Adding a Commenting System
author: Yaniv
post_date: 2015-11-13 05:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/11/adding-a-commenting-system.html
published: true
---
<p> I decided to add comments to this blog. Initially, I didn't want comments, because I didn't see their value, and thought of them mainly as spam. Now I know, though, that the real reason was an anxiety from having other people commenting on my writing. But as I started to post more frequently, and share my learning and experiences, an urge to hear other people thoughts and opinions emerged. I know I'm making a lot of mistakes along the way. Letting other<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> to comment and point to those mistakes seems like a good way to improve. </p>

<p> And so, I begun to search for a commenting system. </p>

<p> My first option was disqus. Why? first, because it's synonymous to comments. Second, becaue <a href="http://docs.getpelican.com/en/latest/">Pelican</a>, which generates this site, supports it by default. I created an account with disqus, but changed my mind just before implementing their widget. I was always reluctant to install 3rd party services in my site, and having to disable "cookie targeting" and "merchant code" related settings, when configuring the commenting widget, didn't help. </p>

<p> Therefore, I started to look for a less obvious solution. Googling "pelican comments" and "static site comment system" reeled few options: </p>

<ul class="org-ul">
<li><a href="https://github.com/getpelican/pelican-plugins/tree/master/pelican_comment_system">Pelican comment plugin</a></li>
<li><a href="http://tildehash.com/?page=hashover">Hashover</a></li>
<li><a href="https://posativ.org/isso/">ISSO</a></li>
</ul>

<p> After doing some research, I decided that those plugins won't work for me. To explain why, I should mention that my site is static. It means that it includes nothing but simple HTML pages, and static files like images and css. Those pages live in a dumb Amazon-S3 storage, and are served "as is". There are no dynamic elemnts, such as database, involved in generating and serving them. </p>

<p> In order to enable comments, though, there must be a dynamic component somewhere in the flow. This component should intercept new comments, store them in a database or files, and tie them together with the relevant post. So, if I don't want to use a cloud service, like disqus, I should either add logic to my hosting server, or become that logic myself. </p>

<p> Since, as I mentioned, S3 is nothing but storage, I have no way to run server-side scripts on it. Nor do I want to, since it will dilute the whole concept of static website... That took Hashover and ISSO off the table, because both require server-side PHP scripts. </p>

<p> I then tried the pelican comment plugin. Installation was quick and smooth, but eventually, like the other options, this plugin didn't work for me either. Well, not that it didn't work, just that I had to work for it. </p>

<p> Unlike the other plugins, this one requires no back-end service. It's truly static. But as I mentioned, there must be a dynamic component <i>somewhere</i>. In this case, this component was me. With this plugin, comments are sent over email. I had to save each email as a file in a specific folder and give it a specific name. I then had to render the site and push it to S3. I had to repeat this process for every new comments. I don't expect many comments, but still, this doesn't look like a scalable or sustainable solution. </p>

<p> And so, disappointed of my failure to find an alternative, I went back to the first option. In less than 5 minutes I got a disqus commenting widget live on my article pages. I'm still uncomfortable having that 3rd party component hosted in my site, but I will keep it until I find a better solution. </p>

<p> Leave a comment if you know of any alternatives I should take a look at... </p>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> Not that I think anyone reads this blog, except for my wife when I ask her to proof read something, or friend whom I force into reading an article here and then. </p></div></div>


</div>
</div>