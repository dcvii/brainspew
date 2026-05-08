---
title: "How I built the core loop of a browser multiplayer game"
source: "https://packagemain.tech/p/how-i-built-the-core-loop-of-a-browser?publication_id=2652085&post_id=196777927&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Julien Singler]]"
published: 2026-05-08
created: 2026-05-08
description: "Why an async, queued action loop can still feel as immediate as a real-time game — and what it took to get there"
tags:
  - "brain_spew"
---
### Why an async, queued action loop can still feel as immediate as a real-time game — and what it took to get there

I’m kicking off a series about [HiddenWars](https://hiddenwars.io/), a personal project I’ve been building with Golang and Svelte. It’s a persistent browser-based hacking game with mostly PvE gameplay, some PvP tension, and an evolving lore where players build botnets, upgrade their systems, hack targets, and uncover secrets while pushing back against powerful mega-corporations.

![](https://substackcdn.com/image/fetch/$s_!IOPb!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5c269d58-3f59-4d32-8bbd-ea9d69bb9aa0_1860x854.png)

## Introduction

Every game has a core loop. In a shooter it's: `see → aim → shoot → reload. `In an idle game it’s:`  click → earn → upgrade.  `The loop is the heartbeat of the design: the smaller it is and the better it feels, the more the rest of the game can hang off it.

For a browser-based multiplayer game, the core loop is harder than it looks. Browsers are not a great real-time runtime. Players come and go. Tabs sleep. WebSocket disconnect on Wi-Fi handovers. You cannot rely on every player being online at the same time, and you definitely cannot rely on a 60Hz tick.

So you have two choices: pretend the browser is a real-time engine and fight it, or accept that your loop is fundamentally async and design around that.

I went with the second option. Here is what I learned.

## The problem: async is correct, but async feels bad

The honest truth about a browser multiplayer game is that almost every meaningful action is going to be asynchronous. You issue a command, the server validates it, persist it, and tells you when it’s done. That round trip takes milliseconds at best, seconds at worst and minutes if the action is long-running (a build, a job, a timer).

If you naively render that flow, it feels terrible. You click a button. Nothing happens. A spinner appears. Two seconds later, a toast sys “Success”. Players read this as lag, not depth.

The job of the core loop, then, is to take an unavoidably async system and make it *feel* responsive — without lying to the player about what just happened.

## The design choice: server-authoritative, locked-on-click, timer-drive

The pattern I settled on has three parts:

1. **Server is the source of truth for actions**. Every game action — scanning a target, hacking a node, queuing a build, starting a launder — is a typed command sent to a Go backend. The server validates, applies, and returns the new state. Clients never mutate game state directly.
2. **The click locks the UI immediately**. The moment the player clicks, the button enters a loading state and the action is in flight. No second click, no double-spend, no ambiguity about whether the request landed. The visible feedback is *intent acknowledged*, not *outcome predicted*.
3. 3\. **The response drives the timer.** When the server returns the new state — usually within tens of milliseconds — the client writes it to the store, the timer starts ticking from the servers’s `finishes_at`, and an `actionWatcher` is registered to refetch when the timer expires.

I deliberately did not go with optimistic UI. The temptation is real: predict the new balance, predict the queue, paint it instantly. But in a game with cooldowns, heat, race conditions between tabs, and a probabilistic resolution, optimism becomes a tax on every future change — every new rule means a new piece of client-side prediction logic that has to stay in sync with the server, or you get jitter.

Instead, I learned on the fact that the server round-trip is shot and the *long* part of every action is the timer that follows. If click-to-acknowledged latency is ~50ms, players read it as instant. What matters is that the timer starts the moment the response arrives and never lies about when the action will complete.

## The implementation: queues, timers, and a signal reactive store

![](https://substackcdn.com/image/fetch/$s_!UpHJ!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F61632a68-ae1c-4e88-9190-f96bf61bb5e6_426x514.png)

On the backend (Go + Echo), every action is a single endpoint that:

1. Loads the player and the affected entity from PostgreSQL inside a transaction.
2. Validates against current state (resources, cooldowns, locks).
3. Writes the new state, including any timed jobs (build, launder, raid).
4. Emits an event for downstream services (achievements, telemetry).

Long-running actions don’t block the request. They are written as rows with a `finishes_at` timestamp, and a background ticker sweeps for completed jobs.

```markup
// Simplified launder handler
func (s *LaunderService) StartLaunder(ctx context.Context, playerID string, amount float64) (*models.LaunderJob, error) {
    if active, _ := s.launder.GetActiveLaunder(ctx, playerID); active != nil {
        return nil, models.ErrLaunderInProgress
    }
    player, _ := s.player.GetByID(ctx, playerID)
    if player.DirtyCrypto < amount {
        return nil, models.ErrInsufficientDirty
    }
    finishesAt := time.Now().Add(tieredLaunderDuration(amount))
    return s.launder.StartLaunder(ctx, playerID, amount, finishesAt)
}
```

The frontend (Svelte + Vite) holds a small set of writable stores — one per domain (`playerStore`, `botnetStore`, `launderStore`, `bountyStore`). Each store wraps the API calls that touch it. A typical action looks like:

```markup
export async function startLaunder(amount) {
  launderStore.update(s => ({ ...s, loading: true }));
  try {
    const job = await gameApi.startLaunder(amount);
    launderStore.update(s => ({
      ...s,
      activeJob: job,
      dirtyCrypto: s.dirtyCrypto - amount,
      loading: false,
      error: null,
    }));
    if (job?.finishes_at) {
      actionWatcher.register(
        \`launder-${job.id}\`,
        new Date(job.finishes_at).getTime(),
        [fetchMe, fetchLaunderStatus],
      );
    }
    return job;
  } catch (err) {
    launderStore.update(s => ({ ...s, loading: false, error: err.message }));
    throw err;
  }
}
```

Three things to notice. The store mutates only after the server confirms (at the exception of the loading) — no predicted balances. The timer is registered against the server’s `finishes_at`, not a client-side `now() + duration`. And the error path doesn’t try to rollback imagined state; it just surfaces the message and lets the next refetch correct anything that drifted.

The pattern is small, repeats everywhere, and is boring on purpose. Boring is good. The complexity is in the game design, not in the plumbing.

## The trade-off: server-authoritative has an honest cost

![](https://substackcdn.com/image/fetch/$s_!k3sL!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F91d9650a-1eac-410c-8b67-bbefb49a32e4_480x214.png)

This pattern is not free either.

- The click-to-feedback gap is real. If the server takes 300ms, players feel 300ms. There is no client-side illusion to mask it. That puts pressure on backend latency in a way an optimistic UI would let you ignore.
- “Loading” states have to be designed, not bolted on. A button that just grey out is dead weight; a button that shows the request is in flight is information. Every action button needs that thought put into it.
- A bad network or a slow query stops looking like a game problem and starts looking like a UI problem. You feel every cold cache and every Postgres lock.

The upside is that there is exactly one source of truth and one place where game rules live: the server. The frontend never has to know that dirty crypto in big amounts has a heat penalty, or that building cost less under certain upgrades, or that a hack is gated by cooldown. It sends an intent, gets a result, and renders it. New rules ship as backend changes alone, and the UI follows for free.

## How this looks in HiddenWars

![](https://substackcdn.com/image/fetch/$s_!rhOd!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2d9cc911-a786-46b2-9add-382286732aaa_1849x432.png)

The core loop in HiddenWars is *scan → hack → launder → upgrade*.

- **Scan** is cheap and asynchronous. The UI updates instantly.
- **Hack** is probabilistic. The UI plays a short animation while the backend waits to resolve with its ticker the outcome of the hack.
- **Launder** can be a long-running async job: dirty crypto goes in, a timer starts, clean crypto comes out. The button locks the moment you commit, the timer starts immediately, and the server reconciles when the job finishes.
- **Upgrade** is similar to launder — queued, timed, server-resolved, but visually live.

The result is a game that *plays* like a real-time strategy game even though almost nothing about it is real-time. Players queue actions, watch timers, return later, and the loop keeps a steady rhythm. The browser is not a pretending to be a console; the is built around what the browser is actually good at.

## Takeaways

If you’re building anything async-heavy in the browser:

1. Treat the server as the only source of truth. Don’t mutate state on the client.
2. Acknowledge intent instantly (lock the button, show the request is in flight) but don’t pretend to know the outcome.
3. Drive timers from the server’s `finishes_at`, never from the client’s `now() + duration`. The client clock is a liar.
4. Be honest about probabilistic actions. A rolling animation is not the same as a fake success.
5. Spend your effort on backend latency, not client-side prediction. Short, reliable round-trips beat clever optimism.

A good core loop is the smallest interaction in your game that can stand on its own. Get it right and the rest of the system — economy, PvP, onboarding — have something to hang off. Get it wrong and no amount of content will save it.

---

*I used these ideas in [HiddenWars](https://hiddenwars.io/), a browser-based multiplayer hacking strategy game. If you want to see how this loop behaves in practice, the game is live.*