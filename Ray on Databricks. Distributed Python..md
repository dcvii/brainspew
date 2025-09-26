---
title: Ray on Databricks. Distributed Python.
source: https://dataengineeringcentral.substack.com/p/ray-on-databricks-distributed-python?publication_id=1224799&post_id=162365203&isFreemail=false&r=7br8e&triedRedirect=true
author:
  - "[[T50/Daniel Beach]]"
published: 2024-12-11
created: 2025-05-01
description: Machine Learning and AI Mastery
tags:
  - clippings
---
### Machine Learning and AI Mastery

![](https://substackcdn.com/image/fetch/w_424)

I haven’t used [Ray](https://docs.ray.io/en/latest/index.html) much in my life, just a few times. Recently, when working on some LLM stuffy-stuff, I managed to find myself setting up a [Ray cluster](https://docs.ray.io/en/latest/index.html) on Databricks for some distributed ML/AI work.

> *Lest you think I am some AI savant, tis not true, I still hold to the old axiom that 90% of all Machine Learning, including that fancy LLM stuff, is mostly the same ole’ Data Engineering.*

So, what I want to do today is nothing fancy: introduce you to **what** Ray is, **why**, and **where** you would use it. Then, I will show you some code examples of how I used Ray on Databricks to fine-tune an LLM model … to help drive home the concepts of what Ray provides.

![](https://substackcdn.com/image/fetch/w_424)

This is what ChatGPT thinks about Ray and its relation to data and ML.

![](https://substackcdn.com/image/fetch/w_424)

I agree with this assessment. What Ray seems to solve, in my experience …

- *making regular Python distributed on a cluster*
- *emphasis on Machine Learning/AI*

I want to walk through a code example at a very high level and just give you some high-level thoughts. I’m not trying to teach you HOW to run Ray on Databricks, but maybe spark (pun intended) some interest on your end and give you some basic knowledge.

## High-Level LLM Fine-Tuning Example - Ray on Databricks

The first thing to note is that Databricks has good introductory notes on how to run Ray on Databricks; [read them](https://docs.databricks.com/aws/en/machine-learning/ray/).

Note … since Ray is ML-specific, you will want two things …

- use a GPU Databricks cluster
- use DBR version ML 15.0 or >
	- *With Databricks Runtime ML 15.0 onwards, Ray is preinstalled on Databricks clusters.*

Also, with **most** machine learning and AI use cases, you will be using **WAY** too many Python packages, and you will have no choice. This will require some trial and error to get all the packages installed and working with the correct versions, etc.

> *This is very common for **ALL** ML workloads and nothing new. In my case, I was fine-tuning a BERT model. This is an example of the imports I had to use.*

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/8477b749-902d-4440-b3a3-6734671da7b7_1936x1004.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:755,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:282599,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/162365203?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8477b749-902d-4440-b3a3-6734671da7b7_1936x1004.png%22,%22isProcessing%22:false,%22align%22:null})

If you are working on a similar project, plan time into the project to get a Cluster running without errors. Next, if using an ML GPU cluster, you will most likely have to match your Ray cluster configs to your cluster size, etc. *(number of works, GPUs, CPUs available, etc.)*

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/492f7aad-c65f-4e89-a2a8-16607f6fee48_1818x1228.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:983,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:311548,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/162365203?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F492f7aad-c65f-4e89-a2a8-16607f6fee48_1818x1228.png%22,%22isProcessing%22:false,%22align%22:null})

Next, if we have a working Cluster and Ray is “working” without errors, we have to set up the “flow” of the ML Pipeline that is specific to Ray and run the code in a distributed manner.

The high-level steps will be …

- Set up your dataset and model.
- Define your single-worker training function. (*the part that needs to be distributed*)

> I am glossing over many details, but it is that simple with Ray; the complication comes from what ML library you are using and WHAT you are trying to accomplish.

Below is an example of Ray training a BERT model.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/f83d70a8-5cf2-42d0-a115-aaeb85e9e7f2_1800x1638.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1325,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:399006,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/162365203?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff83d70a8-5cf2-42d0-a115-aaeb85e9e7f2_1800x1638.png%22,%22isProcessing%22:false,%22align%22:null})

It’s obvious what this code is doing, isn’t it? Ray provides a Torch Trainer out of the box that we can use with BERT. But the magic really happens in the ***train\_func***.

**This is how Ray will distribute the work.**

> I know this looks like a lot of code, but it’s not, it’s just standard ML stuff … wrapped up inside a function that Ray can throw onto a Worker.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/f8cd4572-1a25-4a62-9c98-bfb5fe1fcf4c_2000x3426.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:2494,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:955583,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/162365203?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff8cd4572-1a25-4a62-9c98-bfb5fe1fcf4c_2000x3426.png%22,%22isProcessing%22:false,%22align%22:null})

So, if you have worked on ML workloads, this won’t be an unfamiliar code to you. Training most models... including LLMs is much like classic ML.

- pick your tooling of choice, torch, etc.
- massage your data to prep it for your model
- tokenize your data (LLM specific)
- write the training code to suit your need

It’s really about taking < *whatever Python code* \> and wrapping it in a function to be distributed. This can be seen in the below Ray example.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/10b9bd85-b129-405d-8488-7adadc567871_1600x708.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:644,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:142534,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/162365203?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F10b9bd85-b129-405d-8488-7adadc567871_1600x708.png%22,%22isProcessing%22:false,%22align%22:null})

We have a Python thing … and want to speed it up by distributing it on a cluster.

> **Why use Databricks?** Well, that’s obvious. I can speak from experience; creating your cluster from scratch and installing things for ANY tool isn't trivial.

Databricks ML runtimes (15.0+) come with Ray ready, and the Cluster is ready for use. This slices about 20%+ of work time off the project from the start. You can focus on getting your code running, not configuring clusters.

Also, Ray is helpful because it can distribute specific use cases that don’t work well with Spark, like LLM fine-tuning, etc.