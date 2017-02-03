---
ID: 67
post_title: Bunch of Emacs Tweaks
author: Yaniv
post_date: 2015-12-04 05:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/12/bunch-of-emacs-tweaks.html
published: true
---
<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline1">Comment\Uncomment a Line</a></li>
<li><a href="#orgheadline2">Quick reload of init.el file</a></li>
<li><a href="#orgheadline3">New line bellow</a></li>
<li><a href="#orgheadline4">Quick Open a specific file</a></li>
<li><a href="#orgheadline5">Change cases</a></li>
</ul>
</div>
</div>


<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">Comment\Uncomment a Line</h2>
<div class="outline-text-2" id="text-orgheadline1">
<p> Few useful commands for commenting\uncommenting lines in emacs. Taken from the <a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Comment-Commands.html">Emacs tutorial</a>. Sure, I can go back to the manual, but I want to ducument and keep them here, for quicker referrence. </p>

<blockquote>
<p> <code>M-;</code> Insert or realign comment on current line; if the region is active, comment or uncomment the region instead (comment-dwim). </p>

<p> <code>C-u M-;</code> Kill comment on current line (comment-kill). </p>

<p> <code>C-x ;</code> Set comment column (comment-set-column). </p>

<p> <code>C-M-j</code> <code>M-j</code> Like RET followed by inserting and aligning a comment (comment-indent-new-line). See Multi-Line Comments. </p>

<p> <code>M-x comment-region</code> </p>
</blockquote>

<p> Mastering this command takes me one step further into Emacs, as it used to be one of those funcionalities that keeped drawing me back to Sublime Text. </p>
</div>
</div>
<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Quick reload of init.el file</h2>
<div class="outline-text-2" id="text-orgheadline2">
<p> I'm constantly customizing my emacs. I have an <code>init.el</code> file, but most of the configuration in a more literal way, in an org <a href="https://github.com/yanivdll/.emacs.d/blob/master/config.org">config file</a>. </p>

<p> When I make changes to Emacs settings, I need to reload the init file activate the changes. So far, I typed <code>C-x C-f</code> to find the init file and then <code>M-x [RET] eval-buffer</code> to reload it. Repeating this flow hundreds of times became annoying. </p>

<p> A quick inquery <a href="http://prodissues.com/2015/11/leap-into-the-past-irc.html">in IRC</a>, and now I know that I can call <code>load-file</code> and give it the name of the file I would like to load. Having a function to load a file, means that I can wrap it with my own function, and reload my init file with a customized keybind. </p>

<p> And with the help of <a href="http://stackoverflow.com/a/12558095/1424287">this answer</a> at stack-overflow, I came up with the following shortcut to reload my Emacs configuration: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(global-set-key (kbd <span style="color: #259185;">"&lt;f6&gt;"</span>) (<span style="color: #728a05;">lambda</span>() (interactive)(load-file <span style="color: #259185;">"~/.emacs.d/init.el"</span>)))
</pre>
</div>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">New line bellow</h2>
<div class="outline-text-2" id="text-orgheadline3">
<p> I wondered if there's a command to creat a new line bellow the line my point is on. Here's what I found in <a href="http://superuser.com/a/331661/525565">superuser</a>: </p>

<p> <code>C-e C-m</code> - go to the end of the line, create a new line and move the point to that line. </p>

<p> or </p>

<p> <code>C-e C-j</code> - same as the command above, only that the point will indent if neccessery. </p>

<p> There is also a keybind for creating a new line above the current line, and move the point to that line - <code>C-a C-o</code>. </p>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Quick Open a specific file</h2>
<div class="outline-text-2" id="text-orgheadline4">
<p> Now days I start most of my writing in my <a href="http://prodissues.com/posts_drafts/">draft file</a>. I need a quick way to access this file, whether I'm in Emacs or any other application. I know Emacs has the concept of registers, which are special memory slots, that can be accessed with a command. Those registers can store any type of data, such as strings, integers, files and paths. </p>

<p> It's time to learn how to work with them. When thinking about it, there are other files that I would have liked to access quicker, such as the <a href="https://github.com/yanivdll/.emacs.d/blob/master/init.el">init.el</a> or <a href="https://github.com/yanivdll/.emacs.d/blob/master/config.org">config.org</a>. </p>

<p> Google's first search result was EmacsWiki. Again, it proved to be a great source of information, had I wanted to confuse myself. So I passed. The second result was from <a href="https://www.gnu.org/software/emacs/manual/html_node/emacs/File-Registers.html#File-Registers">Emacs tutorial</a>, which again proved to be clear, concise and informative. </p>

<p> Here are the commands for storing a filename in and loading it from  a register: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(set-register r '(file . name))
</pre>
</div>


<p> For example, </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(set-register ?r '(file . <span style="color: #259185;">"~/Dropbox/Notes/posts/pages/posts_drafts.org"</span>))
</pre>
</div>


<p> To load this file, I should type <code>C-x r j r</code> </p>

<p> In the code examples above, <code>r</code> is the name of the register. It can be replaced with any character. </p>

<p> And to see what's stored in a specific register: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">M-x view-register RET r
</pre>
</div>

<p> Again, <code>r</code> is the register I'm querying. </p>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-2">
<h2 id="orgheadline5">Change cases</h2>
<div class="outline-text-2" id="text-orgheadline5">
<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Keybinding</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>
<tbody>
<tr>
<td class="org-left"><code>M-l</code></td>
<td class="org-left">Convert following word to lower case (downcase-word).</td>
</tr>

<tr>
<td class="org-left"><code>M-u</code></td>
<td class="org-left">Convert following word to upper case (upcase-word).</td>
</tr>

<tr>
<td class="org-left"><code>M-c</code></td>
<td class="org-left">Capitalize the following word (capitalize-word).</td>
</tr>

<tr>
<td class="org-left"><code>C-x C-l</code></td>
<td class="org-left">Convert region to lower case (downcase-region).</td>
</tr>

<tr>
<td class="org-left"><code>C-x C-u</code></td>
<td class="org-left">Convert region to upper case (upcase-region).</td>
</tr>
</tbody>
</table>
</div>
</div>