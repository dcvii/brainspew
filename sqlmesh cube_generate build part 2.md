---
title: "sqlmesh cube_generate build part 2"
source: "https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email"
author:
  - "[[David Jayatillake]]"
published: 2024-12-18
created: 2025-02-07
description: "Time for some AI Engineering"
tags:
  - "clippings duckdb data"
---
Yesterday, I got to a point where I got a CLI command to output JSON, which described the relationships between sqlmesh models and how fields were aggregated. This is the fundamental metadata required to build a semantic layer. When I set out to build this integration this week, I knew it was unlikely I would build something that deterministically generates a Cube data model perfectly. I thought that, at some point, I would come to a point where what I had built harvested the relevant metadata from a sqlmesh project, that I could then use AI to enhance this output.[![sqlmesh cube_generate build part 1](https://substackcdn.com/image/fetch/w_1300,h_650,c_fill,f_auto,q_auto:good,fl_progressive:steep,g_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a2fc488-da2b-4709-972b-894786a46b4c_1454x1804.png)](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part)

After my progress last night, I attempted to enhance the metadata further to enable its deterministic use in generating a Cube semantic layer. However, I reached a stage where minor improvements were consuming excessive time, and I’m not aiming to create something perfect here! Therefore, I believe it’s time to delve into some AI engineering.

My next goal is to add options to the cube\_generate CLI command that will accept OpenAI[1](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email#footnote-1-153306126) credentials and LLM selection. If these credentials are provided, a prompt should be sent to the selected LLM containing the metadata the command can generate already, the rendered SQL for the models, Cube’s documentation on data modeling syntax, and instructions on what to do.

The Gold layer tables in my synthetic[2](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email#footnote-2-153306126) sqlmesh [example project](https://github.com/djayatillake/sqlmesh/tree/main/examples/ecommerce) are a great example of a microcosm of a semantic layer. They have event and dimensional tables joined with field aggregations to create metrics. Cube has the concept of Views, which are like star schemas that prevent you from needing Gold layer tables with fixed grain, where you still need knowledge about what to aggregate to derive metrics. It would be great if Cube Views could be generated for each Gold layer model, referring to Silver layer Cubes.

I’ve written this far without attempting any work at all, so let’s see how it goes!

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F52adef1f-1c62-4818-bf38-4db43371751a_861x294.png)

So this was how I started out, and after some additions, and a few minor fixes[3](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email#footnote-3-153306126), I got something that worked! Compared to yesterday’s hard problem of recursive AST walks, which I wasn’t actually sure how to solve on a conceptual level myself[4](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email#footnote-4-153306126), Cascade laughed[5](https://davidsj.substack.com/p/sqlmesh-cube_generate-build-part-f1f?utm_source=substack&utm_medium=email#footnote-5-153306126) at the simplicity of this task.

Here is my new sqlmesh cube\_generate CLI command:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d6f2a9a-a62c-41d6-85df-f3b0ec57fc6f_1440x1228.png)

this is what `sqlmesh cube_generate —help` outputs, most capable is o1-preview

A lot of what I actually ended up playing with was the prompt text itself. Windsurf built the original prompt really well, summarising the URLs of the Cube docs into a good structure. A few errors resulted in strange output from the summarisation, like using camelCase instead of snake\_case in many places (although this may be valid in an old Cube version). It also found some old ways of describing relationships between Cubes, which were actually valid but that we never really use anymore. Most of my time today has been editing and adjusting the summarised Cube docs that feed into the prompt.

Here is the output of running `sqlmesh cube_generate --generate-yaml --select-models "gold.*" --output test_output.yaml `:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F561c9e02-aaca-41bb-a5dd-1631a6e702d3_1468x12096.heic)

I’m really impressed with the results. I haven’t tried to compile it on a Cube instance yet, and I’m sure there will be some errors, but I had a decent look, and it looks very good! It shows how much can be done with relative ease using Windsurf, especially where it is “workflowy”.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa34e21cc-c1d9-42cc-b659-2f2aab4d0714_680x704.png)