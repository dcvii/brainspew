---
title: "We are under DDoS attack and we do nothing"
source: "https://tableplus.com/blog/2024/03/how-we-deal-with-ddos.html"
author:
  - "[[Huy Pham]]"
published: 2024-03-29
created: 2025-07-01
description: "Modern, native SQL client with intuitive GUI tools to create, access, query & edit multiple relational databases: MySQL, PostgreSQL, SQLite, Microsoft SQL Server, Amazon Redshift, MariaDB, CockroachDB, Vertica, and Redis."
tags:
  - "clippings"
---
![fine](https://tableplus.com/assets/images/ddos/fine.jpg)

### We’re under DDoS attack

Someone has been attempting to DDoS us for weeks now. They have flooded our server with hundreds of millions of requests and attempted to download our setup file millions of times. (In the last 5 days alone, they tried to download it more than 800K times - our setup file is approximately 200MB per download.)

- Most of the traffic came from EU, specifically Germany and United Kingdom, here is the recently API call within 30 days (not includes download request and CDN traffic).

![30-day](https://tableplus.com/assets/images/ddos/traffic.png)

- They have attempted to download the setup file millions of times (800,126 times in the last 5 days, totaling approximately 6 million times in the latest 30 days).
- The attack is still ongoing as we write this blog post.

### What we do in this hot situation

#### We do nothing, except watching them DDoS

- We haven’t blocked any attacker IP addresses.
- Although we use Cloudflare, we haven’t activated the “Under Attack” mode.
- Our server CPUs are almost idle, typically at 0-1% usage most of the time during attack.
- In general, we barely do anything.

#### Why?

- Because our services are capable of handling billions of requests per month without any issues, and it isn’t cost much.
- We have around 8 API services and its databases, all capable of handling billions of requests per month without caching.
- We have unlimited bandwidth with Cloudflare.

#### How?

- Our TablePlus apps design are simple, and this philosophy extends to our backend services, where we keep things as minimal as possible.
- We avoid using third-party services like Vercel or Netlify for rendering, as they can become bottlenecks and surprise you with bills during attacks. Instead, we use our webservers, which have no limitations.
- In the past, the monolith was a bottleneck due to weak VPS/processors. However, with today’s powerful VPS: multiple-core processors, high RAM and fast SSD (fast SSD/RAM speedup database a lot), a monolith service can handle billions of requests per month in a single instance if implemented correctly.

\=> Thus, we build a monolith service for each app, which is easy to deploy and maintain. No Docker, no Kubernetes, no dependencies, no runtime environment - just a binary file that can be deployed on any newly created VPS.

### Let’s talk about the Monolith

- Everyone tends to overcomplicate things, which isn’t an issue until you face pressure or limitations.
- We “heete” complexity, so we opt for the monolith. We consolidate everything an app needs into a single service: API, Website, Email, Payment… everything in one service.
- Deployment is straightforward: just one configuration file, build, and deploy. It’s lightning-fast when deploying or migrating services to another cloud vendor.
- Fewer dependencies make it easier to debug and identify bottlenecks. When there is an error, you don’t need to check as much because there is only a single service or just a few of them.

Monolith frameworks you can choose from include:

- Golang: Echo, Gin…
- PHP: Laravel…
- Ruby: Rails…
- Rust: Actix, Rocket, Warp…

### When done right, a single Web Framework of Go or Rust can handle billions of requests per month

- Choose a high-performance framework; we prefer Golang and Rust.
- Index your databases to reduce fetching time, especially as the dataset grows.
- Separate the main database (which remains unchanged or not increases size over time) from the log/usage database (which grows over time) to ensure your core business isn’t impacted by performance issues.
- Use reverse proxy to handle and distribute requests to your core API. If you need multiple servers, it will greatly assist you. We use Nginx - which is powerful.
- Put everything behind Cloudflare and configure it properly (enable cache, Argo, full SSL between Cloudfare and your servers…).
- Use a CDN that has DDoS protection. We prefer Cloudflare R2 and its CDN over Amazon CloudFront + S3 for both cost savings and protection.
- Don’t put any big downloadable file on your VPS without CDN or caching because it will quickly burn your bandwidth. We’re using Cloudflare CDN with unlimited bandwidth. (Cloudflare CDN will go through Argo if you enable it on the same domain. Be careful, as it will cost you a lot since Argo bandwidth is not free).
- Protect your mailer (when the user sends a request that requires sending an email from the server, e.g., the forgot password function) with throttling

### Let’s talk about the deployment

- At TablePlus, we’ve simplified the deployment process as much as possible. We don’t use Docker, Kubernetes, or any containers, or need to setup the enviroment.
- We use binaries. Binaries are fantastic; just copy them to any Linux server and run them as a process, just like running the TablePlus app on your macOS!
- When using binaries, you can let Linux Systemctl handle the process (by monitoring the process and restarting it if any fatal errors occur). We use everything natively; that is the best way to optimize performance. There is no CPU/RAM wasted on middle layers such as VMs, virtualization, or third-party infrastructure managers.
- We choose Go and Rust because they’re high-performance languages and can generate binary files for deployment.

### Update

##### Vercel reached out to us and they wanted to clarify that

We now have functionality to protect your site during these situations. First, there’s Spend Management, which allows you to set soft or hard spend caps, and then second there’s Attack Challenge Mode, which is similar to CF’s “Under Attack” mode.

\=> So don’t forget to turn on these features if you’re using them.

![30-day](https://tableplus.com/assets/images/ddos/tableplus-vs-hecker.png)