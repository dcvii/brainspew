---
title: "🫰Clickvote: Open-source upvotes, likes, and reviews to any context"
source: https://dev.to/github20k/clickvote-open-source-upvotes-likes-and-reviews-to-any-context-3ef9
author:
  - "[[Nevo David]]"
published: 2023-07-11
created: 2025-02-17
description: TL;DR   I built an open-source app to add upvote, like, and reviews anywhere. And while it... Tagged with webdev, javascript, devops, programming.
tags:
  - clippings
  - boxtag
---
## TL;DR

I built an open-source app to add upvote, like, and reviews anywhere.  
And while it sounds easy, I kind of broke my head on the architecture.  
Let's talk about it.

[![Image description](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Flz5yph314srwxljesaxq.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Flz5yph314srwxljesaxq.gif)

---

## What the hell are you building? 🤯

In the last decade, I had the chance to develop "reviews", "upvotes", and "likes" in multiple places, and I have also seen them in numerous areas like:

- Reddit
- Facebook
- Instagram
- Upwork
- Food apps
- Project management tools
- Customer feedback tools
- Roadmap tools

And the list continues.

Ranking:  
[![Type1](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fsnfnji35yd07eqj70hjm.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fsnfnji35yd07eqj70hjm.gif)

Likes:  
[![Type2](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fdbwei3o2qfvrmz2m5rcj.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fdbwei3o2qfvrmz2m5rcj.gif)

Upvotes:  
[![Type3](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fjyzrewjkz55sh0qdt9tz.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fjyzrewjkz55sh0qdt9tz.gif)

And so far, I have realized it's pretty simple to build it in-house - until it's not.

You need to take care of the following:

- Showing real-time updates of likes, upvotes, and reviews between clients
- Learn about your members through deep analytics
- Deal with an unlimited amount of clicks per second (depends on your scale)
- Actually manage this

---

## The dream 😴

Well, it's not far-fetched...  
What if you could put a super simple component that will add this functionality instantly to you (like literally) in 5 minutes?

Here is the code snippet:

[![Snip](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Faporjrt3sn1x3y0aaf1c.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Faporjrt3sn1x3y0aaf1c.png)

You can wrap your application with `ClickVoteProvider`, providing the current user's id.

And then, distribute different `ClickVoteComponent` around your app with a dynamic id of the thing you want to vote to.

Once you interact with the voting (`LikeStyle`), it will update all the other users watching the same component with the new value.

So we can take the simple dashboard in Novu

[![Novu](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F7wkcch4qbvxshzugnwbb.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F7wkcch4qbvxshzugnwbb.png)

And in one minute change it to something like this:

[![Novu Upvote](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fvy25h5pz64iev63mi7q5.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fvy25h5pz64iev63mi7q5.png)

Ok, now that we all understand what we are trying to build.  
Let's see what it actually looks like.

---

## The Graph! (I added colors)

[![Graph](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fqz3avbh202xnrel1unua.jpg)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fqz3avbh202xnrel1unua.jpg)

It looks a bit complicated for a simple like 🤔  
But let me try and explain.

### The Analytics Board:

Like in every other system, you have the dashboard.  
It's made out of NextJS(for the front end) and NestJS (for the backend), and includes MongoDB.

1. Add new types of votes you want to monitor.
2. Watch analytics of who clicked / how many / which days / what's the best area etc.
3. Provide a way for the customer to attach the data source they want to be informed of once there is an interaction (they might want to change their system).

### The User Application:

Here is where it becomes tricky.

1. We create a WebSocket server that all the clients can connect to receive instant updates about new likes and upvotes. (I have checked Server Sent Events - SSE but there is a hard limit for 6 on the browser, so decided not to)
2. The WebSocket server needs to question and updates the number of votes while handling a heavy load of click; for that, we use Redis, which gives us options like `WATCH` and `MULTI` to add transactions and prevent race conditions where the counter will have a different number than what you expect.
3. Next is Apache Kafka - If you plan to have thousands of likes every second, you can't just insert it into your database (it will crash). Also, you want something to ensure the information gets into the database and does not fail. I have chosen Kafka because it's popular, but you can easily select another service like Apache Pulsar. So we send everything to Kafka.
4. NestJS MicroService Group Consumers will listen to the Kafka topics, pull in information, and add it to the database.
5. I have chosen to use Timescale as a time-series database. I could use something like Clickhouse or Redshift. I like Timescale because it's Postgres with some "plugins" It means that the open-source community can just choose to use Postgres instead of a time-series database. (for a lower scale)
6. Another NestJS MicroService Group Consumer that will send the information to the User application according to their preferences (API, direct DB insert, another Kafka), anything they choose.

---

## How much will it cost me to host this stack? 🤣

If being cheap:

- Vercel Frontend (NextJS) $20
- Timescale $31
- Upstash for serverless Kafka / Redis ~$70
- Digital Ocean Websockets server $25
- Digital Ocean Backend $25
- Digital Ocean 1 Worker (Consumer) $25
- MongoDB Atlas $20

I believe not less than $216.

It can obviosly sit in one server with a docker-compose, but it will not last long.

At a later point I believe that the backend / workers / websockets should be Dockerized, Kuberneterized and sit somewhere on AWS.

Will get there 🤞

[![Making Money](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2h5o0k5fn7nzts3gp20c.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2h5o0k5fn7nzts3gp20c.gif)

---

## Things that are definitely missing

- Option for non authenticated users to see the results.
- Anonymous voting with a fingerprint.
- More varinats of the style button (that I haven't thought about)
- Sync votes from different applications (Bi-Directional)
- Motivation - help me? 😅

---

## What's the adoption aspect of it

So far, it looks like it will mostly fit B2B2C companies like:

- Social Media
- Job websites
- Documentations? (if there's an anonymous feature, most likely work with something like [Fingerprint.com](https://github.com/fingerprintjs/fingerprintjs))
- Reviews websites (Glassdoors?)
- Maps websites

Having B2B businesses adopting this requires some education in the market. (some do it already)

---

## Show me the code 👀

Well, there is no documentation yet.  
It's still a work in progress.  
You can find there:

- Nx Monorepo architecture.
- NestJS Backend.
- NestJS Kafka Microservice.
- NestJS Websockets.
- NextJS - looks bad, I know 🤣

But please show your support with a star ⭐️  
It will help me know if there is a need for that.

[https://github.com/clickvote/clickvote](https://github.com/clickvote/clickvote)

[![Shoot Stars](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fqi8ri6az3xhss2227062.gif)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fqi8ri6az3xhss2227062.gif)

Sorry for the ugly design 😛  
(Logo made with MidJourney)

Follow me on Twitter! [Let's talk](https://twitter.com/nevodavid) 🙇🏻‍♂️

Do you think there is room for a product like that?