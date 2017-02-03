---
ID: 835
post_title: Electric Pair Mode In Emacs
author: Yaniv
post_date: 2016-10-02 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/10/electric-pair-mode-in-emacs.html
published: true
---
So far I've used <a href="https://textexpander.com">TextExpander</a> for text snippets and, well, text expansion. One of my main uses-cases is character pairings. For example, when I type <code>"</code> I almost always enclose it with another <code>"</code>.

But TextExpander is lacking in several ways:
<ol class="org-ol">
 	<li>Performance - it takes a friction of a second for the expansion to happen, but it's notable, and feels like a little hang.</li>
 	<li>If I delete one part of the pair, it won't remove the other.</li>
 	<li>It won't work to wrap text. If I typed something, and then want to wrap it with brackets, for example, I can't select the text and type the bracket character.</li>
</ol>
In addition to the above technical shortcomings, I don't plan to keep using TextExpander in the long run. The recent <a href="http://www.macworld.com/article/3052440/os-x/smile-updates-textexpander-and-switches-to-subscriptions.html">move into subscription based</a> pricing, isn't something I'm interested in. I mean, paying subscription to text snippets...?

Anyway, Emacs comes with an electric-pair-mode, which enables smart pairing. I turned it on, but out of the box it's configured to work mainly with programming major modes. I need it also in other text based modes, such as org, markdown and simple text. For example, in org I use <code>~</code> for inline code snippets, and <code>~</code> isn't paired by default. Same goes with <code>"</code>.

Luckily, defining more pairs is easy, through modifying the electric-pair-pairs variable.

Here's my configuration for this mode:
<div class="org-src-container">
<pre class="src src-emacs-lisp">(electric-pair-mode 1)
(<span style="color: #859900; font-weight: bold;">setq</span> electric-pair-pairs '(
                            (?\" . ?\")
                            (?\` . ?\`)
                            (?\( . ?\))
                            (?\{ . ?\})
                            ) )
</pre>
</div>
I'll add more pairs as I encounter them. Also, I'll need to learn how to add pairs for specific major modes.