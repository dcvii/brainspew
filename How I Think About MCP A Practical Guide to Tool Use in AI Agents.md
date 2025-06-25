---
title: "How I Think About MCP: A Practical Guide to Tool Use in AI Agents"
source: "https://natesnewsletter.substack.com/p/how-i-think-about-mcp-a-practical?r=1z4sm5"
author:
  - "[[Nate]]"
published: 2025-01-30
created: 2025-04-12
description: "What Model Context Protocol really is, where it does and doesn't work, how it compares to APIs and LangChain, and why I think it's the cutting edge of software on the web now!"
tags:
  - "clippings"
---
### What Model Context Protocol really is, where it does and doesn't work, how it compares to APIs and LangChain, and why I think it's the cutting edge of software on the web now!

Here's a wild thought: **what if we stopped telling AI systems exactly what to do?**

I've been obsessing over this question lately, because there's this fascinating shift happening in how AI systems interact with software. It's not about fancier models or better prompts. It's about something more fundamental: **giving AI the power to actually do things in the world.**

If you’ve spent time with tools like ChatGPT or Claude, you’ve likely seen the beginning of this shift: models that can use calculators, fetch calendar events, or send emails through what appear to be "plugins" or "actions." But if you scratch the surface, those integrations are tightly scoped and heavily scripted. They work because someone wrote a very specific bridge from the model to the tool—a custom function, a pre-integrated API, a predictable sequence.

**But what happens when we remove the script?** What happens when the model is given a wide range of possible tools and left to figure out *what* it should do and *how* to do it?

That's where Model Context Protocol (MCP) comes in, and it's probably not what you think.

Look, I know what you're thinking: "Great, another acronym in the AI space." But stick with me here, because this one's different. MCP isn't just another API wrapper or a fancy way to chain prompts together. It's a fundamental rethinking of how AI systems interact with tools.

Here's the key insight: instead of us writing detailed instructions for every possible scenario, what if we just described our tools in a way that AI models could understand, and then... let them figure it out?

That's MCP in a nutshell. It's like handing your AI a manual of available tools and saying "You decide how to use these." No more rigid scripts. No more if-this-then-that logic chains. Just pure, AI-powered problem solving.

In this post, I want to explore what that really means. I’ll start with a concrete example—a model planning and confirming a dinner reservation for you—and use that to break down how MCP works, why it matters, what it changes, and where it fits alongside things like APIs and LangChain. Along the way, we’ll confront some of the real, hard questions anyone building production systems will ask: What happens when it fails? How do we debug it? Can we trust it with sensitive actions? And what’s the actual latency hit when your orchestration layer is, well, a stochastic model?

### A Concrete Scenario: Booking Dinner, the Hard Way

Let’s say I have a task on my nice [Hobonichi](https://www.1101.com/store/techo/en/) to-do list:

> "Book dinner-Friday night"

This sounds simple. But if you try to build a tool that automates that task, you realize it’s not.

To fulfill this one request, your system needs to:

1. Search for restaurants that match a specific vibe ("romantic") and availability.
2. Choose one based on user preferences.
3. Book a reservation.
4. Add it to the user’s calendar.
5. Generate a confirmation script.
6. Call the restaurant to confirm (ideally with voice).

Behind that flow are multiple APIs:

- Yelp or Google Places for restaurant data
- OpenTable or Resy for reservations
- Google Calendar for scheduling
- ElevenLabs for text-to-speech
- Twilio for placing the call

If you’re using traditional tooling, every step requires you to make assumptions: about the flow, the parameters, the logic. You’re writing conditional logic: “if booking succeeds, create calendar event,” and so on. You’re choosing what tools to use and when, and if something fails, you have to define fallback behavior.

And here's where it gets messy: to make this work, you need to stitch together a whole bunch of different services. You've got Yelp or Google Places for finding restaurants, OpenTable for actually booking tables, calendar APIs for scheduling, maybe ElevenLabs for generating natural-sounding speech, and Twilio to actually make the phone call.

If you've ever tried to build something like this the traditional way, you know the drill. You spend weeks writing if-then statements. "If the reservation succeeds, then add to calendar. If that works, then generate the confirmation call..." It's like writing a choose-your-own-adventure book where you have to account for every possible path.

But here's where MCP flips the script (pun intended). Instead of mapping out every possible path ourselves, what if we just described each tool—what it does, what it needs, what it gives back—and let the AI figure out how to use them together?

It's like the difference between giving someone step-by-step directions and handing them a map. With directions, they're stuck following your exact path. With a map, they can find their own way—and maybe even discover better routes you hadn't thought of.

### What MCP Actually Is

Model Context Protocol is a way to describe tools—what they do, what they require, what they return—in a format that an AI model can interpret and reason about. Think of it like writing a user manual that's designed to be read by AI instead of humans. For each tool, you explain:

- What it does (in plain language)
- What information it needs to work
- What kind of results it gives back

These tool definitions are structured in a specific way (JSON schemas). They contain:

- A name and natural language description
- Input parameter definitions
- Output expectations

You also provide an execution endpoint—a tool server—that receives requests and executes the desired action.

This setup isn’t inherently complex. What’s different is who drives the flow. Instead of wiring up logic ahead of time, the model reads the schemas, evaluates what tools are relevant, chooses how to sequence them, and sends structured calls in real time. In other words, once you describe your tools this way, you're not telling the AI *how* to use them anymore. You're just saying "here's what's available" and letting the AI figure out the rest.

That’s orchestration by inference.

And it’s powerful. But it also introduces new operational challenges.

### Operational Realities: How Does Reasoning Hold Up at Scale?

On paper, replacing brittle logic with model-based reasoning sounds ideal. But in production, systems must operate under sustained load, variable user inputs, and a relentless demand for predictability. This is where the limits of autonomous orchestration start to show.

The most pressing operational question is: **how reliably can a model choose the right tools in the real world?** How can we know the model made the right decision?

The answer is: **it depends heavily on the environment**.

In relatively constrained domains—say, a scheduling assistant with clearly defined calendar and messaging tools—models can perform well. When tools are well-scoped, their parameters are tightly defined, and their function is obvious, large language models tend to make reasonable choices.

But once ambiguity enters the picture, reliability drops.

[Studies](https://multiagents.org/2025_artifacts/reliable_decision_making_for_multi_agent_llm_systems.pdf) and [blogs](https://cobusgreyling.medium.com/the-multi-ai-agent-gap-897dc1427f97) on multi-agent systems and tool-augmented LLMs have shown that incorrect tool use becomes more common as:

- The number of tools increases
- Tool definitions become more complex
- Overlapping functionality creates decision ambiguity

When implemented, models have been observed to:

- Attempt to call tools that don’t exist (tool hallucination)
- Confuse required parameters (e.g., treating an email address as a phone number)
- Misinterpret tool descriptions when schema definitions are vague or inconsistent

UW paper on failure modes with related architecture [here](https://homes.cs.washington.edu/~rjust/publ/tallm_testing_ast_2025.pdf),

These issues are common enough to be worries at scale—they’re emerging patterns. Tool hallucination is especially tricky to catch unless every call is rigorously logged and validated against a known registry.

Failure often isn’t catastrophic—it’s silent. A malformed call doesn’t execute, and the user sees no response. That’s scary, right?! Or worse, the model keeps trying, compounding the problem and burning tokens.

To build reliable MCP systems, you need more than just good building tools. You need guardrails, validation layers, and continuous evaluation of how the model interprets tool descriptions under varied prompts.

Diving into the developer side of things a bit, good patterns include:

- **Strict JSON schema validation** before execution
- **Descriptive tool definitions** that clarify intent and disambiguate usage
- **Fallback mechanisms** that allow for safe retries or handoff to a human-coded fallback path
- **Simulated prompt testing** with diverse input to stress-test tool reasoning

So does reasoning hold up at scale?

TLDR; it can—but only with serious investment in operational support. In its current state, model-driven orchestration is flexible and powerful, but not inherently robust. Reliability comes not from the model alone, but from the infrastructure built around it.

### Performance and Latency: What’s the Overhead of Thinking First?

The second unavoidable issue is latency.

Every time a model decides what tool to use, it:

1. Reads the user prompt
2. Interprets the available tool schema(s)
3. Constructs a function call
4. Waits for a result
5. Possibly chains into another tool

Compared to traditional flows—where tools are invoked directly and deterministically—this introduces overhead at two levels:

- **Token-level delay** as the model generates the tool call string
- **Processing delay** if the model must revise or retry tool selection

In production, this can mean an additional 200ms–1s per reasoning hop, depending on model size and complexity.

That might sound minor, but in multi-step chains—or voice-interactive experiences—it adds up.

So where’s the tradeoff worth it?

- If the use case is *highly variable* or *domain-spanning* (e.g., a general assistant)
- If maintaining dozens of hardcoded routes would be expensive or unscalable

But if your flow is fixed, or latency-sensitive (e.g. fraud detection, trading), you probably don’t want a language model deciding whether to call `freeze_account` vs `flag_transaction`. That’s where traditional orchestration wins.

### Observability: What If It Fails in the Weirdest Way?

This is where experienced engineers start asking, rightly: **how do I debug something I didn’t explicitly code?**

MCP-driven systems require a different approach to observability:

- You log **every tool call the model attempts**: tool name, parameters, output, and any failure
- You log **token-level trace output**: what did the model say that led to that decision?
- You tag tool calls with **request metadata** to understand usage patterns across traffic

You also need to build **failure maps**: common patterns where the model:

- Misunderstood tool affordances
- Missed required parameters
- Called tools in the wrong order

And you need visibility tools for non-engineers. For PMs or QA testers to understand what happened, you must render decision traces in plain English—what tools were available, what the model chose, and what the outcome was.

In short, **MCP doesn’t eliminate the need for observability—it raises the bar for it.**

### Security and Safety: Can a Model Be Trusted to Orchestrate Sensitive Workflows?

Finally: security.

When models gain the ability to orchestrate actions, they also gain the ability to misfire. This introduces serious questions for anyone working in a regulated, sensitive, or privacy-critical domain.

What prevents a model from:

- Calling `delete_user` with the wrong ID?
- Sending sensitive data through the wrong channel?
- Making duplicate purchases or transactions?

These aren’t hypothetical. In some early testing scenarios, models have done all three.

Mitigation patterns include:

- **Role-based tool exposure**: different tools for different users, contexts, or flows
- **Parameter-level validation**: preflight checks for things like IDs, tokens, or required fields
- **Policy constraints**: override logic that blocks high-risk tools unless certain conditions are met
- **Sandboxing execution**: don’t let models call prod endpoints directly—route them through verification layers

And yes, **every tool call must be auditable**. Governance teams will require logs that show:

- Who requested the action
- What the model tried to do
- What tool was actually called
- What was returned

If you’re using MCP in finance, healthcare, government, or anything that touches real-world operations, these concerns aren’t edge cases. They’re Day 1 design requirements.

### Why this matters more than you think

Look, I get it. After reading about all these challenges and limitations, you might be wondering: is MCP really worth the hassle?

Here's the thing: MCP isn't just another way to wire up APIs or chain together functions. **It's a fundamental shift in how we think about building software.** We're moving from a world where humans have to spell out every single step to one where we can just describe what's possible and let AI figure out the rest. **And that’s going to keep happening more and more.**

Think about that for a second. **Every major leap in software development has been about abstraction—moving from machine code to assembly to high-level languages. MCP feels like the next step in that evolution.** Instead of writing logic, we're teaching systems how to reason about tools.

I'm not saying it's perfect. The reliability issues are real. Debugging can be a nightmare. And yes, sometimes it's slower than traditional approaches. But you know what? These feel like the same growing pains we had when we first started moving everything to the cloud. They're speed bumps, not roadblocks.

What excites me most is what this enables. When AI can actually understand and compose tools on its own:

- Your chatbots become true assistants
- Your automation adapts instead of breaks
- Your systems can handle edge cases you never even thought about

I've been kicking around tech and acquiring gray hairs for a long time, and I can't shake the feeling that this is one of those moments we'll look back on as the birth of a new internet standard. Not because MCP is perfect, but because it's showing us a glimpse of what's possible when we let AI systems truly reason about the software they're using. And as models get better, MCP will automatically get smarter! Those edge-cases will start to ease up as intelligence scales.

Is it ready for everything? No. Should you rewrite all your systems to use it? Probably not. But if you're building anything (especially something small-scale) that needs to be flexible, adaptive, or truly intelligent, MCP isn't just another tool to consider—it's a whole new way of thinking about what software can be.

And that's what makes it worth paying attention to, despite all the challenges. Because we're not just building better tools— **we're building tools that can think about how to use themselves.** This isn’t just a new trick for agents, **we’re witnessing the birth of a new substrate for software.** It feels weird to me too, but this is what AI disruption looks like! And I, for one, find it pretty cool.

### Getting Started with MCP and Model-Driven Tool Use

#### Must Reads

- **Anthropic’s Introduction to Model Context Protocol (MCP)**
	[https://www.anthropic.com/news/model-context-protocol](https://www.anthropic.com/news/model-context-protocol)
	The original announcement and rationale for MCP from Anthropic. Good overview of intent and tooling model.
- **Official MCP Documentation & Spec (Community-maintained)**
	[https://modelcontextprotocol.io/introduction](https://modelcontextprotocol.io/introduction)
	Emerging hub for open-source MCP schemas, reference servers, and technical details.
- **Composio**
	[https://composio.dev/](https://composio.dev/)
	A marketplace with 250+ MCP servers to play with. Lets you register, define, and expose tools to agents. Also has LangChain and SDK integrations.

#### Hands-On Tutorials & Code Examples

- **Tool Calling with OpenAI Function Calling (aka MCP-lite)**
	[https://platform.openai.com/docs/guides/function-calling](https://platform.openai.com/docs/guides/function-calling)
	While not MCP, OpenAI’s function calling is very similar structurally and useful for experimenting with tool schemas.
- **LangChain Tooling with Agents**
	[https://python.langchain.com/docs/how\_to/#tools](https://python.langchain.com/docs/how_to/#tools)
	How to expose functions and tools for use within LangChain agents—especially relevant when bridging LangChain and MCP-style systems.
- **Deep dive into tool schemas and server setup (from the Composio team)**
	[https://docs.composio.dev/docs/what-is-mcp](https://docs.composio.dev/docs/what-is-mcp)
	Includes working examples of tool definitions, tool servers, error handling, and dynamic tool loading.

#### Think Pieces & Critical Takes

- **Gergely Orosz – “MCP Protocol: a new AI dev tools building block”**
	A must-read for engineers evaluating the operational readiness of agents. Gergely dives much more deeply into the technical side. Always enjoy his posts!
		[The Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/mcp?utm_source=substack&utm_campaign=post_embed&utm_medium=web)
	[
	Before we start: this is the last week of the “What’s in your tech stack?” survey. If you’ve not yet done so, please fill out this survey and tell us about it. If you take part and fill out the survey, you will receive the full results early, plus some extra, exclusive analysis from myself and Elin. (Full results, minus the exclusive analysis will be published in The Pragmatic Engineer). It takes as little as 5 minutes to fill — thank you for your help…
	](https://newsletter.pragmaticengineer.com/p/mcp?utm_source=substack&utm_campaign=post_embed&utm_medium=web)
- **Latent Space – Podcast: “The API for AI Agents”**
	Excellent audio deep dive with builders behind MCP and agents. Helps situate MCP in the broader wave of tool use and agent infrastructure.[Latent.Space](https://www.latent.space/p/mcp?utm_source=substack&utm_campaign=post_embed&utm_medium=web)

[

We are happy to announce that there will be a dedicated MCP track at the 2025 AI Engineer World's Fair, taking place Jun 3rd to 5th in San Francisco, where the MCP core team and major contributors an…

](https://www.latent.space/p/mcp?utm_source=substack&utm_campaign=post_embed&utm_medium=web)

![](https://natesnewsletter.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/7fb97b19-2e18-48c5-afea-dbd62f5ae076_1024x1024.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1024,%22width%22:1024,%22resizeWidth%22:null,%22bytes%22:1430272,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://natesnewsletter.substack.com/i/160913071?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7fb97b19-2e18-48c5-afea-dbd62f5ae076_1024x1024.png%22,%22isProcessing%22:false,%22align%22:null})

The AI has tools now!