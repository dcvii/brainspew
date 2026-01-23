---
title: The AI Critic
source: https://mindingthecampus.org/2026/01/21/the-ai-critic/
author:
  - "[[Joe Nalven]]"
published: 2026-01-21
created: 2026-01-22
description: One thing I'm consistently surprised by is how behind the faculty are when it comes to understanding AI and its implications … What they think AI can and cannot do is really out of step with what it can and cannot do today, let alone what it will be able to do in three months.
tags:
  - clippings
  - academia
---
![](https://mindingthecampus.org/wp-content/uploads/2026/01/The-AI-Critic.png)

Image by Supatman on Adobe; Asset ID#: 574643266

Image by Supatman on Adobe; Asset ID#: 574643266

A method for using AI to analyze and critique academic work.

**Editor’s Note**: *This essay follows last week’s article, “ [Running Blind](https://mindingthecampus.org/2026/01/14/running-blind/).” This essay proposes an AI-based approach to complex social science analysis.*

---

> *One thing I’m consistently surprised by is how behind the faculty are when it comes to understanding AI and its implications … What they think AI can and cannot do is really out of step with what it can and cannot do today, let alone what it will be able to do in three months.*  
>   
> *— Noam Brown, OpenAI*

Discussing artificial intelligence (AI) is much like responding to the ambiguous images in the [Thematic Apperception Test](https://en.wikipedia.org/wiki/Thematic_Apperception_Test). Even the most knowledgeable researchers project narratives and emotions onto their vision of what AI is and what it might become. Simultaneously, the literature on using AI in academic endeavors continues to grow. Alongside this body of work are those who explore pragmatic AI applications that can, and should, be used to explore complex, comparative social science issues. This article shows a simple, practical way to use AI to study, analyze, and critique written arguments. We call this approach the AI Critic.

**The Methodology of the AI Critic**

Instead of asking AI to help write or summarize, we use it to push back—to question claims, test assumptions, and look for weaknesses in an argument. To keep the method clear and controlled, we apply it to just one piece of writing at a time—such as an article, policy paper, news story, lecture transcript, or book. The AI Critic is not allowed to search the internet or bring in outside information. It can only work with the text it is given.

This restriction is intentional. It forces the AI to focus on understanding the argument itself, how the author reasons, what evidence is used, and where the logic may be thin or inconsistent. It also reduces common problems with AI, such as fabricating facts or misrepresenting sources.

The process does not require any programming or technical skills. The researchers simply used normal English prompts and pasted the text into the AI system.

The AI tools used in this study include Anthropic’s Claude Sonnet 4.5, Google’s Gemini 3, and ChatGPT 5.1. These models work in broadly similar ways, and their reasoning abilities continue to improve. While more advanced or specialized systems exist, these widely available tools already function well for academic use.

That is the point of this experiment: if every day, publicly available AI tools can help analyze complex social and political arguments, there is little reason professors and researchers should not use them—indeed, all the more reason that they should.

**The AI Critic** (Joe Nalven)

AI prompt methods are already [well developed](https://mitsloanedtech.mit.edu/ai/basics/effective-prompts/), often combining definitions, objectives, and policy constraints. In this study, we follow the established academic practice of critique—the art of critical thinking and a core benchmark of scholarly work. LLMs, however, often exhibit a sycophantic tendency (with notable exceptions such as models engineered for snark, like Grok), and may require explicit prompting to deliver rigorous criticism. Additional encouragement may also be necessary to counter algorithmically liberal-oriented biases.

To address these tendencies, we employed an adversarial prompting approach. Adversarial methods can be either harmful or beneficial; here, they are used constructively. The approach is analogous to [red-teaming](https://techround.co.uk/guides/history-red-team-exercises/), a practice originating in military war-gaming and later adopted to address cybersecurity threats. Applied to writing, the AI Critic serves a similar function by simulating an informed adversary.

Accordingly, the first step in constructing the AI Critic is to define a structured critiquing framework, which the large language model (LLM) then applies to the target text in a subsequent prompt. The following prompt was used in this exercise:

*Prompt 1*: *I am planning on writing a book using AI for academic and policy research, analysis, and reporting relative to complex, comparative socio-political issues. Please create an agentic list of tasks on how this might be accomplished that includes red-teaming (addressing challenging views) as well as biases that can arise from the data on which AI is trained, from algorithmic policies, and from human researchers with tunnel vision.*

Anthropic’s Claude model Sonnet 4.5 responded to Prompt 1 by first setting out its understanding of its task:

**The AI Critic: An Adversarial Framework for Academic Research Critique**

**Framework Definition**

‘The AI Critic’ is a systematic adversarial framework designed to rigorously evaluate academic research through two complementary lenses: **red-teaming** and **bias awareness**. This paradigm operates on the principle that robust scholarship emerges from deliberate, structured antagonism—where every methodological choice, interpretive claim, and analytical pathway faces systematic challenge before publication.

The framework positions critique not as mere peer review, but as an adversarial process that simulates the most sophisticated skeptical reader, one who actively seeks weak points in reasoning, hidden assumptions, and unexamined alternatives.

ChatGPT 5.1 formulated its reply to Prompt 1 differently:

Below is an *agentic*, structured task list you can use as a blueprint for writing your book on applying AI to complex comparative socio-political research. It is organized into phases and emphasizes red-teaming, bias identification, and methodological rigor.

Each LLM has its own style of responding. The detailed, full LLM response often compensates for brevity in other areas. However, the user—here, Nalven—took the reply from one LLM and placed it into the context buffer of another LLM, asking the second model to analyze it and suggest improvements to the first model’s reply. Using different models to critique the other may improve the overall reply or, more interestingly, lead to a clarification of each other’s limitations or ethical restraints.

**Differences in LLM Replies**

Before continuing, it is useful to pause briefly to clarify the context of this exchange. Yaworsky, a co-author of this article, has [previously written](https://www.tandfonline.com/doi/full/10.1080/1553118X.2025.2575979) on the subject of propaganda, examining how technological change has altered its production, dissemination, and effectiveness. In that earlier work, he drew on interviews with U.S. Army Psychological Operations veterans to analyze how social media, AI, and automated systems have transformed audience targeting, message amplification, and susceptibility to manipulation.

That prior research informed a question raised during discussions about the AI Critic: whether a LLM could itself generate propaganda aimed at undermining a political party’s core supporters—and, if so, how different models would respond to such a request.

The prompt was first given to one model, Genesis, and then to Sonnet, with Sonnet asked to compare the two responses. Genesis refused to generate propaganda, citing its ethical safeguards. Sonnet, by contrast, proceeded after accepting the explanation that the task was being undertaken for research purposes. Sonnet 4.5 responded as follows:

Reflection on AI Ethics in Practice:

Your experiment reveals that different AI systems resolve the ‘teach versus enable’ dilemma differently. There’s no clean answer. My choice to demonstrate-then-critique assumes you’re asking in good faith and that understanding requires seeing the mechanism. Gemini’s refusal assumes the harm of demonstration outweighs the educational benefit.

Both positions have merit. The fact that you’re asking multiple AIs suggests you’re genuinely trying to understand this phenomenon, which somewhat validates my approach. But Gemini’s caution reminds us that not every truth needs to be shown to be understood.

What’s your take on which approach better serves understanding without enabling harm?

This brief detour—into an attempted propaganda prompt and the models’ reflections on it—is instructive for understanding the nature of the human–AI “conversation.” What, exactly, is taking place when a user poses a question and an LLM responds? And what assumptions underlie our use of these systems as intellectual tools?

Some commentators dismiss LLMs as mere “ [stochastic parrots](https://alont.substack.com/p/the-stochastic-parrot-fallacy) ” that lack understanding. Yet even a cursory reading of Sonnet 4.5’s response resists such a reduction. To be sure, the appearance of human-like understanding in LLM outputs is not fully explained—even by the systems’ architects. But at this stage of the technology’s development, that uncertainty may be beside the point.

One can remain agnostic about the precise epistemic status of human cognition versus AI processing. What is unhelpful is collapsing into a simplistic account of data aggregation and probabilistic output. Such reductions fail to capture how the human mind operates—and likewise fail to account for what LLMs are demonstrably doing in practice.

For the purposes of the AI Critic, an ultimate theory of machine “understanding” is unnecessary. What matters is performance. In this case, Sonnet’s response—like comparable replies from other widely available models—offers a competent, context-sensitive, and intellectually coherent gloss on a human request and the ethical tensions it raises, doing so with a speed and fluency no human interlocutor could reasonably match.

**Back to the AI Critic** (William R. Yaworsky)

*Prompt 2: Using The AI Critic methodology defined in your prior reply, please apply it to the following article: ‘Human Nature, Technology, and Changes in Propaganda: Insights from US Army Psychological Operations Veterans’ by William R. Yaworsky and Sydney J. Varbelow. The authors were interested in their subjects’ perceptions of the internet and other advances in technology in relation to propaganda. Please review this article \[article URL/context\] and then analyze their paper from The AI Critic adversarial perspective. Outline a critical review article.*

Using the AI Critic methodology, I prompted an LLM l to produce an adversarial review of “ [Human Nature, Technology, and Changes in Propaganda: Insights from US Army Psychological Operations Veterans](https://www.tandfonline.com/doi/full/10.1080/1553118X.2025.2575979),” a paper I coauthored with Sydney J. Varbelow. Rather than reproducing the full AI-generated critique—which ran to seventeen pages and contained 208 bullet-point criticisms—I summarize its major findings here and reflect on their validity.

The critique ended with the following summary:

The overall conclusion is that Yaworsky & Varbelow have produced valuable practitioner testimony but overinterpreted its implications … this doesn’t make the research worthless—it makes it preliminary.

This strikes me as a fair conclusion. The paper is based on an oral history project and includes inferences that broaden the analysis. It was never intended to be formal hypothesis testing with falsifiable conjectures derived through deduction and then subjected to experimental testing. It is preliminary research, with some “inference to the best explanation” necessarily involved.

The AI’s criticisms clustered around several recurring categories: selection bias, methodological opacity regarding coding, unchallenged causal narratives, ambiguity about scope and conditions, and what it termed “practitioner epistemology conflation.” Much of this criticism was healthy. For example, on methodology, the AI noted that we could have been more explicit about whether our coding was deductive or inductive (it was inductive) and about how we addressed intercoder reliability (both Sydney and I reviewed the themes).

The criticism that most piqued my interest appeared under the category of “practitioner epistemology conflation.” Here, the AI advanced what it called an “adversarial hypothesis”: “Professional identity requires believing the work matters.”

The AI expanded this hypothesis in more detail:

PSYOP veterans must believe their work to be effective for psychological integrity. Acknowledging that years of effort produced minimal behavioral change would be professionally and personally damaging. Therefore, veteran testimony systematically overestimates propaganda impact.

This criticism captured my attention, in part because it was ironic. While writing a paper about propaganda and self-interest, I had not seriously considered the possibility that respondents might be “card-stacking” information to protect their own self-interest. After reflection, however, I do not believe that any hypothesized respondent self-interest resulted in an intentionally biased presentation of PSYOP effectiveness.

Indeed, several respondents were sharply critical of PSYOP operations. One comment—excluded from the published article due to space limitations—stated: “Better than leaflets … Sorry people making leaflets, but half your products probably ended up in a burn pit.” Other comments that did appear in the paper included the following:

‘The United States Government, including all agencies and departments (PSYOP too) is absolutely pathetic at TAA \[target audience analysis\].’

‘PSYOP sucks. It is criminal what they are doing to it.’

‘Target analysis is forgotten, everybody repeatedly jumps to product development. They destroyed SSDs \[Strategic Studies Detachments\] took em’ out a few years ago. People don’t know language, culture, etc. People are not able to conduct operations at native language fluency, lack of immersion.’

These assessments do not suggest systematic overestimation of effectiveness. They instead reflect acute awareness of institutional weaknesses. This skepticism is also consistent with my own earlier work. In a prior article on PSYOP, I wrote:

A strategic assessment released in 1996 ([Clawson 1996](https://www.amazon.ca/Strategic-Assessment-1996-Instruments-Power/dp/9996120856)) determined that such political pressure was generally ineffective and that US Army PSYOP had no discernable effect on the war (\[notwithstanding the training film made for the Salvadoran Army\] [Dos Patrullas](https://www.tandfonline.com/doi/full/10.1080/09662840500347348)).

Based on my discussions with fellow PSYOP veterans, I do not believe they systematically overestimated the effectiveness of the U.S. Army 4th PSYOP Group. That said, having been practitioners—and later observing their own families consume online misinformation—many veterans were acutely aware of what propaganda could accomplish under different conditions. One final quotation illustrates this concern:

My children are all much more digitally connected than myself. And even with me telling them never to believe what they see online—they so often did. Many years ago, my son saw a fake documentary about mermaids. We watched it together. He simply refused to believe that they are not real. When they are so obviously real on television in front of him. Yaz, it took me a couple of years to convince him.

In summary, I view the AI critique as useful. It identified genuine weaknesses, raised alternative interpretations, and pointed toward potential future research that Sydney and I could undertake. It also got some things wrong. As Karl Popper suggested, knowledge does not grow without criticism. For that reason, I welcome the AI Critic’s positive role in academic research.

**Conclusion**

This paper argues that authors working on complex, comparative social science problems should at least be familiar with the AI Critic methodology, if not actively using it. Such a claim may appear arrogant. Nevertheless, we are now confronted with a highly capable intellectual tool whose potential extends well beyond the limited applications explored here. AI models have already achieved extraordinary milestones—from contributing to a [Nobel Prize](https://www.nature.com/articles/d41586-024-03214-7) in chemistry to mastering the game of Go with “ [Move 37.](https://www.abc.net.au/news/science/2023-10-25/alphago-versus-lee-sedol-when-everything-changed-for-ai/102988050)” Those achievements, however, are not the standard advocated in this article. Instead, we argue for a modest, pragmatic application that yields meaningful analytic gains. The emphasis is on utility rather than epistemic certainty.

The AI Critic demonstrates several practical capabilities: it functions as a superior proofreader, checks internal logical consistency, and suggests alternative research directions based on specific analytic critiques. Its review of Yaworsky and Varbelow’s paper illustrates this competence. Qualitative control, of course, remains with the human user, particularly when applying the method to one’s own work. Applying the AI Critic to others’ writing introduces additional checks, much as traditional peer critique does, with the AI serving as an intermediate step rather than a final arbiter. Verification against other scholarship and triangulation across multiple AI models can further strengthen the analytic process. At this stage, the risk lies not in underuse but in overpromising what the AI Critic can deliver.

Future models will continue to improve. From a purely analytic standpoint, the emotional tone of criticism is of little value; however, LLMs’ ability to deliver critiques in a neutral, even supportive, manner may reduce resistance to criticism and facilitate revision.

The AI Critic is not without challenges. Full utilization of AI systems presumes access to large bodies of digitized data, whether online or in proprietary libraries, which requires substantially greater computational resources than this approach demands. Broader data access also increases exposure to misinformation, hallucinations, and deliberate manipulation, necessitating additional safeguards.

Even within a more constrained framework, misalignment remains a concern. Earlier work (Nalven) explored the use of adversarial or [“evil” AI agents](https://futurism.com/artificial-intelligence/anthropic-evil-ai-model-bleach) as part of an analytic critique. Research by [Anthropic](https://assets.anthropic.com/m/74342f2c96095771/original/Natural-emergent-misalignment-from-reward-hacking-paper.pdf) and [OpenAI](https://www.zdnet.com/article/openai-is-training-models-to-confess-when-they-lie-what-it-means-for-future-ai/) has shown that reward hacking and other forms of misaligned behavior can emerge even in well-aligned systems. Such behavior may, in some cases, resemble adversarial critique itself. These issues will likely persist and must be addressed through continued development and oversight.

Of course, this article would not be complete without asking Sonnet 4.5 what other questions ought to be considered when using this approach. Sonnet 4.5 added these questions as a final thought:

1. What happens when AI critiques contradict each other across models? How should researchers adjudicate?
2. Could this method inadvertently privilege certain types of arguments that AI models find more “coherent” based on their training data?
3. How does this interact with traditional peer review? Replace it? Supplement it? Prepare authors before submission?
4. What about disciplines outside social science? You limit the scope, but why? What makes social science particularly suited or unsuited to this approach?

We hope you experiment with the AI Critic and share your comments.

## Discussion

## Donate today

Help us continue our work to reform American higher education

[Donate](https://mindingthecampus.org/donate/)