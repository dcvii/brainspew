---
title: "Portfolio: A Knowledge Base Built on Files"
source: https://www.workings.co/p/portfolio-a-knowledge-base-built?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd06724d6-6ead-4417-a210-7185c1439db0_976x1031.png&open=false
author:
  - "[[Stowe Boyd 1]]"
published: 
created: 2025-03-11
description: How to organize, find, and link information managed in Obsidian, as minimally as possible.
tags:
  - clippings
---
### How to organize, find, and link information managed in Obsidian, as minimally as possible.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd06724d6-6ead-4417-a210-7185c1439db0_976x1031.png)

A segment of my Obsidian graph, centered on the ‘+disaffected’ concept.

---

---

In an earlier installment in the *Portfolio* series — *[Portfolio: How Notetaking Becomes Knowledge](https://www.workings.co/p/portfolio-how-notetaking-becomes)* — lays out the goals for Portfolio, and an initial use case. I recommend reading that before this.

---

### Keeping Track

There is no shortage of advice on organizing information — writing, clippings, images, PDFs, charts, and relationships between them — in Obsidian. Some practitioners have made it their life’s work to create a foolproof system to do just that.

This post is not an analysis or review of those approaches. I will leave that to others or the practitioners themselves. Instead, this post is an exposition of what I refer to as a ‘knowledge base’ in Portfolio, the approach I have developed over the years to manage various classes of information in a relatively stable taxonomy.

These taxa (the plural of taxon, an element of a taxonomy) include concepts, people, organizations, and others.

### Taxa Are Represented by Files, Not Other Information Management Constructs

A simple use case: I’ve clipped an article from the web (using the Official Obsidian Web Clipper), and as I encounter an important concept, I’d like to mark it in some way so that subsequently finding it — and others similarly marked — is easy. Here’s a paragraph in the article:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8fff5aff-b78d-4d51-bc6f-d71c9e5374d5_962x184.png)

I want to capture the mention of ‘Fobazi Ettarh’ and the concept ‘vocational awe’. To create a new people note in the knowledge base, I rely on a small plugin called ‘Link with Alias’, which creates aliased linked between files. It works like this. I add a ‘@’ at sign in front of the person’s name and select the @ sign and name, and hit the shortcut I’ve selected in the plugin, which leads to this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3d30978f-3f12-4e38-a263-b57b74274f8d_967x44.png)

I then delete the second ‘@’, and hit return. This will create a note in my knowledge base called ‘@Fobazi Ettarh’, with an aliased link from the initial note:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff9063922-bae1-4832-8023-f76d62f5135f_1035x508.png)

Notice that an alias to the file has been created based on the text after the pipe in the wikilink, ‘Fobazi Ettarh’. I didn’t have to open that note manually at the time of creation, but I can at some point in the future. I can also add other aliases in the future. For example, it’s common to refer to a person using just their last name, so I very commonly add that as an alias, too.

For the concept ‘vocational awe’, the process is similar, but I use a ‘+’ as the first letter instead of the people marker, ‘@’. Note that I have linked ‘@Fobazi Ettarh’. Here’s that note, which months after creation, not looks like this, and is in use in four files as we see from the backlinks:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbd4c78d9-7c6f-451e-9b93-39c879d5ff09_975x715.png)

In this case, I’ve created three aliases with Link with Alias. The first alias deals with a concept appearing at the start of a sentence and is capitalized.

Once created, aliases can be used directly, simply by typing two brackets and the alias, and then selecting from the popup:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c2d2866-a4cc-4c46-82ac-bfa349ed0b7a_525x330.png)

### Why Notes, As Opposed to Tags or Note Properties?

For years, I relied on tags as a means of organizing notes. I have several reasons for making the switch to note references.

First, tags are added to notes or sections of notes out-of-line, whereas references to ‘@Fobazi Ettarh’ or ‘+disaffected’ occur inline and, when aliased, read as the original text was written.

Secondly, tags are managed in a quite different way than wikilinks, in their own taxonomy, one that stands to one side of folders and notes.

Thirdly, many of the most widely used approaches to leveraging tags rely on quite complex plugins — like Dataview — that introduce new data-oriented approaches to organizing information in Obsidian but which are not native to the platform. It is well-known that the folks at Obsidian are working on an alternative to Dataview, but one which might operate in significantly different ways. As a result, I have decided to wait and see, and in the meantime, rely on wikilinks as the primary tool for organization of — and relationships between — notes.

---

---

### Where do the notes reside?

I rely on another plugin — Auto Note Mover — that uses text matching rules to move notes to specific folders. Concepts and people each have their respective folders in a parent ‘00 knowledge’ base folder:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fff507551-d3a6-4640-9068-8921fbc2fd8f_293x508.png)

Along with concepts and people, there are also events (like ‘∞Hurricane Milton’), images (‘2025-03-06 ¡impact of covid on WFH’), organizations (‘ºTesla’), places (‘~Los Angeles California’), projects (‘•portfolio’, or ‘•booklets project’), queries, and works (like ‘©What’s the Matter With Kansas’).

Each taxon starts with a distinctive first character, which makes rules for their auto moving easy, but also makes it easy to differentiate between a common term like ‘universalism’ with the concept of ‘+universalism’ as political philosophers apply it.

Note also that the backlinks on each taxa note show all references to the note:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F368718c9-62b6-4afc-aa6f-8d917d06d2cf_1032x623.png)

And, of course, a plain vanilla search would lead to the same results, and the use of the ‘+’ means only the references to the concept are found, and all everyday uses of ‘universalism’ are filtered out:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc3a7ae04-9be7-41f7-9625-e74e08ae1ab6_295x690.png)

### What About The Other Taxa?

Some of the other taxa are quite simple, like ‘works’, which are things like books, articles, or works of art, such as the book ‘©Cognitive Capitalism’. Organizations are obvious, like ‘ºApple’ and ‘ºCornell University’.

But others, particularly ‘projects’, are quite sophisticated, and that’s why the next in the series will be dedicated to work management in Portfolio.

### One Final Metaphor

Writing about the Portfolio taxonomy disconnected from the daily flow of my notetaking makes it seem just a bunch of links. But in day-to-day use, the taxonomy constantly provides scaffolding for my work.

For example, I was struck the other day by a quote from the ancient Greek historian Thucydides in an article by Jonathan Kirshner:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6fc1a50f-cc3f-4c73-ab99-07f305fa6ff2_991x260.png)

I imported the article, linked the references to the ‘@Thucydides’ note in the knowledge base, and traversing the graph, I saw this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6d9575f6-ac1f-411f-805e-8554e0dbbe0c_984x632.png)

I followed the link to a W.H. Auden poem I had filed away in 2023, entitled ‘September 1, 1939’… and found this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7cbe77e8-2527-4ee4-85a9-ce2934b7950e_1024x334.png)

When I captured that poem in my notebook in 2023 I could not have known how it would shade my understanding of Kirschner’s 2025 article. And that through a reference to Thucydides, whose *History of the Peloponnesian War* was unfinished at his death in 411 BC.

That’s why all the linking and annotation is worth the work.

---

---

Beyond the paywall are the settings for the Auto Note Mover plugin.

## Keep reading with a 7-day free trial

Subscribe to Workings to keep reading this post and get 7 days of free access to the full post archives.

[Already a paid subscriber? **Sign in**](https://substack.com/sign-in?redirect=%2Fp%2Fportfolio-a-knowledge-base-built%3Fimg%3Dhttps%253A%252F%252Fsubstack-post-media.s3.amazonaws.com%252Fpublic%252Fimages%252Fd06724d6-6ead-4417-a210-7185c1439db0_976x1031.png%26open%3Dfalse&for_pub=workings&change_user=false)