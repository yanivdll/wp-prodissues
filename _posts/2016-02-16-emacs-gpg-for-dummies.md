---
ID: 337
post_title: Emacs GPG For Dummies
author: Yaniv
post_date: 2016-02-16 00:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/02/emacs-gpg-for-dummies.html
published: true
---
I've <a href="http://prodissues.com/2016/02/adding-mu4e-support-to-emacs.html">set up mu4e</a>, and have my Gmail credentials stored in two files:
<ol class="org-ol">
	<li><code>.offlineimaprc</code> - this file is used by Offlineimap to connect to my Gmail and sync my inbox with mu4e.</li>
	<li><code>.authinfo</code> - that file stores my Gmail credential, and used by Emacs to send emails.</li>
</ol>
<!--more-->

Unfortunately, both of those files are plain text, and though I’m not a security freak, I’m uncomfortable storing my passwords out in the open. So, I went ahead to find out how to encrypt them. Most of the tutorials I read were too technical, and covered much more than my simple usecase. It’s not that I couldn’t follow theme, but I know I wouldn’t have retained the information, and able to retract my steps if I needed to in the future.

My goal with this post was to create a simple guide on how to install gpg, generate a key, and use it in mu4e. I failed... I thought I will be able to it non-technical for the most part, but once getting to configure Emacs and mu4e to work with gpg, I had to delve into some heavy configuration, which included the creation of a python script to work along Offlineimap... The good thing is that this guide <i>will</i> help you get Emacs and mu4e work with an encrypted version of a <code>.authinfo</code> file, and your credentials will remain secret.

Now that our expectations are set, and assuming you're up for the ride, lets start this journey.
<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">Installing GPG</h2>
<div id="text-orgheadline1" class="outline-text-2">
<div class="org-src-container">
<pre class="src src-sh">~ $ brew install gpg
</pre>
</div>
Let's make sure gpg was installed:
<div class="org-src-container">
<pre class="src src-sh">~ $ gpg --version
</pre>
</div>
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/gpg--version.png" alt="gpg--version.png" />

<span class="figure-number">Figure 1:</span> gpg version information along with the list of supported algorithms

</div>
Now really, the most informative source of information is gpg's help. Go ahead and skim it:
<div class="org-src-container">
<pre class="src src-emacs-lisp">~ $ gpg -h
</pre>
</div>
</div>
</div>
<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Create a key</h2>
<div id="text-orgheadline2" class="outline-text-2">
<div class="org-src-container">
<pre class="src src-sh">~ $ gpg --gen-key
</pre>
</div>
There’s a simple wizard that lets you set the encryption type, and asks for your name, email address and other comments. Those details will be associated with your key.

Next, you’ll be asked to create a passphrase. This is like the password to your secret key. If you lose it, you’ll have no access to any of the information encrypted with this key. So don’t ever lose it…

Here’s how this flow looks like:
<div class="org-src-container">
<pre class="src src-sh">~ $ gpg --gen-key
<span style="color: #d55e00;">gpg</span> (GnuPG) 1.4.19; Copyright (C) 2015 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 
Requested keysize is 2048 bits   
Please specify how long the key should be valid.
         0 = key does not expire
      &lt;n&gt;  = key expires<span style="color: #56b4e9; font-weight: bold;"> in</span> n days
      &lt;n&gt;w = key expires<span style="color: #56b4e9; font-weight: bold;"> in</span> n weeks
      &lt;n&gt;m = key expires<span style="color: #56b4e9; font-weight: bold;"> in</span> n months
      &lt;n&gt;y = key expires<span style="color: #56b4e9; font-weight: bold;"> in</span> n years
Key is valid for? (0) 
Key does not expire at all
Is this correct? (y/N) y

You need a user ID to identify your key; the software constructs the user ID
from the Real Name, Comment and Email Address<span style="color: #56b4e9; font-weight: bold;"> in</span> this form:
    <span style="color: #848ea9;">"Heinrich Heine (Der Dichter) <a href="mailto:heinrichh%40duesseldorf.de">&lt;heinrichh@duesseldorf.de&gt;</a>"</span>

Real name: Jane Roe            
Email address: jane@example.com
Comment: lorem ipsum           
You selected this USER-ID:
    <span style="color: #848ea9;">"Jane Roe (lorem ipsum) <a href="mailto:jane%40example.com">&lt;jane@example.com&gt;</a>"</span>

<span style="color: #d55e00;">Change</span> (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a Passphrase to protect your secret key.    

We need to generate a lot of random bytes. It is a good idea to perform
some other action (<span style="color: #0072b2;">type</span> on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
..........+++++
<span style="color: #0072b2;">.</span>+++++
We need to generate a lot of random bytes. It is a good idea to perform
some other action (<span style="color: #0072b2;">type</span> on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
..........+++++
...+++++
gpg: key 86B62C98 marked as ultimately trusted
public and secret key created and signed.

gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
pub   2048R/86B62C98 2016-02-17
      Key fingerprint = 42FD C031 BD51 4CC8 7C02  EA14 35D4 80A2 86B6 2C98
uid                  Jane Roe (lorem ipsum) <a href="mailto:jane%40example.com">&lt;jane@example.com&gt;</a>
sub   2048R/8C0D5E5D 2016-02-17

~ $
</pre>
</div>
Now that you've created a key, you can go ahead and sign the <code>.authinfo</code> file.

</div>
</div>
<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">Sign and encrypt the <code>.authinfo</code> file<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup></h2>
<div id="text-orgheadline3" class="outline-text-2">
<div class="org-src-container">
<pre class="src src-sh">~ $ gpg -se .authinfo
</pre>
</div>
You'll be asked for your passphrase. Enter it, and the <code>.authinfo</code> will be signed, and renamed to <code>.authinfo.gpg</code>

<a href="https://www.emacswiki.org/emacs/GnusAuthinfo">EmacsWiki</a> suggests to limit permission to this file. I find it important:
<div class="org-src-container">
<pre class="src src-sh">~ $ chmod 600 .authinfo.gpg
</pre>
</div>
Back in Emacs, there are couple of changes we need to make in order for mu4e to start working with the <code>,authinfo.gpg</code> file. I wish I read <a href="https://gist.github.com/areina/3879626">this gist</a> before, because it covers those changes succinctly, but here is a summary of those modifications:

</div>
</div>
<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Changes to <code>.offlineimaprc</code></h2>
<div id="text-orgheadline4" class="outline-text-2">

Two additions:
<ol class="org-ol">
	<li>A reference to a python file where you'll store a function to fetch your credentials from the <code>.authinfo.gpg</code> file</li>
	<li>Under the <code>[Repository Remote]</code> section add the call to the <code>get_password_emac</code> function</li>
</ol>
Here's how your <code>.offlineimaprc</code> file will look like afterwards:
<div class="org-src-container">
<pre class="src src-emacs-lisp">[general]
accounts = Gmail
maxsyncaccounts = 3
pythonfile = ~/.offlineimap.py

[Account Gmail]
localrepository = Local
remoterepository = Remote

[Repository Local]
type = Maildir
localfolders = ~/Maildir
[Repository Remote]
type = IMAP
remoteuser = yanivdll@gmail.com
remotehost = imap.gmail.com
remotepasseval = get_password_emacs(<span style="color: #848ea9;">"imap.gmail.com"</span>, <span style="color: #848ea9;">"yanivdll@gmail.com"</span>, <span style="color: #848ea9;">"993"</span>)
ssl = yes
sslcacertfile = /usr/local/etc/openssl/certs/ca-bundle.crt
maxconnections = 1
realdelete = no
</pre>
</div>
</div>
</div>
<div id="outline-container-orgheadline5" class="outline-2">
<h2 id="orgheadline5">Add a <code>.offlineimap.py</code> file</h2>
<div id="text-orgheadline5" class="outline-text-2">

This file will define the <code>get_password_emac</code> function:
<div class="org-src-container">
<pre class="src src-python"><span style="color: #009e73; font-style: italic;">#</span><span style="color: #009e73; font-style: italic;">!/usr/bin/python</span>
<span style="color: #56b4e9; font-weight: bold;">import</span> re, os

<span style="color: #56b4e9; font-weight: bold;">def</span> <span style="color: #d55e00;">get_password_emacs</span>(machine, login, port):
    <span style="color: #e69f00; font-weight: bold;">s</span> = <span style="color: #848ea9;">"machine %s login %s port %s password ([^ ]*)\n"</span> % (machine, login, port)
    <span style="color: #e69f00; font-weight: bold;">p</span> = re.<span style="color: #0072b2;">compile</span>(s)
    <span style="color: #e69f00; font-weight: bold;">authinfo</span> = os.popen(<span style="color: #848ea9;">"gpg -q --no-tty -d ~/.authinfo.gpg"</span>).read()
    <span style="color: #56b4e9; font-weight: bold;">return</span> p.search(authinfo).group(1)
</pre>
</div>
</div>
</div>
<div id="outline-container-orgheadline6" class="outline-2">
<h2 id="orgheadline6">Changes to mu4e config</h2>
<div id="text-orgheadline6" class="outline-text-2">

Lastly, in your Emacs config, under the mu4e smtp settings, add a reference to the encrypted auth file:
<div class="org-src-container">
<pre class="src src-emacs-lisp">...
(setq message-send-mail-function 'smtpmail-send-<span style="color: #e69f00; font-weight: bold;">it</span>
      starttls-use-gnutls t
      smtpmail-starttls-credentials
      '((<span style="color: #848ea9;">"smtp.gmail.com"</span> 465 nil nil))
      smtpmail-auth-credentials
      (expand-file-name <span style="color: #848ea9;">"~/.authinfo.gpg"</span>)
      smtpmail-default-smtp-server <span style="color: #848ea9;">"smtp.gmail.com"</span>
      smtpmail-smtp-server <span style="color: #848ea9;">"smtp.gmail.com"</span>
      smtpmail-smtp-service 465
      smtpmail-debug-info t)
...
</pre>
</div>
Now, you're emails should be sent using the <code>.authinfo.gpg</code> file. Go on and try it<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>. Note that before actually sending the email, Emacs will ask for your passphrase<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>.

</div>
</div>
<div id="outline-container-orgheadline10" class="outline-2">
<h2 id="orgheadline10">Extras</h2>
<div id="text-orgheadline10" class="outline-text-2"></div>
<div id="outline-container-orgheadline7" class="outline-3">
<h3 id="orgheadline7">Backup private key</h3>
<div id="text-orgheadline7" class="outline-text-3">

I stored all the information related to my gpg key, as well as a backup file in my <a href="https://agilebits.com/onepassword">1password</a>. Here's how I created the key backup:
<div class="org-src-container">
<pre class="src src-sh">~ $ gpg --export-secret-keys --armor jane@example.com &gt; jroe-privkey.asc
</pre>
</div>
<b>Important:</b> Make sure to store the output file in a secure place; it contains your private key in plain text.

</div>
</div>
<div id="outline-container-orgheadline8" class="outline-3">
<h3 id="orgheadline8">Encrypt text in Emacs</h3>
<div id="text-orgheadline8" class="outline-text-3">
<ol class="org-ol">
	<li>Mark the text you would like to encrypt</li>
	<li>Run <code>M-x epa-encrypt-region</code></li>
	<li>Mark the key you would like to use for encryption</li>
</ol>
Now the encrypted text will replace the original, plain, text:
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/encrypted-text.png" alt="encrypted-text.png" />

<span class="figure-number">Figure 2:</span> <code>M-x epa-encrypt-region</code> will encrypt a region of text in Emacs

</div>
</div>
</div>
<div id="outline-container-orgheadline9" class="outline-3">
<h3 id="orgheadline9">Decrypt text</h3>
<div id="text-orgheadline9" class="outline-text-3">

To decrypt a message, or a file you've encrypted:
<ol class="org-ol">
	<li>Mark the text you would like to decrypt (you'll have to mark also the header and footer of the message)</li>
	<li>Run <code>M-x epa-decrypt-region</code>
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/decrypt-text.png" alt="decrypt-text.png" />

<span class="figure-number">Figure 3:</span> <code>M-x epa-decrypt-region</code> will decrypt a region of text in Emacs

</div></li>
	<li>Enter your passphrase</li>
	<li>Emacs will ask if you want the decrypted text to replace the original text. If you choose "No", it will open the text in a second window.</li>
</ol>
<div class="figure">

<img src="http://media.prodissues.com.s3.amazonaws.com/images/2016/02/decrypted-text-2.png" alt="decrypted-text-2.png" />

<span class="figure-number">Figure 4:</span> The decrypted text in a second window

</div>
That's it. If you're interested in more than the basics that I went through above, try the links bellow.

&nbsp;

</div>
</div>
</div>
<div id="outline-container-orgheadline11" class="outline-2">
<h2 id="orgheadline11">Reference</h2>
<div id="text-orgheadline11" class="outline-text-2">
<ul class="org-ul">
	<li><a href="https://www.gnupg.org/documentation/howtos.html">Gnupg - documentation</a></li>
	<li>Using gpg in emacs - <a href="https://www.gnu.org/software/emacs/manual/html_mono/epa.html#Quick-start">EasyPG Assistant user’s manual</a></li>
	<li><a href="https://fedoraproject.org/wiki/Creating_GPG_Keys#ExportCLI">Fedora Wiki pages</a> - GPG essentials</li>
	<li><a href="https://www.emacswiki.org/emacs/GnusAuthinfo">EmacsWiki - GnusAuthinfo</a></li>
	<li><a href="http://danzorx.tumblr.com/post/11976550618/easypg-for-emacs-on-os-x-or-sometimes-emacs">Tricotism - EasyPG for Emacs on OS X, or sometimes Emacs doesn’t load the env paths you might expect</a></li>
	<li><a href="http://ubuntuforums.org/showthread.php?t=2155060">ubuntu forums</a> - Encrypting and decrypting a message</li>
</ul>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes:</h2>
<div id="text-footnotes">
<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup>
<div class="footpara">
<p class="footpara">Made an edit here (initially, I only signed the file, without encrypting it). Thanks <a href="https://www.reddit.com/user/aminb">/u/aminab</a> for <a href="https://www.reddit.com/r/emacs/comments/46fi6f/adding_mu4e_support_to_emacs_part_two_configuring/d04szm3">the correction</a>.</p>

</div>
</div>
<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup>
<div class="footpara">
<p class="footpara">If you still have the <code>.authinfo</code> file, rename it. Once we see that mu4e sends emails using the encrypted version of the auth file, we can dispose this, decrypted, version of it.</p>

</div>
</div>
<div class="footdef"><sup><a id="fn.3" class="footnum" href="#fnr.3">3</a></sup>
<div class="footpara">
<p class="footpara">If Emacs asks for your passphrase too often, you might find this <a href="https://www.reddit.com/r/emacs/comments/45lx1s/adding_mu4e_support_to_emacs_the_hard_way/d01b1hu">comment in Reddit</a>, by <a href="https://www.reddit.com/user/aminb">/u/aminb</a>, helpful.</p>

</div>
</div>
</div>
</div>