---
ID: 40
post_title: A Recipe To Work-In-Progress Documents
author: Yaniv
post_date: 2015-09-12 01:58:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/09/a-recipe-to-work-in-progress-documents.html
published: true
---
<p> I recently <a href="http://prodissues.com/2015/06/why-i-decided-to-move-away-from-evernote.html">stopped using Evernote</a> and started to manage my notes exclusively in Dropbox. My configuration revolves around a <code>Notes</code> folder. I use <a href="http://brettterpstra.com/projects/nvalt/">nvAlt</a> to browse through the notes in that folder and add new ones. If I want to do more than just a scribble, I use the <code>command-e</code> key binding in nvAlt to open the document in <a href="http://multimarkdown.com/">MultiMarkdown Composer</a>. </p>

<p> Storing all my notes in one folder has a major limitation, though. As notes accumulate, looking for a specific note becomes impossible. This is actually one of the main reasons to my departure from Evernote. To avoid this problem, I set <a href="http://www.noodlesoft.com/hazel.php">Hazel</a> to monitor my <code>Notes</code> folder and move everything that wasn't modified in the last 30 days to a designated archive folder. Archived notes don't show in nvAlt, yet easily accessible through Finder. </p>

<p> Now that I have a home to my notes, I would like to add some logic to streamline my writing workflow. To begin with, I would like to aggregate documents I'm working on, and are in other folders, to my main notes' repository. </p>

<p> For example, I'm currently writing a readme file for one of my git repositories. This repo lives within its own folder, where the readme file resides as well. Keeping this file out of my <code>Notes</code> folder means that it's a hassle to go back and open it when needed. It also means that I can't work on it when I'm on my iPhone <sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>. </p>

<p> So, what I needed was a way to mark a document, and have it magically show up in my <code>Notes</code> folder, hence available in nvAlt. Following is the recipe I came up with to address this need. </p>

<p> Let's start with the ingredients: </p>

<ul class="org-ul">
<li>Finder</li>
<li>Hazel</li>
<li>Python</li>
</ul>

<p> And here's how to mix these components together: </p>

<ol class="org-ol">
<li>Open Finder and tag <code>wip</code> the document I want to work on and make available in nvAlt.<img src="http://media.prodissues.com/images/2015/09/tag_wip.png" alt="tag_wip.png" /></li>
<li>Configure a Hazel rule that monitors my home folder, looking for files containing the <code>wip</code> tag <sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>. <img src="http://media.prodissues.com/images/2015/09/hazel_3.png" alt="hazel_3.png" /></li>
<li>Create a python script that takes a file's path as an input and place a symbolic link to it in my <code>Notes</code> folder.</li>
</ol>

<div class="org-src-container">

<pre class="src src-python"><span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">! /usr/local/bin/python3</span>

<span style="color: #728a05;">import</span> os, sys, shutil
<span style="color: #728a05;">import</span> logging

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Configuring logging to be written into a file in the system's log folder</span>
logging.disable(logging.CRITICAL)
logging.basicConfig(filename=<span style="color: #259185;">'/Users/ygilad/Library/Logs/Python/myPythonLogs.log'</span>, level=logging.DEBUG, <span style="color: #728a05;">format</span>=<span style="color: #259185;">' %(asctime)s - %(levelname)s - %(message)s'</span>)

<span style="color: #728a05;">def</span> <span style="color: #2075c7;">moveFileToNote</span>(filePath):
    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Set the link name to the original file.</span>
    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Path to the original file is included for two reasons</span>
    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">1) Avoid naming conflicts and</span>
    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">2) remind myself where this file came from</span>
    <span style="color: #2075c7;">fileName</span> = <span style="color: #259185;">'link'</span> + filePath.replace(<span style="color: #259185;">'/'</span>,<span style="color: #259185;">'_'</span>).lower()
    logging.debug(<span style="color: #259185;">'Filename: '</span> + fileName)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Make sure that the input is a file and not a folder</span>
    <span style="color: #728a05;">if</span> <span style="color: #728a05;">len</span>(fileName) &gt; 0:
        <span style="color: #728a05;">try</span>:
            <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Add the link to my central note repository</span>
            os.symlink(filePath , <span style="color: #259185;">'/Users/ygilad/Dropbox/Notes/link-'</span>+ fileName)
            logging.debug(<span style="color: #259185;">'Created a file link'</span>)
        <span style="color: #728a05;">except</span> FileExistsError:
            logging.debug(<span style="color: #259185;">'File already exists at the target folder'</span>)
    <span style="color: #728a05;">else</span>:
        logging.debug(<span style="color: #259185;">'Input is not a file'</span>)

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Accept the path coming from Hazel</span>
<span style="color: #2075c7;">hazelLocalFile</span> = sys.argv[1]
logging.debug(hazelLocalFile)

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">The body of the script</span>
moveFileToNote(hazelLocalFile)
</pre>
</div>

<p> There is one drawback I wasn't able to solve - nvAlt doesn't show the content of the link. All it <i>does</i> show is the path of the original document.<img src="http://media.prodissues.com/images/2015/09/nvAlt_and_linked_files.png" alt="nvAlt_and_linked_files.png" /> </p>

<p> While I can't edit the file directly in nvAlt, I can still do it in MultiMarkdown Composer or <a href="http://omz-software.com/editorial/">Editorial</a> on my iPhone. </p>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> I keep git repositories in a local folder out of Dropbox reach, because I heard that <a href="http://scripting.com/2014/01/24/githubAndDropboxDoNotPlayWellTogether.html">you shouldn't mix the two together</a>. </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> I found that creating a rule that monitors a folder and its sub-folders is a bit tricky, but eventually learned how to do it thanks to <a href="http://www.noodlesoft.com/forums/viewtopic.php?f=4&amp;t=470">this post</a>. </p></div></div>


</div>
</div>