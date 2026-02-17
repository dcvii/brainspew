---
title: "Does that use a lot of energy?"
source: "https://hannahritchie.substack.com/p/does-that-use-a-lot-of?publication_id=1199196&post_id=188019870&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Hannah Ritchie]]"
published: 2026-02-15
created: 2026-02-16
description: "An interactive tool to get a sense of scale for energy consumption."
tags:
  - "clippings"
---
### An interactive tool to get a sense of scale for energy consumption.

Without data, it’s incredibly hard to get a sense of scale.

One area where this is extremely apparent is in energy use and carbon emissions. It’s hard to know what matters a lot, and what very little.

A lot of my work with data is about getting a sense of whether something is big or small, effective or not. Is that a big number?

To help, I’ve built [an interactive tool](https://hannahritchie.github.io/energy-use-comparisons/) that lets you compare the energy use of different products and activities: from lighting and cooking, to heating and driving. This is focused on “household” energy use: what people consume at home or while commuting.

In the video below, I’ve shown a quick example of what you can do with it. Select the products or activities you want to compare, and adjust the basic inputs, which are usually the number of hours or minutes of usage, or miles driven.

 <video><source src="/api/v1/video/upload/6c4c7270-7df1-4ae3-8ec2-0a68667a0f4f/src?override_publication_id=1199196&amp;type=hls" type="application/x-mpegURL"> <source src="/api/v1/video/upload/6c4c7270-7df1-4ae3-8ec2-0a68667a0f4f/src?override_publication_id=1199196&amp;type=mp4" type="video/mp4"></video>

To build this, I developed a dataset of energy consumption based on *typical* usage. As I stress in the tool, these are approximations. They will not reflect your life down to the watt-hour level. I have assumed an LED lightbulb is 10 watts; yours might be 8.5.

Getting caught up in these small differences is actually *against* what I’m trying to do here. I’m trying to give people (and myself) a sense of what’s small and big. What order of magnitude are we talking about? Is driving 10 miles equal to 10, 100, or 1000 hours of lighting?

If this tool looks useful and is making a difference, I might build a similar one for carbon emissions (it will allow me to include things like food and other purchases).

---

## Do you have feedback?

This is still a work-in-progress, so if you have feedback to share, I’d really appreciate it. There are now more than 70,000 of you following this newsletter, so I can’t promise a reply to everyone, but I do promise to read your messages and use them to make improvements.

Below the tool, I’ve written a methodology document detailing my assumptions for each product. It was a long list, took quite a bit of work, and there might be a few mistakes in there.

Feedback that is useful is along the lines of:

- Your assumption for the energy rating or power consumption of X is really off
- This component/configuration is broken
- This tool would be much more useful if it had X functionality
- It would be great to add \[some product/activity not listed\]

Comments that are less helpful:

- Those focused on small differences between my numbers and your actual usage. As I said, I’m going for typical approximations here; it won’t reflect precise reality for everyone

Things that make the tool **a lot more complex**. The simplicity here is important and deliberate, so people can make relatively quick comparisons. I don’t want people to have to put in the specific model of television, dishwasher, or car; or give precise details about the fabric of their home.