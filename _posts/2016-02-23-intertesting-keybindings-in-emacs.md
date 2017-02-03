---
ID: 374
post_title: Just A Couple Of Emacs Keybindings
author: Yaniv
post_date: 2016-02-23 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/02/intertesting-keybindings-in-emacs.html
published: true
---
Every now and then I'll type something in Emacs with a certain goal, just to find that I get something completely different from what I've intended.

When in org file, I tried to convert a list item to a sub-header. The keybinding to make this conversion is <code>C-c *</code>. But when I (thought I) typed it, instead of getting a sub-header, a new buffer opened at the bottom of the frame - a calculator:
<div id="outline-container-orgheadline1" class="outline-2">
<div id="text-orgheadline1" class="outline-text-2">
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/emacs-calc-mode.png" alt="emacs-calc-mode.png" />

<span class="figure-number">Figure 1:</span> Calc mode

</div>
</div>
</div>
<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">view-lossage</h2>
<div id="text-orgheadline2" class="outline-text-2">

I had no idea how did <i>that</i> happen, and luckily recalled a <a href="https://www.reddit.com/r/emacs/comments/3w46xu/how_did_i_get_here_command/cxt6w6r">tip I got</a>, on how to move back in time using the <code>view-lossage</code> command, which display last 300 input keystrokes. Doing so, I found that instead of <code>C-c *</code>, I typed <code>C-x *</code>.

So now I know (and hopefully remember) that:
<ol class="org-ol">
	<li>There's a calculator<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> in Emacs, bound to <code>C-x *</code></li>
	<li><code>C-h l</code> is a useful way to track back clumsy keystrokes</li>
</ol>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes:</h2>
<div id="text-footnotes">
<div class="footdef">

<sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup>
<div class="footpara">
<p class="footpara">Not that I had any doubts there is, just didn't think to look for it just yet. There are so many other "to-learn" things on my list...</p>

</div>
</div>
</div>
</div>