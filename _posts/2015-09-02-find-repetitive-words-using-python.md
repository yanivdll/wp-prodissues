---
ID: 37
post_title: Find Repetitive Words Using Python
author: Yaniv
post_date: 2015-09-02 04:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/09/find-repetitive-words-using-python.html
published: true
---
Read this question from <a href="http://stackoverflow.com/questions/2823016/regular-expression-for-consecutive-duplicate-words">stackoverflow</a>:
<blockquote>Paris in the
the spring. Not that
that is related.

Why are you laughing? Are my my regular expressions THAT bad??</blockquote>
Have you notice the repetitions? chances are you haven't. The eye sees what the eye wants to see, and it'll take away any obstacle to let your brain comprehend. I too often catch myself writing the same word twice. The problem is that when I do, it's usually too late. The email was sent or post got published.

To make sure I find those repetitions in time, I wrote a simple Python script that removes superfluous spaces and highlight words' duplications, using <a href="http://criticmarkup.com/">CriticMarkup</a>. I run this script as soon as I finish writing. It works much better than my eyes in finding those elusive duplications.

Here's the script:
<div class="org-src-container">
<pre class="src src-python"><span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">! /usr/local/bin/python3</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">removeRepeatWords.py - find and remove repeat words</span>
<span style="color: #728a05;">import</span> logging
logging.basicConfig(filename=<span style="color: #259185;">'/Users/ygilad/Library/Logs/Python/myPythonLogs.log'</span>, level=logging.DEBUG, <span style="color: #728a05;">format</span>=<span style="color: #259185;">' %(asctime)s - %(levelname)s - %(message)s'</span>)

logging.disable(logging.CRITICAL)

<span style="color: #728a05;">import</span> pyperclip, re

<span style="color: #2075c7;">text</span> = <span style="color: #728a05;">str</span>(pyperclip.paste())

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">regex definitions for reapeated spaces</span>
<span style="color: #2075c7;">repeatSpacesRegex</span> = re.<span style="color: #728a05;">compile</span>(r<span style="color: #259185;">'\b(\s)+\1+\b'</span>) 

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">regex definitions for reapeated words</span>
<span style="color: #2075c7;">repeatWordsRegex</span> = re.<span style="color: #728a05;">compile</span>(r<span style="color: #259185;">'\b(\w+)\b[\s\r\n]*(\1[\s\r\n])+'</span>, re.IGNORECASE|re.DOTALL)

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">remove the extra spaces</span>
<span style="color: #2075c7;">repeatSpces</span> = repeatSpacesRegex.findall(text)

<span style="color: #728a05;">if</span> <span style="color: #728a05;">len</span>(repeatSpces) &gt; 1:
    <span style="color: #2075c7;">text</span> = repeatSpacesRegex.sub(r<span style="color: #259185;">'\1'</span>, text)
    <span style="color: #728a05;">print</span>(<span style="color: #728a05;">str</span>(<span style="color: #728a05;">len</span>(repeatSpces)) + <span style="color: #259185;">' repeat spaces were removed.'</span>)

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">remove repeated words</span>
<span style="color: #2075c7;">repeatWords</span> = repeatWordsRegex.findall(text)
logging.debug(repeatWords)

<span style="color: #728a05;">if</span> <span style="color: #728a05;">len</span>(repeatWords) &gt; 0:
    <span style="color: #2075c7;">text</span> = repeatWordsRegex.sub(r<span style="color: #259185;">'{~~\1 \2~&gt;\1 ~~}{&gt;&gt;repeating words&lt;&lt;}'</span>, text)

pyperclip.copy(text)
</pre>
</div>
To use it, copy the text you want to check into the clipboard. You then run the script and its output will be ready for you back in the clipboard. Just past it over the original text. Note that if the script finds repetitions it won't remove them, but mark them using CriticMarkup. If your editor supports CM, you can decide whether to accept or reject those changes.

Running this script on the quote from stackoverflow above produces the following output:
<pre class="example">Paris in {~~the  the ~&gt;the~~}{&gt;&gt;repeating words&lt;&lt;}spring. Not {~~that  that ~&gt;that~~}{&gt;&gt;repeating words&lt;&lt;}is related.

Why are you laughing? Are {~~my  my ~&gt;my~~}{&gt;&gt;repeating words&lt;&lt;}regular expressions THAT bad??
</pre>