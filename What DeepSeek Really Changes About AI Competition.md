---
title: "What DeepSeek Really Changes About AI Competition"
source: "https://www.rand.org/pubs/commentary/2025/02/what-deepseek-really-changes-about-ai-competition.html"
author:
  - "[[Konstantin F. Pilz]]"
  - "[[Lennart Heim]]"
published: 2025-02-04
created: 2025-02-06
description: "DeepSeek's models are freely downloadable by anyone. If Chinese companies continue to develop the leading open models, the democratic world could face a critical security challenge: These widely accessible models might harbor censorship controls or deliberately planted vulnerabilities that could affect global AI infrastructure."
tags:
  - "clippings llm"
---
- [Skip to page content](https://www.rand.org/pubs/commentary/2025/02/#page-content)

[![RAND](https://www.rand.org/etc/rand/designs/common/images/logo-corp.svg)](https://www.rand.org/)

[Toggle Menu](https://www.rand.org/site_info/sitemap.html)

## Site-wide navigation

- ### Research Divisions

RAND's divisions conduct research on a uniquely broad front for clients around the globe.

- #### Federally Funded Research Divisions

- [RAND Army Research Division](https://www.rand.org/ard.html)
- [RAND Homeland Security Research Division](https://www.rand.org/hsrd.html)
- [RAND National Security Research Division](https://www.rand.org/nsrd.html)
- [RAND Project AIR FORCE](https://www.rand.org/paf.html)
- #### Social and Economic Policy Divisions

- [RAND Education and Labor](https://www.rand.org/education-and-labor.html)
- [RAND Health Care](https://www.rand.org/health-care.html)
- [RAND Social and Economic Well-Being](https://www.rand.org/well-being.html)
- [RAND Global and Emerging Risks](https://www.rand.org/global-and-emerging-risks.html)
- #### International

- [RAND Europe](https://www.rand.org/randeurope.html)
- [RAND Australia](https://www.rand.org/australia.html)
- [Services & Impact](https://www.rand.org/services-and-impact.html)
- [Careers](https://www.rand.org/jobs.html)
- [Graduate School](https://www.pardeerand.edu/)
- [Give](https://www.rand.org/support-us.html)
- [Cart](https://shop.rand.org/cart/)

1. [RAND](https://www.rand.org/)
2. [Research & Commentary](https://www.rand.org/pubs.html)
3. [Commentary](https://www.rand.org/pubs/commentary.html)
4. [\>What DeepSeek Really Changes About AI Competition](https://www.rand.org/pubs/commentary/2025/02/what-deepseek-really-changes-about-ai-competition.html)

## What DeepSeek Really Changes About AI Competition

 ![The DeepSeek LOGO displayed on a smartphone with Tencent Cloud displayed in the background in Suqian, Jiangsu province, China, February 3, 2025, photo by Costfoto/NurPhoto via Reuters](https://www.rand.org/content/rand/pubs/commentary/2025/02/what-deepseek-really-changes-about-ai-competition/_jcr_content/par/blogpost.crop.888x522.cm.jpeg/1738720544471.jpeg)

Photo by Costfoto/NurPhoto via Reuters

This commentary originally appeared on *[Just Security](https://www.justsecurity.org/107245/deepseek-ai-competition/)* on February 3, 2025.

## The Initial Shock

Just months ago, China seemed far behind the frontier AI advances being made in the United States. Two new models from DeepSeek have shattered that perception: Its V3 model matches GPT-4's performance while reportedly using just a fraction of the training compute. Its R1 reasoning model—akin to OpenAI's o1 introduced last September—appears to match OpenAI's o1 at a fraction of the cost per token.

Some have [suggested](https://www.thewirechina.com/2025/01/26/deepseek-and-the-strategic-limits-of-u-s-sanctions/) that DeepSeek's achievements diminish the importance of computational resources (compute). That narrative may be compelling, but it is misleading. If anything, these efficiency gains have made access to vast computing power more crucial than ever—both for advancing AI capabilities and deploying them at scale.

What DeepSeek's emergence truly changes is the landscape of model access: Their models are freely downloadable by anyone. If Chinese companies continue to develop the leading open models, the democratic world could face a critical security challenge: These widely accessible models might harbor censorship controls or deliberately planted vulnerabilities that could affect global AI infrastructure.

What DeepSeek's emergence truly changes is the landscape of model access: Their models are freely downloadable by anyone.

## A Close Look at DeepSeek's Costs

One number that shocked [analysts and the stock market](https://www.nytimes.com/2025/01/27/business/us-stock-market-deepseek-ai-sp500-nvidia.html) was that DeepSeek spent only [$5.6 million](https://arxiv.org/abs/2412.19437) to train their V3 large language model (LLM), matching GPT-4 on performance benchmarks. While this appears dramatically lower than reported estimates for GPT-4's training costs, two important caveats apply. First, the comparison is not apples-to-apples: U.S. companies have never publicly disclosed their actual training costs. When CEOs refer to staggering costs in the hundreds of millions of dollars, they likely include a more exhaustive view—hardware acquisition, staffing costs, and research expenses. In contrast, DeepSeek only reported the cost of the final training run, excluding crucial expenses like preliminary experiments, staffing, and the massive initial investment in hardware.

Second, V3's efficiency improvement is not surprising. Algorithmic advances alone typically cut training costs in half [every eight months](https://epoch.ai/blog/algorithmic-progress-in-language-models), with hardware improvements driving additional efficiency gains. Using [current](https://blog.lepton.ai/the-missing-guide-to-the-h100-gpu-market-91ebfed34516) cloud compute prices and accounting for these predictable advances, a final training run for a GPT-4–level model should cost around $3 million today. That means DeepSeek's efficiency gains are not a great leap, but align with industry trends.

The story of DeepSeek's R1 model might be different. This reasoning model—which thinks through problems step by step before answering—matches the capabilities of OpenAI's o1 released last December. Since early 2024, DeepSeek has made significant strides in reasoning, particularly excelling at [mathematical problem-solving](https://arxiv.org/abs/2402.03300). Its public release provides the first look into the details of how these reasoning models work. What is notable is that DeepSeek offers R1 at roughly [four percent](https://api-docs.deepseek.com/quick_start/pricing) the cost of o1. While such improvements are expected in AI, this could mean DeepSeek is leading on reasoning efficiency, although comparisons remain difficult because companies like Google have not released pricing for their reasoning models.

Given all this context, DeepSeek's achievements on both V3 and R1 do not represent revolutionary breakthroughs, but rather continuations of computing's long history of exponential efficiency gains—[Moore's Law](https://ourworldindata.org/moores-law) being a prime example. To be sure, direct comparisons are hard to make because while some Chinese companies openly share their advances, leading U.S. companies keep their capabilities private. Still, for those closely watching the field, DeepSeek's improvements follow expected patterns.

## Why Compute Actually Still Matters

Counterintuitively, DeepSeeks advances make compute more important, not less.

Here is why. Recreating existing capabilities requires less compute, but the same compute now enables building far more powerful models with the same compute resources (this is called [a performance effect (PDF)](https://arxiv.org/pdf/2311.15377)). When OpenAI, Google, or Anthropic apply these efficiency gains to their vast compute clusters (each with tens of thousands of advanced AI chips), they can push capabilities far beyond current limits. Indeed, if DeepSeek had had access to even more AI chips, it could have trained a more powerful AI model, made certain discoveries earlier, and served a larger user base with its existing models—which in turn would increase its revenue.

Second, new models like DeepSeek's R1 and OpenAI's o1 reveal another crucial role for compute: These “reasoning” models get [predictably better the more time they spend thinking](https://darioamodei.com/on-deepseek-and-export-controls). As AI systems take on worker-like roles, compute capacity could directly determine both how many AI workers can be deployed and how skilled each one is.

## Leading in Open Models, a Potential Security Concern

DeepSeek does highlight a new strategic challenge: What happens if China becomes the leader in providing publicly available AI models that are freely downloadable? That would not directly generate revenue for DeepSeek, but it creates soft power. More importantly, it raises serious national security concerns.

DeepSeek's downloadable model shows [fewer](https://x.com/DFinsterwalder/status/1881687398893146465) [signs](https://x.com/AvisVolans/status/1881596209724547543) of built-in censorship in contrast to its hosted models, which appear to [filter politically sensitive topics](https://www.theguardian.com/technology/2025/jan/28/chinese-ai-chatbot-deepseek-censors-itself-in-realtime-users-report) like Tiananmen Square. Most current censoring happens through additional filtering tools [after](https://x.com/dkaushik96/status/1881383386591445247) the model generates its output. However, the downloadable model still exhibits some censorship, and other Chinese models like [Qwen](https://huggingface.co/blog/leonardlin/chinese-llm-censorship-analysis) already exhibit stronger systematic censorship built into the model. As these models gain widespread adoption, the ability to subtly shape or restrict information through model design becomes a critical concern. What if such models become the foundation of educational systems worldwide?

DeepSeek does highlight a new strategic challenge: What happens if China becomes the leader in providing publicly available AI models that are freely downloadable?

Furthermore, DeepSeek presents at least two types of potential “backdoor” risks. The first is traditional security vulnerabilities, like [remote code execution](https://github.com/pytorch/pytorch/blob/main/SECURITY.md) (as [demonstrated in PyTorch incidents](https://www.oligo.security/blog/shelltorch-explained-multiple-vulnerabilities-in-pytorch-model-server)). The second, and more subtle, risk involves behaviors embedded within the model itself—what researchers call “sleeper agents.” [Research from U.S. company Anthropic](https://www.anthropic.com/research/sleeper-agents-training-deceptive-llms-that-persist-through-safety-training) shows that a model could be designed to write secure code most of the time but insert subtle vulnerabilities when used by specific organizations or in specific contexts. Once a backdoor is present in a model, it becomes extremely difficult to detect or remove—even with extensive safety testing. Traditional red-teaming often fails to catch these vulnerabilities, and attempts to train away problematic behaviors can paradoxically make models better at hiding their backdoors.

## The Path Forward

These developments force the United States to confront two distinct challenges. First, when efficiency improvements are rapidly diffusing the ability to train and access powerful models, can the United States prevent China from achieving truly transformative AI capabilities? Second, how can the United States manage the security risks if Chinese companies become the primary suppliers of open models? Policymakers should consider three priorities in response to DeepSeek:

First, [strengthen (PDF)](https://selectcommitteeontheccp.house.gov/sites/evo-subsites/selectcommitteeontheccp.house.gov/files/evo-media-document/1.29.25%20Letter%20to%20NSC%20on%20DeepSeek.pdf) rather than abandon export controls. While DeepSeek shows that determined actors can achieve impressive results with limited compute, they could go much further if they had access to the same resources of leading U.S. companies.

Second, restrict the integration of Chinese open models into critical U.S. systems and infrastructure. Just as the government tries to manage [supply chain risks in tech hardware](https://www.cisa.gov/executive-order-14017-securing-americas-supply-chains), it will need frameworks for AI models that could harbor hidden vulnerabilities. The [U.S. Framework for Artificial Intelligence Diffusion](https://www.rand.org/pubs/perspectives/PEA3776-1.html) already requires validated end users to cut ties with intelligence and military actors from untrusted countries. Under some interpretations, this requirement could extend to prohibiting the hosting of these models.

Finally, there is a critical gap in AI security research. Without better tools to detect backdoors and verify model safety, the United States is flying blind in evaluating which systems to trust. This security challenge becomes particularly acute as advanced AI emerges from regions with limited transparency, and as AI systems [play an increasing role](https://www.rand.org/pubs/commentary/2024/10/how-ai-can-automate-ai-research-and-development.html) in developing the next generation of models—potentially cascading security vulnerabilities across future AI generations.