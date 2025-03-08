---
title: What is ChatDev? | IBM
source: https://www.ibm.com/think/topics/chatdev
author:
  - "[[Vanna Winland]]"
  - "[[Erika Russi]]"
published: 2024-09-16
created: 2025-02-18
description: ChatDev is an open source agentic framework that implements multiagent collaboration via an organized team of specialized intelligent agents powered by large language models (LLMs).
tags:
  - clippings
---

## What is ChatDev?

ChatDev is an open source agentic framework that implements multiagent collaboration through an organized team of specialized intelligent agents that are powered by [large language models (LLMs)](https://www.ibm.com/topics/large-language-models). Each [AI agent](https://www.ibm.com/think/topics/ai-agents) is orchestrated to collaborate on tasks within the core phases of the software development lifecycle to autonomously generate and produce a software application.[](https://www.ibm.com/think/topics/ai-agents)

ChatDev simulates a virtual software company that operates through various intelligent agents holding different roles within the organization’s environment. These agents form a multiagent organizational structure where they can collaborate by participating in functional seminars that aid in streamlining the software development process. ChatDev applies AI to the widely adopted “waterfall” model, a software development lifecycle model that breaks down the development process into phases: designing, coding, testing and documenting. Specialized agents work collaboratively to complete each phase.

ChatDev’s primary objectives are to offer a customizable and scalable agentic [LLM orchestration](https://www.ibm.com/think/topics/llm-orchestration) framework and to serve as an ideal scenario for studying collective intelligence. Collective intelligence is effective collaboration, the phenomenon where a group can outperform an individual in a complex task. The widely accepted approach to collective intelligence defines individuals as entities that can act with purpose and reason and adapt to an environment.[1](https://www.ibm.com/think/topics/chatdev#f1) In agentic frameworks like ChatDev, these intelligent entities are known as agents.

## Collective intelligence in multiagent systems (MAS)

Collective intelligence applications in AI and machine learning include collective intelligence systems or frameworks called [multiagent systems (MAS)](https://www.ibm.com/think/topics/multiagent-system). A MAS can be described as an interconnected network of problem-solving entities, or agents, that collaborate to solve problems that exceed the capabilities or knowledge of a single agent.[2](https://www.ibm.com/think/topics/chatdev#f2)

AI tools like multiagent systems are an approach to collective intelligence (COIN) design. COIN is an extensive multiagent system that is characterized by minimal to no centralized communication or control. It features a world utility function that evaluates the potential histories of the entire system.[3](https://www.ibm.com/think/topics/chatdev#f3) The field of MAS is concerned with the interactions among agents within the system as well as the makeup of each agent themselves. Although there are several ways to design a MAS, the core goal remains the same: to achieve a global task through the actions of its components.

## Cooperative multiagent interactions

One of the most difficult steps in the design of a functional MAS is the coordination of the agents in a way that helps ensure that they cooperate on the global task.[4](https://www.ibm.com/think/topics/chatdev#f4) Effective collaboration requires both individual task-solving abilities and well-coordinated interactions among participating individuals.[5](https://www.ibm.com/think/topics/chatdev#f5) Planning a MAS environment involves the following considerations:

1. The constraints that the other agents’ activities place on an agent’s choice of actions
2. The constraints that an agent’s commitments to others place on an agent’s choice of actions
3. The unpredictable evolution of the world that is caused by other, unmodeled agents[6](https://www.ibm.com/think/topics/chatdev#f6)[](https://www.ibm.com/think/topics/chatdev#_ftn3)

One way to approach this design challenge is to model teamwork explicitly through multiagent collaboration.

The multi-collaborative design pattern breaks down a complex prompt and delegates the abstracted tasks to agents who execute them based on their specialized roles.[7](https://www.ibm.com/think/topics/chatdev#f7) For example, ChatDev uses a dual-agent communication design that is called ChatChain to facilitate cooperative communication.

## How does ChatDev work?

Frameworks like ChatDev expand the functionality of LLMs beyond their exceptional natural language processing capabilities for text generation. ChatDev positions LLMs as versatile agents through its orchestration techniques that involve prompting and evaluating multiple collaborative agents with various social roles (for example software engineer, chief technology officer, chief executive officer, designer, tester).

Each agent uses their specialized role to work collaboratively on the core phases of the software development lifecycle. This process involves extensive communication among agents in their specialized roles to comprehend and analyze requirements through natural language, and development and debugging using programming languages. Phases in the ChatChain have varying levels of engagement in both natural and programming languages depending on the agents’ role and prompt.

### How ChatDev prompts its autonomous AI Agents

ChatDev’s agents use role-playing and inception prompting as guides to complete their tasks. Inception prompting is a conversational LLM auto-prompting method that enables agents to prompt each other to solve tasks through role-playing.[8](https://www.ibm.com/think/topics/chatdev#f8)

ChatDev applies [prompt engineering](https://www.ibm.com/topics/prompt-engineering) at the start of each subtask phase. Although ChatChain does well at defining the task-solving process, agents simply exchanging responses without any additional prompting or guardrails is not effective for multi-round, task-oriented communication. To advance the progression of productive communications and avoid challenges like role flipping, instruction repeating and fake replies, ChatDev employs an inception prompting mechanism.

The inception prompting mechanism works by hypnotizing the LLMs with the instructor and the assistant system prompt as they are instantiated. [LLM hypnosis](https://securityintelligence.com/posts/unmasking-hypnotized-ai-hidden-risks-large-language-models/?utm_medium=OSocial&utm_source=Youtube&utm_content=RSRWW&utm_id=YT-201-Hypnotized-AI-and-Large-Language-Model-Security) can have a negative connotation (it can be used maliciously to manipulate a model) but in this case, it is a way to effectively prompt role-playing agents. In the prompt, tasks and roles are specified to help ensure that the LLM is instructing agents on how to fulfill their collaborative role and follow instructions.

These initial prompts for each role guide agents to give appropriate responses without role-flipping. The prompts for both roles in the system are nearly identical, addressing the overview and goals of the current subtask, the specialized roles, available external tools, communication protocols, termination conditions and constraints or requirements to prevent undesirable behaviors.[9](https://www.ibm.com/think/topics/chatdev#f9) This mechanism functions like an LLM guardrail, enhancing the quality of responses and reducing the need for human intervention.

### How AI agents interact in ChatDev

To guide proper cooperative communication between agents, ChatDev introduces an agentic workflow that is called ChatChain to further break down each phase into more manageable subtasks. This process guides multi-turn communications between different roles to propose and validate solutions for each subtask. Agents are governed with a mechanism called a communicative dehallucination, a communicative pattern to alleviate unexpected [hallucinations](https://www.ibm.com/topics/ai-hallucinations). With this mechanism, agents request more detailed information before responding directly and then continuing the next phase of communication based on these details.[10](https://www.ibm.com/think/topics/chatdev#f10)

ChatDev provides a browser-based visualizer to study the interactions of each individual agent acting within its role and environment. This interface provides users with the ability to investigate the multiagent system design itself. Users can view the artificial cooperation structure that allows the agents to work together to complete a global task beyond their individual capabilities.

#### ChatChain

ChatChain follows a dual-agent communication design that simplifies the task-solving process along the agentic workflow. The agentic design pattern begins by segmenting the software development process into three sequential phases: design, coding and testing. The coding and testing phases are further broken up into subtasks: code writing and completion, and code review (static testing) and system testing (dynamic testing).

Each communication phase within a ChatChain is made of one instructor agent and one assistant agent. In each subtask, two agents with distinct specialized roles (such as a reviewer and a GUI design programmer) fulfill the functions of an instructor and an assistant. The instructor agent instructs the discourse toward the completion of a task while the assistant agent receives and follows these instructions and responds with appropriate solutions.[11](https://www.ibm.com/think/topics/chatdev#f11) The agents engage in multi-turn dialog until the task is complete or consensus is reached. Solutions extracted from the communication phase range from text (for example a description of the application’s wanted functionality) to code (for example the initial source code).

This agentic workflow simplifies communications by avoiding complicated multiagent topologies and effectively streamlining the consensus process.[12](https://www.ibm.com/think/topics/chatdev#f12) This approach provides a smooth transition between subtasks, as solutions from previous tasks serve as bridges to the next phase. This workflow continues until all subtasks are completed, guiding agents along the way. The workflow’s chain-style structure links natural language and programming-language subtasks, effectively guiding agents on what to communicate. ChatChain is one solution to the most challenging problem of MAS design, agentic cooperation. 

Using the default settings, the ChatChain produces software in the following order:

- **Demand analysis:** Decide the overall method procedure process for the application.
- **Language selection:** Decide what programming language to use to build and run the software.
- **Coding:** Agents write the code to build the application.
- **CodeCompleteAll**: Complete the code including missing functions/classes.
- **CodeReview:** Review and modify the code for functionality.
- **Test**: Run the software and modify the code based on the test report.
- **EnvironmentDoc:** Document the environment.
- **Manual:** Document and write a manual for the application.

#### Communicative Dehallucination

LLM hallucinations occur when models produce inaccurate or nonsensical output. Coding hallucinations are a type of hallucination that affects the outputs of models performing programming-related tasks. ChatDev’s researchers have found that coding hallucinations frequently appear when the agent performing the assistant functionality struggles to follow precise instructions.[13](https://www.ibm.com/think/topics/chatdev#f13) Assistants struggle to comply with instructions typically due to vagueness that requires multiple follow-up interactions and adjustments. To avoid undesirable outputs, ChatDev introduces communicative dehallucination.[](https://www.ibm.com/think/topics/chatdev#f13)

Communicative dehallucination prompts the assistant to actively request more detailed suggestions from the instructor before providing a formal response.[14](https://www.ibm.com/think/topics/chatdev#f14) Assistants take on an instructor-like role and proactively seek more information (for example the precise names of external dependencies, or which GitHub repository to commit changes to), taking on a deliberate “role reversal” before delivering a response. The assistant performs precise optimization after the instructor responds with modifications. The communication pattern instructs agents on how to communicate, enabling fine-grained information exchange while also reducing coding hallucinations.

### Visualizer

ChatDev’s Visualizer is a Python app that runs a local web demo where users can view real-time logs, replayed logs and ChatChain. The app contains three separate log viewers for each.

- **Log Visualizer:** A real-time log that prints the agent’s dialog information, environment changes and other system information useful for debugging.
- **Replay Visualizer:** The replay log prints the dialog information of the agent.
- **ChatChain Visualizer:** Users can upload any ChatChain configuration file and view the agentic workflow chain for any current or previous software projects. This feature offers a transparent view of the entire software development process for users to examine each subtask solution and identify any possible inefficiencies.

The Visualizer also contains a Chat Replay page that shows the dialogs in natural languages between agents for a given generated software application.

### ChatDev’s LLM Integration

The concept of ChatDev's agentic design pattern is like the [mixture of experts](https://www.ibm.com/topics/mixture-of-experts) machine learning technique except its AI agents that are specialized experts handling complex tasks. Orchestration systems are needed to coordinate collaboration among a mixture of specialized agents.

The foundation of such orchestrations is pre-trained transformer models like OpenAI’s GPT models.[15](https://www.ibm.com/think/topics/chatdev#f15) Foundation models like [IBM’s granite series](https://www.ibm.com/products/watsonx-ai/foundation-models?utm_content=SRCWW&p1=Search&p4=43700078747002614&p5=e&p9=58700008385933274&gclid=CjwKCAjw59q2BhBOEiwAKc0ijRy9x1fr5cDzy3o6fdX2mFp-a8m-reH-nA2FZk0htpcbmVcWdMq8pRoCRtsQAvD_BwE&gclsrc=aw.ds) can also be used to ground agents with robust language capabilities and grant them specialized functionality. For instance, Granite Code is a family of models ranging from 3B and 34B parameter sizes and is trained on 116 programming languages. This offering is beneficial for agentic frameworks planning on using communicative agents for software development. At the time of writing, ChatDev supports OpenAI’s GPT-3.5-turbo and GPT-4 models to power their intelligent agents.

### How ChatDev scales

ChatDev is implementing a way to scale LLM-based multiagent collaboration with multiagent collaboration networks (MacNet). MacNet is inspired by the neural scaling law, which suggests that increasing neurons leads to emergent abilities.[16](https://www.ibm.com/think/topics/chatdev#f16) ChatDev proposes a similar principle that applies to increasing agents in multiagent collaboration.

MacNet uses acyclic graphs to structure agents and enhance their interactive reasoning through topological ordering. Solutions are derived from the agents’ interactions. This process consistently outperforms baseline models, facilitating efficient collaboration among agents across different network topologies and accommodating cooperation between more than a thousand agents. Through this application, ChatDev identified a collaborative scaling law that shows that the quality of solutions improves in a logistic growth pattern as the number of agents increases.

## Multiagent systems for software development

Rather than trying to encompass all capabilities within a single model, multiagent systems divvy up tasks among several specialized agents. Agents can use the same language model or different ones, providing them the potential to accomplish a wide range of tasks.

ChatDev did an evaluation in a popular research paper that compares performances of itself and two other LLM-based software development orchestration frameworks, GPT-Engineer and MetaGPT. The metrics were based on completeness, executability, consistency and quality. ChatDev and MetaGPT outperformed GPT-Engineer, a single-agent orchestration approach, demonstrating that complex tasks are more challenging to solve in a single-step solution. These performance results suggest that breaking down complex tasks into more manageable subtasks enhances the effectiveness of task completion.

ChatDev outperformed MetaGPT significantly in the quality metric due to the agents' cooperative communication methods that use both natural and programming languages. Agents that are capable of efficient communication were able to guide each subtask to completion, overcoming the restrictions that are typically linked to manually established optimization rules.[17](https://www.ibm.com/think/topics/chatdev#f17) This outcome suggests that multiagent frameworks that use communicative and collaborative agents offer more versatile and adaptable functions.

## Other multiagent frameworks

**GPT-Engineer** – A single agent orchestration framework for building software applications. The user prompts the AI to build an application with the wanted software functionality and can communicate back and forth with the system to make improvements or updates.[18](https://www.ibm.com/think/topics/chatdev#f18) Users are able to benchmark their own agent implementations against popular datasets through ‘bench,’ a binary installed in the system that contains a simple benchmarking interface.

**MetaGPT** – A multiagent framework that operates as a collaborative software entity that assigns different role-playing agents to GPT models to complete complex tasks. Like ChatDev, agents maintain various roles within a virtual environment akin to a software company. MetaGPT also uses carefully orchestrated SOPs (Standard Operating Procedures) to generate software.

**crewAI** – [crewAI](https://www.ibm.com/think/topics/crew-ai) is an open-source multiagent framework that operates on LangChain. It organizes autonomous AI agents into teams that handle workflows and tasks that are related to LLM applications. crewAI integrates with any LLM.

**AutoGen** – Microsoft’s open-source multiagent conversation framework provides an elevated abstraction of foundation models. AutoGen is an agent-based framework that employs multiple agents to interact and address tasks. Its key features include customizable AI agents that participate in multiagent dialogs with adaptable patterns, enabling the creation of diverse LLM applications.




1 Leimeister, J.M. “Collective Intelligence.” *Bus Inf Syst Eng* **2**, no.4 (June 24, 2010): 245–48. [https://link.springer.com/article/10.1007/s12599-010-0114-8](https://link.springer.com/article/10.1007/s12599-010-0114-8).

2 E. H. Durfee and V. Lesser, "Negotiating Task Decomposition and Allocation Using Partial Global Planning," in *Distributed Artificial Intelligence Volume II*, ed. L. Gasser and M. Huhns (London: Pitman Publishing; San Mateo, CA: Morgan Kaufmann, 1989), 229–244.

3 Wolpert, David H. and Kagan Tumer. "An introduction to collective intelligence." *arXiv preprint cs/9908014* (1999). [https://arxiv.org/abs/cs/9908014](https://arxiv.org/abs/cs/9908014).

4 Leimeister, J.M. “Collective Intelligence.” 3-4.

5 Li, Yuan, Yixuan Zhang and Lichao Sun. "Metaagents: Simulating interactions of human behaviors for llm-based task-oriented coordination via collaborative generative agents." *arXiv preprint arXiv:2310.06500* (2023). [https://arxiv.org/abs/2310.06500](https://arxiv.org/abs/2310.06500). 

6 Nicholas R. Jennings, Katia Sycara and Michael Wooldridge, “A Roadmap of Agent Research and Development,” *Autonomous Agents and Multi-Agent Systems* 1, no. 1 (1998): 7–38, [https://link.springer.com/article/10.1023/A:1010090405266](https://link.springer.com/article/10.1023/A:1010090405266).

7 DeepLearning.AI, “Agentic Design Patterns Part 5, Multi-Agent Collaboration Prompting an LLM to Play Different Roles for Different Parts of a Complex Task Summons a Team of AI Agents That Can Do the Job More Effectively.,” Agentic Design Patterns Part 5, Multi-Agent Collaboration, April 17, 2024, [https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-5-multi-agent-collaboration/](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-5-multi-agent-collaboration/).

8 Li, G., Hasan Hammoud, Hani Itani, Dmitrii Khizbullin and Bernard Ghanem. “CAMEL: Communicative Agents for "Mind" Exploration of Large Scale Language Model Society.” *ArXiv* abs/2303.17760 (2023). [https://arxiv.org/abs/2303.17760](https://arxiv.org/abs/2303.17760).

9 Qian, Chen, Wei Liu, Hongzhang Liu, Nuo Chen, Yufan Dang, Jiahao Li, Cheng Yang et al. "Chatdev: Communicative agents for software development." In *Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, pp. 15174-15186. 2024. [https://arxiv.org/abs/2307.07924](https://arxiv.org/abs/2307.07924).

10 Qian, et al. "Chatdev: Communicative agents for software development." 15178-15179.

11 Qian, et al. "Chatdev: Communicative agents for software development." 141773.

12 Qian, et al. "Chatdev: Communicative agents for software development." 151784.

13 Qian, et al. "Chatdev: Communicative agents for software development." 15179.

14 Qian, et al. "Chatdev: Communicative agents for software development."15179.

15 Duncan, Dennis. “Mixture of Agents Model (MAM): An AI-Driven Full-Stack Development Team,” Hugging Face – The AI community building the future. [https://huggingface.co/blog/dnnsdunca/mam-model#mixture-of-agents-model-mam-an-ai-driven-full-stack-development-team](https://huggingface.co/blog/dnnsdunca/mam-model#mixture-of-agents-model-mam-an-ai-driven-full-stack-development-team).

16 Qian, Chen, Zihao Xie, Yifei Wang, Wei Liu, Yufan Dang, Zhuoyun Du, Weize Chen, Cheng Yang, Zhiyuan Liu and Maosong Sun. "Scaling Large-Language-Model-based Multi-Agent Collaboration." *arXiv preprint arXiv:2406.07155* (2024). [https://arxiv.org/abs/2406.07155](https://arxiv.org/abs/2406.07155)

17 Qian, et al. "Chatdev: Communicative agents for software development." 15180.

18 Gpt-Engineer-Org, “GPT-Engineer-Org/GPT-Engineer,” GitHub, [https://github.com/gpt-engineer-org/gpt-engineer](https://github.com/gpt-engineer-org/gpt-engineer).