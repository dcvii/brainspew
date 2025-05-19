---
title: "First Look: Note Annotations"
source: https://www.workings.co/p/first-look-note-annotations
author:
  - "[[Stowe Boyd 1]]"
published: 2022-02-27
created: 2025-03-11
description: Another approach to sidenotes in Obsidian.
tags:
  - clippings
---
### Another approach to sidenotes in Obsidian.

I read about a new plugin for getting an implementation of Tufte sidenotes in Obsidian. I’ve written about sidenotes a number of times, in particular [Obsidian Tufte-style Sidenotes](https://www.workings.co/p/obsidian-tufte-style-sidenotes), where I detail using an implementation by TfTHacker:

> *I was contacted by TfT Hacker just recently about a new development in the [Cornell Notes Learning Vault](https://tfthacker.com/cornell-notes), which I wrote about in [Using Cornell Notes CSS to ‘Fake’ Tufte-style Sidenotes](https://www.workings.tools/p/using-cornell-notes-css-to-fake-tufte). So it turns out that TfT Hacker wanted me to test a full implementation of Tufte-style sidenotes built into Cornell Notes. And it works.*

I really very heavily on sidenotes as a way to, honestly, leave notes for my future self when closely reading materials written by others, generally. I must have thousands by this point.

However, to be fair, the implementation relies on using markdown footnotes as the source of the notes, which is niddley: having to create the `^[` at the start of the note leads to `^{` a lot of the time (I am not a great typist). Also, in cases where I create a lot of sidenotes, the TfTHacker implementation can’t space paragraphs apart to allow room for all the sidenotes, and they will overlap, requiring extra manual reformatting, a real pain, but infrequent.

All that said, in general, the Cornell Notes sidenotes implementation works well.

But I am always open to see if something else works better.

---

---

### Note Annotations

The new plugin is Note Annotations, which adds an HTML comment following a highlight section of markdown to represent a sidenote. This is source mode:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd485323c-c1d6-4fe4-a5f7-2f0d4312a12f_817x170.png)

Edit mode, hovering over the highlighted commented text.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F673ee2b4-4223-4c05-a218-5d64179f0442_821x148.png)

And reading mode:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3cb33371-035a-47c5-92b0-14ead9d687bf_830x206.png)

Adding a note is pretty easy. After highlighting text in the normal way, mousing over the highlight and clicking leads to this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb501ef03-5c82-47d7-8b00-618eec2c00f6_852x169.png)

And clicking on the edit icon open a text window, where you type or paste the note content:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fadcdf681-fd38-4394-a925-11a833bd007f_821x303.png)

#### Problems Arise

Looks fine. But if I create more than one sidenote in a paragraph the HTML comments are added, like this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2c399328-3e26-4b07-b79a-254b0ddd6727_827x364.png)

But in reading mode, disaster:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F34504567-6cae-49ad-bd95-a36b6259c8bd_844x395.png)

All the comments overlap at the top of the paragraph. End of investigation, for me.

Contrast that with the Cornell Sidenotes implementation:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01e781ce-dd0d-459f-885b-4b41911040c0_857x398.png)

And I appreciate the numbering. Also, if I’d like to I can have all the sidenotes appear at the bottom of the note, as regular-old footnotes, which is sometime convenient, as when I have too many long sidenotes, and they overlap in the right margin. (For more info on that see [Obsidian Tufte-style Sidenotes](https://www.workings.co/p/obsidian-tufte-style-sidenotes).)

---

---

#### Oh, And Transclusion?

One last point: Note Annotations do work — in their limited way — when rendered through transclusions, like a clock reference. Here you can read the note that is reached through hovering over a block reference.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ae01797-e7c1-487f-ad12-6bfafee69db6_933x308.png)

---

---

#### Note Annotations is a non-starter with current limitations.

I can’t recommend Note Annotations for practical, everyday use as currently configured. It will have to support multiple notes per block.

I didn’t show all the odd behaviors, like getting text backwards like the example below. I typed ‘and another’ after the comment and note.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9ff29c25-39c1-47de-b11d-0b18d8310804_541x64.png)

And I haven’t yet tried other functionality in the tool, like extracting a highlight into a new file, which might be useful, or copying the highlighted text into the clipboard.

---

#### Subscribe to Workings

By Stowe Boyd · Launched 4 years ago

The tools we use to think, write, and remember.

6 Likes∙

[1 Restack](https://substack.com/note/p-157213369/restacks?utm_source=substack&utm_content=facepile-restacks)