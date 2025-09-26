---
title: "Sequoia Backs Zed's Vision for Collaborative Coding - Zed Blog"
source: "https://zed.dev/blog/sequoia-backs-zed"
author:
  - "[[@nathansobo]]"
published: 2025-08-20
created: 2025-08-20
description: "From the Zed Blog: This investment lets us pursue our vision for bringing a new kind of collaboration directly into the IDE."
tags:
  - "clippings"
---
## Sequoia Backs Zed's Vision for Collaborative Coding

## Sequoia Backs Zed's Vision for Collaborative Coding[Nathan Sobo](https://zed.dev/team#nathan-sobo)

August 20th, 2025

Today we're announcing our $32M Series B led by Sequoia Capital with participation from [our existing investors](https://zed.dev/about#our-investors), bringing our total funding to over $42M.

For the past four years, we've been building the world's fastest IDE, but that's just the foundation for what comes next. Our ultimate vision is a new way to collaborate on software, where conversations about code remain connected to the code itself, instead of being tied to aging snapshots or scattered across different tools. The first step was creating a high-quality editor to serve as the user interface. Now this new investment lets us expand to tackle the next phase of our plan. We're developing a new kind of operation-based version control that incrementally tracks the evolution of your code with edit-level granularity, and we're integrating it into Zed to make collaboration, both with agents and teammates, a first-class part of the coding experience.

Sequoia is excited about our vision, and we're thrilled to have their help making it a reality. We're actively hiring, so if the future we're building excites you, [we'd love to talk](https://zed.dev/jobs).

## Why Snapshots Constrain Our Conversations About Code

Real-world software is the product of a never-ending stream of conversations: With yourself, your teammates, and now also with generative AI models. Talking about code helps us understand it, both individually and as a team. But with current tooling, these discussions (and all the insights they generate) seem to exist everywhere except the code itself.

Git lets you collaborate by sharing commits and branches, but between commits you work alone in your own isolated working copy. It's fairly easy to discuss code that's changing in a pull request, but if you want to have a conversation about an arbitrary part of your codebase, you're stuck pasting text into a chat app linking to a particular version of the relevant code in a snapshot. As snapshots become stale and messages scroll into the past, your conversations quickly lose their link to the latest version of the code, and all of their valuable context is lost.

The limitations of snapshots become even more apparent when working with AI agents. While you might manage simple tasks by exchanging comments with an agent on a pull request, real-world development often requires interaction between commits. You need to guide agents, correct their course, and iterate rapidly—all without the overhead of creating snapshots for every exchange. Our existing tools were built for humans trading commits asynchronously, not for instant back-and-forth with synthetic collaborators. Forcing every AI interaction through the commit-based workflow is like trying to have a conversation through a fax machine.

Today's AI editors patch over these limitations, but miss the core problem: collaboration is continuous conversation, not discrete commits. You can't snapshot every clarification, every pivot, every back-and-forth that shapes the code. We're building a system that captures this entire dialogue: every edit, every discussion, linked durably to the code as it evolves. This frees collaboration from the rigid structure of commits.

## Introducing DeltaDB: Operation-Level Version Control

Our vision is turn your IDE into a collaborative workspace where humans and AI agents work together across a range of time scales, with every insight preserved and linked to the code forever. To make this possible, we're building DeltaDB: a new kind of version control that tracks every operation, not just commits.

DeltaDB uses [CRDTs](https://zed.dev/blog/crdts) to incrementally record and synchronize changes as they happen. Its designed to interoperate with Git, but its operation-based design supports real-time interactions that aren't supported by Git's snapshots. For async interactions, fine-grained change tracking also enables character-level permalinks that survive any code transformation, so we can anchor our interactions to arbitrary locations in the codebase, not just to snapshots of recently-changed code.

Zed's goal is to make your codebase a living, navigable history of how your software evolved, where discussions with humans and AI agents are durably linked to the code they reference and always up-to-date. It's an evolution beyond version control that incorporates not just the code itself, but also the background information of how and why the code got into a particular state—context that AI agents can query to make more informed edits, understanding the assumptions, constraints, and decisions that shaped the existing code.

Picture a new engineer facing a production stack trace in Zed. They highlight a problematic line, like an `unwrap` that caused a crash, and see every related discussion: why the function was written or what an AI agent assumed about an invariant. They ping the responsible human, sparking a quick chat that turns into an audio call, all indexed to the exact code spot, creating a shared, revisitable record without leaving the codebase.

[Zed is open-source](https://github.com/zed-industries/zed) with an [optional paid offering](https://zed.dev/pricing), and we plan to do the same with DeltaDB: build it, open-source it, and offer an optional paid service. We'll share more details as development progresses; this is just the beginning of reimagining how developers work together, both with AI agents and their team.

## Help Us Build a Collaborative Future

We have the vision, technical foundation, and funding to fundamentally improve how developers collaborate. Now we just need you. We’re hiring across engineering and product design; whether you're interested in collaboration in the IDE, core Zed projects like cross-OS font rendering and GPU shaders, or improving the world's best [open-source open-data language model for Edit Prediction](https://zed.dev/edit-prediction), there's room for you here. [Join us](https://zed.dev/jobs) to shape the future of software development.

---

### Looking for a better editor?

You can try Zed today on macOS or Linux. [Download now](https://zed.dev/download)!

---

### We are hiring!

If you're passionate about the topics we cover on our blog, please consider [joining our team](https://zed.dev/jobs) to help us ship the future of software development.