---
ID: 59
post_title: Copy Git Changes to a New Branch
author: Yaniv
post_date: 2015-11-12 05:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/11/copy-git-changes-to-a-new-branch.html
published: true
---
<p> I'm still not fluent with git and version control. I manage repositories for projects I'm working on, but sill have hard time managing my changes, commits and branches. </p>

<p> For example, I'm currently working on integrating Emacs's org-mode support to Pelican, a static web-page generator I use for this blog. I was proud of myself for remembering to create a new branch when starting the work. Somewhere in the middle of the integration, I drift away, and started to explore a new idea - adding a commenting system to the site. Before I knew it I was already working on it. Unfortunately, not only that I didn't work on that feature in a dedicated branch, I was still on the branch I created for the org integration. </p>

<p> I wondered if there is a way to take the changes I made since the last commit, and pour them over into a new branch. Luckily, there is. Here's how, thank to <a href="http://stackoverflow.com/a/4746696/1424287">this answer in stack-overflow</a>: </p>

<blockquote>
<p> You can simply check out a new branch, and then commit: </p>

<div class="org-src-container">

<pre class="src src-bash">git checkout -b my_new_branch
git commit
</pre>
</div>

<p> Checking out the new branch will not discard your changes. </p>
</blockquote>

<p> Tried it and it worked. </p>