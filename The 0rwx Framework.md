---
title: "The 0rwx Framework"
source: "https://www.youtube.com/watch?v=E6-1u_savRs&t=12s"
author:
  - "[[No Boilerplate]]"
published: 2026-11-07
created: 2026-11-11
description: "We need new language to talk about AI. http://0rwx.com is my attempt.A labelling system is vital for domain experts to talk about AI in a clear way. The difference between the 4 levels is not necess"
tags:
  - "brainspew"
---
![](https://www.youtube.com/watch?v=E6-1u_savRs)

We need new language to talk about AI. http://0rwx.com is my attempt.  
  
A labelling system is vital for domain experts to talk about AI in a clear way. The difference between the 4 levels is not necessarily about what TOOL you use, but your ability to scrutinise the generated work.  
  
I have employed this simple framework to discuss my and others' work with less judgement and confusion, and I hope the 0rwx framework makes it just a little easier for you too.  
  
Article and links here https://www.namtao.com/0rwx/  
  
❤️ If you would like to support what I do, I have set up a patreon here: https://www.patreon.com/noboilerplate - Thank you!  
📄 All my videos are built in compile-checked markdown, transcript sourcecode available here https://github.com/NamtaoProductions/namtao-com this is also where you'll find links to everything mentioned.  
🖊️ Corrections are in the pinned ERRATA comment.  
👕 Bad shirts available here https://noboilerplate.org/  
  
🙏🏻 CREDITS & PROMO  
My name is Tris Oaten and I produce fast, technical videos.  
Follow me here https://namtao.com/@noboilerplate  
Website for the show: https://noboilerplate.org  
Come chat to me on my discord server: https://discord.gg/mCY2bBmDKZ  
  
If you like sci-fi, I also produce a hopepunk podcast narrated by a little AI, videos written in Rust! https://www.lostterminal.com  
If urban fantasy is more your thing, I also produce a podcast of wonderful modern folktales https://www.modemprometheus.com  
Season 4 of The Phosphene Catalogue is in pre-production, if you like mysteries and art, check it out! https://phosphenecatalogue.com/  
  
👏🏻 Special thanks to my patreon sponsors:  
\- Jaycee,  
And to all my patrons!

## Transcript

**0:00** · Hi friends, my name is Tris and this is No Boilerplate, where I focus on fast technical videos. Data centers, water use, job losses, what the hell is happening and more importantly, how do we talk about it sensibly? I don't have time to explain the former, but I hopefully can help with the latter. I have a simple mental framework to think and talk about AI work, which I'm calling zero RWX. This framework is easy to explain even to those with just a passing familiarity with the current state of tech. You can probably guess already and it's broadly applicable to any kind of generative AI tool.

**0:31** · Language is powerful. I have employed this simple framework to discuss my and others work without judgement or confusion over the last 6 months. But why did I need this in the first place? I dedicate my video scripts to the public domain. Everything you see here was written and recorded by me and the script links and images are part of a markdown document available freely on my website namtao.com and GitHub. Tell me if this has ever happened to you. I was enjoying using a new Obsidian plugin for organizing my writing, but kept finding that there was something strange with the software.

**1:05** · Things were not quite where I expected.

**1:07** · Features were slightly buggy or surprising. There was something entirely off about the whole thing. The maintainer was helpful and responsive, always happy to talk and fix bugs as I reported to them, but when I came across the third or fourth weird design decision, I realized that the problem ran deeper than just bugs. I read more about the project and the maintainer and quickly found a post confirming my initial suspicions. The plugin was vibe coded. Okay, that's disappointing, but I've used good vibe coded software before.

**1:37** · As a software engineer, I know that reliable systems can be made from unreliable parts. Fine, but what really hit me was when I realized that the maintainer was a writer, not a programmer. They had vibe coded the entire project, not just without reading the code, but without any frame of reference to know what good software design should be in the first place.

**2:00** · This realization caused two things.

**2:02** · One, I was greatly impressed that the state of technology and the attitude of this writer was such that non-programmers could now get exactly the software they want with no training.

**2:11** · And two, I uninstalled the plugin.

**2:14** · This experience was not the first time I'd had my heart broken, and the cause was labeling, not live coding itself. I resolved to find a framework that wasn't just the stages of grief. My early ideas about the zero RWX framework began, as so many things do, with reading an iconic tweet by Mitchell Hashimoto. This is fascinating, and I have a number of comments. I liked I read the code on principle, but I thought he didn't go far enough. I wanted something more like I write the code, not just read it.

**2:44** · Sure, I might short-circuit a particularly cryptic error by digitally pair programming with a chatbot, but personally, I prefer every character of what I write to be written by me. This is the thesis of brainmade.org. Head there for more of my thoughts on this topic. By the way, I'll mostly be using programming examples in this video, because that's what I'm familiar with, but the problems that using zero RWX solves are the same for anything you write, from a song to a sonnet. It's obvious that there are a few different levels of AI you can work with, and an all-or-nothing approach lacks nuance in discussion.

**3:15** · My feelings on what is the right level for me might not be the same as you or, too often, your boss. I wanted to find a few simple terms, like the ones that we use at a restaurant when ordering food for the table. I'm vegan, but you go ahead, I'll order the food that I'm comfortable with. Any vegetarians in the party? You're pescetarian, right? I'll eat anything.

**3:36** · It's easy to use these terms to figure out our individual preferences for what we want to put in our bodies.

**3:43** · This is what I want \[laughter\] for AI, and there is prior art here from the automotive industry regarding driverless car assistance levels. The five levels are: zero, no controls as a regular manual car; one, simple driver assist, lane beeps and adaptive cruise control; two, complex combined driver assist, like autopilot and lane following. This is the current state of the art at the time of recording, no matter what car company CEOs say. Three, automatic driving with human on standby. This does danger avoidance. Four, automatic driving but only in controlled circumstances, like highway route following.

**4:14** · And five, automatic driving in all conditions, never falling back to a human. This is a robot taxi, like a Johnnycab from Total Recall. The problem I found with existing AI categorization methods is that they're based on this automotive model, which is based in fantasy. We've been at level two for a decade, and it doesn't seem likely that we'll have full self-driving cars anytime soon. Making a car kickflip is easy. Ensuring it never kills a skateboarder in the street is not.

**4:38** · And the issue with higher levels is that the closer the automated cars get to perfection, paradoxically, the more dangerous they become on our streets.

**4:49** · This effect is famously described in the 1983 paper, Ironies of Automation, by Lisanne Bainbridge. And I promise this is relevant to AI. In it, she argues that once you automate nearly all of the work of a system, the human becomes complacent, and their skills atrophy, and their senses dull.

**5:06** · This means that it's very unlikely that they will be prepared to jump in when the machine fails. And even if they do, their skills may not be up to the challenge anymore. Rather than automation empowering unskilled operators, Bainbridge argues that they actually need to be trained differently to be ready to identify the rare but vital times that their intervention is needed. This is like the Japanese rail system of shisa kanko, pointing and calling. A simple procedure that reduces errors by up to 85% and is even used in the New York City Metro.

**5:36** · When automation becomes close to perfect, the operator skill set switches from being expert at the task to being expert at monitoring the machine doing the task. Do you see where I'm going with this? At high levels of AI automation, like with Claude code, I think people who say they read the code are lying to themselves. They can't. Not anymore, anyway. They have become an unreliable narrator of their own experience. Claude tested it for me doesn't cut it. We must be specific.

**6:08** · It's just me running this channel and I'm so grateful to everyone for supporting me on this wild adventure. If you'd like to see and give feedback on my videos up to a week early, as well as get private Discord access and even your name in the credits, it would be very kind of you to check my Patreon. I also offer regular mentoring. If you'd like one-to-one tuition on Obsidian, personal organization, programming, creative production, or anything that I talk about in my videos, do sign up and let's chat. After a few months of refining my thoughts on this subject, please allow me to present my simplified model of AI categories inspired by Unix permissions.

**6:37** · There are just four simple levels. Level zero is deny. AI has no access to your work. You write or paint as you have always done. Level one is read-only permissions. You can question the AI and it can read your work, but only to advise you, not to write to it. This is the limit of what I would consider brainmade and my personal comfort level for my projects. Level two is write permissions. The AI can make isolated changes to your work, but you can still check it. And the final level is execute permissions. Fully agentic, it builds your work opaquely.

**7:06** · The difference in these levels is not exactly about what tool you use, but your ability to scrutinize the generated work. I believe a labeling system is important for domain experts working with AI in a healthy way. And like with most things, it's about tolerances. CEOs and managers don't know how to actually do the work, so they all think that AI is fine to use because it speeds them up. But they are novices. That is, someone who, according to Adam Savage, doesn't know when they need to employ tight or loose tolerances.

**7:38** · Professionals know when the corners can be cut, but only if we know the corners are being cut, and that requires clear language.

**7:48** · I've made some simple icons available on 0rwax.com for you to use to mark your own work to clue others into what level of AI automation was used in your projects. But unlike brainmade.org, this is not necessarily a virtue signaling farm-to-table mark. I think it's most useful in conversation to clarify your thinking and to avoid confusion. If the framework doesn't quite vibe with you, then consider using the language of accreditation.

**8:12** · At the read level, credit an AI research assistant as someone who aided you while you made your work.

**8:18** · If AI-generated work ends up in your final project, then credit it as a co-writer.

**8:23** · And if the project was mostly AI-written, own it. Don't be that guy in the group project getting equal credit for no work. I ended my first video on AI, The Second Renaissance, published 5,000 years ago in 2022 by asking the question, "What would you do if you could do it all?" Well, we now have that answer, and it's not all sunshine and rainbows. It's not even all slop and bankrolls. We need new language to talk about large language models, and I hope the zero auto X framework makes it just a little easier.

**8:52** · Thank you.

**8:53** · If you'd like to support my channel, get early ad-free and tracking-free videos, your name in the credits, or one-to-one mentoring, head to my Patreon or Ko-fi.

**9:00** · If you're interested in transhumanism and hopepunk, please check out my weekly sci-fi audio fiction podcast, Lost Terminal.

**9:06** · If you like urban fantasy, I produce a wonderful podcast called Modem Prometheus.

**9:10** · Season 4 of The Phosphine Catalog is just out. If you like mysteries and art, check it out. Transcripts and compiled check markdown source code available namtao.com on GitHub. Links are in the descriptions, and corrections are in the pinned errata comment. Thank you so much for watching. Talk to you on Discord.