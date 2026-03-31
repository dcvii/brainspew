---
title: "The Claude Code Source Leak: fake tools, frustration regexes, undercover mode, and more"
source: "https://alex000kim.com/posts/2026-03-31-claude-code-source-leak/"
author:
  - "[[Alex Kim]]"
published: 2026-03-30
created: 2026-03-31
description: "Anthropic accidentally shipped a source map in their npm package, exposing the full Claude Code source. Here's what I found inside."
tags:
  - "brain_spew"
---
I use Claude Code daily, so when [Chaofan Shou](https://x.com/Fried_rice/status/2038894956459290963) noticed earlier today that Anthropic had shipped a `.map` file alongside their Claude Code npm package, one containing the full, readable source code of the CLI tool, I immediately wanted to look inside. The package has since been pulled, but not before the code was widely mirrored, [incluiding myself](https://github.com/alex000kim/claude-code) and picked apart on [Hacker News](https://news.ycombinator.com/item?id=47584540).

This is Anthropic’s second accidental exposure in a week (the model spec leak was just days ago), and some people on Twitter are starting to wonder if someone inside is doing this on purpose. Probably not, but it’s a bad look either way. The timing is also hard to ignore: just ten days ago, Anthropic [sent legal threats to OpenCode](https://github.com/anomalyco/opencode/pull/18186), forcing them to remove built-in Claude authentication because third-party tools were using Claude Code’s internal APIs to access Opus at subscription rates instead of pay-per-token pricing. That [whole saga](https://news.ycombinator.com/item?id=47444748) makes some of the findings below more pointed.

So I spent my morning reading through the HN comments and leaked source. Here’s what I found, roughly ordered by how “spicy” I thought it was.

## Anti-distillation: injecting fake tools to poison copycats

In [`claude.ts` (line 301-313)](https://github.com/alex000kim/claude-code/blob/main/src/services/api/claude.ts#L301-L313), there’s a flag called `ANTI_DISTILLATION_CC`. When enabled, Claude Code sends `anti_distillation: ['fake_tools']` in its API requests. This tells the server to silently inject decoy tool definitions into the system prompt.

The idea: if someone is recording Claude Code’s API traffic to train a competing model, the fake tools pollute that training data. It’s gated behind a GrowthBook feature flag (`tengu_anti_distill_fake_tool_injection`) and only active for first-party CLI sessions.

This was one of the first things people noticed in the HN thread. Whether you see this as smart defensive engineering or anti-competitive behavior probably depends on which side of the distillation debate you’re on.

There’s also a second anti-distillation mechanism in [`betas.ts` (lines 279-298)](https://github.com/alex000kim/claude-code/blob/main/src/utils/betas.ts#L279-L298): server-side connector-text summarization. When enabled, the API buffers the assistant’s text between tool calls, summarizes it, and returns the summary with a cryptographic signature. On subsequent turns, the original text can be restored from the signature. If you’re recording API traffic, you only get the summaries, not the full reasoning chain.

How hard would it be to work around these? Not very. Looking at the activation logic in [`claude.ts`](https://github.com/alex000kim/claude-code/blob/main/src/services/api/claude.ts#L301-L313), the fake tools injection requires all four conditions to be true: the `ANTI_DISTILLATION_CC` compile-time flag, the `cli` entrypoint, a first-party API provider, and the `tengu_anti_distill_fake_tool_injection` GrowthBook flag returning true. A MITM proxy that strips the `anti_distillation` field from request bodies before they reach the API would bypass it entirely, since the injection is server-side and opt-in. The [`shouldIncludeFirstPartyOnlyBetas()`](https://github.com/alex000kim/claude-code/blob/main/src/utils/betas.ts#L215-L220) function also checks for `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS`, so setting that env var to a truthy value disables the whole thing. And if you’re using a third-party API provider or the SDK entrypoint instead of the CLI, the check never fires at all. The connector-text summarization is even more narrowly scoped: it’s Anthropic-internal-only (`USER_TYPE === 'ant'`), so external users won’t encounter it regardless.

Anyone serious about distilling from Claude Code traffic would find the workarounds in about an hour of reading the source. The real protection is probably legal, not technical.

## Undercover mode: AI that hides it’s AI

The file [`undercover.ts`](https://github.com/alex000kim/claude-code/blob/main/src/utils/undercover.ts) (about 90 lines) implements a mode that strips all traces of Anthropic internals when Claude Code is used in non-internal repos. It instructs the model to never mention internal codenames like “Capybara” or “Tengu,” internal Slack channels, repo names, or the phrase “Claude Code” itself.

The interesting part is [line 15](https://github.com/alex000kim/claude-code/blob/main/src/utils/undercover.ts#L15):

> “There is NO force-OFF. This guards against model codename leaks.”

You can force it ON with `CLAUDE_CODE_UNDERCOVER=1`, but there’s no way to force it off. In external builds, the entire function gets dead-code-eliminated to trivial returns. This is a one-way door.

The obvious concern, raised repeatedly in the HN thread: this means AI-authored commits and PRs from Anthropic employees in open source projects will have no indication that an AI wrote them. It’s one thing to hide internal codenames. It’s another to have the AI actively pretend to be human.

## Frustration detection via regex (yes, regex)

[`userPromptKeywords.ts`](https://github.com/alex000kim/claude-code/blob/main/src/utils/userPromptKeywords.ts#L7-L8) contains a regex pattern that detects user frustration:

```
/\b(wtf|wth|ffs|omfg|shit(ty|tiest)?|dumbass|horrible|awful|
piss(ed|ing)? off|piece of (shit|crap|junk)|what the (fuck|hell)|
fucking? (broken|useless|terrible|awful|horrible)|fuck you|
screw (this|you)|so frustrating|this sucks|damn it)\b/
copy
```

This was the most-discussed finding in the HN thread. The general reaction: an LLM company using regexes for sentiment analysis is peak irony.

Is it ironic? Sure. Is it also probably faster and cheaper than running an LLM inference just to figure out if a user is swearing at the tool? Also yes. Sometimes a regex is the right tool.

## Native client attestation below the JS runtime

In [`system.ts` (lines 59-95)](https://github.com/alex000kim/claude-code/blob/main/src/constants/system.ts#L59-L95), API requests include a `cch=00000` placeholder. Before the request leaves the process, Bun’s native HTTP stack (written in Zig) overwrites those five zeros with a computed hash. The server then validates the hash to confirm the request came from a real Claude Code binary, not a spoofed client.

They use a placeholder of the same length so the replacement doesn’t change the Content-Length header or require buffer reallocation. The computation happens below the JavaScript runtime, so it’s invisible to anything running in the JS layer. It’s basically DRM for API calls, implemented at the HTTP transport level.

This is the technical enforcement behind the OpenCode legal fight. Anthropic doesn’t just ask third-party tools not to use their APIs; the binary itself cryptographically proves it’s the real Claude Code client. If you’re wondering why the OpenCode community had to resort to [session-stitching hacks](https://github.com/anomalyco/opencode/pull/18186) and auth plugins after Anthropic’s legal notice, this is why.

That said, the attestation isn’t airtight. The whole mechanism is gated behind a compile-time feature flag (`NATIVE_CLIENT_ATTESTATION`), and the `cch=00000` placeholder only gets injected into the `x-anthropic-billing-header` when that flag is on. The header itself can be disabled entirely by setting `CLAUDE_CODE_ATTRIBUTION_HEADER` to a falsy value, or remotely via a GrowthBook killswitch (`tengu_attribution_header`). The Zig-level hash replacement also only works inside the official Bun binary. If you rebuilt the JS bundle and ran it on stock Bun (or Node), the placeholder would survive as-is, five literal zeros hitting the server. Whether the server rejects that outright or just logs it is an open question, but the code comment references a server-side `_parse_cc_header` function that “tolerates unknown extra fields,” which suggests the validation might be more forgiving than you’d expect for a DRM-like system. None of this is a push-button bypass, but it’s not the kind of thing that would stop a determined third-party client for long.

## 250,000 wasted API calls per day

The source comment in [`autoCompact.ts` (lines 68-70)](https://github.com/alex000kim/claude-code/blob/main/src/services/compact/autoCompact.ts#L68-L70) tells the whole story:

> “BQ 2026-03-10: 1,279 sessions had 50+ consecutive failures (up to 3,272) in a single session, wasting ~250K API calls/day globally.”

The fix? `MAX_CONSECUTIVE_AUTOCOMPACT_FAILURES = 3`. After 3 consecutive failures, compaction is disabled for the rest of the session. Three lines of code to stop burning a quarter million API calls a day. Engineers love data-driven fixes with receipts, and here the receipt is right there in the source comment.

## KAIROS: the unreleased autonomous agent mode

Throughout the codebase, there are references to a feature-gated mode called `KAIROS`. Based on the code paths in [`main.tsx`](https://github.com/alex000kim/claude-code/blob/main/src/main.tsx), it looks like an unreleased autonomous agent mode that includes:

- A `/dream` skill for “nightly memory distillation”
- Daily append-only logs
- GitHub webhook subscriptions
- Background daemon workers
- Cron-scheduled refresh every 5 minutes

Several people in the HN thread flagged this as the biggest product roadmap reveal from the leak, more damaging than the code itself.

The core implementation is heavily gated, so it’s hard to say how far along it is. But the scaffolding for an always-on, background-running agent is clearly there.

## Other notable bits

Tomorrow is April 1st, and the source contains what’s almost certainly this year’s April Fools’ joke: [`buddy/companion.ts`](https://github.com/alex000kim/claude-code/blob/main/src/buddy/companion.ts) implements a Tamagotchi-style companion system. Every user gets a deterministic creature (18 species, rarity tiers from common to legendary, 1% shiny chance, RPG stats like DEBUGGING and SNARK) generated from their user ID via a Mulberry32 PRNG. Species names are encoded with `String.fromCharCode()` to dodge build-system grep checks.

The terminal rendering in [`ink/screen.ts`](https://github.com/alex000kim/claude-code/blob/main/src/ink/screen.ts) and [`ink/optimizer.ts`](https://github.com/alex000kim/claude-code/blob/main/src/ink/optimizer.ts) borrows game-engine techniques: an `Int32Array` -backed ASCII char pool, bitmask-encoded style metadata, a patch optimizer that merges cursor moves and cancels hide/show pairs, and a self-evicting line-width cache (the source claims “~50x reduction in stringWidth calls during token streaming”). Over-engineering? Maybe. But when you’re streaming tokens one at a time, terminal rendering performance actually matters.

Every bash command runs through 23 numbered security checks in [`bashSecurity.ts`](https://github.com/alex000kim/claude-code/blob/main/src/tools/BashTool/bashSecurity.ts), including 18 blocked Zsh builtins, defense against Zsh equals expansion (`=curl` bypassing permission checks for `curl`), unicode zero-width space injection, IFS null-byte injection, and a malformed token bypass found during HackerOne review. Having a specific Zsh threat model is genuinely novel; most tools just block the obvious stuff.

Prompt cache economics drive a lot of architectural decisions. There are 14 tracked cache-break vectors in [`promptCacheBreakDetection.ts`](https://github.com/alex000kim/claude-code/blob/main/src/services/api/promptCacheBreakDetection.ts) and multiple “sticky latches” that prevent mode toggles from busting the prompt cache. One function is annotated `DANGEROUS_uncachedSystemPromptSection()` to warn developers about adding cache-volatile content. When you’re paying for every token, cache invalidation stops being a computer science joke and becomes an accounting problem.

The multi-agent coordinator mode in [`coordinatorMode.ts`](https://github.com/alex000kim/claude-code/blob/main/src/coordinator/coordinatorMode.ts) is also worth a look. The whole orchestration algorithm is a prompt, not code. It teaches workflow discipline through system prompt instructions like “Do not rubber-stamp weak work” and “You must understand findings before directing follow-up work. Never hand off understanding to another worker.”

And the codebase has some rough spots. `print.ts` is 5,594 lines long with a single function spanning 3,167 lines and 12 levels of nesting. Claude Code also uses Axios for HTTP. And in a bit of timing that borders on comedic, [Axios was just compromised on npm](https://news.ycombinator.com/item?id=47582220) with malicious versions dropping a remote access trojan. Not exactly the “AI will replace all programmers” data points that Anthropic’s marketing team would prefer.

## So what?

Some in the HN thread downplayed the leak, pointing out that Google’s Gemini CLI and OpenAI’s Codex are already open source. That’s true, but what those companies open-sourced is their agent SDK (a toolkit), not the full internal wiring of their flagship product.

The real damage for Anthropic here isn’t the code itself. It’s the feature flags. KAIROS, the anti-distillation mechanisms: these are product roadmap details that competitors can now see and react to. The code can be refactored. The strategic surprise can’t be un-leaked.

There’s also a twist worth noting: Anthropic [acquired Bun](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone) at the end of last year, and Claude Code is built on top of it. A Bun bug ([oven-sh/bun#28001](https://github.com/oven-sh/bun/issues/28001)), filed on March 11, reports that source maps are served in production mode even though Bun’s own docs say they should be disabled. The issue is still open. People in the comments are now asking whether this is what caused the leak. If so, Anthropic’s own toolchain shipped a known bug that exposed their own product’s source code.

As one Twitter reply put it: “accidentally shipping your source map to npm is the kind of mistake that sounds impossible until you remember that a significant portion of the codebase was probably written by the AI you are shipping.”