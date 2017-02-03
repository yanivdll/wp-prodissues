---
ID: 323
post_title: Adding mu4e Support To Emacs
author: Yaniv
post_date: 2016-02-12 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/02/adding-mu4e-support-to-emacs.html
published: true
---
Couple of months ago<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> I started to use Emacs as my secondary email client; the primary one remains Gmail's web interface. Bringing my Gmail account to Emacs wasn't as smooth sail as I hoped it to be, but I'm happy with the results so far.
<div id="outline-container-orgheadline1" class="outline-2">

<!--more-->
<h2 id="orgheadline1">Why use Emacs for emails?</h2>
<div id="text-orgheadline1" class="outline-text-2">
<ul class="org-ul">
	<li>Because <del>I</del> Emac can.</li>
	<li>Because when writing a serious email (one with more than two lines), I usually draft it in an editor first. Now that this editor is Emacs, it makes sense to do the editing <i>and</i> the sending parts in it...</li>
	<li>Because I want org support for my emails</li>
	<li>And, because <a href="https://www.google.com/search?q=emacs+email%5C&amp;client=safari&amp;rls=en&amp;source=lnms&amp;tbm=isch&amp;sa=X&amp;ved=0ahUKEwjSnqe8ys_JAhXH2D4KHYPAD4kQ_AUIBygB&amp;biw=1496&amp;bih=1003#tbm=isch&amp;q=emacs+email">these images</a> makes emails look way cooler in Emacs than in any other client.</li>
</ul>
</div>
</div>
<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Chosing an email client</h2>
<div id="text-orgheadline2" class="outline-text-2">

I went back and forth between mu4e and gnus, and finally took <a href="http://codingquark.com/setting-up-gnus-in-emacs/">Dhavan Vaidya's</a> advice to pick one and just move on with it. Unlike him, though, I chose mu4e, mainly because its focus on search.

So here we go - implementing mu4e in Emacs. For a quick and dirty checklist, follow the first part, which summaries the steps to get mu4e working. If you're more of an FPS person, and interested in the details, read through the second part, which journals my steps as well as the errors I encountered and their fixes.
<div class="callbox">

Note: The <a href="http://www.djcbsoftware.nl/code/mu/mu4e/index.html">Mu4e official manual</a> is great, as long as everything works flawlessly. In my case, though, I run through every problem and error possible. So if you want to install mu4e, I recommend you'll start with the manual. If you get stuck, or encounter a problem, you might find the solution here.

</div>
</div>
<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">The short story</h2>
<div id="text-orgheadline3" class="outline-text-2">
<ol class="org-ol">
	<li>Install <a href="http://brew.sh/">Homebrew</a></li>
	<li>Install <a href="http://offlineimap.org/">offlineimap</a></li>
	<li>Configure offlineimap to point to the IMAP server you would like to connect to.</li>
	<li>Run offlineimap for the first time to download your IMAP folder from the remote server.</li>
	<li>Get mu from git: <a href="https://github.com/djcb/mu">https://github.com/djcb/mu</a></li>
	<li>Run mu to index and load the messages into Emacs.</li>
	<li>Configure your Emacs init file to connect with mu4e and customize the client.</li>
	<li>On Emacs, run - <code>M-x mu4e</code></li>
</ol>
</div>
</div>
<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">The details</h2>
<div id="text-orgheadline4" class="outline-text-2">

According to the manual, mu4e is only a client, or an interface to my emails, and does non of the fetching, storing, editing or sending them on its own.
<blockquote>This leaves mu4e to concentrate on what it does best: quickly finding the mails you are looking for, and handle them as efficiently as possible.</blockquote>
Mu4e should, therefore, be complemented with the other components to work. My hope is that installing all those packages won't be too big of a hassle... And with that, let's move on to the installation checklist.

The <a href="http://www.djcbsoftware.nl/code/mu/mu4e/Installation.html#Installation">mu4e manual</a> is thorough and informative, but I'm not sure how to install mu and make it available in Emacs. I also don't understand what I should use to manage the IMAP repository for me. I'm getting confused...

Searching for unofficial documentation, or a blog post for some extra hand holding, I find <a href="http://blog.developwithpassion.com/2013/05/02/getting-up-and-running-with-a-sane-mutt-setup/">this one</a> by Jean-Paul. It turned out that I should install offlineimap from brew, as well as SQLite, which will store messages' states:

</div>
<div id="outline-container-orgheadline5" class="outline-3">
<h3 id="orgheadline5">Installing offlineimap</h3>
<div id="text-orgheadline5" class="outline-text-3">
<div class="org-src-container">
<pre class="src src-sh">// install brew
$ brew install wget
</pre>
</div>
<div class="org-src-container">
<pre class="src src-sh">//install offlineimap
$ brew install offlineimap
</pre>
</div>
Done. Next - modify the offlineimap configuration file. Here's my Gmail setup:
<div class="org-src-container">
<pre class="src src-sh">[general]
accounts = Gmail
maxsyncaccounts = 3

[Account Gmail]
localrepository = Local
remoterepository = Remote

[Repository Local]
<span style="color: #728a05;">type</span> = Maildir
localfolders = ~/Maildir

[Repository Remote]
<span style="color: #728a05;">type</span> = IMAP
remotehost = imap.gmail.com
remoteuser = USERNAME@gmail.com //change with your email
remotepass = PASSWORD         //change with your password
ssl = yes
sslcacertfile = /etc/ssl/certs/ca-certificates.crt
maxconnections = 1
realdelete = no
</pre>
</div>
This <code>sslcacertfile</code> line I got from <a href="http://superuser.com/questions/927632/configuring-offlineimap-for-gmail-ssl-error">stack-overflow</a>, after getting an error when trying to load <code>offlineimap</code>.

Offlineimap still refuses to load. Apparently the folder specified in <code>sslcacertfile</code> doesn't exist in my computer, and offlineimap can't connect to my Gmail account. More research, and I finally find this helpful, <a href="http://lists.alioth.debian.org/pipermail/offlineimap-project/2014-August/004916.html">"How can I use sslcertfile"</a>, article. Here's the gist of it:
<ol class="org-ol">
	<li>Download the ca-cert bundle from <a href="https://downloads.sourceforge.net/project/machomebrew/mirror/curl-ca-bundle-1.87.tar.bz2">sourceforge</a>.</li>
	<li>Copy the <code>ca-bundle.crt</code> file to <code>/usr/local/etc/openssl/certs/</code></li>
	<li>I didn't have to, but if it still doesn't work, try running <code>/usr/local/opt/openssl/bin/c_rehas</code> , so openssl can take note of the new certificate.</li>
	<li>Update the <code>sslcacertifile</code> parameter with the new folder:</li>
</ol>
<div class="org-src-container">
<pre class="src src-sh">sslcacertfile = /usr/local/etc/openssl/certs/ca-bundle.crt
</pre>
</div>
Offlineimap is finally working, and downloading my emails.

Waiting... I have 45977 messages to sync, so it's going to take some time. I'll do other stuff in the meantime.

Damn! In my stupidity I closed the lid of my laptop, and when opened it again found that the offilneimap sync process hangs. I kill it, and try to run it again. I can't - another error. The fix - delete the <code>Gmail.lock</code> file:
<div class="org-src-container">
<pre class="src src-sh">$ rm .offlineimap/Gmail.lock
</pre>
</div>
Running <code>offlineimap</code> again. Works this time.
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/offlineimap-sync.png" alt="offlineimap-sync.png" />

</div>
While my repository is syncing, I switch to configure mu and mu4e.

</div>
</div>
<div id="outline-container-orgheadline6" class="outline-3">
<h3 id="orgheadline6">Installing mu</h3>
<div id="text-orgheadline6" class="outline-text-3">

First, I clone the mu repository and install libtool (I have no idea what it does, just that it's required for building mu)
<div class="org-src-container">
<pre class="src src-sh">$ git clone https://github.com/djcb/mu.git
$ brew install libtool
</pre>
</div>
Next, build mu:
<div class="org-src-container">
<pre class="src src-sh">$ cd mu
mu/$ autoreconf -i &amp;&amp; ./configure &amp;&amp; make
</pre>
</div>
Once the offlineimap process ends, I run mu to index my emails, which located at the <code>/Maildir</code> folder, as defined in the <code>~/.offlineimaprc</code> file.
<div class="org-src-container">
<pre class="src src-sh">/usr/local/Cellar/mu/mu/$ ./mu index
</pre>
</div>
Here's the result:
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/mu-index.png" alt="mu-index.png" />

</div>
We're making progress here...

</div>
</div>
<div id="outline-container-orgheadline7" class="outline-3">
<h3 id="orgheadline7">Emacs config</h3>
<div id="text-orgheadline7" class="outline-text-3">

Now I have to setup mu4e (mu for Emacs, I assume...). In my <a href="https://github.com/yanivdll/.emacs.d/blob/master/config.org#mu4e">config</a> file, I add the following settings, taken almost as-is from mu4e manual:
<div class="org-src-container">
<pre class="src src-emacs-lisp">(add-to-list 'load-path <span style="color: #259185;">"/usr/local/Cellar/mu/mu4e"</span>)
(setq mu4e-mu-binary (executable-find <span style="color: #259185;">"/usr/local/Cellar/mu/mu/mu"</span>))
(<span style="color: #728a05;">require</span> '<span style="color: #259185;">mu4e</span>)

<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">default</span>
(setq mu4e-maildir <span style="color: #259185;">"~/Maildir"</span>)
(setq mu4e-drafts-folder <span style="color: #259185;">"/[Gmail].Drafts"</span>)
(setq mu4e-sent-folder   <span style="color: #259185;">"/[Gmail].Sent Mail"</span>)
(setq mu4e-trash-folder  <span style="color: #259185;">"/[Gmail].Trash"</span>)
(setq mu4e-refile-folder  <span style="color: #259185;">"/[Gmail].All Mail"</span>)

<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">don't save message to Sent Messages, Gmail/IMAP takes care of this</span>
(setq mu4e-sent-messages-behavior 'delete)

<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">(See the documentation for `</span><span style="color: #259185; font-style: italic;">mu4e-sent-messages-behavior</span><span style="color: #81908f; font-style: italic;">' if you have</span>
<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">additional non-Gmail addresses and want assign them different</span>
<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">behavior.)</span>

<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">setup some handy shortcuts</span>
<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">you can quickly switch to your Inbox -- press ``</span><span style="color: #259185; font-style: italic;">ji</span><span style="color: #81908f; font-style: italic;">''</span>
<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">then, when you want archive some messages, move them to</span>
<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">the 'All Mail' folder by pressing ``</span><span style="color: #259185; font-style: italic;">ma</span><span style="color: #81908f; font-style: italic;">''.</span>

(setq mu4e-maildir-shortcuts
    '( (<span style="color: #259185;">"/INBOX"</span>               . ?i)
       (<span style="color: #259185;">"/[Gmail].Sent Mail"</span>   . ?s)
       (<span style="color: #259185;">"/[Gmail].Trash"</span>       . ?t)
       (<span style="color: #259185;">"/[Gmail].All Mail"</span>    . ?a)))

<span style="color: #81908f; font-style: italic;">;; </span><span style="color: #81908f; font-style: italic;">allow for updating mail using 'U' in the main view:</span>
(setq mu4e-get-mail-command <span style="color: #259185;">"offlineimap"</span>
</pre>
</div>
Note that I had to add the first two lines, because without them Emacs doesn't know about mu4e, and about where to find the mu executable. I know it because I tried evaluating the config many times time, without mu4e loading...

And now, finally, when I run <code>M-x mu4e</code>, Hooray!
<div class="figure">

<img src="http://media.prodissues.com/images/2015/12/mu4e_first_screen.png" alt="mu4e_first_screen.png" />

</div>
Now that I have all my emails in Emacs, I'll start learning the ins-and-outs of mu4e, and customize it further.

</div>
</div>
</div>
<div id="outline-container-orgheadline8" class="outline-2">
<h2 id="orgheadline8">Update</h2>
<div id="text-orgheadline8" class="outline-text-2">

Couple of weeks ago, Gmail asked that I change my password, due to a suspicious login attempt to my account. I did, and updated the password in my <code>.offlineimaprc</code> file. But since then, although incoming emails worked fine, I was unable to send emails from mu4e, and kept getting this error message:
<div class="org-src-container">
<pre class="src src-sh">smtpmail-send-it: Sending failed: 535-5.7.8 Username and Password not accepted. Learn more at
535 5.7.8  https://support.google.com/mail/answer/14257 64sm1217489qhf.40 - gsmtp<span style="color: #728a05;"> in</span> response to AUTH PLAIN AHlhbml2ZGxsADExODc3WWFu
</pre>
</div>
I spent days trying to sort this problem out. I went through <a href="https://support.google.com/mail/answer/14257">Google's detailed checklist</a> numerous times, read and posted in Google's support forum, looked in stack-overflow, but found nothing to help me solve that error.

Finally, I found an EmacWiki's article about <a href="https://www.emacswiki.org/emacs/SendingMail">sending mail</a> in Emacs. It mentions the <code>$(HOME)/.authinfo</code> file and I suspected it had something to do with the problem I had... I opened this file, and lo and behold... it had my Gmail credentials, including my old password in it. I updated the password and now I can use mu4e to send emails again.

</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes:</h2>
<div id="text-footnotes">
<div class="footdef">

<sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup>
<div class="footpara">
<p class="footpara">I was writing this post while going through the installation process, although I published it just now.</p>

</div>
</div>
</div>
</div>
</div>