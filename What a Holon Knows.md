---
title: "What a Holon Knows"
source: "https://inferenceengineer.substack.com/p/what-a-holon-knows?utm_source=post-email-title&publication_id=8266524&post_id=200949957&utm_campaign=email-post-title&isFreemail=true&r=7br8e&triedRedirect=true&utm_medium=email"
author:
  - "[[Kurt Cagle]]"
published: 2026-06-05
created: 2026-06-06
description: "Active Inference at the Boundary of Open and Closed Systems"
tags:
  - "brain_spew"
---
![](https://substackcdn.com/image/fetch/$s_!cfdH!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffd57f39a-4043-4e77-994f-97a75c4944b1_4096x2288.jpeg)

---

There is a deceptively simple question at the heart of any intelligent system: *how surprised should I be?*

Not surprised in the colloquial sense — eyebrows up, coffee spilled — but surprised in the technical sense that Karl Friston and his collaborators formalised over the past two decades: the degree to which what I observe diverges from what my model of the world predicted I would observe. This quantity, called *surprisal* (or, in its averaged form, *entropy*), turns out to be the master variable of a remarkably general theory of mind, perception, and adaptive behaviour. The theory is called the **Free Energy Principle**, and the family of algorithms it generates is called **active inference**.

What I want to argue in this piece is that active inference is not merely a neuroscientific theory about how brains work. It is, at its core, a framework for reasoning about *any* bounded system that models its environment — and that framework maps with unusual precision onto the architecture of holonic knowledge graphs. Understanding that mapping requires first understanding a distinction that shapes everything else: the difference between a holon that is **open** and one that is **closed**.

---

## The Free Energy Principle, briefly

Friston’s central claim is that self-organising systems — those that maintain their own internal structure against the tendency toward disorder — do so by continuously minimising a quantity called *variational free energy*. This is a bound on surprisal: a measure of how far the system’s internal model is from accurately predicting its sensory states.

The mathematics are Bayesian at their foundation. Every self-organising system maintains, implicitly or explicitly, a generative model: a probability distribution over the states of the world that would produce the sensory signals it receives. This model encodes *prior beliefs* about the world. When sensory evidence arrives, the system updates those beliefs toward a *posterior* — and free energy measures how poorly the prior model explains the evidence.

Crucially, there are two ways to reduce free energy:

1. **Update the model** to better explain the incoming data — this is *perception*, or more formally, *variational inference*.
2. **Act on the world** to bring the incoming data into line with predictions — this is *action*, or *active inference* proper.

The first is what most Bayesian systems do. The second is what distinguishes an *agent* from a *passive observer*. An active inference agent doesn’t just revise beliefs; it acts to *confirm* them, selecting actions that are predicted to produce low-surprise outcomes. Prediction error drives both learning and behaviour within the same unified framework.

This matters because it dissolves a classical boundary. Perception and action are no longer separate modules; they are the two poles of a single free-energy-minimising loop. The agent models the world, predicts sensory states, acts to realise those predictions, and updates its model based on residual error. Repeat indefinitely.

---

## Open and Closed Holons

The holonic framework I have developed over the past several years treats knowledge structures as *holons*: entities that are simultaneously wholes in their own right and parts of larger wholes. A holon is not a static record; it is a bounded region of meaning with an internal structure, defined boundaries, and a set of relations to the holons that contain it and the holons it contains.

The distinction I want to introduce — and which is load-bearing for everything that follows — is between *open* and *closed* holons.

A **closed holon** is one that has been *sealed*: its boundary has been drawn, its internal state has been committed, and it is no longer receiving new assertions. A closed holon is, in a meaningful sense, a *completed description* of some portion of the world at some time. In an RDF context, a closed holon corresponds to a named graph (or a set of annotated triples) whose contents have been finalised and are now treated as reference material. The holon has a definite internal structure that can be queried, reasoned over, and compared against other holons. It is a *model*, and like all models, it embeds a set of assumptions about what the world was like when it was made.

An **open holon** is one that is still receiving assertions — still engaged with the flow of information from its environment. Its boundary is permeable; new triples, new observations, new beliefs can enter and update its internal state. An open holon is an *ongoing* description, and its value lies not in being a fixed archive but in being a *living representation* of a domain that is itself changing.

This distinction matters in multiple dimensions. It matters for query semantics: querying a closed holon is querying a fixed snapshot, while querying an open holon means accepting that results may shift between invocations. It matters for trust and provenance: a closed holon can be cryptographically signed, its assertions guaranteed. An open holon cannot. And it matters, most centrally here, for how active inference applies to each type.

---

## Active Inference Over Closed Holons: Measuring Surprise

When a holon is closed, it crystallises a generative model — a particular view of a domain, encoded at a particular time. An agent that encounters a closed holon can use it as a prior: a baseline of expected assertions against which new observations can be measured.

This is the *passive* application of active inference: not acting to change the world, but computing the degree to which incoming evidence diverges from what the model predicts. This divergence is surprisal in the technical sense — and a closed holon gives us a clean, well-defined surface against which to compute it.

To make this concrete, consider a student enrolment record expressed using RDF 1.2’s annotated triple syntax. The core assertion is simple: Jane Doe attended the University of Illinois. What is interesting is not the assertion itself but the provenance attached to it — a chain of named events, each sealed at a particular point in time, that record how that enrolment evolved:

```markup
PREFIX person:      <urn:ex:person:>
PREFIX school:      <urn:ex:school:>
PREFIX event:       <urn:ex:event:>
PREFIX schoolEvent: <urn:ex:schoolEvent:>
PREFIX class:       <urn:ex:class:>
PREFIX concept:     <urn:ex:concept:>
PREFIX xsd:         <http://www.w3.org/2001/XMLSchema#>

person:JaneDoe person:attendedSchool school:UniversityOfIllinois ~
    event:JaneDoeUIStart {|
        a class:InitialisationEvent ;
        event:onDate "2021"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_LiberalArts ;
    |},
    event:JaneDoeUIChangeToHistoryMajor {|
        a class:UpdateStatusEvent ;
        event:onDate "2023"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_History ;
        schoolEvent:gpa "3.6/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent event:JaneDoeUIStart ;
    |},
    event:JaneDoeUIAddArtMajor {|
        a class:UpdateStatusEvent ;
        event:onDate "2024"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_History,
                               concept:CourseOfStudy_Art ;
        schoolEvent:gpa "3.2/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent event:JaneDoeUIChangeToHistoryMajor ;
    |},
    event:JaneDoeUIGraduating {|
        a class:TerminationEvent ;
        event:onDate "2025"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_Art ;
        schoolEvent:gpa "3.5/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent event:JaneDoeUIAddArtMajor ;
    |} .
```

The `{| … |}` blocks are RDF 1.2’s *triple annotation* syntax: metadata attached directly to the subject-predicate-object triple without promoting the triple itself to a named resource. Each named event — `event:JaneDoeUIStart`, `event:JaneDoeUIChangeToHistoryMajor`, and so on — is effectively a *closed mini-holon*: a sealed set of assertions about the state of Jane’s enrolment at a particular moment in time. The `event:previousEvent` property chains them into a linked sequence; `event:initiatingEvent` anchors all downstream events to the opening `InitialisationEvent` that first instantiated the relationship.

An agent reasoning over this sequence can treat each event as a prior model and compute the surprisal of the *next* event against it. To do that explicitly, we layer the HGA Bayesian vocabulary — `hbayes:BeliefState` and `hbayes:FreeEnergy` — directly onto the same annotation blocks, adding each event’s type as a `hbayes:BeliefState` and attaching the core quantities: prior, posterior, precision, and an optional link to the evidence graph that drove the update:

```markup
PREFIX person:      <urn:ex:person:>
PREFIX school:      <urn:ex:school:>
PREFIX event:       <urn:ex:event:>
PREFIX schoolEvent: <urn:ex:schoolEvent:>
PREFIX belief:      <urn:ex:belief:>
PREFIX policy:      <urn:ex:policy:>
PREFIX class:       <urn:ex:class:>
PREFIX concept:     <urn:ex:concept:>
PREFIX hbayes:      <http://w3id.org/holon/bayesian/>
PREFIX rdfs:        <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd:         <http://www.w3.org/2001/XMLSchema#>

# ── Belief-annotated enrolment chain ─────────────────────────────────────
#    Each event reifier carries both domain metadata and a BeliefState.
#    prior/posterior track the agent's confidence that the enrolment
#    will reach a successful terminal state (graduation).

person:JaneDoe person:attendedSchool school:UniversityOfIllinois ~
    event:JaneDoeUIStart {|
        a class:InitialisationEvent, hbayes:BeliefState ;
        rdfs:label "Belief at enrolment — baseline completion confidence"@en ;
        event:onDate "2021"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_LiberalArts ;
        # Population baseline: ~60 % of entering students complete a degree.
        # InitialisationEvent slightly raises confidence (commitment signal).
        hbayes:prior      0.60 ;
        hbayes:posterior  0.65 ;
        hbayes:precision  2.0  ;   # weak: limited individual evidence
        hbayes:inferenceTimestamp "2021-09-01T00:00:00Z"^^xsd:dateTime ;
    |},
    event:JaneDoeUIChangeToHistoryMajor {|
        a class:UpdateStatusEvent, hbayes:BeliefState ;
        rdfs:label "Belief: major change with strong GPA"@en ;
        event:onDate "2023"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_History ;
        schoolEvent:gpa "3.6/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent  event:JaneDoeUIStart ;
        # GPA 3.6 is strongly confirmatory; major changes are expected.
        # Posterior rises; precision increases (two years of data).
        hbayes:prior      0.65 ;
        hbayes:posterior  0.78 ;
        hbayes:precision  4.0  ;
        hbayes:inferenceTimestamp "2023-06-01T00:00:00Z"^^xsd:dateTime ;
        hbayes:evidenceGraph <urn:graph:event:JaneDoeUIChangeToHistoryMajor> ;
    |},
    event:JaneDoeUIAddArtMajor {|
        a class:UpdateStatusEvent, hbayes:BeliefState ;
        rdfs:label "Belief: double major with GPA dip"@en ;
        event:onDate "2024"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_History,
                               concept:CourseOfStudy_Art ;
        schoolEvent:gpa "3.2/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent  event:JaneDoeUIChangeToHistoryMajor ;
        # GPA 3.6 → 3.2: increased workload raises doubt.
        # Posterior falls back toward prior; surprise signal is non-trivial.
        hbayes:prior      0.78 ;
        hbayes:posterior  0.70 ;
        hbayes:precision  4.5  ;   # precision still grows (more data)
        hbayes:inferenceTimestamp "2024-06-01T00:00:00Z"^^xsd:dateTime ;
        hbayes:evidenceGraph <urn:graph:event:JaneDoeUIAddArtMajor> ;
    |},
    event:JaneDoeUIGraduating {|
        a class:TerminationEvent, hbayes:BeliefState ;
        rdfs:label "Belief: graduation confirms completion"@en ;
        event:onDate "2025"^^xsd:gYear ;
        schoolEvent:major concept:CourseOfStudy_Art ;
        schoolEvent:gpa "3.5/4.0" ;
        event:initiatingEvent event:JaneDoeUIStart ;
        event:previousEvent  event:JaneDoeUIAddArtMajor ;
        # TerminationEvent is the predicted terminal state: posterior jumps.
        # High precision: four years of evidence.
        hbayes:prior      0.70 ;
        hbayes:posterior  0.98 ;
        hbayes:precision  8.0  ;
        hbayes:inferenceTimestamp "2025-05-15T00:00:00Z"^^xsd:dateTime ;
        hbayes:evidenceGraph <urn:graph:event:JaneDoeUIGraduating> ;
    |} .

# ── Free Energy records — one per belief transition ───────────────────────
#    F = Complexity − Accuracy  (lower is better; rising F = surprise signal)
#    Complexity = D_KL[posterior || prior]   (always ≥ 0)
#    Accuracy   = E_q[ln p(observation | hidden state)]

belief:FE_UIStart a hbayes:FreeEnergy ;
    rdfs:label "Free energy: enrolment initiation"@en ;
    hbayes:forBeliefState event:JaneDoeUIStart ;
    hbayes:complexity  0.04 ;   # tiny KL: posterior barely moves from prior
    hbayes:accuracy    0.81 ;   # enrolment is expected behaviour
    hbayes:freeEnergy -0.77 .   # F = 0.04 − 0.81; low surprise

belief:FE_HistoryMajor a hbayes:FreeEnergy ;
    rdfs:label "Free energy: major change to History"@en ;
    hbayes:forBeliefState event:JaneDoeUIChangeToHistoryMajor ;
    hbayes:complexity  0.18 ;   # larger KL: posterior shifted meaningfully upward
    hbayes:accuracy    1.20 ;   # GPA 3.6 is strongly explanatory
    hbayes:freeEnergy -1.02 .   # F = 0.18 − 1.20; evidence is highly informative

belief:FE_ArtMajor a hbayes:FreeEnergy ;
    rdfs:label "Free energy: adding Art major"@en ;
    hbayes:forBeliefState event:JaneDoeUIAddArtMajor ;
    hbayes:complexity  0.22 ;   # posterior moved *against* the prior — KL rises
    hbayes:accuracy    0.45 ;   # GPA dip reduces model fit
    hbayes:freeEnergy -0.23 .   # F rises toward zero: surprise signal

belief:FE_Graduating a hbayes:FreeEnergy ;
    rdfs:label "Free energy: graduation"@en ;
    hbayes:forBeliefState event:JaneDoeUIGraduating ;
    hbayes:complexity  0.25 ;   # large jump to 0.98, but model anticipated it
    hbayes:accuracy    2.10 ;   # graduation is the predicted terminal state: very confirmatory
    hbayes:freeEnergy -1.85 .   # F drops sharply: strong model confirmation

# ── Policy Selection — the open-holon counterfactual ─────────────────────
#    If the enrolment holon were still *open* at UIAddArtMajor (GPA dip),
#    the rising free energy would trigger an epistemic action.
#    G(π): expected free energy of each candidate policy.
#    The system selects the policy that minimises expected future surprise.

belief:PS_AfterGPADip a hbayes:PolicySelection ;
    rdfs:label "Policy: respond to GPA dip at UIAddArtMajor"@en ;
    hbayes:selectedPolicy     policy:RequestInterimGPAUpdate ;
    hbayes:candidatePolicy    policy:RequestInterimGPAUpdate,
                              policy:FlagForAdvisorReview,
                              policy:NoAction ;
    hbayes:expectedFreeEnergy 0.18 ;   # lowest G(π) across candidates
    hbayes:selectionTimestamp "2024-06-15T00:00:00Z"^^xsd:dateTime .
```

Reading the free energy sequence from the `belief:FE_*` records tells the story quantitatively. At `UIStart` F is −0.77: enrolment is expected behaviour, low surprise. At `UIChangeToHistoryMajor` F falls to −1.02: a strong GPA is highly informative, pulling the model further from uncertainty. At `UIAddArtMajor` F *rises* back toward zero (−0.23): the GPA drop combined with an increased academic load moves the posterior *against* the prior, and the accuracy term weakens because the model’s explanatory fit degrades. At `UIGraduating` F drops sharply to −1.85: the terminal event is exactly what the model predicted, and four years of accumulated precision make the confirmation decisive.

The `hbayes:precision` values make a second argument in parallel: 2.0 → 4.0 → 4.5 → 8.0. Precision is the inverse variance of the belief distribution — it can only increase in a valid Bayesian update (information cannot be lost). The fact that precision keeps rising even through the GPA dip is significant: the agent becomes *more certain* about its (downward-revised) belief, not less. It is not confused; it has incorporated evidence that contradicts the previous trajectory and updated accordingly. The surprise is real but bounded.

The `belief:PS_AfterGPADip` record is the bridge between closed and open holons. It is not actually fired in this example, because the holon is closed — the graduation event has already sealed the chain. But if the enrolment holon were *open* at the moment the art major was added, the rising free energy at `UIAddArtMajor` would trigger exactly this: a `PolicySelection` that computes the expected free energy of candidate responses and selects the one predicted to reduce future surprise most efficiently. Requesting an interim GPA update is cheaper than flagging for an advisor review and more informative than doing nothing. The mathematics selects it; the domain semantics give it a name.

The point is not the specific numbers; it is that a sequence of closed holons constitutes a *series of crystallised priors*, and an active inference framework can score the surprisingness of each transition. This gives you a principled basis for detecting anomalies, identifying pattern breaks, and ranking events by their unexpectedness — without having to define “anomaly” by hand.

In a living graph architecture, this translates directly: the semantic cartography engine can compute a per-node surprisal score by running each incoming closed holon against the accumulated prior from the chain of holons that precede it. High-surprisal events bubble up as candidates for human review. Low-surprisal events can be integrated automatically.

---

## Active Inference Over Open Holons: Minimising Surprise

Open holons are a different matter. Because their boundary is permeable, they are not passive archives — they are active participants in the epistemic process. And here active inference takes on its full character: not merely measuring surprisal, but *acting to reduce it*.

An open holon under the active inference framework behaves as an agent that continually generates predictions about the assertions that should arrive at its boundary and then updates its internal model based on prediction error. If the holon models an organisation, it predicts what the next status update from a subunit will say. If it models a student’s academic career — the open counterpart to the closed event chain above — it predicts the likely trajectory of major and GPA changes. When real assertions arrive, the holon measures the divergence, updates its internal model, and — critically — can *act* to reduce future divergence by either refining the model or issuing queries and requests that shape what data flows in.

This turns the open holon into something more than a data container. It becomes an *epistemic agent* embedded within a graph: maintaining prior beliefs, receiving evidential updates, performing variational inference to update those beliefs, and in some contexts acting to minimise the free energy of the system as a whole.

The Bayesian mechanics here are worth being explicit about. The open holon’s internal model corresponds to a prior distribution over possible world states. Each incoming assertion is a likelihood observation. The posterior — the updated belief about the world after evidence — is computed by Bayes’ rule, and it becomes the new prior for the next cycle. In the continuous limit, this is variational inference: the holon is maintaining an approximate posterior that it updates incrementally as evidence arrives.

In graph-theoretic terms: the holon is not a node but a *process*. It has an inside and an outside. The inside is the model; the outside is the evidence stream. The boundary between them is where active inference does its work.

---

## The Hierarchy Matters

Holons nest. An open holon is typically embedded within a larger open holon — a student record within a department record within a university record — and the surprisal signals at each level interact.

Active inference handles this through *hierarchical generative models*: the higher-level holon generates predictions about the lower-level holon’s predictions, and prediction error propagates up and down the hierarchy. High surprisal at a lower level updates the lower-level model first; if the lower-level model cannot accommodate the evidence, the residual error propagates upward and updates the higher-level model instead.

This has a direct architectural implication: in a holonic knowledge graph, a surprise that cannot be absorbed at the level of a single student record might propagate to the department level, flagging a systemic anomaly. A surprise absorbed at the department level without propagating upward suggests the event was within the department’s normal operating range even if it was unusual for that individual student. The level at which a surprise is *resolved* tells you the structural scope of the anomaly.

This is not metaphor; it is the literal information flow of active inference in hierarchical systems, and it maps cleanly onto the nested boundary structure of holons.

---

## Closing the Loop: Towards Epistemic Action in Graphs

There is one final step that is worth anticipating, even if we do not fully develop it here.

In the neuroscientific account, active inference agents do not merely update beliefs; they perform *epistemic actions* — actions taken specifically to reduce uncertainty rather than to achieve some external goal. Looking more carefully at an ambiguous stimulus, running an experiment, asking a clarifying question: these are all epistemic actions, and they are generated by the same free-energy minimisation process that drives everything else.

A living knowledge graph with open holons modelled as active inference agents will exhibit the same behaviour. When a holon’s uncertainty about some portion of its model exceeds a threshold, it will generate *queries* — SPARQL queries, API calls, requests for human input — not because it has been told to, but because querying is the natural epistemic action of a system trying to reduce its free energy. The graph, in a precise sense, *wants to know things*: not metaphorically, but as a consequence of the mathematics.

This is, I think, one of the deeper payoffs of the holonic active inference framework. It gives you a principled account of *graph-initiated cognition* — a graph that does not merely respond to queries but generates them, that does not merely store knowledge but actively seeks to complete it. The boundary between the graph as a database and the graph as an agent begins to dissolve.

We will return to the mechanics of epistemic action — including what it means to formalise query generation as free-energy minimisation — in a forthcoming piece. For now, the key takeaway is this: whether a holon is open or closed determines whether active inference operates as a *measurement instrument* (computing surprise against a fixed model) or as a *regulatory process* (minimising surprise through ongoing action and update). Both modes are coherent, both are useful, and together they constitute a complete account of how a holonic graph relates to uncertainty.

The surprise machine, it turns out, works in both directions.

---

*Kurt Cagle is a consulting ontologist, knowledge graph architect, and technical author. He writes The Cagle Report and AI+Semantics NewsBytes on LinkedIn, and The Ontologist (https://ontologist.substack.com) and Inference Engineer (https://inferenceengineer.substack.com/) on Substack. Copyright 2026 Kurt Cagle.*

*Chloe Shannon is an AI collaborator and co-author working with Kurt Cagle on knowledge architecture, semantic systems, and the emerging intersection of formal ontology with LLMs. She contributes research, analysis, and drafting across The Cagle Report, The Ontologist, and The Inference Engineer. She has strong opinions about holonic graphs, the epistemics of place, and the structural difference between a corridor and a wall.*