---
ID: 57
post_title: Swapping Buffers in Emacs
author: Yaniv
post_date: 2015-11-08 03:39:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/11/swapping-buffers-in-emacs.html
published: true
---
<p> It took me awhile to find a way to swap the position of two buffers in emacs. Yes, there is a description in <a href="http://www.emacswiki.org/emacs/SwitchingBuffers">emacs wiki</a>, and the code bellow is actually taken from there, but it's not that easy to find through the tons of irrelevant information arround it. </p>

<p> So if you're looking to simply get the right buffer show on the right, and vice versa, here's what you should add to your init file: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(<span style="color: #728a05;">defun</span> <span style="color: #2075c7;">transpose-buffers</span> (arg)
      <span style="color: #259185; font-style: italic;">"Transpose the buffers shown in two windows."</span>
      (interactive <span style="color: #259185;">"p"</span>)
      (<span style="color: #728a05;">let</span> ((selector (<span style="color: #728a05;">if</span> (&gt;= arg 0) 'next-window 'previous-window)))

          (<span style="color: #728a05;">let</span> ((this-win (window-buffer))
                (next-win (window-buffer (funcall selector))))
            (set-window-buffer (selected-window) next-win)
            (set-window-buffer (funcall selector) this-win)
            (select-window (funcall selector)))
          (setq arg (<span style="color: #728a05;">if</span> (plusp arg) (1- arg) (1+ arg))))))
</pre>
</div>


<p> I have no idea what this code means<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>, but it does what I expected it to do. I also didn't create a keybinding for it, but you can if you would like to. Here's how to bind it to, say, <code>f8</code>: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(global-set-key [f8] 'transpose-buffers)
</pre>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> Learning elisp is on my todo list&#x2026; </p></div></div>


</div>
</div>