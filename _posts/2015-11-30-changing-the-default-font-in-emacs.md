---
ID: 65
post_title: Changing the default font in Emacs
author: Yaniv
post_date: 2015-11-30 05:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/11/changing-the-default-font-in-emacs.html
published: true
---
<p> Josh Stella wrote a <a href="https://blog.fugue.co/2015-11-11-guide-to-emacs.html">delightful post</a> about how he uses Emacs, not necessarily for development work. I found quite a few configuration tips, and already implemented few of them. One of those tweaks is using the Input font family. Visiting <a href="http://input.fontbureau.com/">fontbureau</a> made me want this font too! </p>

<p> I thought it will be as simple as <code>copy-paste</code> (I'm still not used to the appropriate <code>kill-yank</code> terminology) Josh's configuration. It wasn't - after reloading my init, the font didn't pick up. </p>

<p> Few experimentations later, though, and it <i>did</i> work. First, I had to download and install the font in my mac, dahhh... Then, I had to modify the name of the font (Josh used <code>InputSerif</code>; I had to change it to <code>Input</code>). Here's my configuration: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp"><span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">set up fonts for different OSes. OSX toggles to full screen.</span>
(setq myfont <span style="color: #259185;">"Input"</span>)
(<span style="color: #728a05;">cond</span>
((string-equal system-name <span style="color: #259185;">"ygilad.local"</span>)
 (set-face-attribute 'default nil <span style="color: #728a05;">:font</span> myfont <span style="color: #728a05;">:height</span> 144)
 (toggle-frame-fullscreen)))
</pre>
</div>

<p> Indeed, it looks beautiful. Here's a screen grab of this post in Input: <img src="http://media.prodissues.com/images/2015/11/emacs_with_input_font.png" alt="emacs_with_input_font.png" /> </p>

<p> There's still one problem - this modification to my config broke the org-reader plugin, and I can't export my org files to Pelican. Sadly, I'll have to resort to the default font (Menlo), until I figure out a fix. </p>