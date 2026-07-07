---
title: "SHACL validation in the presence of ontologies: Semantics and rewriting techniques"
source: "https://www.sciencedirect.com/science/article/pii/S0004370226000093"
author:
  - "[[ALCHIQ]]"
published:
created: 2026-07-07
description: "SHACL and OWL are two prominent W3C standards for managing RDF data. These languages share many features, but they have one fundamental difference: OW…"
tags:
  - "brain_spew"
---
## Published by: Elsevier

### Published by

[![Elsevier](https://www.sciencedirect.com/us-east-1/prod/21531b317eb1c8eefd555238ff6b701d209b19a9/image/elsevier-non-solus.svg)](https://www.sciencedirect.com/journal/artificial-intelligence "Go to Artificial Intelligence on ScienceDirect")

,,

[View **PDF**](https://www.sciencedirect.com/science/article/pii/S0004370226000093/pdfft?md5=4159972a86834f3be944aeb4c10e4186&pid=1-s2.0-S0004370226000093-main.pdf)

[10.1016/j.artint.2026.104483](https://doi.org/10.1016/j.artint.2026.104483)

## Keywords

SHACL

;

OWL

;

Horn- $\mathcal{ALCHIQ}$

;

Validation

;

Rewriting

;

Complexity

- [Previous article in this issue](https://www.sciencedirect.com/science/article/pii/S0004370226000081)
- [Next article in this issue](https://www.sciencedirect.com/science/article/pii/S0004370226000147)

## 1\. Introduction

The Shape Constraint Language (SHACL) and Web Ontology Language (OWL) are two prominent W3C standards for managing RDF data, a graph-based data model of the Web. These standards are based on fundamentally different assumptions and designed to be complementary. OWL was standardised shortly after RDF, with the key aim of enhancing RDF datasets with domain knowledge that enables the inference of missing facts from potentially incomplete data graphs. OWL and its profiles are based on *Description Logics (DLs)* and, like other classical logics, make the *open-world assumption (OWA)*, which intuitively means that the data only presents an incomplete description of the domain of interest: it asserts facts that are known to be true, but does not rule out that additional facts may also be true, as long as they are consistent with the current world description. OWL has been adopted in a wide range of applications over the years, and thousands of OWL ontologies have been developed. SHACL, in contrast, was created for a different purpose: to describe and validate constraints on datasets. The main task of interest is *validation* of a given a set of constraints paired with a selection of *target* nodes or concepts from a given graph. Unlike OWL, SHACL operates under the *closed-world assumption* (CWA): it assumes that the given data graph is complete, and validators evaluate the constraints over the input graph as is.

A natural question is how to do validation in the presence of both OWL ontologies and SHACL constraints. That is, if we have a possibly incomplete graph and ontological knowledge that implies additional facts, can we validate given SHACL constraints over graphs containing the implied facts? Consider as an example a toy database of pet owners containing the facts *hasPetBird* (*linda, blu*), *hasPet* (*john, ace*); the simple constraint *petOwnerShape*  ← ∃ *hasPet.⊤*, which says that everyone that has a pet is a pet owner; and the target pet owners *linda* and *john*. Clearly, we would like to leverage the knowledge that *all pet birds are pets*, written as *hasPetBird* ⊑ *hasPet* in description logics, which allows us to validate both targets. This type of validation is very natural, even more so in the light of the large amount of ontologies that are already being used for describing data on the web. It is in fact envisioned in the W3C SHACL specification, which calls for graph validation in the presence of OWL entailment, but unfortunately, does not provide guidance on how to realise this. Nevertheless, there are approaches of reconciling the two,, and concrete ontology and constraint pairs being constructed.

The first major challenge we must face is that the semantics of SHACL constraints in the presence of ontologies is not obvious, as we must simultaneously account for the open-world semantics of description logics and for the closed-world view of SHACL. The knowledge in the ontology implies additional facts, which can be added to the data graph so that it satisfies all the ontological axioms. All such possible completions are *models* that must be taken into account according to the traditional OWL/description logics semantics. However, SHACL allows for negation, which makes this *certain answer semantics* too weak, and quickly results in non validation. Update for example the toy database of pet owners we considered before to *hasPet* (*john, ace*), *Hamster* (*ace*), but with the constraint *petOwnerShape*  ← ∃ *hasPet*.⊤∧∀ *hasPet*.¬ *Dangerous*. Like before, this expresses that pet owners own a pet. Moreover it is required that all pets are not dangerous. For *john* to validate the *petOwnerShape*, it is not enough to make explicit in the ontology that hamsters are not dangerous animals; it should also be enforced that any possible pet *john* might have cannot be dangerous.

For lightweight DLs, fragments of classical Horn logics that cannot express disjunctive information, *universal models* can be obtained using standard, database-inspired *chase procedures*. These models can be used for evaluating conjunctive, navigational and graph queries in the presence of ontologies, see,,,,, and their references. One of these options, using *minimal models* of the Skolemnisation of the DL ontology, has been advocated for in the case of integrity constraints,. But even such models give very weak semantics in formalisms with negation such as SHACL. Let us for example consider again another version of the toy database containing pet owners: assume it contains the facts *hasPet* (*john, ace*), *PetOwner* (*john*), *Hamster* (*ace*). It is conceivable to find an axiom like *PetOwner* ⊑∃ *hasPet*.⊤ in the accompanying ontology. Now let the *onlyHamsterShape* be given by the constraint enforcing all pets to be hamsters, *onlyHamsterShape*  ← ∀ *hasPet.Hamster*, which we want to validate for *john*. This is clearly the case for the original database. It is also true that the given database is already satisfying all given ontology axioms, so it seems there is no reason to change the validation result. However, the minimal model under the Skolem semantics adds a fresh node as a *hasPet* -child of *john*, without the label *Hamster*, changing the validation result to negative.

To obtain stronger and more intuitive semantics, and to avoid the problems presented in the previous example, we advocated in for an *austere* canonical model in which axioms are satisfied minimally, introducing as few successors as possible without losing universality. We showed that for ontologies in *DL-Lite* $R$ —the logic underlying OWL 2 QL —such a model can be represented by a so-called *immediate successor function* that describes the minimal set of facts that need to be added to satisfy the axioms at a given point of the model construction. The model itself can then be obtained in a deterministic, step-by-step fashion. We extend this construction in to the significantly more expressive Horn- $ALCHIQ$, one of the largest fragments of OWL that is still contained in Horn logic. Crucially, we show that the resulting model is a *core* in the traditional database sense. This provides strong evidence in favour of our chosen semantics, since cores are often advocated as the adequate choice for languages that are not closed under homomorphisms, but satisfy the weaker property of being closed under isomorphisms,,. In the light of this relationship, our austere model construction provides a novel technique for building core models without the expensive core-checking step of traditional core chase procedures. As we point out, the same applies to some previous model constructions from the DL literature,.

With our semantics based on austere (i.e., core) models in place, we can tackle the problem of devising an algorithm for validation. Constructing the austere model may be infeasible in practice, since it is infinite in general. Instead, we use our finite representation of the model. Ideally, we would like to realise validation via *rewriting*. That is, we want to compile a given ontology and a set of SHACL constraints into a new set of SHACL constraints that incorporate the relevant knowledge of the ontology in such a way that the implicit facts are taken into account in validation, without having to explicitly add them to the graph. Rewriting techniques are very desirable as they open the way to reuse standard SHACL validators to perform validation in the presence of ontologies. We use the finite representation of the austere canonical model to construct a complex structure that stores so-called *2-types*, which intuitively represent an abstract copy of a possible object and its neighbours in the austere model of a given data graph—enriched with information about the shapes that are (not) satisfied in implied substructures. This structure is used to induce a modified set of SHACL constraints that validate over a given data graph exactly when the original constraints validate over the austere canonical model of the input graph and the ontology. We first develop the technique for a positive fragment of SHACL (with minor restrictions) and then lift it to the case of *stratified SHACL* which allows both recursion and negation, but restricts their interaction.

The contributions of this paper can be summarised as follows:
- •
	In, we provide a semantics for validating SHACL in presence of ontologies, and argue why it is intuitive. For this, we introduce the notion of the austere canonical model, a canonical model which locally does not contain redundant structures, and advocate checking for validation over this specific model.
- •
	In, we discuss that, although the austere canonical model may be infinite, we can provide a finite representation in the form of the *good successor configuration*. We show that the result of our construction coincides with the model construction proposed in and is indeed universal. Moreover, we show that the local minimality of the austere canonical model suffices for global minimality: the austere canonical model is a core, and it is the unique universal core model of the consistent Horn- $ALCHIQ$ TBox.
- •
	In, we define a fragment of recursive SHACL named *stratified SHACL*. Our notion of stratification is based on the well-known class of stratified logic programs. We define a *least fixed point semantics* for it that coincides with both the stable and the well-founded semantics. We also show that our fragment has a rather simple normal form with the same expressivity.
- •
	In and, we are able to bring validation over the possibly infinite austere canonical model back to validation of a rewritten set of constraints over an enriched ABox. We do this by combining the normal form of stratified SHACL with the information captured in the good successor configuration.
- •
	In, we discuss some techniques to create a pure rewriting of SHACL with ontologies into plain SHACL. One of these techniques proposes an extension of SHACL, SHACL <sup><em>b</em></sup>, which also allows to define labels for roles.
- •
	Lastly, in, we determine the complexity of validating SHACL with ontologies. We find that in presence of Horn- $ALCHIQ$ TBoxes, SHACL validation is ExpTime complete in combined complexity, and PTime complete in data complexity. Moreover, we show that validating a very simple fragment of SHACL, simple SHACL, over a rather light (less expressive than *DL-Lite* $R$) description logic ontology already suffices to find ExpTime hardness in combined complexity.

## 2\. Preliminaries

*Data Graphs and Interpretations* Let *N <sub>C</sub>, N <sub>R</sub>, N <sub>I</sub>* and *N <sub>B</sub>* denote countably infinite, mutually disjoint sets of *concept names* (also known as *class names*), *role names* (or, *property names*), *individuals* (or, *constants*), and *blank nodes* respectively. Let $N‾R:={p,p−∣p∈NR}$ denote *roles*, and let $N‾C:=NC∪{⊤,⊥}$. For every *p*  ∈  *N <sub>R</sub>*, let $\left(p^{-}\right)^{-} = p$. For each set of roles $R⊆N‾R$, set $R−:={r−∣r∈N‾R}$. An *atom* (or, *assertion*) is an expression of the form *A* (*e*) or *p* (*e, e* ′), for *A*  ∈  *N <sub>C</sub>, p*  ∈  *N <sub>R</sub>* and { *e, e* ′}⊆ *N <sub>I</sub>*  ∪  *N <sub>B</sub>*. An *ABox* (or a *data graph*) $A$ is a finite set of atoms such that no blank nodes are used.

An *interpretation* is a pair $\mathcal{I} = \left(\Delta^{\mathcal{I}} , \cdot^{\mathcal{I}}\right)$, where $\Delta^{\mathcal{I}}$ is a non-empty set (called *domain*) and $\cdot^{\mathcal{I}}$ is a function that maps every *A*  ∈  *N <sub>C</sub>* to a set $A^{\mathcal{I}} \subseteq \Delta^{\mathcal{I}}$, every *p*  ∈  *N <sub>R</sub>* to a binary relation $p^{\mathcal{I}} \subseteq \Delta^{\mathcal{I}} \times \Delta^{\mathcal{I}}$, and every individual and blank node *e*  ∈  *N <sub>I</sub>*  ∪  *N <sub>B</sub>* to an element $e^{\mathcal{I}} \in \Delta^{\mathcal{I}}$. Let $(p−)I:={(e′,e)∣(e,e′)∈pI}$. We make the standard name assumption, which means $e^{\mathcal{I}} = e$ for all interpretations $I$, and all *e*  ∈  *N <sub>I</sub>*  ∪  *N <sub>B</sub>*.

The *canonical interpretation* $\mathcal{I}_{\mathcal{A}}$ for an ABox $A$ is defined by setting $\Delta^{\mathcal{I}_{\mathcal{A}}} = N_{I} \cup N_{B}$, $AIA={c∣A(c)∈A}$ for all *A*  ∈  *N <sub>C</sub>*, $pIA={(c,d)∣p(c,d)∈A}$ for all *p*  ∈  *N <sub>R</sub>*, and $e^{\mathcal{I}_{\mathcal{A}}} = e$ for every individual or blank node *e*  ∈  *N <sub>I</sub>*  ∪  *N <sub>B</sub>*. We consider an interpretation to be *finite* whenever $A^{\mathcal{I}}$ and $p^{\mathcal{I}}$ are finite sets, for each *A*  ∈  *N <sub>C</sub>* and *p*  ∈  *N <sub>R</sub>*, and only finitely many concepts and roles have a non-empty interpretation.

*Morphisms* Let $A$ and $\mathcal{A}^{'}$ be sets of atoms. A *homomorphism* from $A$ to $\mathcal{A}^{'}$ is a function $h : \Delta^{\mathcal{I}_{\mathcal{A}}} \rightarrow \Delta^{\mathcal{I}_{\mathcal{A}}^{'}}$ such that for all { *e, e* ′}⊆ *N <sub>I</sub>*  ∪  *N <sub>B</sub>*, all *A*  ∈  *N <sub>C</sub>* and all *p*  ∈  *N <sub>R</sub>*, (i) if $e \in \Delta^{\mathcal{A}} \cap N_{I}$, then $h(e)=e$, (ii) if $A(e)∈A$, then $A \left(h \left(e\right)\right) \in \mathcal{A}^{'}$, and (iii) if $p \left(e , e^{'}\right) \in \mathcal{A}$, then *p* (*h* (*e*), *h* (*e* ′)) ∈  *A* ′. A homomorphism is called *strong* if (ii) and (iii) are strengthened to “ $A(e)∈A$ iff $A \left(h \left(e\right)\right) \in \mathcal{A}^{'}$ ” and “ $p \left(e , e^{'}\right) \in \mathcal{A}$ iff *p* (*h* (*e*), *h* (*e* ′)) ∈  *A* ′”, respectively. An *embedding* is a strong injective homomorphism, an *isomorphism* is a surjective embedding and an *endomorphism* of $A$ is a homomorphism from $A$ to itself.

*Syntax and Semantics of normalised Horn-* $ALCHIQ$ Given a set $M={M0,…,Mk}$ consisting of only concept or role names, let $\sqcap M : = M_{0} \sqcap \ldots \sqcap M_{k}$. $P(X)$ denotes the power set of *X*. For a tuple $\overset{\rightarrow}{x} = \left(x_{1} , \ldots , x_{n}\right)$ and 1 ≤  *j*  ≤  *n*, we let $\pi_{i} \left(\overset{\rightarrow}{x}\right) = x_{i}$ be its *ith projection*.

In a *normalised Horn-* $ALCHIQ$ *TBox* $T$ each concept inclusion takes one of the following forms:$\begin{aligned}(\text{F1}) A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq B & (\text{F3}) A \sqsubseteq \forall r . B \\ (\text{F2}) A \sqsubseteq \leq_{1} r . B & (\text{F4}) A \sqsubseteq \exists r . B\end{aligned}$ for ${A,A0,…,An,B}⊆N‾C$ and $r∈N‾R$. Furthermore, $T$ may contain role inclusions of the form *r* ⊑ *r* ′, for ${r,r′}⊆N‾R$. For more details and a discussion regarding going beyond normalised Horn- $ALCHIQ$, we refer the reader to.

The semantics of normalised Horn- $ALCHIQ$ is defined in terms of interpretations $I$: a role or concept inclusion axiom *C* ⊑ *D* is satisfied whenever $C^{\mathcal{I}} \subseteq D^{\mathcal{I}}$. To this end, the interpretation function is extended in the following way: $\top^{\mathcal{I}} : = \Delta^{\mathcal{I}}$, $⊥^{\mathcal{I}} : = \emptyset$, $\left(A_{0} \sqcap \ldots \sqcap A_{n}\right)^{\mathcal{I}} : = A_{0}^{\mathcal{I}} \cap \ldots \cap A_{n}^{\mathcal{I}}$, $(≤1r.B)I:={e∈ΔI∣|{e′∈ΔI∣(e,e′)∈rI,e′∈BI}|≤1}$, $(∀r.B)I:={e∈ΔI∣∀e′∈ΔI.(e,e′)∈rI→e′∈BI}$, $(∃r.B)I:={e∈ΔI∣∃e′∈ΔI.(e,e′)∈rI∧e′∈BI}$. We say a TBox $T$ is satisfied in $I$ if all its axioms are satisfied. In that case, we say $I$ is a model of $T$. To denote logical entailment, we may write $T⊧γ$ if every model of the TBox $T$ is also a model of *γ* (where the latter may be any inclusion, a TBox, or an ABox). We call the combination of a Horn- $ALCHIQ$ TBox $T$ and any ABox $A$ a Horn- $ALCHIQ$ knowledge base $(T,A)$. We say that $A$ is *consistent* with $T$ (or, that $(T,A)$ is consistent) if there is a model of $A$ and $T$.

We call an interpretation $I$ a *universal model* (of a knowledge base $(T,A)$) whenever $I$ is a model of $(T,A)$ and there exists a homomorphism of $I$ into any model of $(T,A)$. Every consistent $(T,A)$ has a universal model. Moreover, the universal model of $(T,A)$ coincides with the universal model of $\left(\mathcal{T}^{\mathit{pos}} , \mathcal{A}\right)$, where $\mathcal{T}^{\mathit{pos}}$ contains all axioms in $T$ that do not contain ⊥. Therefore, we may assume that there are no occurrences of ⊥ if $(T,A)$ is consistent.

*Regular Path Expressions* Let *E* be any *regular expression* over some alphabet Σ, and *L <sub>E</sub>* the language defined by some regular expression *E*. We say *E* is a regular *path* expression, if $Σ=N‾R$. For each interpretation $I$ and each regular path expression *E* over the alphabet $N‾R$, set $\left(e , e^{'}\right) \in E^{\mathcal{I}}$ if there exists *r* <sub>0</sub> ⋅⋅⋅ *r <sub>n</sub>*  ∈  *L <sub>E</sub>* and ${e1,…,en}⊆ΔI$ such that $\left(e , e_{1}\right) \in r_{0}^{\mathcal{I}}$, $\left(e_{n} , e^{'}\right) \in r_{n}^{\mathcal{I}}$ and for all $1≤i≤n−1$, $\left(e_{i} , e_{i + 1}\right) \in r_{i}^{\mathcal{I}}$.

Furthermore, for each language *L <sub>E</sub>*, there exists a non-deterministic finite automaton $\mathcal{M} = \left(Q , \Sigma , q_{I} , \Delta , q_{F}\right)$ that accepts exactly all words in *L <sub>E</sub>*. Here *Q* is a set of states, Σ the alphabet, { *q <sub>I</sub>, q <sub>F</sub>* }⊆ *Q* the initial and final state, and Δ⊆ *Q*  × Σ ×  *Q* the transition relation. In this case, we say $M$ recognises *L <sub>E</sub>*.

*Non-Recursive Shape Constraint Language (SHACL)*

We define *shape expressions*, following, in the following way $\begin{matrix}\varphi : : = c \mid A \mid \top \mid \neg \varphi \mid \varphi \land \varphi \mid \varphi \lor \varphi \mid \exists_{\geq n} E . \varphi \mid \mathsf{eq} \left(E , r\right) \mid \mathsf{disj} \left(E , r\right) \mid \mathsf{closed} \left(R\right) ,\end{matrix}$where *c*  ∈  *N <sub>I</sub>, A*  ∈  *N <sub>C</sub>, n*  ≥ 1, *R* a finite subset of $N‾R$ and *E* a regular path expression. We use ⊤ as a shorthand for *A* ∨¬ *A*, for some concept name *A*  ∈  *N <sub>C</sub>*. As we impose restrictions on the use of negation later in this work, we add φ∨φ and φ∧φ explicitly to the syntax.

Given an interpretation $I$, we say a node *e*  ∈  *N <sub>I</sub>*  ∪  *N <sub>B</sub> validates* a shape expression φ, if $e∈I(φ)$, where $I(φ)$ is inductively defined in. Furthermore, let $G$ be a set of targets of the form φ(*c*) or φ(*A*), where φ is a shape expression, *c*  ∈  *N <sub>I</sub>* and *A*  ∈  *N <sub>C</sub>*. Given an interpretation $I$, we say $I$ *validates* $G$ if for all $φ(c)∈G$, we find *c* validates φ, and for all $φ(A)∈G$, if $c \in A^{\mathcal{I}}$, then *c* validates φ. Considering readability, we will also write $A$ validates $G$, for any set of atoms $A$, instead of using the canonical interpretation $\mathcal{I}_{\mathcal{A}}$.

![Fig. 1](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr1.jpg)

Download: Download high-res image (181KB)

In this definition, we do not allow shape names in shape expressions, as introduced in. This makes SHACL *non-recursive* and allows for the simple semantics we define above. In general, SHACL allows shape names in shapes expressions and may be *recursive*, in which case there is no unique accepted semantics,,. For simplicity, we formulate all the results in and for non-recursive SHACL. However, the results and definitions can be directly applied to recursive SHACL under all the semantics considered in,,. Starting from, we concentrate on a recursive form of SHACL, stratified SHACL, extending the work presented in. The fragment we study in this work is not the full stratified, recursive version; it lacks counting quantifiers and the closed-operator, and only treats a guarded version of disjointness and equality. This is discussed in more detail in and. Removing these constraints leads to new interesting problems we leave for future work.

## 3\. Validation with ontologies

In this section we propose a semantics for SHACL validation in the presence of a Horn- $ALCHIQ$ ontology. More precisely, for a given TBox $T$, an ABox $A$, and a set of targets $G$, we aim to define when $(T,A)$ validates $G$. A natural first idea would be to follow the usual open-world semantics of Horn- $ALCHIQ$ and check validation on *all models* of $A$ and $T$. While this works well for positive constraints, it does not yield a natural semantics in the presence of negation, as illustrated in the following simple example.

**Example 3.1**

Consider the ABox $A$ consisting of the facts *hasPet* (*linda, blu*), *Bird* (*blu*), an empty TBox $T$ and the target φ(*linda*) such that φ is given by $\begin{matrix}\varphi = \exists \mathit{hasPet} . \neg \mathit{Dog} .\end{matrix}$Naturally, $A$ validates $G$, as *linda* indeed validates φ, which corresponds to having a pet that is not a dog. Note that since we have an empty TBox, we would like to be in the usual setting of validation here. That is, one would expect $(T,A)$ to validate $G$. However, if we consider all possible models of $(T,A)$, we find non-validation: the case in which *blu* is both a *Bird* and a *Dog* is also a model of $(T,A)$. This shows that the certain answer semantics, guaranteeing validation in all models, is not always meaningful in the presence of negation.♥

The above example illustrates the problem of finding an intuitive semantics for shape expressions, or, on the same note, queries, with negation. Similar issues show up in shape expressions containing a more hidden form of negation, like equality, disjointness and the closed-operator. Also counting quantifiers have the capability of distinguishing between different universal models. Roughly speaking, adding facts to the data may cause a previously validated setting to become invalid. To this end, we aim at an intuitive semantics that coincides with the usual validation in case the TBox is empty, but also lets the TBox axioms influence the validation results in the relevant cases. As done in related settings (see e.g.,,, ) we rely on the *chase* procedure known from Knowledge Representation and Database Theory. The idea is that a chase procedure takes as input an ABox and TBox and iteratively applies the axioms of the TBox to the data by adding atoms over possibly fresh individuals until all the axioms in the TBox are satisfied. The result of the chase is a so-called *canonical* or *universal* model. Since there exists a homomorphism of all models of this type into every other model of the ABox and TBox, a canonical model is often used as a representative of all models.

There are several chase variants producing canonical models with different properties. While for positive shape expressions these differences do not lead to different validation results, shape expressions using negation can distinguish between them. Thus, the semantics we propose is based on a particular variant of the set of universal models, based on local minimality. The idea is to avoid redundant structures as much as we can: as illustrated in the next example, we do not wish to assume the existence of a second pet of *linda* if there is no need for this assumption. At the same time, we do not want to give up on the model being universal. This specific model, the *austere canonical model*, will be constructed in the rest of this section.

In the following example, we show that shape expressions with negation can indeed distinguish between different universal models, and illustrate how the austere canonical model does not have the redundant structures that may appear in other universal models.

**Example 3.2**

Consider the ABox $A={PetOwner(linda),hasWingedPet(linda,blu),Bird(blu)}$ and the following three axioms:$\begin{aligned}\mathit{PetOwner} \sqsubseteq \exists \mathit{hasPet} , & \mathit{hasWingedPet} \sqsubseteq \mathit{hasPet} , \\ \mathit{PetOwner} \sqsubseteq \exists \mathit{hasWingedPet} .\end{aligned}$The austere canonical model (right in ) will only add a *hasPet* -role from *linda* to *blue*, as we will see below. In contrast, the canonical model obtained from the oblivious chase or Skolem chase (left in ) will introduce two fresh objects to satisfy the two axioms with existential restrictions.

![Fig. 2](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr2.jpg)

Download: Download high-res image (86KB)

When graphically representing interpretations, domain objects are written in rectangular boxes (individuals in red and blank nodes in orange boxes), followed by a semicolon and the concept names in whose interpretations it participates, if any. Roles are depicted as labelled arrows.

Now let us consider the same shape expression and target as in the previous example: $φ=∃hasPet.¬Bird}$ and $G={φ(linda)}$. The target asks to validate whether *linda* has a pet that is not a bird. Clearly, the austere canonical model provides the expected answer, as it does not validate $G$. In contrast, the canonical model on the left-hand-side of the figure, also the semantics of adopted for SHACL in, results in the unintended validation of $(C,G)$.♥

In the rest of this section, we will make the above precise.

### 3.1. Good successor configuration

To capture local minimality, we define the auxiliary notion of the *good successor configuration*. It determines, for each point *e* in a model, the set of fresh successor individuals and the roles connecting them to *e* in the austere canonical model, together with the concepts that must hold at *e*. To describe the good successor configuration, we use *2-types, 1½-types* and *1-types*. We say *t* is a *2* -type if $t∈P(NC)×P(N‾R)×P(NC)$. Similarly, we let *u* be a *1½* -type in case $u∈P(N‾R)×P(NC)$. A *2* -type describes a pair of nodes and the roles between them, while a *1½* -type describes a set of roles leading to one node. A *1* -type $c \in \mathcal{P} \left(N_{C}\right)$ is simply a set of concept names. Furthermore, we define the *inverse* function *inv* mapping a *2* -type to a *2* -type by setting $\mathit{inv} \left(t\right) : = \left(\pi_{3} \left(t\right) , \left(\pi_{2} \left(t\right)\right)^{-} , \pi_{1} \left(t\right)\right)$.

To understand the good successor configuration, assume we are building a model in a chase-like step-by-step manner. We want to introduce the children that a node *c* needs to satisfy the TBox. Let $c_{1} , \ldots , c_{n}$ be the neighbours that *c* already has (either multiple neighbours already given in the ABox, or the one single neighbour/parent *c* <sub>1</sub> has in the anonymous part). We use a set *F* of *2* -types to describe *c* and its environment as follows. For each *c <sub>i</sub>*, some type *t <sub>i</sub>*  ∈  *F* describes *c* in relation to *c <sub>i</sub>*: (i) *π* <sub>1</sub> (*t <sub>i</sub>*) is the *1* -type of *c*, that is, the concept names whose interpretations contain *c*, (ii) *π* <sub>3</sub> (*t <sub>i</sub>*) is the *1* -type of *c <sub>i</sub>*, and (iii) *π* <sub>2</sub> (*t <sub>i</sub>*) contains all role names connecting *c* and *c <sub>i</sub>*. Note that, by item (i), $\pi_{1} \left(t_{i}\right) = \pi_{1} \left(t_{j}\right)$ for all { *t <sub>i</sub>, t <sub>j</sub>* }⊆ *F*. The good successor configuration $\mathit{succ}_{\mathcal{T}}$, which is defined in the following definition, is a function that takes such an *F*, and returns the description of the children that *c* needs to satisfy all axioms in $T$, as a set of *1½* -types: we will add a new blank node *d <sub>i</sub>* for each $u_{i} \in \mathit{succ}_{\mathcal{T}} \left(F\right)$; *d <sub>i</sub>* will be connected to *c* via the roles in *π* <sub>1</sub> (*u <sub>i</sub>*), and have *1* -type *π* <sub>2</sub> (*u <sub>i</sub>*).

However, the good successor configuration does not just take specific neighbourhoods of the nodes in some database as input; it is defined for all possible *F* ’s. This makes the good successor configuration data independent. Thus, when determining the data complexity of any algorithm using the good successor configuration, its size does not have to be considered.

Moreover, the following definition defines a unique set of *1½* -types; this is proven at the end of this subsection. Finally, note that we use expressions of the form ∃(⊓ *R*).⊓ *N* below, for $R⊆N‾R$, *N* ⊆ *N <sub>C</sub>* with the following semantics:$(∃(⊓R).⊓N)I:={e∈ΔI∣∃e′∈ΔI∀r∈R.(e,e′)∈rI∧e′∈(⊓N)I}.$ 

**Definition 3.3**

Given a normalised Horn- $ALCHIQ$ TBox $T$ and set of *2* -types *F* such that $\pi_{1} \left(t\right) = \pi_{1} \left(t^{'}\right)$ for all { *t, t* ′}⊆ *F*, the *good successor configuration* $\mathit{succ}_{\mathcal{T}} \left(F\right)$ is a possibly empty set of *1½* -types *u* such that:
- (R1)
	If (i) *M* ⊆ *π* <sub>1</sub> (*t*) for some *t*  ∈  *F*, (ii) $T⊧⊓M⊑∃(⊓R).⊓N$ for some *N* ⊆ *N <sub>C</sub>*, $R⊆N‾R$, and (iii) for all *t*  ∈  *F*, $R \neg \subseteq \pi_{2} \left(t\right)$ or $N \neg \subseteq \pi_{3} \left(t\right)$, then there exists $u \in \mathit{succ}_{\mathcal{T}} \left(F\right)$ such that *R* ⊆ *π* <sub>1</sub> (*u*) and *N* ⊆ *π* <sub>2</sub> (*u*);
- (R2)
	If $u \in \mathit{succ}_{\mathcal{T}} \left(F\right)$, then there exist *M* ⊆ *π* <sub>1</sub> (*t*) for some *t*  ∈  *F*, such that $\mathcal{T} \models \sqcap M \sqsubseteq \exists \left(\sqcap \pi_{1} \left(u\right)\right) . \sqcap \pi_{2} \left(u\right)$;
- (R3)
	There does not exist ${u,u′}⊆succT(F)$ with $u \neq u^{'}$ such that *π* <sub>1</sub> (*u*)⊆ *π* <sub>1</sub> (*u* ′) and *π* <sub>2</sub> (*u*)⊆ *π* <sub>2</sub> (*u* ′);
- (R4)
	If $u \in \mathit{succ}_{\mathcal{T}} \left(F\right)$, then $\pi_{1} \left(u\right) \neg \subseteq \pi_{2} \left(t\right)$ or $\pi_{2} \left(u\right) \neg \subseteq \pi_{3} \left(t\right)$, for all *t*  ∈  *F*.

A *child* of a *2* -type *t* is a *2* -type $t^{'} \in \mathit{child}_{\mathcal{T}} \left(t\right)$ such that $\pi_{1} \left(t^{'}\right) = \pi_{3} \left(t\right)$ and $\left(\pi_{2} \left(t^{'}\right) , \pi_{3} \left(t^{'}\right)\right) \in \mathit{succ}_{\mathcal{T}} \left(\mathit{inv} \left(t\right)\right)$.

For readability, we define the good successor configuration of a single type as the good successor configuration of the set containing only this type.

As mentioned, the good successor configuration focusses on checking which axioms are not yet satisfied in the context described by *F*. For each such unsatisfied axiom (R1) implies the existence of a child *d <sub>i</sub>* represented by some *u <sub>i</sub>* that ensures the satisfaction of the axiom. (R2) represents the other direction: for each child *d <sub>i</sub>*, there must exist an axiom implying the information in the *1½* -type *u <sub>i</sub>*. Lastly, (R3) and (R4) check whether there are no superfluous children: they enforce we do not add two children *d <sub>i</sub>* and *d <sub>j</sub>* such that all information about *d <sub>i</sub>* is subsumed by *d <sub>j</sub>*, or a child *d <sub>i</sub>* that is already subsumed by the environment described in *F*. We will use these properties extensively in to prove that the austere canonical model is in fact a core.

In the following example, we compute the good successor configuration for a concrete case.

**Example 3.4**

Consider the axioms below, together forming the TBox $T$.$\begin{aligned}(\text{T1}) B_{0} \sqsubseteq \exists r_{0} . A_{0} & (\text{T5}) r_{0} \sqsubseteq r_{1} \\ (\text{T2}) B_{0} \sqsubseteq \exists r_{1} . A_{1} & (\text{T6}) B_{1} \sqsubseteq \exists r_{2} . \top \\ (\text{T3}) B_{1} \sqsubseteq \leq_{1} r_{1} . A_{1} & (\text{T7}) B_{0} \sqsubseteq \forall r_{2} . A_{2} \\ (\text{T4}) A_{0} \sqsubseteq A_{1}\end{aligned}$

We want to compute the good successor configuration for the following sets of *2* -types: $F={({B0,B1},{r1},{A2}),({B0,B1},{r1},{A2})}$ and $F′={({B0,B1},{r1,r2},{A2})}$.

First, note that (T1–5) together lets us conclude $\mathcal{T} \models B_{0} \sqcap B_{1} \sqsubseteq \exists \left(r_{0} \sqcap r_{1}\right) . \left(A_{0} \sqcap A_{1}\right)$. Moreover, combining (T6) and (T7) gives us $\mathcal{T} \models B_{0} \sqcap B_{1} \sqsubseteq \exists r_{2} . A_{2}$. Thus, by (R1), we find that there must exist ${u,u′}⊆succT(F)$ such that { *r* <sub>0</sub>, *r* <sub>1</sub> }⊆ *π* <sub>1</sub> (*u*), { *A* <sub>0</sub>, *A* <sub>1</sub> }⊆ *π* <sub>2</sub> (*u*), { *r* <sub>2</sub> }⊆ *π* <sub>1</sub> (*u* ′) and { *A* <sub>2</sub> }⊆ *π* <sub>2</sub> (*u* ′). Note that considering $π1(u)={r0,r1}$, $π2(u)={A0,A1}$, $π1(u′)={r2}$ and $π2(u′)={A2}$ suffices, as we know that these are the axioms carrying most information that can be derived. It is easy to check that indeed $succT(F)={u,u′}$; see also.

![Fig. 3](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr3.jpg)

Download: Download high-res image (90KB)

For computing the good successor configuration of *F* ′, we can mostly follow the above strategy. However, *u* ′ cannot be added by (R1), as *u* ′ is already contained in the environment described by *F* ′. This does not hold for *u*, so it is easy to check that $succT(F′)={u}$.♥

Essential to the rest of this article is the uniqueness and existence of the good successor configuration. This implies that the construction described in the next chapter creates a unique structure.

**Proposition 3.5**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *, for each set of* $2$ *\-types F, such that* $\pi_{1} \left(t\right) = \pi_{1} \left(t^{'}\right)$ *for all* { *t, t* ′}⊆ *F, there exists a unique good successor configuration* $\left(s u c c\right)_{\mathcal{T}} \left(F\right)$ *.*

**Proof**

To show uniqueness, suppose for a given set of *2* -types *F*, such that $\pi_{1} \left(t\right) = \pi_{1} \left(t^{'}\right)$ for all { *t, t* ′}⊆ *F*, there exist two good successor configurations $U \neq U^{'}$. W.l.o.g., assume that there exists *u*  ∈  *U*, such that $u \notin U^{'}$. By (R2), we know that there exists *M* ⊆ *π* <sub>1</sub> (*t*) for some *t*  ∈  *F* such that $\mathcal{T} \models \sqcap M \sqsubseteq \exists \left(\sqcap \pi_{1} \left(u\right)\right) . \sqcap \pi_{2} \left(u\right)$. Moreover, by (R4), we can conclude that $\pi_{1} \left(u\right) \neg \subseteq \pi_{2} \left(t\right)$ or $\pi_{2} \left(u\right) \neg \subseteq \pi_{3} \left(t\right)$ for all *t*  ∈  *F*, so we can apply rule (R1) with respect to *U* ′: there must exist *u* ′ ∈  *U* ′ such that *π* <sub>1</sub> (*u*)⊆ *π* <sub>1</sub> (*u* ′) and *π* <sub>2</sub> (*u*)⊆ *π* <sub>2</sub> (*u* ′). By similar reasoning, we find that there must exist *u* ″ ∈  *U* such that *π* <sub>1</sub> (*u* ′)⊆ *π* <sub>1</sub> (*u* ″) and *π* <sub>2</sub> (*u* ′)⊆ *π* <sub>2</sub> (*u* ″). Combining this with (R4), we find that $\pi_{1} \left(u\right) = \pi_{1} \left(u^{''}\right)$ and $\pi_{2} \left(u\right) = \pi_{2} \left(u^{''}\right)$, from which we derive that *u*  ∈  *U* ′, which is a contradiction. Thus, $U = U^{'}$. For existence, note that we can first add all possible *1½* -types that are not eliminated by (R2). It follows that (R1) is clearly satisfied. Then, remove all *1½* -types that are eliminated because of (R3) or (R4).

By using the inference rules from Table 2 in, combined with the approach described in this proof, it becomes clear that the good successor configuration can actually be computed.

### 3.2. Austere canonical model

The good successor configuration locally describes how to satisfy the TBox axioms based on some incentives; minimality and universality. Before we use it as a building block in the austere canonical model, we first want to complete $A$ under all but the axioms with existential restrictions. We will use the notation $\mathcal{A}_{\mathcal{T}}$ for this completed ABox, which is in fact the least fixed point of an immediate consequence operator, a monotone function. Note that a function *f* is *monotone* if *x* ⊆ *y* implies *f* (*x*)⊆ *f* (*y*). The point of this operator is to mimic firing the axioms without existential restrictions as soon as they become applicable. We perform the least fixed point starting from a non-empty set: the ABox. This is made precise in the following definitions.

**Definition 3.6**

Let *X* be any set and *T*: *X*  →  *X* be any monotone function, which we will call an *immediate consequence operator*, define for any *S* ⊆ *X, T* ↑ <sup><em>ω</em></sup> (*S*) as follows:
- 1.
	*T* ↑ <sup>0</sup> (*S*) ≔  *S*,
- 2.
	$\left(T \uparrow\right)^{n + 1} \left(S\right) : = T \left(T \uparrow^{n} \left(S\right)\right)$ for *n*  ≥ 0, and
- 3.
	$\left(T \uparrow\right)^{\omega} \left(S\right) : = \cup_{n = 0}^{\infty} \left(T \uparrow\right)^{n} \left(S\right)$.

**Definition 3.7 (Completion**

$\mathcal{A}_{\mathcal{T}}$ **)** Given a normalised Horn- $ALCHIQ$ TBox $T$, define an immediate consequence operator $T_{\mathcal{T}}$ that maps a set of atoms *X* to a set of atoms as follows:$TT(X):=X∪{B(a)∣{A0(a),…,An(a)}⊆X,T⊧A0⊓…⊓An⊑B}∪{B(a)∣{r(b,a),A(b)}⊆X,A⊑∀r.B∈T}∪{r(a,b)∣r′(a,b)∈X,T⊧r′⊑r}∪{r(b,a)∣r′(a,b)∈X,T⊧r′⊑r−}∪{Bi(b)∣{A(a),A1(a),…,An(a),r(a,b),B(b)}⊆X,A⊑≤1r.B∈T,T⊧A1⊓…⊓An⊑∃(r1⊓…⊓rm).B1⊓…⊓Bm,A=Aj,r=rkforsomej,k}∪{ri(a,b)∣{A(a),A1(a),…,An(a),r(a,b),B(b)}⊆X,A⊑≤1r.B∈T,T⊧A1⊓…⊓An⊑∃(r1⊓…⊓rm).B1⊓…⊓Bm,A=Aj,r=rkforsomej,k}.$Given any ABox $A$, let $N_{I} \left(\mathcal{A}\right)$ be the set of individuals occurring in $A$. We set $A \left(a\right) \in \mathcal{A}_{\mathcal{T}}$ and $r \left(a , b\right) \in \mathcal{A}_{\mathcal{T}}$, iff $A \left(a\right) \in T_{\mathcal{T}} \uparrow^{\omega} \left(\mathcal{A}\right)$, respectively $r \left(a , b\right) \in T_{\mathcal{T}} \uparrow^{\omega} \left(\mathcal{A}\right)$, for all *A*  ∈  *N <sub>C</sub>, r*  ∈  *N <sub>R</sub>*, ${a,b}⊆NI(A)$.

It can be verified how the rules in this definition mimic the completion rules for ABoxes under Horn- $SHIQ$ ontologies in.

**Example 3.8**

Let $A={B0(a),r0(a,b),r2(a,b),A0(b)}$ and $T$ as in. Then $AT=A∪{r1(a,b),A1(b),A2(b)}$.♥

Now we are ready to define the austere canonical model. In this model, we use words to represent the elements in the anonymous parts of the model: the first letter corresponds to an individual in the data graph, followed by a letter for each node connecting the named node to the data graph. Thus, the length of the word naming an anonymous node indicates its ‘distance’ from the data graph. We mainly use this distance in the next section in which we discuss the relation to core models.

**Definition 3.9**

Let $(T,A)$ be a normalised Horn- $ALCHIQ$ knowledge base, and let $N_{\left(\mathcal{T} , \mathcal{A}\right)} \subseteq N_{B}$ be the set of finite words of the form $a k_{1} \ldots k_{n}$, with $a \in N_{I} \left(\mathcal{A}\right)$ such that for all 1 ≤  *i*  ≤  *n, k <sub>i</sub>* is a *2* -type such that the following hold:
- 1.
	$π1(k1)={A∣A(a)∈AT}$ and $\left(\pi_{2} \left(k_{1}\right) , \pi_{3} \left(k_{1}\right)\right) \in \mathit{succ}_{\mathcal{T}} \left(T_{a}\right)$, for $Ta={({A∣A(a)∈AT},∅,∅)}∪⋃b∈NI,r(a,b)∈AT{({A∣A(a)∈AT},{r∣r(a,b)∈AT},{A∣A(b)∈AT})};$
- 2.
	for every 1 ≤  *i*  <  *n*, $k_{i + 1} \in \mathit{child}_{\mathcal{T}} \left(k_{i}\right)$.

We use *tail* (*w*) to denote the last *2* -type *k <sub>n</sub>* in, and $|w|=n+1$ as the length of a word $w \in N_{\left(\mathcal{T} , \mathcal{A}\right)}$ of the form $a k_{1} \ldots k_{n}$.

The *austere canonical model* $can(T,A)$ of a normalised Horn- $ALCHIQ$ knowledge base $(T,A)$ is the interpretation $can(T,A)$ with domain $\Delta^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)} : = N_{I} \left(\mathcal{A}\right) \cup N_{\left(\mathcal{T} , \mathcal{A}\right)}$ such that for all $a \in N_{I} \left(\mathcal{A}\right)$, concept names *A* and roles *r*, the following hold:$acan(T,A):=aAcan(T,A):={a∈NI∣A(a)∈AT}∪{w∈N(T,A)∣A∈π3(tail(w))}rcan(T,A):={(a,b)∈NI×NI∣r(a,b)∈AT}}∪{(w1,w2)∈(NI∪N(T,A))×N(T,A)∣w2=w1k,r∈π2(k)}∪{(w2,w1)∈(NI∪N(T,A))×N(T,A)∣w2=w1k,r−∈π2(k)}.$

This is illustrated in the following example.

**Example 3.10**

Let $A={B0(a),B1(a),r1(a,b),r1(a,c),A2(b),A2(c)}$ and suppose $T$ contains the same axioms as in. We find that $\mathcal{A}_{\mathcal{T}} = \mathcal{A}$, as none of the axioms there can derive any new information about ABox individuals.

Now consider the set $Fa={({B0,B1},{r1},{A2}),({B0,B1},{r1},{A2})}$, based on the neighbours of *a*. The good successor configuration of this set has already been computed in: $succT(Fa)={u,u′}$, where $u=({r0,r1},{A0,A1})$ and $u′=({r2},{A2})$. Following the definition of the austere canonical model, we find ${at,at′}⊆N(T,A)$, for $t=({B0,B1},π1(u),π2(u))$ and $t′=({B0,B1},π1(u′),π2(u′))$. Now we can read off the structure of the anonymous part of the constructed model: we find for instance that $\left(a , a t\right) \in r_{0}^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$ and $a t \in A_{0}^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$.♥

For a consistent knowledge base $(T,A)$, the austere canonical model $can(T,A)$ exists and is unique, which follows directly from the uniqueness and existence of the good successor configuration and $\mathcal{A}_{\mathcal{T}}$.

Note that the austere canonical model coincides with the result of the model construction presented in. In that construction, $A$ is first closed under all implied axioms, except for the ones with existential restrictions, followed by applying all so-called ‘maximal’ axioms with existential restrictions in a chase like manner whenever applicable. To see the correspondence with our construction, it suffices to check that formalises the first step, whilst the good successor configuration captures exactly the ‘maximality’ of axioms in (R3) and the applicability in (R3) and (R4).

**Corollary 3.11**

*For each normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *,* $can(T,A)$ *is (i) a model of* $(T,A)$ *that is (ii) universal.*

This result follows directly from in and justifies the name ‘canonical’ we gave to our construction. Finally, we define SHACL validation with Horn- $ALCHIQ$ as validation of SHACL over the austere canonical model.

**Definition 3.12 (Validation with Horn-**

$ALCHIQ$ **)** Given a normalised Horn- $ALCHIQ$ knowledge base $(T,A)$ and a set of targets $G$, we say $(T,A)$ validates $G$ if $can(T,A)$ validates $G$.

In general, given any semantics for SHACL validation, we define the semantics of SHACL validation with Horn- $ALCHIQ$ ontologies, as validation of SHACL over the austere canonical model. In particular, this approach will be used for stratified SHACL, a fragment of recursive SHACL. We refer the reader to for more details.

## 4\. Finite and infinite cores

In database theory, the property of an interpretation or structure being a core is well studied. It is a property that ultimately represents the lack of redundant structures. Therefore, this property is not only nice to have, but particularly relevant in our setting. In fact, we will show that the austere canonical model is a core. Before we get there, we first provide the required theoretical background.

To start, we say an interpretation $I$ is a *core* if each endomorphism of $I$ is an embedding. That is, each homomorphism of $I$ into itself is both strong and injective. The core of a set of atoms $A$ is a set of atoms $B⊆A$, such that (i) there exists an endomorphism *h* from $A$ to $B$, (ii) $B$ is the restriction to the image of *h*, and (iii) $B$ is a core. We write $\mathcal{A} \overset{\mathit{core}}{\rightarrow} \mathcal{B}$. Each finite set of atoms has a core that is unique up to isomorphism.

**Example 4.1**

Recall, which illustrates the results of the oblivious chase and the austere canonical model of some given knowledge base. The oblivious chase model is the following set of facts:$X={PetOwner(linda),Bird(blu),hasWingedPet(linda,blu),hasPet(linda,blu),hasWingedPet(linda,b),hasPet(linda,b),hasPet(linda,c)}$ where *b* and *c* are unknown individuals, i.e., elements of the set *N <sub>B</sub>*, whereas { *linda, blu* }⊆ *N <sub>I</sub>*. Thus, in each homomorphism from *X* to *X*, that is, each endomorphism of *X*, ‘ *linda* ’, and ‘ *blu* ’ must be mapped to themselves, which is not true for *b* and *c*. It is easy to check that *h*: *X*  →  *X* given by $h(linda)=linda$, $h(blu)=blu$, $h(b)=blu$ and $h(c)=blu$ is an homomorphism, but not injective or strong. Thus, *h* is not an embedding and *X* is not a core. Nevertheless, the austere canonical model described in the same, is a core, and also the core of *X*.♥

In the rest of this section, we first show that the austere canonical model is the unique universal core model of a given normalised Horn- $ALCHIQ$ knowledge base $(T,A)$. After that, we discuss the tight connection between the austere canonical model and the core chase.

In the rest of this section, we also allow sets of atoms to be models. This is a shorthand for saying that the canonical interpretation of this set is a model.

### 4.1. Universal core model

To show that $can(T,A)$ is a core, we use the notion *core cover*: an interpretation $I$ has a *core cover* whenever there exist a series of finite interpretations $\mathcal{I}_{1} \subseteq \mathcal{I}_{2} \subseteq \ldots$ with $\mathcal{I} = \cup_{i > 0} \mathcal{I}_{i}$, such that for all $\mathcal{I}_{i}$, each homomorphism $h : \mathcal{I}_{i} \rightarrow \mathcal{I}$ is an embedding. Showing there exists a core cover is enough to show our structure is a core.

**Definition 4.2**

Set $c a n_{n} \left(\mathcal{T} , \mathcal{A}\right)$ for each positive natural number *n* as a *finite approximation* of $can(T,A)$, as follows:
- 1.
	$Δcann(T,A):={x∈Δcan(T,A)∣|x|≤n}$;
- 2.
	$a^{c a n_{n} \left(\mathcal{T} , \mathcal{A}\right)} : = a^{c a n \left(\mathcal{T} , \mathcal{A}\right)}$, for all *a*  ∈  *N <sub>I</sub>*;
- 3.
	$Ccann(T,A):={x∈Ccan(T,A)∣|x|≤n}$, for all *C*  ∈  *N <sub>C</sub>*;
- 4.
	$rcann(T,A):={(x,y)∈rcan(T,A)∣|x|≤n,|y|≤n}$, for all $r \in N_{R}^{+}$.

Note that $\mathit{can}_{n} \left(\mathcal{T} , \mathcal{A}\right)$ is not per se a model of $(T,A)$. However, if the *n* th approximation is a model, then $\mathit{can}_{n} \left(\mathcal{T} , \mathcal{A}\right) = \mathit{can} \left(\mathcal{T} , \mathcal{A}\right)$.

**Example 4.3**

Suppose $A={A(a)}$ and $T={A⊑∃r.A}$. Let $t=({A},{r},{A})$ be a *2* -type. First, notice that $t \in \mathit{child}_{\mathcal{T}} \left(t\right)$. Then the *n* th approximation is a chain of length *n*: $Δcann(T,A)={ati∣i<n}$, $Acann(T,A)={ati∣i<n}$ and $rcann(T,A):={(ati,ati+1)∣i<n−1}$, where *t <sup>i</sup>* denotes the concatenation of *i* times *t*.♥

**Theorem 4.4**

*For each normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *,* $can(T,A)$ *is a core.*

**Proof**

From, Theorem 16, we learn that each interpretation that has a core cover is a core. Thus, it suffices to show that $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$ is a core cover for $\mathcal{I} = \underset{i > 0}{\cup} \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right) = \mathit{can} \left(\mathcal{T} , \mathcal{A}\right) .$It is immediate that for each *i*, the identity mapping $h_{i} : \Delta^{\mathcal{I}_{i}} \rightarrow \Delta^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$ given by *x* ↦ *x* is an embedding.

Consider a fixed *i*. By induction on | *x* | it is shown that for all homomorphisms $h : \Delta^{\mathcal{I}_{i}} \rightarrow \Delta^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$, $h \left(x\right) = h_{i} \left(x\right) = x$ holds.
- •
	$|x|=1$. As by definition, ${x∈ΔIi∣|x|=1}=ΔIi∩NC$, it follows directly that for each homomorphism *h*, $h(x)=x$.
- •
	$|x|≤n+1≤i$. Let us consider some $a k_{1} \ldots k_{n} \in \Delta^{\mathcal{I}_{i}}$. By induction hypothesis, we know that for all homomorphisms *h*, $h \left(a k_{1} \ldots k_{n - 1}\right) = a k_{1} \ldots k_{n - 1}$. As $\left(a k_{1} \ldots k_{n - 1} , a k_{1} \ldots k_{n}\right) \in r^{\mathcal{I}_{i}}$ for all roles *r* in *k <sub>n</sub>*, we also have to ensure $\left(a k_{1} \ldots k_{n - 1} , h \left(a k_{1} \ldots k_{n}\right)\right) \in r^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$, which means that we can already restrict $h(ak1…kn)∈{ak1…kn−2}∪{ak1…kn−1kn′∣kn′∈childT(kn−1)}$ for each possible homomorphism *h*. By (R4) of, we find that $h \left(a k_{1} \ldots k_{n}\right) \neq a k_{1} \ldots k_{n - 2}$. Similarly, (R3) eliminates $h \left(a k_{1} \ldots k_{n}\right) = a k_{1} \ldots k_{n}^{'}$ for all $k_{n}^{'} \neq k_{n}$. So, the only option is $h \left(a k_{1} \ldots k_{n}\right) = a k_{1} \ldots k_{n}$, which concludes the induction step.

Thus, *h <sub>i</sub>* is the only homomorphism $h : \mathcal{I}_{i} \rightarrow \mathit{can} \left(\mathcal{T} , \mathcal{A}\right)$ and the identity mapping is trivially an embedding, which concludes the proof.

The following corollary can be shown with a similar proof.

**Corollary 4.5**

*Every finite approximation* $\mathit{can}_{n} \left(\mathcal{T} , \mathcal{A}\right)$ *of the austere canonical model is a core.*

Next to being a core, the austere canonical model is also the unique core universal model, up to isomorphism, for each normalised Horn- $ALCHIQ$ knowledge base. This is proven in the following theorem.

**Theorem 4.6**

*Each consistent normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *has a unique (up to isomorphism) universal core model, namely the austere canonical model* $can(T,A).$

Before we get into the actual proof, note that the definition of a core was originally solely intended for finite structures. There are multiple ways to define a core for infinite structures that all coincide for finite cases,. One of these approaches, requiring that each endomorphism is an embedding, is the one used up till now in this section. A stronger considered version is to also require each endomorphism to be surjective, that is, requiring that each endomorphism is an isomorphism. To distinguish this case from the core definitions discussed before, we say such an interpretation is a *strong core*. According to Bauslaugh, these stronger cores have the nicest behaviour in the infinite case. However, they might not exist: an infinite chain of blank nodes can be a core and at the same time not a strong core.

In the following proof, we prove that the austere canonical model is also a strong core. Some properties of this stronger definition then help to show that there exists indeed a unique universal core model, up to isomorphism. In line with the definition above, we say an interpretation $I$ has a *strong core cover* if there exist finite interpretations $\mathcal{I}_{1} \subseteq \mathcal{I}_{2} \subseteq \ldots$ with $\mathcal{I} = \cup_{i > 0} \mathcal{I}_{i}$, such that for all $\mathcal{I}_{i}$, each homomorphism $h : \mathcal{I}_{i} \rightarrow \mathcal{I}$ is an isomorphism.

**Proof**

First, note that the proof of Theorem 16 in can easily be extended to also hold in this case: if an instance has a strong core cover then it is a strong core.

From the proof of, it is clear that $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$ is a strong core cover for $can(T,A)$, and thus that $can(T,A)$ is a strong core. Now suppose there exists another universal core model $J$ of the knowledge base $(T,A)$. Because both models are universal, there exists homomorphisms in both directions. Since each endomorphism of $can(T,A)$ must be bijective and strong, and each one of $J$ injective and strong, it is straightforward to conclude that the homomorphism mapping $J$ to $can(T,A)$ must be bijective and strong too: $J$ and $can(T,A)$ are indeed isomorphic, as required.

**Corollary 4.7**

*Each consistent normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *has a unique universal strong core model, namely* $can(T,A)$ *.*

### 4.2. Core chase

The core chase is a method that is complete for finding the unique (up to isomorphism) *finite* universal core model, whenever it exists. We specifically note that the core chase never produces an *infinite* structure, that is, it is only relevant to compare the austere canonical model to the result of the core chase in case the core chase terminates and produces a finite universal core model. In fact, we will see that in that case, the results coincide. Following this same paper, we will now briefly introduce the core chase. Recall we may view any set of atoms $A$ as an interpretation with domain $\Delta^{\mathcal{A}}$. As chase procedures are often seen as series of sets of atoms, this assumption makes the following definitions more in line with the literature on chase procedures.

The core chase is constructed by alternating the application of two operations: firing all not-yet satisfied axioms and taking the core of the resulting structure. This procedure is repeated until it terminates, producing a series of sets of atoms where the last set is defined to be the result of the core chase. If the series does not terminate, the core chase is undefined.

We start by formalising the first operation. For this, we consider a function that fires the right-hand side of axioms: the function *f <sub>x</sub>*, defined for each *x*  ∈  *N <sub>I</sub>*  ∪  *N <sub>B</sub>*. This function translates a concept into a set of atoms, and is inductively defined in the following way: *f <sub>x</sub>* (⊤) ≔ ∅, *f <sub>x</sub>* (*A*) ≔ { *A* (*x*)}, $fx(∃(r0⊓…⊓rn).C):={r0(x,y),r0−(y,x),…,rn(x,y),rn−(y,x)}∪fy(C)$ for some fresh variable *y* and *f <sub>x</sub>* (*C* ⊓ *C* ′) ≔  *f <sub>x</sub>* (*C*) ∪  *f <sub>x</sub>* (*C* ′).

To determine which axioms we want to fire, we define a set of matches $m(T,A)$ containing pairs of one or two nodes in *N <sub>I</sub>*  ∪  *N <sub>B</sub>* and a Horn- $ALCHIQ$ axiom. We say $(c,C⊑D)∈m(T,A)$ iff there exists an axiom $C⊑D∈T$ and a homomorphism *h* from *f <sub>x</sub>* (*C*) to $A$, such that $h(x)=c$ and there is no homomorphism from *f <sub>x</sub>* (*D*) to $A$ such that $h(x)=c$. Similarly, we say $\left(\left(c , d\right) , r \sqsubseteq r^{'}\right) \in \mathit{m} \left(\mathcal{T} , \mathcal{A}\right)$ iff there exists an axiom $r \sqsubseteq r^{'} \in \mathcal{T}$ such that $r(c,d)∈A$ and $r^{'} \left(c , d\right) \notin \mathcal{A}$. No other elements are contained in $m(T,A)$.

Combining the above, we can fully define the first operation: for an normalised Horn- $ALCHIQ$ TBox $T$ and ABoxes $\mathcal{A} , \mathcal{A}^{'}$, we let $\mathcal{A} \overset{\mathcal{T}}{\rightarrow} \mathcal{A}^{'}$ iff $\begin{matrix}\mathcal{A}^{'} = \mathcal{A} \cup \underset{\left(c , C \sqsubseteq D\right) \in \mathit{m} \left(\mathcal{T} , \mathcal{A}\right)}{\cup} f_{c} \left(D\right) \cup \underset{\left(\left(c , d\right) , r \sqsubseteq r^{'}\right) \in \mathit{m} \left(\mathcal{T} , \mathcal{A}\right)}{\cup} r^{'} \left(c , d\right) .\end{matrix}$If there exists an axiom of the form *A* ⊑ ≥  <sub>1</sub> *r.B* in $T$, such that { *A* (*x*), *r* (*x, y*), *B* (*y*), *r* (*x, z*), *B* (*z*)} would be contained in $\mathcal{A}^{'}$ for some { *x, y, z* }⊆ *N <sub>I</sub>*  ∪  *N <sub>B</sub>*, a simple substitution of all *y* ’s by *z* ’s is performed to get the final $\mathcal{A}^{'}$, assuming $y \notin N_{I}$.

Furthermore, for any binary relation  →, we use the notation $\mathcal{A} \left(\rightarrow\right)^{\omega} \mathcal{A}^{'}$ to denote that there exists a natural number *n* such that $\mathcal{A} \left(\rightarrow\right)^{n} \mathcal{A}^{'}$ and for all $\mathcal{A}^{''}$ such that $\mathcal{A}^{'} \rightarrow \mathcal{A}^{''}$ we find $\mathcal{A}^{'} = \mathcal{A}^{''}$. With ∘ we denote the concatenation of two binary relations, that is, $\mathcal{A} \rightarrow \circ \rightarrow^{'} \mathcal{B}$ iff there exists $\mathcal{A}^{'}$ such that $\mathcal{A} \rightarrow \mathcal{A}^{'}$ and $\mathcal{A}^{'} \rightarrow^{'} \mathcal{B}$, for each pair of binary relations  →  and  → ′. Recall we write $\mathcal{A} \overset{\mathit{core}}{\rightarrow} \mathcal{B}$ in case $B$ is the core of $A$.

**Definition 4.8**

## \[26\]

Given a normalised Horn- $ALCHIQ$ knowledge base $(T,A)$, the *core chase* is the unique, up to isomorphism, set of atoms $B$ such that $\mathcal{A} \left(\overset{\mathcal{T}}{\rightarrow} \circ \overset{\mathit{core}}{\rightarrow}\right)^{\omega} \mathcal{B}$.

Clearly, this series is not guaranteed to be finite, see for instance the following example.

**Example 4.9**

Suppose $A={A(a)}$ and $T={A⊑∃r.A}$. Then $A(→T∘→core)n{A(a),r(a,a1),A(a1),r(a1,a2),A(a2),…,r(an−1,an),A(an)}$ for each natural number *n*.♥

As mentioned before, in non-terminating cases, the core chase does not produce a result. Simply taking the union of the sets in the core chase construction is in any case not a good idea. More on this topic is discussed in, combined with a proposal on how to generalise the core chase construction to an infinite setting: the stable chase. A drawback of this approach is that the result of the stable chase in general misses the universality property. It is unclear whether the stable chase for description logics might result in an non-universal model too. In case the result of the stable chase for normalised Horn- $ALCHIQ$ is indeed universal, this result coincides with the austere canonical model, up to isomorphism, which can be shown in a similar fashion as.

To conclude, drawbacks of the core chase construction are that it is unclear whether the core chase terminates and produces a result. Furthermore, the process of performing the core chase construction itself is expensive, as taking the core of a structure is expensive and happens regularly. The good news is that for normalised Horn- $ALCHIQ$, the austere canonical model coincides with the result of the core chase, if existent. This means the above troubles are resolved: the austere canonical model is always defined and is constructed without having to take cores of structures.

**Theorem 4.10**

*Given a normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *such that* $can(T,A)$ *is finite, and let* $B$ *be the unique, up to isomorphism, structure such that* $\mathcal{A} \left(\overset{\mathcal{T}}{\rightarrow} \circ \overset{\mathit{core}}{\rightarrow}\right)^{\omega} \mathcal{B}$ *, then* $B≅can(T,A).$

**Proof**

We note that $B$ is a core by definition, and the same holds for $can(T,A)$ by. Since both are cores, it suffices to show that there exists homomorphisms in both directions.

Note that $can(T,A)$ is a model by. As $B$ is a universal model, it follows that there exists a homomorphism from $B$ into each model, including $can(T,A)$. By we also have that $can(T,A)$ is universal, which means also the other required homomorphism must exist.

## 5\. Recursive SHACL

In the third section, we described non-recursive SHACL validation in presence of ontologies. We will continue the rest of the paper considering a fragment of SHACL that allows recursion: *stratified SHACL*. There is no unique way to extend the simple semantics we discussed before to the recursive case, and some alternatives have been explored in the literature, like the stable model semantics, the supported model semantics and the well-founded semantics. The semantics we will discuss here is the *least fixed point* semantics. We note it coincides with the stable model semantics and the well-founded semantics on each set of stratified constraints.

As discussed, recursive SHACL allows shape names in the definition of shape constraints. To this end, let *N <sub>S</sub>* denote a countably infinite set of *shape names* that is disjoint from *N <sub>C</sub>*  ∪  *N <sub>R</sub>*  ∪  *N <sub>I</sub>*  ∪  *N <sub>B</sub>*. A *shape constraint* is an expression of the form *s*  ← φ, where *s*  ∈  *N <sub>S</sub>* and φ a shape expression defined like in the preliminaries, with the addition of allowing referencing shape names *s* within φ. We call *s* the *head* of a constraint *s*  ← φ. Note that we allow *s* to appear as the head of multiple constraints. In the rest of this article, we impose some additional restrictions and consider only a fragment of recursive SHACL. We leave the generalisation of our results to full recursive SHACL for future work.

That is, let φ be defined in the following way $\begin{matrix}\varphi : : = c \mid s \mid \neg s \mid A \mid \varphi \lor \varphi \mid \varphi \land \varphi \mid \exists \left(\sqcap R\right) . \varphi \mid \exists E . \varphi \mid c \land \mathsf{eq} \left(E , E^{'}\right) \mid c \land \mathsf{disj} \left(E , E^{'}\right) ,\end{matrix}$where *c*  ∈  *N <sub>I</sub>, s*  ∈  *N <sub>S</sub>*, $A∈N‾C$, $R⊆N‾R$, and *E* and *E* ′ regular expressions over the alphabet $N‾R$.

First, note that our versions of path equality and disjointness, $c \land \mathsf{eq} \left(E , E^{'}\right)$ and $c \land \mathsf{disj} \left(E , E^{'}\right)$, distinguish themselves from the version in the preliminaries and the SHACL standard in two ways. First, the standard requires $E′∈N‾R$. We generalise this and allow *E* ′ to be any regular expression. Secondly, for technical reasons, we add a ‘guard’ in the form of an individual *c*  ∈  *N <sub>I</sub>*. Furthermore, this fragment lacks counting over regular path expressions and closure constraints. We note that our results do not simply extend to the setting without these restrictions; especially counting over regular paths is a feature that requires a lot of attention, and that no results for the unrestricted setting are known in the literature. We refer the reader to for a more extensive discussion. Lastly, we increase the expressivity of SHACL slightly by adding conjunction of roles in the form ∃ *R*.φ, for *R* a conjunction of roles in $N‾R$, which we use to reduce Horn- $ALCHIQ$ -reasoning combined with SHACL to plain SHACL reasoning.

The semantics of recursive SHACL is defined in terms of a *shape assignment.* A shape assignment is a set of shape atoms *S*, such that the rules specified in are satisfied, taken into account that $s←φ∈C$ implies that $\left(\varphi\right)^{\mathcal{I} , S} \subseteq s^{\mathcal{I} , S}$. As mentioned before, there is no agreement on a unique semantics for recursive SHACL in the literature. Nevertheless, what all semantics have in common is that the shape assignment *S*, a set of *shape atoms*, of the form *s* (*c*), for *s*  ∈  *N <sub>S</sub>* and *c*  ∈  *N <sub>I</sub>*, satisfies this same set of rules.

![Fig. 4](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr4.jpg)

Download: Download high-res image (220KB)

In the recursive setting, the form of targets is changed: we now consider a set of shape atoms *s* (*c*). We will discuss this further in. As we are considering shape atoms, we also need constraints providing meaning to the shape names. Thus, the notion of targets is replaced by *shape graphs*. A shape graph is a pair $(C,G)$, where $C$ is a set of shape constraints and $G$ is a set of shape atoms.

### 5.1. Stratified SHACL

In this article, we are interested in shape assignments where each shape atom has a proper justification. That is, we do not wish to consider any set of shape atoms *S*, but put some constraints on the type of shape assignments we accept. One option would be to resort to the full stable model semantics, but only if we want to give up on polynomial time data complexity. Thus, we focus on a more straight-forward semantics, based on *stratified* sets of constraints. This is a fragment of recursive SHACL which supports negation to a certain extend, but restricts the full combination of recursion and negation. To this end and following the logic programming literature, a partition of constraints (stratification) is defined such that a justified shape assignment can be constructed by processing each partition individually.

**Definition 5.1**

We say a shape name *s occurs negatively* in a shape constraint *s* ′ ← φ if ¬ *s* occurs in φ. We say a shape name *s* is *defined* in a set $C$ of constraints if $s←φ∈C$ for some φ.

A set $C$ of constraints is *stratified* if it can be partitioned into sets $\mathcal{C}_{0} , \ldots , \mathcal{C}_{k}$, called *strata*, such that, for all 0 ≤  *i*  ≤  *k*, the following hold.
- 1.
	If *i*  <  *k* and *s* ′ occurs in φ for some $s \leftarrow \varphi \in \mathcal{C}_{i}$, then *s* ′ is not defined in $\mathcal{C}_{i + 1} \cup \ldots \cup \mathcal{C}_{k}$.
- 2.
	If *s* ′ occurs negatively in φ for some $s \leftarrow \varphi \in \mathcal{C}_{i}$, then *s* ′ is not defined in $\mathcal{C}_{i} \cup \ldots \cup \mathcal{C}_{k}$.

A set of constraints is *stratified* if it admits a stratification.

Without loss of generality, we can assume that all constraints with the same head are defined in the same stratum.

A standard way to obtain a stratification is to define a dependency graph (*V, E, E* \*) with the set of shape names used as the nodes *V*. In this graph, there are two types of edges: marked edges *E* \* and standard edges *E*, such that *E* \*⊆ *E*. We use the standard edges to mark that *s* occurs in a shape constraint with head *s* ′. In that case, we set (*s, s* ′) ∈  *E*. If this is not just any occurrence, but *s* occurs *negatively* in a shape constraint with head *s* ′, then we also set (*s, s* ′) ∈  *E* \*. The lowest stratum is the biggest set of nodes *X* such that if *s*  ∈  *X* and (*s* ′, *s*) ∈  *E*, then *s* ′ ∈  *X* and for all *s*  ∈  *X*, there does not exist any *s* ′ ∈  *V* such that (*s* ′, *s*) ∈  *E* \*. To find the next lowest stratum, simply remove all shape names in *X* from the dependency graph and repeat the above. This may be repeated until all shape names are assigned a stratum.

Given any stratification of a set of constraints, we compute the shape assignment of stratified SHACL with a least fixed point operator over each stratum, with negation as failure to compute the opposite in an earlier stratum. To do so, we first define the notion of an immediate consequence operator $T_{\mathcal{I} , \mathcal{C}}$ that, given a shape assignment *S*, adds new shape atoms to satisfy the constraints that are fired by the constraints in $C$ based on *S* and $I$.

**Definition 5.2**

Given a set of constraints $C$ and an interpretation $I$ with *N <sub>I</sub>* ⊆Δ <sup><em>I</em></sup>, we define an immediate consequence operator $T_{\mathcal{I} , \mathcal{C}}$ that maps shape assignments to shape assignments as follows:$TI,C(S):=S∪{s(a)∣s←φ∈C,a∈(φ)I,S}.$

The following two propositions are a direct consequence of the characterisations from in the context of stratified logic programs. Here, we will again use the definition of the least fixed point starting from a given set. We refer the reader back to for the precise definition.

**Proposition 5.3**

*If* $C$ *is a constraint set that does not define any shape names that occur negatively in* $C$ *, then the following hold:*
- 1.
	$T_{\mathcal{I} , \mathcal{C}}$ *is monotonic, i.e. if S* ⊆ *S* ′*, then* $T_{\mathcal{I} , \mathcal{C}} \left(S\right) \subseteq T_{\mathcal{I} , \mathcal{C}} \left(S^{'}\right)$ *;*
- 2.
	$T_{\mathcal{I} , \mathcal{C}}$ *is finitary, i.e.* $T_{\mathcal{I} , \mathcal{C}} \left(\cup_{n = 0}^{\infty} S_{n}\right) \subseteq \cup_{n = 0}^{\infty} T_{\mathcal{I} , \mathcal{C}} \left(S_{n}\right)$ *for all infinite sequences* $S_{0} \subseteq S_{1} \subseteq \hdots$ *;*
- 3.
	$T_{\mathcal{I} , \mathcal{C}}$ *is growing, i.e.* $T_{\mathcal{I} , \mathcal{C}} \left(S_{2}\right) \subseteq T_{\mathcal{I} , \mathcal{C}} \left(S_{3}\right)$ *for all S* <sub>1</sub>, *S* <sub>2</sub>, *S* <sub>3</sub> *such that* $S_{1} \subseteq S_{2} \subseteq S_{3} \subseteq T_{\mathcal{I} , \mathcal{C}} \uparrow^{\omega} \left(S_{1}\right)$ *.*

**Proposition 5.4**

*If* $I$ *is an interpretation and* $\mathcal{C}_{0} , \ldots , \mathcal{C}_{k}$ *is a stratification of* $C$ *, then each* $T_{\mathcal{I} , \mathcal{C}_{0}} , \hdots , T_{\mathcal{I} , \mathcal{C}_{k}}$ *is monotone, finitary, and growing. Thus, for any shape assignment S and each* 0 ≤  *j*  ≤  *k,* $T_{\mathcal{I} , \mathcal{C}_{j}} \uparrow^{\omega} \left(S\right)$ *is a fixpoint of* $T_{\mathcal{I} , \mathcal{C}_{j}}$ *.*

Based on the above, we can now define the computation of the desired shape assignment along a stratification $\mathcal{C}_{0} , \ldots , \mathcal{C}_{k}$ of $C$.

**Definition 5.5**

Assume $I$ is an interpretation, $C$ is a stratified set of constraints, and let $\mathcal{C}_{0} , \ldots , \mathcal{C}_{k}$ be a stratification of $C$. Then let $\begin{aligned}M_{0} : = & T_{\mathcal{I} , \mathcal{C}_{0}} \uparrow^{\omega} \left(\emptyset\right) \\ M_{i} : = & T_{\mathcal{I} , \mathcal{C}_{i}} \uparrow^{\omega} \left(M_{i - 1}\right) \text{for} \text{each} 1 \leq i < k .\end{aligned}$We call *M <sub>k</sub>* be the *perfect assignment* for $C$ and $I$, and use the notation $\mathit{PA} \left(\mathcal{C} , \mathcal{I}\right) : = M_{k}$. An interpretation $I$ (resp., ABox $A$) *validates* a shapes graph $(C,G)$ if $G⊆PA(C,I)$ (resp., $\mathcal{G} \subseteq \mathit{PA} \left(\mathcal{C} , \mathcal{I}_{\mathcal{A}}\right)$).

A well-known result is that the particular stratification chosen does not matter: any stratification will give the same perfect assignment. Given this semantics, it is now straightforward to extend to recursive SHACL and shapes graphs.

**Definition 5.6**

Given a normalised Horn- $ALCHIQ$ TBox $T$ and ABox $A$, and a shapes graph $(C,G)$, we say $(T,A)$ validates $(C,G)$ if $can(T,A)$ validates $(C,G)$.

### 5.2. Normal form

A nice feature of the SHACL fragment introduced at the start of this section, is that it has a rather succinct normal form with the same expressivity. In the rest of the paper, we will assume that all the given sets of constraints are in normal form. This will be particularly useful in the following two sections, restricting the shapes of constraints we need to consider.

**Definition 5.7**

A SHACL constraint is in *normal form* if it has one of the following forms $\begin{aligned}(\text{NC1}) s \leftarrow c & (\text{NC4}) s \leftarrow s^{'} \land s^{''} \\ (\text{NC2}) s \leftarrow s^{'} & (\text{NC5}) s \leftarrow \exists \left(\sqcap R\right) . s^{'} \\ (\text{NC3}) s \leftarrow A & (\text{NC6}) s \leftarrow \neg s^{'} ,\end{aligned}$where *c*  ∈  *N <sub>I</sub>*, $R⊆N‾R$, { *s, s* ′, *s* ″}⊆ *N <sub>S</sub>* and $A∈N‾C$.

We use the term *negative constraints* to refer to constraints of the form (NC6) and *positive constraints* for constraints of the form (NC1)–(NC5). Clearly, each set of positive constraints is automatically stratified. Furthermore, for simplicity, if $R={r}$, we may write *s*  ← ∃ *r.s* ′ instead of *s*  ← ∃(⊓ *R*).*s* ′.

We can indeed rewrite parts of SHACL into this restricted, normalised, form of SHACL, as formalised below.

**Proposition 5.8**

*Each set of constraints* $C$ *can be translated in time polynomial in* $|C|$ *, into a set of constraints* $\mathcal{C}^{'}$ *in normal form such that for all* $G$ *and each normalised Horn-* $ALCHIQ$ *knowledge base* $(T,A)$ *, we have* $(T,A)$ *validates* $(C,G)$ *iff* $(T,A)$ *validates* $\left(\mathcal{C}^{'} , \mathcal{G}\right)$ *.*

In particular, the above statement holds for $T=∅$, that is, the standard case of SHACL validation, without ontologies. Furthermore, normalising a set of constraints in the way described below does not influence it being stratified or not.

**Proof**

We extend the results for normal forms of and. That is, we first recursively introduce fresh shapes for sub-expressions that appear in constraints, as in.

Next to that, we also allow shape names to appear as heads in multiple constraints, which means that *s*  ← φ∨φ′ can be replaced by *s*  ← φ and *s*  ← φ′ without affecting validation. Now, what is left to show is that also constraints of the form $s \leftarrow c \land \mathsf{eq} \left(E , E^{'}\right)$, $s \leftarrow c \land \mathsf{disj} \left(E , E^{'}\right)$ and *s*  ← ∃ *E.s* ′ can be translated into constraints in normal form in polynomial time. The last case, *s*  ← ∃ *E.s* ′, we already covered in, but is repeated here for completeness.
- •
	*s*  ← ∃ *E.s* ′. Suppose $\mathcal{M} = \left(Q , \Sigma , q_{I} , \Delta , q_{F}\right)$ is the automaton recognising *E*. Take fresh shape names *s <sub>q</sub>* for each *q*  ∈  *Q* and add the following constraints
	| $s \leftarrow s_{q_{I}}$ |  |
	| --- | --- |
	| $s_{q} \leftarrow \exists r . s_{q}^{'}$ | if $\left(q , r , q^{'}\right) \in \Delta$ |
	| $s_{q_{F}} \leftarrow s^{'}$. |  |
	Here, the idea is to encode the states of the automaton in the set of shape names. However, we do not consider them in the standard initial state towards final state mode, but the other way around. In the end, the idea is that we let every state that is an *s* ′ be a final state, and see whether we can work our way back through the automaton to an initial state. Thus, we find that a node is assigned $s_{q_{I}}$ iff that node has an *E* -path to a node that is an *s* ′.
- •
	$s \leftarrow c \land \mathsf{eq} \left(E , E^{'}\right)$. Suppose $\mathcal{M} = \left(Q , \Sigma , q_{I} , \Delta , q_{F}\right)$ and $\mathcal{M}^{'} = \left(Q^{'} , \Sigma , q_{I}^{'} , \Delta^{'} , q_{F}^{'}\right)$ are the automata recognising *E* and *E* ′ respectively, such that $Q \cap Q^{'} = \emptyset$. Take fresh shape names *s <sub>error</sub>, s <sub>noerror</sub> s <sub>pos</sub>, s <sub>neg</sub>*, and *s <sub>q</sub>* for each *q*  ∈  *Q*  ∪  *Q* ′ and add the following constraints
	| $s_{q} \leftarrow c$ | if $sq∈{sqI,sqI′}$ |
	| --- | --- |
	| $s_{q^{'}} \leftarrow \exists r^{-} . s_{q}$ | if $\left(q , r , q^{'}\right) \in \Delta \cup \Delta^{'}$ |
	| $s_{\mathit{pos}} \leftarrow s_{q}$ | if $sq∈{sqF,sqF′}$ |
	| $s_{\mathit{neg}} \leftarrow \neg s_{q}$ | if $sq∈{sqF,sqF′}$ |
	| $s_{\mathit{error}} \leftarrow s_{\mathit{pos}} \land s_{\mathit{neg}}$ |  |
	| $s_{\mathit{error}} \leftarrow \exists r . s_{\mathit{error}}$ | if $r∈Σ$ |
	| $s_{\mathit{noerror}} \leftarrow \neg s_{\mathit{error}}$ |  |
	| $s \leftarrow s_{q} \land s_{\mathit{noerror}}$. |  |
	In this case, because of the ‘guard’ *c*, there is only one node considered to be the initial state of both automata. From there, we assign the states using their encoding in shape names. This time, we consider the states of the automaton from initial state towards, possibly, a final state somewhere. After finishing assigning states, it is decided which nodes are the final state of any of the two automata. The last thing to do is to see whether there exists a node that is the final state of one of the two automata (thus being assigned *s <sub>pos</sub>*), but not of the other automaton (thus also being assigned *s <sub>neg</sub>*). The last thing to do is to bring this information back towards *c*, with the constraints *s <sub>error</sub>*  ← ∃ *r.s <sub>error</sub>* for each *r* appearing in the automata.
- •
	$s \leftarrow c \land \mathsf{disj} \left(E , E^{'}\right)$. Similar solution as $s \leftarrow c \land \mathsf{eq} \left(E , E^{'}\right)$, but define the error shape *s <sub>error</sub>* as $s_{\mathit{error}} \leftarrow s_{q_{F}} \land s_{q_{F}^{'}}$.

Note that the automata can be constructed in polynomial time, which is a standard result in the literature, see for instance.

## 6\. Rewriting for positive SHACL

Now we will return to problem of SHACL validation in presence of ontologies. In, we defined the semantics of SHACL in presence of ontologies as SHACL validation over the core universal model. This was independent of the chosen semantics for SHACL. As we decided on the least fixed point semantics for SHACL in the previous section, it is now clear what the intended meaning is of a knowledge base validating a shapes graph.

However, we also care about computability. To this end, we do not wish to materialise the full, possibly infinite, core universal model. Instead, we will bring SHACL validation over the core universal model back to SHACL validation over the enriched ABox $\mathcal{A}_{\mathcal{T}}$, as defined in, by rewriting the set of constraints. More precisely, given a TBox $T$ and a set of stratified constraints $C$, we want to compile $T$ and $C$ into a new set $\mathcal{C}_{\mathcal{T}}$ of stratified constraints so that for every ABox $A$ consistent with $T$, and every target $G$, we have $\left(\mathcal{T} , \mathcal{A}\right) \text{validates} \left(\mathcal{C} , \mathcal{G}\right) \text{iff} \mathcal{A}_{\mathcal{T}} \text{validates} \left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right) .$This will be achieved by means of an inference procedure that uses a collection of inference rules to capture the possible “propagation” of shape names in the anonymous part of the austere canonical model. In the following, the rewriting procedure for SHACL without any occurrence of negation is discussed, followed by the general case of recursive SHACL.

### 6.1. Rewriting algorithm

The idea of the rewriting is that we can encode all reasoning of axioms in the constraints. The core of our technique is an inference procedure that derives a set of quadruples (*t, P, Q, H*), where *t* a *2* -type, as introduced at the start of. Intuitively, deriving (*t, P, Q, H*) tells us that an object that satisfies all concept names in *π* <sub>1</sub> (*t*), that satisfies all expressions (assumptions) in *P*, and does not satisfy every single expression in *Q*, must validate all shape names in *H*. Note that there may be some overlap in the information stored in *t* and *P*.

**Definition 6.1**

Let ⊤, *c*, ∃ *r.s*, be *basic shape expressions*, for $r∈N‾R$, *s*  ∈  *N <sub>S</sub>*, and *c*  ∈  *N <sub>I</sub>*. Moreover, let ∃(⊓ *R*).⊓ *N* be called a *basic concept expression*, for each $R⊆N‾R$ and *N* ⊆ *N <sub>C</sub>*.

Syntactically, *P* and *Q* are sets of basic shape and basic concept expressions, whereas the set *H* may only contain shape names in *N <sub>S</sub>*.

**Definition 6.2**

A *2* -type *t* is called *locally consistent* if the following are satisfied.
- •
	If $\mathcal{T} \models A_{1} \sqcap \ldots \sqcap A_{n} \sqsubseteq B$ and ${A1,…,An}⊆πi(t)$, then *B*  ∈  *π <sub>i</sub>* (*t*), for *i*  ∈ {1, 3}.
- •
	If $\mathcal{T} \models \sqcap R \sqsubseteq r^{'}$ and *R* ⊆ *π* <sub>2</sub> (*t*), then *r* ′ ∈  *π* <sub>2</sub> (*t*).
- •
	If $A⊑∀r.B∈T$, *A*  ∈  *π* <sub>1</sub> (*t*) and *r*  ∈  *π* <sub>2</sub> (*t*), then *B*  ∈  *π* <sub>3</sub> (*t*).
- •
	If $A⊑∀r.B∈T$, *A*  ∈  *π* <sub>3</sub> (*t*) and $r^{-} \in \pi_{2} \left(t\right)$, then *B*  ∈  *π* <sub>1</sub> (*t*).

Recall that we are only considering consistent knowledge bases. As discussed in the preliminaries, this means we may ignore all axioms containing ‘⊥’ in the universal model construction. On the same note, there is also no need to consider those axioms in the following rewriting procedure.

**Definition 6.3**

Given a normalised Horn- $ALCHIQ$ TBox $T$ and $C$ a set of normalised constraints, let $N_{C}^{\mathcal{T}} \subseteq N_{C}$ be the (finite) set of concepts occurring in $T$ or $C$. We let $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$ be the smallest set of quadruples (*t, P, Q, H*) that is closed under the following rules.
- 1.
	If *t* is a locally consistent *2* -type, and *Q* is a set of basic shape expressions such that for all ∃(⊓ *R*).(⊓ *N*) ∈  *Q*, we have $\left(R , N\right) \in \mathit{succ}_{\mathcal{T}} \left(t\right)$ and not both *R* ⊆ *π* <sub>2</sub> (*t*) and *N* ⊆ *π* <sub>3</sub> (*t*), then $\left(t , \bar{Q} , Q , \emptyset\right)$ belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$, where $Q¯:={⊤}∪{∃(⊓R).(⊓N)∣(R,N)∈succT((π1(t),∅,∅)),∃(⊓R).(⊓N)∉Q}.$
- 2.
	If ${(t,P,Q,H),(t,P′,Q′,H′)}⊆psatC,T$ such that ∃(⊓ *R*).(⊓ *N*) ∈  *Q* iff ∃(⊓ *R*).(⊓ *N*) ∈  *Q* ′, then (*t, P*  ∪  *P* ′, *Q*  ∪  *Q* ′, *H*  ∪  *H* ′) belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$.
- 3.
	If $s←S∈C$ for some basic shape expression *S* and $\left(t , P , Q , H\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$, then (*t, P*  ∪ ({ *S* }∖ *N <sub>C</sub>*), *Q, H*  ∪ { *s* }) belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$ if either
	- •
		$S=c$, for *c*  ∈  *N <sub>I</sub>* and $c∉Q$; or
	- •
		$S=A$, for *A*  ∈  *π* <sub>1</sub> (*t*); or
	- •
		$S = \exists r . s^{'}$ and *r*  ∈  *π* <sub>2</sub> (*t*) or there exists ∃(⊓ *R*).(⊓ *N*) ∈  *P* such that *r*  ∈  *R* and $\exists r . s^{'} \notin Q$.
- 4.
	If $s \leftarrow s^{'} \in \mathcal{C}$, $\left(t , P , Q , H\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ and { *s* ′}⊆ *H*, then (*t, P, Q, H*  ∪ { *s* }) belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$.
- 5.
	If $s \leftarrow s_{1} \land s_{2} \in \mathcal{C}$, $\left(t , P , Q , H\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ and { *s* <sub>1</sub>, *s* <sub>2</sub> }⊆ *H*, then (*t, P, Q, H*  ∪ { *s* }) belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$.
- 6.
	If $s \leftarrow \exists \left(\sqcap R\right) . s^{'} \in \mathcal{C}$, ${(t,P,Q,H),(t′,P′,Q′,H′)}⊆psatC,T$, $R^{-} \subseteq \pi_{2} \left(t^{'}\right)$, $P^{'} \cap N_{I} = \emptyset$, *s* ′ ∈  *H* ′ and $\mathit{inv} \left(t^{'}\right) \in \mathit{child}_{\mathcal{T}} \left(\mathit{inv} \left(t\right)\right)$ such that
	- •
		∃(⊓ *R* ′).(⊓ *N* ′) ∈  *P* ′ iff $\left(R^{'} , N^{'}\right) \in \mathit{succ}_{\mathcal{T}} \left(\left(\pi_{1} \left(t^{'}\right) , \emptyset , \emptyset\right)\right) \backslash \mathit{succ}_{\mathcal{T}} \left(t^{'}\right)$; and
	- •
		{ *s* ″∣∃ *r* ″.*s* ″ ∈  *P* ′}⊆ *H*,
	then (*t, P, Q, H*  ∪ { *s* }) belongs to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$.

In this definition, Rule 1 ensures that for each possible node in a data graph, there is a quadruple describing the *1* -type of that node in *π* <sub>1</sub> (*t*), restricted to the concept names occurring in $T$. Furthermore, the set of neighbours this *1* -type needs to have in all models is partitioned into a set of neighbours we observe (*P*), and which will be introduced as children of this *1* -type (*Q*). Because of this, we may consider the first three entries of the quadruple as a description of a small part of a model, containing all information about its type and neighbours that might be relevant. In this way, it contains enough information to mimic the least fixed point operator for shape names step by step by Rules 3–6. Note that because we are considering the *2* -type from the ‘perspective’ of the node, that is, ‘looking back towards the data’, we have to consider their inverses when checking the child-relationship in Rule 6. Lastly, Rule 1 is not necessary, but eases the completeness proof. We note that the same set of rules will be reused for the rewriting of stratified SHACL. Because of this, certain conditions do not have a purpose yet, like $c∉Q$ in Rule 3, which will always be met in the current positive setting.

**Definition 6.4** Rewriting Procedure

Consider a normalised Horn- $ALCHIQ$ TBox $T$, $C$ a set of normalised constraints and *K* a set of quadruples (*t, P, Q, H*). Let $\mathcal{C}_{\mathcal{T} , K}$ be the set of constraints that contains $C$, and moreover, for each (*t, P, Q, H*) ∈  *K* and each *s*  ∈  *H*, the constraint(1) $\begin{matrix}s \leftarrow \underset{A \in \pi_{1} \left(t\right)}{\wedge} A \land \underset{A \in N_{C}^{\mathcal{T}} \backslash \pi_{1} \left(t\right)}{\wedge} \neg A \land \underset{X \in P}{\wedge} X \land \underset{Y \in Q}{\wedge} \neg Y .\end{matrix}$

Note that only *π* <sub>1</sub> (*t*) and not the full *2* -type is taken into account when transforming a triple into a constraint. This suffices as we are considering axioms in normal form. Thus, knowing exactly which concept names are true in a node implies knowing exactly which structures may appear in the anonymous tree structure with this node as its root. The next step is eliminating the superfluous substructures of this anonymous tree, similar to what can be expected in any core universal model construction. This boils down to knowing exactly which of the substructures of depth at most 1 are already present in the enriched ABox $\mathcal{A}_{\mathcal{T}}$. Dividing all relevant substructures in the positive or negative set *P* and *Q* happens in Rule 1. As *P* is subsuming the information stemming from *π* <sub>2</sub> (*t*) and *π* <sub>3</sub> (*t*), it does not have to be repeated in.

**Example 6.5**

Suppose $T={A⊑∃p.B,B⊑∃q.C}$ and consider the following constraints $C$:$\begin{matrix}s \leftarrow \exists p . s s \leftarrow \exists q . s s \leftarrow s^{'} \land s^{''} s^{'} \leftarrow \exists p^{-} . s^{'} s^{'} \leftarrow \exists q^{-} . s^{'} s^{'} \leftarrow A s^{''} \leftarrow C .\end{matrix}$Let $t=({A},{p},{B})$ and $t′=({B},{q},{C})$ and recall the definition of the inverse of a *2* -type: $inv(t)=({B},{p−},{A})$. Note that both *inv* (*t*), *inv* (*t* ′) and *t <sub>A</sub>*  ≔ ({ *A* }, ∅, ∅) are locally consistent *2* -types. Thus, according to the Rule 1 of, the following quadruples belong to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$:$(tA,{⊤},{∃p.B},∅),(inv(t),{⊤},{∃q.C},∅),(inv(t′),{⊤},∅,∅).$Given these quadruples and following Rule 3 (of ) multiple times, we can also derive the following quadruples:$(tA,{⊤},{∃p.B},{s′}),(inv(t),{⊤,∃p−.s′},{∃q.C},{s′}),(inv(t′),{⊤,∃q−.s′},∅,{s′,s″}).$That is, in the first quadruple, *s* ′ is added as a conclusion as *A* is contained in *π* <sub>1</sub> (*t <sub>A</sub>*). For the second quadruple, we add $\exists p^{-} . s^{'}$ to the set of positive assumptions, thus also describing an environment in which *s* ′ can be concluded. To see that the third quadruple is contained in $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$, Rule 3 is applied twice: once because *C* is contained in *π* <sub>1</sub> (*inv* (*t* ′)), and once because of the addition $\exists q^{-} . s^{'}$ to the positive assumptions. The last quadruple may be updated to $(inv(t′),{⊤,∃q−.s′},∅,{s,s′,s″})$ because of *s*  ←  *s* ′∧ *s* ″. Now Rule 6 can be used based on *s*  ← ∃ *q.s*, $(inv(t),{⊤,∃p−.s′},{∃q.C},{s′})$ and the quadruple $(inv(t′),{⊤,∃q−.s′},∅,{s,s′,s″})$ to infer that $(inv(t),{⊤,∃p−.s′},{∃q.C},{s,s′})$ must belong to $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$ too. That is, we compare the environments described by these two quadruples: the main idea is that we want to derive *s* in the first quadruple because of a *q* connecting the first environment to the second one (reflected by the check ${q−}⊆π2(inv(t′))$), where *s* will be derived (*s*  ∈  *H* ′). The existence of this second environment must be supported by its type being a child of the first type ($\mathit{inv} \left(\mathit{inv} \left(t^{'}\right)\right) \in \mathit{child}_{\mathcal{T}} \left(\mathit{inv} \left(\mathit{inv} \left(t\right)\right)\right)$) and thus cannot have an individual name in the set of positive assumptions ($P^{'} \cap N_{I} = \emptyset$). Lastly, every assumption of the form ∃ *r.s* assumes, in case of an anonymous node, that its parent must be an *s*, and in case of a data node, that there exists an *r* -neighbour that is an *s*. As the second environment is assumed to describe an anonymous node, with as ‘parent environment’ the first quadruple, we have to check whether *s* ′ ∈  *H*. Similarly, positive assumptions of the form ∃(⊓ *R* ′).(⊓ *N* ′) must be evaluated ‘upwards towards the parent environment’ as well, that is *R* ′⊆ *π* <sub>2</sub> (*t* ′) and *N* ′⊆ *π* <sub>3</sub> (*t* ′). Note that this exactly corresponds to $\left(R^{'} , N^{'}\right) \in \mathit{succ}_{\mathcal{T}} \left(\left(\pi_{1} \left(t^{'}\right) , \emptyset , \emptyset\right)\right) \backslash \mathit{succ}_{\mathcal{T}} \left(t^{'}\right)$ for all ∃(⊓ *R* ′).(⊓ *N* ′) that may appear in *P* ′. Using this derived quadruple and again Rule 6, but now together with the quadruple (*t <sub>A</sub>*, {⊤}, {∃ *p.B* }, { *s* ′}) and constraint *s*  ← ∃ *p.s*, we also find $(tA,{⊤},{∃p.B},{s,s′})∈psatC,T$. Thus, the following constraint is contained in $\mathcal{C}_{\mathcal{T} , \emptyset}$:$\begin{matrix}s \leftarrow A \land \neg B \land \neg C \land \top \land \neg \exists p . B .\end{matrix}$

Now let $A={A(a),p(a,b)}$. The target we wish to validate is $G={s(a)}$. It is now simple to check that this target, *s* (*a*), is validated by considering the above constraint on $\mathcal{A}_{\mathcal{T}}$, which coincides with $A$ in this example.

The other approach to test validation is to build $can(T,A)$, graphically depicted in, and then check validation of $(C,G)$. In this figure, the same notation is used as described in. It is straightforward to check that $can(T,A)$ indeed validates $(C,G)$, as required.♥

1. [Download: Download high-res image (35KB)](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr5_lrg.jpg "Download high-res image (35KB)")
2. [Download: Download full-size image](https://ars.els-cdn.com/content/image/1-s2.0-S0004370226000093-gr5.jpg "Download full-size image")

Fig. 5. Austere Canonical Model $can(T,A)$, for $A={A(a),p(a,b)}$ and $T={A⊑∃p.B,B⊑∃q.C}$.

We note that, even in the best-case scenario, creates an amount of quadruples exponential in size of $T$ and $C$. This expressive power is used to describe all possible relevant settings that may appear at the border between the data and anonymous part of the austere canonical model. However, what is considered relevant, is only dependent on the TBox $T$; concept names that do not appear in any axiom cannot be introduced or introduce anything new and may thus be ignored. This means that the exponential blow-up observed in this definition does not influence the data complexity of determining SHACL validation in presence of ontologies. Moreover, as the described SHACL constraint rewriting happens completely independent of the data, the same rewritten shape constraint sets may be reused for different data graphs.

### 6.2. Completeness and correctness

In the rest of this section, we will show completeness and correctness of the presented rewriting technique to translate (positive) SHACL validation in presence of ontologies to plain SHACL validation over the enriched ABox $\mathcal{A}_{\mathcal{T}}$. After that we aim further: in the next subsection, we discuss how to handle stratified negation in the rewriting, followed by a section on how to achieve a pure rewriting, that is, to plain SHACL validation over the original ABox $A$.

For a quadruple $ρ=(t,P,Q,H)$ a shape name *s*  ∈  *H* and a fresh shape name *s <sub>ρ</sub>*, we define the constraint *s <sub>ρ</sub>* as follows:$\begin{matrix}s_{\rho} \leftarrow \underset{A \in \pi_{1} \left(t\right)}{\wedge} A \land \underset{A \in N_{C}^{\mathcal{T}} \backslash \pi_{1} \left(t\right)}{\wedge} \neg A \land \underset{X \in P}{\wedge} X \land \underset{Y \in Q}{\wedge} \neg Y .\end{matrix}$Note that this definition is very close to. However, it has a different purpose. In the following proofs, we will focus on validating *s <sub>ρ</sub>* instead of *s*. This makes the connection to a certain quadruple precise. And clearly, if *s <sub>ρ</sub>* (*c*) is contained in some perfect assignment, also *s* (*c*) is contained in that same assignment. We will use the notation $\mathcal{C} \cup s_{\rho}$ to denote that the constraint defining *s <sub>ρ</sub>* as above is added to the constraints in $C$.

Furthermore, we note that quadruples are designed to model the direct environment of a node that is on the ‘border’ of the model under construction. More precisely, they model the environment of *c* in $\mathit{can}_{\left|c\right|} \left(\mathcal{T} , \mathcal{A}\right)$ (sometimes shortened to $\mathcal{I}_{\left|c\right|}$,) the approximation of the austere canonical model, as defined in. In this interpretation, *c* is missing its successors. For this reason, we will evaluate *s <sub>ρ</sub>* (*c*) specifically on $\mathit{can}_{\left|c\right|} \left(\mathcal{T} , \mathcal{A}\right)$. When proving this in general, it definitely also holds for all *c* such that $|c|=1$, or put differently, all *c*  ∈  *N <sub>I</sub>*.

To clarify which shape atoms depend on others, we consider the immediate consequence operator defined in. Where ‘depending’ is intended in the sense that *s* (*c*) depends on *s* ′(*c*) and *s* ″(*c*) in case of the constraint *s*  ←  *s* ′∧ *s* ″. Recall that the perfect assignment for positive constraints consists simply of the least fixed point of this operator. With all this machinery, we can demonstrate how the rules in can mimic all these types of dependencies. In this way, we show first the completeness, and then, in, the correctness of the rewriting for positive constraints.

**Proposition 6.6**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *and* $C$ *a set of positive, normalised constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that if* $(T,A)$ *validates* $(C,G)$ *, then* $\mathit{can}_{0} \left(\mathcal{T} , \mathcal{A}\right)$ *validates* $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ *.*

6

**Proof**

It suffices to prove the following claim, which will be shown by induction on *n*.

Let $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$ and $S_{n} = T_{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}} \uparrow^{n} \left(\emptyset\right)$. If $s \left(c\right) \in S_{n + 1}$, there exists a quadruple $\rho = \left(t , P , Q , H\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ such that *s*  ∈  *H*, $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(S_{n}\right)$ and furthermore:
- 1.
	if $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)} \backslash N_{I}$, then
	- (a)
		$t=inv(tail(c))$;
	- (b)
		$P⊇{∃(⊓R).(⊓N)∣(R,N)∈succT((π1(t),∅,∅))∖succT(t)}$ and $P \cap N_{I} = \emptyset$;
	- (c)
		$Q⊇{∃(⊓R).(⊓N)∣(R,N)∈succT((π1(t),∅,∅))}$;
- 2.
	for all other *c*  ∈  *N <sub>I</sub>*, we have
	- (a)
		$t=({A∈NC∣A(c)∈AT},∅,∅)$;
	- (b)
		$P⊇{∃(⊓R).(⊓N)∣(R,N)∈succT(t),c∈(∃(⊓R).(⊓N))AT}$ and $(P∩NI)∖{c}=∅$;
	- (c)
		$Q⊇{∃(⊓R).(⊓N)∣(R,N)∈succT(t),c∉(∃(⊓R).(⊓N))AT}$;
For $(n=0)$, note that either $s←c∈C$ or $s←A∈C$. In the first case, $ρ=(t,P∪{c},Q,{s})$ can be constructed by performing Rule 1, followed by Rule 3, where $t=({A∈NC∣A(c)∈AT},∅,∅)$, and *P* and *Q* are the smallest sets that satisfy the criteria. Removing { *c* } from the second entry in the quadruple, and possibly using $t=inv(tail(c))$ instead of $t=({A∈NC∣A(c)∈AT},∅,∅)$ in case $c \notin N_{I}$, suffices for the second case. It is then easy to check that indeed $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{0} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(\emptyset\right)$.

Now suppose $s \left(c\right) \in S_{n + 1} \backslash S_{n}$. In this induction step, we will only focus on the case *s* (*c*) got derived from $s \leftarrow \exists r . s^{'} \in \mathcal{C}$ and *s* ′(*d*) ∈  *S <sub>n</sub>*, for some *r* -neighbour *d* of *c*, as the other derivation options are reflected in a straightforward way in the rules of. We distinguish two cases: | *d* | ≤ | *c* |, which we call ‘upwards’, and | *d* | > | *c* |, which we call ‘downwards’.

For the upwards case, if | *d* | ≤ | *c* | then either there exists a *2* -type *t* such that $dt=c$ and $r^{-} \in \pi_{2} \left(t\right)$, or { *c, d* }⊆ *N <sub>I</sub>*.
- •
	$dt=c$. By Rule 1, we find $\left(\mathit{inv} \left(t\right) , P , Q , \emptyset\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$, such that 1a, 1b and 1c of the claim are satisfied. With Rule 3, recalling that we assumed $s \leftarrow \exists r . s^{'} \in \mathcal{C}$, we can update this quadruple to find $ρ=(inv(t),P∪{∃r.s′},Q,{s})∈psatC,T$. As *s* ′(*d*) ∈  *S <sub>n</sub>*, it is straightforward to see that $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(S_{n}\right)$, which concludes this case.
- •
	{ *c, d* }⊆ *N <sub>I</sub>*. Again, by Rule 1, we find $\left(t , P , Q , \emptyset\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$, where $t=({A∈NC∣A(c)∈I0},∅,∅)$ and such that 1a, 1b and 1c of the claim are satisfied. Applying Rule 3, means that also $ρ=(t,P∪{∃r.s′},Q,{s})∈psatC,T$. With similar reasoning as in the previous case, it is clear that indeed $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{0} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(S_{n}\right)$.

In the second case, downwards, we have | *d* | > | *c* |, that is, $c t^{'} = d$, for some *2* -type *t* ′. In the following argument, we assume $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)} \backslash N_{I}$, but a similar argument works for *c*  ∈  *N <sub>I</sub>*. Because we assumed that *s* ′(*d*) ∈  *S <sub>n</sub>*, we can apply the induction hypothesis to find $\rho^{'} = \left(\mathit{inv} \left(t^{'}\right) , P^{'} , Q^{'} , H^{'}\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ such that (i) $r^{-} \in \pi_{2} \left(\mathit{inv} \left(t^{'}\right)\right)$, (ii) $P^{'} \cap N_{I} = \emptyset$, (iii) *s* ′ ∈  *H* ′, (iv) ∃(⊓ *R*).(⊓ *N*) ∈  *P* ′ iff $\left(R , N\right) \in \mathit{succ}_{\mathcal{T}} \left(\left(\pi_{1} \left(t^{'}\right) , \emptyset , \emptyset\right)\right) \backslash \mathit{succ}_{\mathcal{T}} \left(t^{'}\right)$. Furthermore, by construction of elements in $N_{\left(\mathcal{T} , \mathcal{A}\right)}$, we find $t^{'} \in \mathit{child}_{\mathcal{T}} \left(\mathit{tail} \left(c\right)\right)$. This means that to perform Rule 6, we only need a second quadruple (*t, P, Q, H*) for which we have to ensure that { *s* ″∣∃ *r* ″.*s* ″ ∈  *P* ′} ∈  *H*.

So, suppose ∃ *r* ″.*s* ″ ∈  *P* ′. Since, by induction hypothesis, $s_{\rho^{'}} \left(d\right) \in T_{\mathcal{I}_{\left|d\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho^{'}}} \left(S_{n}\right)$, we know *s* ″(*c*) ∈  *S <sub>n</sub>*. Thus, we can also apply the induction hypothesis to *s* ″(*c*), to find that $\rho_{s^{''}} = \left(\mathit{inv} \left(\mathit{tail} \left(c\right)\right) , P_{s^{''}} , Q_{s^{''}} , H_{s^{''}}\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ such that $P_{s^{''}}$ and $Q_{s^{''}}$ satisfy the constraints in 1b and 1c of the claim we are currently proving, and $s^{''} \in H_{s^{''}}$. Furthermore, we find that $s_{\rho_{s^{''}}} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}}} \left(S_{n}\right)$.

For each ∃ *r* ″.*s* ″ ∈  *P* ′, we can construct such a quadruple $s_{\rho^{''}}$ and combine them with Rule 2 to conclude $\rho^{''} = \left(\mathit{inv} \left(\mathit{tail} \left(c\right)\right) , \underset{\exists r^{''} . s^{''} \in P^{'}}{\cup} P_{s^{''}} , \underset{\exists r^{''} . s^{''} \in P^{'}}{\cup} Q_{s^{''}} , \underset{\exists r^{''} . s^{''} \in P^{'}}{\cup} H_{s^{''}}\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}} ,$which can serve exactly as the quadruple we were looking for to apply Rule 6, which we also do. Thus, we find that $ρ=(inv(tail(c)),⋃∃r″.s″∈P′Ps″,⋃∃r″.s″∈P′Qs″,⋃∃r″.s″∈P′Hs″∪{s})∈psatC,T,$too. Note that this quadruple satisfies all properties requested in the claim, which naturally follows from the point that all $\rho_{s^{''}}$ satisfy these properties. Furthermore, note that $s_{\rho^{''}} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho^{''}}} \left(S_{n}\right)$ holds, because for each ∃ *r* ″.*s* ″ ∈  *P* ′, we have $s_{\rho_{s^{''}}} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho_{s^{''}}}} \left(S_{n}\right)$. Thus, we can conclude that $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(S_{n}\right)$, as required.

In case ${s″∣∃r″.s″∈P′}=∅$, the above does not work. Instead, we can simply apply Rule 1 to construct the required $ρ=(t,P,Q,H)$, such that $P={∃(⊓R).(⊓N)∣(R,N)∈succT((π1(t),∅,∅))∖succT(t)}$ and $Q={∃(⊓R).(⊓N)∣(R,N)∈succT((π1(t),∅,∅))}$. Then a simple argument suffices to show that $s_{\rho} \left(c\right) \in T_{\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T}} \cup s_{\rho}} \left(S_{n}\right)$, which concludes the induction step.

**Proposition 6.8**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *and* $C$ *a set of positive, normalised constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that if* $\mathit{can}_{0} \left(\mathcal{T} , \mathcal{A}\right)$ *validates* $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ *, then* $(T,A)$ *validates* $(C,G)$ *.*

8

**Proof**

We consider the following claim. Taking $i=0$ suffices to conclude the above proposition.

Let $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$. If $\rho = \left(t , P , Q , H\right) \in \mathit{psat}_{\mathcal{C} , \mathcal{T}}$ with *s*  ∈  *H* and $sρ(c)∈PA(CT∪{sρ},Ii)$ for some $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)}$ such that $|c|=i$, then $s(c)∈PA(C,can(T,A))$. We show this by letting *i* decrease step-by-step until reaching 0. Note that because we are considering a least fixed point computation and $\mathcal{C} \subseteq \mathcal{C}_{\mathcal{T}}$, there must exist an $i=n$ such that the above naturally holds.

Assume $i=n−1$. Suppose that $sρ(c)∈PA(CT∪{sρ},In−1)$, such that $|c|=n−1$. The proof is based on unwinding how *ρ* got constructed, by an induction on the construction. Without loss of generality, we can assume *s* got added to *H* in the last rule applied. Now suppose the last rule applied was Rule 6 (the other cases are rather straightforward). Thus, there exists some $s \leftarrow \exists r . s^{'} \in \mathcal{C}$ and moreover we find that ${(t,P,Q,H∖{s}),(t′,P′,Q′,H′)}∈psatC,T$, such that *s* ′ ∈  *H* ′. Let $\rho^{'} = \left(t^{'} , P^{'} , Q^{'} , H^{'}\right)$ and note that because we were able to perform Rule 6, we can conclude that $sρ′′(ct′)∈PA(CT∪{sρ′′},In)$. By construction of the austere core model, it is clear that in $\mathcal{I}_{n}$ the node *ct* ′ satisfies exactly all concept names mentioned in *π* <sub>1</sub> (*t* ′); if ∃(⊓ *R*).⊓ *N*  ∈  *P* ′, it follows that *R* ⊆ *π* <sub>2</sub> (*t* ′) and *N* ⊆ *π* <sub>3</sub> (*t* ′); and if ∃ *r* ′.*s* ″ ∈  *P*, then *s* ″ must be contained in *H*, which means we can first perform this same proof on *s* ″ and the quadruple (*t, P, Q, H* ∖{ *s* }) to conclude that $s^{''} \left(c\right) \in \mathit{PA} \left(\mathcal{C} , \mathit{can} \left(\mathcal{T} , \mathcal{A}\right)\right)$, and thus $s^{''} \left(c\right) \in \mathit{PA} \left(\mathcal{C}_{\mathcal{T}} , \mathcal{I}_{n}\right)$ by. This means that indeed $c t^{'} \in \left(\exists r^{'} . s^{''}\right)^{\mathcal{I}_{n} , \emptyset}$, as required. As *ct* ′ will not have any successor nodes in $\mathcal{I}_{n}$, the conditions posed by *Q* ′ are enforced too.

Combining $sρ′′(ct′)∈PA(CT∪{sρ′′},In)$ with assuming the claim holds for $i=n$, we derive that $s^{'} \left(c t^{'}\right) \in \mathit{PA} \left(\mathcal{C} , \mathit{can} \left(\mathcal{T} , \mathcal{A}\right)\right)$. Since $s \leftarrow \exists r . s^{'} \in \mathcal{C}$, and $r^{-} \in \pi_{2} \left(t^{'}\right)$ we find $s(c)∈PA(C,can(T,A))$ too, as required.

These results can be summarised in the following way.

**Theorem 6.10**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *and* $C$ *a set of positive, normalised constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that* $(T,A)$ *validates* $(C,G)$ *iff* $\mathcal{A}_{\mathcal{T}}$ *validates* $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ *.*

## 7\. Rewriting for stratified SHACL

We now extend the rewriting to constraint sets $C$ with stratified negation. Intuitively, this is done by running a saturation procedure in the rewriting for each stratum of $C$, starting with the lowermost. For the transition to the next stratum in the rewriting procedure, we need to ensure that the outcome of the saturation at a non-topmost stratum is completed with negative information. To this end, we w.l.o.g. assume that all constraints from $C$ with the same shape name on the left-hand-side occur together in the same stratum.

We will operate again on quadruples (*t, P, Q, H*), which are similar to the ones in the previous section, except that *H* might additionally contain expressions of the form ¬ *s* for a shape name *s*. For a set *K* of such quadruples, we say (*t, P, Q, H*) is *maximal* in *K* if (*t, P, Q, H*) ∈  *K* and there is no *H* ′⊃ *H* with (*t, P, Q, H* ′) ∈  *K*. Then the notion of *completion* is defined as follows:

**Definition 7.1**

The *completion* $\mathit{comp}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ of a set *K* of quadruples w.r.t. a normalised Horn- $ALCHIQ$ TBox $T$ and a set of constraints $C$ is a set, defined as follows:$compC,T(K)={(t,P,Q∪Q′,H∪H¯)∣(t,P,Q,H)ismaximalinK},$where $H¯:={¬s∣soccursinC,s∉H}Q′:={∃r.s′∣s←∃r.s′∈C,s∉H}∪{c∣s←c∈C,s∉H}.$

We need to augment the inference rules of the rewriting procedure for positive constraints with an additional rule to handle constraints of the form *s*  ← ¬ *s* ′. Furthermore, Rule 6, is updated to also consider the newly added information to *Q*. Note that using the following updated definition of $\mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ will give the same results as the previously defined $\mathit{psat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ in on the first stratum, as the proposed changes do not have any effect if no ¬∃ *r.s* ’s or ¬ *s* ’s are present in the quadruples.

**Definition 7.2**

Given a normalised Horn- $ALCHIQ$ TBox $T$ and $C$ a set of normalised constraints, we let $\mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ be the smallest set of pairs containing *K* closed under Rules 2–5 defined of, where ‘ $\mathit{psat}_{\mathcal{C} , \mathcal{T}}$ ’ is replaced by ‘ $\mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ ’, and additionally under the following Rule 6’ and 7:
- 6’.
	If $s \leftarrow \exists r . s^{'} \in \mathcal{C}$, ${(t,P,Q,H),(t′,P′,Q′,H′)}⊆satC,T(K)$, $r^{-} \in \pi_{2} \left(t^{'}\right)$, $P^{'} \cap N_{I} = \emptyset$, *s* ′ ∈  *H* ′ and $\mathit{inv} \left(t^{'}\right) \in \mathit{child}_{\mathcal{T}} \left(\mathit{inv} \left(t\right)\right)$ such that
	- •
		∃(⊓ *R*).⊓ *N*  ∈  *P* ′ iff $\left(R , N\right) \in \mathit{succ}_{\mathcal{T}} \left(\pi_{1} \left(t^{'}\right) , \emptyset , \emptyset\right) \backslash \mathit{succ}_{\mathcal{T}} \left(t^{'}\right)$;
	- •
		{ *s* ″∣∃ *r* ″.*s* ″ ∈  *P* ′} ∪ {¬ *s* ″∣∃ *r* ″.*s* ″ ∈  *Q* ′, *r* ″ ∈  *π* <sub>2</sub> (*t* ′)}⊆ *H*,
	then (*t, P, Q, H*  ∪ { *s* }) belongs to $\mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$.
- 7.
	If $s \leftarrow \neg s^{'} \in \mathcal{C}$ and $\left(t , P , Q , H\right) \in \mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$ such that ¬ *s* ′ ∈  *H*, then (*t, P, Q, H*  ∪ { *s* }) belongs to $\mathit{sat}_{\mathcal{C} , \mathcal{T}} \left(K\right)$.

Now can we define the inference procedure that processes strata from the lowest to the topmost, performing saturation using the updated set of rules at every stratum, interleaved with a computation of the completion in between.

**Definition 7.3**

For a TBox $T$ and a constraint set $C$ with stratification $\mathcal{C}_{0} , \ldots , \mathcal{C}_{n}$, we let $K_{0} = \mathit{psat}_{\mathcal{C}_{0} , \mathcal{T}}$ and for each 0 <  *i*  ≤  *n* $K_{i} = \mathit{sat}_{\mathcal{C}_{i} , \mathcal{T}} \left(c o m p_{\mathcal{C}_{i - 1} , \mathcal{T}} \left(K_{i - 1}\right)\right) .$We let $\mathcal{C}_{\mathcal{T}} = \mathcal{C}_{\mathcal{T} , K_{n}}$, where $\mathcal{C}_{\mathcal{T} , K_{n}}$ is defined as in.

**Example 7.4**

Suppose $T={A⊑∃p.B}$ and consider the following set of constraints $\mathcal{C} = \mathcal{C}_{0} \cup \mathcal{C}_{1}$:$C0={sC←C,s′←∃p.sC}C1={s″←∃p.sC,sC←¬sC,s←s′∧s″}.$We consider the following two *2* -types in the rest of this example: *t <sub>A</sub>*  ≔ ({ *A* }, ∅, ∅) and *t*  ≔ ({ *A* }, { *p* }, { *B* }). Because of Rule 1, we find that the following two quadruples are contained in *K* <sub>0</sub>:$(tA,{⊤},{∃p.B},∅),(inv(t),{⊤},∅,∅).$Here, the first one can be updated to (*t <sub>A</sub>*, {⊤, ∃ *p.s <sub>C</sub>* }, {∃ *p.B* }, { *s* ′}). Note that all three quadruples are maximal in *K* <sub>0</sub>, which means we find the following quadruples in $\mathit{comp}_{\mathcal{C}_{0} , \mathcal{T}}$:$(tA,{⊤},{∃p.B,∃p.sC},{¬s′¬sC}),(tA,{⊤,∃p.sC},{∃p.B},{s′,¬sC}),(inv(t),{⊤},{∃p.sC},{¬s′,¬sC}).$By definition, these quadruples are also contained in *K* <sub>1</sub>, and thus, because of Rule 7, also the versions in which *s <sub>C</sub>* is added to the fourth set in each quadruple. Then, we can apply Rule 6’ to (*t <sub>A</sub>*, {⊤, ∃ *p.s <sub>C</sub>* }, {∃ *p.B* }, { *s* ′, ¬ *s <sub>C</sub>, s <sub>C</sub>* }), (*inv* (*t*), {⊤}, {∃ *p.s <sub>C</sub>* }, {¬ *s* ′, ¬ *s <sub>C</sub>, s <sub>C</sub>* }) and the constraint *s* ″ ← ∃ *p*.¬ *s <sub>C</sub>*, to find $(tA,{⊤,∃p.sC},{∃p.B},{s′,¬sC,sC,s″})∈K1$ too. After applying Rule 5 based on the constraint $s \leftarrow s^{'} \land s^{''} \in \mathcal{C}_{1}$, we can extract the following rewritten constraint:$\begin{matrix}s \leftarrow A \land \neg B \land \neg C \land \exists p . s_{C} \land \neg \exists p . B \in \mathcal{C}_{\mathcal{T}} ,\end{matrix}$Now let $A={A(a),p(a,b),C(b)}$ and set the target to $G={s(a)}$. As $\mathcal{A} = \mathcal{A}_{\mathcal{T}}$, we indeed find a positive answer when validating $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ over $\mathcal{A}_{\mathcal{T}}$. Notice $can(T,A)$ corresponds to the canonical interpretation of { *A* (*a*), *p* (*a, b*), *C* (*b*), *p* (*a, at*), *B* (*at*)}. Thus, we can conclude that $(T,A)$ validates $(C,G)$ too. ♥

Given a stratified set of constraints $C$ with stratification $\mathcal{C}_{0} , \ldots , \mathcal{C}_{n}$, let $\mathcal{C}_{\leq i} : = \mathcal{C}_{0} \cup \ldots \cup \mathcal{C}_{i}$. Similarly, we will use $\mathcal{C}_{\mathcal{T} , \leq i}$ to denote $\mathcal{C}_{\mathcal{T} , K_{0}} \cup \ldots \cup \mathcal{C}_{\mathcal{T} , K_{i}}$.

**Theorem 7.5**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *and* $C$ *a set of stratified constraints with stratification* $\mathcal{C}_{0} , \ldots , \mathcal{C}_{n}$ *, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that* $(T,A)$ *validates* $(C,G)$ *iff* $\mathcal{A}_{\mathcal{T}}$ *validates* $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ *.*

5

**Proof**

(⇒). We will prove completeness by proving the following claim by induction on *i*

Let $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$. For each $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)}$ and for each 0 ≤  *i*  ≤  *n*, there exists $\rho = \left(t , P , Q , H\right) \in K_{i}$ that is maximal in *K <sub>i</sub>*, and moreover:
- 1.
	if $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)} \backslash N_{I}$, then
	- (a)
		$t=inv(tail(c))$;
	- (b)
		$P⊇{∃(⊓R).⊓N∣(R,N)∈succT((π1(t),∅,∅))∖succT(t)}$ and $P \cap N_{I} = \emptyset$;
	- (c)
		$Q⊇{∃(⊓R).⊓N∣(R,N)∈succT((π1(t),∅,∅))}$;
- 2.
	for all other *c*  ∈  *N <sub>I</sub>*, we have
	- (a)
		$t=({A∈NC∣A(c)∈AT},∅,∅)$;
	- (b)
		$P⊇{∃(⊓R).⊓N∣(R,N)∈succT(t),c∈(∃(⊓R).⊓N)AT}$ and $(P∩NI)∖{c}=∅$;
	- (c)
		$Q⊇{∃(⊓R).⊓N∣(R,N)∈succT(t),c∉(∃(⊓R).⊓N)AT}$;
- 3.
	$H={s∣s(c)∈PA(can(T,A),C≤i)}∪{¬s∣s(c)∉PA(can(T,A),C≤i),sdefinedinCi−1}$;
- 4.
	and $s_{\rho} \left(c\right) \in \mathit{PA} \left(\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T} , \leq i} \cup s_{\rho}\right)$.
Analogous to, it follows that for each *s* such that $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq 0}\right)$, there exists a quadruple $\left(t , P_{s} , Q_{s} , H_{s}\right) \in \mathit{sat}_{\mathcal{C}_{0} , \mathcal{T}} \left(\emptyset\right) = K_{0}$ such that *s*  ∈  *H <sub>s</sub>* and such that requirements 1, 2 and 4 of the claim hold. Now let $X={s∣s(c)∈PA(can(T,A),C≤0)}$. Then, following Rule 2 of the rewriting algorithm in, we must conclude that also $\left(t , \cup_{s \in X} P_{s} , \cup_{s \in X} Q_{s} , \cup_{s \in X} H_{s}\right) \in K_{0}$. This quadruple is exactly the quadruple we were looking for: requirements 1, 2 and 4 have to be satisfied, as they are satisfied for each (*t, P <sub>s</sub>, Q <sub>s</sub>, H <sub>s</sub>*) separately; requirement 3 follows, as *s*  ∈  *H <sub>s</sub>* implies $X \subseteq \cup_{s \in X} H_{s}$, and at the same time the correctness of the rewriting forbids that $H_{s} \backslash X \neq \emptyset$. In the same way, maximality of the quadruple is implied.

For the induction step, $i=j+1$, note that for each $c \in N_{I} \cup N_{\left(\mathcal{T} , \mathcal{A}\right)}$, we are given some (*t, P, Q, H*) ∈  *K <sub>j</sub>* that is maximal and satisfies requirements 1 to 4 for $i=j$. As this quadruple is assumed to be maximal, completion $\mathit{comp}_{\mathcal{C}_{j} , \mathcal{T}}$ can be applied to (*t, P, Q, H*). Thus, we find $\left(t , P , Q \cup Q^{'} , H \cup \bar{H}\right) \in K_{j + 1}$. Since *s*  ∈  *H* iff $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j}\right)$, it must follow that $\neg s \in \bar{H}$ iff $s \left(c\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j}\right)$ and *s* occurs in $\mathcal{C}_{\leq j}$. Now suppose $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j + 1}\right) \backslash \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j}\right)$, then there must exist a constraint $s←C∈C$ that caused this addition.

If $C = \neg s^{'}$, then *s* ′ is defined in $\mathcal{C}_{\leq j}$ by the stratification rules, and $s^{'} \left(c\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j}\right)$, which means $\neg s^{'} \in \bar{H}$, thus Rule 7 can be applied to conclude that $(t,P,Q∪Q′,H∪H¯∪{s})∈Kj+1$. If *C* is any of the other options, the same reasoning as in the proof of can be used.

Now all that is left to show, is that each *Y*  ∈  *Q* ′ is not blocking the satisfaction of requirement 4. By taking a closer look a the completion procedure, we see that $Y = \exists r . s^{'}$ for some $s \leftarrow \exists r . s^{'} \in \mathcal{C}_{\leq j}$ such that $s∉H$, or $Y=c$, for some $s \leftarrow c \in \mathcal{C}_{\leq j}$ and $s∉H$. For both cases, note that $s∉H$, which means $s \left(c\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq j}\right)$. Assuming that any of these *Y* is indeed blocking restriction 4, directly leads to a contradiction with the previous observation. Thus, we have indeed found the required quadruple.

(⇐). Again, let $\mathcal{I}_{i} = \mathit{can}_{i} \left(\mathcal{T} , \mathcal{A}\right)$. To show correctness, we will show by induction on *i* that for each $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)}$ and for each $\rho = \left(t , P , Q , H\right) \in K_{i}$ such that (a) $s_{\rho} \left(c\right) \in \mathit{PA} \left(\mathcal{I}_{\left|c\right|} , \mathcal{C}_{\mathcal{T} , \leq i} \cup s_{\rho}\right)$, we find for each *s*  ∈  *H* that $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$.

First, note that provides the induction basis. So, for the induction step, suppose we are given some $c \in N_{\left(\mathcal{T} , \mathcal{A}\right)}$ and $\left(t , P , Q , H\right) \in K_{i + 1}$ such that (a) holds. We will focus on the case that there exists a (*t, P, Q* ′, *H* ′) ∈  *K <sub>i</sub>* that is maximal in *K <sub>i</sub>*, such that (*t, P, Q, H*) is the result of first applying completion to (*t, P, Q* ′, *H* ′) to find $\left(t , P , Q^{'} \cup Q^{''} , H^{'} \cup \bar{H^{'}}\right) \in \mathit{comp}_{\mathcal{C}_{i} , \mathcal{T}}$, followed by application(s) of rules 3–5, 6’ or 7. Here, we will only consider the result of applying Rule 7, as the treatment of the application of the other rules is very similar to what is discussed in. Note that Rules 1 and 2 are not really having any relevant effects after finishing the first stratum.

So, assume $s \leftarrow \neg s^{'} \in \mathcal{C}_{i + 1}$ and $\neg s^{'} \in \bar{H^{'}}$. We argue that each $s^{'} \leftarrow C \in \mathcal{C}$ cannot be used to deduce $s^{'} \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$.
- •
	*C*  ∈  *N <sub>C</sub>*. If *C*  ∈  *π* <sub>1</sub> (*t*), we would have found *s* ′ ∈  *H* ′ by maximality of (*t, P, Q* ′, *H* ′). Thus, $C \notin \pi_{1} \left(t\right)$, which means ¬ *C* appears in *s* <sub>(<em>t,P,Q,H</em>)</sub>. Since (a) holds, this means that $c \notin C^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$, which suffices.
- •
	*C*  ∈  *N <sub>I</sub>*. As $\neg s^{'} \in \bar{H^{'}}$, we find *C*  ∈  *Q*. Since (a) holds, this means $C^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)} \neq c^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$, which suffices.
- •
	*C*  ∈ { *s* ″, *s* ″∧ *s* ‴∣{ *s* ″, *s* ‴}⊆ *N <sub>S</sub>* }. Perform this same argument for *s* ″ or *s* ‴. As we are considering a least fixed point semantics, this regression must terminate.
- •
	$C = \exists r . s^{''}$, for some *r*  ∈  *N <sub>R</sub>, s*  ∈  *N <sub>S</sub>*. As $\neg s^{'} \in \bar{H^{'}}$, we find *C*  ∈  *Q*. Note we derived completeness and correctness of all strata up till *i*, that is for all *s*, for all natural numbers *n*, and all *c* such that | *c* | ≤  *n*, we have $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$ iff $s \left(c\right) \in \mathit{PA} \left(\mathcal{I}_{n} , \mathcal{C}_{\mathcal{T} , \leq i}\right)$. Thus, combining this with (*a*), we find that in any case $s^{''} \left(d\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$, for $dt=c$, such that $r^{-} \in \pi_{2} \left(t\right)$.
	The other option we have to exclude is $d=ct$, for some *r*  ∈  *π* <sub>2</sub> (*t*). For contradiction, assume $s^{''} \left(d\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$. So we know there must exist a quadruple $\rho_{d} = \left(\mathit{inv} \left(t\right) , P_{d} , Q_{d} , H_{d}\right) \in K_{i}$ such that *s* ″ ∈  *H <sub>d</sub>* and $s_{\rho_{d}} \left(d\right) \in \mathit{PA} \left(\mathcal{I}_{\left|d\right|} , \mathcal{C}_{\leq i , \mathcal{T}} \cup s_{\rho_{d}}\right)$, and such that these there does not exist $\left(\mathit{inv} \left(t\right) , P_{d}^{'} , Q_{d}^{'} , H_{d}^{'}\right) \in K_{i}$ with the same properties, but $|{∃r.s∈Pd′}|<|{∃r.s∈Pd}|$. First of all, note that {¬ *s* ∣∃ *r.s*  ∈  *Q <sub>d</sub>* }⊆ *H*; for all such *s*, we have $¬s∉H$, implies *s*  ∈  *H*. Thus, $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$ by induction hypothesis. Using completeness and correctness, this implies $s_{\rho_{d}} \left(d\right) \notin \mathit{PA} \left(\mathit{can}_{\left|d\right|} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i , \mathcal{T}} \cup s_{\rho_{d}}\right)$, which is a contradiction.
	Now there are two options: if { *s* ∣∃ *r.s*  ∈  *P <sub>d</sub>* }⊆ *H*, then Rule 6’ could have been applied on *s* ′ ← ∃ *r.s* ″ at a certain point, which is in contradiction with the maximality of (*t, P, Q* ′, *H* ′). So, we are left with the second option: ${s∣∃r.s∈Pd}¬⊆H$. Now we can repeat this same argument for each member of { *s* ∣∃ *r.s*  ∈  *P <sub>d</sub>* }∖ *H*. Because we are solely considering the least amount of ∃ *r.s* ’s in *P <sub>d</sub>*, we know they all are essential in deriving *s* ″(*d*). Thus, $s^{''} \left(d\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$ for all *d* such that $\left(c , d\right) \in \left(r\right)^{\mathit{can} \left(\mathcal{T} , \mathcal{A}\right)}$, which automatically implies the required result.
- •
	$C = \neg s^{''}$. If $s \leftarrow \neg s^{'} \in \mathcal{C}_{i + 1}$, then $s^{'} \leftarrow \neg s^{''} \in \mathcal{C}_{\leq i}$, by definition of the strata. This means that ¬ *s* ″ cannot be part of $\bar{H^{'}}$. So, to apply Rule 7, it must be that ¬ *s* ″ ∈  *H* ′. However, this is in contradiction with the maximality of (*t, P, Q* ′, *H* ′) that would imply *s* ′ ∈  *H* ′, which concludes this case.

Thus, we conclude that $s^{'} \left(c\right) \notin \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i}\right)$, and thus that indeed $s \left(c\right) \in \mathit{PA} \left(\mathit{can} \left(\mathcal{T} , \mathcal{A}\right) , \mathcal{C}_{\leq i + 1}\right)$, as required.

## 8\. Pure rewritings

lets us reduce SHACL validation in the presence of Horn- $ALCHI$ TBoxes to plain SHACL validation over the completed ABox $\mathcal{A}_{\mathcal{T}}$. In this section we discuss how to update this rewriting to a pure rewriting. That is, how to produce a set of constraints $\mathcal{C}^{'}$, in a data-independent way, such that $(T,A)$ validates $(C,G)$ iff $A$ validates $\left(\mathcal{C}^{'} , \mathcal{G}\right)$.

To make the rewriting pure, we have to encode the information added to $A$ by the immediate consequence operator $T_{\mathcal{T}}$ defined in in new constraints. However, SHACL as introduced in can only propagate information on nodes, and information about the properties/roles connecting the nodes cannot be directly represented.

We discuss two ways around this. First we present a solution for TBoxes that do not contain counting axioms (*A* ⊑ ≤  <sub>1</sub> *r.B*). The role information added to $\mathcal{A}_{\mathcal{T}}$ in this case is simple, and it can be directly derived from locally satisfying axioms of the form $r_{0} \sqcap \ldots \sqcap r_{n} \sqsubseteq r$. For the general case, we extend SHACL and enable it to describe edges, rather than just nodes.

Without loss of generality, we assume in this section that there are no cycles over role inclusions. That is, no TBox contains a set of role inclusions of the form ${r⊑r1,r1⊑r2,…,rn⊑r}$. If such a cycle exists, then all roles names appearing in the cycle are replaced by one unique role name.

### 8.1. Rewriting for normalised Horn-ALCHI

Let us first focus on how to define a pure rewriting for normalised Horn- $ALCHI$.

**Definition 8.1**

A Horn- $ALCHI$ TBox $T$ is in normal form if each of the concept inclusions in $T$ are of one of the following forms:$\begin{aligned}(\text{F1}) A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq B & (\text{F3}) A \sqsubseteq \forall r . B \\ (\text{F4}) A \sqsubseteq \exists r . B ,\end{aligned}$for ${A,A0,…,An,B}⊆N‾C$ and $r∈N‾R$. Furthermore, $T$ may contain role inclusions of the form *r* ⊑ *r* ′, for ${r,r′}⊆N‾R$.

For each Horn- $ALCHI$ TBox $T$, we define the following set of constraints, capturing most of the information derived by the immediate consequence operator $T_{\mathcal{T}}$, defined in.

**Definition 8.2**

For each *A*  ∈  *N <sub>C</sub>*, we let *s <sub>A</sub>*  ∈  *N <sub>S</sub>* be a fresh shape name. Given a normalised Horn- $ALCHI$ TBox $T$, let $\mathcal{T}_{s}$ be the smallest set of constraints containing for each $\mathcal{T} \models A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq B$, the constraint(2) $\begin{matrix}s_{B} \leftarrow \underset{0 \leq i \leq n}{\wedge} s_{A_{i}} \in \mathcal{T}_{s} ,\end{matrix}$furthermore, for each $A⊑∀r.B∈T$ and $T⊧S⊑r$ the constraint(3) $\begin{matrix}s_{B} \leftarrow \exists S^{-} . s_{A} \in \mathcal{T}_{s} ,\end{matrix}$and for each $A∈N‾C$, the constraint(4) $\begin{matrix}s_{A} \leftarrow A \in \mathcal{T}_{s} .\end{matrix}$

**Definition 8.3**

Given a normalised Horn- $ALCHI$ TBox $T$, let $\mathcal{C}_{\mathcal{T}}^{+}$ be the set of constraints consisting of the constraints in $\mathcal{C}_{\mathcal{T}}$, taking into account the following alterations:
- •
	each concept name *A*  ∈  *N <sub>C</sub>* appearing in an axiom in $\mathcal{C}_{\mathcal{T}}$ is replaced by *s <sub>A</sub>*; and
- •
	for each $T⊧⊓R⊑r$, such that *R*  ∪ { *r* }⊆ *R* ′, and ⊓ *R* ′ appears in some constraint, ⊓ *R* ′ is replaced by ⊓(*R* ′∖{ *r* }).

Note that when considering $\mathcal{C}_{\mathcal{T}}^{+} \cup \mathcal{T}_{s}$ instead of $\mathcal{C}_{\mathcal{T}}$, we are introducing a new lowest stratum: the set of freshly introduced constraints, based on existing concept names. However, the only point of this stratum is to mimic exactly which concept names hold at which points in the enriched ABox $\mathcal{A}_{\mathcal{T}}$, defined in.

**Proposition 8.4**

*Given a normalised Horn-* $ALCHI$ *TBox* $T$ *and* $C$ *a set of positive constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that* $\mathit{can}_{0} \left(\mathcal{T} , \mathcal{A}\right)$ *validates* $\left(\mathcal{C}_{\mathcal{T}} , \mathcal{G}\right)$ *iff* $A$ *validates* $\left(\mathcal{C}_{\mathcal{T}}^{+} \cup \mathcal{T}_{s} , \mathcal{G}\right)$ *.*

**Proof**

Note that $\mathit{can}_{0} \left(\mathcal{T} , \mathcal{A}\right)$ corresponds to $\mathcal{A}_{\mathcal{T}}$, the first layer in building the austere canonical model, defined in. In this definition, the ABox is completed in a least fixed point manner under certain axioms ($A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq B$ and *A* ⊑∀ *r.B*) that are precisely encoded in constraints of the form and. The only difference is that we cannot translate axioms of the form $\mathcal{T} \models S \sqsubseteq r^{'}$ directly. A simple fix suffices: as role atoms in $\mathcal{A}_{\mathcal{T}} \backslash \mathcal{A}$ can only be the result of an axiom of the form *r* ⊑ *r* ′, the replacement in in combination with the implied roles in constraints of the form is sufficient. As we are also considering a least fixed point semantics for SHACL validation, the above result directly follows.

Thus, considering $\mathcal{C}_{\mathcal{T}}^{+} \cup \mathcal{T}_{s}$ as rewritten set of constraints indeed provides us with a pure rewriting. The following theorem follows from combining the results of and.

**Theorem 8.5**

*Given a normalised Horn-* $ALCHI$ *TBox* $T$ *and* $C$ *a set of stratified constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that* $(T,A)$ *validates* $(C,G)$ *iff* $A$ *validates* $\left(\mathcal{C}_{\mathcal{T}}^{+} , \mathcal{G}\right)$ *.*

### 8.2. SHACLb

For a pure rewriting of normalised Horn- $ALCHIQ$, we propose a different solution: we define an extension of SHACL that we call SHACL <sup><em>b</em></sup>. Here we also allow ‘binary’ shape constraints *b*: we can also express constraints on pairs of nodes. We note that not all operators defined in SHACL <sup><em>b</em></sup> are necessary to define a pure rewriting for normalised Horn- $ALCHIQ$. However, we do resort to the following version to demonstrate how the imbalance between unary and binary (shape) atoms in SHACL can be fully reduced.

**Definition 8.6**

Let *SHACL* <sup><em>b</em></sup> consist of shape constraints of the form *s*  ← φ, or *b*  ←  *ψ*, for { *s, b* }⊆ *N <sub>S</sub>*, such that $\begin{aligned}\varphi & : : = c \mid s \mid A \mid \varphi \land \varphi \mid \neg \varphi \mid \exists \psi . \varphi \\ \psi & : : = s ? \mid b \mid r \mid \psi \cup \psi \mid \psi \cap \psi \mid \psi \cdot \psi \mid \psi^{\star} \mid \psi^{-} \mid \psi \backslash \psi ,\end{aligned}$where *c*  ∈  *N <sub>I</sub>*, { *s, b* }⊆ *N <sub>S</sub>, A*  ∈  *N <sub>C</sub>* and $r∈N‾R$. We evaluate SHACL <sup><em>b</em></sup> as defined in, extended with $(∃ψ.φ)I,S:={e∈ΔI∣∃e′∈ΔI:(e,e′)∈(ψ)I,S∧e′∈(φ)I,S}(s?)I,S:={(e,e)∈ΔI×ΔI∣e∈sI,S}(b)I,S:={(e,e′)∈ΔI×ΔI∣b(e,e′)∈S}(r)I,S:=rI(ψ∪ψ′)I,S:=(ψ)I,S∪(ψ′)I,S(ψ∩ψ′)I,S:=(ψ)I,S∩(ψ′)I,S(ψ·ψ′)I,S:={(e,e′)∈ΔI×ΔI∣∃e″∈ΔI:(e,e″)∈(ψ)I,S∧(e″,e′)∈(ψ′)I,S}(ψ*)I,S:={(e,e′)∈ΔI×ΔI∣∃{e0,…,en}⊆ΔI:∀i∈{0,…,n1}:(ei,ei+1)∈(ψ)I,S∧e0=e∧en=e′}(ψ−)I,S:={(e,e′)∈ΔI×ΔI∣(e′,e)∈(ψ)I,S}(ψ∖ψ′)I,S:=(ψ)I,S∖(ψ′)I,S.$

The following shape expressions, although not explicitly present, are also expressible in SHACL <sup><em>b</em></sup>.$\begin{aligned}\exists R . \varphi & = \exists \left(r_{0} \cap \ldots \cap r_{n}\right) . \varphi \\ \mathsf{eq} \left(E , E^{'}\right) & = \neg \exists . \left(E \backslash E^{'}\right) . \top \land \neg \exists . \left(E^{'} \backslash E\right) . \top \\ \mathsf{disj} \left(E , E^{'}\right) & = \neg \exists \left(E \cap E^{'}\right) . \top\end{aligned}$ where $R = r_{0} \sqcap \ldots \sqcap r_{n}$.

**Definition 8.7**

Define *s <sub>A</sub>*  ∈  *N <sub>S</sub>* and *b <sub>r</sub>*  ∈  *N <sub>S</sub>* to be a fresh shape names for each *A*  ∈  *N <sub>C</sub>*, respectively $r∈N‾R$. Given a normalised Horn- $ALCHIQ$ TBox $T$, let $\mathcal{T}_{s}$ be the smallest set of binary SHACL constraints containing for each $\mathcal{T} \models A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq B$, the constraint(5) $\begin{matrix}s_{B} \leftarrow \underset{0 \leq i \leq n}{\wedge} s_{A_{i}} \in \mathcal{T}_{s} ,\end{matrix}$for each $A \sqsubseteq \forall r^{'} . B \in \mathcal{T}$ the constraint(6) $\begin{matrix}s_{B} \leftarrow \exists b_{r^{-}} . s_{A} \in \mathcal{T}_{s} ,\end{matrix}$and, for each $\mathcal{T} \models A_{0} \sqcap \ldots \sqcap A_{n} \sqsubseteq \exists \left(r_{0} \sqcap \ldots \sqcap r_{m}\right) . \left(B_{0} \sqcap \ldots \sqcap B_{k}\right)$ and $A \sqsubseteq \leq_{1} r . B \in \mathcal{T}$ such that $r∈{r0,…,rm}$ and $B∈{B0,…,Bk}$, the constraints(7) ${bri←s^?·br·sB?,s^←sA∧sA0∧…∧sAn,$(8) $sBj←sB∧∃br−.s^}⊆Ts,$for each $i∈{0,…,m}$ and $j∈{0,…,k}$, and a fresh shape name $s^$, furthermore, for each $r \sqsubseteq r^{'} \in \mathcal{T}$, the constraint(9) $\begin{matrix}b_{r^{'}} \leftarrow b_{r} \in \mathcal{T}_{s} ,\end{matrix}$and for each $r∈N‾R$, *p*  ∈  *N <sub>R</sub>* the constraints(10) ${br←r,b(p−)←(bp)−,bp←(bp−)−}⊆Ts,$and, lastly, for each $A∈N‾C$, the constraint(11) $\begin{matrix}s_{A} \leftarrow A \in \mathcal{T}_{s} .\end{matrix}$

**Proposition 8.8**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *, for each* $A$ *, we find that for all A*  ∈  *N <sub>C</sub>, all* $r∈N‾R$ *, and all* ${c,d}⊆ΔA$ *,*
- •
	$A \left(c\right) \in \mathcal{A}_{\mathcal{T}}$ *iff* $s_{A} \left(c\right) \in \mathit{PA} \left(\mathcal{T}_{s} , \mathcal{A}\right)$ *;*
- •
	$r \left(c , d\right) \in \mathcal{A}_{\mathcal{T}}$ *iff* $b_{r} \left(c , d\right) \in \mathit{PA} \left(\mathcal{T}_{s} , \mathcal{A}\right)$ *.*

**Proof**

Let $\mathcal{T}_{s}^{\star}$ consists of the constraints in $\mathcal{T}_{s}$ defined by and. Then, it is clear that $A(c)∈A$ iff $s_{A} \left(c\right) \in \mathit{PA} \left(\mathcal{T}_{s}^{\star} , \mathcal{A}\right)$ and $r(c,d)∈A$ iff $b_{r} \left(c , d\right) \in \mathit{PA} \left(\mathcal{T}_{s}^{\star} , \mathcal{A}\right)$. This means that all information of the ABox can be precisely captured in shape names. For the rest, note how the different lines in defining the immediate consequence operator used to build $\mathcal{A}_{\mathcal{T}}$ from $A$ correspond one-to-one to the constraints defined in to, with the exception of using the shorthand $s^$. As both the perfect assignment *PA* as the construction of $\mathcal{A}_{\mathcal{T}}$ are based on a least fixed point semantics, the result follows.

The completeness and correctness of the full rewriting now directly follow. Clearly, we concluded that all information in $\mathcal{A}_{\mathcal{T}}$, albeit in the form *s <sub>A</sub>* and *b <sub>r</sub>*, can be derived by SHACL <sup><em>b</em></sup> constraints constructed to this end. Therefore, there is not really a difference between evaluating $\mathcal{C}_{\mathcal{T}}$ over $\mathcal{A}_{\mathcal{T}}$, or $\mathcal{C}_{\mathcal{T}} \cup \mathcal{T}_{s}$ over $A$, except that we should replace concept names and roles by their shape names referring to them.

**Definition 8.9**

Given a normalised Horn- $ALCHIQ$ TBox $T$, let $\mathcal{C}_{\mathcal{T}}^{+}$ be the set of constraints consisting of the axioms in $\mathcal{C}_{\mathcal{T}}$, such that each concept name *A*  ∈  *N <sub>C</sub>* appearing in an axiom in $\mathcal{C}_{\mathcal{T}}$ is replaced by *s <sub>A</sub>*, and similarly, each $r∈N‾R$ by *b <sub>r</sub>*.

Now that the concept and role names are replaced by their shape equivalents, we have indeed produced a pure rewriting.

**Theorem 8.10**

*Given a normalised Horn-* $ALCHIQ$ *TBox* $T$ *and* $C$ *a set of stratified constraints, for every target* $G$ *and every ABox* $A$ *that is consistent with* $T$ *, we have that* $(T,A)$ *validates* $(C,G)$ *iff* $A$ *validates* $\left(\mathcal{C}_{\mathcal{T}}^{+} \cup \mathcal{T}_{s} , \mathcal{G}\right)$ *.*

## 9\. Complexity results

We now discuss the computational complexity of SHACL validation in the presence of Horn- $ALCHIQ$ TBoxes. Specifically, we discuss the *combined complexity* and the *data complexity* of the problem. The former is measured in terms of the combined size of all input components, while the latter is measured assuming all components except the ABox are of fixed size.

**Theorem 9.1**

*The problem of SHACL validation in the presence of normalised Horn-* $ALCHIQ$ *TBoxes is ExpTime-complete in combined complexity and PTime-complete in data complexity.*

**Proof**

For data complexity, the PTime lower bound was shown in, which already applies in the absence of ontologies. The matching PTime upper bound follows from, combined with the fact that $\mathcal{A}_{\mathcal{T}}$ has size polynomial in $A$ ’s size itself, and that validation under stratified constraints without ontologies in feasible in polynomial time in data complexity. We note that checking whether the input graph is consistent with a TBox can also be done in polynomial time.

For the upper bound in combined complexity, we rely on the rewriting algorithm discussed in and. Let $(T,A)$ be a normalised Horn- $ALCHIQ$ knowledge base and $C$ any set of (stratified) constraints. Observe that the number of different quadruples (*t, P, Q, H*) over the signature of $T$ and $C$ that can be added to any *K <sub>i</sub>* during the rewriting is bounded by an exponential in the size of $T$ and $C$. An application of any of the rules takes polynomial time in the size of $T$, $A$, $C$ and $\cup_{i > 0} K_{i}$, which means the application of all rules in the procedure is bounded by an exponential in the size of $T$, $A$ and $C$. Computing $\mathcal{C}_{\mathcal{T} , K}$ is polynomial in the size of *K*, for all possible *K*. Thus, overall we get a procedure that runs in exponential time in the size of $T$, $A$ and $C$.

The hardness result in combined complexity follows from the hardness of reasoning in the ontology alone: checking whether an atom of the form *r* (*a, b*) or *A* (*a*) is implied by a knowledge base is already ExpTime-complete in combined complexity.

The hardness inherited from the ontology alone is not the only source of complexity. ExpTime-hardness holds even for very weak description logics like *DL-Lite* $R$ and a very simple fragment of SHACL.

Define a *simple* shape expression φ in the following way $\begin{matrix}\varphi : : = s \mid A \mid \varphi \land \varphi \mid \exists r . \varphi ,\end{matrix}$for *s*  ∈  *N <sub>S</sub>, A*  ∈  *N <sub>C</sub>* and $r∈N‾R$. Shape constraints in *simple-* SHACL are then build in the same way as for regular SHACL by using simple shape expressions instead of regular ones. All other definitions extend in a straightforward way to simple-SHACL.

**Theorem 9.2**

*Let* $L$ *be any DL that support axioms of the forms A* ⊑∃ *r*.⊤ *and* ∃ *r* <sub>1</sub>.⊤⊑∃ *r* <sub>2</sub>.⊤ *and r* <sub>1</sub> ⊑ *r* <sub>2</sub>*. In the presence of* $L$ *TBoxes, simple-SHACL validation is ExpTime-complete in combined complexity.*

**Proof**

Membership follows directly from. To prove ExpTime-hardness in combined complexity we reduce the word problem of polynomially space-bounded *Alternating Turing Machines (ATMs)* to validating shapes under an $L$ ontology.

An *ATM* is defined as a tuple of the form $\mathcal{M} = \left(\Sigma , Q_{\exists} , Q_{\forall} , q_{0} , q_{a c c} , q_{r e j} , \delta\right)$ where Σ is an *alphabet, Q* <sub>∃</sub> is a set of *existential states, Q* <sub>∀</sub> is a set of *universal states*, disjoint from *Q* <sub>∃</sub>, *q* <sub>0</sub>  ∈  *Q* <sub>∃</sub> is an *initial state, q <sub>acc</sub>*  ∈  *Q* <sub>∃</sub>  ∪  *Q* <sub>∀</sub> is an *accepting state, q <sub>rej</sub>*  ∈  *Q* <sub>∃</sub>  ∪  *Q* <sub>∀</sub> is a *rejecting state*, and *δ* is a *transition relation* of the form $δ⊆Q×(Σ∪{B})×Q×(Σ∪{B})×{−1,0,+1}$ with $Q = Q_{\exists} \cup Q_{\forall}$. Here *B* is the *blank symbol*. We let $δ(q,a)={(q′,b,D)∣(q,a,q′,b,D)∈δ}$. W.l.o.g., we assume that in $M$ universal and existential states are strictly alternating: if (*q, a, q* ′, *b, m*) ∈  *δ* and *q*  ∈  *Q* <sub>∃</sub> (resp., *q*  ∈  *Q* <sub>∀</sub>), then *q* ′ ∈  *Q* <sub>∀</sub> (resp., *q* ′ ∈  *Q* <sub>∃</sub>). We further assume that $|δ(q,a)|=2$ for all combinations of states *q*  ∈  *Q* and symbols *a*  ∈ Σ ∪ { *B* }. If $δ(q,a)={(q1,a1,D1),(q2,a2,D2)}$, we let $\delta_{ℓ} \left(q , a\right) = \left(q_{1} , a_{1} , D_{1}\right)$ and $\delta_{r} \left(q , a\right) = \left(q_{2} , a_{2} , D_{2}\right)$.

A run of an ATM $M$ on an input word *w* is defined as usual. We assume a word $w = d_{1} \hdots d_{n} \in \Sigma^{\star}$ with *n*  > 0 together with an ATM $M$ that only uses the tape cells where the input word was written, i.e., it only uses the first *n* cells. Checking if such $M$ accepts *w* is an ExpTime-hard problem.

We show how to construct a knowledge base $(T,A)$ and shapes graph $(C,{sacc(a)})$ such that $M$ accepts *w* iff $(T,A)$ validates $(C,{sacc(a)})$. The reduction takes polynomial time in the size of $M$ and *w*. It uses the following symbols:
- •
	a concept name *Init* and a shape name *s <sub>acc</sub>*;
- •
	role names *succ, succ* <sub>ℓ</sub>, *succ <sub>r</sub>*;
- •
	shape names *s <sub>q</sub>* for all states *q*  ∈  *Q* <sub>∃</sub>  ∪  *Q* <sub>∀</sub>;
- •
	shape names *h <sub>i</sub>* for all 1 ≤  *i*  ≤  *n*;
- •
	shape names $c_{b}^{\left(i\right)}$ for all *b*  ∈ Σ ∪ { *B* } and 1 ≤  *i*  ≤  *n*.

Set $A={Init(a)}$ and let $T$ contain the following inclusions:$\begin{matrix}\mathit{Init} \sqsubseteq \exists \mathit{succ}_{ℓ} . \top \mathit{succ}_{ℓ} \sqsubseteq \mathit{succ} \exists \mathit{succ}^{-} . \top \sqsubseteq \exists \mathit{succ}_{ℓ} . \top \\ \mathit{Init} \sqsubseteq \exists \mathit{succ}_{r} . \top \mathit{succ}_{r} \sqsubseteq \mathit{succ} \exists \mathit{succ}^{-} . \top \sqsubseteq \exists \mathit{succ}_{r} . \top .\end{matrix}$The interpretation $can(T,A)$ provides us with an infinite binary tree. In that tree, the root is representing the starting configuration of $M$ and each child of a node represents a next step in the run of the ATM $M$.

To mimic the start configuration, we define the following shapes:$\begin{matrix}h_{1} \leftarrow \mathit{Init} s_{q_{0}} \leftarrow \mathit{Init} c_{d_{i}}^{\left(i\right)} \leftarrow \mathit{Init} \text{for} \text{all} 1 \leq i \leq n\end{matrix}$ Intuitively, this is setting the starting state to *q* <sub>0</sub> (denoted by the shape name $s_{q_{0}}$), putting the head in the starting position (*h* <sub>1</sub>), and stating the input word written on each tape cell ($c_{d_{i}}^{\left(i\right)}$).

The next step is to encode the transition relation of the $M$. For each 1 ≤  *i*  ≤  *n*, each (*q, a*) ∈  *Q*  × (Σ ∪ { *B* }), and *γ*  ∈ {ℓ, *r* } we add the following shapes, where $\left(q^{'} , b , D\right) = \delta_{\gamma} \left(q , a\right)$:$\begin{matrix}s_{q^{'}} \leftarrow \exists \mathit{succ}_{\gamma}^{-} . \left(s_{q} \land h_{i} \land c_{a}^{\left(i\right)}\right) c_{b}^{\left(i\right)} \leftarrow \exists \mathit{succ}_{\gamma}^{-} . \left(s_{q} \land h_{i} \land c_{a}^{\left(i\right)}\right) h_{i + D} \leftarrow \exists \mathit{succ}_{\gamma}^{-} . \left(s_{q} \land h_{i} \land c_{a}^{\left(i\right)}\right) .\end{matrix}$Furthermore, the tape cells that are not under the read-write head have their content preserved. Thus, for each 1 ≤  *i*  ≤  *n*, and 1 ≤  *j*  ≤  *n* with $i≠j$, add $c_{a}^{\left(i\right)} \leftarrow \exists \mathit{succ}^{-} . \left(c_{a}^{\left(i\right)} \land h_{j}\right) .$

We now identify subtrees that represent accepting computations. For all *q*  ∈  *Q* <sub>∃</sub> and all *q* ′ ∈  *Q* <sub>∀</sub> we add the following:$\begin{matrix}s_{\mathit{acc}} \leftarrow s_{q_{\mathit{acc}}} s_{\mathit{acc}} \leftarrow s_{q} \land \exists \mathit{succ} . s_{\mathit{acc}} s_{\mathit{acc}} \leftarrow s_{q^{'}} \land \exists \mathit{succ}_{ℓ} . s_{\mathit{acc}} \land \exists \mathit{succ}_{r} . s_{\mathit{acc}} .\end{matrix}$This concludes the reduction.

As we assumed $|δ(q,a)|=2$ for all *q*  ∈  *Q, a*  ∈ Σ ∪ { *B* }, the run of $M$ on an input word *w* can be thought of as a binary tree with nodes in {0, 1}\* and edges *succ* <sub>ℓ</sub>  ≔ {(*x, x* 0)∣ *x*  ∈ {0, 1}\*} and *succ <sub>r</sub>*  ≔ {(*x, x* 1)∣ *x*  ∈ {0, 1}\*}, such that the root, ϵ, represents the input word, combined with the starting position of the head and the name of the starting state; and each other node of this tree represents the next configurations of the run, such that if some node *x* represents the word *e* <sub>1</sub> ⋅⋅⋅ *e <sub>n</sub>*  ∈ Σ\*, with the head in position *i* and state name *q*, such that $\delta_{ℓ} \left(q , e_{i}\right) = \left(q^{'} , a^{'} , D^{'}\right)$, then the left-child of this node, *x* 0, represents the word $e_{1} \hdots e_{i - 1} a^{'} e_{i + 1} \hdots e_{n}$, head position $i+D$ and state name *q* ′, and similarly for the child on the right, *x* 1, and *δ <sub>r</sub>* (*q, e <sub>i</sub>*).

Let *h* be an homomorphism of {0, 1}\* into $can(T,A)$. A simple check suffices to see that *x* represents the word *e* <sub>1</sub> ⋅⋅⋅ *e <sub>n</sub>*, head position *i* and state name *q* iff *h* (*x*) is decorated with the shape names $c_{e_{i}}^{\left(i\right)}$ for each 1 ≤  *i*  ≤  *n, h <sub>i</sub>* and *s <sub>q</sub>* in the perfect assignment.

An accepting run of $M$ on the input word *w* is a binary tree as described above such that there exists a (finite) subtree in which, if *x* represents a state name *q*  ∈  *Q* <sub>∃</sub> ∖{ *q <sub>acc</sub>* }, then either *x* 0 or *x* 1 is part of the subtree, and if *x* represents a state name *q*  ∈  *Q* <sub>∀</sub> ∖{ *q <sub>acc</sub>* }, then both *x* 0 and *x* 1 are part of the subtree. As we already concluded that *x* represents a state *q* iff *h* (*x*) is decorated with *s <sub>q</sub>* in the perfect assignment, and a decoration with *s <sub>acc</sub>* requires a state to be an accepting state, or one successor to be decorated with *s <sub>acc</sub>* in case of *x* representing a *Q* <sub>∃</sub> state, resp. two in case of a *Q* <sub>∀</sub> state, it is immediate that there exists such a subtree with all leaves representing the state name *q <sub>acc</sub>* iff we can decorate the root node *a* in $can(T,A)$ with the shape name *s <sub>acc</sub>*. Thus, $M$ accepts *w* iff $can(T,A)$ validates $(C,{sacc(a)})$.

## 10\. Discussion and conclusion

*Beyond normalised Horn-* $ALCHIQ$ In this article we considered Horn- $ALCHIQ$ TBoxes in normal form. Unfortunately, we cannot easily lift the results to general Horn- $ALCHIQ$, as our techniques are not immune to the usual normalisation procedures. For instance, the procedures in and may significantly change the form of the universal core model; the fresh concepts introduced during normalisation may force us to use different objects to satisfy axioms that would otherwise be satisfied by the same object. Take for instance the axiom *A* ⊑ ≥  <sub>2</sub> *r.B* and the ABox $A={A(a),r(a,b),B(b),r(a,c),B(c)}$. In this case, $A$ itself is a core universal model already. However, if we follow the normalisation as proposed in Lemma 2 of, we would find the following set of axioms, $T={A⊑∃r.B1,A⊑∃r.B2,B1⊑B,B2⊑B,B1⊓B2⊑⊥}$. It is easy to check that in the core universal model $can(T,A)$, *a* has four outgoing *r* -edges to a *B*, instead of two. We believe it is possible to obtain similar results for full Horn- $ALCHIQ$, albeit with a more cautious normalisation and a weaker notion of homomorphism. We leave the details for further work.

It would also be desirable to add transitivity axioms and thus cover the well-known Horn- $SHIQ$ description logic. But unfortunately, in the presence of transitive roles, the uniqueness of the core universal model can no longer be guaranteed: take for instance $A={A(a)}$ and $T={A⊑∃r.B,A⊑∃r.B′,B⊑∃r.B′,B′⊑∃r.B}$ where *r* is transitive. In this case, there are two (not strong) core universal models: a chain of *r* ’s such that the concept names along this chain are, in the first node *A*, and then *B* and *B* ′, in an alternating fashion, closed under transitive roles, and the version in which *B* and *B* ′ swap places. Note that there exist (non-surjective) homomorphisms between both models. It is unclear what would be a good semantics if multiple core universal models exist.

*Towards full SHACL* Extending the considered SHACL fragment is also a promising avenue. However, we first point that the ‘guard’ *c* we introduced for constraints of the forms $eq(E,r)$ and $disj(E,r)$, cannot easily be dropped. Without it, the normalisation as described in the proof of does not work well. There is no straightforward way to distinguish from which starting point it was possible to reach a final state, as becomes clear in the following example.

**Example 10.1**

Let $A={r(a,c),t(b,c)}$. Over this graph, we wish to check validation for the constraint $s←eq(r,t)$ with targets *s* (*a*) and *s* (*c*). Clearly, we expect non-validation. However, this cannot easily be achieved by a similar rewriting technique.

To see this, let us consider the following constraints as, loosely following the construction above to rewrite $s←eq(r,t)$ and based on the automata $M=({q,q′},{r,t},q,{(q,r,q′)},q′)$ and $M′=({q″,q″′},{r,t},q″,{(q″,t,q″′)},q″′)$ we find the following constraints:$\begin{aligned}s_{q} & \leftarrow a s_{q} \leftarrow c s_{q^{'}} \leftarrow \exists r^{-} . s_{q} s_{\mathit{pos}} \leftarrow s_{q^{'}} s_{\mathit{neg}} \leftarrow \neg s_{q^{'}} s_{q^{''}} \leftarrow a s_{q^{''}} \leftarrow c s_{q^{'' '}} \leftarrow \exists t^{-} . s_{q^{''}} \\ s_{\mathit{pos}} & \leftarrow s_{q^{'' '}} s_{\mathit{neg}} \leftarrow \neg s_{q^{'}} s_{\mathit{e}} \leftarrow s_{\mathit{pos}} \land s_{\mathit{neg}} s_{\mathit{e}} \leftarrow \exists r . s_{\mathit{e}} s_{\mathit{e}} \leftarrow \exists t . s_{\mathit{e}} s_{\mathit{noe}} \leftarrow \neg s_{\mathit{e}} s \leftarrow s_{q} \land s_{\mathit{noe}}\end{aligned}$ where we shortened the names of the error-shapes to *s <sub>e</sub>* and *s <sub>noe</sub>*. As *b* is reachable from starting states *a* and *c* by both an *r* and a *t, b* will only be assigned *s <sub>pos</sub>*, the shape name denoting being the final state of at least one of the automata, not causing any error-shape *s <sub>e</sub>* to fire, which breaks our expectation of non-validation. The problem is that we cannot distinguish which initial state caused the positive outcome.♥

For non-recursive SHACL, it is known that adding path equality or disjointness increases expressivity, but we do not know whether this also holds for recursive SHACL. In any case, it seems hard to include full path equality and disjointness due their ‘non-local’ nature.

On the other hand, it might be possible to encode local counting constraints of the form ∃ <sub>≤  <em>n</em></sub> *r*.φ, after a careful examination of our techniques. Extending counting over roles to counting over regular paths is even more interesting. It will be quite a challenge to also define a rewriting in which the quadruples store information on counting over regular paths. However, as the anonymous parts of the core universal model are tree-like, it might be possible to also achieve such a rewriting.

In parallel to increasing the expressivity of the considered shape expressions, we may also consider richer targets. Additionally to shape atoms, the SHACL standard considers *target classes*: if a concept name *A* is given as target, all nodes in the interpretation of *A* must validate the given shape. For plain validation, without ontologies, class targets reduce trivially to sheer shape atoms: the set of domain elements is known and can replace the class or concept name. But if ontology axioms are given, this is a whole different story: the set of domain elements that forms the interpretation of the target concept name is not known a priori. Nevertheless, under the assumption that the input data graph is connected, it is possible to model this for *s*  ← φ with target class *A*, by creating new constraints of the form “there does not exists a path (the Kleene star of the union of all roles appearing) to an *A* that does not satisfy φ”. Now any domain element in the graph can be considered as the target to get a logically equivalent constraint. Clearly, a similar trick works if it is known which parts of the graph are connected.

Finally, we would like to emphasise that allowing full negation would be a very nice, but complicated challenge.

*Conclusion* We have considered the validation of SHACL constraints in the presence of normalised Horn- $ALCHIQ$ ontologies. To this end, we defined the semantics over a carefully constructed notion of a canonical model that minimises the number of fresh successors introduced to satisfy the ontology axioms at each chase step and which happens to be the unique core universal model. Moreover, we have argued that this semantics is natural and intuitive. We proposed a normal form and a rewriting algorithm for recursive SHACL constraints with *stratified* negation. It takes as an input a SHACL shapes graph and an ontology, and constructs a new SHACL shapes graph (also with stratified negation) that can be used for sound and complete validation over a slightly extended version of the data graph alone, without needing to reason about the ontology at validation time. We also discussed some approaches to even get to validation over the pure data graph. We showed that, under our semantics, validation in the presence of normalised Horn- $ALCHIQ$ is complete for ExpTime, but it remains PTime complete in data complexity, and hence it is not harder than validation of stratified SHACL alone, without the ontology axioms.

## CRediT authorship contribution statement

**Anouk Oudshoorn:** Writing – original draft, Validation, Formal analysis, Conceptualization. **Magdalena Ortiz:** Writing – review & editing, Supervision, Methodology, Funding acquisition, Conceptualization. **Mantas Šimkus:** Writing – review & editing, Supervision, Methodology, Conceptualization.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Acknowledgements

The project leading to this application has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement No 101034440.

This work was partially supported by the Wallenberg AI, Autonomous Systems and Software Program (WASP) funded by the Knut and Alice Wallenberg Foundation. In addition, Šimkus was supported by the Austrian Science Fund (FWF) \[\], Ortiz was supported by the Austrian Science Fund (FWF) \[\] and Oudshoorn was supported by the Netidee stipend 6794.

## Data availability

No data was used for the research described in the article.

## References

The impossibility of such a rewriting for SHACL with negation given in of does not hold, neither for our semantics nor for the minimal-model semantics adopted in that work, as acknowledged by the authors in personal communication, and shown by the results of this work.

The conclusion of rule **R** <sub>≤</sub> should be updated to *M* ⊓ *M* ′⊓ *A* ⊑∃(*S* ⊓ *S* ′⊓ *r*).(*N* ⊓ *N* ′⊓ *B*), as confirmed by the authors of.