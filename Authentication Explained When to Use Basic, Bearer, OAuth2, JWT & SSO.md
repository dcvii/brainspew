---
title: "Authentication Explained: When to Use Basic, Bearer, OAuth2, JWT & SSO"
source: "https://javarevisited.substack.com/p/system-design-basics-authentication"
author:
  - "[[javinpaul]]"
published: 2025-12-02
created: 2025-12-05
description: "Authentication Explained: When to Use Basic, Bearer, OAuth2, JWT & SSO"
tags:
  - "clippings"
---
### Authentication Explained: When to Use Basic, Bearer, OAuth2, JWT & SSO

> **Preparing for System Design Interviews? [Join ByteByteGo now](https://bytebytego.com/pricing?fpr=javarevisited) for a structured preparation. They are also offering a rare [50% discount](https://bytebytego.com/pricing?fpr=javarevisited) now on their lifetime plan.**

![](https://substackcdn.com/image/fetch/$s_!Ccz_!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F107deea3-3deb-4462-a4a3-5db60fe96be4_800x450.png)

Hello guys, when you design any modern distributed system, one of the earliest, and most critical questions is: **How do users and services prove who they are?**  
**Authentication** isn’t just a security checkbox; it shapes your system’s scalability, user experience, latency, caching strategy, and even how microservices talk to each other.

In system design interviews, candidates often jump straight into databases, load balancers, and microservices but overlook how authentication fits into the overall architecture.

A solid understanding of authentication models helps you design systems that are secure *and* practical to operate at scale.

In this guide , Senior Software engineer, System Design expert, YouTuber and instructor of popular System Design course - **[System Design for Beginners: Build Scalable Backend Systems](https://trk.udemy.com/c/3294490/3262185/39854?u=https%3A%2F%2Fwww.udemy.com%2Fcourse%2Fsystem-design-mastery%2F%3FcouponCode%3DMT180825A)** on Udemy, breaks down the core building blocks of authentication — **Basic Auth, Bearer Tokens, OAuth2, JWT, and SSO** and explains **when** and **why** you’d use each in a real-world system design scenario.

By the end, you’ll understand how these mechanisms work, the trade-offs involved, and how to select the right approach for large, distributed applications.

By the way, If you’re preparing for **System Design Interviews** or want to move from being a developer to thinking like an architect, mastering these concepts is essential. I highly recommend **[ByteByteGo](https://bytebytego.com/pricing?fpr=javarevisited)** — one of the best platforms that explains these distributed system patterns visually and intuitively.

Their diagrams and case studies (like how browsers fetch content, how CDNs reduce latency, and how DNS propagation works) make complex concepts easy to grasp.

ByteByteGo is currently offering **[up to 50% OFF](https://bytebytego.com/pricing?fpr=javarevisited)** [on their annual plan](https://bytebytego.com/pricing?fpr=javarevisited) — a perfect time to start your system design learning journey.

With that, over to [Hayk](https://open.substack.com/users/145622767-hayk?utm_source=mentions) to take you through the rest of the article.

Before a system can authorize or restrict anything, it needs to know the identity of the requester.

![](https://substackcdn.com/image/fetch/$s_!C3ZR!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc7dc599e-06d1-4794-b122-076927576435_800x448.png)

That’s what authentication does — it verifies that the person or system trying to access your app is legit.

In this post, you’ll learn how modern apps handle authentication, from basic tokens to OAuth flows and Single Sign-On.

---

### What is Authentication?

Authentication is the first gate.

Before you can access data or perform actions, the system needs to know who you are.

![](https://substackcdn.com/image/fetch/$s_!1PhS!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F02540aaf-0d9c-4398-b709-e26181b5aa19_800x445.png)

Once identity is confirmed, then the system can move on to what you’re allowed to do — that’s authorization, which we’ll cover in the next lesson.

---

### Basic Authentication

Basic Authentication is the oldest method, username and password are encoded and sent with every request.

![](https://substackcdn.com/image/fetch/$s_!1Kvt!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa27395d8-1748-48d1-9108-25ac3b601b75_800x451.png)

It’s simple, but insecure unless wrapped in HTTPS. That’s why it’s almost never used in production anymore.

---

### Bearer Tokens

Bearer tokens are more secure. Instead of a password, you send a token with each request.

![](https://substackcdn.com/image/fetch/$s_!qxvj!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2cc6b78c-68b8-492a-ad6c-c3c0abc4f40a_800x447.png)

The server checks the token and, if valid, grants access.

This is the standard approach in API design today. It’s fast, stateless, and because of that, it’s easy to scale.

---

### OAuth2 and JWTs

OAuth2 is a protocol that lets users log in through a trusted provider — like Google or GitHub — without sharing passwords with your app.

![](https://substackcdn.com/image/fetch/$s_!eEVn!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6e17ec43-d8c9-4bf6-b3a3-740361f88d7e_800x446.png)

The provider gives you an **access token**, usually in the form of a **JWT**,which is a signed object that contains user info.

JWTs are also stateless, which means you don’t need to store sessions. The server just verifies the token and reads the data inside.

---

### Want to See This in Real Projects?

If you want to see how these authentication flows are implemented in real-world projects — not just in theory — .

![](https://substackcdn.com/image/fetch/$s_!trM4!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F26916e08-1d11-4c64-be5f-fd21d04b169c_800x447.png)

---

### Access and Refresh Tokens

Modern systems use short-lived access tokens for API calls and long-lived refresh tokens to stay logged in.

When the access token expires, the refresh token quietly gets a new one behind the scenes.

![](https://substackcdn.com/image/fetch/$s_!u4qn!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa9110e8e-bdd4-42d8-82b0-1f668b19ca6c_800x448.png)

This way, users don’t have to log in again, and your system stays secure.

---

### Single Sign-On (SSO) and Identity Protocols

SSO lets users log in once and access multiple services.

Behind the scenes, it’s powered by identity protocols like **OAuth2** and **SAML**.

![](https://substackcdn.com/image/fetch/$s_!wHbX!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffe7a2043-2652-4f10-96a5-350271f0e5cf_800x447.png)

OAuth2 is used in most modern apps, like “Login with Google.”

SAML is older and XML-based, but still common in companies that use things like Salesforce or internal dashboards.

These are identity protocols, meaning they define how apps securely exchange user login info.

---

### Authorization is Next

You now know how apps verify identity using tokens, OAuth2, JWTs, and SSO. These are the same tools used by the systems you use every day — and they form the backbone of secure, scalable systems.

Authentication tells us *who* the user is…

![](https://substackcdn.com/image/fetch/$s_!dWsP!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc62f8436-b2cc-4df6-b948-9ce9dbab089c_800x442.png)

But that’s not enough.

We still need to decide what they’re *allowed* to do — and that’s **Authorization**, which we’ll cover in the next post.

If you like this article then I highly recommend you to subscribe to [Hayk’s newsletter](https://hayksimonyan.substack.com/?r=a1ck9) and his [YouTube channel](https://www.youtube.com/watch?v=lcPcyNAEZgo)

<iframe src="https://www.youtube-nocookie.com/embed/adOkTjIIDnk?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen="true" width="728" height="409"></iframe>

**Other System Design Articles you may like**