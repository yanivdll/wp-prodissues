---
ID: 893
post_title: 'use-package&#8217;s :config vs. :init'
author: Yaniv
post_date: 2016-10-25 10:36:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/10/use-packages-config-vs-init.html
published: true
---
I read <a href="https://www.reddit.com/r/emacs/comments/58v6id/what_is_your_favorite_dark_theme_that_works_well/?ref=share&amp;ref_source=link">this</a> Reddit thread about favorite themes, and got intrigued by the <a href="https://github.com/nashamri/spacemacs-theme">spacemacs</a> theme<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>.

I added that theme to my <code>init</code> file, and tried making it the default theme. I use <code>use-package</code>, and configured the theme as follows:
<div class="org-src-container">
<pre class="src src-emacs-lisp">(<span style="color: #3a81c3; font-weight: bold;">use-package</span> <span style="color: #4e3163;">spacemacs-theme</span>
<span style="color: #3a81c3;">:ensure</span> t
<span style="color: #3a81c3;">:config</span>
(load-theme 'spacemacs-light t)
)
</pre>
</div>
When re-evaluating my <code>init</code> file, the theme didn't load. I tried to run only the <code>(load-theme 'spacemacs-light t)</code> line, and the theme loaded. I changed the <code>:config</code> to <code>:init</code> in the package configuration, and it loaded when I re-loaded emacs.

What, then, is the difference between <code>:init</code> and <code>:config</code> in <code>use-package</code>?

The answer to that question, which I found it in this <a href="http://emacs.stackexchange.com/a/10403">stack-overflow answer</a>, is that in <code>use-package</code>, whatever defined inside the <code>:init</code> keyword, will load whenever emacs is loading. What's in the <code>:config</code>, though, will be executed only when the package is actually loaded (i.e lazy loading)<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>.

Here's how my configuration for that theme looks like now:
<div class="org-src-container">
<pre class="src src-emacs-lisp">(<span style="color: #3a81c3; font-weight: bold;">use-package</span> <span style="color: #4e3163;">spacemacs-theme</span>
<span style="color: #3a81c3;">:ensure</span> t
<span style="color: #3a81c3;">:init</span>
(load-theme 'spacemacs-light t)
)
</pre>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes:</h2>
<div id="text-footnotes">
<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup>
<div class="footpara">
<p class="footpara">I tried spacemacs before, and liked its look and feel, but didn't know I can take it back with me to gnu emacs</p>

</div>
</div>
<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup>
<div class="footpara">
<p class="footpara">Needless to say that, going back to the <code>use-package</code> documentation, the difference between <code>:init</code> and <code>:config</code> is clearly described…</p>

</div>
</div>
</div>
</div>