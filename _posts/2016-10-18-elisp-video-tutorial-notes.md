---
ID: 867
post_title: 'Elisp Video Tutorial &#8211; Notes'
author: Yaniv
post_date: 2016-10-18 22:12:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/10/elisp-video-tutorial-notes.html
published: true
---
<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline1">Part 1 - Intro</a></li>
<li><a href="#orgheadline2">Part 2 - Create A Simple Function And A Test Of That Function</a></li>
<li><a href="#orgheadline3">Part 3 - Looping And Local Variables</a></li>
<li><a href="#orgheadline4">Part 4 - Interactive Functions</a></li>
</ul>
</div>
</div>
<p> I've just finished watching <a href="http://www.pygopar.com/">Daniel Gopar's</a> elisp <a href="https://www.youtube.com/watch?list=PL3kg5TcOuFlpyqiZspzlkk6Ro66nQdESz&amp;params=OAFIAVgB&amp;v=CH0RUrO_oww&amp;mode=NORMAL&amp;app=desktop">video tutorial</a>. So far there are 4 parts to the tutorial, and based on <a href="https://www.reddit.com/r/emacs/comments/5542rm/made_some_elisp_videos/?">this thread</a> on Reddit, there are more to come. </p>

<p> After watching the guide I don't feel more proficient in elisp, yet less timid running <code>evals</code> and more courageous tinkering with my <a href="https://github.com/yanivdll/.emacs.d/blob/master/config.org">config</a> file. </p>

<p> Following is a short summary of the code exercises and shortcuts I logged while watching. </p>



<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">Part 1 - Intro</h2>
<div class="outline-text-2" id="text-orgheadline1">
<p> <a href="https://www.youtube.com/watch?list=PL3kg5TcOuFlpyqiZspzlkk6Ro66nQdESz&amp;params=OAFIAVgB&amp;v=CH0RUrO_oww&amp;mode=NORMAL&amp;app=desktop">Link to episode 1</a> </p>

<p> REPL - read-eval-print-loop </p>

<p> Define functions: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(<span style="color: #859900; font-weight: bold;">defun</span> <span style="color: #268bd2;">add-num</span> (a b) (+ a b))
</pre>
</div>


<p> Define a test: </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(<span style="color: #859900; font-weight: bold;">require</span> '<span style="color: #268bd2; font-weight: bold;">ert</span>)
(<span style="color: #859900; font-weight: bold;">ert-deftest</span> <span style="color: #268bd2;">add-num-pos</span> ()
         (should
         (equal (add-num 10 10) 20)))
</pre>
</div>

<p> To run the test that I've just created: <code>M-x ert-run-tests-interactively</code> </p>

<p> Choose the test I would like to run (in this case "pos-add-num") </p>
</div>
</div>

<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Part 2 - Create A Simple Function And A Test Of That Function</h2>
<div class="outline-text-2" id="text-orgheadline2">
<p> <a href="https://www.youtube.com/watch?list=PL3kg5TcOuFlpyqiZspzlkk6Ro66nQdESz&amp;params=OAFIAVgB&amp;v=CH0RUrO_oww&amp;mode=NORMAL&amp;app=desktop">Link to episode 2</a> </p>

<p> <code>setq</code>  to set variables and lists <code>(setq my-list '(1 2 3))</code> </p>

<p> <code>add-to-list</code> to add element <code>(add-to-list 'my-list 4)</code> </p>

<p> Another way to add to list, but this time to a copy of the list: <code>(cons 5 my-list)</code> - this will return (5 1 2 3 4) But when inquiring my-list, we will get (1 2 3 4) </p>

<p> <code>car</code> returns the first element in every list <code>(car my-list)</code> -&gt; 1 </p>

<p> <code>cdr</code> returns everything from a list, after the first element <code>(crd my-list)</code> -&gt; (2 3 4) </p>

<p> <code>nth</code> return a certain element in the list <code>(nth 4 my-list)</code> -&gt; 3 </p>

<p> <code>member</code> check for a certain value in a list, and return the elements in that list from that value on <code>(member 3 my-list)</code> -&gt; (3 4) <code>(member 7 my-list)</code> -&gt; nil </p>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">Part 3 - Looping And Local Variables</h2>
<div class="outline-text-2" id="text-orgheadline3">
<p> <a href="https://www.youtube.com/watch?v=VqCSbDqHziM&amp;list=PL3kg5TcOuFlpyqiZspzlkk6Ro66nQdESz&amp;index=3">Link to episode 3</a> </p>

<p> Use the <b>scratch</b> buffer, so I can write in multiple lines </p>

<p> <code>C-x C-e</code> to evaluate code. Point needs to be at the end of the code in order to get evaluated. </p>

<p> Looping through variables: </p>

<p> <code>let</code> to create a local variable </p>

<p> <code>when</code> and <code>if</code> - what they suppose to do... </p>

<p> If there is more than one statement in the <code>if</code> statement, need to use to wrap those lines with <code>progn</code>. There is no such limitation in the <code>else</code> statement. </p>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Part 4 - Interactive Functions</h2>
<div class="outline-text-2" id="text-orgheadline4">
<p> <a href="https://www.youtube.com/watch?v=KwBRpS9Bs4U&amp;index=4&amp;list=PL3kg5TcOuFlpyqiZspzlkk6Ro66nQdESz">Link to episode 4</a> </p>

<p> Created a function to count words, plus the test for it. </p>

<div class="org-src-container">

<pre class="src src-emacs-lisp">(<span style="color: #859900; font-weight: bold;">defun</span> <span style="color: #268bd2;">cheap-count-words</span>()
  (<span style="color: #859900; font-weight: bold;">interactive</span>)
  (<span style="color: #859900; font-weight: bold;">let</span> ((words 0))
    (<span style="color: #859900; font-weight: bold;">save-excursion</span>
      (goto-char (point-min))
    (<span style="color: #859900; font-weight: bold;">while</span> (forward-word)
      (<span style="color: #859900; font-weight: bold;">setq</span> words (1+ words)) ))
    (message (format <span style="color: #2aa198;">"Words in Buffer: %s"</span> words))words))



<span style="color: #93a1a1;">;; </span><span style="color: #93a1a1;">Tests</span>
(<span style="color: #859900; font-weight: bold;">require</span> '<span style="color: #268bd2; font-weight: bold;">ert</span>)

(<span style="color: #859900; font-weight: bold;">ert-deftest</span> <span style="color: #268bd2;">count-words-test</span> ()
  (get-buffer-create <span style="color: #2aa198;">"*test*"</span>)
  (<span style="color: #859900; font-weight: bold;">with-current-buffer</span> <span style="color: #2aa198;">"*test*"</span>
    (erase-buffer)
    (insert <span style="color: #2aa198;">"Hello world"</span>)
    (should (=(cheap-count-words) 2)))
  (kill-buffer <span style="color: #2aa198;">"*test*"</span>))
</pre>
</div>
</div>
</div>