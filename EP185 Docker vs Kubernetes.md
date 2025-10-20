---
title: "EP185: Docker vs Kubernetes"
source: "https://blog.bytebytego.com/p/ep185-docker-vs-kubernetes?publication_id=817132&post_id=175216722&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2025-10-18
created: 2025-10-18
description: "Docker is a container platform that lets you package applications with their dependencies and run them on a single machine. Here’s how it works"
tags:
  - "clippings"
---
## AWS Guide to Cloud Architecture Diagrams (Sponsored)

![](https://substackcdn.com/image/fetch/$s_!fQaA!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2e0e22f6-5557-4ac6-9dcd-ce755009b98c_2400x2400.png)

Enhance visibility into your cloud architecture with expert insights from AWS + Datadog. In this ebook, AWS Solutions Architects Jason Mimick and James Wenzel guide you through best practices for creating professional and impactful diagrams.

---

This week’s system design refresher:

- Rate Limiter System Design: Token Bucket, Leaky Bucket, Scaling (Youtube video)
- Docker vs Kubernetes
- Batch vs Stream Processing
- What are Modular Monoliths?
- What is the difference between Process and Thread?
- How AI Agents Chain Tools, Memory, and Reasoning?
- SPONSOR US

---

## Rate Limiter System Design: Token Bucket, Leaky Bucket, Scaling

<iframe src="https://www.youtube-nocookie.com/embed/YXkOdWBwqaA?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen="true" width="728" height="409"></iframe>

---

## Docker vs Kubernetes

![Image](https://substackcdn.com/image/fetch/$s_!9WZ4!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9cfa2d94-1602-47c2-8942-b585c1d8d285_2252x2752.jpeg)

Docker is a container platform that lets you package applications with their dependencies and run them on a single machine. Here’s how it works:

1. Starts with the app code and dependencies written into a Dockerfile.
2. The build image step creates a portable container image.
3. A container runtime runs the image directly on the host machine.
4. Networking connects containers and external services and produces the final running app.

Kubernetes is a container orchestration platform that manages containerized applications across a cluster of machines for scalability and resilience. Here’s how it works:

1. Starts with the app code and dependencies in a Dockerfile.
2. The build image is passed to a container runtime supported by Kubernetes.
3. A master node runs the API server, etcd (key-value store), controller manager, and scheduler to coordinate the cluster.
4. Worker nodes run the actual containers inside the Pods, managed by Kubelet and kube-proxy for networking.
5. Produces a running app that is distributed, scalable, and self-healing in nature.

Over to you: Have you used Docker or Kubernetes in your projects?

---

## Batch vs Stream Processing

Data never stops flowing, but how we process it makes all the difference. When building data systems, two main approaches emerge: batch processing and stream processing. Both have their place, depending on whether you need accuracy over time or immediate insights.

![](https://substackcdn.com/image/fetch/$s_!P-gB!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8c9090b5-77c7-4f04-88bc-481df27de32d.tif)

Batch Processing: Collects data in chunks and processes it at scheduled intervals, great for reports and historical analysis.

Stream Processing: Processes events continuously in real-time, powering dashboards, alerts, and recommendations.

Batch = high-volume, historical accuracy.  
Stream = low-latency, real-time action.

Over to you: Which do you find harder to scale, batch pipelines or real-time streams?

---

## What are Modular Monoliths?

A modular monolith is an architectural pattern that divides an application into independent modules or components. Each of these modules has well-defined boundaries that group related functionalities. Doing so results in better cohesion.

![](https://substackcdn.com/image/fetch/$s_!f0s-!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb6d1ef48-faea-4d57-b2ea-f8411efc8334_2360x2770.png)

Here are the main characteristics of modular monoliths:

1. The modules are independent.
2. Each module provides a specific functionality.
3. Each module should expose a well-defined interface.

What is the main advantage of modular monoliths?

A monolith clubs all the functionalities into one big deployment unit. This makes monoliths simple to understand.

Microservices distribute the functionalities into separate deployable units. This makes them more scalable.

However, A modular monolith divides the application into modules that are part of the same deployment unit. They combine the simplicity of traditional monolithic applications with the flexibility of microservices.

In other words, you can have the best of both worlds with modular monoliths.

So - have you used modular monoliths to build applications?

---

## Popular interview question: What is the difference between Process and Thread?

![Image](https://substackcdn.com/image/fetch/$s_!MDHC!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7cf3f3a0-726f-47a3-94e4-755fa9aa8036_2196x2319.jpeg)

Main differences between process and thread:

- Processes are usually independent, while threads exist as process subsets.
- Each process has its own memory space. Threads that belong to the same process share the same memory.
- A process is a heavyweight operation. It takes more time to create and terminate.
- Context switching is more expensive between processes.
- Inter-thread communication is faster for threads.

---

## How AI Agents Chain Tools, Memory, and Reasoning?

![Image](https://substackcdn.com/image/fetch/$s_!JDKz!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01195e6a-77eb-406d-8972-f5cc5e7b99ab_2360x2920.png)

1. Reasoning: This is the brain of the AI agent. It receives the user’s goal as a query and uses its reasoning agent (using frameworks like ReAct) to break the goal into a series of smaller, logical steps.
2. Tools: For each step, the agent selects an appropriate tool. These can be external programs or APIs that it can call upon, such as a web search, a calculator, a code interpreter, or documents.
3. Memory: This is like the notebook. The agent records the outcome of each tool’s use in its memory. This notebook allows it to learn from results, maintain context over long conversations, and refine its plan based on new findings.

This continuous loop of reasoning, acting with a tool, and remembering the outcomes creates a chain. Finally, when the agent is satisfied that it has fulfilled the user’s query, it responds to the user.

Over to you: Have you used AI agents?

---

## Help us Make ByteByteGo Newsletter Better

TL:DR: Take this 2-minute survey so I can learn more about who you are, what you do, and how I can improve ByteByteGo

---

## SPONSOR US

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **sponsorship@bytebytego.com.**