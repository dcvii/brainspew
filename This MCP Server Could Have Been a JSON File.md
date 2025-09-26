---
title: "This MCP Server Could Have Been a JSON File"
source: "https://materializedview.io/p/mcp-server-could-have-been-json-file?r=7br8e"
author:
  - "[[Chris]]"
published: 2025-09-11
created: 2025-09-11
description: "There's a lot of buzz around MCP. I'm not convinced it needs to exist."
tags:
  - "MCP"
---
### There's a lot of buzz around MCP. I'm not convinced it needs to exist.

[Model context protocol (MCP)](https://modelcontextprotocol.io/) servers are very buzzy right now. The idea is simple: teach [large language models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) how to interact with other software systems. In doing so, LLMs can learn from and affect the real world; they can call a web service to make a phone call, invoke a [command line interface (CLI)](https://en.wikipedia.org/wiki/Command-line_interface) tool to add an item to a grocery list in a reminder app, and so on. To make such calls, LLMs must know what software it can call and how to do so. This is the problem that MCP solves: it informs LLMs of available software, teaches the LLM how to use it, and provides an avenue through which the LLM can call the software.

Developers write MCP servers that provide *resources*, *prompts*, and *tools* to the LLM. The MCP site [discusses these concepts in detail](https://modelcontextprotocol.io/docs/learn/server-concepts), but the [Core MCP Concepts](https://modelcontextprotocol.io/docs/develop/build-server#core-mcp-concepts) section provides a summary:

> 1. **[Resources](https://modelcontextprotocol.io/docs/learn/server-concepts#resources)**: File-like data that can be read by clients (like API responses or file contents)
> 2. **[Tools](https://modelcontextprotocol.io/docs/learn/server-concepts#tools)**: Functions that can be called by the LLM (with user approval)
> 3. **[Prompts](https://modelcontextprotocol.io/docs/learn/server-concepts#prompts)**: Pre-written templates that help users accomplish specific tasks

These categories are arbitrary and confusing. At first blush, it seems resources are read-only and tools are write-only. But the MCP server documentation uses [searchFlights](https://modelcontextprotocol.io/docs/learn/server-concepts#how-tools-work) as their tool example—a read-only operation. Even more baffling, they later show flight searching as a resource. Here’s their tool definition:

```markup
{
  name: "searchFlights",
  description: "Search for available flights",
  inputSchema: {
    type: "object",
    properties: {
      origin: { type: "string", description: "Departure city" },
      destination: { type: "string", description: "Arrival city" },
      date: { type: "string", format: "date", description: "Travel date" }
    },
    required: ["origin", "destination", "date"]
  }
}
```

And here’s their resource definition:

```markup
{
  "uriTemplate": "travel://flights/{origin}/{destination}",
  "name": "flight-search",
  "title": "Flight Search",
  "description": "Search available flights between cities",
  "mimeType": "application/json"
}
```

Prompts are simply [static JSON definitions](https://modelcontextprotocol.io/docs/learn/server-concepts#example%3A-streamlined-workflows) that describe potential user activities.

The whole protocol feels off to me. Prompts are just static documentation, resources are static URL definitions, and tools look like [remote procedure call (RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call) definitions. I asked [ChatGPT 5 Thinking](https://openai.com/index/introducing-gpt-5/) to convert the `searchFlights` tool definition to an [OpenAPI definition](https://swagger.io/specification/) (an actual RPC definition). Unsurprisingly, it worked just fine:

```markup
openapi: 3.0.0
info:
  title: Flights API
  version: "1.0.0"
paths:
  /searchFlights:
    get:
      operationId: searchFlights
      summary: Search for available flights
      description: Search for available flights
      parameters:
        - in: query
          name: origin
          required: true
          description: Departure city
          schema:
            type: string
        - in: query
          name: destination
          required: true
          description: Arrival city
          schema:
            type: string
        - in: query
          name: date
          required: true
          description: Travel date
          schema:
            type: string
            format: date
      responses:
        "200":
          description: Search results
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
```

This begs the question: why do we need MCP for tool definitions? We already have [OpenAPI](https://www.openapis.org/), [gRPC](https://grpc.io/), and CLIs. ChatGPT understands OpenAPI definitions. Millions of web services already provide OpenAPI definitions, too. And ChatGPT is actually better at CLIs than most humans—just watch [Codex](https://openai.com/codex/) fly through sed, awk, and grep commands. A friend recently informed me that they successfully taught ChatGPT to use [tmux](https://github.com/tmux/tmux/wiki). [MCP vs CLI: Benchmarking Tools for Coding Agents](https://mariozechner.at/posts/2025-08-15-mcp-vs-cli/) reflects this sentiment:

> MCP vs CLI truly is a wash: Both `terminalcp` MCP and CLI versions achieved 100% success rates. The MCP version was 23% faster (51m vs 66m) and 2.5% cheaper ($19.45 vs $19.95).

I’ve seen [several arguments](https://bsky.app/profile/did:plc:bjaceaxgoto5p7gor2rcov3g/post/3lxdmbcfsx226?ref_src=embed) made to justify MCP’s existence:

1. LLMs have a limited context window. OpenAPI documentation takes up too much context space.
2. Many services are not well documented; they don’t come with an API spec.
3. LLMs need a way to discover what tools are available to it.

I’m skeptical. Perhaps MCP does allow us to squeeze a few more tools into the context window. Perhaps it does let models run a little faster. OpenAPI documents are indeed somewhat verbose. But for how long will this matter?

Last year we were talking about 1 million token models. Now, we have [2 million token models](https://x.com/OpenRouterAI/status/1964128504670540264) in [OpenRouter](https://openrouter.ai/). Smaller models, fine tuning, and other research also continues apace. Viewed from this lens, MCP seems like a temporary kludge.

The final argument that many services have poor documentation is true for internal enterprise services. [Jake Mannix](https://www.linkedin.com/in/jakemannix) makes this point in [his recent thread](https://bsky.app/profile/yetanotheruseless.com/post/3lxdmbcpuac26). I hear that MCP is most widely adopted for this segment.

Customer-facing SaaS APIs are a different story. Most [are](https://docs.github.com/en/rest?apiVersion=2022-11-28) [remarkably](https://docs.stripe.com/api) [well](https://plaid.com/docs/api/) [documented](https://auth0.com/docs/api/authentication). Some are complex, but these are often (I can attest to this after working with [WePay’s API](https://developer.wepay.com/api/)).

Moreover, the argument seems to be that the same people that wrote the bad OpenAPI specs are going to write good MCP specs. I don’t buy it. (And again, even if they *could* do this, why not write the endpoint as an OpenAPI endpoint or a CLI tool?)

![](https://substackcdn.com/image/fetch/$s_!HJgE!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Faded91f2-44a4-4e2b-a7f6-cb171417897f_684x196.png)

[View Post](https://x.com/ianlivingstone/status/1965768133752262863)

As for discovery, I accept that LLMs need to know where tools are and how to use them. But this is static content. We already have [AGENTS.md](https://agents.md/), [.github/instructions](http://.github/instructions), [openapi.json](https://swagger.io/specification/#openapi-description-structure), and so on.

[Developers](https://x.com/sriramsubram/status/1960366044209467875) [are](https://x.com/spencershum/status/1960379872490234342) [waking](https://x.com/kylemathews/status/1960365038918656093) up to this. [Bruin](https://getbruin.com/) ﹩ is using MCP [just to expose documentation](https://x.com/burakkarakann/status/1960391792202772956); their tool calls are done through normal CLI commands. [Donobu](https://www.donobu.com/) ﹩ simply provides an OpenAPI spec. Both solutions work. Meanwhile, MCP’s Google trend looks bleak.

![](https://substackcdn.com/image/fetch/$s_!cMux!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdd7b8f6f-0253-49e7-82c7-23309e34ad02_1142x704.png)

Google Trends “mcp” Interest Over Time

I don’t blame the MCP authors for this mess. Things happen fast in the AI ecosystem. MCP is a victim of its own success. [MCP: An (Accidentally) Universal Plugin System](https://worksonmymachine.ai/p/mcp-an-accidentally-universal-plugin) does a good job explaining the situation.

We need to take a step back and think about what we’re trying to accomplish. There’s no law that LLMs need a new protocol to interact with software. In most cases, we have what we need. Where we don’t, we should write CLIs, web services, and documentation using existing standards.

> My takeaway? Maybe instead of arguing about MCP vs CLI, we should start building better tools. The protocol is just plumbing. What matters is whether your tool helps or hinders the agent's ability to complete tasks.
> 
> —Mario Zechner, [MCP vs CLI: Benchmarking Tools for Coding Agents](https://mariozechner.at/posts/2025-08-15-mcp-vs-cli/)

---

#### Book

Support this newsletter by purchasing [The Missing README: A Guide for the New Software Engineer](https://www.amazon.com/Missing-README-Guide-Software-Engineer/dp/1718501838) for yourself or gifting it to someone.

![](https://substackcdn.com/image/fetch/$s_!CI0B!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fde442631-41a6-4119-a99a-62957cd53edb_870x978.png)

---

#### Disclaimer

I occasionally invest in infrastructure startups. Companies that I’ve invested in are marked with a ﹩ in this newsletter. See my [LinkedIn profile](https://www.linkedin.com/in/riccomini/) and [Materialized View Capital](https://materializedview.capital/) for a complete list.