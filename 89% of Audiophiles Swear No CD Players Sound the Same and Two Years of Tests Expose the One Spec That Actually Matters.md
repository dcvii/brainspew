---
title: 89% of Audiophiles Swear No CD Players Sound the Same and Two Years of Tests Expose the One Spec That Actually Matters
source: https://www.headphonesty.com/2026/03/cd-players-tests-expose-one-spec-matters/
author:
  - "[[Colin Toh]]"
published: 2026-03-12
created: 2026-03-16
description: Measurements of 50+ players and four blind tests agreed on nearly everything, except one.
tags:
  - brain_spew
  - audiophile
---
Measurements of 50+ players and four blind tests agreed on nearly everything, except one.

In a Steve Hoffman Forums poll, [89% of respondents](https://forums.stevehoffman.tv/threads/do-all-cd-players-sound-the-same.1197354/) said CD players have distinct sound. But over the past two years, that belief ran into an unusual test.

One community member [measured more than 50 players](https://www.audiosciencereview.com/forum/index.php?threads/what-cd-player-would-you-like-to-see-tested.63260/) with a custom test disc, while several groups ran blind listening tests in parallel.

The results settled several long-running debates about transports, jitter, and audible differences. They also pointed to one area where players really do diverge.

Here is what the data actually shows.

## The CD Player Measurement Dataset

To measure CD players more rigorously than the industry-standard approach allows, NTTY created a [custom test CD (version 7.4)](https://www.audiosciencereview.com/forum/index.php?threads/test-cd-for-measurements-of-cd-players.58046/) built around a 999.91 Hz tone instead of the usual 1 kHz signal.

At 999.91 Hz, this signal generates 65,535 unique samples before repeating. In turn, it reduces those artifacts and makes it harder for mediocre players to coast through standard benchmarks.

Over 18 months, he [ran the disc through more than 50 players](https://www.audiosciencereview.com/forum/index.php?threads/what-cd-player-would-you-like-to-see-tested.63260/) spanning decades, price brackets, and design philosophies:

- vintage Sony flagships
- budget FiiO portables
- Denon mid-range units
- Revox broadcast machines, and more.

He also published [standardized measurement protocols](https://audiosciencereview.com/forum/index.php?threads/more-than-we-hear-with-a-cd-player.59505/) covering THD, jitter, intersample peak handling, and DAC resolution, which created the most comprehensive independent CD player dataset in audiophile history.

The results confirmed some expectations and overturned others.

His most revealing finding, however, was not a measurement in the usual sense but evidence that at least one manufacturer had optimized for the test bench itself.

In Denon’s case, the AL32 digital filter [detects standard test tones and switches between three filter modes](https://www.audiosciencereview.com/forum/index.php?threads/denon-dcd-900ne-review-cd-player.56587/) in ways that improve published bench numbers. By adding an 80 Hz tone to the signal, NTTY defeated that detection and exposed the filter behavior the player uses with actual music.

![Custom 999.91 Hz sine tone used to avoid test tone interference and reveal true performance. (From: Audio Science Review)](https://www.headphonesty.com/wp-content/uploads/2025/08/999_91.jpg)

Custom 999.91 Hz sine tone used to avoid test tone interference and reveal true performance. (From: Audio Science Review)

## Evidence From Four Blind Tests

While NTTY was building the measurement record, listening tests in multiple countries were arriving at much the same conclusion. Once listeners lost sight of which machine was playing, the differences between CD players largely disappeared.

- Lovegrove’s [seven-player comparison](https://www.headphonesty.com/2025/10/cd-player-indistinguishable-blind-test/) pitted models from 1989 to 2023 against each other with level matching and single-blind controls. Listeners found differences “small,” and when every player fed a common external DAC, those gaps vanished.
- An engineer known as tcpip [heard unmistakable differences](https://www.headphonesty.com/2025/08/engineer-cd-player-rack-mount-listening-test/) between his CD players in normal listening. Confident enough to stake his credibility on it, he built a rack-mounted switching setup for proper ABX testing. He scored 7 out of 16 on one round, 8 out of 16 on the next, which are results consistent with chance.
- Guido Guarducci of the ANA\[DIA\]LOG YouTube channel [tested dozens of tracks across multiple genres](https://www.headphonesty.com/2025/02/audiophiles-experiment-cd-sound-superiority-myth/), comparing CD playback directly against lossless streaming from Qobuz.
	“I have to admit that I do not with CD quality hear any difference,” Guarducci concluded.
- Archimago’s [2024 DAC survey](https://archimago.blogspot.com/2024/05/high-end-dac-blind-listening-results.html) asked 105 listeners to compare three devices spanning the full price range. It asked 105 listeners to compare devices ranging from a $9 Apple dongle to a roughly $3,000 Linn Majik DS and a $20,000 Linn Klimax DSM. The results were, again, not strong enough to rule out chance.

### Limits of the evidence

None of these tests was beyond criticism.

For instance, Mart68 [argued](https://www.audiosciencereview.com/forum/index.php?threads/interesting-blind-test-comparisons-of-cd-players.66215/) that Lovegrove’s protocol asked listeners whether they thought they could distinguish players instead of requiring formal ABX identification, which he called “a critical flaw.”

rdenney [also](https://www.audiosciencereview.com/forum/index.php?threads/interesting-blind-test-comparisons-of-cd-players.66215/) [noted](https://www.audiosciencereview.com/forum/index.php?threads/interesting-blind-test-comparisons-of-cd-players.66215/) that 0.5 dB attenuator steps could leave residual level differences large enough to bias perception.

The thing is, human hearing routinely interprets the louder source as more detailed, dynamic, and engaging. Even a half-decibel difference can tilt a comparison, and none of these setups could guarantee tighter matching than 0.5 dB. Those are fair limitations.

Even so, four separate tests with different methods, different listeners, and different settings converged on essentially the same outcome, which makes the broader pattern difficult to dismiss.

## Three Things the Wars Settled

Two years of measurements and listening tests did not resolve every debate about CD players. But they did settle several long-standing claims about transports, jitter, and audible differences.

### Every transport is bit-perfect

If you’re buying a CD transport for its digital output, NTTY’s measurements have bad news. **Every transport he tested output identical data**.

For one, the [SMSL PL200T](https://www.audiosciencereview.com/forum/index.php?threads/smsl-pl200t-review-cd-transport.67018/), at roughly €550 (~US$600), matched the source WAV file bit for bit through its optical output, with no measurable distortion, signal loss, or clock deviation.

That result held across the broader set of players he tested, from vintage Teac units to budget SMSL models and heavy Denon flagships. The bits coming off the disc were the same.

> On that question, spending more on a transport for its digital output has no measurable justification.

Even the Teac VRDS-25X, a vintage flagship with significant analog-stage flaws, delivered [bit-perfect data with no clock deviation](https://www.audiosciencereview.com/forum/index.php?threads/teac-vrds-25x-review-cd-player.58483/) through its optical output.

The problems only appeared after digital-to-analog conversion. But for anyone using an external DAC, the transport is functionally irrelevant.

### Jitter is a non-issue

Identical bits don’t settle the question by themselves. Those bits still need to arrive at precise intervals, and clock accuracy was supposed to be where expensive transports earned their premium.

Manufacturers marketed femtosecond clocks and custom oscillators as essential upgrades, and built entire product lines around timing precision. The theory was that timing errors would color the sound, introducing distortion only top-shelf engineering could tame.

But the data told a different story. Archimago, for instance, noted that modern jitter has been “all but eliminated” and was “never significantly audible” except in worst-case hardware.

NTTY’s measurements also pointed the same way across every transport he tested, regardless of price or vintage.

### Nobody can hear the difference

This is the part most likely to sting for people who are convinced CD players have distinct sonic signatures. Every methodological critique is valid, but none of them explains why four uncoordinated groups all landed at chance level.

Sighted differences that collapse under blinding point to a perceptual cause, not flawed methodology. If the tests were simply broken, at least one should have produced a different result.

## The One Thing They Couldn’t Settle

![Intersample overs test shows the Denon DCD-900NE distorting heavily while the Yamaha CD-1 remains clean. (From: Audio Science Review)](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%201200%20306'%3E%3C/svg%3E)

Intersample overs test shows the Denon DCD-900NE distorting heavily while the Yamaha CD-1 remains clean. (From: Audio Science Review)

When NTTY tested how CD players reconstruct the analog signal between digital samples, the numbers split wide open.

His measurements showed a [49 dB gap](https://audiosciencereview.com/forum/index.php?threads/more-than-we-hear-with-a-cd-player.59505/) between the Teac VRDS-20 (-30.7 dB THD+N) and the Yamaha CD-1 in non-oversampling mode (-79.6 dB) on the same intersample peak test. That is a large spread on a single measurement of the same behavior.

The mechanism is straightforward. Between digital samples, the reconstructed analog waveform can exceed 0 dBFS.

If a DAC’s oversampling filter does not leave enough headroom, those peaks clip into bursts of harmonic distortion concentrated in the upper frequencies. But in practice, that can add a hard edge to cymbals, sibilants, and other treble-heavy material.

Archimago’s DAC survey found no significant overall preference (p =.175). But [headphone listeners](https://archimago.blogspot.com/2024/05/high-end-dac-blind-listening-results.html) told a different story: their preference for the more expensive DACs was highly significant (p =.00084), meaning the result was much less likely to be random. Because headphones remove room acoustics, speaker interactions, and placement variables, they may expose source-level differences more clearly.

Archimago’s DAC survey found no significant overall preference (p =.175), but [headphone listeners](https://archimago.blogspot.com/2024/05/high-end-dac-blind-listening-results.html) told a different story. Their preference for the expensive DACs was highly significant (p =.00084).

No controlled blind test has isolated intersample clipping as an independent variable to determine whether listeners can actually hear the distortion it produces. That leaves the largest measurable gap between CD players in a blind spot.

## What the 89% Are Actually Hearing

In 1997, Cowan Audio organized a blind comparison of a $1,800 CD player against a $300 Sony for two Australian audiophiles. Both were experienced listeners and confident they could identify the premium player.

“This will be easy,” [the participants said](https://www.head-fi.org/threads/testing-audiophile-claims-and-myths.486598/) before scoring at chance.

Three decades later, the same confidence shows up in modern discussions. In a [Steve Hoffman Forums poll](https://forums.stevehoffman.tv/threads/do-all-cd-players-sound-the-same.1197354/), **89% of respondents said CD players have distinct sonic signatures**.

> That does not necessarily mean those listeners are wrong about their experience. They’re just wrong about the source.

A volume offset of even half a decibel can make the louder player seem more detailed, more dynamic, and more engaging. That perceptual bias, already visible as a concern in the blind tests discussed earlier, is enough to create a consistent preference.

Digital filter choices can reinforce that effect. Slow-rolloff filters trade some upper-frequency extension for smoother transients, while fast-rolloff filters do the reverse.

So when listeners already know which player costs $20,000 and which costs $300, those subtle tonal differences can easily register as obvious improvements.

Expectation and context do the rest, anchoring perception to price, design, and brand reputation. Those variables compound until the differences feel genuine, even if they disappear once the labels come off.

Two years of the most data-rich CD player debate in audiophile history delivered a verdict, with one asterisk. Intersample peak handling creates measurable differences. Roughly 40% of CDs trigger it. Nobody seems willing to test whether listeners can hear it.