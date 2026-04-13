---
title: "Quantifying Curriculum Degradation: Evidence from the University of Chicago"
source: "https://hxstem.substack.com/p/quantifying-curriculum-degradation?utm_source=post-email-title&publication_id=618970&post_id=190430107&utm_campaign=email-post-title&isFreemail=true&r=7br8e&triedRedirect=true&utm_medium=email"
author:
  - "[[Iván Marinovic]]"
published: 2026-03-15
created: 2026-03-15
description: "1."
tags:
  - "brain_spew"
---
[Ideology](https://hxstem.substack.com/s/ideology/?utm_source=substack&utm_medium=menu)

### 1\. Introduction

American universities—especially in the humanities and social sciences—have undergone a decades-long shift away from the Western intellectual tradition and toward ideological and activist content (see Bloom 1987; Dewey 1916). We present a keyword-based methodology for quantifying this process using course catalog data. Applying it to thirteen years of University of Chicago catalogs (2012–2025), we find that the progressive-signal share of the catalog more than doubled from 12.7% to 28.3%, while the Western-canon signal remained flat at ≈12%, causing the progressive-to-canon ratio to rise from 1.0× to 2.4×. These patterns are most pronounced in the humanities and social sciences, yet, perhaps unexpectedly, they also extend into STEM fields. We propose a collaborative, open index of curriculum content at the university-year level to help families, donors, and policymakers make informed decisions.\*

*\* Policymakers should refrain from the temptation to micro-manage the university curriculum. Such attempts will likely be counterproductive to the goal of promoting and revitalizing the Western tradition.*

### 2\. Methodology

We classify every course in a university catalog using two keyword lists: a progressive list and a Western canon list, as described below. We assign a course to a category if its title or description contains at least one keyword from the category’s keyword list.

We matched via word-boundary regular expressions on the combined title and description text (case-insensitive). Word-boundary matching ensures that partial matches are avoided (e.g., the term “race” does not match “interface” or “brace”). Each course’s title and description are concatenated into a single text field; if any keyword from a given list appears within that text, the course is flagged for that category.

The progressive keyword list comprises approximately 55 terms and phrases signaling engagement with progressive social frameworks, diversity/equity/inclusion initiatives, or critical identity scholarship. These terms are organized into eleven thematic sub-categories, shown in Table 1.

![](https://substackcdn.com/image/fetch/$s_!GsqW!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa3418700-07c0-4248-9a5a-c139c7ae476a_1580x940.png)

Table 1: Progressive-signal keyword list by thematic category.

The Western canon keyword list comprises approximately 45 terms and phrases signaling engagement with the traditional Western intellectual and literary canon, spanning classical antiquity through the Enlightenment. These terms are organized into six thematic sub-categories, shown in Table 2.

![](https://substackcdn.com/image/fetch/$s_!oNP1!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb50db54f-f82c-4d81-87c5-ebf68927f926_1580x638.png)

Table 2: Western-canon keyword list by thematic category.

#### 2.1 Classification rules and interpretation

A course may match both lists, one, or neither. The categories are non-exclusive: for example, a seminar on Aristotle’s political philosophy that also discusses social justice concepts would be flagged under both the canon and progressive signals.

We acknowledge the limitations of this type of analysis. The signals are coarse and are likely to yield many false positives and false negatives. The signals are also easily manipulable. A university can manipulate signals by avoiding these terms without changing the substance of what is taught to students. The value of these signals, however, lies in tracking changes over time and differences across institutions.

### 3\. An Example: The University of Chicago

The University of Chicago occupies a unique position in American higher education. Its undergraduate Core Curriculum, built on the Hutchins-era Great Books model, has historically been the strongest institutional commitment to the Western canon at any major research university. If curriculum degradation is occurring even at Chicago, it is likely occurring everywhere.

We extract course data from thirteen annual catalogs (2012–2013 through 2024–2025). After deduplicating crosslisted courses, which appear under multiple department codes, we obtain 21,381 unique courses across 114 departments. Departments are mapped to broad areas: Humanities, Social Sciences, STEM, Professional, and Other.

Figure 1 presents the central finding. The progressive signal rose from 12.7% of the catalog in 2012–2013 to 28.3% in 2024–2025—more than doubling over thirteen years. The canon signal dropped from 13.2% to 11.9%. The progressive-to-canon ratio consequently rose from 1.0× (parity) to 2.4×.

![Progressive and canon signal shares over time](https://substackcdn.com/image/fetch/$s_!qnGx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1335fb63-398d-4e87-a89d-e2c023f27bb4_1600x791.png)

Figure 1: Progressive and canon signal shares, 2012–2024.

Table 3 shows that the progressive signal is highest in the Social Sciences (27.4%) and Humanities (24.6%). The progressive signal is naturally lower in STEM (7.6%) but still unexpectedly high given the technical nature of STEM content.

![](https://substackcdn.com/image/fetch/$s_!8jEW!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F45df1880-ba24-4088-bc20-9c95c1e5ff33_1524x388.png)

Table 3: Signal prevalence by academic area (all years pooled).

### 4\. Toward a Curriculum Content Index

Quantifying curriculum content across institutions and over time could serve the same function as the FIRE Free Expression Rankings: providing transparent, comparable data that families, donors, legislators, and University administrators can use to make informed decisions.

We envision a **Curriculum Content Index (CCI)** at the university-year level, constructed from publicly available course catalog data and syllabi. Ideally, one should also include student enrollment data to get a more accurate understanding of the content students are actually learning from universities. Perhaps understandably, universities are reluctant to share this information. But transparency is the best disinfectant here.

Such an index would allow prospective students to assess how much of a university’s catalog engages the Western intellectual tradition versus ideological content; donors to direct funding toward institutions that maintain intellectual breadth, and policymakers to monitor trends and evaluate the effects of reform efforts.

Building such an index requires data from many institutions. We invite scholars, students, administrators, and concerned citizens to collaborate on this project by contributing course catalog data—whether in CSV, PDF, or other machine-readable formats—and by helping to refine the keyword methodology. The analysis code and data for the University of Chicago is publicly available [at this link](https://drive.google.com/drive/folders/1z3itoda-HlU1rg5BC8hf_gqylRynF47r?usp=sharing), and the methodology is designed to be simple enough that any institution’s catalog can be processed in a few hours.

A word of caution is in order. Keyword-based textual analysis of course descriptions is a blunt instrument. A course flagged by our progressive keyword list may turn out, on closer inspection, to be a rigorous scholarly treatment of the topic; conversely, a course that escapes detection may nonetheless promote an activist agenda in practice. The signals we measure should therefore be understood as a noisy first approximation—useful for identifying broad trends and prompting further inquiry, but never a substitute for substantive evaluation of what is actually taught. Policymakers, in particular, should resist the temptation to use simple keyword counts as the basis for funding decisions or regulatory action. Our goal is to promote transparency and informed conversation, not to supply a scorecard that short-circuits careful judgment.

### References

Bloom, Allan. 1987. *The Closing of the American Mind: How Higher Education Has Failed Democracy and Impoverished the Souls of Today’s Students.* New York: Simon and Schuster.

Dewey, John. 1916. *Democracy and Education.* New York: Macmillan.

---