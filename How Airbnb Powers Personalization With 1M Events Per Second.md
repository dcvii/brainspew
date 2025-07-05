---
title: "How Airbnb Powers Personalization With 1M Events Per Second"
source: "https://blog.bytebytego.com/p/how-airbnb-powers-personalization?publication_id=817132&post_id=161114564&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2023-04-19
created: 2025-04-21
description: "Personalizing an experience meaningfully, especially across a product as broad as Airbnb, requires understanding users while they interact with the app."
tags:
  - "clippings"
---
## Build Private AI Agents at Scale (Sponsored)

![](https://substackcdn.com/image/fetch/w_424)

Agentic AI is transforming how enterprises work — but building secure, auditable AI agents at scale isn’t easy. Join Redpanda Founder & CEO Alex Gallego and Senior Software Engineer Tyler Rockwood for a live Launch Stream unveiling the **Agentic Runtime Platform**: a new way to run private, traceable, multi-agent AI systems in your own cloud. See live demos, get insights from AI leaders, and discover how to overcome the hidden infrastructure challenges behind today’s enterprise AI.

This is your first look at the infrastructure powering the agentic enterprise.

---

*Disclaimer: The details in this post have been derived from the articles written by the Airbnb engineering team. All credit for the technical details goes to the Airbnb Engineering Team. The links to the original articles and videos are present in the references section at the end of the post. We’ve attempted to analyze the details and provide our input about them. If you find any inaccuracies or omissions, please leave a comment, and we will do our best to fix them.*

Modern digital platforms rely on personalization to stay relevant. However, personalizing an experience meaningfully, especially across a product as broad as Airbnb, requires understanding users while they interact with the app.

The task is difficult due to the following reasons:

- **User journeys are non-linear**: A guest might view ten homes, bounce for a day, come back and wishlist three, then finally book one.
- **Engagement signals are fragmented**: Searches, scrolls, views, and bookings each live in a different system.
- **Latency matters**: Knowing that someone searched for a specific query is only useful if we can act on it within seconds, not after the fact.
- **Teams want insights:** Not everyone wants to be a stream processing expert. Most product teams don’t want to learn Flink or Kafka to build features.

User Signals Platform (USP) is Airbnb’s answer to these challenges. This platform was built to:

- Ingest and process user actions in near real-time with end-to-end latency under 1 second.
- Store real-time and historical user engagement data in a way that’s queryable and durable.
- Support both synchronous and asynchronous computation.
- Expose a clean interface for the product team so they can define signals, cohorts, and behaviors without needing to write code.
- Power personalization across Airbnb from home page listings to in-app notifications and customer support intelligence.

In this article, we’ll look at the architecture of the User Signals Platform along with the challenges faced by the Airbnb engineering team while trying to make it a reality.

## Architecture Overview

There’s a reason most companies don’t have a robust real-time personalization platform: streaming architecture is hard to get right, especially when you care about both low latency and long-term correctness.

The User Signals Platform (USP) does this by combining a Lambda-style pipeline with an online query layer, built on top of a few battle-tested primitives such as Kafka, Flink, a KV store, and some disciplined design principles.

See the diagram below for the architecture overview:

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/668f8ea5-ca06-4f2f-ad72-579a778f4a33_1600x1094.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:996,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

At a high level, USP is split into two main components.

### 1 - Data Pipeline Layer

This is where the heavy lifting happens. The pipeline ingests raw Kafka events, transforms them into structured user signals, and writes them into a versioned KV store.

It includes:

- **Real-Time Streaming (Flink):** Every user interaction (searches, clicks, views, bookings) gets processed event-by-event using Flink, not micro-batch jobs.
- **Offline Batch (Backfill + Corrections):** If something breaks or if business logic changes, the system can reprocess historical events and reconcile the store without rewriting production pipelines.

This dual-path setup follows the Lambda Architecture model.

### 2 - Online Serving Layer

Once the data is processed and stored, they wanted a fast way to serve it to downstream services. The online serving layer took care of this requirement.

Here’s what this layer does:

- It exposes an API for querying user signals by type, user, time range, etc.
- Talks directly to the KV store for sub-second lookup performance.
- Performs lightweight query-time logic when needed (for example, filtering and session computation).

### The Signal Lifecycle

Here’s how an individual user action flows through the system:

- User performs an action (for example, searching for a specific type of house in a certain location.
- The app emits a Kafka event with the details of that interaction.
- Flink picks it up, applies a developer-defined transform, and converts it into a structured signal.
- The signal is written to the KV store with a versioned timestamp (append-only).
- It’s also emitted to another Kafka topic, so downstream jobs (like segmentation or session analysis) can subscribe and react.
- Product features query the store in real-time. For example: “What did this user search for in the last 10 minutes?”

That’s the main loop. It sounds simple, but a lot is happening under the hood to make it safe, fast, and reliable.

See the diagram below:

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/44c61b09-3a0b-4335-a1dc-2428d2cae1b3_1600x1093.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:995,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

## Key Engineering Decisions

A few important architectural decisions the Airbnb engineering team took while building the USP were as follows:

### 1 - Flink Over Spark

Airbnb chose to use Flink instead of Spark.

Spark uses a micro-batch model. Instead of processing events as they arrive, it groups them into small batches (say, every 2 seconds) and runs them through the pipeline.

That’s fine for dashboards. But if your downstream use case is real-time product personalization, a few seconds of delay can feel like a lifetime. Imagine opening the Airbnb app, searching for “Paris”, and seeing homepage recommendations that still reflect your last trip to Kyoto.

The Spark model created delays that broke the user experience. Worse, those delays weren’t easy to tune away.

Flink, by contrast, is natively event-driven. It processes each event as it arrives. That gives:

- Lower end-to-end latency
- Better control over event time semantics
- Cleaner handling of stateful operations, like windowed aggregations and stream joins

As a trade-off, Flink had a steeper operational curve. However, for use cases where personalization needs to react in-session, not post-session, it was the appropriate choice for Airbnb.

### 2 - Append-Only Data Model

In stream processing, it is difficult to guarantee that an event will be processed exactly once. Even with Kafka and Flink’s best efforts, things can get retried, reordered, or replayed.

So, instead of fighting that, Airbnb leaned into it. They made every write to the KV store append-only, with a processing timestamp as the version. There are no in-place updates, and idempotency is handled by versioning.

This simplifies:

- **Reprocessing/Backfills**: They can replay events without worrying about overwriting the wrong thing.
- **Debugging**: They can trace what happened when, with a clear sequence.
- **Correctness under failure**: Crashes and retries couldn’t corrupt the data.

The trade-off was spending more on storage costs, but saving a ton on operational complexity.

### 3 - Config-Driven Developer Workflow

One of the most underrated engineering challenges isn’t building the system. It’s making it usable for the rest of the company.

USP tackles that head-on by giving developers a config-first interface to define their signal logic.

Here’s how it works:

- Engineers define new signals via a YAML-style config that contains details about the Kafka source topic, the transform class, and signal type
- They implement the transform class, which is essentially a small Java or Scala function.
- Next, they run a setup script.

The script autogenerates the necessary Flink job configurations, batch backfill scripts, and monitoring YAMLs. This pattern standardizes signal definitions across teams and reduces boilerplate and manual configuration.

## User Signal Types

When a user interacts with Airbnb (searches, clicks, or saves a home), the behavior emits a bunch of raw events. Most of them are meaningless on their own. But with the right structure and filtering, they become User Signals: queryable, composable, and rich with context.

USP makes it dead simple for engineers to define, transform, and consume these signals, without writing complex stream processing jobs from scratch.

See the code example below for a signal definition and the transform class.

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/27ddb540-f18d-4580-963b-4d8b28848d00_1426x912.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:912,%22width%22:1426,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

Source: Airbnb Tech Blog

There are two core signal types:

- **Simple User Signals:** A direct mapping from a Kafka event to a signal.
- **Join Signals:** A real-time join of two Kafka sources using a shared key.

### User Signals

These are the building blocks. Each user signal represents a stream of recent activity (searches, views, bookings, wishlists) attached to a user ID and timestamped for querying.

Engineers use a config file to define a new signal, and the heavy lifting happens in the transform class.

A few things to note:

- Validation is built in. Signals can reject noisy or malformed events up front.
- Transformations are composable. Every signal becomes a structured object and something the product logic can use.

### Join Signals

Sometimes, a single event isn’t enough. Maybe, there is a need to join them. For example:

- A page view with a user session
- A click event with a listing metadata update
- A wishlist add with trip intent signals

Rather than batch-processing this later, USP supports Join Signals: real-time stateful joins between two Kafka streams using a shared key.

To support this, a Join Signal configuration needs to be written. Under the hood, Flink does the join in real-time. RocksDB acts as the state store to hold intermediate join keys, and the result is a merged signal with richer context: ready to feed into ML models, personalization rules, or session-based analysis.

## User Segments

A User Segment is a logical group: a cohort of users who match a behavioral pattern or intent.

In most systems, user segmentation is a batch job. You run a SQL query once a day, label users as “engaged” or “likely to churn,” and hope that snapshot is still relevant tomorrow.

That doesn’t cut it when your product needs to react to user intent as it forms.

Airbnb’s User Signals Platform flips the script. With User Segments, engineers can define dynamic cohorts that update in near real-time, triggered by live user actions, not stale offline data.

The segment is defined by:

- A triggering condition (for example, a search or a wishlist add).
- A start time.
- An expiration time, which removes the user if they go inactive or meet some end condition.

These segments are recalculated on the fly, based on live signals flowing through the system.

Let’s say they want to target users who are actively planning a trip: people who are more likely to book in the next few days.

Here’s how segmentation might look:

- A user enters the “Active Trip Planner” segment when they perform a search on Airbnb.
- They stay in that segment for up to 14 days, unless they make a booking earlier.
- Every time they search again, the expiration window resets, keeping them in the cohort.

This segment powers things like trip recommendation modules, push notifications (for example: “Still looking for a beach house?”), and custom homepage experiences. Since it's built on streaming logic, updates happen within seconds of user activity, not hours later after a batch job finishes.

## Session Engagements

Most personalization systems are great at long-term memory: what you searched for last week, which cities you’ve favorited, and what kind of stays you usually book.

But they often miss the recent stuff.

Session engagements feature of the USP fixes that. It lets the platform answer queries like:

- “What is the user focused on right now?”
- “What kinds of listings are they engaging with in this session?”
- “Are they actively evaluating, or passively browsing?”

Instead of looking at user behavior in aggregate, session engagements look at bursts of activity within a session window covering short, meaningful slices of time that capture a user’s current goal or intent.

See the diagram below:

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/336227f0-cee3-4f86-b9f3-b1dc105a3065_1600x1092.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:994,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

Session engagements are powered by Flink streaming jobs that ingest transformed signals (from upstream user actions), group them by user ID, and process them in windowed intervals using two patterns:

### Sliding Windows

They are fixed-size windows that advance by a smaller step.

For example, a 10-minute window sliding every 5 minutes. It is useful for rolling insight, such as “What kind of listings is this user clicking every 10 minutes?”

### Session Windows

These are dynamically sized windows based on inactivity gaps. For example, start a session when the user clicks and close it after 30 minutes of silence.

This is useful for natural interaction clusters, such as listings viewed in a single burst of planning.

## Flink Stability with Hot Standby

One of the most critical pieces of a real-time stream processing system is operational resilience. You can have the smartest signal logic, the fastest queries, the cleanest data pipeline, but if your jobs stall when a server crashes, it will cause trouble.

Airbnb hardened its Flink deployment against exactly this kind of failure, with a simple but effective strategy: hot standby Task Managers.

Rather than waiting for Kubernetes to create new pods during failure, the team pre-provisions extra Task Managers that sit idle but are ready. These hot standbys are kept warm and registered with the Flink JobManager, so when failure hits, they can pick up tasks immediately.

See the diagram below:

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/dd0e65ec-edb0-4f07-b9c6-ad5f69a918a5_1600x989.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:900,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

This helps achieve zero cold-start lag for task reassignment and faster recovery time (seconds instead of minutes). There is also a lower event backlog risk with this setup.

## Conclusion

Airbnb’s User Signals Platform isn’t a prototype. It’s a production-grade engine powering critical personalization across one of the largest travel platforms in the world.

Here’s what the system is doing today in terms of scale:

- Processing over 1 million events per second.
- 100+ Flink jobs in production.
- 70K queries per second on the USP service layer.

In a way, USP is part of the core Airbnb infrastructure, running across dozens of teams, all contributing their signal definitions, segments, and use cases.

Even with all this machinery in place, the team sees room for growth, especially in how they handle asynchronous compute. The plan is to go further in smarter pipeline-level orchestration, pluggable execution backends, and end-to-end compute graphs.

It’s tempting to look at systems like this and focus on the streaming tech. But what makes the User Signals Platform successful isn’t just Flink or Kafka or RocksDB.

It’s the design choices such as:

- Embracing append-only data for resilience
- Hiding complexity behind clean developer abstractions
- Treating operational resilience as a first-class concern

The philosophy also matters: real-time data isn’t valuable unless it’s usable. Teams across the company can define signals, derive insights, and deploy personalized experiences without becoming stream engineers.

**References:**

- [Building a User Signals Platform at Airbnb](https://medium.com/airbnb-engineering/building-a-user-signals-platform-at-airbnb-b236078ec82b)
- [Flink Architecture](https://flink.apache.org/what-is-flink/flink-architecture/)

---

## SPONSOR US

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **[sponsorship@bytebytego.com](https://blog.bytebytego.com/p/)**.