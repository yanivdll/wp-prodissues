---
ID: 810
post_title: Self User Testing
author: Yaniv
post_date: 2016-09-27 23:30:00
post_excerpt: ""
layout: post
permalink: >
  http://prodissues.com/2016/09/self-user-testing.html
published: true
---
OK, so I'm retracting from agreeing that descriptions are useless. I just had an experience that proved that wrong.

Well, some context will be helpful... let me step back and explain. Yesterday we had a heated discussion in the team about the usefulness of showing a description of a post inside a recommendation tile in our chatbot. Take a look at the screenshot bellow. This is how we currently display recommendations in <a href="http://m.me/outbrain">our Facebook Messenger bot</a>:
<div class="figure">

<img src="http://media.prodissues.com/images/2016/09/fb-chatbot-ctas.PNG" alt="fb-chatbot-ctas.PNG" />

</div>
Each recommendation comes with a set of metadata: thumbnail, title, source, and description. The bot.outbrain.com is an ugly appendage forced by Facebook. Then there are the actions you can take on a recommendation. Clicking on the thumbnail will open the article in a webview. Summary will return an auto generated summary<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup>, stash will save it for later, and #{topic} will return more recommendations from the same topic.

You'll notice that the description in this example (taken from the article page) isn't great. It's trimmed, and do little to explain what this story is about. Essentially, it doesn't help me taking a decision to read or pass on this recommendation.

One of the ideas we came up with is replacing the description with the reason the user see a specific recommendation. We call this feature "Amplify the WHY". So in the example the image above,  I'm probably seeing this story because I read a lot about science and astronomy. So the "WHY" in this case might read something like "because you're interested in astronomy".

It would have been nice to show both description <b>and</b> the "WHY", but we have limited real-estate to work in, and need to choose one of them.

My team was adamant that we should drop the description and go with the "WHY". At first, I was reluctant to agree. "I want to see data first", I said. "Let's run AB testing". "Well, we don't have users yet, so AB testing isn't relevant at that point. Also, it is clear that 'amplifying the WHY' is so much better than showing a crappy description that we should take this as the baseline" was the reply I got. How can you argue with such compelling reasoning...

Now, circling back to my opening, I'm taking my agreement back.

I woke up at 7am today and wanted to read about the results of the debate yesterday night. I didn't know where I can find this information, quickly and succinctly<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>. I thought about the CNN chatbot, but CNN's top stories are posted only at about 9am. Then I figure, let's try to see if I can find something relevant in our bot.

I typed "hi", and (to my surprise) the first story I got was right on point -
<div class="figure">

<img src="http://media.prodissues.com/images/2016/09/fb-chatbot-election-debate.PNG" alt="fb-chatbot-election-debate.PNG" />

</div>
Then I browsed a little more, and suddenly took notice that in any recommendation, which has a relevant title, I skim the description for more context. I also realized that I don't look for completeness or quality; just few more words that will give better idea what the article is about.

"WHY" I get a recommendation, and why it's important to me wasn't relevant in the context I were in - checking the news, the objective news, not that that that's in my "bubble".

Summary wasn't relevant in that usecases either, because much like clicking to read the story, it means "choosing" and focusing on one article, whereas I was still at the decision making stage.

So, what I've learned from observing myself (and in that rare instance, I acted as a user, rather than a stakeholder) is that description does have value, and in certain usecased, such as browsing the news, I need objective hooks. Description, in that case, and not personalized reason, were more relevant.

Definitely not representative experience, but one that makes me rethink what should be the baseline. And whatever the baseline is, we should put it to test.
<div id="footnotes">
<h2 class="footnotes">Footnotes:</h2>
<div id="text-footnotes">
<div class="footdef">

<sup><a id="fn.1" class="footnum" href="#fnr.1">1</a></sup>
<div class="footpara">
<p class="footpara">Works pretty neatly. Here's the summary for this article in the picture: "On Tuesday, thousands of people stampeded into a lecture hall in Guadalajara, Mexico, to hear SpaceX CEO Elon Musk talk about how he wants to colonize Mars. Another question is how — and if — Musk plans to prevent Earth microbes from contaminating Mars, and Mars microbes (if there are any) from contaminating Earth."</p>

</div>
</div>
<div class="footdef">

<sup><a id="fn.2" class="footnum" href="#fnr.2">2</a></sup>
<div class="footpara">
<p class="footpara">I don't go to sites to look for news anymore, and rarly google for news. And since the extinction of <a href="https://en.wikipedia.org/wiki/Flipboard">Zite</a>, I now realize, I have no idea where I get my news from...</p>

</div>
</div>
</div>
</div>