---
title: User story example
source: https://chatgpt.com/share/68d98862-ed64-800d-97b1-e3a0e30862f9
author:
  - "[[FRMS Conversion]]"
published:
created: 2025-09-29
description: ChatGPT helps you get answers, find inspiration and be more productive. It is free to use and easy to try. Just ask and ChatGPT can help with writing, learning, brainstorming and more.
tags:
  - clippings
---
Uploaded a file

Give me an example user story of the sort of interactions that the authors are proposing.

---

Here’s an example user story that illustrates the kind of interaction the authors of *Interactive Recommendation Agent with Active User Commands* (Tang et al., 2025) are proposing:

---

### Scenario: Shopping for Clothes in an E-Commerce Feed

- **Round 0 (Initial Feed):**  
	The user opens a shopping app and sees a set of recommended short skirts.
	**User Command:**  
	*“How come these are all short skirts? It’s autumn now, I’d like to see long skirts.”*
	→ The Parser agent converts this into a structured preference: *positive = long skirts; negative = short skirts.*  
	→ The Planner agent filters the candidate pool and adjusts the scoring so long skirts rise to the top.

---

- **Round 1 (Updated Feed):**  
	The system now displays mostly long skirts.
	**User Command:**  
	*“Are there any in light blue?”*
	→ Parser updates preferences (positive = light blue, long skirts).  
	→ Planner integrates the new color preference into its tool chain.

---

- **Round 2 (Refinement):**  
	The user now sees several long skirts, some light blue, some not.
	**User Command:**  
	*“Just around 200.”* (budget constraint)
	→ Parser adds a *hard constraint*: price ≈ 200.  
	→ Planner filters out items above this threshold.

---

- **Round 3 (Negative Feedback):**  
	The system shows budget-friendly long skirts, including floral designs.
	**User Command:**  
	*“Don’t want any floral dresses.”*
	→ Parser sets a *negative preference* for floral patterns.  
	→ Planner attenuates scores of floral items.

---

- **Round 4 (Convergence):**  
	The system presents a long, light blue dress around the desired budget, not floral.
	**User Feedback:**  
	*“Perfect, I love this long dress!”*
	→ Interaction ends with user satisfaction.

---

This step-by-step interaction (shown in *Figure 8 on page 14* of the paper) demonstrates how the **Interactive Recommendation Feed (IRF)** and **RecBot** framework let users iteratively refine results through free-form natural language commands. Instead of being limited to likes/dislikes, the user can actively steer recommendations by articulating preferences, constraints, and negative feedback, with the system dynamically adapting in real time.

Would you like me to also create a **short “scripted dialogue” version** (like a chat transcript) that could be reused directly as an example in a product design context?