---
title: "Portfolio: Tasks and Simple Projects"
source: https://www.workings.co/p/portfolio-tasks-and-simple-projects?publication_id=375885&post_id=160528342&isFreemail=true&r=7br8e&triedRedirect=true
author:
  - "[[Stowe Boyd 1]]"
published: 
created: 2025-04-05
description: Yes, Markdown supports tasks (minimally), but you need more to make them work.
tags:
  - clippings
---
### Yes, Markdown supports tasks (minimally), but you need more to make them work.

### Basic Taskology

Tasks are a built-in feature of the Markdown text formatting language. A text line like this:

`- [ ] this is something to do`

will be rendered in core Obsidian (without any plugins) in read or edit mode, as this

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F08661c05-34df-44f6-b548-b440ddf0b3fb_799x76.png)

Click on the box to convert the ‘state’ of the task from ‘open’ to ‘closed’ or ‘completed’.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F21cb57c1-e83e-41c6-b3a8-a2dbc788ca0c_778x89.png)

Also, tasks can be managed in lists:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4dfa8378-2392-4fd1-bc17-eb2ea563566f_795x162.png)

To create a bit more structure, tasks can be indented, making them an addressable group, not just a series of individually addressable tasks:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F29f6eae3-2d0b-41fb-9cd5-f43f2eca7940_798x177.png)

Notice that the top-most task, which a user might want to represent completing the list, does not automatically check itself off when the others are checked.

But the group of tasks is now a group with a shared block reference:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe6f69723-7716-4ce5-a260-ec1c7edc3bdc_809x529.png)

This leads to this, once applied:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5aa1fa24-8676-4383-abab-31fffbc8fed3_820x190.png)

Note the ‘^pzbs7r’ (which can be manually edited to be easier to remember). I can use that in block reference from any note, like this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01a3a707-9d85-43b2-810d-3ac2ae327507_846x201.png)

For many basic purposes — like creating a grocery list — that level of ‘project management’ may be sufficient. But for all serious work, more is needed.

### Extended Task States

Extended task states are the first significant enhancement of tasks that I rely on in Portfolio. Instead of being limited to just ‘open’ and ‘closed’, it’s possible to have an extended list of states using the Minimal theme and others. Here's the list of alternative states that I use at this time in Portfolio, grouped by classes:

`important`

`- [!] most important, urgent - only a few per formal project `

`- [>] queued - pull from queued and make urgent`

`active`

`- [/] working - in process`

`- [<] waiting - waiting on other tasks or people`

`- [ ] open - active but not started yet`

`inactive`

`- [?] maybe - unsure if it should be undertaken`

`- [i] info - supporting other present or future activities`

`- [-] - canceled `

`- [x] - closed, done, completed`

And here’s how they render with the Minimal theme:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F401d04f7-9d3f-43e6-856d-fe2e64c83a20_834x719.png)

Minimal supports more task states. Still, I have settled on this collection, and the groups allow me to array them when using queries to collate tasks based on project and other knowledge base taxa (see *[Portfolio: A Knowledge Base Built on Files](https://www.workings.co/p/portfolio-a-knowledge-base-built)* for a grounding on Portfolio’s knowledge base).

### Tasks and Projects Are All in Your Head

Task lists are not named but are implicitly activities comprising a project. The project could involve only a single task or a bunch of them. One convention is to use the parent task to indicate the project:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F90c56f44-f95e-40ad-9295-766534d8bd32_856x212.png)

There is only one active task in this ‘project’; everything else is on hold until that can be done. Note I had to manually edit the states of all the tasks to indicate their specific states, but there are plugins to help with that.[1](https://www.workings.co/p/portfolio-tasks-and-simple-projects?publication_id=375885&post_id=160528342&isFreemail=true&r=7br8e&triedRedirect=true#footnote-1-160528342)

Projects like these might be considered ‘simple’ projects: they have no other organizational overhead. There are all sorts of things in Obsidian that are simple or implicit projects. Whenever I clip something from the web into my vault, for example, there is an implied project to read (and annotate) that note and maybe take other actions, like writing something about it.

Generally, though, I tend not to rely much on simple projects because the informality and the number of projects that may be created over months or years make keeping track of things difficult.

In the next installment in the series, I will dig into a more formal and structured model for managing projects that form the heart of project management in Portfolio.

…

Before closing, here is a note on breaking one limitation on Obsidian’s tasks. Like Markdown, Obsidian requires that tasks start with the first non-blank letter on a line of text. But what if we could ignore that limitation and create tasks anywhere on a line, so long as the convention of a specific series of characters is retained, they can be found by search?

For example, the ‘fix the fence’ simple project could all be placed on a single line, carrying the same meaning:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6cbf360d-8c46-48e2-b89a-1cff6e9422ec_874x130.png)

Or, I might want to add a task to a block in some note by embedding the task in a footnote:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea6aafd0-61a5-4cdd-afcf-b06e316f8e05_879x214.png)

In read mode, the task state is not rendered prettily, but it can still represent a task in the reader’s mind [2](https://www.workings.co/p/portfolio-tasks-and-simple-projects?publication_id=375885&post_id=160528342&isFreemail=true&r=7br8e&triedRedirect=true#footnote-2-160528342):

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4488ef89-ff2a-459a-9f09-8e6910b42c23_881x266.png)

A search for all tasks regarding ‘forecasting’ would yield a list of such tasks, including the one from the footnote:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa9ad7b45-bf0e-445a-aaa2-96ad8034fff4_899x553.png)

As we shall see in the next installment — formal project management and endeavors — findability is more important than almost everything else.

## Keep reading with a 7-day free trial

[Already a paid subscriber?**Switch accounts**](https://substack.com/sign-in?redirect=%2Fp%2Fportfolio-tasks-and-simple-projects%3Fpublication_id%3D375885%26post_id%3D160528342%26isFreemail%3Dtrue%26r%3D7br8e%26triedRedirect%3Dtrue&for_pub=workings&change_user=true)