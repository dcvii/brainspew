---
title: "Claude Code for writers"
source: "https://www.platformer.news/claude-code-for-writers-tips-ideas/?ref=platformer-newsletter"
author:
  - "[[Casey Newton]]"
published: 2026-01-15
created: 2026-01-20
description: "Five useful things I’ve built so far. Plus: Grok caves, and Thinking Machines implodes"
tags:
  - "clippings"
---
*This is a column about Claude Code. My boyfriend works at Anthropic. See* [*my full ethics disclosure here*](https://www.platformer.news/ethics/)*.*

Three years ago this month, the prominent AI researcher and commentator Andrej Karpathy declared that “ [the hottest new programming language is English](https://x.com/karpathy/status/1617979122625712128?ref=platformer.news).” At the time, ChatGPT was less than two months old, and millions of people were discovering that natural language could now be used to generate code. GPT-3.5 had demonstrated that large language models could follow complex instructions with increasing reliability. Karpathy’s tweet predicted a world where knowledge of a programming language would no longer be required to program.

At the time, I remember a CEO friend of mine gently scoffing at the idea of English as a programming language. As the leader of an engineering team, he spent all day “programming” in English: giving projects to his engineers and telling them what to build. The method was less reliable than you might expect, he told me. In the eternal quest to build digital products by describing them in words, something almost always gets lost in translation.

Over the next three years, the CEO’s experience matched my own. English is the only language in which I am fluent, and for the most part it made for a poor programming language. Unable to write anything more complicated than HTML, I found that the advent of vibe coding (another Karpathy coinage) largely passed me by. After every major new model release, I would dutifully ask it to build me some basic but ultimately useless piece of software. Programming remained something other people did.

As I noted last week, [the release of Claude Opus 4.5 in Claude Code changed that](https://www.platformer.news/claude-code-review-web-design/). In just about an hour of typing into a box — of programming in English, as Karpathy put it — I made a personal website that far surpassed anything I had been able to put together in Squarespace. Like my CEO friend’s engineers, Claude regularly made strange choices and outright errors that I would have to correct. Without too much effort, though, I was able to get the site that I asked for — as well as several features I never would have thought to build had Claude not suggested them.

In the week since, amid a general craze for Claude Code, I have let my imagination run wild. In just a few days, I built a series of tools I expect to return to over and over again to help me in my work. As with my website, I don’t understand the underlying code at all. But for the moment, anyway, I’m not certain it matters.

ChatGPT was [the moment when people woke up](https://www.platformer.news/the-promise-and-the-peril-of-chatgpt/) to the power of LLMs to generate text. The Claude Code moment, while orders of magnitude smaller, strikes me as potentially just as significant. It's waking people up to LLMs' power to generate *tools*. And I suspect the consequences of this strange new ability will reverberate over the next several years.

In the spirit of showing rather than telling, today I wanted to share a few of the things I’ve built for myself as a writer. Some are tools I’ve wanted for years. Others were suggested by Claude itself. All are things that I would not have been able to create before a few months ago.

A couple caveats up top. One is that I’m not interested in AI tools that do the writing for me. I occasionally experiment with trying to get models to write in my voice, for the same reason you might check the area surrounding your tent for grizzly bears before camping for the night. But I’m almost always more interested in tools that improve my thinking, rather than substitute for it.

That’s why you’ll note that a common thread running through these tools is that they help me make sense of things. To cover technology is to be at the center of a sprawling collection of characters, events, narratives, and history. Tools that help me capture and organize them are invaluable to me.

Second, given my [conflict of interest](https://www.platformer.news/ethics/), I realize today’s edition may come across as wide-eyed Claude-glazing. Should that be a concern, I encourage you to swap out Claude for [OpenAI’s similar Codex](https://openai.com/codex/?ref=platformer.news) or [Google’s Antigravity](https://antigravity.google/?ref=platformer.news), both of which should be capable of building software of similar quality. My goal here is not to persuade you to use any particular framework to tackle your project; it’s simply to suggest what is newly possible.

If nothing else, Claude Code fulfills a desperate need that every writer has at one time or another: to procrastinate. So, with that said, here are some things writers can build with the tools now available — along with some notes on the obstacles I still find myself running into.

---

**Build a website**. While I covered this last week, it’s worth saying that I think a website is the ideal place to start after downloading Claude Code. Every writer can benefit from having a website, and you probably already have a few things in mind for what might belong there. (If you don’t, ask Claude for some ideas.)

Building a website with Claude Code will help familiarize you with the basic rhythms of this work. Type what you want into the box; Claude either goes forth and does it or asks follow-up questions to help you refine your idea. Look at the resulting product, then tell Claude what you want it to change.

The best part about this project is that you don’t even have to publish the site Claude makes for you — you can just spend an hour or so building something locally and tweaking it to your liking.

If you *do* like what you build, you can publish your site more cheaply than you would on Squarespace using a service like [Netlify](https://www.netlify.com/?ref=platformer.news) (which I’m using at the moment) or [GitHub Pages](https://docs.github.com/en/pages?ref=platformer.news). As a bonus, you can integrate a simple blog onto your site. I used [micro.blog](https://micro.blog/?ref=platformer.news).

**Where Claude falls short:** If you’re working on local files, Claude moves very quickly. If it has to debug anything in your browser, though, it will go *much* more slowly, and ask for permission at every step of the way. I implemented a simple website in about an hour; the blog, which involved lots of Code poking around in various online services in Chrome tabs, was a half-day project. There was probably a faster way to do it, and I’ll never know what it is!

---

**Build a searchable database of your own work.** I’ve always wanted a database of my writing that I could run semantic queries on. Stuff like: “When was the last time I wrote a column about Grok?” Or, “what criticisms have people made of the Meta Oversight Board?” It is possible to get answers to these questions via Google. But I’ve always wanted answers grounded in my own work, with quick links to the relevant materials.

After describing this idea to Claude, it went to work. It exported 818 editions of **Platformer** into a folder of text files organized by date, and then connected it to Claude. Now when I ask Claude questions about my archive, it reads through relevant posts and gives me an answer. I have wanted something like this for nearly half a decade now, and Claude built it in less than half an hour.