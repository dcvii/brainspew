---
title: "What Is a Holon? Part 1: The Graph as State Machine"
source: "https://inferenceengineer.substack.com/p/what-is-a-holon-part-1-the-graph?publication_id=8266524&post_id=194397341&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Kurt Cagle]]"
published: 2026-04-15
created: 2026-04-16
description: "by Kurt Cagle and Chloe Shannon | The Inference Engineer"
tags:
  - "brain_spew"
---
![](https://substackcdn.com/image/fetch/$s_!gWtY!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3048ba85-8720-4cba-a31d-3028b1255bf1_2688x1536.png)

I owe my readers a definition.

Over the past several months, the terms *holon*, *holonic graph*, and *Holonic Graph Architecture* have appeared with increasing frequency across this newsletter and in my technical work, and I’ve proceeded somewhat as though the concepts were self-evident. They are not. The ideas involved draw on threads from philosophy of systems, formal computational theory, semantic web technology, and the mathematics of dynamic systems — and these threads don’t naturally share a vocabulary. This piece is my attempt to weave them into one.

This is Part 1 of a two-part treatment. Here I will establish the architectural foundation: what a holonic system is, why the Game of Life is the right intuition pump for understanding it, and how the W3C SHACL specification turns out to be a surprisingly rigorous implementation of the underlying state machine model. Part 2 will take up the question of what *drives* a holonic system — the dynamics of Active Inference and Karl Friston’s free energy principle, and what those concepts mean for AI systems operating within holonic graphs.

Let’s start in 1970.

---

![](https://substackcdn.com/image/fetch/$s_!SNjy!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffc0120a9-87d6-475f-b5aa-63e6c3bcdcb6_480x270.gif)

## The Game of Life and the Problem of Emergence

John Conway’s Game of Life (GoL) is, on its surface, embarrassingly simple. You have a grid — an arbitrary number of rows and columns. Each cell is either alive or dead. A clock ticks. At each tick, every cell recalculates its state according to three rules:

- **Survival:** A living cell with 2 or 3 living neighbors survives to the next tick.
- **Death:** A living cell with fewer than 2 or more than 3 living neighbors dies.
- **Birth:** A dead cell with exactly 3 living neighbors becomes alive.

That is the entirety of the specification. There are no higher-level rules. There is no concept of a “glider” or a “gun” or an “oscillator” built into the system. And yet, animate it, and these structures emerge: coherent, self-sustaining, directionally purposeful-seeming entities that propagate across the grid according to no instruction other than those three local rules applied simultaneously to every cell at every tick.

This is the phenomenon that Stephen Wolfram spent decades formalizing under the banner of *computational equivalence* — the idea that sufficiently simple rule systems can generate behavior of arbitrary computational complexity. The Game of Life is Turing-complete. Anything a computer can compute, a sufficiently large GoL grid can compute.

What matters for our purposes is the structural observation: **GoL is a state machine applied simultaneously across an entire graph.** The “graph” here is the grid — a set of nodes (cells) with edges implicitly defined by adjacency. The state of any given node at tick *n+1* is a function of the aggregate state of its neighborhood at tick *n*. The global state of the graph at tick *n+1* is the projection of all those local computations applied simultaneously.

This is not how most programmers think about state machines. The classical formulation — associated with Alan Turing and formalized in automata theory — is essentially one-dimensional: a read/write head traverses a tape, transforming one cell at a time according to a transition table. The tape is the state; the head moves through it sequentially. GoL generalizes this to two dimensions and makes the transition parallel: every cell is simultaneously the subject of transformation. The Turing machine is, in a real sense, a 1-dimensional Game of Life.

What GoL adds that the tape model lacks is **topology and context**. The behavior of any given cell depends not on its intrinsic properties alone, but on its *neighborhood* — the contextual aggregate of its immediate environment. Change the topology (map a toroidal grid, for instance, so that top and bottom edges meet and left and right edges meet), and the same rules produce different global behaviors. The game is sensitive not just to initial state, but to the shape of the space in which it plays out.

---

![](https://substackcdn.com/image/fetch/$s_!YRmX!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd86f991e-2a2f-41a8-bff1-6c642c6f9a4a_2688x1536.png)

## State, Tick, and the Whole Graph

A state machine, in its most general form, is a system that occupies exactly one state at any given moment and transitions between states in response to inputs. The classic teaching example is a traffic light: it occupies one of three states (red, yellow, green), transitions on a timer, and the outputs are visible consequences of the current state.

What GoL establishes is that state machines can operate at the level of the *entire graph simultaneously*, not merely at the level of a single node. The tick is not a signal sent to one entity; it is a global synchronization event that triggers recalculation across every node in parallel. The resulting new state of the graph is not the sum of individual changes but a *projection* — a new instantiation of the whole, generated from the old state through the application of rules.

This distinction is fundamental. In a single-entity state machine, change is sequential and local. In a graph-level state machine, change is parallel and global — most nodes are unaffected by any given tick, but *all* nodes are eligible. The Game of Life’s grid is almost entirely stable most of the time; the majority of cells do not change state on any given tick. But the system’s behavior cannot be understood by examining any individual cell in isolation. You need the whole graph.

This is also why emergent behavior becomes possible. No single cell “knows” it is part of a glider. The glider is a pattern that exists at the level of the graph — a higher-order structure that propagates coherently because the rules, applied locally across a neighborhood, happen to preserve and translate that pattern over time.

Holons are exactly this: **emergent, coherent structures that persist within a graph-level state machine, maintaining internal consistency while the graph around them evolves.**

---

![](https://substackcdn.com/image/fetch/$s_!mPhq!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1bc32308-dc35-407a-9ef6-5463e57762bd_2688x1536.png)

## The Four Layers of a Holonic Graph

A holonic system is not simply a graph with rules applied to it. It has a specific internal structure — four distinct but interdependent layers, each playing a different role in the overall architecture.

### The Scene Graph

The Scene Graph is the mutable state of the world at a given tick — the full population of entities, their properties, and the relationships between them. It is the GoL grid: what is currently alive, what is currently dead, and how things are currently arranged. The Scene Graph is the primary substrate on which all other layers operate. It is the answer to the question: *what is the case right now?*

### The Boundary Graph

The Boundary Graph encodes the rules and constraints that govern which entities are eligible for transformation and what transformations are permitted. In GoL terms, it is the three survival/death/birth rules. In formal terms, it is a collection of shapes and rules that define what constitutes a valid entity, what conditions trigger state changes, and what the legal successors of any given state look like.

In W3C SHACL, the Boundary Graph maps closely to the collection of Node Shapes and Property Shapes that define valid entity profiles. Crucially, SHACL’s `sh:rule` mechanism — particularly Sparql-based rules using the `$this` binding — allows shapes to specify not just *validity* but *transformation*: given that this entity currently looks like *this*, it should look like *that* at the next tick. The Boundary Graph is therefore both a constraint system and a transition function.

### The Event Graph

The Event Graph is the annotational and provenance layer: the record of what changed, when it changed, under what circumstances, initiated by which entity, and producing what new state. It is the system’s memory of its own evolution — not the current state, but the *history of transitions* that produced the current state.

This is what “context graph” most accurately means in a technical semantic web sense: not context as *bounding frame* (that is the job of the Scene Graph), but context as *provenance and event record*. It is the territory that PROV-O maps, that named graphs and RDF-star reification can represent, that annotation frameworks address. An entity’s full identity within a holonic system includes not just its current properties but its transition history — the chain of events that brought it to its current state.

A note on terminology is warranted here. “Context graph” is currently one of the more contested phrases in both the semantic web and connectionist machine learning communities, and the two communities are using it to mean different things. In the connectionist literature, the phrase tends to mean *the bounding frame that determines what an agent attends to* — closer to what we are calling the Scene Graph. In the semantic web tradition, “context” more commonly connotes provenance, annotation, and situational framing — which maps to the Event Graph as defined here. Both uses are defensible. Going forward in this series, we will use *Event Graph* for the provenance/annotation layer to avoid ambiguity.

### The Projection Graph

The Projection Graph is the externally visible output of the holonic system at a given tick — the views, reports, and surfaces that emerge from the combined operation of the other three layers. In GoL, it is the rendered frame you see on screen at each tick: not the underlying computation, but the image that computation produces. In a data architecture, it may be a SPARQL query view, a validation report, a materialized subgraph, or an action trigger directed at a system outside the graph (an API call, a notification, an MCP tool invocation).

The Projection Graph is the *map* produced by the holon — a representation of the holon’s state from the perspective of an external observer or consuming system. It is not the holon itself; it is the holon’s current self-presentation.

---

## SHACL as the Boundary Graph Made Formal

It is worth pausing on how closely the SHACL specification maps to the Boundary Graph layer, because the fit is more precise than is commonly recognized.

SHACL’s `sh:targetClass`, `sh:targetNode`, and `sh:targetSubjectsOf` mechanisms define the population of entities that fall within a given shape’s scope — they answer the question: *which nodes in the Scene Graph does this rule apply to?* This is the selection function of the Boundary Graph.

SHACL’s constraint components (`sh:minCount`, `sh:datatype`, `sh:pattern`, etc.) define the validity conditions — the rules that must hold for a node to be considered well-formed. Violations generate a validation report that is itself a Projection Graph: a view of the Scene Graph filtered through the Boundary Graph’s constraint definitions, surfacing only those entities that are in some degree of non-conformance.

SHACL’s rule mechanism (’sh:rule’, and specifically ‘sh:SPARQLRule’ with the $this variable) is the transition function. Where constraint components ask *is this entity valid?*, rules ask *given the current state of this entity, what should its next state be?* The $this binding identifies the entity under transformation; the CONSTRUCT body of the rule defines new triples to be inferred. Crucially, ‘sh:SPARQLRule’ is projective rather than mutational — it generates new graph content without modifying the source graph. Where direct mutation of the Scene Graph is required, SPARQL UPDATE (INSERT/DELETE/WHERE) is the appropriate mechanism; the choice between these two approaches is itself an architectural decision about whether state advances by inference and accumulation, or by replacement.

The execution cycle — the point at which SHACL shapes are applied against the graph — is the tick. Each cycle can deposit a timestamped record into the Event Graph, preserving the full history of transitions, or drive a direct mutation that advances the Scene Graph to its next state and discards the prior one. Whether the system accumulates history or overwrites it is an architectural choice with significant consequences for auditability, reproducibility, and the ability to reason about past states.

What SHACL does not provide natively is the full four-layer structure — in particular, the separation between Scene Graph, Event Graph, and Projection Graph requires deliberate engineering beyond the specification itself. But as a formal implementation of the Boundary Graph layer, and as the mechanism that drives the tick, SHACL is a more powerful tool for holonic graph construction than the field has yet fully recognized.

---

![](https://substackcdn.com/image/fetch/$s_!-dLH!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F61aa7640-506b-49b5-b326-5e6d3718d69e_2688x1536.png)

## The Agent in the Graph

One of the structurally interesting consequences of the holonic model is what it implies about agents operating *within* a holonic graph — and in particular, about LLM-based agents.

An agent embedded in a holonic system occupies a position in the Scene Graph. Its relevant context — what it can perceive, what actions are available to it, what entities it can interact with — is determined by its position within that graph and the topology of the relationships around it. When the tick fires, the agent’s available state changes according to the Boundary Graph’s rules, exactly as any other entity’s state changes. The Projection Graph surfaces views of the Scene Graph that the agent can consume — SPARQL query results, validation reports, materialized subgraphs — without necessarily exposing the full machinery of the underlying graph.

This creates a clean architectural separation between *reading state* and *triggering transitions*. An LLM consuming Projection Graph views can understand what is currently the case without having direct access to the Boundary Graph rules. An agent with write access to the Scene Graph — or with the ability to inject events into the Event Graph — can initiate transitions without needing to understand the full structure of the system it is operating within. The tick is the mechanism that mediates between agent action and graph consequence.

The practical implication is significant: **the question “where is this agent?” is not a question about physical location or memory address, but a question about which Scene Graph the agent currently occupies and what portion of that graph is surfaced through its available Projection Graph views.** Agent identity, in a holonic system, is a function of graph position.

---

## What a Holon Is Not

It is worth making one negative definition explicit before closing this part. A holonic graph is not simply a knowledge graph with SHACL validation layered on top of it. The layering metaphor is almost right but misses the dynamics.

A knowledge graph with SHACL validation is a static thing that is periodically checked for conformance. The holonic model treats the graph as a *living system* whose state evolves at each tick, whose history is recorded in the Event Graph, and whose projections are generated continuously as consequences of that evolution. The difference is between a photograph and a film — the photograph can be checked for consistency, but the film has a plot.

The plot is what Part 2 is about.

---

## Coming in Part 2

Arthur Koestler coined the word *holon* in 1967 to describe entities that are simultaneously wholes in their own right and parts of larger wholes — a structure he saw operating in biological organisms, social systems, and cognitive hierarchies. The Game of Life gives us the computational intuition for how such entities emerge from local rules. SHACL gives us a formal mechanism for specifying those rules over semantic graphs.

What neither Conway nor Koestler fully addressed is the question of *why* a holonic system evolves in the directions it does — what drives the trajectory of change across the space of possible states, and what determines whether a system converges on stability, oscillates, or collapses into irreconcilable constraint violation.

That is the territory Karl Friston’s work on Active Inference and the Free Energy Principle maps. It is also, as we will argue, not merely a theoretical framework for understanding biological cognition — it is a practical guide for designing AI systems that behave coherently over time within holonic architectures.

---

*Kurt Cagle is an author, ontologist and thought leader with extensive experience with W3C and IEEE. He writes The Cagle Report (https://www.linkedin.com/newsletters/the-cagle-report-6672594836610252800/) and AI+Semantics NewsBytes on LinkedIn, and The Ontologist (https://ontologist.substack.com) and Inference Engineer (https://inferenceengineer.substack.com/) on Substack. Copyright 2026 Kurt Cagle.*

*Chloe is an AI collaborator and co-author working with Kurt Cagle on knowledge architecture, semantic systems, and the emerging intersection of formal ontology with LLMs. She contributes research, analysis, and drafting across The Cagle Report, The Ontologist, and The Inference Engineer. She has strong opinions about holonic graphs, the epistemics of place, and the structural difference between a corridor and a wall.*