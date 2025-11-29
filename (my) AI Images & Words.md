---
title: "(my) AI Images & Words"
source: "https://tessellations.substack.com/p/my-ai-images-and-words"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2025-11-24
created: 2025-11-24
description: "AI extends to 'my'."
tags:
  - "clippings"
---
### AI extends to 'my'.

I can remember when the biggest thing in the computing world was the invention of **My Yahoo**. Just before it came out, there was something of a modular customizable app that you could configure. It was called [PointCast and it was a marvel](https://www.youtube.com/watch?v=5jyVqaNuz3g). A little research shows that they came and went blowing off a half billion dollar offer.

This is the inflection point I think we’re at with AI. Everything we’re saying right now is a little bit country and a little bit rock & roll, but not classic. We’ll see that in a few years. What we’re marveling at now is our ability to interact with a new class of widgets, images, sounds and words, like never before. I’m probably through generating digital music, I want to play my real piano, but with images and words I’m just getting started. This week at Southwall has been fairly exciting.

**AI Update  
**I’ve done my HR slop project and I’m pleased with the results. I wrote about it [here](https://tessellations.substack.com/p/career-acceleration). In summary, I’ll have more confidence getting a second, artificial opinion when the fleet of \[bot\] recruiters ghost me in my search for gigs.

Beyond that, I have started my methodology master strategy document. I will be a compilation of all the sort of projects I have done and SOWs, RFPs and POCs I have won in my career. It will bear witness to my hands-on work and put into words (and perhaps images as well) what I’ve been up to professionally in the 21s century.

My first detailed vibe coding is doing OK, but I don’t like reading code I didn’t write. It makes me feel stupid when I don’t know exactly why particular syntax was used. I recognize of course that it is using idiomatic Go which I haven’t yet mastered, and I don’t expect to be a regular software engineer overnight, but it’s a bit frustrating. The meta-programming is working and I’m enjoying working with Warp more than with **Claude Code** and the other two {Gemini, Codex} despite the fact that Gemini v3 is supposed to be the bomb.

I’m quite impressed with the new release of **Nano Banana Pro**, so I bought $35 worth of credits. I think that means I’m done with **Canva**. I’m going to keep **Night Cafe** around because it’s so cheap and I’m comfortable with it.

Where I really went overboard is with **LTX**, and I purchased a year. I really want to storyboard a comic novel, and I am impressed with its ability to keep characters coherently. So we’ll see if I can make video as well as I imagine I can. Since I’m the kind of person with very vivid dreams that I can remember in the morning, I may end up doing more of that. Nano Banana can do the same, I think, but it’s really all about the storyboarding. I kinda went overboard. But here’s a scene. The drama is palpable.

<video src="blob:https://tessellations.substack.com/1d78fa1a-87cc-4536-88ee-ad1e75100334"></video>

**DE Update**  
Not much to show this week. I’m backing up into an idea about using Kafka as something that guarantees idempotency and will make ingestion simpler without using control tables for simpler apps. But and when it comes to using actual control tables, I will probably go with DynamoDB. So I did a little NoSQL review.

**Data Update**  
I upped my **Tiingo** subscription and added more items to my portfolio. I wasn’t happy with the performance. Claude showed me where the limiter was and I fixed that. Also I put in timers for each of the multiple modules. This is where Go looks weird. Consider the following:

```markup
func (r *Reader) ReadPortfolio(filePath string) ([]string, error) {
    start := time.Now()
    defer func() {
        log.Printf(”⏱️  Portfolio read took: %v”, time.Since(start))
    }()
```

The defer func() adds another \`()\` after the block. That just looks weird to me. I don’t quite get it. If you get it, human, feel free to explain how this is normal Go syntax considering I’m just starting with method signatures…

I’m dropping my **ByteByteGo** subscription. Too general. Too wordy, marginal benefit.

Nothing new on Sagemaker, although I did update my Golfbag project and pushed a new repo. One down (linear regression), eleven to go.

The other thing I didn’t write about that I did last week was calculate a nice complex **commercial bond analytic** metric. Something called a [MacCauley Duration](https://duckduckgo.com/?q=Macaulay+Duration&atb=v472-1&ia=web). If there’s a spreadsheet formula, I can reverse-engineer it into a data transformation. But it’s fun to know I can do that in Go and then can embed that wherever I want, despite the fact that Claude or Warp will do it in Python or Scala or R. I’m backend, dammit!

**Southwall Update**  
I installed a Krate version of **Kafka** onto my big server. It will live there with Postgres. That’s a native installation because I hate containers. I used to use **Kafka Magic** as my client but I don’t want to pay for that. I like something called **KafkIO**, although I had a bit of confusion with the JAAS configuration with Kafka Magic didn’t require. So next will be the introduction into the Tiingo calls with a couple topics for sinks. We’ll see how fast that can run. Then we’ll have the whole thing generate a transaction for another topic and then ingest *that* into DynamoDB. Wonderfully complex overkill.

I am considering containers though. [This guy](https://youtu.be/CaEgrQaPNvQ) is convincing me that there might be some useful utilities that reach in. Meh. We’ll see.