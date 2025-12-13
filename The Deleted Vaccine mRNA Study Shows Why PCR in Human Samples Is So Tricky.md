---
title: "The Deleted Vaccine mRNA Study Shows Why PCR in Human Samples Is So Tricky"
source: "https://www.usmortality.com/p/the-deleted-vaccine-mrna-study-shows?publication_id=631983&post_id=181297257&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[US Mortality]]"
published: 2025-12-10
created: 2025-12-11
description: "When your primers accidentally match the human genome"
tags:
  - "clippings"
---
### When your primers accidentally match the human genome

Last month, a study from Israel made waves claiming Pfizer vaccine mRNA persists in blood, placenta, sperm and seminal fluid - still detectable in 50% of women over 200 days after their last dose.

Even stranger: they claimed to find it in 3 of 6 unvaccinated pregnant women.

Then the study vanished - not retracted, just deleted.

I decided to check their primers. What I found illustrates a fundamental challenge with PCR and the so-called human genome…

**TL;DR:** The study used faulty primers that match the human genome, so they detected human DNA instead of vaccine mRNA - that’s why 50% of unvaccinated people tested “positive”.

All details below:

## Analysis of the Deleted Mordechay et al. Study on Vaccine mRNA Detection

## The Study’s Claim

A study published in October 2025 claimed to detect Pfizer vaccine mRNA in blood, placenta, and semen of vaccinated individuals - and remarkably, in **50% of unvaccinated women** too. The study was **completely deleted** (not retracted) shortly after publication.

I analyzed their primer sequences against the human genome. Here’s what I found.

## The Primers: 8 Out of 12 Were Unusable

The researchers designed 12 PCR primers to detect “vaccine-specific” sequences:

![](https://substackcdn.com/image/fetch/$s_!dazK!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c72b4e4-29a1-44e1-9358-4549b383af12_1846x318.png)

The authors admitted the UTR primers gave “non-specific amplification” - because Pfizer used human gene sequences for the vaccine’s regulatory regions. **Only the 4 spike-region primers were used.**

## The Problem: Those 4 “Vaccine-Specific” Primers Match the Human Genome

I BLASTed all 4 primers against the human reference genome (GRCh38.p14):

![](https://substackcdn.com/image/fetch/$s_!VS-u!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fca9e25e2-936b-484b-9a28-aaed535b4e61_1854x316.png)

**The nested forward primer is a PERFECT match to human chromosome 1.**

## Why This Matters for PCR

The study used **nested PCR** \- two rounds of amplification:

\- Round 1: Outer primers (20 cycles)

\- Round 2: **Nested primers (30 cycles)** \- generates the final product

With **50 total cycles** and primers that match human DNA:

\- The nested forward primer (100% human match) **will bind human DNA**

\- The 18/20 matches (90%) **can still bind** \- PCR tolerates 1-2 mismatches, especially at the 5’ end

\- Any human sample could potentially give a “positive” result

## The Unvaccinated Results Make Sense Now

From the study’s own data:

![](https://substackcdn.com/image/fetch/$s_!e2lx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff94cc449-1f76-4632-9626-0f21e808666e_1856x286.png)

The detection rate in vaccinated people **drops to the same level as unvaccinated** over time. This suggests the ~50% “baseline” is likely **assay noise from human DNA cross-reactivity**, not vaccine mRNA.

3 of 6 unvaccinated women tested “positive” - exactly what you’d expect if the primers are amplifying human sequences.

## Conclusion

The study’s “vaccine-specific” primers are not vaccine-specific at all:

\- **1 primer perfectly matches human chromosome 1**

\- **3 primers match human DNA at 18/20 bases** (sufficient for PCR binding)

\- The 50% positive rate in unvaccinated people likely reflects **human DNA amplification, not vaccine detection**

This is a fundamental primer design flaw that should have been caught by:

1\. The researchers (basic BLAST check before experiments)

2\. Peer reviewers

3\. The journal editors

## Why Deleted Instead of Retracted?

Speculation:

\- **Retraction requires a formal process** \- investigation, author response, public record

\- **Deletion leaves no trace** \- no DOI, no retraction notice, no explanation

\- The flaw is so fundamental (primers match human genome) that it’s not a “mistake” that can be corrected - **the entire study is invalid**

\- A retraction notice explaining “our vaccine-specific primers match human DNA” would be embarrassing and quotable

\- Deletion allows the journal and authors to pretend it never happened

## TL;DR

Researchers claimed to find vaccine mRNA in 50% of unvaccinated people. Their “vaccine-specific” detection method uses primers that match the human genome - including one **perfect 20/20 match to chromosome 1**. They were likely detecting human DNA, not vaccine mRNA. The study was deleted rather than retracted, leaving no public record of what went wrong.

\---

## Technical Details

### BLAST Results Against GRCh38.p14

**\*\*Primer 1 -** \`CGTGATCCGGGGAGATGAAG\` **(1254 F outer):\*\***

\- NC\_000016.10 (Chromosome 16), position 6,834,975-6,834,994: 90% identity (18/20, 2 mismatches)

**\*\*Primer 2 -** \`ACTTCACCGGCTGTGTGATT\` **(1337 F nested):\*\***

\- NC\_000001.11 (Chromosome 1), position 33,048,488-33,048,507: **\*\*100% identity (20/20, 0 mismatches)\*\***

**\*\*Primer 3 -** \`TGCTGGAATGGCAGGAACTT\` **(1745 R nested):\*\***

\- NC\_000012.12 (Chromosome 12), position 55,432,051-55,432,070: 90% identity (18/20, 2 mismatches)

**\*\*Primer 4 -** \`GGGATCTCTAACGGCGTCTG\` **(1791 R outer):\*\***

\- NC\_000003.12 (Chromosome 3), position 187,273,415-187,273,434: 90% identity (18/20, 2 mismatches)

## Study Reference

Mordechay L, Baum G, Gabbay-Benziv R, Weinberger H, Morgenstern MF. (2025). Detection of Pfizer BioNTech Messenger RNA COVID-19 Vaccine in Human Blood, Placenta and Semen. Ann Case Rep 10: 2428. DOI: 10.29011/2574-7754.102428

*Archived version: https://web.archive.org/web/20251205172931/https:/www.gavinpublishers.com/assets/articles\_pdf/Detection-of-Pfizer-BioNTech-Messenger-RNA-COVID-19-Vaccine-in-Human-Blood-Placenta-and-Semen.pdf*