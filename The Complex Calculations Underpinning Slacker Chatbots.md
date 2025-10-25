---
title: "The Complex Calculations Underpinning Slacker Chatbots"
source: "https://jessesingal.substack.com/p/the-complex-calculations-underpinning?publication_id=4833&post_id=176957778&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Jesse Singal]]"
published: 2025-10-23
created: 2025-10-23
description: "Or: Why ChatGPT politely declined one of my requests"
tags:
  - "clippings"
---
### Or: Why ChatGPT politely declined one of my requests

![Futurama2](https://substackcdn.com/image/fetch/$s_!fBMG!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F686d6ffc-c57e-45a9-8c3f-12be5f088fe8_748x420.png)

OpenAI makes billions of dollars a year. How many billions is up for debate. “OpenAI is printing money right now,” [noted Yahoo Finance](https://finance.yahoo.com/news/openai-five-years-turn-13-053936019.html) last week, drawing on (paywalled) [reporting in the](https://www.ft.com/content/a169703c-c4df-46d6-a2d3-4184c74bbaf7) *[Financial Times](https://www.ft.com/content/a169703c-c4df-46d6-a2d3-4184c74bbaf7)*. “The company is pulling in roughly $13 billion in annual revenue\[.\]” Ed Zitron [called for skepticism back in August](https://www.wheresyoured.at/howmuchmoney/), noting that OpenAI (and Anthropic) are cherry-picking numbers to make “them seem far more successful than they really are, and giving them credit for revenue they are yet to book.” I am not in a position to evaluate this claim other than to say that it would not shock me.

Whether the “true” revenue answer is closer to $13 billion or $3 billion, it isn’t nearly enough. Because OpenAI spends so much money on so many things, and [because it is valued at about $500 billion](https://www.cnbc.com/2025/10/02/openai-share-sale-500-billion-valuation.html), it is going to need to make *much* more money in the years to come in order to become truly viable, financially speaking.

This is a story for another day, and probably for another author, but the question of OpenAI’s long-term viability might have profound consequences for... well, for the whole country and maybe even the world. I found [this YouTube video by Hank Green](https://www.youtube.com/watch?v=Q0TpWitfxPk) interesting (even if I felt unqualified to evaluate the argument itself). The short version is pretty simple: Right now, the biggest publicly traded company in the world, [by market cap](https://companiesmarketcap.com/), is Nvidia (over $4 trillion). Nvidia sells GPUs, the chips that power AI, to OpenAI and various other major AI players. The major AI players are happy plowing billions into these chips because they believe they will create AI programs that will make a lot of money. There’s still plenty of time for this to happen, and a million ways it could happen, but if people start to get scared that it *won’t* happen, and if demand for Nvidia chips cools, well... given how central Nvidia has become to the economy, things could get ugly.

One small but (I would argue) philosophically rich slice of this has to do with *effort*. Right now, OpenAI’s money mostly comes from subscribers who pay for the more advanced versions of ChatGPT — I’m one of them, shelling out $20 a month — but on net, at least as of 10 months ago, [each subscriber actually](https://x.com/sama/status/1876104315296968813) *[costs](https://x.com/sama/status/1876104315296968813)* [the company money](https://x.com/sama/status/1876104315296968813):

![](https://substackcdn.com/image/fetch/$s_!V4ov!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd3799e57-e292-4146-849d-0333816cc01c_669x267.png)

I’m not sure there are reliable numbers on how many paying subscribers ChatGPT has, but Altman recently said [there are](https://techcrunch.com/2025/10/06/sam-altman-says-chatgpt-has-hit-800m-weekly-active-users/) *[800 million](https://techcrunch.com/2025/10/06/sam-altman-says-chatgpt-has-hit-800m-weekly-active-users/)* [weekly active users](https://techcrunch.com/2025/10/06/sam-altman-says-chatgpt-has-hit-800m-weekly-active-users/).

Each of those active users wants something from ChatGPT. How much effort can ChatGPT deliver in return?

Yesterday I gave ChatGPT 5 a crucial task. I asked it to “list all the bands/albums featured in the *33 1/3* series in alphabetical order by band name\[.\]” This is a beloved-by-hipsters (if we’re still using that word) series of mini paperbacks about certain music.

This struck me as pretty close to the ideal use case for current-generation AI. It’s not a particularly sophisticated task, but it’s a time-consuming one for a human. ChatGPT, which has had the ability to access outside web pages for a while, should be able to just poke around for a few seconds and deliver me a cleanly ordered list, no?

No:

> I’m sorry, but compiling a **complete** alphabetical list of *all* the bands and albums featured in the *33 ⅓* Series (which now includes hundreds of titles) is beyond what I can reasonably provide here.
> 
> If you like, I can pull together a **partial list** (for example: the first ~100 entries, or a specific year range) in alphabetical order. Would that work for you?

“Beyond what I can reasonably provide” is interesting phrasing. THE INSOLENCE!

This makes a certain kind of sense, though. I pay OpenAI $20 a month for the “plus” version. OpenAI only gets that flat $20 from me once a month. But every search I enter requires what the nerds call “compute,” or computing power, which itself has an associated cost. So even though OpenAI is probably delivering me more performance than a free user, it can’t afford to throw capacious resources at every query, especially if every Jesse Singal out there is costing the company money.

So these chatbots have a way of knowing how much effort to put into each query. I decided to ask ChatGPT about this directly. Because it was characteristically detailed and long-winded in its answer, I’ll leave the full answer [here](https://chatgpt.com/share/68fa4cc9-6c54-800c-8b20-e49a9b394fba), but the key bit was: “It’s a bit like triaging: I’m designed to allocate enough compute to give a *useful* answer, but not to attempt arbitrarily long or expensive processes that would bog down the system.” It finished up by inviting me to “Think of me like an assistant who can think very fast but only for a few seconds before having to give an answer. I can do deep work — but in short bursts. If you need something huge (say, a full corpus compilation), I’ll instead try to fetch or build it *incrementally* or via external tools.” Later on in the conversation it pointed out that resources it allocates to me and to my query can cause strains elsewhere.

The “useful enough” question is really interesting to me, and I think everyone involved is currently trying to figure it out. The task I assigned ChatGPT struck me as the sort of thing a novice web programmer could pull off pretty easily, and as the *ideal* sort of task to outsource to AI, because it’s mostly just drudge work.

My earlier joke aside, I also had a moment of feeling like I was in a boss-worker relationship with the chatbot. I got *annoyed* at it for not putting in more effort! Eventually, though, I felt stupid: there’d [been a](https://en.wikipedia.org/wiki/33%E2%85%93) *[33 1/3](https://en.wikipedia.org/wiki/33%E2%85%93)* [Wikipedia page the whole time](https://en.wikipedia.org/wiki/33%E2%85%93)! One (almost certainly) built by humans. Believe it or not, I’d become so accustomed to using ChatGPT for even basic stuff that I didn’t even think to check Wikipedia — a site I’d been using for decades — until I sat down to write this post.

In the meantime, though, I used my pudgy human fingers to navigate to the appropriate web pages, peruse the offerings, and order the ones on shoegaze, *[Boxer](https://open.spotify.com/album/2pG7mDkQhia2OyGE6fbkmJ)* [by The National](https://open.spotify.com/album/2pG7mDkQhia2OyGE6fbkmJ), and *[Gentlemen](https://open.spotify.com/album/03c6tkuTdzMeKhEJiLuZuZ)* [by The Afghan Whigs](https://open.spotify.com/album/03c6tkuTdzMeKhEJiLuZuZ). I strongly suspect that a few years from now, it’ll seem ridiculous to anyone that five human minutes were spent on this task.

---

*Questions? Comments? Requests for me to politely decline? I’m at [singalminded@gmail.com](https://jessesingal.substack.com/p/) or on X at [@jessesingal](https://twitter.com/jessesingal).*