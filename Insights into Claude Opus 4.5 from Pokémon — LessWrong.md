---
title: "Insights into Claude Opus 4.5 from Pokémon — LessWrong"
source: "https://www.lesswrong.com/posts/u6Lacc7wx4yYkBQ3r/insights-into-claude-opus-4-5-from-pokemon"
author:
  - "[[Julian Bradshaw]]"
published: 2025-12-09
created: 2025-12-16
description: "Credit: Nano Banana, with some text provided.You may be surprised to learn that ClaudePlaysPokemon is still running today, and that Claude still has…"
tags:
  - "clippings"
---
![Credit: Nano Banana.](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/u6Lacc7wx4yYkBQ3r/ij8rjifoatsjhuita0aq)

Credit: Nano Banana, with some text provided.

x

Insights into Claude Opus 4.5 from Pokémon — LessWrong

[^1]: That's failures to improve by Claude Sonnet 4, Claude Opus 4, Claude Opus 4.1, and Claude Sonnet 4.5. At least in terms of story progression anyway, they have gotten faster at getting to the same story point at which they get stuck.

[^2]: There have been a few changes: support for Surf (now that Claude can get that far), removal of a bunch of tailored prompts, and a change where spinner tiles in mazes are labeled like obstructions, as well as a related change to wait for the player character to stop spinning before the screenshot of the current game state is taken. The latter two changes in particular make the Team Rocket Hideout easier than previous runs, though they don't trivialize it. See [this doc](https://docs.google.com/document/u/1/d/e/2PACX-1vRIsu2pLI21W4KjfYbN13or8E-8cvJYw570wGMEp4UQU63ZhEh9FPGgj2ark8Yk7Vyrtt9MWq3jnn4h/pub) for more details.

[^3]: For more on Pokémon agent harnesses, see [this previous LW post](https://www.lesswrong.com/posts/8aPyKyRrMAQatFSnG/research-notes-running-claude-3-7-gemini-2-5-pro-and-o3-on). But tl;dr harnesses do a lot of work to make the game understandable to an LLM, and use several techniques to address agentic weaknesses common to all LLMs. Even though the harnesses may seem fairly simple, and can (and have!) had their tools coded by the LLMs using them, game-winning harnesses have also been relentlessly optimized by human trial and error to provide exactly the support necessary to overcome current LLM limitations.

[^4]: With some editing on my part.

[^5]: Modern Gemini/GPT models can also handle this now.

[^6]: This might be considered a form of [inattentional blindness](https://en.wikipedia.org/wiki/Inattentional_blindness), the classic example of which is [the guy in a gorilla suit walking through a basketball game.](https://www.youtube.com/watch?v=UtKt8YF7dgQ&t=179s)

[^7]: Probably helps that he can't really remember enough of his experiences to get bored. That may be what we all do in the posthuman future, though on a longer timescale.

[^8]: 9000 of those spent stuck on that left arrow spinner issue.

[^9]: Technically it still took Claude a few hours to notice the CUT-able trees inside the gym that block access to Erika, the gym leader, but he noticed eventually.

[^10]: The minimap only fills out as the LLM explores. Good prompting ensures that the LLM explores basically everything as a first priority, which means in practice the LLM always has a good map of the area it can understand. This bypasses a lot of vision and spatial reasoning weaknesses. Other key tools include an LLM-reasoning-powered navigator and the ability to place map markers.