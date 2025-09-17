---
title: "Nushell in a Nutshell"
source: "https://dataengineeringcentral.substack.com/p/nushell-in-a-nutshell?publication_id=1224799&post_id=165210253&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2025-06-09
created: 2025-06-09
description: "guest post by Anonymous Rust Dev"
tags:
  - "clippings"
---
### guest post by Anonymous Rust Dev

![](https://substackcdn.com/image/fetch/w_424)

> *It's the Anonymous Rust Dev back unbidden, trying to pry the Python from your cold... errr, I mean, sell you on new things.*

You know the drill... A file comes across your desk, and you want to know what's in it. Perhaps you're one of those individuals who receives a 4 GB text document and attempts to open it with Excel or Notepad.

You may have a bash command that you reach for to grok its contents, or a fancy GUI application, or perhaps with all those fancy Python skills, you code up a throwaway application to scry its contents. And you've even reached for something like [xonsh](https://xon.sh/tutorial.html), allowing you to ply your Python skills directly within the shell.

I submit, however, that there may be **a better way**. In today's episode of "Not Another Rust-based Tool," I present [Nushell](https://www.nushell.sh/).

![](https://substackcdn.com/image/fetch/w_424)

> Obviously, one person's " *better* " is another person's no-thank-you. **Hopefully, I can win you over to my side with some persuasive arguing**...

## New shell?

Okay, it's time for a confession. When presented with the above problem, in the past, I would have reached for some unconventional tools. For instance, the [NodeJS repl](https://nodejs.org/en/learn/command-line/how-to-use-the-nodejs-repl) is a useful tool for looking around in JSON files.

Firefox does a bang-up job of graphically representing my XML documents. And let's be clear: this isn't a new problem - several years' worth of developers beating their heads against files have given us tools like head or [yq](https://github.com/mikefarah/yq) that can be strung together in the command line.

Perhaps my favorite (and most controversial) pick, though, has long been [Microsoft PowerShell](https://learn.microsoft.com/en-us/powershell/). Yeah, you heard me right, I'm one of those M$ fanbois - or, rather, used to be.

Because at the end of the day, I am more interested in working with data structures than arcane text parsing utilities (*looking at you,* `awk` *and* `xargs`). My favorite part of the Perl language is where you tell the commands to `die` \- I love me some regex, but no way am I using that language to wrangle with a text document.

So, why PowerShell? The answer is simple: everything is backed by a data structure, even if it's something simple like `System.Object`. Once you are in the rich type system of.NET, you also get the opportunity to use its vast system libraries to work with objects.

Below is an example of how I might scrape a folder's worth of XML contents for a particular node, grab the first 10 hits, and tabulate the results:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/56430da0-8c95-4f14-ae27-8e4477be1b4d_2000x930.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:677,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:279295,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F56430da0-8c95-4f14-ae27-8e4477be1b4d_2000x930.png%22,%22isProcessing%22:false,%22align%22:null})

Maybe then I want to know, after getting a peek, what the volume is - I can build on those results with a fancier piped command:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/b0148b22-24bf-44de-a758-9a76e238c8c7_2000x1042.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:759,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:341097,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb0148b22-24bf-44de-a758-9a76e238c8c7_2000x1042.png%22,%22isProcessing%22:false,%22align%22:null})

Okay, so that gets clunky fast, and admittedly, it took a bit of effort to write. I've lived with this pain for some time, so when I started hearing whispers of Yet Another CLI that does the same kind of work, I was already feeling a bit jaded.

Also, this happened at the same time as I was trying to learn the Fish shell (*also Rust-based; can't let an opportunity slip to plug it*). Well, whatever, I'll at least see what the fuss is about.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/176750b4-fb89-4485-9295-64a82aab09a6_1924x1064.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:805,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:372554,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://github.com/nushell/nushell%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F176750b4-fb89-4485-9295-64a82aab09a6_1924x1064.png%22,%22isProcessing%22:false,%22align%22:null})

So, [Nushell](https://www.nushell.sh/)... The landing page has a few quick illustrations and some installation commands for some hand-picked package managers. What immediately becomes apparent, though (*partly because they literally say it in the heading*) is that the data is structured.

In one example, they pipe the results of an HTTP GET into the `get` command, which only works because it implicitly parses the document (JSON-based):

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/6d196e04-0f1d-4b15-ad16-6aa77cd53ebf_2000x670.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:488,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:148217,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6d196e04-0f1d-4b15-ad16-6aa77cd53ebf_2000x670.png%22,%22isProcessing%22:false,%22align%22:null})

Or, maybe I don't want all that and just want the license name:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/cc5289b1-e0ac-48fd-9c72-9d93a22b0e88_2000x446.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:325,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:98326,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcc5289b1-e0ac-48fd-9c72-9d93a22b0e88_2000x446.png%22,%22isProcessing%22:false,%22align%22:null})

Above, in a single terse and easy-to-read statement, I've fetched a JSON document, parsed it, and run a nested property selector. Of course, you could have accomplished the same with other tools, e.g.:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/09b9a899-4d77-4a09-afb0-fd219661d506_2000x446.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:325,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:99064,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F09b9a899-4d77-4a09-afb0-fd219661d506_2000x446.png%22,%22isProcessing%22:false,%22align%22:null})

Thus far, it has not been a game changer, but I have to admit that the [Nushell](https://www.nushell.sh/) version looks nicer. We're going to need to look harder to find a justification to stay on this course, I think.

## Crash course

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/0f718731-f6d1-4887-8d3f-c5094756cbe9_1924x1064.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:805,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:312203,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://www.nushell.sh/book/%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0f718731-f6d1-4887-8d3f-c5094756cbe9_1924x1064.png%22,%22isProcessing%22:false,%22align%22:null})

A disclaimer - I'm new to this, so I need to review the documentation as I proceed. The [Nushell Book](https://www.nushell.sh/book/nu_fundamentals.html) will present more information than I plan to give here, and I'd recommend to the curious that they check it out for themselves. **That said, I can hand-pick some of its elements to pave the way.**

### Some random examples

First, as a shell, it's designed to be usable by anyone who's used the likes of bash or zsh. Many (not all) of the same commands (`ls`*,* `cd`*, etc.*) have Nushell-specific implementations, and it will fall through to system commands (*for instance,* `cat`) when it doesn't itself have a built-in alternative.

Unless you're doing some kind of fancy bash semantics, chances are you could switch shells without having to learn anything new, and get all the fancy UI benefits from how Nushell formats results. For illustration, consider a directory listing in bash vs. nu:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/b840e539-3dcc-47e6-9aa2-0e32d29bca4f_2000x1080.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:786,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:351423,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb840e539-3dcc-47e6-9aa2-0e32d29bca4f_2000x1080.png%22,%22isProcessing%22:false,%22align%22:null})

vs

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/99fd6db8-6b58-43c7-bcf8-98b3e804a6f1_2000x1192.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:868,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:346250,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F99fd6db8-6b58-43c7-bcf8-98b3e804a6f1_2000x1192.png%22,%22isProcessing%22:false,%22align%22:null})

You'll instantly notice the `#` column - tabulated results come back with row index, making it easier to work with a single result. You might also notice less information coming from Nushell, which by default holds a bit back -- we can force the issue with an argument:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/039090ec-b82f-4501-87e3-4cc7c1da4868_2000x1898.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1382,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:645696,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F039090ec-b82f-4501-87e3-4cc7c1da4868_2000x1898.png%22,%22isProcessing%22:false,%22align%22:null})

The first apparent difference in this output from bash is just how *readable* it is - sizes and times have type-aware context, the table columns are more clearly delineated, and if you're foolish enough to run the same command on a narrow screen:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/2a9a0aa5-1ecc-4a82-a72a-8b8fb02d027c_2200x1154.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:764,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:412865,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a9a0aa5-1ecc-4a82-a72a-8b8fb02d027c_2200x1154.png%22,%22isProcessing%22:false,%22align%22:null})

...it collapses remaining columns, keeping things presentable. So, what if I want to know more about that #0 (access\_log) entry? I can pipe that index into the `get` command we saw earlier to learn more:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/33670900-c58b-4e00-93f7-c65cd8f188c1_1800x968.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:783,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:186354,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F33670900-c58b-4e00-93f7-c65cd8f188c1_1800x968.png%22,%22isProcessing%22:false,%22align%22:null})

Nice. What if I wanted to know more about that `modified` property?

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/d0e6984c-8d31-4f66-b172-39d476d6337f_1800x446.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:361,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:105987,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd0e6984c-8d31-4f66-b172-39d476d6337f_1800x446.png%22,%22isProcessing%22:false,%22align%22:null})

> *The getter correctly navigates object hierarchy in the same way* `jq` *or* `yq` *would. Additionally, now that we have more screen real estate, it gives us the backing time that backs that "hour ago" language. Under the hood, that's because we are dealing with the [Datetime](https://www.nushell.sh/lang-guide/chapters/types/basic_types/datetime.html) data type.*

Likewise, with the file size:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/dbdc0f89-79f4-4d10-9a23-15a112d4bde4_1800x446.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:361,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:90154,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdbdc0f89-79f4-4d10-9a23-15a112d4bde4_1800x446.png%22,%22isProcessing%22:false,%22align%22:null})

Maybe you don't want it to automatically choose the units? You can use some math to coerce the units:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/85f21788-aae5-46a1-afbb-e4947fda1cf3_1800x632.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:511,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:143497,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F85f21788-aae5-46a1-afbb-e4947fda1cf3_1800x632.png%22,%22isProcessing%22:false,%22align%22:null})

Oh yeah, we are indeed doing math on the command-line prompt:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/529e49c8-3762-4d66-88d5-729d8e558357_1800x856.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:692,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:173988,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F529e49c8-3762-4d66-88d5-729d8e558357_1800x856.png%22,%22isProcessing%22:false,%22align%22:null})

Here, you can see me naively trying something and failing. These are its Rust roots in action - informative error messages will guide you to the correct answer, as happened here.

I attempted to use the wrong math operator, which the authors correctly thought I might try and guided me to the appropriate selection.

> Now, what happens when we use a command that isn't directly offered by Nushell? I happen to know of one such example:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/0adcf64e-814a-4f3a-b65b-f36971e4c72c_1800x894.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:723,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:279056,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0adcf64e-814a-4f3a-b65b-f36971e4c72c_1800x894.png%22,%22isProcessing%22:false,%22align%22:null})

Lame. It just piped out to the boring text-based `df` shell command. But, Nushell has our back in situations like this:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/d4fe87ef-86ad-46e7-a324-33cd687263cc_2512x968.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:561,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:313315,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd4fe87ef-86ad-46e7-a324-33cd687263cc_2512x968.png%22,%22isProcessing%22:false,%22align%22:null})

Don't get too excited just yet - the fact that those numbers are left-aligned (*including the Use%*) tells me that this was parsed as text. However, once again, we have a Nushell way to work with this data:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/9baea128-25bc-403e-a3a6-9e49e73291e9_2512x968.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:561,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:324401,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9baea128-25bc-403e-a3a6-9e49e73291e9_2512x968.png%22,%22isProcessing%22:false,%22align%22:null})

### Tables

Tabular data is a [first-class citizen](https://www.nushell.sh/book/types_of_data.html#tables) in Nushell. Our `ls` and `df | detect columns` illustrations above come back in this format, and give us enormous opportunity to work with data in the command line.

What if we didn't want to know the Used or Use% figures in the first place?

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/8f571eeb-f470-4623-b65d-54be08c0c7d5_2400x1004.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:609,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:311543,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8f571eeb-f470-4623-b65d-54be08c0c7d5_2400x1004.png%22,%22isProcessing%22:false,%22align%22:null})

Perhaps it would be easier just to have instead selected the columns we wanted:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/81b0048f-152f-4b72-ae94-af696e481d99_2000x968.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:705,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:229430,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F81b0048f-152f-4b72-ae94-af696e481d99_2000x968.png%22,%22isProcessing%22:false,%22align%22:null})

Filtering is intuitive, as long as you're aware of the available [operators](https://www.nushell.sh/book/operators.html) (also see [this](https://www.nushell.sh/book/nushell_operator_map.html) if coming from another language):

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/05c7056a-bb2f-4e3e-b046-af395048432f_2000x1080.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:786,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:313430,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F05c7056a-bb2f-4e3e-b046-af395048432f_2000x1080.png%22,%22isProcessing%22:false,%22align%22:null})

And, we can sort this stuff as well (but remember the fact that this data is currently text-based):

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/287568a1-12e7-4828-b13d-95935c2ec1dd_2512x968.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:561,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:313749,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F287568a1-12e7-4828-b13d-95935c2ec1dd_2512x968.png%22,%22isProcessing%22:false,%22align%22:null})

If you've followed me this far, you may be wondering about some of the practical implications of this tabular data. Out of the box, there is built-in support for various data types (see [Opening files](https://www.nushell.sh/book/loading_data.html#opening-files) for the current list).

It's a small but useful list at the moment includes popular formats like CSV/TSV, JSON, yaml, and even Excel documents. Perhaps my own favorite would that it also reads from [SQLite](https://www.nushell.sh/book/loading_data.html#sqlite), complete with the ability to specify the data source via query - alternatively, if you just open the database, you end up with a hierarchical object where the tables are represented as key-value pairs, where the key is the table name and the value the table's contents.

### Reading data

Alluded to above is the fact that we can import data from sources. Early on we saw the `http get` command, just now the `open` command, and somewhere along the way we even composed a table de novo. Maybe the format you're looking for wasn't in the supported list I linked to, or you want a better way to get data.

Well, as I said, this is a Rust-based project, so of course they had to go and make a way for you to [use Polars](https://www.nushell.sh/book/dataframes.html). It requires an additional plugin to make it work, which the linked page gives more help on. I'm sure the creative among you can figure out how to access even more file formats from this point, including Parquet.

In a pinch, you can also just pipe your content in:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/57966ef6-c1ba-4887-863b-1f2d9f8ab49d_1600x632.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:575,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:121762,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F57966ef6-c1ba-4887-863b-1f2d9f8ab49d_1600x632.png%22,%22isProcessing%22:false,%22align%22:null})

Finally, if you have the Rust chops and think something important is missing from those formats, you could always write your own plugin.

### Lists, and records

Not everything's a table. I spent the most time on tables because I expect that's where my audience is at, but we also need to consider other types.

Lists are exactly as you'd think - heterogeneous collections of values.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/de3c9944-57b3-4b65-8ba4-230668b0fa31_1600x1154.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1050,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:166773,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fde3c9944-57b3-4b65-8ba4-230668b0fa31_1600x1154.png%22,%22isProcessing%22:false,%22align%22:null})

A simple transformation:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/90e40fc2-3d96-411f-89ea-4720274de139_1600x632.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:575,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:110695,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F90e40fc2-3d96-411f-89ea-4720274de139_1600x632.png%22,%22isProcessing%22:false,%22align%22:null})

...and going a step further, creating an array of "records", leads to an accidental Table:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/c52446c5-ff5c-44d3-b0f2-0fa316771e60_1600x708.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:644,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:114289,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc52446c5-ff5c-44d3-b0f2-0fa316771e60_1600x708.png%22,%22isProcessing%22:false,%22align%22:null})

In that last example, we effectively ended up with a value akin to:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/2d232008-5186-4cfa-9852-791148a50e64_1600x708.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:644,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:110736,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2d232008-5186-4cfa-9852-791148a50e64_1600x708.png%22,%22isProcessing%22:false,%22align%22:null})

A record is defined with a [syntax largely similar to JSON](https://www.nushell.sh/lang-guide/chapters/types/basic_types/record.html#record-literal-syntax). Getting around in these should hopefully be intuitive, but the [docs](https://www.nushell.sh/book/navigating_structured_data.html#index-to-this-section) may nevertheless offer some insights.

The big thing that I think will trip people up is the array accessor - don't use `$var[3]` to access the `3` index, but instead use the dot operator `$var.3` (or the earlier mentioned `get` command, `$var | get 3`). Instead, think of arrays/tables as objects whose keys are the positional indexes.

Revisiting the GitHub repo illustration (`http get https://api.github.com/repos/nushell/nushell`), we'll find a JSON document similar to the following (redacted heavily for brevity):

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/8e5399fb-1071-48a4-bec4-3294ad001e0f_1600x1080.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:983,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:187198,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8e5399fb-1071-48a4-bec4-3294ad001e0f_1600x1080.png%22,%22isProcessing%22:false,%22align%22:null})

Treating this stripped-down document as an object, we'd end up with:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/7a3b3e5e-8ea3-47ee-91c7-84142fc383f5_2000x1564.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1139,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:319717,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7a3b3e5e-8ea3-47ee-91c7-84142fc383f5_2000x1564.png%22,%22isProcessing%22:false,%22align%22:null})

From here, we could access individual properties:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/3b87fdbd-8728-498e-b7a3-9d63a6d77963_2000x596.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:434,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:153853,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b87fdbd-8728-498e-b7a3-9d63a6d77963_2000x596.png%22,%22isProcessing%22:false,%22align%22:null})

That JSON-like syntax being used is called [NUON](https://www.nushell.sh/book/loading_data.html#nuon), which is a bit looser in some regards (e.g. automatic string inference allowing for optional quotes, comments are supported).

### Saving (and converting) data

I didn't find much help from The Book, but I did take a stab at guessing what the command might be called. As with `open`, there's a corresponding `save`:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/d01b2a0f-c074-44d0-aa36-f902baeff5bc_2000x1898.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1382,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:418429,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd01b2a0f-c074-44d0-aa36-f902baeff5bc_2000x1898.png%22,%22isProcessing%22:false,%22align%22:null})

Reading between the lines, it seems to be file-type aware. Building off our last CSV example, let's see if we can cast our table to JSON:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/bdea71f4-c21b-4f66-9344-fc6e50dad0c7_2000x894.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:651,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:148957,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbdea71f4-c21b-4f66-9344-fc6e50dad0c7_2000x894.png%22,%22isProcessing%22:false,%22align%22:null})

Be aware of the list - in particular, the `to <xxx>` commands, as they will indicate the valid output formats you can use to save files. Really, relying on the `save` command to cast your data is shorthand for `$data | to <fmt> | save --raw <dest>` \- just in case you need to take ownership of the format.

### Scripting

It's a shell, so of course it comes with its own scripting layer. It takes cues from its daddy Rust, in case you're wondering what's up with that goofy [closure](https://www.nushell.sh/lang-guide/chapters/types/basic_types/closure.html) syntax we saw in our column casting illustrations earlier.

#### Variables

The simplest (and perhaps most useful to you) thing you might need to know right now is how to do assignments:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/e78cb605-d3cd-4d6f-8574-8a08dd97589a_2000x484.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:352,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:110480,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe78cb605-d3cd-4d6f-8574-8a08dd97589a_2000x484.png%22,%22isProcessing%22:false,%22align%22:null})

All those times I went through that `df | detect columns` business, I could have just instead done something like:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/1cd5c1c5-3607-4bc6-883d-6db851e47639_2000x596.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:434,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:139762,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1cd5c1c5-3607-4bc6-883d-6db851e47639_2000x596.png%22,%22isProcessing%22:false,%22align%22:null})

But, keep in mind Nushell's Rust roots. By default, variables are immutable:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/11d8caf6-cf1e-44f1-8c73-5a7fbe15fd43_2000x1302.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:948,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:282137,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F11d8caf6-cf1e-44f1-8c73-5a7fbe15fd43_2000x1302.png%22,%22isProcessing%22:false,%22align%22:null})

#### Flow control

All the standard stuff (`if` [/](https://www.nushell.sh/lang-guide/chapters/flow_control/if-else.html) `else`, `for`, `while`) can be expected to do the usual stuff. As with Rust, parentheses are optional around the block conditions.

Unlike Rust, though, most of those commands are statements, not expressions (meaning, no return values). The exception here is the `match` expression, which occupies the same role as `switch` would in other languages:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/b0d0e3cc-2e00-4c1b-aa51-5f1477c4b965_2000x596.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:434,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:117835,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb0d0e3cc-2e00-4c1b-aa51-5f1477c4b965_2000x596.png%22,%22isProcessing%22:false,%22align%22:null})

Of course, you're not required to have `match` return anything:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/5a52f160-a54d-43ea-8ce6-4842f06db30e_2000x708.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:515,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:149159,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5a52f160-a54d-43ea-8ce6-4842f06db30e_2000x708.png%22,%22isProcessing%22:false,%22align%22:null})

#### Functions

Not everything needs to be a closure. In fact, they're hard on the eyes, and there's a better way (if you don't need the closure scope, that is).

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/9d9f06f7-8210-40af-84d6-8f06649d0028_2000x782.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:569,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:163023,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d9f06f7-8210-40af-84d6-8f06649d0028_2000x782.png%22,%22isProcessing%22:false,%22align%22:null})

And, with strong types:

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/4745ba64-fdc5-42be-bb07-9bbd0438d348_2000x1116.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:812,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:217722,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165210253?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4745ba64-fdc5-42be-bb07-9bbd0438d348_2000x1116.png%22,%22isProcessing%22:false,%22align%22:null})

Whether you care about types or not is your business, but if you accept loose values you should be prepared to deal with the ramifications (e.g. casting in your functions).

I'd recommend getting familiar with The Book's section on [Scripts](https://www.nushell.sh/book/scripts.html) if this seems like something you'd want to pursue.

## Takeaways

Changing shells can be an ordeal, particularly if you don't know the advantages of doing so. Hopefully, you've seen how easily you can explore your data without reaching for a plethora of other tools, as well as the quality-of-life improvements it offers over boring old Bash.

> Its native support for structured data and assorted data types, coupled with an expressive programming syntax, should hopefully sway you to consider this in lieu of whatever boring shell your computer currently has going on.

This article only scrapes the surface, and there are some awesome features (e.g. [parallelism](https://www.nushell.sh/book/parallelism.html)) I didn't even get to touch here. Also, while I chose to focus on the ETL side of things, this is also a fully functional CLI shell intended to do almost everything that your current shell of choice does with minimal pain and lots of eye candy.

The [Coming to Nu](https://www.nushell.sh/book/coming_to_nu.html) section should hopefully make a transition to Nushell a straightforward and easy process if you're willing to give it a try.

> Also, an important aside: nobody seems to be talking about how "Nushell" sounds like "Nutshell", which when translated to German is "Nussschale" - which also sounds suspiciously like Nushell to me. I feel like there's a missed opportunity there somewhere.