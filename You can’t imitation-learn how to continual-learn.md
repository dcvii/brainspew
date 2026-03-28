---
title: "You can’t imitation-learn how to continual-learn"
source: "https://www.lesswrong.com/posts/9rCTjbJpZB4KzqhiQ/you-can-t-imitation-learn-how-to-continual-learn"
author:
  - "[[By Steven Byrnes]]"
published:
created: 2026-03-27
description:
tags:
  - "brain_spew"
---
[^1]: I guess I also need to mention the “algorithmic distillation” paper ([Laskin et al. 2022](https://arxiv.org/abs/2210.14215)), but I’m hesitant to take it at face value, see discussion [here](https://www.lesswrong.com/posts/avvXAvGhhGgkJDDso/caution-when-interpreting-deepmind-s-in-context-rl-paper)

[^2]: You can replace “a forward pass” with “10,000 forward passes with chain-of-thought reasoning”; it doesn’t change anything in this post.

[^3]: Outer-loop search over learning algorithms is so expensive that it’s generally only used for adjusting a handful of legible hyperparameters, not doing open-ended search where we don’t even vaguely know what we’re looking for. Even comparatively ambitious searches over spaces of learning algorithms in the literature have a search space of e.g. [≈100 bits](https://www.lesswrong.com/posts/pz7Mxyr7Ac43tWMaC/against-evolution-as-an-analogy-for-how-humans-will-create?commentId=pYwZAgwcEhCqbWyh8), which is tiny compared to the information content of a learning algorithm source code repository.