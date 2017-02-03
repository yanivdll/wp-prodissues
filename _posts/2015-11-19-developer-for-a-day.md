---
ID: 61
post_title: Developer for a day
author: Yaniv
post_date: 2015-11-19 05:00:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2015/11/developer-for-a-day.html
published: true
---
<p> Earlier today I demoed a simple search page that I developed as part of a 24 hour hackathon here at Outbrain. What makes this search page unique is that it uses the Sphere platform<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> to find content that isn't only relevant to the search query, but also caters to the user's interests. So, for example, if I search for "python", I'll get articles about python, the programming language. If my mom, on the other hand, do the same search, she'll get articles <a href="http://www.cnn.com/videos/us/2015/11/10/alligator-python-photo-florida-dnt-wftx.wftx">like this one</a>. </p>

<p> But <i>what</i> I developed isn't the subject of this article (I might write about it in a separate post). What I <i>do</i> want to share is my experience at putting a developer hat for a day. As a product manager, who works very closely with engineers, this turned out to be an invaluable lesson. </p>

<p> I had no intention of building anything in that hackathon. My plan was to help and support the hacking teams<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>. A few minutes after the hackathon began, though, I thought it will be cool to build this search page. Unfortunately, at that point there were no developers around to whom I could pitch my idea. All of them were already assigned to other teams. But I got this impulse to build something, so I decided to challenge my lack of development skills, and form a team of one. </p>

<p> Well, saying that I'm not a developer isn't entirely true. Afterall, I graduated as a software engineer, I understand technology, I can speak intelligently about software architecture and design patterns, and I was intimately involved in designing and building the Sphere platform. I even do some coding in my spare time<sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>. But, I've never coded with a mission or under a strict deadline. So I thought, this would be an opportunity to get serious about coding. Indeed, serious I became, spending the next 24 hours (minus 6 hours of sleep) hacking my way toward something I'll be proud to present. </p>

<p> Here's how my next 24 hours have looked like: </p>

<p> <b>10:20am</b> - 20 minutes into the hackathon I'm having this idea, and yada yada yada I decide to code. </p>

<p> <b>10:40am</b> - I can see what the architecture of the solution should look like, and what APIs I'll have to use. It's going to be easier than I thought... </p>

<p> <b>11:30am</b> - Hitting a dead-end. My initial approach won't work, because I don't have access, from the environment I'm using, to the API I rely on. Need to think of a new direction. </p>

<p> <b>12:00pm</b> - Found a new direction. I'm not sure it's the right one, and I'll have to learn a framework that I didn't use before (well, I didn't use <i>any</i> framework before...), but I'm running out of options, so I'm taking the chance. I find a tutorial, and hope to learn everything I need to know before the hackathon is over. </p>

<p> <b>1:30pm</b> - Urr... this is the longest tutorial ever, and it's not even related to the use-case I'm trying to solve. </p>

<p> <b>2:15pm</b> - OK, good news and bad news. The good - I finally finished the tutorial. The bad - I still don't have a clue how to work with this framework to build what I have in mind. </p>

<p> <b>3:00pm</b> - 5 hours have passed, and I still have nothing. What's worse - people around me have high expectations of me. I have no idea why, but I know I'm going to disappoint them. I'm loosing my patience, and even the quietest chatter in the room distracts me. I'm agitated, and my fuse shortens by the minute. I hope no one will talk to me. I need silence. Maybe I should put headphones on, or go to a secluded room... </p>

<p> <b>4:10pm</b> - Half a day went by, and I'm farther away from my initial idea than I was 6 hours ago. Maybe some coffee and fresh air will help me regain energy and spirit. </p>

<p> <b>4:20</b> - I don't know if it's the coffee or the time off the computer, but I'm thinking more clearly now. In fact, I have an idea. I need to run back to the office. </p>

<p> <b>5:30pm</b>  - I have a working solution! It looks awful, but works.... all I have to do now is take care of the front-end. Easy breezy. </p>

<p> <b>9:15pm</b> - <b>I hate CSS</b>. I'm about to loose my mind. I must eat. </p>

<p> <b>10:00pm</b> - I need to have <i>some</i> sleep. I'm sure things will look easier tomorrow. </p>

<p> <b>8:10am</b> - CSS is still CSS. </p>

<p> <b>9:55am</b> - 5 minutes to my demo. With some help, hand-holding and a lot of duct-tape my work is somewhat presentable. I hope people see the potential, and won't get caught-up with the UI. </p>

<p> <b>10:10am</b> - I've just presented my thing. <b>I feel awesome</b>. I built something and got people's  applause. </p>

<p> Now, what did I learn from this schizophrenic experience: </p>
<div id="outline-container-orgheadline1" class="outline-2">
<h2 id="orgheadline1">I don't want to be a developer.</h2>
<div class="outline-text-2" id="text-orgheadline1">
<p> Yeah, as simple as that. I'll keep doing it as a hobby, but I'll never do it professionally. I mean, I love the problem solving, and creating something with my own hands is amazing. But, getting sucked into the smallest of details, spending hours trying to figure out what I did wrong, only to find a missing <code>;</code>, and wasting tons of time on configuration before I can do <i>anything</i>, make me go nuts... </p>

<p> OK, so as this door is now closed, what did I learn about coding that will help me understand engineers better? </p>
</div>
</div>

<div id="outline-container-orgheadline2" class="outline-2">
<h2 id="orgheadline2">Coding requires focus</h2>
<div class="outline-text-2" id="text-orgheadline2">
<p> Soooo much of it. Even the slightest distraction can throw your thought process miles away. It then takes a lot of time to regain your thoughts, and get back to where you were before. I now understand even better Joel's <a href="http://www.joelonsoftware.com/articles/fog0000000022.html">"Human Task Switches Considered Harmful"</a> post. </p>
</div>
</div>

<div id="outline-container-orgheadline3" class="outline-2">
<h2 id="orgheadline3">Tools are important</h2>
<div class="outline-text-2" id="text-orgheadline3">
<p> Don't ask why, but I've started to learn <a href="https://www.gnu.org/software/emacs/">Emacs</a> recently, and so far I love it. But, Emacs isn't the most dummy proof app out there. Here's a funny chart, that actually stops being that funny when you start learning Emacs: </p>

<div class="figure"> <p><img src="http://media.prodissues.com/images/2015/11/3251176498_c3485a55fb.jpg" alt="3251176498_c3485a55fb.jpg" /> </p> </div>

<p> So, since I'm somewhere at the bottom of the learning curve still, I thought this hackathon would be an opportunity to learn the tool better and faster. But as soon as time started to press on me, and at the first instance when I didn't know how to do something in Emacs that was trivial in other tools, I closed it and opened the other tools I feel comfortable with (<a href="https://www.sublimetext.com/">Sublime</a> and <a href="https://coderunnerapp.com/">CodeRunner</a>). </p>
</div>
</div>

<div id="outline-container-orgheadline4" class="outline-2">
<h2 id="orgheadline4">Knowing what's the expected outcome is key</h2>
<div class="outline-text-2" id="text-orgheadline4">
<p> Having a clear idea of what my end product should do, and to some extent - how it should look like, was crucial. I had so much to learn in a very short time, but knowing what my end goal was kept me focused. It also helped me stay on course and learn only what was relevant to getting my project done (otherwise I have the tendency to drift away quickly). </p>

<p> And lastly, I experienced first hand how deadlines and quality [don't] play [well] together: </p>
</div>
</div>

<div id="outline-container-orgheadline5" class="outline-2">
<h2 id="orgheadline5">Code becomes crappier as deadline approaches</h2>
<div class="outline-text-2" id="text-orgheadline5">
<p> You might think that my experience isn't a good enough example, and I might agree. I'm just saying that now I can better relate to this <a href="https://twitter.com/hashtag/NOdeadlines?src=hash">#NoDeadlines</a> trend. </p>

<p> If you're involved, at any capacity, in product development, you already know this lesson, because crappy code keeps bouncing back at you and eats the time and resources you need in order to build new stuff. Don't be fooled by fancy terms, such as "tech-debt" and "refactoring" - these are politically correct ways to refer to crappy code. And the stricter the deadlines, the more of it you'll get<sup><a id="fnr.4" class="footref" href="#fn.4">4</a></sup>. </p>

<p> So with that, I'll put my developer hat down. It's too big for me... </p>
</div>
</div>
<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup> <div class="footpara"><p class="footpara"> Check out the platform <a href="http://developers.sphere.com/#/">here</a>, and leave a comment if you're interested to learn more. </p></div></div>

<div class="footdef"><sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup> <div class="footpara"><p class="footpara"> There were 19 internal and external teams hacking. </p></div></div>

<div class="footdef"><sup><a id="fn.3" class="footnum" href="#fnr.3">3</a></sup> <div class="footpara"><p class="footpara"> In case you're interested, here's <a href="https://github.com/yanivdll">my GitHub account</a>. </p></div></div>

<div class="footdef"><sup><a id="fn.4" class="footnum" href="#fnr.4">4</a></sup> <div class="footpara"><p class="footpara"> No, it doesn't mean I won't ask for time-lines and set deadlines in the future... </p></div></div>


</div>
</div>