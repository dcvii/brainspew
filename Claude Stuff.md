---
title: "Note Detail"
source: "https://notegpt.io/detail?id=f45cb227-f22d-4f96-a248-fb14425a57cd"
author:
published:
created: 2026-07-15
description:
tags:
  - "brain_spew"
---
30% Off

S

ClaudeClass\_2026-07-13 21-37-33.mov

## Best Practices for Prompt Engineering and Agent Design in Large Language Models

## Introduction

This chapter explores the critical skill of **prompt engineering** —the art and science of crafting clear, structured, and effective instructions for **large language models (LLMs)**, particularly in the context of evolving AI systems like Claude from Anthropic. Prompt engineering has emerged as a foundational competency for developers and applied AI engineers working with LLMs, enabling better task comprehension, output consistency, and error handling.

We delve into two major real-world scenarios that highlight prompt engineering challenges and solutions: maintaining and migrating existing prompts across new LLM versions, and constructing agentic systems from the ground up. The discussion extends into tooling, **evaluation (eval) strategies**, and the use of agents—models empowered to autonomously interact with tools and environments—drawing from actual cases in customer support automation, accident report analysis, retail scheduling, and AI product development workflows.

Key vocabulary includes:

- **Prompt Engineering**: Crafting precise natural language instructions and context to guide LLM behavior.
- **Evaluation Suite (Eval Suite)**: A set of test cases to rigorously assess prompt performance and regression in model behavior.
- **Agentic Models / Agents**: LLMs enhanced with the ability to use external tools iteratively and independently to complete complex tasks.
- **Tool Use Accuracy**: Correctness in the selection and application of external tools by the agent.
- **Context Window Management**: Techniques to optimize or extend the input size available to LLMs during long or complex interactions.
- **Output Contract**: Specifications about the format and structure of model responses to ensure consistency and usability.

Understanding these concepts equips engineers and product teams to build scalable, reliable AI applications and continuously improve model-driven workflows.

---

## Maintaining and Migrating Existing Prompts: The Customer Support Case

### Scenario and Challenge

When migrating a prompt from an older LLM to a newer version, unexpected drops in performance can occur. For example, in a **telco customer support bot** called *Meridian Mobile*, a complex prompt initially worked well but began failing key test cases after switching models.

- The prompt had been collaboratively assembled with no clear ownership.
- It contained patches and mixed instructions from previous model migrations.
- It combined various policy, tone, and process guidelines compacted in unstructured paragraphs.

### Evaluation Framework

A critical step is setting up an **evaluation (eval) suite** comprising three types of test cases:

- **Control Cases**: Simple, unambiguous queries the model should always answer correctly (e.g., “What is the data limit in the basic plan?”).
- **Edge Cases**: Previously failing queries to ensure regressions don’t reoccur (e.g., billing proration calculations).
- **Capability Assessment Cases**: Scenarios where the model should defer to humans or refuse to answer (e.g., billing errors requiring escalation).

This thorough eval allowed engineers to pinpoint failures and measure improvements quantitatively.

### Prompt Hygiene and Structure

The initial step was applying **general hygiene** and structuring the prompt more explicitly:

- Removing redundant or irrelevant content copied from webpages (e.g., references to hero images and cookies).
- Avoiding telling the bot it is human (since it is not).
- Separating **policy**, **guidelines**, and **tone instructions** with clear XML-like tags.
- Adding an **output contract** specifying consistent tags (e.g., XML tags) and using API-level stop sequences to enforce response boundaries.

**Key takeaway**: “If you’re reading a prompt and can’t tell policy from guidelines from data, the model likely can’t either.”

### Targeting Failure Modes Systematically

The team next tackled individual failure cases.

- **Hotspot Data Query:** The model avoided giving hotspot data for legacy customers due to prior patches saying “never give wrong info.” Updating the prompt to allow balanced responses — acknowledging legacy plans but using accurate customer data — restored correct answers.
	- Lesson: Defensive patches may lead to withheld information; **version control** on prompt changes helps avoid such pitfalls.
- **Proration Calculation:** The model struggled with mental math for prorated billing adjustments, providing vague answers.
	- Solution: Introduce a **calculation tool** accessible to the model through the prompt and API, enabling correct calculation rather than relying on internal reasoning.
		- Lesson: **Instructions alone don’t add capability; providing appropriate tools does.**
- **Billing Error Escalation:** The model hesitated to escalate due to prompt instructions emphasizing cost avoidance.
	- Fix: Add balanced cost-benefit reasoning, showing the cost of escalation vs. risk of refund and loss of trust.

### Outcomes and Principles

- Structured prompts and cleaning redundant text improved performance quickly.
- Explicitly defining model capabilities and tool access yielded more reliable outputs.
- Prompting is an ongoing, empirical process requiring **iteration** and **evals** to monitor regressions or improvements.

---

## Building New Agentic Systems: The Retail Staff Scheduling Agent

### Problem Context

Building an agentic system from scratch introduces complexities with:

- Model choice.
- Prompt design.
- Tool/harness infrastructure.

The example used was an agent responsible for generating a **week-long staff schedule** for retail employees based on availability and constraints.

### Baseline and Model Comparisons

- Initial prompt with **Sonnet 4.6** model produced invalid schedules with numerous violations and high token usage.
- Switching to **Opus 4.7** reduced violations but still failed all test cases.
- Using **adaptive thinking** in Opus 4.7 improved compliance but at a great cost of latency and token consumption.

### Prompt Optimization on Smaller Models

- Enhancing the prompt with **structured reasoning steps** and instructing the model to **check its work** improved results.
- Result: 2/5 test cases passing; failures caused by hitting output token limits rather than logic errors.
- Further increasing tokens solved functional issues but increased latency, making this approach inefficient.

### Agentic Generate-Evaluate-Repair Loop

- Introduced a **three-step agentic process**:
	1. **Generator** produces an initial schedule.
		2. **Evaluator** (powered by a separate LLM prompt) identifies violations and provides evidence.
		3. **Repairer** modifies schedule to fix specific errors.
- Advantages:
	- Passed all test cases more efficiently.
		- Lower token usage and latency than larger models.
		- Allowed injecting **soft constraints dynamically** (e.g., employee conflicts, shift requirements) without rewriting backend code.

### Lessons Learned

- Agentic loops enable modular problem solving and fine-grained control.
- Separating concerns supports iterative debugging and easier extensibility.
- Balancing latency, token costs, and model capabilities is crucial in practical deployments.

---

## Best Practices in Prompt Engineering for Real-World Scenarios

Drawing from the described cases and methodologies, practitioners should adopt the following principles:

### Structured Prompting

- Separate **roles**, **guidelines**, **policy**, and **tone**.
- Use **markup languages** like XML or Markdown to delineate sections.
- Provide **background context** and static data in system prompts or prompt caching to reduce redundant processing.
- Define **output contracts** specifying format and boundary to enhance downstream parsing.

### Iterative and Empirical Development

- Start with small, realistic **eval test suites**.
- Focus on passing baseline and control cases before complex failures.
- Use **manual and automated evals** and **LLM-as-judge** frameworks to quantify progress.
- Track patches and changes with **version control** practices for prompt content.

### Incorporating Tools and Capabilities

- **Tools complement LLM reasoning**; add them when internal reasoning is insufficient (e.g., calculators, schedulers).
- Define tools clearly with accurate names and descriptions.
- Avoid overloading agents with redundant or overly similar tools.

### Handling Uncertainty and Output Behavior

- Guide models to **defer when uncertain**, refuse to hallucinate facts, or escalate to humans where necessary.
- Include balanced instructions covering **trade-offs**, preventing unwanted overfitting.
- Use **stepwise examination** within prompts when analyzing data or documents to improve confidence and traceability.

---

## Advanced Prompting: Agents as Tool-Using Models in Loops

### Defining Agents

Agents are LLMs endowed with the ability to use tools and interact with their environment iteratively, managing multiple steps autonomously until task completion.

- Agents require:
	- A **defined environment** and set of tools.
		- A **system prompt** instructing objectives and permissible behavior.
		- Access to **tool APIs** and **feedback loops** for refinement.

### When to Use Agents

- For **complex, valuable tasks** lacking a straightforward procedure.
- When parts of task or workflow are uncertain or exploratory.
- When **error costs are manageable** or correction mechanisms exist.
- Examples: coding assistants generating PRs, complex data analysis, autonomous research.

### Structuring Agent Prompts

- Begin with a **simple, minimal prompt**.
- Gradually add instructions addressing observed failures or edge cases.
- Avoid overly prescriptive examples; rely on models’ internalized chain of thought.
- Use **heuristics** to set agent budgets and guardrails.
- Explicitly instruct when and how to stop tasks, avoid over-searching or infinite loops.

### Context and Memory Management

- Agents may hit **context window limits** on long tasks.
- Techniques:
	- **Compaction**: automatic summarization of past context.
		- External memory files for storing and recalling state.
		- Use of **multi-agent systems** where lead agents coordinate sub-agents (e.g., lead agent manages results from sub-agent searches).

### Best Practices in Tool Design for Agents

- Tools should be:
	- **Distinct**, avoiding confusion.
		- **Accurately described** for human and model understanding.
		- Tested robustly before integration.
- Combine similar tools where possible.

---

## Prompt Engineering in Practice: Customer Accident Report Analysis

### Problem Setting

Building a prompt for an insurance claims assistant to interpret:

- A Swedish car accident report form (fixed structure with 17 checkboxes).
- A human-drawn sketch of the accident.

### Iterative Prompt Development

- **Initial Version 1**: Minimal context; model mistakenly thought the incident was a skiing accident.
- **Version 2**: Added clear task descriptions, role definition, tone (fact-based, confident, avoid guessing).
- **Version 3**: Included detailed **background data** about the form structure in system prompt to reduce ambiguity.
- Added instructions for **order of analysis**:
	- Parse form carefully, box by box.
		- Then analyze sketch against form findings.
- Specify behavior around **uncertainty**: only assert facts confident in; otherwise, admit ignorance.
- Output formatting: wrap final verdicts in XML tags for downstream parsing.

### Key Prompt Insights

- Emphasize **structured information** and explicit analysis order to align reasoning.
- Baking in **background knowledge** or static documents enables better comprehension and faster answers.
- Use **stepwise output** to communicate model’s reasoning transparently.
- Output formatting contracts ease data pipeline integration.

---

## Product Development and Team Workflows for AI Systems

### Anthropic Labs “Bet Factory” Model

- Small, cross-functional teams with blurred role lines (engineers talk to users; PMs write code; designers analyze data).
- Very rapid iteration cycles: shipping new features or fixes daily.
- Avoid traditional heavy documentation (no PRDs, OKRs, or multi-page plans upfront).
- Use **prototypes and transcripts** from team conversations as living specs.
- Early-stage exploration for “sparks” of promise, then scale teams up moderately.

### User Feedback Integration

- Share Slack channels with product users for real-time feedback.
- Employ AI (Claude) to cluster, analyze, and prioritize feedback at scale.
- Automate suggestions and streamline handoff to developers.

### Learning from Mistakes

- Example: Removed complex fine-control UI features after early negative user feedback.
- Allowed rapid iteration cycles to minimize impact of misdirected effort.

### Key Recommendations for Teams

- Prototype rapidly and iteratively rather than planning exhaustively.
- “Prototype the thing that almost works” rather than perfect.
- Use model improvements as a tide that lifts all boats; some problems may resolve simply by adopting newer models.
- Test real feature requests end-to-end in 24-hour cycles to expose process bottlenecks and optimize development flow.

---

## Conclusion

Mastering **prompt engineering** and **agent design** involves a combination of structured, clear communication, empirical testing with eval suites, and judicious tool augmentation. Through practical scenarios—ranging from maintaining complex multi-contributor prompts to architecting efficient agentic workflows—this chapter illustrates the iterative, detail-oriented nature of producing effective LLM applications.

Key takeaways include:

- Always begin with well-structured prompts that clearly separate **roles**, **policies**, and **instructions**.
- Use **evaluation test cases** from the start to track performance and regressions effectively.
- Incorporate external **tools** to enhance capabilities where LLMs’ internal reasoning falls short.
- Agentic models thrive when given **clear environmental context**, **reasonable heuristics**, and **well-designed tools**.
- Embrace rapid **prototype-driven development** and continuous **user feedback loops** over heavy upfront planning.
- Remain aware that **model advances** often transform what is feasible, letting teams focus on shaping product experience rather than low-level fixes.

These lessons empower practitioners to continuously elevate AI systems’ reliability, efficiency, and value in real-world deployments.

---

## Advanced Bullet-Point Notes

- **Prompt engineering** is essential for guiding LLM behavior effectively, especially as models evolve.
- Migrating complex prompts across models requires **structured cleanup**, **eval suites**, and isolation of **failure modes**.
- Defensive prompt patches in prior versions can **cause information withholding**; tracking changes via version control is crucial.
- **Providing tools** (e.g., calculators) empowers models to reliably handle tasks beyond native reasoning.
- A **generate-evaluate-repair pattern** can enhance agentic systems’ efficiency and modularity.
- Agent use is best suited for **complex, high-value tasks** involving variable pathways and tool-based interactions.
- Agents benefit from explicit **heuristics**, clear **tool distinctions**, and **context window management** strategies like *compaction*.
- Structured prompts with XML/Markdown tags improve content digestion and consistency.
- Including **examples** and ordering analysis steps guides model reasoning and confidence.
- Rapid prototyping outperforms traditional documentation-heavy development, enabling faster discovery and course correction.
- Integrating AI for **feedback clustering and analysis** maximizes team responsiveness and product quality.
- Early-stage team sizes remain small (~3), with cross-role skill application to minimize overhead.
- Model improvements (e.g., new Claude versions) may automatically overcome prompt limitations.
- Consistent eval suites and LLM-as-judge frameworks foster robust, scalable prompt development.
- Agents exhibit unpredictable behavior; iteration and rollback on prompt changes are routine.
- Practical deployments balance latency, token costs, and accuracy through tooling and prompt engineering.
- Prototype-driven design with direct user feedback loops reduces long-term risk and accelerates value delivery.

By synthesizing these principles, developers and product teams can harness LLMs’ power more reliably and build effective AI-driven solutions across domains.

00:00

115:43

1.0x

00:06

Hello everyone and thank you so much for joining me this afternoon in the breakout room. The last session today of code with Claude. I hope you've all had a fantastic day so far. My name is Margo Van Laar. I am an applied AI engineer at anthropic here in London.

00:23

And this afternoon, we're going to be talking about the prompting playbook. And prompting is arguably one of the first skills, if not the first skill, that we had to learn as engineers when we first started to work with LLMs. And even now, it continues to be one of the most critical skills to building effective AI systems.

00:47

So today we're going to discuss some best practices in the context of two practical scenarios that you're probably encountering at work. The first is where you have an existing prompt in production that you've been maintaining for some time and possibly you're migrating it to a new model or making a change to the architecture and for some reason it's no longer working as well.

01:13

The second scenario is where we're building an entirely new agentic use case from the ground up and we need to build the prompt from 0 to 1. Now. In order to illustrate these best practices, I don't just want to give you a list of do's and don'ts. I want to walk through a practical example that's been inspired by real prompts that I've seen some of our customers work with who are building on Claude. So.

01:42

The prompt that we'll look at today is a miniaturized example. The prompts that you're working with are probably a lot longer and more complex than the one we'll see today, but it's representative of some common problems that you might encounter when maintaining a prompt.

02:00

So imagine that we have a prompt that multiple people have been collaborating on, contributing to. There's no clear owner. It covers a lot of different areas like policy, like tone, processes. And we have some patches for kind of previous models that we've migrated greater to all mixed together. It's built up and it's complex.

02:25

And when we're migrating to a new model, we're finding that suddenly a lot of our test cases are no longer working as well as we expected. So what's actually going on here? Well, in order to start unpacking that question, we need a starting point. And that starting point is evaluations.

02:45

We need evaluations to provide that rigor to understand whether a change to our prompt is actually correlating to an improvement in its performance.

02:57

And we have different models which have different capabilities and different behaviors. And when you migrate to a different model, it could be that your system is no longer working as well for two reasons. First of all, the new model might be capable, but it's behaving differently. And therefore, we can tune our prompting to fix that behavior.

03:21

The second case is where actually the model that we're changing to isn't as capable and no amount of prompting is going to fix that. So we need to have an eval suite to act as a way of testing that regression so that we can apply our prompting best practices to that.

03:42

So in the example that we're going to be looking at today, as I said, it's going to be a miniaturized example. We'll have five test cases in our eval. In reality, you'll have a lot more test cases in your eval suite, but the key thing here is that it's representative of three key cases that we need to cover.

04:03

Those three key cases include having a control case, which is a case which should always pass. It's something that we know the model handles well. It's unambiguous. The second is edge cases. And these are cases where we've seen the model fail before. And by including instructions into the prompt, we're making sure that same behavior doesn't slip through again in the future.

04:30

And finally and critically, we need to make sure that the model has a good understanding of the extent of its capabilities, where it should be handing off to a human or where actually maybe it should be point blank refusing to answer a request.

04:47

So in the example that we're going to be looking at today will be using a prompt for a customer support bot for a telco company called Meridian Mobile and these are the five test cases that we are going to be looking at today we have a simple control case looking at. You know what's the data limit in the basic plan we're also looking at.

05:14

such as its ability to do calculations, such as calculating proration bills. If I switch my plan halfway through the month, what will my bill look like? We want to check that it's accurately addressing key questions which are covered by our policy. We need to make sure that it's escalating to a human whenever there is a billing error.

05:42

And finally, we want to make sure that our model isn't withholding any information that it has access to, which it should be handing over to the customer. So what we're going to do in this process is we'll take our prompt.

Summarize

Mind Map

Infographic

Slides

Audio Overview

Quiz

Flashcards

## Best Practices for Prompt Engineering and Agent Design in Large Language Models

## Introduction

This chapter explores the critical skill of **prompt engineering** —the art and science of crafting clear, structured, and effective instructions for **large language models (LLMs)**, particularly in the context of evolving AI systems like Claude from Anthropic. Prompt engineering has emerged as a foundational competency for developers and applied AI engineers working with LLMs, enabling better task comprehension, output consistency, and error handling.

We delve into two major real-world scenarios that highlight prompt engineering challenges and solutions: maintaining and migrating existing prompts across new LLM versions, and constructing agentic systems from the ground up. The discussion extends into tooling, **evaluation (eval) strategies**, and the use of agents—models empowered to autonomously interact with tools and environments—drawing from actual cases in customer support automation, accident report analysis, retail scheduling, and AI product development workflows.

Key vocabulary includes:

- **Prompt Engineering**: Crafting precise natural language instructions and context to guide LLM behavior.
- **Evaluation Suite (Eval Suite)**: A set of test cases to rigorously assess prompt performance and regression in model behavior.
- **Agentic Models / Agents**: LLMs enhanced with the ability to use external tools iteratively and independently to complete complex tasks.
- **Tool Use Accuracy**: Correctness in the selection and application of external tools by the agent.
- **Context Window Management**: Techniques to optimize or extend the input size available to LLMs during long or complex interactions.
- **Output Contract**: Specifications about the format and structure of model responses to ensure consistency and usability.

Understanding these concepts equips engineers and product teams to build scalable, reliable AI applications and continuously improve model-driven workflows.

---

## Maintaining and Migrating Existing Prompts: The Customer Support Case

### Scenario and Challenge

When migrating a prompt from an older LLM to a newer version, unexpected drops in performance can occur. For example, in a **telco customer support bot** called *Meridian Mobile*, a complex prompt initially worked well but began failing key test cases after switching models.

- The prompt had been collaboratively assembled with no clear ownership.
- It contained patches and mixed instructions from previous model migrations.
- It combined various policy, tone, and process guidelines compacted in unstructured paragraphs.

### Evaluation Framework

A critical step is setting up an **evaluation (eval) suite** comprising three types of test cases:

- **Control Cases**: Simple, unambiguous queries the model should always answer correctly (e.g., "What is the data limit in the basic plan?").
- **Edge Cases**: Previously failing queries to ensure regressions don’t reoccur (e.g., billing proration calculations).
- **Capability Assessment Cases**: Scenarios where the model should defer to humans or refuse to answer (e.g., billing errors requiring escalation).

This thorough eval allowed engineers to pinpoint failures and measure improvements quantitatively.

### Prompt Hygiene and Structure

The initial step was applying **general hygiene** and structuring the prompt more explicitly:

- Removing redundant or irrelevant content copied from webpages (e.g., references to hero images and cookies).
- Avoiding telling the bot it is human (since it is not).
- Separating **policy**, **guidelines**, and **tone instructions** with clear XML-like tags.
- Adding an **output contract** specifying consistent tags (e.g., XML tags) and using API-level stop sequences to enforce response boundaries.

**Key takeaway**: "If you’re reading a prompt and can’t tell policy from guidelines from data, the model likely can’t either."

### Targeting Failure Modes Systematically

The team next tackled individual failure cases.

- **Hotspot Data Query:** The model avoided giving hotspot data for legacy customers due to prior patches saying “never give wrong info.” Updating the prompt to allow balanced responses — acknowledging legacy plans but using accurate customer data — restored correct answers.
	- Lesson: Defensive patches may lead to withheld information; **version control** on prompt changes helps avoid such pitfalls.
- **Proration Calculation:** The model struggled with mental math for prorated billing adjustments, providing vague answers.
	- Solution: Introduce a **calculation tool** accessible to the model through the prompt and API, enabling correct calculation rather than relying on internal reasoning.
		- Lesson: **Instructions alone don’t add capability; providing appropriate tools does.**
- **Billing Error Escalation:** The model hesitated to escalate due to prompt instructions emphasizing cost avoidance.
	- Fix: Add balanced cost-benefit reasoning, showing the cost of escalation vs. risk of refund and loss of trust.

### Outcomes and Principles

- Structured prompts and cleaning redundant text improved performance quickly.
- Explicitly defining model capabilities and tool access yielded more reliable outputs.
- Prompting is an ongoing, empirical process requiring **iteration** and **evals** to monitor regressions or improvements.

---

## Building New Agentic Systems: The Retail Staff Scheduling Agent

### Problem Context

Building an agentic system from scratch introduces complexities with:

- Model choice.
- Prompt design.
- Tool/harness infrastructure.

The example used was an agent responsible for generating a **week-long staff schedule** for retail employees based on availability and constraints.

### Baseline and Model Comparisons

- Initial prompt with **Sonnet 4.6** model produced invalid schedules with numerous violations and high token usage.
- Switching to **Opus 4.7** reduced violations but still failed all test cases.
- Using **adaptive thinking** in Opus 4.7 improved compliance but at a great cost of latency and token consumption.

### Prompt Optimization on Smaller Models

- Enhancing the prompt with **structured reasoning steps** and instructing the model to **check its work** improved results.
- Result: 2/5 test cases passing; failures caused by hitting output token limits rather than logic errors.
- Further increasing tokens solved functional issues but increased latency, making this approach inefficient.

### Agentic Generate-Evaluate-Repair Loop

- Introduced a **three-step agentic process**:
	1. **Generator** produces an initial schedule.
		2. **Evaluator** (powered by a separate LLM prompt) identifies violations and provides evidence.
		3. **Repairer** modifies schedule to fix specific errors.
- Advantages:
	- Passed all test cases more efficiently.
		- Lower token usage and latency than larger models.
		- Allowed injecting **soft constraints dynamically** (e.g., employee conflicts, shift requirements) without rewriting backend code.

### Lessons Learned

- Agentic loops enable modular problem solving and fine-grained control.
- Separating concerns supports iterative debugging and easier extensibility.
- Balancing latency, token costs, and model capabilities is crucial in practical deployments.

---

## Best Practices in Prompt Engineering for Real-World Scenarios

Drawing from the described cases and methodologies, practitioners should adopt the following principles:

### Structured Prompting

- Separate **roles**, **guidelines**, **policy**, and **tone**.
- Use **markup languages** like XML or Markdown to delineate sections.
- Provide **background context** and static data in system prompts or prompt caching to reduce redundant processing.
- Define **output contracts** specifying format and boundary to enhance downstream parsing.

### Iterative and Empirical Development

- Start with small, realistic **eval test suites**.
- Focus on passing baseline and control cases before complex failures.
- Use **manual and automated evals** and **LLM-as-judge** frameworks to quantify progress.
- Track patches and changes with **version control** practices for prompt content.

### Incorporating Tools and Capabilities

- **Tools complement LLM reasoning**; add them when internal reasoning is insufficient (e.g., calculators, schedulers).
- Define tools clearly with accurate names and descriptions.
- Avoid overloading agents with redundant or overly similar tools.

### Handling Uncertainty and Output Behavior

- Guide models to **defer when uncertain**, refuse to hallucinate facts, or escalate to humans where necessary.
- Include balanced instructions covering **trade-offs**, preventing unwanted overfitting.
- Use **stepwise examination** within prompts when analyzing data or documents to improve confidence and traceability.

---

## Advanced Prompting: Agents as Tool-Using Models in Loops

### Defining Agents

Agents are LLMs endowed with the ability to use tools and interact with their environment iteratively, managing multiple steps autonomously until task completion.

- Agents require:
	- A **defined environment** and set of tools.
		- A **system prompt** instructing objectives and permissible behavior.
		- Access to **tool APIs** and **feedback loops** for refinement.

### When to Use Agents

- For **complex, valuable tasks** lacking a straightforward procedure.
- When parts of task or workflow are uncertain or exploratory.
- When **error costs are manageable** or correction mechanisms exist.
- Examples: coding assistants generating PRs, complex data analysis, autonomous research.

### Structuring Agent Prompts

- Begin with a **simple, minimal prompt**.
- Gradually add instructions addressing observed failures or edge cases.
- Avoid overly prescriptive examples; rely on models’ internalized chain of thought.
- Use **heuristics** to set agent budgets and guardrails.
- Explicitly instruct when and how to stop tasks, avoid over-searching or infinite loops.

### Context and Memory Management

- Agents may hit **context window limits** on long tasks.
- Techniques:
	- **Compaction**: automatic summarization of past context.
		- External memory files for storing and recalling state.
		- Use of **multi-agent systems** where lead agents coordinate sub-agents (e.g., lead agent manages results from sub-agent searches).

### Best Practices in Tool Design for Agents

- Tools should be:
	- **Distinct**, avoiding confusion.
		- **Accurately described** for human and model understanding.
		- Tested robustly before integration.
- Combine similar tools where possible.

---

## Prompt Engineering in Practice: Customer Accident Report Analysis

### Problem Setting

Building a prompt for an insurance claims assistant to interpret:

- A Swedish car accident report form (fixed structure with 17 checkboxes).
- A human-drawn sketch of the accident.

### Iterative Prompt Development

- **Initial Version 1**: Minimal context; model mistakenly thought the incident was a skiing accident.
- **Version 2**: Added clear task descriptions, role definition, tone (fact-based, confident, avoid guessing).
- **Version 3**: Included detailed **background data** about the form structure in system prompt to reduce ambiguity.
- Added instructions for **order of analysis**:
	- Parse form carefully, box by box.
		- Then analyze sketch against form findings.
- Specify behavior around **uncertainty**: only assert facts confident in; otherwise, admit ignorance.
- Output formatting: wrap final verdicts in XML tags for downstream parsing.

### Key Prompt Insights

- Emphasize **structured information** and explicit analysis order to align reasoning.
- Baking in **background knowledge** or static documents enables better comprehension and faster answers.
- Use **stepwise output** to communicate model's reasoning transparently.
- Output formatting contracts ease data pipeline integration.

---

## Product Development and Team Workflows for AI Systems

### Anthropic Labs “Bet Factory” Model

- Small, cross-functional teams with blurred role lines (engineers talk to users; PMs write code; designers analyze data).
- Very rapid iteration cycles: shipping new features or fixes daily.
- Avoid traditional heavy documentation (no PRDs, OKRs, or multi-page plans upfront).
- Use **prototypes and transcripts** from team conversations as living specs.
- Early-stage exploration for “sparks” of promise, then scale teams up moderately.

### User Feedback Integration

- Share Slack channels with product users for real-time feedback.
- Employ AI (Claude) to cluster, analyze, and prioritize feedback at scale.
- Automate suggestions and streamline handoff to developers.

### Learning from Mistakes

- Example: Removed complex fine-control UI features after early negative user feedback.
- Allowed rapid iteration cycles to minimize impact of misdirected effort.

### Key Recommendations for Teams

- Prototype rapidly and iteratively rather than planning exhaustively.
- “Prototype the thing that almost works” rather than perfect.
- Use model improvements as a tide that lifts all boats; some problems may resolve simply by adopting newer models.
- Test real feature requests end-to-end in 24-hour cycles to expose process bottlenecks and optimize development flow.

---

## Conclusion

Mastering **prompt engineering** and **agent design** involves a combination of structured, clear communication, empirical testing with eval suites, and judicious tool augmentation. Through practical scenarios—ranging from maintaining complex multi-contributor prompts to architecting efficient agentic workflows—this chapter illustrates the iterative, detail-oriented nature of producing effective LLM applications.

Key takeaways include:

- Always begin with well-structured prompts that clearly separate **roles**, **policies**, and **instructions**.
- Use **evaluation test cases** from the start to track performance and regressions effectively.
- Incorporate external **tools** to enhance capabilities where LLMs’ internal reasoning falls short.
- Agentic models thrive when given **clear environmental context**, **reasonable heuristics**, and **well-designed tools**.
- Embrace rapid **prototype-driven development** and continuous **user feedback loops** over heavy upfront planning.
- Remain aware that **model advances** often transform what is feasible, letting teams focus on shaping product experience rather than low-level fixes.

These lessons empower practitioners to continuously elevate AI systems’ reliability, efficiency, and value in real-world deployments.

---

## Advanced Bullet-Point Notes

- **Prompt engineering** is essential for guiding LLM behavior effectively, especially as models evolve.
- Migrating complex prompts across models requires **structured cleanup**, **eval suites**, and isolation of **failure modes**.
- Defensive prompt patches in prior versions can **cause information withholding**; tracking changes via version control is crucial.
- **Providing tools** (e.g., calculators) empowers models to reliably handle tasks beyond native reasoning.
- A **generate-evaluate-repair pattern** can enhance agentic systems’ efficiency and modularity.
- Agent use is best suited for **complex, high-value tasks** involving variable pathways and tool-based interactions.
- Agents benefit from explicit **heuristics**, clear **tool distinctions**, and **context window management** strategies like *compaction*.
- Structured prompts with XML/Markdown tags improve content digestion and consistency.
- Including **examples** and ordering analysis steps guides model reasoning and confidence.
- Rapid prototyping outperforms traditional documentation-heavy development, enabling faster discovery and course correction.
- Integrating AI for **feedback clustering and analysis** maximizes team responsiveness and product quality.
- Early-stage team sizes remain small (~3), with cross-role skill application to minimize overhead.
- Model improvements (e.g., new Claude versions) may automatically overcome prompt limitations.
- Consistent eval suites and LLM-as-judge frameworks foster robust, scalable prompt development.
- Agents exhibit unpredictable behavior; iteration and rollback on prompt changes are routine.
- Practical deployments balance latency, token costs, and accuracy through tooling and prompt engineering.
- Prototype-driven design with direct user feedback loops reduces long-term risk and accelerates value delivery.

By synthesizing these principles, developers and product teams can harness LLMs’ power more reliably and build effective AI-driven solutions across domains.

AI Note