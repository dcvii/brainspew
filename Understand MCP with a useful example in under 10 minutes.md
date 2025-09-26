---
title: "Understand MCP with a useful example in under 10 minutes"
source: "https://medium.com/@eduardojld/understand-mcp-with-a-useful-example-in-under-10-minutes-f13bc9d6c852"
author:
  - "[[Eduardo Lugo]]"
published: 2025-04-16
created: 2025-04-22
description: "If you are here, you have read about MCP and how it will change everything, but you are not sure how it works and how you can use it, so you are basically feeling like I was during these past couple…"
tags:
  - "clippings"
---
If you are here, you have read about MCP and how it will change everything, but you are not sure how it works and how you can use it, so you are basically feeling like I was during these past couple of weeks

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*yTC8P8_7bh9m_kgyyvJnhg.gif)

not actually me

So, how about if we build something to really know how it works and what possibilities it has for us?

**By the end of the article, we will have an agent that can grab a YouTube video and create a travel itinerary and directions to move between the sights mentioned in the video.**

## What you’ll need

- [Claude desktop](https://claude.ai/download)
- [Docker](https://www.docker.com/products/docker-desktop/)

## Tools we will use

- [Google Maps](https://hub.docker.com/r/mcp/google-maps)
- [Youtube Transcript](https://hub.docker.com/r/mcp/youtube-transcript)

## Configure Claude

We are going to be adding all of our tools in this file

```c
code ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

And it will end up looking like this

```c
{
    "mcpServers": {
        "youtube_transcript": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "mcp/youtube-transcript"
                ]
            },
        "google-maps": {
            "command": "docker",
            "args": [
                "run",
                "-i",
                "--rm",
                "-e",
                "GOOGLE_MAPS_API_KEY",
                "mcp/google-maps"
            ],
            "env": {
                "GOOGLE_MAPS_API_KEY": "YOUR_API_KEY"
                }
        } 
    }   
}
```

()

Now let's fire up Claude Desktop and we should see a little hammer as an indication that it will have access to the tools we just configured

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*muC4311jDKA5MKhkDcrQ9A.png)

We are now ready to give it a test run. Let’s try this

> From this video [https://www.youtube.com/watch?v=-Tz4G11f9T8](https://www.youtube.com/watch?v=-Tz4G11f9T8) I want to build a itinerary for next week that includes the top 10 places mentioned in the video I need you to validate each place with reviews.
> 
> For each day in the itinerary I want to know what directions I need to follow to move from one place to the next.
> 
> You should also generate a csv file I can import into Google My Maps with those directions and additional relevant information

## What is actually going on

Claude Desktop will ask permission to execute some of the tools we have configured above. This tells us a couple of things about how this works

- We did not tell Claude in any way or form when to use each tool
- We are not required to know what parameters each tool needs
- However, Claude is choosing to use one tool or the other on its own based on the requirement given and how to best comply with it
![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*kdC0uQkp7vQrQCOfHq92Yg.jpeg)

We will see as Claude works on the answer, the reasoning and to what end it will use each tool.

You can see the [full itinerary I got in this link](https://medium.com/@eduardojld/orlando-7-day-itinerary-top-10-attractions-2d5b0c678c4e)

Our Final schedule imported into Google My Maps looks like this

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*8JB7iQWorC0dnOuFCw9hVg.png)

## Let’s break it down

Claude Desktop is the MCP Client. It acts as the **brain or orchestrator**, interpreting your input and figuring out what needs to be done. It doesn’t do the work itself, but it knows which tool (or *MCP Server*) to call to get it done.

The **tools** we configured (like `youtube_transcript` and `google-maps`) are running inside **Docker containers**, and they are each **MCP Servers**. These are **the workers** — they perform specific tasks when Claude requests them.

## Why does it matter

When you think about **MCP**, imagine each tool, integration, and agent… as a **LEGO piece**.

You’re not just building for yourself — you’re creating **modular, reusable components** that **anyone else can plug into** their own workflows.  
Whether it’s grabbing transcripts, generating maps, or talking to APIs, each tool becomes a **building block** in the broader AI ecosystem.

This opens the door to a future where:

- Tools can be shared like npm packages
- Workflows can be mixed and matched like Zapier flows
- And anyone — even non-devs — can build powerful automations

## Where do we go from here?

You can add more tools to Claude to test more flows with different integrations (here is a list of [Dockerized MCP servers](https://hub.docker.com/u/mcp))

You can build custom tools as MCP servers based on your own APIs ([look at the Claude documentation](https://modelcontextprotocol.io/quickstart/server))

[I added the weather tool in Claude documentation, and this was a schedule I got where I also requested weather information for each day](https://medium.com/@eduardojld/orlando-7-day-itinerary-top-10-attractions-2d5b0c678c4e)

That’s it, You now have a door into making a world of ideas a reality! Best of luck on trying out crazy stuff!! You got this!

## Troubleshooting/Sources

- Troubleshoot Claude [https://modelcontextprotocol.io/quickstart/server](https://modelcontextprotocol.io/quickstart/server)
- Troubleshoot Google Maps API

Generalist. I write Coding and DevOps articles, that being said I'll write about whatever else helps me deliver value to what I'm doing

## More from Eduardo Lugo

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--f13bc9d6c852---------------------------------------)