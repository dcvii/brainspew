---
title: "How Anthropic Builds Claude’s Personality"
source: "https://www.bigtechnology.com/p/how-anthropic-builds-claudes-personality?publication_id=46510&post_id=164755713&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alex Kantrowitz]]"
published: 2025-05-29
created: 2025-05-30
description: "AI research house Anthropic wants its chatbot to behave like a “well-liked traveler,\" says researcher Amanda Askell. Here’s how it programs its values."
tags:
  - "clippings"
---
### AI research house Anthropic wants its chatbot to behave like a “well-liked traveler," says researcher Amanda Askell. Here’s how it programs its values.

![](https://substackcdn.com/image/fetch/w_424)

**Every AI bot’s** **personality** is the product of intentional decisions made within AI research houses, often behind closed doors. We typically only see glimpses of those decisions when things go awry, like in the cases of [“white-genocide” Grok](https://www.nytimes.com/2025/05/16/technology/xai-elon-musk-south-africa.html) or [“sycophant” ChatGPT](https://www.bbc.com/news/articles/cn4jnwdvg9qo). But otherwise, the process occurs in the background, influencing the type of conversations we have with the bots without our awareness.

But late last week, Anthropic gave the public a peek into how it tunes Claude’s personality. In a revealing session with reporters at the company’s first developer event in San Francisco. Amanda Askell, a researcher who works on the chatbot’s character, shared how the company is optimizing Claude.

So here’s a look into how Anthropic thinks about its chatbot’s character, and how it actually builds the personality we see:

## The Entry Point

Claude’s starting point is speaking to people around the world, often without lots of context or full knowledge of their intentions. It’s a difficult problem, Askell said, and requires the bot to take on some human-like qualities to respond.

“Claude’s situation is a bit weird. It has to assist lots of people across the world with lots of different needs,” Askell wrote on a slide. “A starting point might be something like ‘what would an ideal human do if they were in Claude’s situation.’”

## The Disposition

Instead of giving Claude a bunch of rules to follow in specific situations, Anthropic is trying to build a disposition into the bot. The concept of a robot’s disposition is similar to a human’s, where we have inherent qualities that manifest in our behavior. The bot’s disposition should come through in all interactions.

Claude’s disposition isn’t limited to ethical traits such as kindness and generosity, it also encompasses qualities that make someone a good conversationalist or friend, like integrity and wit. When the bot demonstrates these traits in new situations, it’s a sign that the disposition Anthropic is building is working.

## The Character

When you speak with Claude, you get a distinct sense of character as well. “A template here that I like is the idea of a well-liked traveler who can adjust to local customs and the person they're talking to without pandering to them,” Askell said. “They're often very open and thoughtful.”

This also means Anthropic is intentional about whether Claude tries to get us to prolong a conversation, even if it might one day be good for business. “If we think about people who are just trying to engage us, I don't think we often think of those people as good people that we want to hang out with all the time,” Askell said. “We think our friends are good because \[they tell us what\] we need to hear and don't just try and capture our attention.”

## The Implementation

Much of Claude’s personality is built in the post-training or fine-tuning stage. In this process, Anthropic asks people to write messages where the traits it wants to see would be relevant, and then write responses to those messages that are consistent with the ideal traits. The company then feeds the message chains into the model and asks it to emulate its desired behavior.

How Anthropic gets Claude to model these behaviors could be the subject of another, longer post (and if there’s interest, we can probably do it) but this is largely how the company gets the job done and makes Claude what (or who?) it is today.

---

## He’s already IPO’d once – this time’s different (sponsor)

![](https://www.bigtechnology.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/d6744497-a1aa-4dcd-aad5-139b852a2673_1920x1080.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:819,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:2486357,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://invest.pacaso.com/?utm_source=email&utm_medium=paid-partnership&utm_campaign=partnership45-01_05-29_10758330809%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://www.bigtechnology.com/i/164755713?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd6744497-a1aa-4dcd-aad5-139b852a2673_1920x1080.png%22,%22isProcessing%22:false,%22align%22:null})

Spencer Rascoff co-founded Zillow, scaling it into a $16B real estate giant. But everyday investors couldn’t invest until after the IPO, missing early gains.

"I wish we had done a round accessible to retail investors prior to Zillow's IPO," Spencer later said.

Now he’s doing just that. Spencer teamed up with fellow Zillow exec Austin Allison to launch Pacaso. Pacaso’s co-ownership marketplace is disrupting the $1.3T vacation home market. They’ve already surpassed $110M in gross profit and $1B in transactions.

Unlike Zillow, you can [invest in Pacaso](https://invest.pacaso.com/?utm_source=email&utm_medium=paid-partnership&utm_campaign=partnership45-01_05-29_10758330809) as a private company. Pacaso’s already reserved their Nasdaq ticker PCSO. But you don’t have to wait for a public listing to invest.

[Invest in Pacaso for just $2.80/share before midnight PST tonight.](https://invest.pacaso.com/?utm_source=email&utm_medium=paid-partnership&utm_campaign=partnership45-01_05-29_10758330809)

###### \*This is a paid advertisement for Pacaso’s Regulation A offering. Please read the offering circular at invest.pacaso.com. Reserving a ticker symbol is not a guarantee that the company will go public. Listing on the NASDAQ is subject to approvals. Under Regulation A+, a company has the ability to change its share price by up to 20%, without requalifying the offering with the SEC.

---

## Advertise with Big Technology?

Reach 160,000+ plugged-in tech readers with your company’s latest campaign, product, or thought leadership. To learn more, write [alex@bigtechnology.com](https://www.bigtechnology.com/p/) or reply to this email.

## What Else I’m Reading, Etc.

Semi trucks are driving themselves \[[New York Times](https://www.nytimes.com/2025/05/27/business/driverless-semi-trucks-aurora-innovation.html?unlocked_article_code=1.Kk8.rjwV.AFSR5-EII4fA&smid=url-share)\]

Y Combinator’s Luther Lowe: Little tech has a “valid fear of retaliation” from tech giants \[[FT](https://www.ft.com/content/0f32119b-d496-4b66-a9f1-cd6e7716c566)\]

Apple dips its toes into video game development \[[Digital Trends](https://www.digitaltrends.com/gaming/apple-acquires-rac7-sneaky-sasquatch/)\]

Chip manufacturers are running out of an essential substrate, leading to delays \[[Tom’s Hardware](https://www.tomshardware.com/tech-industry/semiconductors/ai-chip-boom-sparks-bt-substrate-materials-shortage-tsmcs-huge-demand-causes-supply-disruptions-for-nand-flash-controllers-ssds)\]

BYD is selling more EVs than Tesla is in Europe \[[TechNode](https://technode.com/2025/05/26/byd-surpasses-tesla-in-europe-ev-sales-for-the-first-time-jato/)\]

Musk takes a shot at Trump, says he is “disappointed” by spending bill \[[CBS](https://www.cbsnews.com/news/elon-musk-disappointed-by-trump-big-beautiful-bill-doge/)\]

Sergey Brin is bringing back zeppelins \[[IEEE](https://spectrum.ieee.org/lta-research-airship)\]

## Number of The Week

> 73%

Growth for Nvidia’s data center business, according to [their Wednesday earnings report](https://www.cnbc.com/2025/05/28/nvidia-nvda-earnings-report-q1-2026.html).

**Quote of The Week**

> “It's going to get to the point where we all have to have safe words, and you and I get on a Zoom and we have to have our secret pre-shared key.”

— Abnormal AI CIO Mike Britton told [Axios of AI](https://www.axios.com/2025/05/27/chatgpt-phishing-emails-scam-fraud) enhanced phishing emails.

## This Week On Big Technology Podcast: She Wants AI To Help You Thrive, Not Just Keep You Company — Y-Lan Boureau

![](https://www.bigtechnology.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/1707c8fe-0417-44b9-9562-11327dc31f4b_1600x1600.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1456,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

Y-Lan Boureau is the founder & CEO of ThrivePal, an OpenAI-funded AI startup, and a former Meta AI researcher. Boureau joins Big Technology Podcast to discuss why the next frontier for AI should be science‑backed coaching that nudges us toward healthier habits and deeper real‑world relationships. Tune in to hear how large‑language models can push users to lift weights, regulate emotions, and support their friends’ growth.

You can listen on [Apple Podcasts](https://apple.co/3AebxCK), [Spotify](https://spoti.fi/32aZGZx), or your [podcast app of choice](https://pod.link/1522960417/%C2%A0)

**Thanks again for reading.** Please share Big Technology if you like it!

**And hit that Like Button** to channel that well-liked traveler side of your personality

**My book Always Day One** digs into the tech giants’ inner workings, focusing on automation and culture. I’d be thrilled if you’d give it a read. [You can find it here](https://www.amazon.com/Always-Day-One-Titans-Forever-ebook/dp/B07V65YKZT/).

Questions? News tips? Email me by responding to this email, or by writing [alex@bigtechnology.com](https://www.bigtechnology.com/p/) Or find me on Signal at 516-695-8680

## Join Big Technology’s Discord Server

We’re talking about AI and the latest tech news every day in Big Technology private Discord server. It’s open to our paid subscribers and you can hop in here: