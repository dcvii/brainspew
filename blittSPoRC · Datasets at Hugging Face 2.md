---
title: "blitt/SPoRC · Datasets at Hugging Face"
source: "https://huggingface.co/datasets/blitt/SPoRC"
author:
published: 2024-11-12
created: 2026-01-22
description: "We’re on a journey to advance and democratize artificial intelligence through open source and open science."
tags:
  - "clippings"
---
## You need to agree to share your contact information to access this dataset

This repository is publicly accessible, but you have to accept the conditions to access its files and content.

License agreement  
We, the researchers at the University of Michigan, provide access to the SPORC dataset under the following conditions. By selecting 'I agree' the researcher agrees to the following

1. the SPORC dataset must only be used for research or education purposes. Use of this resource for malicious purposes violates this agreement. This resource should not be used for financial gain or profit.
2. If you want to use the SPORC dataset for other purposes, please check the terms of use for each individual original data source.
3. There is no warranty regarding the SPORC dataset. We cannot be held liable for providing access to this resource.
4. This resource should not be provided to any third party.
5. The researcher takes full responsibility for consequences resulting from usage of the provided resource.
6. If any part of this agreement is found to be invalid, this should not affect the other parts of the remaining agreement.

By agreeing you accept to share your contact information (email and username) with the repository authors.

## SPORC: the Structured Podcast Open Research Corpus (V 1.0)

SPORC is a large multimodal dataset for the study of the podcast ecosystem. Included in our data are podcast metadata, transcripts, speaker-turn labels, speaker-role labels, and speaker audio features. For more information on the collection and processing of this data alongside an initial analysis of the podcast ecosystem please refer to our paper [here](http://arxiv.org/abs/2411.07892) or our github repositories for [analysis](https://github.com/blitt2018/SPoRC_analysis) and [data processing](https://github.com/blitt2018/SPoRC_analysis).

Our dataset is comprised of two tables linked through the podcast episode mp3 urls -- a unique key. The first table provides episode-level information about each podcast such as the transcript, publication date, category, inferred host and guest names, and more. Our second table provides speaker turn-level information such as generic speaker labels (e.g. SPEAKER\_03), inferred roles where available (e.g. "host"), the text spoken by speaker(s) for a given turn, and the average audio features for speakers over a given turn. We also provide sample versions of this data with the first 10,000 rows at the episode-level and the first 200,000 rows at the speaker-turn level. Usage of our data is conditional on agreement to our data-usage terms. Furthermore, we provide a [*removal form*](https://forms.gle/qkxQrf8eAr7FaAec7) for podcast creators who would like their content removed from the data.

## Important Columns:

While a number of our columns at the episode-level may be self evident based on their name, certain columns contained information that is inferred or is an indicator of data quality.

**overlapPropDuration**: *Important indicator diarization quality.* The proportion of an episode that has been assigned to multiple speakers. Indicates how often speakers are found to overlap.

**overlapPropTurnCount**: *Important indicator of diarization quality.* The proportion of speaker turns with multiple assigned speakers. Indicates how often speakers are found to overlap.

**avgTurnDuration**: *Potential indicator of diarization quality.* The average duration of speaker turns.

**totalSpLabels**: *Potential indicator of diarization quality.* The total number of speaker labels with any speaking time in the episode. Contrast with the "mainEpSpeakers" column.

**hostPredictedNames**: Names of predicted hosts using our NER + role-inference model.

**guestPredictedNames**: Names of predicted guests using our NER + role-inference model.

**neitherPredictedNames**: Names not predicted to be either hosts or guests using our NER + role-inference model.

**mainEpSpeakers**: The speakers in this episode with over 5% of the speaking time based on our diarization output.

**numMainSpeakers**: The number of "mainEpSpeakers"

**hostSpeakerLabels**: A dictionary mapping the name of hosts to their speaker labels in the diarization data. This is done using the heuristic that the first speaker to mention the host's full name is the host.

**guestSpeakerLabels**: A dictionary mapping the name of guests to their speaker labels in the diarization data. Guests are inferred only for the case where 2 main speakers are present and the host is identified in "hostSpeakerLabels" -- leaving only one speaker to be the guest.

Downloads last month

74

[Edit dataset card](https://huggingface.co/datasets/blitt/SPoRC/edit/main/README.md)