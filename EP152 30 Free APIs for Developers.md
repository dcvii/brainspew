---
title: "EP152: 30 Free APIs for Developers"
source: "https://blog.bytebytego.com/p/ep152-30-free-apis-for-developers?utm_source=post-email-title&publication_id=817132&post_id=158100775&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email"
author:
  - "[[ByteByteGo]]"
published: 2025-03-01
created: 2025-03-01
description: "APIs are the backbone of modern software development."
tags:
  - "clippings"
---
![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F348fd618-f3c5-482c-bf2b-07281d79461b_1200x628.heic)

To better understand the vulnerabilities and threats facing modern DevOps organizations, Datadog analyzed security posture data from a sample of thousands of organizations that use AWS, Azure, or Google Cloud.

In this report, you’ll gain valuable cloud security insights based on this research including:

- How long-lived credentials create opportunities for attackers to breach cloud environments
- Adoption of proactive cloud security mechanisms such as S3 Public Access Block or IMDSv2 in AWS
- Most common risks when using managed Kubernetes distributions

[Read the report](https://bit.ly/Datadog_030125)

This weeks’ system design refresher:

- 8 Most Important Tips for Designing Fault-Tolerant System (Youtube video)
- 30 Free APIs for Developers
- The Generative AI Learning Roadmap
- HTTP/1 -> HTTP/2 -> HTTP/3
- Structure of URL
- SPONSOR US

<iframe src="https://www.youtube-nocookie.com/embed/3Lis4w4_bBc?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" loading="lazy" gesture="media" allow="autoplay; fullscreen" allowautoplay="true" allowfullscreen="true" width="728" height="409"></iframe>

APIs are the backbone of modern software development. Whether it is a hobby project or a real-world application, developers need APIs. These APIs (some completely free and some with free tiers) can help kickstart development.

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_lossy/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff112df94-df52-4140-98ec-873e5b74d988_1280x1601.gif)

1. Public APIs for Open Data  
OpenStreetMap, NASA, World Bank, GeoNames, and Open Library APIs provide a lot of useful data.
2. Weather APIs  
OpenWeather, Weather API, StormGlass, Visual Crossing, and WeatherBit are some APIs to fetch weather-related information
3. News APIs  
The News API, GNews, Guardian News, Current News API, and New York Times API can help developers fetch the latest news.
4. AI & NLP APIs  
Open AI API, Gemini, HugginFace API, Claude API, and Grok API can help developers experiment with AI models and tools.
5. Sports API  
Football Data Org, NBA API, All Sports API, ESPN API, and API-Football can help fetch sports-related information.
6. Miscellaneous  
Some interesting miscellaneous APIs are TimeZone API, Unsplash API, Marvel API, Dictionary API, and QR Generation API.

Over to you: Which other API will you add to the list?

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6f2c4e99-ae78-4671-b055-60fd049856be_1200x628.png)

Join Lazar from Sentry for a hands-on session where you’ll build it, watch it break, debug it, and go from “no idea what’s wrong” to fixing issues—all in one go. Since we’re serious developers (obviously), we’ll use Next.js and:

- Setup Sentry from the ground up - including Errors, Session Replay, and Tracing
- Learn ways to use Replays to understand the real user experience, and how to use Tracing to debug application issues
- Leverage Sentry AI and the context of your application to understand what’s actually broken, and use Autofix to generate a fix - from root cause all the way to PR.

[RSVP](https://bit.ly/Sentry_030125)

Generative AI is a type of AI that can create new content based on what it has learned from existing knowledge. It has the potential to revolutionize human learning.

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_lossy/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc3bf4776-744b-4e87-85f8-6dddd6d85597_1280x1566.gif)

Here’s a GenAI roadmap with learning resources:

1. Learn about important concepts like Probability, Statistics, Calculus, and Linear Algebra.
2. Understand the working of foundational models like GPT, MetaAI’s Llama, Gemini, DeepSeek, and Claude.
3. Learn the GenAI development stack that includes Python, Language, ChatGPT APIs, Prompt Engineering, VectorDB, DeepSeek, Llama, and Huggingface.
4. Learn how to train and fine-tune a foundation model.
5. Understand the role of AI Agents and how to build one using GenAI tools.
6. Learn about GenAI models for computer vision such as GAN (Generative Adversarial Networks), MidJourney, DALL E, Flux, and so on.
7. Make use of GenAI Learning Resources such as DeepLearning AI platform, Kaggle, Generative AI Insider’s Guide by ByteByteGo, Google Labs, and Nvidia Learning platforms.

Over to you: What else will you add to the GenAI learning roadmap?

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_lossy/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc1dbb32e-8d1b-4c13-ae48-fe485ad92191_1280x1601.gif)

HTTP 1 started in 1996 followed by HTTP 1.1 the very next year. In 2015, HTTP 2 came about and in 2019 we got HTTP 3.

With each iteration, the protocol has evolved in new and interesting ways.

1 - HTTP 1 (and its sub-versions) introduced features like persistent connections, pipelining, and the concept of headers. The protocol was built on top of TCP and provided a reliable way of communication over the World Wide Web. It is still used despite being over 25 years old.

2 - HTTP 2 brought new features such as multiplexing, stream prioritization, server push, and HPACK compression. However, it still used TCP as the underlying protocol.

3 - HTTP 3 uses Google’s QUIC, which is built on top of UDP. In other words, HTTP 3 has moved away from TCP.

Over to you: What would you add to understand the evolution of HTTP over the years?

Do you know all the components of a URL?

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_lossy/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd864f35c-537c-4571-8644-ce20d1a0caa5_1280x1427.gif)

Uniform Resource Locator (URL) is a term familiar to most people, as it is used to locate resources on the internet. When you type a URL into a web browser's address bar, you are accessing a "resource", not just a webpage.

URLs comprise several components:

- The protocol or scheme, such as http, https, and ftp.
- The domain name and port, separated by a period (.)
- The path to the resource, separated by a slash (/)
- The parameters, which start with a question mark (?) and consist of key-value pairs, such as a=b&c=d.
- The fragment or anchor, indicated by a pound sign (#), which is used to bookmark a specific section of the resource.

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **[sponsorship@bytebytego.com](https://blog.bytebytego.com/p/)**.