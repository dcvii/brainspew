---
title: "Is the Rust hype real?"
source: "https://medium.com/@gabriel.rodrigues.0501/is-the-rust-hype-real-17dbd6865a34"
author:
  - "[[Gabriel Rodrigues]]"
published: 2023-02-09
created: 2025-02-17
description: "Hello World, Gabriel here again to bring you some new ones, this time more related to programming during this article I will tell you how was my first contact with Rust and the Actix Web Framework…"
tags:
  - "clippings"
---
## Getting Started with Rust and understanding why is so loved and also deploying and stress testing my first web API within the Actix Framework + comparing it with Django REST Framework(Python REST API)

[

![Gabriel Rodrigues](https://miro.medium.com/v2/resize:fill:88:88/1*uQMy3R9LYQxd_1J0PP8X4w.png)

](https://medium.com/@gabriel.rodrigues.0501?source=post_page---byline--17dbd6865a34---------------------------------------)

## **Introduction**

Hello World, Gabriel here again to bring you some new ones, this time more related to programming during this article I will tell you how was my first contact with Rust and the Actix Web Framework. For the people who still don’t know me you can check out [my profile](https://www.linkedin.com/in/gabrielucido/) on LinkedIn, so, let's cut the check and get started.

## **Why Rust?**

So in January of 2023, I was as always in my daily routine as a developer at [ViaHub Tecnologia](https://medium.com/u/e21a0d3e7898?source=post_page---user_mention--17dbd6865a34---------------------------------------), and recently internally as the Developer Centric team we tend always find new ways of both improving performance, reliability, quality, costs, Dora metrics, and many aspects present at a technology company.

It's pretty interesting when the developer's survey of Stack Overflow comes out every year you can check out the full survey at the link down below and it's interesting what it says.

> Rust is on its seventh year as the most loved language with 87% of developers saying they want to continue using it.

![](https://miro.medium.com/v2/resize:fit:700/1*EIM-4fS2yZZfjG2PHEF5dA.png)

## **Honor mention to GoLang**

Go Lang is being widely used in some other relevant marketplaces and it is making its name mainly because is an alternative with more performance and lower resource consumption when compared with stacks like DOTNET, Java, node, and other high-level programming languages. I particularly still am not involved too much with it since my other colleagues of mine already are evaluating and documenting the pros and cons of using Go Lang initially in our team and potentially at a company level.

![](https://miro.medium.com/v2/resize:fit:700/0*bAEQBV0-B4dAzlB7.png)

Pretty Cute Ferries ❤

Another language we currently looking at is Rust which also appeared in [Stack Overflow](https://survey.stackoverflow.co/2022/) survey with an expressive community growth alongside tremendous love among the developers. That last part being the most loved programming language in the world catches my attention since we are the Developer Centric team so if Rust means developers are happier so I guess it’s worth the effort.

My goal here does not is to prove that one is best than the other but at first, to understand why It is being so loved and If it’s better in some basic concepts like performance, developer experience, infrastructure cost, and so on within our organizational structure.

## Getting Started with Rust

So for this challenge, I would need to learn Rust. Because I already coded in other languages like Javascript, Typescript, Python, and C# the logic fundamentals were as always after you pass the First language barrier pretty trivial but in Rust, I was particularly scared about pointers and the sophisticated ownership and borrow checker features. But I won't be able to write code in Rust just by understanding the concepts and due to my nature of "***JUST DO IT "*** I needed to get the basics syntax. To do so, I started with this awesome and free introduction course at [Traversy Media Youtube](https://www.youtube.com/@TraversyMedia) Channel that you can check down below.

Also in this video description, you can access [this repository](https://github.com/bradtraversy/rust_sandbox) with an all set of snippets that I would frequently consult in my first steps to get used to the new syntax. After the first week, I really didn't need to use it anymore which to me gives the impression that besides looking a little bit strange at the beginning but is perfectly adaptable even if you came from a higher-level language like Typescript or Python so you can easily get the hang of it.

**The Rust Documentation**

In general, the [Rust documentation](https://www.rust-lang.org/learn) is pretty good and it helps a lot to understand the key concepts of the language I can say that it is at least well-written and categorized. For example, I found some code that was using what we call closures which was a completely new concept to me and just looking up the documentation about closures I could find [this snippet](https://doc.rust-lang.org/book/ch13-01-closures.html) which really is a no-brainer to me.

```
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```

## **Why Actix Web?**

You probably should be thinking why Actix? ==In fact, the reasons just don’t fit on a single post without becoming extremely boring so for the sake of content think I will try to summarize what lead me to Actix.==

The TLDR Actix is the most adaptive for making REST both small and big-size applications while being one of the most performant, well-documented, and popular of Rust.

I had to search through many forums, articles, and tech influencers talking about frameworks like Actix, Rocket, and Axum. It was a lot to consider. Community support, scalability, performance, productivity, and so on. But, the main thing for me is to combine both your application needs, with the gold rule of considering the final user who probably won't know or even doesn't care if at the end of the day what you are using delivers, and does it with acceptable performance, consistency, and reliability considering the modern standards for applications nowadays.

![](https://miro.medium.com/v2/resize:fit:700/1*wssJ_jqFoB5bLo6r2Dt9sA.png)

[https://www.techempower.com/benchmarks/#section=data-r21&o=e&test=composite](https://www.techempower.com/benchmarks/#section=data-r21&o=e&test=composite)

This reference above shows the composite scores in multiple tests filtered by Full ORM versions only. You can see that Actix was right on the top portion after the also rust framework Xitca-web. Although, this benchmark doesn't really mean too much is cool to see that it is capable of beating up some other popular frameworks like spring, and even its improved brother Quarkus. You can check out more about the Actix framework at their official website down below.

## Demo Time!

## Defining how and when it would happen

Now it's finely the demo time when I create a project from scratch and code it till we can make some comparisons between other frameworks.  
For this demo, I had an opportunity to implement a simple application because I already would need to implement a Django REST(Python) API endpoint for internal work purposes.

The issue was pretty simple. I had a database filled with users that have this structure:

> Obs.: Many informations was ommited or redacted due to legal, etchical, professional or security reasons.

```
CREATE TABLE users (
  id VARCHAR NOT NULL PRIMARY KEY,
  github_username VARCHAR NOT NULL,
  name VARCHAR,
  email VARCHAR NOT NULL,
)
```

This database would be externally fed by an external worker who consumes a User Message Queue. So, while the workers still weren't turned on which means a static count of users on the database I generated a dump and populate another database instance mirroring the first one then run the tests on both without(or at least minimal) variation of the database in the application performance.

What the application would actually need to do was simply query this data from the database which in this case was just a few dozen and parse it to a specific JSON structure compatible with the [backstage](https://backstage.io/) user Entity custom provider and respond with the parsed data.

All of this only was possible because we have incredible Planning and preparation here at **Developer Centric** squad which allowed me to know that I would need to implement this feature in weeks of advance.

## Implementation and Stress Test

This test was made with strict time boxes and I would have way more complete, conclusive, and reliable results within more time to spend.

![](https://miro.medium.com/v2/resize:fit:700/1*bZs6-OpHydm40enyz4LkIg.jpeg)

A Single request to Django REST with a 494ms response time (Content Redacted)

![](https://miro.medium.com/v2/resize:fit:700/1*nseOYCyVbLUhu50XQwgjmg.png)

Django REST Latency During the stress test

![](https://miro.medium.com/v2/resize:fit:700/1*yUoviYX75MDlcHFpLhgbZw.png)

Python Application CPU Usage during the stress test

![](https://miro.medium.com/v2/resize:fit:700/1*e48hPQhqirgyi0dRi3sBZQ.png)

Python Application Memory Usage during the stress test

![](https://miro.medium.com/v2/resize:fit:700/1*yvIIo5tRldi3KvZiy1NiuQ.jpeg)

A single request to Actix Web with 50ms response time (Content Redacted)

![](https://miro.medium.com/v2/resize:fit:700/1*S2GiF-mLdG4k5QL3I75WmQ.png)

Actix Latency Chart

![](https://miro.medium.com/v2/resize:fit:700/1*s2GXQtsE4_ZpGhJmr2gyow.png)

Actix CPU Usage During the Test

![](https://miro.medium.com/v2/resize:fit:700/1*fQIGQ3cXilnW5we8akMEqA.png)

Actix Memory Usage During the Test

## **Conclusion**

During this journey, my experience was a bit painful at the beginning but there is a lot of content to guide you completely for free and another honorable mention to the youtube channel [Let's Get Rusty](https://www.youtube.com/c/LetsGetRusty?app=desktop) helped me so much to go through it.

Here are some pros and cons I one expose:

**Cons**

- The code is more verbose
- The compiler is really slow, It really can be improved but if wanna your code to break the better time would be never of course if it does the best time to happen is at compile time but for my small project wasn't a concern.
- The community is small yet beside its 50% growth in 2022.
- Learn curve beside it was pretty fun for me =)

**Pros**

- The Compiler is really intelligent and helps a lot to code
- The performance is blazing fast
- The **memory consumption** was more than **40x lower** than Django (19MB vs 843MB) which can result in tremendous infrastructure cost savings.
- Is incredible how things simply work right after the codes compile. In Typescript or Python, I often would have codes that compile but would have to be tweaked many times until it actually works. The way you code in Rust just makes you aware of almost anything that could go wrong so you can handle recoverable errors, in other languages you simply can make a try/catch error handling but it's way more painful than in Rust.

So that's it, I really enjoyed it a lot and I hope that Rust keeps growing in this amazing shape and love! what do you think about Rust? Feel free to comment below and also hit the clap button to upvote this post! Best Regards, see you next time!