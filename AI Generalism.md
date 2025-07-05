---
title: "AI Generalism"
source: "https://davidsj.substack.com/p/ai-generalism?publication_id=658281&post_id=160083216&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[David Jayatillake]]"
published: 2023-03-22
created: 2025-04-04
description: "!= ML Specialism"
tags:
  - "clippings"
---
### != ML Specialism

![selective focus photo of black-and-brown ball-peen hammers](https://images.unsplash.com/photo-1490557162706-284736f48784?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=M3wzMDAzMzh8MHwxfHNlYXJjaHwyfHxoYW1tZXJzfGVufDB8fHx8MTc0MzY5Mjc2MHww&ixlib=rb-4.0.3&q=80&w=1080)

Photo by [Adam Sherez](https://davidsj.substack.com/p/true) on [Unsplash](https://unsplash.com/)

One thing I’ve been seeing from people hiring is that companies are thinking about hiring or repurposing MLOps and ML engineering teams to work on Generative AI use cases.

ML engineering teams and their ML ops counterparts are highly specialised. They possess the most specialised skillsets in the field of data. These skills are dedicated to different aspects of the ML lifecycle, depending on the role. Some overlap with data engineering, although this work is often handled by data engineers directly; beyond that point, it becomes primarily specialised to ML.

Feature engineering is similar in some ways to analytics engineering but different enough that being good at one wouldn’t make you wholly competent with the other. The tooling is different, and the goals are different.

ML engineers are then responsible for building and selecting models for predictive classification and regression scenarios using the previously engineered features, often by themselves but also by others who make the features they created available centrally in a feature store. A feature store has many similarities to a semantic layer but is different enough that they are not interchangeable.

ML ops teams then look after the selected models in production by ensuring they are continually fed with high-quality data that is similar enough to training data to allow the model to perform well. They make sure that the model serving infrastructure exists and is reliable. They monitor model performance to make sure the model hasn’t degraded or data drifted, due to pipeline or demographic change.

This is a very short version of what ML teams do, but, as I said earlier, it is incredibly specialised.

Let’s take a look at AI Engineering. Is it like ML engineering? Not really… and it’s probably less like ML Engineering than Data Engineering or Analytics Engineering. There is very little overlap in the work that needs to be done in AI Engineering and ML Engineering. There aren’t parallels in tooling, such as between feature stores and semantic layers.

AI Engineering is much more similar to full stack or backend software engineering. Whereas these kinds of software engineering are often centred around a database and providing an application with interfaces around the database, AI Engineering is centred around the LLM. You make prompts instead of queries. You have MCPs and RAG instead of ORMs.

AI Engineering, when you are considering Generative AI and LLMs [^1], could be considered probabilistic software engineering, and full stack/backend could be considered deterministic software engineering. This difference between probabilistic and deterministic is the difference between AI and Software engineers. Otherwise, the activities are incredibly similar.

AI Engineers build an application around an LLM and RAG system to get the most out of the LLM, optimising its reliability, capability, and performance. Software engineers build applications around a database to provide the most functionality, optimising reliability and performance.

On this basis, I think it’s a mistake to redeploy or hire ML folks into AI roles. It’s a conflation by senior management who don’t really understand how ML or AI works. It’s a conflation caused by years of interchangeably using ML and AI in the era before generative AI. Some ML teams are probably also afraid to miss the train and put themselves forward to get involved with these projects, but honestly, I would take a full-stack software engineer to work on an AI project any day over an ML engineer [^2]. Very little of the ML lifecycle applies to Generative AI applications.

Just like software engineers don’t build databases, they buy or host existing ones; they can pay to use or host LLMs that already exist… and then build an application around them. The parallels are much stronger. No one really seriously asks an LLM for a prediction at the moment [^3]. Most of the testing and monitoring applicable to traditional ML models do not apply to Generative AI systems; the applicable testing exists in software engineering, and ML engineering has inherited it.

Testing for Generative AI systems is much closer to unit/integration/e2e testing from software engineering, except that it’s probabilistic in nature, and there is tolerance for a certain amount of failure. Generative AI systems do things; they don’t predict things. They don’t usually need extensive pipelines or feature engineering. Vectorisation and RAG are probably on the deeper end of data preparation for a Generative AI application.

This is only untrue if you are pre-training LLMs at your company, but in reality, only about 100 companies worldwide have deep enough pockets and the skillsets in-house to do this. I worry about executive teams being hoodwinked by ambitious ML teams into trying to pre-train their own LLMs. I would say that for many of the largest 100 companies in the world, pre-training LLMs is outside of their capability. So that probably means that your company shouldn’t be doing it.

There is still plenty of need for ML models to be built and served, and now perhaps more, as their outputs can additionally be used as an input for Generative AI applications. We should keep our ML teams working on ML and repurpose software engineers to work on Generative AI Applications. At any given point in time, at least 20% of software engineers are working on a feature or product of questionable value, and we know that they are. We might as well re-purpose these whole product teams to work on a Generative AI Application instead of touching our ML resources.

[^1]: There are other AI methods and research going on.

[^2]: The caveat to this, which is significant, is that many ML engineers have transitioned from backend engineering. This background makes them a strong choice, but remember that it is this skill set that proves to be the most valuable.

[^3]: However, if you reverse this and put ML model inputs into AI engineering, they could be very helpful for improving output from an LLM. This is no different to how ML model outputs can be very helpful for a traditional software application.