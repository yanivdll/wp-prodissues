---
ID: 841
post_title: 'Magit &#8211; My Simple Workflow'
author: Yaniv
post_date: 2016-10-05 20:30:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/10/magit-my-simple-workflow.html
published: true
---
I still not fluent with Magit's terminology and workflow. Probably because I'm not using git, in general, too often. When I do, and when I try to use Magit as the interface, I usually get confused by the wealth of options and switches, and resort to git in the terminal.

Today I decided to give Magit yet another try. I read the <a href="https://magit.vc/manual/magit/Getting-started.html#Getting-started">Getting Started</a> guide, and now things makes much more sense. However, I can see how I forget what I've just read a week from now, so here's the gist of that, my simplest cheat-sheet:
<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">(Ma)git status:</h2>
<div class="outline-text-2" id="text-orgheadline1">

 <code>C-x g</code>

</div>
</div>
<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">(Ma)git add</h2>
<div class="outline-text-2" id="text-orgheadline2">

 For each unstage file: <code>s</code>

</div>
</div>
<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">(Ma)git commit</h2>
<div class="outline-text-2" id="text-orgheadline3">

 <code>c c</code>

Type the commit note and then <code>C-c C-c</code> to create the commit.

</div>
</div>
<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">(Ma)git push</h2>
<div class="outline-text-2" id="text-orgheadline4">

 <code>p u</code>

Done. Now I can type <code>q</code> to close the Magit pop-up buffer, and be back on the file I was working on.

</div>
</div>