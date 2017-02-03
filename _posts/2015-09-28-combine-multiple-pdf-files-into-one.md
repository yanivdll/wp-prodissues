---
ID: 52
post_title: Combine Multiple PDF Files Into One
author: Yaniv
post_date: 2015-09-28 04:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/09/combine-multiple-pdf-files-into-one.html
published: true
---
<p> I often have to send pdf documents via email. When I do, I prefer to send one document that merges all those pdfs. Form a recipient point-of-view, I find it better to receive one attachment, because it's easier to manage and to keep track of. The problem is that I've yet to find an easy way to stitch together multiple pdf files. Preview supose to let you do it, but I usually can't get it to work, and when I do, the process is painful<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>. </p>

<p> Recently, I came up with way to do just that, thanks to a python script I found in the <a href="https://automatetheboringstuff.com/chapter13/">"Automate the Boring Stuff with Python"</a> book. This script takes a folder of documents as an input, search for all the pdf files in that folder, and combine them into one pdf file. </p>

<p> However, I had to modify this script to fit my workflow better. My pdf files are all over the place, and I don't want to move them around just for the sake of merging them together. I therefore made a little tinkering to the original script, so it can take a list of files' paths as an input. Here's my modified version: </p>

<div class="org-src-container">

<pre class="src src-python"><span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">! /usr/local/bin/python3</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">combinePdfsFromFiles.py - </span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Script gets a list of pdf files' paths and combine them into one file</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">I use it together with keyboard maestro</span>

<span style="color: #728a05;">import</span> PyPDF2
<span style="color: #728a05;">import</span> os
<span style="color: #728a05;">import</span> sys
<span style="color: #728a05;">import</span> logging
<span style="color: #728a05;">import</span> pyperclip

<span style="color: #2075c7;">pdfFiles</span> = []

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Get PDF filenames from the clipboard</span>
<span style="color: #728a05;">for</span> filename <span style="color: #728a05;">in</span> pyperclip.paste().split(<span style="color: #259185;">','</span>):
    <span style="color: #728a05;">if</span> filename.endswith(<span style="color: #259185;">'.pdf'</span>) <span style="color: #728a05;">and</span> filename != <span style="color: #259185;">''</span>:
        pdfFiles.append(filename)

pdfFiles.sort(key=<span style="color: #728a05;">str</span>.lower)

<span style="color: #2075c7;">pdfWriter</span> = PyPDF2.PdfFileWriter()

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">Loop through all the PDF files.</span>
<span style="color: #728a05;">for</span> filename <span style="color: #728a05;">in</span> pdfFiles:
    <span style="color: #2075c7;">pdfFileObj</span> = <span style="color: #728a05;">open</span>(filename, <span style="color: #259185;">'rb'</span>)
    <span style="color: #2075c7;">pdfReader</span> = PyPDF2.PdfFileReader(pdfFileObj)
    <span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">Loop through all the pages (except the first) and add them.</span>
    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">If first page should be discarded, change firt param of range to 1</span>
    <span style="color: #728a05;">for</span> pageNum <span style="color: #728a05;">in</span> <span style="color: #728a05;">range</span>(0, pdfReader.numPages):
        <span style="color: #2075c7;">pageObj</span> = pdfReader.getPage(pageNum)
        pdfWriter.addPage(pageObj)

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">TODO: add an argument that determine whether cover should be included.</span>

<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">Save the resulting PDF to a file.</span>
<span style="color: #2075c7;">pdfOutput</span> = <span style="color: #728a05;">open</span>(<span style="color: #259185;">'/Users/ygilad/Desktop/allminutes.pdf'</span>, <span style="color: #259185;">'wb'</span>)
pdfWriter.write(pdfOutput)
pdfOutput.close()
</pre>
</div>

<p> I created a simple keyboard maestro macro that goes along with this script and serves as an interface with it: </p>

<p> <img src="http://media.prodissues.com/images/2015/09/combine_pdfs_macro.jpg" alt="combine_pdfs_macro.jpg" /> Now, All I have to do is select in Finder the files I want to stitch: </p>

<p> <img src="http://media.prodissues.com/images/2015/09/stich_pdf_-_select_files.png" alt="stich_pdf_-_select_files.png" /> I can then execute the KM macro, which pass the list of files to the python script for processing. </p>

<p> I know this process might sound tedious, and even more painful than using Preview for that job. But that's the beauty of automation - you pay once use freely ever after. </p>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> To get it done with Preview, you'll have to open each of the pdfs, expose the thumbnails' sidebar, and start dragging and dropping the pages you would like to combine. If you're still interested, <a href="https://support.apple.com/en-us/HT202945">here's</a> Apple's support guide.  ↩ </p></div></div>


</div>
</div>