---
ID: 90
post_title: Uploading Images To Amazon S3
author: Yaniv
post_date: 2016-01-19 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/01/uploading-images-to-amazon-s3.html
published: true
---
<p> Here's a cool little  workflow that I use to automate the usage of images in my posts<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>. </p>

<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">The flow</h2>
<div class="outline-text-2" id="text-orgheadline1">
<ul class="org-ul">
<li>Move the image I would like to use to my <code>black-hole</code> folder</li>
<li>When a new file is added to the folder, or existing file is modified, a <a href="https://www.noodlesoft.com/hazel.php">Hazel</a> is triggered</li>
<li>This Hazel rule fires up a python script</li>
<li>The python script:

<ul class="org-ul">
<li>Pushes updates to my Amazon S3</li>
<li>Returns a link to the uploaded file</li>
<li>Place the link in the clipboard</li>
<li>Add a log entry that includes the timestemp and the link to that file</li>
</ul></li>
</ul>

<!--more-->
</div>
</div>

<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">The Porcelain</h2>
<div class="outline-text-2" id="text-orgheadline2">
<p> Here's how the flow in action: </p>

<iframe width="420" height="315" src="https://www.youtube.com/embed/IKt3MdXRfXo" frameborder="0" allowfullscreen></iframe>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">The Plumbing</h2>
<div class="outline-text-2" id="text-orgheadline3">
<p> And here are the ingredients in more detail: </p>
</div>

<div id="outline-container-orgheadline4" class="outline-3">
<h3 id="orgheadline4">The Hazel rule</h3>
<div class="outline-text-3" id="text-orgheadline4">
<div class="figure"> <p><img src="http://media.prodissues.com/images/2016/01/upload_to_s3.png" alt="upload_to_s3.png" /> </p> <p><span class="figure-number">Figure 1:</span> Note that I rename the filename, such that spaces replaced by <code>_</code>. Otherwise the upload to S3 doesn't work</p> </div>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-3">
<h3 id="orgheadline5">The python script</h3>
<div class="outline-text-3" id="text-orgheadline5">
<div class="org-src-container">

<pre class="src src-python"><span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">+BLOG: yanivgilad</span>
<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">+POSTID: 57</span>
<span style="color: #81908f; font-style: italic;">#</span><span style="color: #81908f; font-style: italic;">+DATE: [2016-01-19 Tue 20:42]</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Source: https://github.com/yanivdll/python-scripts/blob/master/s3_upload.py</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">This script upload files (at the moment images and slideshows) to S3. </span>
<span style="color: #81908f; font-style: italic;">#</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Credits:</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">This script is inspired by macdrifter script, which can be found at:</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">http://www.macdrifter.com/2012/05/upload-to-amazon-s3-from-dropbox-using-hazel.html</span>

<span style="color: #728a05;">import</span> boto
<span style="color: #728a05;">from</span> boto.s3.connection <span style="color: #728a05;">import</span> S3Connection
<span style="color: #728a05;">import</span> pyperclip
<span style="color: #728a05;">import</span> os
<span style="color: #728a05;">import</span> sys
<span style="color: #728a05;">from</span> datetime <span style="color: #728a05;">import</span> date, datetime

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">This is how Hazel passes in the file path</span>
<span style="color: #2075c7;">hazelFilePath</span> = sys.argv[1]
<span style="color: #2075c7;">contentType</span> = sys.argv[2]

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">This is where I store my log file for these links. It's a Dropbox file in my NVAlt notes folder</span>
<span style="color: #2075c7;">logFilePath</span> = <span style="color: #259185;">"~/Dropbox/Notes/Linkin_Logs.txt"</span>
<span style="color: #2075c7;">nowTime</span> = <span style="color: #728a05;">str</span>(datetime.now())


<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">This is the method that does all of the uploading and writing to the log file.</span>
<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">The method is generic enough to work with any S3 bucket that is passed.</span>
<span style="color: #728a05;">def</span> <span style="color: #2075c7;">uploadToS3</span>(localFilePath, localFileType, S3Bucket):
    <span style="color: #2075c7;">fileName</span> = os.path.basename(localFilePath)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Determine the current month and year to create the upload path</span>
    <span style="color: #2075c7;">today</span> = date.today()
    <span style="color: #2075c7;">datePath</span> = today.strftime(<span style="color: #259185;">"/%Y/%m/"</span>)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Connect to S3</span>
    <span style="color: #2075c7;">s3</span> = boto.connect_s3()
    <span style="color: #2075c7;">bucket</span> = s3.get_bucket(S3Bucket)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Set the folder name based on the content type image\slideshow</span>
    <span style="color: #728a05;">if</span> localFileType == <span style="color: #259185;">'slideshow'</span>:
        <span style="color: #2075c7;">key</span> = bucket.new_key(<span style="color: #259185;">'slideshows/'</span> + fileName)
    <span style="color: #728a05;">else</span>:
        <span style="color: #2075c7;">key</span> = bucket.new_key(<span style="color: #259185;">'images'</span> + datePath + fileName)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Upload file to S3</span>
    key.set_contents_from_filename(localFilePath)
    key.set_acl(<span style="color: #259185;">'public-read'</span>)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Log the url of the hosted file</span>
    <span style="color: #2075c7;">logfile</span> = <span style="color: #728a05;">open</span>(logFilePath, <span style="color: #259185;">"a"</span>)

    <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">Create the URL for the image</span>
    <span style="color: #2075c7;">imageLink</span> = <span style="color: #259185;">'http://'</span> + S3Bucket + <span style="color: #259185;">'/'</span> + key.name

    <span style="color: #728a05;">try</span>:
        <span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">encode the file name and append the URL to the log file</span>
        logfile.write(nowTime+<span style="color: #259185;">'  '</span>+imageLink+<span style="color: #259185;">'\n'</span>)
        pyperclip.copy(imageLink)
    <span style="color: #728a05;">finally</span>:
        logfile.close()

<span style="color: #81908f; font-style: italic;"># </span><span style="color: #81908f; font-style: italic;">The body of the script.</span>
uploadToS3(hazelFilePath, contentType,<span style="color: #259185;">'media.prodissues.com'</span>)
</pre>
</div>
</div>
</div>

<div id="outline-container-orgheadline6" class="outline-3">
<h3 id="orgheadline6">Few remarks about boto</h3>
<div class="outline-text-3" id="text-orgheadline6">
<ul class="org-ul">
<li>If you're new to boto, a python interface to Amazon AWS, read through <a href="http://boto.readthedocs.org/en/latest/boto_config_tut.html">this tutorial</a>.</li>
<li>Boto's credentials file lives in <code>~/.boto</code> file. However, I found that when not running the <code>s3_upload.py</code> from a python environment such as IDLE, but from a terminal, the credential file that is being used is the <code>~/.aws/credentials</code> file. So I just made sure that my AWS credentials exist in both files.</li>

<li>Since my bucket has dots in it (<code>media.prodissues.com</code>) I had to define the S3 bucket format<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup> explicitly:</li>
</ul>

<div class="org-src-container">

<pre class="src src-sh">[default]
aws_access_key_id = [my_aws_access_key]
aws_secret_access_key = [my_aws_secret_access_key]

[s3]
calling_format = boto.s3.connection.OrdinaryCallingFormat
</pre>
</div>
</div>
</div>

<div id="outline-container-orgheadline7" class="outline-3">
<h3 id="orgheadline7">The log file</h3>
<div class="outline-text-3" id="text-orgheadline7">
<div class="figure"> <p><img src="http://media.prodissues.com/images/2016/01/Screen_Shot_2016-01-19_at_15.18.16.png" alt="Screen_Shot_2016-01-19_at_15.18.16.png" /> </p> </div>
</div>
</div>
</div>


<div id="outline-container-orgheadline8" class="outline-2">
<h2 id="orgheadline8">Summary</h2>
<div class="outline-text-2" id="text-orgheadline8">
<p> Setting this workflow might look more intimidating than it really is. But even if it is, the gratifing feeling of throwing a file into a folder and getting a live link in exchange is totally worth it. </p>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> Heavily inspiered by Macdrifter's "<a href="http://www.macdrifter.com/2012/05/upload-to-amazon-s3-from-dropbox-using-hazel.html">Upload to Amazon S3 from Dropbox using Hazel</a>" </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> See this thread for more details: <a href="https://github.com/boto/boto/issues/2836">https://github.com/boto/boto/issues/2836</a> </p></div></div>


</div>
</div>