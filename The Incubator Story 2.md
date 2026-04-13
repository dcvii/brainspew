---
title: "The Incubator Story"
source: "https://tessellations.substack.com/p/the-incubator-story"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2026-03-16
created: 2026-03-23
description: "Grass roots are good."
tags:
  - "brain_spew"
---
### Grass roots are good.

![](https://substackcdn.com/image/fetch/$s_!Yfew!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F010dfac7-ca4a-4f57-8705-de4c011ef2f4_5712x4284.jpeg)

So this year, you may know I’m going rather high gear into agentic programming. I had another quantum leap over the weekend. There’s no easy way to abstract it - I’m just working a new set of skills and developing new muscle memories.

[MicroBizLaunchpad](https://microbizlaunchpad.org/) is my new connection. They’re running a couple incubators in NoCal and SoCal. This weekend they were in Sacramento and Orange County. I was down here at Chapman College. It’s a completely different feel than the techbro or VC futurist attitude. These are good folks taking AI’s potential both offensively and defensively. The economy is going fractional. Do you know your fraction?

Long story short. I took a leap and kicked off a new level of vibe coding. Moreover I met a lot of cool people, some just wading in and some all the way at the deep end. What I did in several short hours was run through several iterations of an iPhone UI design that will integrate into the Circle Protocol soon. Literally a year ago I had the drawing up. Now it’s demonstrable.

[

## Circle Protocol Recap

](https://tessellations.substack.com/p/circle-protocol-recap)

[Michael David Cobb Bowen](https://substack.com/profile/12305822-michael-david-cobb-bowen)

·

March 18, 2025

[![Circle Protocol Recap](https://substackcdn.com/image/fetch/$s_!O__G!,w_280,h_280,c_fill,f_webp,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fab7a9942-c6c9-494d-9e7c-ba0e63911897_3024x4032.jpeg)](https://tessellations.substack.com/p/circle-protocol-recap)

I don’t have a pseud for my friend DG, although he has a cool one for himself. We’ve known each other professionally for several years now, but I’m just getting to know a few things about the man. What’s exciting to me is when I can get people excited about what goes on in my head - because.. a lot of reasons. Suffice it to say that one of the reasons I…[Read full story](https://tessellations.substack.com/p/circle-protocol-recap)

---

What I didn’t know, and who knew how many people knew, was it would take less than a day and a half to make this puppy real. So here’s the brief demo.

 <video><source src="https://tessellations.substack.com/api/v1/video/upload/6e7a0580-aeef-4212-b214-7bda27549b74/src?override_publication_id=1655845&amp;type=hls" type="application/x-mpegURL"> <source src="https://tessellations.substack.com/api/v1/video/upload/6e7a0580-aeef-4212-b214-7bda27549b74/src?override_publication_id=1655845&amp;type=mp4" type="video/mp4"></video>

People around me were using different combinations of tools. I couldn’t match the people and projects with the tools but they were { **Replit**, **Lovable**, **Bolt** }. I was using my own established tools including **[Warp](https://www.warp.dev/)** and **[Zed](https://zed.dev/)**. I used Claude Code a little bit more than Oz which is the native LM for Warp.

I have never heard of **Figma**, and really I didn’t get bogged down with it. All I did was make sure the MCP server was available to Warp. I cranked out 60 lines of prompt for my first prototype, and about 25 more for my changes to that. Then I did something I would never do which is have an LM combine two prompts together including a few more requirements that I put into the interactive prompt. I gave that task to Claude Code and it pushed out about 250 lines of prompt, which I had it turn around and process. The above was the end result.

I thought I would have to learn a bit more JavaScript and more UI terminology, but it turns out that I didn’t need to. It’s still lacking in finesse but it gets the message across and I think it will be relatively simple to improve and hook up to APIs. The prototype turned out to simply be html and javascript. What’s crazy is that when I showed my drawing to Ryan, who ran the class, he said “Oh, like a hockey rink”. So I used his terms in the first couple of iterations. Now I know I can move a lot faster than I ever thought possible.

Here’s the prompt.

```markup
<role> You are an expert visual desiger with Figma. You specialize in interactive iPhone app design.
</role>

<goal>I want to build an interactive iPhone app demonstration that has both haptic and color feedback. It involves dragging objects around the screen and seeing the color change based on the drag.
</goal>

<design-overview>
    The primary screen to be built is shaped like a hockey rink. It is arranged lengthwise with a goal at each end represented by a semi-circular area. This screen will not change orientation - it will always be in portrait mode.
    The rink itself is divided into seven zones, with Limbo being the topmost semicircle and Me being the bottommost semicircle.

    Another way to think of the overall design is that each zone can represent the orbit of a planet around the Sun
    Keep that in mind as an alternative perspective. 
    
- The topmost semicircle is called Limbo.
- The bottommost semicircle is called Me.
- The objects to be moved are called pucks. 
- At the beginning, all pucks are in Limbo.
- No pucks can be dragged into Me.
- Between Limbo and Me lies the rink itself which is divided into five zones.
- Limbo is also called C7.
- C6 is the next zone down from Limbo (C7)
- Me is C1. 

</design-overview>

<instructions>
    STEP ONE: Layout
    - create the necesary template in figma that sets up the initial layout. 
    - make the lines between the zones a speicific dark color.
    - Each zone will use a color gradient which increases in opacity as you move down the rink.

STEP TWO: Population
- Put 3 pucks into Limbo.
- Pucks are three dimensional objects that move between zones.

STEP THREE: Interaction
- When a puck is dragged into a zone, it moves to that zone.
- The puck's color changes to match the zone it enters but retains a dark outline.
- As the puck crosses a border between zones, there should be a haptic feedback.
- Whe the finger is lifted, the puck stays in place and a sound effect plays.

</instructions> 

<output>
    Create a valid Figma file that implements the prototype.

</output>

<data model>
    Each zone represents a Circle of Trust. To move a puck from one zone to another generates a transcation of either a promotion or a demotion. C1 is the highest level of trust and C7 is the lowest.
</data model>
```

---

The best part about the weekend was networking and getting around enough people who understand systems so that I can have fun. It reinforces the technical me. Really had a good time. Weird, I trust vibe coding to do more and myself to do yet another higher level of abstraction. I didn’t expect that, and I can see how it’s slowing me down. A bit..