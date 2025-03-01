---
title: The most underreported and important story in AI right now is that pure scaling has failed to produce AGI
source: https://fortune.com/2025/02/19/generative-ai-scaling-agi-deep-learning/
author:
  - "[[Gary Marcus]]"
published: 2025-02-19
created: 2025-02-20
description: Grok 3’s somewhat underwhelming performance should be a wake-up call.
tags:
  - artificial_intelligence
---
Virtually all of the generative AI industry has been built on this presumption; projects like the OpenAI/Oracle/Softbank joint venture [Stargate](https://en.wikipedia.org/wiki/Stargate_LLC), allegedly another half trillion dollars, are also largely based on this premise.

As one [commentary](https://subcriticalappraisal.com/2022/AGI-Scale-Is-All-You-Need/) put it, the idea behind the scaling hypothesis was that “the blessing of scale suggests that merely throwing more computing power into training Al models will produce machine superintelligence that can beat any human and the entire human civilisation at *all cognitive tasks.”* Elon Musk’s projection, made last year, that “[we’ll have AI that is smarter than any one human](https://arstechnica.com/information-technology/2024/04/elon-musk-ai-will-be-smarter-than-any-human-around-the-end-of-next-year/) probably around the end of next year” \[by which he meant the end of 2025\] seemed to flow from the same premise.

Much of the enthusiasm for scaling originated with a 2020 paper from OpenAI called “[Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361#openai),” which claimed to establish that “simple equations governed performance” and that there was a “power-law with model size, dataset size, and the amount of compute used for training, with some trends spanning more than seven orders of magnitude.”

For a while that even seemed to be true.

§

But I always knew it couldn’t last forever. When I said as much, the field was absolutely furious at me.

I first aired my concern in March 2022, in an article called “Deep learning is hitting a wall.”  Central to that piece were these two paragraphs:

*There are serious holes in the scaling argument. To begin with, the measures that have scaled have not captured what we desperately need to improve: genuine comprehension. Insiders have long known that one of the biggest problems in AI research is the tests (“**benchmarks**”) that we use to evaluate AI systems. The well-known Turing Test aimed to measure genuine intelligence turns out to be easily gamed by chatbots that act paranoid or uncooperative. Scaling the measures Kaplan and his OpenAI colleagues looked at—about predicting words in a sentence—is not tantamount to the kind of deep comprehension true AI would require.*

*What’s more, the so-called scaling laws aren’t universal laws like gravity but rather mere observations that might not hold forever, much like Moore’s Law, a trend in computer chip production that held for decades but arguably began to slow a decade ago.*

Almost the entire elite of deep learning fought back, vociferously. Sam Altman, Greg Brockman, Elon Musk, Yann LeCun, and many more [went so far as to publicly ridicule me](https://garymarcus.substack.com/p/satya-nadella-and-the-three-stages). “Not only is AI not ‘hitting a wall’, cars with AI-powered driving assistance aren’t hitting walls, or anything else either,” wrote Meta’s AI chief Yann LeCun. “Give me the confidence of a mediocre deep learning skeptic,” wrote OpenAI CEO Sam Altman. Even as recently as June 2024 Musk circulated a meme mocking the idea that scaling deep learning would hit a wall.

Indeed, as recently as last May, the scaling idea was still being championed, loud and strong, as in this screenshot from a talk by [Microsoft](https://fortune.com/company/microsoft/) CTO Kevin Scott:

![](https://fortune.com/img-assets/wp-content/uploads/2025/02/kevin-scott-microsoft.jpeg?w=1440&q=75)

But the whale still hasn’t come, and times have quietly changed—significantly—in recent months. Groupthink isn’t always correct.

§

The first signs that the pure scaling of data and compute might in fact be hitting a wall came from industry leaks from people like famed investor Marc Andreessen, who said in early November 2024 that current models are “[sort of hitting the same ceiling on capabilities](https://observer.com/2024/11/vc-andreessen-horowitz-ai-models-hitting-wall/).” Then, in December, Microsoft CEO Satya Nadella echoed many of my 2022 themes, saying at a Microsoft Ignite [event](https://www.youtube.com/watch?v=3YiB2OvK6sY), “in the last multiple weeks there is a lot of debate on have we hit the wall with scaling laws. Is it gonna continue? Again, the thing to remember at the end of the day these are not physical laws. There are just empirical observations that hold true just like Moore’s Law did for a long period of time and so therefore it’s actually good to have some skepticism some debate.”

In the last few days, several more cracks in the scaling edifice started to show. Starting with some smaller and moving to the largest:

- Heavy AI booster [Klarna did an about-face from its all in on AI stance](https://x.com/gergelyorosz/status/1892196257608687842?s=61). They assumed scaling would make things work, and seem to have changed their mind.
- [Humane AI Pin was canceled](https://trib.al/2LsxJX8) and the company sold for parts. The founders were forced to retreat from their glorious TED Talk [vision of new AI-driven gadgets](https://www.ted.com/talks/imran_chaudhri_the_disappearing_computer_and_a_world_where_you_can_take_ai_everywhere) to working far more modestly, for [HP](https://fortune.com/company/hp/), to “[integrate artificial intelligence into](https://www.bloomberg.com/news/articles/2025-02-18/hp-116-million-deal-for-humane-includes-ip-but-no-ai-pin-device) the company’s personal computers, printers and connected conference rooms.”
- OpenAI [implicitly acknowledged that they don’t yet have GPT-5](https://garymarcus.substack.com/p/breaking-openais-efforts-at-pure?r=8tdk6), and would not get there purely by building massive clusters and gathering more training data.
- Mathematician Daniel Litt [exposed massive hallucinations in OpenAI’s Deep Research](https://x.com/littmath/status/1891868756340547809?s=61). (I independently pointed out similar issues in [Grok 3 Deep Search](https://open.substack.com/pub/garymarcus/p/grok-3-beta-in-shambles?r=8tdk6&utm_campaign=post&utm_medium=web&showWelcomeOnShare=false) last night.)
- Finally, and perhaps most significantly: Elon Musk said over that weekend that Grok 3, with 15x the compute of Grok 2, and immense energy (and construction and chop) bills, would be “the smartest AI on the earth.” Yet the world quickly saw that Grok 3 is still afflicted by the kind of unreliability that has hobbled earlier models. The famous ML expert Andrej Karpathy reported that Grok 3 [occasionally stumbles on basics like math and spelling](https://x.com/karpathy/status/1891720635363254772?s=61). In my own experiments, I quickly [found a wide array of errors](https://garymarcus.substack.com/p/grok-3-beta-in-shambles?r=8tdk6&utm_campaign=post&utm_medium=web&triedRedirect=true), such as hallucinations (e.g, it told me with certainty that there was a significant 5.6-sized earthquake on Feb. 10 in Billings, Montana, when no such thing had happened) and extremely poor visual comprehension (e.g. it could not properly label the basic parts of a bicycle).

§

Nadella, in his December speech, pointed to test-time compute, in which systems are allowed extra time for “reasoning” as the next big thing, and to some degree he is right; it is the next big thing, a new thing to try to scale, since merely scaling compute and data is no longer bringing the massive returns it once did. At least for a while, adding more and more computing time will help, at least on some kinds of problems.

But test-time compute is probably not enough to rescue the rickety enterprise of generative AI, and one can already see multiple signs of this.

- First, everybody who is doing test-time-compute is demoing the same kinds of benchmarks, for math and coding. This is likely because in those particular domains, it is possible to generate massive amounts of verified data. That’s fine for those domains, but unlikely to work well in the face of the complexities of the open-ended real world.
- Hallucinations still plague even the newest systems, as the examples from Daniel Litt and myself (which were both generated by test-time-compute systems) make clear.
- Finally, although DeepSeek lowered the costs of training these new systems, they are still expensive to operate, which is why companies like OpenAI are limiting their usage. When customers begin to realize that even with the greater expenses, errors still seep in, they are likely to be disappointed. One irate customer cc:d me yesterday on a several page demand for a refund, writing in part that “GPT-4o Pro \[which includes access to test time compute\] has consistently underperformed,” and enumerated problems such as “Severely degraded memory” and “Hallucinations and Unreliable Answers.”

§

The fact is, pure scaling has not worked. I am not alone in thinking this; the illustrious Stanford Natural Language Processing group [reached a similar conclusion](https://x.com/stanfordnlp/status/1889768783834976431?s=61), reading between the lines of OpenAI’s recent announcement in the same way I did. In their words, Altman’s recent OpenAI roadmap was “the final admission that the 2023 strategy of OpenAI, Anthropic, etc. ‘“simply scaling up model size, data, compute, and dollars spent will get us to AGI/ASI’) is no longer working!”

In short, half a trillion dollars have been invested in a misguided premise; a great deal more funding seems to be headed in the same direction for now.

Unfortunately, none of this looks to be sustainable. Most of the money has been invested on the premise that one of these companies would reach artificial general intelligence, which seems (at least in the near term) increasingly unlikely. Yet virtually all of them, from American companies like OpenAI, Grok, and Anthropic to Chinese companies like DeepSeek and ByteDance, are following essentially the same playbook, making mild improvements but not solving the core problems—unreliability, hallucinations, and occasionally absurd reasoning—that have plagued LLMs since the beginning. The reason we are having a price war is that everybody knows basically the same recipe, but nobody has been able to produce a true quantum leap forward.

Given the double whammy of price wars and unreliability, many AI companies will probably never make back their investments. Expect a major correction, possibly soon.

Investors and nations should continue to invest in AI, but not in more of the same. The real prize will be to investors and nations that are willing to make long-term bets in companies willing to think outside the box. Scaling may be part of the solution, but we will likely need genuinely new ideas if we are to create a reliable AI that we can trust.

*The opinions expressed in Fortune.com commentary pieces are solely the views of their authors and do not necessarily reflect the opinions and beliefs of Fortune.*