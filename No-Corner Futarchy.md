---
title: No-Corner Futarchy
source: https://www.overcomingbias.com/p/no-corner-futarchy?publication_id=1245641&post_id=178212593&isFreemail=true&r=7br8e&triedRedirect=true
author:
  - "[[Robin Hanson]]"
published: 2025-11-06
created: 2025-11-06
description: In March 1980, the Hunt Brothers tried but failed to corner the silver market.
tags:
  - clippings
  - crypto
---
In March 1980, the Hunt Brothers tried but failed to corner the silver market. The big fall in price after caused “panic”. People try to design markets to avoid the possibility of cornering.

No one can corner a betting market, as more bets can always be created from cash fast in unlimited supply. And because I’ve thought of futarchy as built out of betting markets, I haven’t worried about people cornering futarchy markets.

But futarchy is often used to try to raise the value of assets that have unlimited upside, like firm stocks or crypto tokens. As these are not bets, they cannot be created in unlimited supply. Making the possibility of cornering more realistic.

For example, imagine a coalition controlled a majority of the tokens traded when the futarchy markets were open. This coalition might perhaps be able to dominate the selling in either the token-if-yes or the token-if-no markets, preventing other traders from pushing down one of those prices via selling tokens.

A solution I recommend is to actually use bet-like derivatives of such assets in your official futarchy markets. Imagine an asset *a* with min value of zero, an unlimited max value, an initial reference price of r, and a final settlement price of p. Let M = N\*r. We can create this derivative asset of a: “Pays $p if p<M, else pays $M”, and this anti-derivative: “Pays $(M-p) if p<M, else pays zero”.

Here are the exchange rules of these derivatives.

1. Before settlement, “banks” can convert $M into one derivative and one anti-derivative, or vice versa.
2. Before settlement, “banks” can convert an asset *a* into one derivative, and one option to buy that asset for $M, or vice versa.
3. After settlement, each derivative or anti-derivative can be exchanged for the cash declared in its words.
4. At any time, the holder of an option to buy asset *a* for $M can exercise that option.

The futarchy markets compare conditional prices of the derivative given various possible decisions during some key price measurement period. This futarchy choice process should be called off, with no policy change, if any of those conditional prices get consistently close to M during the futarchy price measurement period. N is chosen to trade off losses from calling off the futarchy choices once in a while, vs making trading harder due to less trading leverage from larger M.

And that’s how to make uncornerable futarchy.