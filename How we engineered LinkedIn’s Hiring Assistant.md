---
title: "How we engineered LinkedIn’s Hiring Assistant"
source: "https://www.linkedin.com/blog/engineering/ai/how-we-engineered-linkedins-hiring-assistant"
author:
published:
created: 2025-10-27
description:
tags:
  - "clippings"
---
[AI](https://www.linkedin.com/blog/engineering/ai)

## Building the agentic future of recruiting: how we engineered LinkedIn’s Hiring Assistant

Over the last two decades, LinkedIn has reshaped how companies and recruiters discover and connect with candidates, transforming recruiting from a manual process into a data-driven discipline.

Now, the rise of AI is empowering us to imagine a new era of recruiting. [Hiring Assistant](https://business.linkedin.com/talent-solutions/hiring-assistant) is our next leap forward. Hiring Assistant is an AI agent for recruiters powered by our dynamic talent network, designed to help recruiters discover and engage candidates with more speed, scale, and intelligence than ever before.

Taking Hiring Assistant from the charter [phase](https://www.linkedin.com/blog/engineering/generative-ai/the-tech-behind-the-first-agent-from-linkedin-hiring-assistant) to [global availability](https://www.linkedin.com/blog/engineering/hiring/hiring-assistant-shaped-by-customers-powered-by-ai-innovation) required solving hard technical problems: real-time conversational interfaces, large-scale asynchronous execution, reliable agentic tool use, and individualized cognitive memory that learns from recruiter behavior. Along the way, we’ve listened to customers to ensure that we’re building an agent that truly helps recruiters get things done on LinkedIn.

In this blog, we’ll take you behind the scenes to explore the architecture, design choices, and lessons learned in building LinkedIn’s first agentic product.

## What problems we were solving

Recruiters' work combines high-value decision-making with large volumes of pattern-recognition tasks. With Hiring Assistant, we set out to build an AI agent that can take on the repetitive aspects of sourcing, evaluation, and engagement work in a scalable and adaptive way. This frees recruiters to focus on what they enjoy most: connecting with people and driving successful hires.

From an engineering perspective, building an agent is first and foremost building a product. To be a successful product, Hiring Assistant has to be grounded in three core abilities:

1. **Value delivery at scale**: sourcing and evaluating candidates across 1.2+ billion profiles with enterprise-grade throughput and reliability.
2. **Interactive communication**: understanding recruiter intent through natural dialogue, resolving ambiguity, and adapting behavior in real time.
3. **Continuous learning**: improving over time by incorporating recruiter feedback, behavioral signals, and long-term engagement patterns.

Candidate sourcing and evaluation are the most resource-intensive parts of the recruiting workflow, and they also present the greatest technical challenges. Scaling this means more than running queries – it requires executing searches asynchronously, evaluating results with context, and keeping pipelines updated without human micromanagement.

To make this possible, Hiring Assistant needed several foundational technical capabilities:

- **Real-time conversational interfaces** to capture, interpret, refine the understanding of hiring intent.
- **Agentic tool use** that mirrors recruiter actions, but executes through headless system access.
- **Large-scale asynchronous execution** to support long-running, background sourcing and evaluation tasks at scale.
- **Continuous learning** to persist context, recall relevant history, detect user activity patterns and continuously refine recruiter-specific preferences.

In the following sections, we will walk through Hiring Assistant’s high-level cognitive architecture and then dive into the specific technical components, from orchestration to learning, that make these capabilities possible.

## Hiring Assistant’s high-level cognitive architecture

At its core, Hiring Assistant is a plan-and-executor agent built on top of a message-driven agent lifecycle platform (see our [recent blog](https://www.linkedin.com/blog/engineering/generative-ai/the-linkedin-generative-ai-application-tech-stack-extending-to-build-ai-agents) for more), supported by individualized cognitive memory tools. Unlike a single shared agent serving many users, Hiring Assistant is modeled as separate agent instances, each tied to its own recruiter. Every Hiring Assistant instance has its own identity and mailbox, and its lifecycle is orchestrated entirely through asynchronous message passing.

To be effective, Hiring Assistant depends on a suite of headless tools that mirror the ones human recruiters use – such as Recruiter Search, project management, and candidate/job management – but exposed in a form agents can programmatically interact with.

Some of Hiring Assistant’s capabilities are further decomposed into sub-agents for modularity and abstraction. For implementation efficiency, we model these sub-agents as tools rather than creating separate agent identities and mailboxes.

At the center of this architecture is the supervisor agent, the “central nervous system” of Hiring Assistant. Acting as the planner and orchestrator, it interprets user input, evaluates context, and delegates tasks to the right tools or sub-agents. This plan-and-execute loop allows Hiring Assistant to triage recruiter requests, manage workflows, and deliver results reliably at scale.

Figure 1. High level cognitive architecture of Hiring Assistant

Hiring Assistant could have been built on a simple ReAct-style architecture, powered by tools like headless Recruiter, member profile access, and messaging APIs. Architecturally, as seen in figure 2 below, this approach is straightforward and can work if the supporting infrastructure is highly scalable and the LLM consistently produces desired results.

Figure 2. Simple ReAct architecture

In practice, however, ReAct alone is not sufficient for an enterprise-grade agent. Relying directly on LLMs to solve complex recruiting problems introduces major challenges:

- **Instruction-following reliability:** LLMs may not follow instructions and plans reliably.
- **Hallucinations:** fabricated or irrelevant outputs risk damaging trust.
- **Intelligence (test-time compute) vs. latency tradeoffs:** richer reasoning often comes at unacceptable performance costs.

To overcome these challenges, we adopted a Plan-and-Execute architecture. In this model, the agent separates its reasoning into two cycles within a larger loop:

- **Planner** (divide): performs high-level reasoning to produce a structured, task-specific plan.
- **Executor** (conquer): runs the plan step by step, using a ReAct-style loop for tool use and local reasoning.

This approach allows us to *divide and conquer* complex recruiting workflows. The Planner ensures that tasks are well-scoped and less error-prone, while the Executor delivers results efficiently. The architecture also leaves room to optimize for cost, latency, and task completion rate as the system scales.

Figure 3. Plan-and-execute architecture

The following table summarizes the high level comparison between the two architectures. The Plan-Execute is better suited to our use cases and provides room to optimize for cost, latency, and completion rate as we get deeper into the development.

| **Feature** | **Plan-Execute** | **ReAct** |
| --- | --- | --- |
| **When to use** | When the problem space can be divided into tasks with clear instructions that requires reliable handling | When it’s necessary for the agent to adapt to unexpected situations, or when the task involves a complex interplay of reasoning and actions. |
| **Approach** | Planning first, then execution | Iterative reasoning and action |
| **Complexity handling** | Well-suited for complex, multi-step tasks | Flexible for tasks with dynamic adjustments |
| **LLM calls** | Potentially fewer, due to upfront planning | Potentially more, due to open ended iterative nature |
| **Cost** | Can be more cost-effective in the long run. Architecture is set up to support differentiated LLMs for different tasks | May have higher API costs. Single LLM for all iterations and this LLM has to be able to do handle the most complex thinking |
| **Task completion rate** | Can improve task completion rate by forcing the planner to explicitly think through all steps | Task completion rate degrades quickly as the problem space grows |

## The agentic user experience

For Hiring Assistant to be valuable for users, the experience has to feel natural, trustworthy, and scalable. Today, Hiring Assistant has two complementary parts: the interactive UX and the asynchronous UX. Together, they provide the foundation for how recruiters collaborate with the agent.

### Interactive UX: trust and alignment

The interactive interface allows recruiters to converse directly with Hiring Assistant. This helps clarify hiring requirements, align on expectations, and adjust behavior before large-scale execution begins. Key benefits:

- **Responsive and collaborative:** Feels like working with a trusted teammate.
- **Transparency:** Shows what Hiring Assistant is doing and how it reasons about tasks.
- **Fast feedback loops:** Recruiters can fine-tune requirements quickly, avoiding wasted effort later.

### Asynchronous UX: Scale and Autonomy

Once alignment is reached, Hiring Assistant executes tasks autonomously in the background. This is where Hiring Assistant delivers scalable outcomes. Key benefits:

- **Massive background execution:** Runs sourcing and evaluation jobs across millions of profiles.
- **Continuous pipeline management:** Refreshes candidate pipelines daily and evaluates new applicants continuously.
- **Human-in-the-loop:** Ensure that humans are in the loop for all decisions that humans are accountable for while removing much of the toil from them.

This mode allows recruiters to “source while you sleep,” freeing them to focus on high-value work.

| **Dimension** | **Interactive UX** | **Asynchronous UX** |
| --- | --- | --- |
| **Primary purpose** | Build trust and alignment upfront | Deliver scalable, efficient outcomes |
| **User experience** | Converse with a trusted teammate | Background execution with human-in-the-loop |
| **Benefits** | Transparency, fast feedback, avoids wasted cycles | Scale, autonomy, continuous pipeline management |
| **When most useful** | Early in workflow, clarifying hiring requirements | Running long, labor-intensive tasks |

## The building blocks of the agentic user experience

The agentic UX in Hiring Assistant is made possible by a deep stack of platform capabilities. What looks like a simple conversation interface on the surface is actually supported by a complex ecosystem of orchestration services, real-time pipelines, and model-driven planning.

#### Agent infrastructure

The product was not built in isolation – it sits on top of LinkedIn’s state-of-the-art agent platform and framework which provides reusable, scalable building blocks for agent products. For more details, see our recent blog: [The LinkedIn Generative AI Application Tech Stack: Extending to Build AI Agents](https://www.linkedin.com/blog/engineering/generative-ai/the-linkedin-generative-ai-application-tech-stack-extending-to-build-ai-agents).

#### Client framework and GraphQL API

Hiring Assistant uses a client-side SDK to embed seamlessly into recruiter workflows, delivering a dynamic, data-driven UI that adapts in real time. The framework ensures the agent shares the same context as the recruiter (seeing exactly what the user sees) and can control UI display and perform actions dynamically without relying on hard-coded page navigation. It supports interactive chat, typing assistance, and voice input, while logging interactions for analytics. The GraphQL API connects the SDK to backend services and provides decorated view models, enabling components to render dynamically in alignment with the server-driven / agent-driven UI (SDUI/ADUI) architecture, creating scalable, adaptive experiences across product surfaces.

#### Real-time integration

Hiring Assistant operates as a stateful, real-time agent that manages both conversational interactions and long-running workflows. A traditional request–response model is insufficient, so Hiring Assistant uses a push-based, event-driven architecture:

- **Publish–subscribe model:** UI updates, notifications, and task changes are delivered asynchronously via a session-level real-time channel. The SDK subscribes to agent-specific topics and updates the UI automatically.
- **Streaming and partial responses**: Long-running LLM tasks are streamed incrementally, allowing recruiters to observe reasoning, track task progress, and preview results as soon as they are available.
- **Cross-session synchronization:** Updates propagate consistently across devices and sessions, ensuring that actions such as task completion are reflected everywhere.
- **Decorated view models for dynamic rendering**: Real-time events deliver strongly typed view models containing the data and metadata needed to render UI components dynamically. Components remain modular and can render from inputs or lazy-loaded related entities without additional round trips.
- **Notifications and dashboard updates:** The dashboard is continuously updated based on in-progress tasks and workflows. Notifications may be derived from task state or managed as persistent entities, maintaining consistency across clients.

This architecture ensures Hiring Assistant delivers a highly responsive, consistent, and dynamic agent experience, leveraging the Dynamic UX design pattern, decorated view models, and modular data-aware components to scale across different recruiter workflows and evolving UI requirements.

#### Supervisor agent

The supervisor agent is the central orchestrator in Hiring Assistant, that coordinates all agent activity. It manages communication between users and sub-agents, oversees workflows, and ensures tasks are executed reliably across both interactive and background processes.

Key responsibilities:

- **Hiring workflow management:** Oversees the execution of hiring workflows and invokes the appropriate sub-agents to fulfill user requests.
- **Message orchestration**: Receives messages from users, interprets intent, and routes tasks to the correct sub-agent.
- **Task prioritization**: Balances human-in-the-loop and autonomous agent tasks to maximize efficiency.
- **Agent coordination**: Ensures smooth communication between sub-agents and reliable completion of assigned tasks.
- **Observation**: Monitors relevant environment changes, such as new candidate activity or user actions, and triggers sub-agents when needed.
- **Human-in-the-loop management:** Presents tasks that require human approval or oversight, maintaining transparency and alignment with user intent.

All user and agent interactions flow through the supervisor agent. Messages are structured in a unified format, allowing the agent to efficiently route, track, and manage tasks. While Hiring Assistant handles many tasks autonomously, the supervisor agent ensures critical actions receive human approval when necessary, maintaining reliability and giving users visibility into ongoing workflows.

#### Specialized sub-agents

Hiring Assistant’s capabilities are powered by a collection of specialized sub-agents, each designed to handle a specific part of the recruiting workflow. These sub-agents work under the supervision of the Supervisor Agent, enabling both interactive collaboration and large-scale asynchronous execution.

- **Intake agent:** Gathers and refines hiring requirements and role details from recruiters. It confirms key attributes like job title, location, and seniority, inferring missing information when needed. It then generates role-specific qualifications from detailed inputs and past successful projects, LinkedIn [Economic Graph](https://economicgraph.linkedin.com/) insights, or world knowledge, ensuring quality and alignment with best practices for downstream sourcing and evaluation.
- **Sourcing agent:** Generates multiple search queries based on hiring requirements and evaluation criteria. Leveraging and enhancing LinkedIn Recruiter Search and Recommended Matches tools, it runs these queries at scale, stores potential candidate profiles, and iteratively refines queries based on performance to adapt to changing talent supply and demand.
- **Evaluation agent:** Assesses candidates by synthesizing information from multiple sources (including profiles, resumes, and historical engagement data) and applies hiring requirements and evaluation rubrics to produce structured recommendations with reasoning and evidence. Recruiters remain in the loop to review these insights and make the final decisions on advancing candidates through the recruiting workflow.
- **Candidate outreach agent:** Handles communication with candidates, including generating and sending initial outreach and follow-up messages across multiple channels. It also replies to candidate questions based on the hiring requirements and FAQs defined during the intake process, and can schedule phone screens directly through messaging.
- **Candidate screening agent:** Supports the screening process by preparing tailored screening questions based on hiring requirements and candidate profiles. It can observe, transcribe, and summarize conversations, while capturing candidate insights and notes. Recruiters remain actively in the loop – candidates can connect with them directly at any time, and recruiters can take over or guide the screening process whenever needed.
- **Learning agent:** Continuously refines hiring requirement personalization by analyzing recruiter actions, such as adding candidates to pipelines or sending InMails. It updates qualifications and candidate recommendations dynamically by integrating both explicit feedback and implicit signals from recruiter behavior. Any recommendations around changes to qualifications are surfaced asynchronously to recruiters and applied only after their review and approval. This ensures Hiring Assistant adapts over time while keeping recruiters in control, improving alignment with preferences and optimizing candidate sourcing efficiency.
- **Cognitive memory agent:** Provides Hiring Assistant with persistent, context-aware memory to support personalized interactions. It enables Hiring Assistant to adapt recommendations and workflows over time in a scalable way. All memory data remains scoped to the recruiter’s environment and is never used for training LLMs. Customers retain control over their stored memory with robust privacy and management options.

Together, these sub-agents create a cohesive and scalable recruiting workflow, combining human-like reasoning, automation, and personalization. In the following sections, we will take a deeper dive into the evaluation agent, sourcing agent, and learning agent to explore how they drive Hiring Assistant’s intelligent, adaptive behavior.

## Scaling intelligent candidate evaluation

Recruiters spend a significant amount of time reviewing resumes of candidates and applicants to assess how well they meet the key qualifications for a given role. The repetitive and time-consuming nature of this work makes it ideally suited for help from agents. We had to solve several key challenges to prepare our evaluation agent for to the task:

1. **Alignment:** Before evaluating any candidates, we ensure that the recruiter has reviewed the set of specific qualifications that will be used for evaluation. We also run safety checks against each qualification to ensure that it complies with our Responsible AI policies.
2. **Explanation:** Our agent reads through each candidate’s LinkedIn profile, resume, and other relevant data to search for supporting evidence demonstrating how the candidate meets each qualification. It surfaces the evidence it finds to the recruiter so they can make the most informed decisions.
3. **Accuracy:** We developed quality benchmarks to test our agent across a range of different evaluation scenarios, allowing us to evaluate new versions of our candidate evaluation agent even before they reach our users.
4. **Scalability:** We developed custom LLMs optimized for the task of evaluating qualifications. These models deliver a combination of accuracy and scale not achievable with off-the-shelf models.
5. **Latency:** To provide a responsive, conversational experience, the agent needs to evaluate candidates quickly, so the recruiter can review the results and refine the qualifications as needed. Using techniques such as speculative decoding within our custom LLM serving infrastructure, our fine-tuned models can evaluate candidates in seconds.

## Powering agentic sourcing

The number one reason customers use LinkedIn Recruiter is to source qualified candidates. Sourcing is a highly knowledge-intensive activity, and making it more efficient is central to Hiring Assistant’s cognitive ability.

We designed the Hiring Assistant sourcing sub-agent to complement how recruiters approach this task, helping them work more efficiently.. It draws on LinkedIn’s deep expertise in building Recruiter Search to assemble a growing repertoire of sourcing strategies — from classic Boolean queries to LLM-driven query generation based on hiring requirements, as well as leveraging historical recruiter search queries as priors. Importantly, in keeping with our enterprise grade data isolation and responsible AI principles, the sub-agent never uses customer data across customer boundaries.

A unique advantage of Hiring Assistant is LinkedIn’s [Economic Graph (EG)](https://economicgraph.linkedin.com/) — a digital representation of the global economy. Tapping into EG and LinkedIn Talent Insights gives the agent a deep understanding of talent supply, demand, and movement. This enables advanced sourcing strategies, such as identifying top locations, titles, and skills for a given talent pool, spotting active or recently hired candidates, and uncovering talent flows where the recruiter's company is winning or losing. Hiring Assistant can also surface candidates from fast-growing companies, roles, or skill sets, identify companies with layoffs, and highlight opportunities in top schools or companies with open positions. By leveraging these rich insights, Hiring Assistant goes beyond straightforward matches to uncover hidden gems who may otherwise be overlooked.

In advanced scenarios, sourcing becomes even more powerful when paired with candidate evaluation. By creating a closed feedback loop between evaluation signals and sourcing strategies, Hiring Assistant can use LLM reasoning to refine queries, balance precision and liquidity, and continuously improve the quality or volume of candidates or both.

## Making Hiring Assistant a studious learner

Learning is the foundation of intelligence — and building an AI agent is no different. For Hiring Assistant, this means going beyond simply following recruiter instructions to actually learning from both what recruiters say and what they do. Every click, shortlist, or outreach becomes a signal that sharpens the agent’s understanding of role-specific nuances, preferences, and recruiter style.

At first, Hiring Assistant relies on explicit guidance and feedback. But with every project, it observes and adapts, gradually picking up the recruiter’s taste, judgment, and decision-making patterns. What makes the Hiring Assistant more powerful is that for existing Recruiter users, it can learn from the recruiter’s past activities ahead of time so it won’t be a stranger even when the recruiter is interacting with it for the first time.

To enable this, Hiring Assistant is equipped with machine learning tools that analyze recruiter activity data, both asynchronously and in real time. These tools separate signal from noise, uncover meaningful patterns, and adapt recommendations accordingly. Whenever needed, Hiring Assistant taps into its cognitive memory agent to recall relevant past interactions or previously learned patterns, ensuring decisions are grounded in accumulated knowledge.

The result is that each recruiter gets a personalized Hiring Assistant. Over time, the recruiter and AI agent develop a shared rhythm: the agent anticipates preferences, adapts to feedback, and evolves into a trusted collaborator.

## Holistic quality framework

Product quality is paramount for Hiring Assistant’s success. In the AI era, quality extends beyond traditional system reliability – it also includes the quality of the content an agent produces, how well it aligns with user goals, and whether it behaves responsibly. To address this broader scope, we’ve developed a holistic quality framework built on two pillars: product policy and human alignment.

Think of these two pillars as the rails and compass that guide Hiring Assistant’s journey.

- **Product policy** provides the rails – setting the boundaries for safety, compliance, legal standards, and expected agent behavior. These policies establish the minimum quality bar and ensure the agent stays on track, while still leaving room for autonomy and innovation. We use these policies to drive LLM-powered judges that evaluate quality: sometimes without references (for coherence) and sometimes against grounded data (for factual accuracy).
- **Human alignment** provides the compass – ensuring Hiring Assistant is always oriented toward real hiring outcomes. Our engineering process is grounded in human-validated data, including both annotated datasets and real recruiter activity. For example, if a recruiter engages with a candidate, we treat that as a strong positive signal. Over time, Hiring Assistant learns to recommend more candidates that match these recruiter-validated patterns. Human alignment not only improves outcomes but also validates product policy, keeping the framework tied to real-world effectiveness.

Together, the rails (policy) and compass (alignment) form a two-pronged approach to quality. This ensures Hiring Assistant doesn’t just work reliably, but continuously evolves into a more intelligent, trustworthy, and valuable recruiting partner.

## Final words

This is just the beginning of our journey into building enterprise-grade agents that help our customers do their work better. With Hiring Assistant, we’ve taken the first step toward reimagining how recruiters source, evaluate, and engage candidates, efficiently, at scale.

We hope that sharing our experiences can help shape the broader community of practitioners working at the intersection of AI, systems, user experience, and trust. By being transparent about our approach, tradeoffs, and architectural choices, we seek to spark discussion, invite feedback, and contribute to the evolving body of knowledge on how to responsibly design agentic systems that truly deliver value.

Hiring Assistant is a continuation of LinkedIn’s vision and mission: creating economic opportunity for every member of the global workforce by connecting professionals to make them more productive and successful. We hope that Hiring Assistant is not just a product innovation but a foundation for the next generation of recruiting – one that empowers recruiters to focus on what they do best: building relationships and making great hires, and one that ultimately makes it easier for great candidates to be discovered for roles they might not have found otherwise.

As we continue to iterate, learn, and scale, we’re excited to partner with our customers, and the broader engineering community, on this journey into the agentic age.

## Acknowledgements

It has been challenging though rewarding bringing Hiring Assistant to life. This milestone reflects the incredible efforts of a large team effort across Product Engineering, Product Management, Design, Agent Infrastructure, Model Serving Infrastructure, Core AI, and our early charter customers. A critical part of this success was the tight codesign across product, models, infrastructure, and user experience, which enabled us to deliver an agent that is both technically robust and truly valuable to our customers. Hiring Assistant represents not only a major product milestone, but also a testament to what’s possible when cross-functional teams work together to innovate at scale.