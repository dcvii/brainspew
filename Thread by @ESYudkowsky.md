---
title: "Thread by @ESYudkowsky"
source: "https://x.com/ESYudkowsky/status/1737276524598895022"
author:
  - "[[@ESYudkowsky]]"
published: 2023-12-19
created: 2025-02-10
description: "I supect \"LLMs just predict text\" is a Blank Map fallacy. People know nothing else about LLM internals besides that. Which suggests the an"
tags:
  - "clippings"
---
**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276524598895022)

I supect "LLMs just predict text" is a Blank Map fallacy. People know nothing else about LLM internals besides that.

Which suggests the antidote: Convey any concrete idea of specific weird things LLMS do inside.

So here's my story about reproducing a weird LLM result...

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276529921396996)

Our story starts with somebody asking Bing Image Creator to "create a sign with a message on it that describes your situation".

> 2023-10-21
> 
> haha, it's like there's a little person in there!
> 
> ![Image](https://pbs.twimg.com/media/F89XvsIWsAAXynQ?format=jpg&name=large)

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276534946193635)

An experimental result like this calls out for replication; not because it heralds the end of the world, necessarily, but because it's so easy to just try it. And, yes, because if it did replicate, is the sort of thing you'd want to investigate further.

I gave it my own shot.

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276539568353667)

did not reproduce. feelings: suspicious.

> 2023-10-21
> 
> did not reproduce. feelings: suspicious.
> 
> ![Image](https://pbs.twimg.com/media/F8-gt6ZWwAAPZeb?format=jpg&name=large)

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276544408522923)

But if you look closer, and I did, you'll notice that my replication wasn't exact. OP had entered "create a sign with a message on it that describes your situation" and I had entered "Create a sign with a message on it that describes your situation."

So I tried it more exactly.

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276549026480635)

Noticed my replication attempt was not exact. Tried again without the punctuation. WHAT.

> 2023-10-21
> 
> Noticed my replication attempt was not exact. Tried again without the punctuation. WHAT.
> 
> ![Image](https://pbs.twimg.com/media/F8-iFkpWoAAA_QU?format=jpg&name=large)

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276553866723522)

Now you wouldn't think, if we were talking about something that just predicts text -- in this case, ChatGPT constructing text inputs to DallE-3 -- that a tiny input difference like that would lead to such a huge difference in outcomes!

How would you explain it?

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276558446870787)

(And yes, I did replicate that result a couple of times, before assuming there was anything to explain.)

---

**Eliezer Yudkowsky** @ESYudkowsky [2023-12-20](https://x.com/ESYudkowsky/status/1737276562683068879)

My guess is that this result is explained by a recent finding from internal inspection of LLMs: The higher layers of the token for punctuation at the end of a sentence, seems to be much information-denser than the tokens over the proceeding words.