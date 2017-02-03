---
ID: 77
post_title: 'Get The Current File&#8217;s Path in Emacs'
author: Yaniv
post_date: 2016-01-04 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/01/get-the-current-files-path-in-emacs.html
published: true
---
Here's a small function I borrowed from <a href="http://stackoverflow.com/questions/3669511/the-function-to-show-current-files-full-path-in-mini-buffer">this question</a> on stack-overflow. It returns the full path of the file I currently edit in the buffer:
<div class="org-src-container">
<pre class="src src-emacs-lisp">(<span style="color: #728a05;">defun</span> <span style="color: #2075c7;">show-file-name</span> ()
  <span style="color: #259185; font-style: italic;">"Show the full path file name in the minibuffer."</span>
  (interactive)
  (message (buffer-file-name))
  (kill-new (file-truename buffer-file-name))
)
(global-set-key <span style="color: #259185;">"\C-cz"</span> 'show-file-name)
</pre>
</div>
You'll note that this function is bind to <code>C-c z</code>. So when typing it, you should see the path showing in the minibuffer. As a bonus, it stores the path in the kill ring, so <code>C-y</code> (<code>CMD-v</code> works as well on my mac) will paste the value.