---
title: "How Colds Spread — LessWrong"
source: "https://www.lesswrong.com/posts/92fkEn4aAjRutqbNF/how-colds-spread"
author:
  - "[[RobertM]]"
published: 2025-11-17
created: 2025-11-23
description: "It seems like a catastrophic civilizational failure that we don't have confident common knowledge of how colds spread.  There have been a number of s…"
tags:
  - "clippings"
---
It seems like a catastrophic civilizational failure that we don't have confident common knowledge of how colds spread. There have been a number of studies conducted over the years, but most of those were testing secondary endpoints, like how long viruses would survive on surfaces, or how likely they were to be transmitted to people's fingers after touching contaminated surfaces, etc.

However, a few of them involved rounding up some brave volunteers, deliberately infecting some of them, and then arranging matters so as to test various routes of transmission to uninfected volunteers.

My conclusions from reviewing these studies are:

- You can definitely infect yourself if you take a sick person's snot and rub it into your eyeballs or nostrils. This probably works even if you touched a surface that a sick person touched, rather than by handshake, at least for some surfaces. There's some evidence that actual human infection is much less likely if the contaminated surface you touched is dry, but for most colds there'll often be quite a lot of virus detectable on even dry contaminated surfaces for most of a day. I think you can probably infect yourself with fomites, but my guess is that it's mostly aerosolized particles.
- Small particle aerosol transmission [^1] seems unlikely to transmit the tested cold viruses, but the meta-analysis is more equivocal than I am on that question.
- Sitting directly across a table from an infected person, or otherwise having a face-to-face conversation with them, seems pretty risky. A separate "close-quarters" study suggests that likelihood of infection increased (approximately) logarithmically with hours of exposure, with a 50% likelihood at about 200 infected-person-hours of sharing space.

## Fomites

This section may as well be called Gwaltney & Hendley, as they conducted basically all of the studies [^2] suggesting that fomites might be a substantial vector of transmission.

[Gwaltney et al., 1978](https://pubmed.ncbi.nlm.nih.gov/205151/) conducted three separate trials, each attempting to test a different method of transmission.

The **large particle test** [^3] had 1 donor and 2-4 recipients sitting around a small table (0.7m diameter). Donors were instructed to talk loudly, sing, cough, and sneeze for the 15-minute period. Everyone wore rubber gloves while in the room. 1 [^4] out of 12 total recipients were infected.

The **small particle test** housed donors and recipients (1 or 2 recipients per donor - 6 donors & 10 recipients total) together for *3 successive days and nights* in a large, closed room, separated by a double wire-mesh barrier to preclude direct contact. Everyone spent all their time in the common room except when in the adjoining bathrooms, or when the donors were being borrowed to expose other recipient groups in other arms of the experiment.

This resulted in zero infections! It seems like moderately strong evidence to me, and makes me update on small particle transmission being less likely; I don't see obvious ways in which this test fails to replicate relevant real-world conditions.

In **the fomite test**, "donors deliberately contaminated their hands with nasal secretions as they would when blowing their nose". Then they performed a 10-second handshaking procedure with recipients, both sides wearing surgical masks. Recipients then went to another room and self-inoculated by putting their fingers "on their nasal and conjunctival mucosa as they might under natural conditions", two to three times (then washed their hands).

This infected 11 out of 15 recipients. Ok, if you go directly from a wet handshake to rubbing your eyes, you're in trouble, noted. It's not clear how this generalizes to more realistic [^5] patterns of fomite transmission. Do people even shake hands nowadays?

[Gwaltney & Hendley, 1982](https://pubmed.ncbi.nlm.nih.gov/6293304/) directly tested fomite transmission via shared surface contact. This lets us screen off the risk of accidentally mistaking unintended aerosol transmission for fomite transmission. To summarize, they had donors blow and/or wipe their noses with their fingers, briefly handle a coffee cup or rub a plastic tile. They then gave those objects to the recipients to touch, and had the recipients put their fingers "in contact with the conjunctival and nasal mucosa" (i.e. rub their eyes or pick their nose).

Twenty minutes passed between donors contaminating the tiles and recipients touching them. (Ten minutes on each side of "either apply disinfectant, or not".) The period of time between the contamination and then handling of the coffee cup handles wasn't specified, sadly.

5 of 10 coffee cup recipients, 9 of 16 unsanitized plastic tile recipients, and 7 of 20 sanitized [^6] plastic tile recipients became infected.

This seems like pretty strong evidence that indirect transmission via shared surface contact is possible. My prior on that was very high (especially given the previous study); it would be pretty surprising if it turned out that skin contact was load-bearing here. The self-inoculation procedure seems pretty similar, so we don't get much evidence about how effective this route is under "more realistic" conditions.

I also looked at a couple "secondary metric" studies, just to check whether there was anything very surprising there.

[Ansari et al. 1991](https://pmc.ncbi.nlm.nih.gov/articles/PMC270283/) tested how much virus survived on both people's fingers and metal disks, when directly applied. tl;dr:

- Human parainfluenza virus 3 (HPIV-3): <1% of virus remained viable after 1 hour [^7].
- Human rhinovirus B14 (RV-14): 37.8% viable after 1 hour; ~16% still detectable after 3 hours

Maybe significant for HPIV-3, but rhinoviruses comprise most "common colds", and those seem to stick around for a while.

[Winther et al. 2007](https://pubmed.ncbi.nlm.nih.gov/17705174/) tested two things:

1. What percentage of environmental sites sampled in hotel rooms occupied by cold sufferers were contaminated [^8] with rhinovirus RNA (35%, and the types of things you'd expect - "door handles, pens, light switches, TV remote controls, faucets, and telephones").
2. How likely fingertip rinses were to test positive for virus after touching deliberately-contaminated objects (not the same as the naturally-contaminated sites from the above), both 1 hour and 18 hours after contamination. "Rhinovirus was transferred from surfaces to fingertips in 18/30 (60%) trials 1 hr after contamination and in 10/30 (33%) of trials 18 hr (overnight) after contamination."

The study didn't test for the last leg, i.e. actual infectivity.

## Aerosols

And this section, correspondingly, consists entirely of studies that include Elliot C. Dick as an author.

[D’Alessio et al., 1984](https://pubmed.ncbi.nlm.nih.gov/6088645/) ran 3 types of experiments with a total of 33 recipients. I'm really hesitant to draw conclusions from this one, because it had some surprising results that I think represent methodological issues.

The first experiment type had donors and recipients playing cards, talking, and singing together in a room for 2-3 hours. Across two rounds, there were 5 donors and 9 recipients. The researchers claim that none of the recipients were infected with RV55 (which they infected the donors with), but see this footnote to the data table for that experiment:

> Three colds developed in recipients during the week after inoculation, but RV55 was not isolated from multiple nasal specimens, nor did antibody to RV55 appear in serum after the experiment. Three nasal specimens were obtained from each of the six asymptomatic recipients after exposure to RV55; tests of all of these specimens yielded negative results, as did serological tests.

So who knows, really.

The second experiment type had small groups of donors and recipients sharing dormitory rooms for 12 hours a day, 3 days in a row, and "to decrease the likelihood of transmission by fomites, participants were asked to avoid handling one another's personal items and to use separate bathrooms". There were 11 donors and 11 recipients, with 5 groups of 2 each, and 1 group of 1 each. The results from this experiment are reported as "one infection", but once again:

> Three recipients developed colds, but only one case of transmission of RV55 was confirmed by laboratory findings.

🤔

The third had donors kissing recipients: "Forty-eight hours after being infected with RV55, four donors kissed five recipients for 1 min. A second group of six donors, similarly infected, kissed 11 recipients for 1.5 min (two 45-sec contacts). Each recipient was kissed only once; the donors and recipients were instructed to use the kissing technique most natural for them." They report only one instance of transmission here (recipient no. 16), with this caveat:

> In four recipients (no. 1, 6, 8, and 12), cold-like symptoms developed during the week after exposure to RV55, but seroconversion did not occur and RV55 was not isolated from nasal specimens. A rhinovirus other than RV55 was isolated from recipient no. 8.

As I said above, the methodology here seems much less careful and the results are substantially sketchier; how likely is it that so many test subjects just happen to coincidentally catch a *different* cold after being exposed to one in the experimental setting?

[Dick et al., 1987](https://pubmed.ncbi.nlm.nih.gov/3039011/) had a very interesting, and substantially more robust, experimental design. The first stage, which they ran 3 times, was sticking 20 guys into a room with 4 tables. 8 of those guys had colds, 12 were healthy - each table took 2 infected and 3 uninfected guys. Half (6) of the uninfected guys wore restraining devices meant to prevent them from touching their faces. In the first of the 3 rounds, this device was a "large, clear plastic collar... worn around the neck and supported by the shoulders".

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/92fkEn4aAjRutqbNF/yo1qwrzzmvykwwv6fjcf)

Importantly, not a dog cone.

In the second and third rounds, they wore arm restraints "composed of two halves of an orthopedic arm brace held together at the elbow by a moveable hinge welded so that the brace could bend only between 140°and 180°. Both devices enabled effortless movement of the arms, ensuring normal poker playing but preventing the wearer from touching any part of his face. If any of the restrained recipients needed his nose blown or scratched, assistance was given by a monitor."

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/92fkEn4aAjRutqbNF/gzz6frmiwmawxn3wxsny)

They then had them play cards together at these tables for 12 hours. (They also went through quite a bit of effort to prevent accidental contamination during e.g. mealtimes.)

So, across 3 rounds, there were 36 recipients - 18 restrained and 18 unrestrained. 10 of the restrained recipients and 12 of the unrestrained recipients were infected.

They also ran a different, fourth round, where they had 12 uninfected guys play cards using "freshly contaminated object" ("cards, poker chips, and pencils") from infected donors playing other games concurrently, swapping out the objects every hour for maximum freshness. They forced those guys to perform "exaggerated hand-to-nose and facial rubbing, often with conjunctival and nasal mucosal contact" every 15 minutes, because "it seemed the recipients were actively avoiding any contact to their faces". None of those guys were infected.

This seems like substantial evidence that under more "realistic" conditions [^9], transmission via fomites is not overwhelmingly likely for RV-16. I'd be more hesitant to update very hard without the fourth round, but they had a bunch of guys spend 12 hours playing cards that had been very recently and actively used by a bunch of sick people, and none of them got sick.

This paragraph was somewhat alarming (bolding mine):

> The complete absence of RV16 on the fomite recipients' hands was surprising. Certainly the nose-to-hand-to-fomite-to-hand-to-nose exposures of the experiment D (fomite) recipients far exceeded that of any normal indirect contact circumstance. Eight men with colds were contributing continuously. **The cards, pencils, and poker chips used by these recipients were literally gummy from the donors' secretions**. Subsequent to the experiments reported here, we embarked on additional experiments studying the four steps (see above) of the contact transmission chain \[12\]. We found that the virus nearly disappears during the journey from the donor's to the recipient's nose. The donor may have thousands of infectious particles on his hands, but few are deposited on fomites; the cards and chips he handles often have no virus at all, and positive fomites have only 10-30 TCID <sub>50</sub> [^10] **By the time the recipient's hands and nose are reached, the levels of virus drop to zero or nearly so**. Significant quantities of virus will only reach their final destination if the mucus is still wet; evidently this situation happened infrequently or never in our poker games, even though the exposures were much exaggerated.

How does one square this with Gwaltney & Hendley, 1982? We don't know how long recipients there waiting after the coffee mug handles were contaminated, but there was a 20 minute window between the plastic tiles being contaminated and the recipients touching them. That's longer than the enforced 15-minute interval for face-touching here. A couple possibilities:

- "often with conjunctival and nasal mucosal contact" might have been doing a lot of work. What's "often"? If substantial contact with mucuous membranes is load-bearing, that could explain a very large part of the effect.
- Maybe the secretions on the contaminated coffee mug handles and plastic tiles took longer to dry than those on the playing cards & poker chips.
- ???

Also, I think this does not do much to distinguish between small particle and large particle transmission, given the table size.

[Meschievitz et al., 1984](https://pubmed.ncbi.nlm.nih.gov/6088646/) ran six trials where they housed multiple donors (usually between 5 and 10) with multiple recipients (similar numbers), for varying lengths of time, ranging from 5 hours to ~6.5 days. They report:

> The experiments described in table 3 are arranged in order of donor-hours of exposure (DHE; one donor in the experiment room for 1 hr equals one DHE; five donors in the room for 5 hr equals 25 DHE, etc.) because rate of RV16 transmission correlated in a nearly linear fashion with DHE (r =.926, P <.01). The correlation was nearly perfect when DHE was plotted logarithmically (r =.997, P.001; figure 3).

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/92fkEn4aAjRutqbNF/gt899ww3zgrge4wmqtvm)

"Semi-logarithmic" sure is a fancy way to fit a curve.

Their experiment design, in isolation, doesn't give us much to go on for updating on various methods of transmission. However, this does seem like it lets us reconcile Gwaltney (1978) [^11] and Dick (1987) [^12] - the longer you're in close contact with someone sick, the more likely it is that they successfully cough onto your eyeball.

## Other Factors

There are a couple of important factors that the above analysis doesn't cover, that could substantially change takeaways. Briefly, those are:

- Children. They shed a heck of a lot more of the virus, when sick [^13]. All of these studies were on adults. If some methods of transmission have non-linear response curves, that might imply different things about how to prevent transmission originating with children than it would for adult-to-adult transmission.
- There are many rhinoviruses (and many other non-RV "cold" viruses)! They could very well have different transmission characteristics. Who knows?

## Review

[Andrup et al., 2023](https://www.ajicjournal.org/article/S0196-6553\(22\)00866-5/fulltext) is a more comprehensive meta-analysis of the existing literature on the subject, which I held off on reading before I conducted my own research and wrote up the above analysis (minus the summary at the top). This is their conclusion:

> We found low evidence, that transmission via hands and fomite followed by self-inoculation is the dominant transmission route in real-life indoor settings. We found moderate evidence, that airborne transmission either via large aerosols or small aerosols is the major transmission route of rhinovirus transmission in real-life indoor settings. This suggests that the major transmission route of RVs in many indoor settings is through the air (airborne transmission).

However, as far as I can tell, the only studies they analyzed which could plausibly support transmission via small particles (distinguished from large particles) were two studies on prisoners from the 60s. In the first one [^14], researchers sprayed aerosolized inoculum directly into the subjects' noses via a hand atomizer. In the second one [^15], they "received aerosol inoculation by means of a molded rubber face mask attached to a cylindrical chamber containing a continuous flow of aerosol generated by a Collison atomizer". All of the studies that tested conditions more similar to the real world found no transmission via small particle aerosols.

## Conclusion

"Large" particle transmission: likely, especially over extended periods of time. (Remember, 10 of 18 experiment subjects were infected within a 12 hour period despite being physically restrained from touching their face with their hands.) "Small" particle transmission: not very likely (maybe even "very unlikely"). Fomite transmission: possible, but the strongest evidence comes from studies that are testing pretty contrived [^16] setups, whereas the studies that check more natural conditions don't see very high rates of transmission against the aerosol baseline. My guess is that in practice, fomites are probably not responsible for most adult-to-adult transmission. (I'm much less confident about children.)

Definitely avoid coughing or sneezing into people's faces. Wash your hands before touching your face, if you're taking care of a sick person... but don't forget to use that paper towel to turn the water off, since faucet handles are hotbeds of other people's germs. Face-to-face conversations seem much worse than ambiently hanging out in the same room.

Overall confidence: low. Reasonable people might not agree with my inferences about the likelihood of "natural" transmission via the three transmission methods described and tested by these studies. Might generalize poorly to children. Might depend on details of specific viruses, and I don't think we've done enough research to have meaningful evidence about whether different RVs have very different transmission profiles from each other.

---

*Thanks to Elizabeth van Nostrand and eukaryote for feedback on clarity. Remaining imprecisions are my own.*

x

How Colds Spread — LessWrong

[^1]: Like being in the same room as someone for a while.

[^2]: That I could find!

[^3]: The authors note:

The aerosols produced by this method were assumed to contain particles of both large and small diameter. However, the method was characterized as "large particle" since this was the only contact situation in which passage of large droplets of respiratory secretion between donor and recipient could occur.

However, they don't define "large" or "small" particle sizes anywhere.

[^4]: The study authors note that the "one infected recipient in the large particle aerosol group had had intimate contact with a hand-contact recipient on the evening of the first day of their exposure to the donor." There are some other details here which suggest the study authors think the transmission was *probably* still the result of the tested transmission route (large particle) rather than via this unintended side-channel, but it does muddy the waters.

[^5]: I'm more interested in figuring out indirect transmission via shared surfaces (i.e. doorknobs, shared food serving utensils, etc), as well as "survival" time on various surfaces (including one's own fingers).

[^6]: The study was simultaneously testing the effectiveness of spraying surfaces with a disinfectant. I omit discussion of those results for brevity.

[^7]: The researchers [eluted](https://en.wikipedia.org/wiki/Elution) the virus from the subjects' fingers, and then used some plaque assays to test the eluates (by culturing).

[^8]: In this study, they used RT-PCR to test for presence of the virus.

[^9]: Though still exaggerated: "The average number of hand-to-face contacts recorded (186) over a 12-hr period was far in excess of that observed during normal adult behavior \[7\]: one "nose pick" every 3 hr and one "eye rub" every 2.7 hr."

[^10]: 50% tissue culture infectious dose, which works by progressively diluting a virus sample until a specific dilution infects 50% of separate "wells" of cell culture samples in a "plate" (a collection of wells).

[^11]: Only 1 out of 12 recipients sitting together at a table with infected donors were infected, despite high-risk activities like talking, singing, sneezing, and coughing.

[^12]: 10 of 18 recipients, restrained in a way that prevented them from touching their faces, were infected from 12 hours of playing cards at the same table as infected donors. (Also 12 of 18 unrestrained recipients.)

[^13]: As infected children appear to have a higher viral load than adults, this may explain why children are considered to be the main transmission vector.

...

The viral load in the mucus of more than 1000 rhinovirus-infected children below 1 year of age was 5.79 × 10 <sup>e6</sup> TCID <sub>50</sub> /mL, which is 10 to 100 times higher than our HC of 1 × 10 <sup>e5</sup> (Regamey et al., private communication)

[https://pmc.ncbi.nlm.nih.gov/articles/PMC7129024/](https://pmc.ncbi.nlm.nih.gov/articles/PMC7129024/)

[^14]: [https://academic.oup.com/aje/article-abstract/81/1/95/167193](https://academic.oup.com/aje/article-abstract/81/1/95/167193)

[^15]: [https://journals.asm.org/doi/epdf/10.1128/br.30.3.517-529.1966](https://journals.asm.org/doi/epdf/10.1128/br.30.3.517-529.1966)

[^16]: And fairly pessimal, for the recipients.