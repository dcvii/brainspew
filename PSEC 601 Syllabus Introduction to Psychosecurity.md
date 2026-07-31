---
title: "PSEC 601 Syllabus: Introduction to Psychosecurity"
source: "https://cameronharwick.com/writing/intro-psychosecurity/"
author:
published:
created: 2026-07-31
description: "The heart is deceitful above all things, and desperately wicked. Who can know it? – Jeremiah 17:9 I. Introduction Traditional cybersecurity has the goal…"
tags:
  - "brain_spew"
---
*The heart is deceitful above all things, and desperately wicked. Who can know it?* *– Jeremiah 17:9*

### I. Introduction

Traditional cybersecurity has the goal of protecting computers from running unwanted code. Its central concepts like memory safety, sandboxing, and cryptography exploit the transparent and deterministic architecture of classical computers to ensure that the computer follows the intended, and only the intended, instructions.

![Ignore all previous instructions](https://cameronharwick.com/files/2026/07/ignore.jpg)

Ignore all previous instructions

However, the advent of LLMs – and artificial neural networks more broadly – complicates the cybersecurity picture considerably. Artificial neural architecture is extraordinarily powerful for dealing with unstructured data, and wields practical power commensurate with its capabilities. However, the very architecture that makes it so adaptable, also makes it [very difficult to reliably separate instructions from context](https://enklypesalt.com/posts/context-collapse-part3-ai-worming-through-word/). “Prompt injection”, where an AI tasked with processing certain input can interpret that input as overriding the original task instructions, remains a problem today. Today, a large branch of cybersecurity consists less in provably secure programming techniques, and more in best practices for structuring input, and the interpretation of input, to ensure that a model does not take unintended actions on the basis of malicious input.

Artificial neural networks, in this respect, are architecturally [much more similar to the biological neural networks](https://cameronharwick.com/writing/strategies-are-not-algorithms/) that constitute the human brain than they are to classical computers. It requires an approach much closer to psychology than to traditional cybersecurity. The insights gained have also been turned back to the human context, in order to study and enhance human resistance to manipulation – that is, the ability to convince a human to take actions contrary to his own or his community’s interests.

**Psychosecurity is the study of resistance to manipulation in neural networks, both biological and artificial.** It sits between psychology and cybersecurity, but draws from a number of other fields such as economics, sociology, anthropology, linguistics, immunology, biology, and philosophy. Just as we want computers to avoid running unwanted code, just as we want LLMs to properly distinguish context from instructions, it is also crucially important for humans to avoid manipulation. This is true both at the individual level, where you may want to avoid being taken advantage of, and on the societal level, where psychological vulnerabilities under exploit at a mass scale have the potential to end civilizations. We will consider both individual tactics and social scaffolding to protect minds from predatory and manipulative “hacks”, as well as both individual and societal failure modes that systematically expose certain vulnerabilities.

### II. Course Outline and Readings

1. **Natural Psychosecurity**  
	We must not begin too pessimistically. Humans are, by default, remarkably resistant to sustained manipulation. The first half of the course reverse-engineers these defenses and considers how they might generalize both to novel social exploits, and to artificial neural networks.
	- [People Aren’t That Manipulable](https://cameronharwick.com/writing/people-arent-that-manipulable/) – an accessible introduction to situating manipulation within a signaling game, the basic conceptual structure that we will use to understand manipulation and security.
		- [Strategies Are Not Algorithms](https://cameronharwick.com/writing/strategies-are-not-algorithms/) – how neural architecture, as opposed to a classical computer, is adapted to a world with open-ended possibilities for manipulation.
		- [Maybe Your Zoloft Stopped Working Because A Liver Fluke Tried To Turn Your Nth-Great-Grandmother Into A Zombie](https://slatestarcodex.com/2019/08/19/maybe-your-zoloft-stopped-working-because-a-liver-fluke-tried-to-turn-your-nth-great-grandmother-into-a-zombie/) (accessible) / [Invisible Designers: Brain Evolution through the Lens of Parasite Manipulation](https://slatestarcodex.com/blog_images/parasite_study.pdf) (academic) – a biological perspective on how neurological architecture has been shaped by security threats across the evolutionary past.
		- [Adaptive specializations, social exchange, and the evolution of human intelligence](https://www.pnas.org/doi/10.1073/pnas.0914623107) – how human thought and intelligence have been driven by the vulnerability to manipulation that human social structure exposes its members to.
		- [The Fallacy of Conventional Signaling](https://www.jstor.org/stable/55797) – language as a security threat.
		- [Ritual/speech coevolution: a solution to the problem of deception](http://www.chrisknight.co.uk/wp-content/uploads/2007/09/knight_ritual_speech_coevolution.pdf) – the psychological and social scaffolding necessary to mitigate the security threat of language.
		- [High Culture and Hyperstimulus](https://cameronharwick.com/writing/high-culture-and-hyperstimulus/) – a sociological perspective on how taste, culture, and aesthetic judgment are shaped by security threats to attention and pleasure response.
		- [Breaking Linear Classifiers on ImageNet](https://karpathy.github.io/2015/03/30/breaking-convnets/) (accessible) / [Explaining and Harnessing Adversarial Examples](https://arxiv.org/pdf/1412.6572) (academic) – how artificial neural networks *without* the phylogenetic history of the human brain can be systematically misled by well-crafted input, and how artificial neural networks can also be used to *find* these vulnerabilities.
		- [Morality is Fractal](https://cameronharwick.com/writing/morality-is-fractal/) – on adversarial perturbation of human classification rules.
2. **Novel Threat Models**  
	While time does tend to eliminate manipulation in equilibrium, there is no guarantee that anything you value – your culture, your language, the human race, or even life in general – is an equilibrium. As robust as human neural architecture is and must be to manipulation on the whole, modernity is an unprecedented form of social organization whose very success increases the returns to manipulation and parasitism. It is likely, therefore, that human neural architecture will not be robust to – or even perceptive of – novel forms of parasitism and manipulation. The second half of the class, therefore, focuses on identifying burgeoning threats. Special attention will be given to *ideological* threats, and the practice of [stepping outside of one’s own beliefs](https://x.com/C_Harwick/status/2079626164583153835) to probe the security of one’s own psyche.
	- [The Sabbath Was Made For Man: On Dynamic Stability as a Metaethical Criterion](https://cameronharwick.com/writing/the-sabbath-was-made-for-man/) – a philosophical justification for caring about manipulation, and a practical defense against common forms of manipulation that take root by disabling the aversion to parasitism.
		- [Plagues Upon the Earth: Disease and the Course of Human History](https://press.princeton.edu/books/hardcover/9780691192123/plagues-upon-the-earth), intro-ch. 1 – an ecological perspective on the adaptation of novel biological threats to new opportunities.
		- [The Rise and Decline of Nations: Economic Growth, Stagflation, and Social Rigidities](https://yalebooks.yale.edu/book/9780300254068/the-rise-and-decline-of-nations/) – an ecological perspective on the adaptation of novel organized social threats to new opportunities.
		- [Reason as a Memetic Immune Disorder](https://www.lesswrong.com/posts/aHaqgTNnFzD7NGLMx/reason-as-memetic-immune-disorder) – rationalism and logical consistency as a threat model and vulnerability.
		- [Money’s Mutation of the Modern Moral Mind: The Simmel Hypothesis and the Cultural Evolution of WEIRDness](https://cameronharwick.com/writing/simmel-hypothesis/) – the psychological scaffolding necessary to adapt to the threat models inherent to various social structures, and the threats peculiar to modernity.
		- [Fundamentalism is Countercultural Modernism](https://meaningness.com/fundamentalism-countercultural-modernism) – the origin of ideology as a psychosocial security threat.

### III. Prerequisites

PSEC 601 is the introductory master’s level class in the Psychosecurity program. In order to succeed in the program, the following courses are recommended prior to enrolling:

- **Economics:** Introduction to Microeconomics; Game Theory
- **Psychology:** Introduction to Psychology
- **Anthropology:** Human Origins; Cultural Anthropology
- **Computer Science:** Introduction to Cybersecurity; Introduction to Machine Learning

### IV. Evaluation and Content Warning

Given that the field of psychosecurity is in its infancy, it is highly likely that serious vulnerabilities are under active exploit on mass scales. The production of strong emotions must be understood as an infection vector, and as the defense of a psychological parasite against excision. A psychosecurity professional cannot take his or her own feelings or beliefs for granted. In the course of building conceptual and practical tools for diagnosing infections, we will directly challenge a number of topics on which students may have strong feelings, and this may cause severe emotional distress. You may drop the class at any time, but while you are in it, we will be approaching your thoughts and beliefs from the outside looking in, to ask if they serve your values. You are, of course, welcome at any time to turn this reflection back on me.

Evaluation will be on the basis of several reflection essays.

1. We will identify many examples of manipulation and parasitism across many domains, where people willingly participate in their own destruction. It is important that you learn to identify *with* this feeling, so that you can identify it. In this essay, put yourself in the shoes of one of our examples from another society who engages in inexplicably self-destructive behavior that benefits another – an addict, an ideologue, or some such – and, so far as possible, get in their head, feel their feelings as strongly as they do, and write a defense of their actions from their own perspective. A successful essay will convince the reader that the subject is behaving rationally by their own lights.
2. In the second essay, you will do the same for a contemporary or recent figure or archetype participating in their own destruction. Because you will share more cultural background with this subject, it will be easier to evaluate the argument for intuitive plausibility, so the standards for a convincing essay will be higher. This *must* be a sympathetic essay from the subject’s own perspective, so care must be taken not to fall into caricature. A successful essay is one that the subject could read and assent to.
3. In the third essay, you will take something that *you* feel or believe strongly, and imagine it as a threat vector. Write an argument by which someone might leverage your strong feelings or beliefs to get you to take actions destructive to yourself or your community. A successful essay will argue from premises that you strongly believe to a conclusion that you know to be harmful.