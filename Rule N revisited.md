---
title: Rule N revisited
source: https://climateaudit.org/2014/09/03/rule-n-revisited/
author:
  - "[[Jean S]]"
published: 2014-09-03
created: 2026-06-28
description: PCA was also performed on certain proxy sub-networks (spatially dense regional networks of tree-ring data available separately in different continents) as means of dimensional reduction of the predictor network. In this case, the procedure was performed separately for each independent step of the stepwise calibration/reconstruction procedure described in "3" below. A decreasing number of PCs…
tags:
  - brain_spew
  - climate_change
---
> PCA was also performed on certain proxy sub-networks (spatially dense regional networks of tree-ring data available separately in different continents) as means of dimensional reduction of the predictor network. In this case, the procedure was performed separately for each independent step of the stepwise calibration/reconstruction procedure described in “3” below. A decreasing number of PCs of these sub-networks are retained increasingly further back in time, as dictated by application of objective selection criteria (consideration of results of both Preisendorffers Rule N and Scree test).
> 
> ***MBH98 Corrigendum***

> We employed a standard, objective criterion for determining how many PCs should be kept for each region.
> 
> ***Michael E. Mann in his book.***

Let’s continue with another housekeeping post.

When Steve and Ross uncovered Mann’s flawed PCA, Mann’s defence was that MM had failed to use Preisendorfer’s Rule N in the selection of the PCs in the NOAMER AD1400 step (for the background of this story, see [here](https://climateaudit.org/2008/03/14/mbh-pc-retention-rules/) or read it from Montford’s excellent book). Steve observed immediately that the use of “Rule N” was not mentioned in MBH98 in connection to the tree ring PCA. He then [emulated the claimed rule](http://www.climateaudit.info/data/climate2003/pages/blog/preisendorfer.MBH98.htm) convincingly showing that it was pretty impossible that the rule was actually used. Further, up to now Mann has failed to reproduce any code or documentary evidence for the supposed use of the rule. It is hard to imagine, even in the context of the Hockey Stick, any other argument with so little support but which is still alive and well with the usual suspects. In fact, this fairy tale now seems to be the official story line in [Wikipedia](https://en.wikipedia.org/wiki/Hockey_stick_controversy#Principal_components_analysis_methodology) (citing Mann’s book, of course).

When I got my hands in the MBH9X file archive contained in the Climategate files, among the first things I checked was that if it contained the code for the selection rule, or even a file indicating the use of such code. Nope. Later I observed a curious thing in the files. MBH9X is a stepwise procedure, and in every step (if there were enough proxies), one supposedly (as the Corrigendum statement indicates) calculated the tree ring PCs. However, there were quite a few calculation steps missing from the archive. For instance, Stahle & Cleveland Oklahoma/Texas (STAHLE OK) precipitation chronologies had a single calculation step (AD1700) although they were also used in the later steps (AD1730, AD1750, AD1760, AD1800, and AD1820). I then checked the actual MBH98 data, and vola, I noticed that instead of calculating the PCs for the STAHLE OK network at, say, AD1820 step Mann had simply recycled the 1820-1980 part of the AD1700 step PCs (1700-1980)! The correspondence between the archive and the PCs actually used was almost one-to-one: every “missing” step in the archive matched the reuse of the PCs from the previous step in the MBH98 data. In other words, contrary what is claimed in the Corrigendum PCs were not calculated for every step.

So what has the above to do with the PC selection rule? Well, [Steve had observed](http://www.climateaudit.info/data/climate2003/pages/blog/preisendorfer.MBH98.htm) that there are three (\*) cases (SOAMER AD1750, STAHLE SW AD1750, and NOAMER AD 1500), where MBH98 retains more PCs than in the previous step although the network does not change (i.e., the same proxies are inputs to the PCA). But it was not only that the network was (supposed to be) the same … *the PCs were exactly the same* as in the previous step! Of course then, it is impossible for any “rule” to retain different number of PCs. The most striking example comes from the NOAMER AD1500 step, which is using PCs from the AD1450 step. Mann is keeping 2 PCs in the AD1450 step, but in AD1500 step 6 PCs are retained from the same PC set!

As Steve has said several times, MBH9X is the gift that keeps on giving! When now preparing for this post, I discovered yet-another Mannian mystery. There is a single exception to the above mentioned correspondence between the archive and PCs actually used. Namely, PCs are calculated for the SOAMER AD1450 step, but no SOAMER PCs are used prior the AD1600 step. The corrigendum text cited in the beginning continues

> PCs were no longer calculated back in time once a given network contained fewer than 7 available series (with the exception that PCs were calculated for the ‘Stahle Southwest U.S./Mexico network’ with 6 series available). Thus, although some series may be available further back in time, they may not have been used to calculate PCs. For example,there are 110 series available back to 1400, but only 95 are used because PCs were not calculated on 6 Australian and 6 South American ITRDB series and 3 ‘Vaganov’ series.

SOAMER contains 7 series in the AD1450 step. Why were none of those PCs used?

(\*) Actually there is a fourth case (AUSTRAL AD1750), which is immaterial here as it has the corresponding calculation step in the archive.