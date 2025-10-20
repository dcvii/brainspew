---
title: "Bitcoin Could Consume as Much Electricity as Denmark by 2020"
source: "https://www.vice.com/en/article/bitcoin-could-consume-as-much-electricity-as-denmark-by-2020/"
author:
  - "[[Sebastiaan Deetman]]"
published: 2016-03-29
created: 2025-10-20
description: "An environmental researcher modeled pessimistic and optimistic scenarios for Bitcoin’s energy consumption over the next few years."
tags:
  - "clippings"
---
I’m an engaged environmental researcher and have recently become a bitcoin enthusiast.

These are two possibly conflicting fascinations, as previously pointed out by [Christopher Malmo here at Motherboard](http://motherboard.vice.com/read/bitcoin-is-unsustainable). That’s because bitcoin is incredibly energy intensive: at the time of Malmo’s piece, he calculated that a single bitcoin transaction requires as much electricity as the daily consumption of 1.6 American households, and that number has increased since then. “Adopting Bitcoin as a major currency anytime in the next few decades,” he wrote, “would just exacerbate anthropogenic climate change by needlessly increasing electricity consumption until it’s too late.”

## Videos by VICE

As I have some experience in developing energy scenarios, I wanted to see how this could develop into the future. My findings weren’t much more encouraging. According to my calculations, if the bitcoin network keeps expanding the way it has done recently, it could lead to a continuous electricity consumption that lies between the output of a small power plant and the total consumption of a small country like Denmark by 2020.

**What determines the energy consumption of the bitcoin network?**

Let’s start with the basics. Bitcoin transactions are validated and processed by a decentralized network of volunteers, usually hosting dedicated hardware to perform calculations, called “hashes,” to find solutions to a complex mathematical algorithm in return for a reward of brand-new bitcoins plus some transaction fees.

This network of so-called bitcoin “miners” ensures the security of the system, but unfortunately also consumes a lot of electricity—currently about 350 megawatts according to my own calculations, which is roughly equivalent to the electricity demand of 280,000 [American households](http://www.eia.gov/tools/faqs/faq.cfm?id=97&t=3).

**Efficiency of mining hardware**

I started with the the amount of operational mining hardware (measured as the hashrate in number of hashes per second), and the efficiency of the hardware (which can be measured in Joules per hash).

The total bitcoin mining network currently comprises a calculation speed of over 800 petahashes per second, which requires over 10,000 metric tonnes of hardware, considering that even the newer machines weigh over 12 kilograms each (15 grams per GHash/sec. on average in the analysis below). That is enough material to build another [Eiffel tower](https://en.wikipedia.org/wiki/Eiffel_Tower).\*

In the beginning of the bitcoin phenomenon, miners used any laptop or computer to generate bitcoins. As the difficulty of mining bitcoin increased—part of the cryptocurrency’s design—miners upgraded to graphics cards, and then more sophisticated hardware. The state of the art is dedicated bitcoin mining chips (called application specific integrated circuits, or ASICs). ASICs have been [available for three years](http://cseweb.ucsd.edu/~mbtaylor/papers/bitcoin_taylor_cases_2013.pdf), so we have a small basis to explore the improvements in the efficiency of mining hardware.

Let’s have a look at the efficiency of those ASIC miners over time. I took an existing [comparison of bitcoin mining hardware](https://en.bitcoin.it/wiki/Mining_hardware_comparison), to which I added a few miners myself and looked up all their first shipping dates, based on various sources (company specifications, blog-posts, first reviews, etc.). After exclusion of the ones that were never actually shipped to customers, and after exclusion of some of the early highly inefficient ASIC miners because they didn’t fit any trend, I ended up with a list of 53 types of bitcoin miners and plotted their efficiencies against their original shipping dates as can be seen below.

I further excluded the USB miners (red squares) from any trend analysis, because regardless of their high efficiency, their purchase prices (per hash) are generally so much higher than for other miners that they are not likely to contribute a significant share of the total hashrate of the bitcoin network.

Drawing a trend from the other 46 miners has been done in two distinctly different ways, to represent both an optimistic as well as a more pessimistic assumption for the future development.

The pessimistic trend line is based on the average of all ASIC miners (the blue dots) and has the form of a power equation, thus it starts with a higher electricity consumption and though it assumes a continued increase in efficiency, it leads to a slightly higher future projection of electricity consumption per hash as compared to the optimistic approach. For the optimistic case, I based the trend line only on the most efficient devices brought on the market (indicated with a black outline in the graph), and assumed an exponential decrease in electricity demand per hash, which actually represented the best fit to the data and leads to an even higher long-term efficiency.

Though these trend lines give us a hint of the future to come, they are only based on the efficiency of new mining hardware, and as such don’t represent the efficiency of the current bitcoin network, which still partially depends on the calculation power of older, less efficient mining devices. To approximate the effective efficiency of the whole network I assumed that the growth of the network’s hashrate determined the amount of newly installed mining capacity each month, and then used weighted averaging over a period of either three or five years to represent the efficiency of the total stock of bitcoin mining hardware in an optimistic and pessimistic case respectively. The resulting long term trends of both new and effective electricity consumption per hash can be seen below.

My internal torment between environmental concerns and my enthusiasm about bitcoin mellowed somewhat when I saw these initial results. Apparently, the technological advancements at chipmakers and hardware manufacturers made sure that in the future, bitcoin miners will probably become more than three times as efficient. I could rest assured without a feeling of guilt. Or could I?

Knowing that the efficiency of the miners was only one part of the equation, the other part started haunting me at night. Could it be that as bitcoin usage grows, the total hashrate of the bitcoin network kept growing at such a speed that it would outcompete the increase in efficiency of the miners? Could it be that the total energy consumption would keep on growing?

**Popularity of bitcoin**

To complete the picture and answer this question, I dug up the historic development of the monthly hashrate at [blockchain.info](http://blockchain.info/). Since the introduction of the first ASIC mining hardware in January 2013, the average monthly growth of the network’s hashrate has been a daunting 37 percent. If we use that as a proxy for the monthly growth in the years to come, the bitcoin network would require more electricity than is currently generated globally, by the end of 2016 (yes, December this year, regardless even of the assumptions for mining efficiency).

That couldn’t be right. The bitcoin price was increasing rapidly in 2013, [hitting $1,000 apiece in late 2013 and again in early 2014](http://www.coindesk.com/bitcoin-price-crossed-1000-again/). This price runup seemed like an anomaly fueled by hype, so it didn’t seem accurate to use in my calculations for expected hashrate growth. I had to find a more realistic estimate.

As can be seen in the graph below, the high growth in hashrate originated mostly in the early days of ASIC mining, thus averaging over the more modest growth in more recent months should give a more balanced indication of the expected growth.

I applied two growth rates on the current 800 Peta hashes per second, one being optimistic and defined by the average of the network growth rate in the 12 months with the lowest growth since the introduction of ASIC miners (covered by the small blue box, which in fact was a period with a flat or sometimes even declining bitcoin price), leading to a 5 percent growth rate each month.

The other rate is a bit more pessimistic (for the environment, not for the network security), and is based on the period that includes the three months preceding and following these 12 months (the larger blue box), leading to a 12 percent monthly increase.

Obviously, these growth rates are highly uncertain and are always related to the bitcoin price, as miners will keep adding hashpower as long as it is profitable. However, the price of bitcoin has been so volatile that it is simply impossible to predict. Therefore I use the previously mentioned historic average growth in hashrate as a conservative (5 percent) and a more daring (12 percent) estimate of the stable growth for the years to come.

**The block reward**

Two other factors that may influence the growth rate of the network’s total hashrate are the bitcoin block size and the halving of the bitcoin block-reward, expected to happen [this summer](http://www.bitcoinblockhalf.com/). I’ve not accounted for any outcome of the [discussion on the block size](https://motherboard.vice.com/read/the-dream-of-buying-a-coffee-with-bitcoin-is-dying-if-its-not-already-dead-block-size-fees), as it is still being debated and the outcome is unknown still. However, the block-reward halving is by design, based on the idea that bitcoin transaction fees will slowly take over as the main incentive for mining, thus it may have severe consequences on the energy consumption.

However, the long-term effect on the total hashrate of this halving is unknown. Some have argued that the reduced bitcoin reward would lower the incentive to bitcoin miners, possibly even leading to a large decrease in mining activity (what some call the “mining gap”) as electricity costs will make mining unprofitable until the price of bitcoin rises again.

Others have argued that the halving of the mining reward will lead to increased bitcoin scarcity and therefore a quick increase in the bitcoin price, which would possibly lead to an even higher growth in hashrate quickly after the gap. Again, it is impossible to say who is right. But to somehow account for the diminishing block-reward, I assumed that the hashrate will either stop growing and stabilize during the six months following the halving of the block-reward (optimistic) or that it will simply keep growing as it did historically (pessimistic).

**Two scenarios**

With the combination of both optimistic and pessimistic assumptions on the energy consumption of the bitcoin network we have in fact created two wildly different scenarios on how the bitcoin future may unfold. What would this mean for the environmental impact of bitcoin by, say, January 2020? The table below summarizes the main assumptions and gives an indication of the expected power consumption of the bitcoin network.

The results show that in an optimistic scenario, the increase in electricity consumption of the bitcoin network compared to now is not shocking, from around 350 MW to around 417 MW, but still on the order of one small power station. If things play out a little less favorably, however, the bitcoin network may draw over 14 Gigawatts of electricity by 2020, equivalent to the total power generation capacity of a [small country](http://www.tsp-data-portal.org/Breakdown-of-Electricity-Capacity-by-Energy-Source#tspQvChart), like Denmark for example.

This is by no means a comprehensive analysis and these numbers should be taken with a pinch of salt, but the conclusion is an important one: If the network of bitcoin miners keeps expanding the way it has done, the increased efficiency of mining devices is most likely offset, leaving us anywhere between a slight growth or an explosion of the total energy consumption.

Even in the optimistic scenario, just mining one bitcoin in 2020 would require a shocking 5,500 kWh, or about half the annual electricity consumption of an American household. And even if we assume that by that time only half of that electricity is generated by fossil fuels, still over 4,000 kg of [carbon dioxide](https://www.eia.gov/tools/faqs/faq.cfm?id=74&t=11) would be emitted per bitcoin mined. It makes you wonder whether bitcoin could still be called a virtual currency, when the physical effects could become so tangible.

Personally, I haven’t given up on the idea of distributed network transactions, but a radical rethinking of how these may be secured would be beneficial, be it at least for the environment. Perhaps a system where all miners are rewarded for their pledged surplus in CPU processing power, but the actual hashing is performed only by a few thousand randomly selected and continuously changing CPUs, would be a solution. We could throw the remnants of our destructive arms race for hashing power out the window, perhaps find a way to make a few old miners [useful in functional calculations](https://www.curecoin.net/), and use the rest of them to build a rusty totem in honor of Satoshi.

---

\*The starting point for my calculation is the total hashrate of the bitcoin network over time as reported by blockchain.info. This is the total of all pools and nodes—over 800 petahashes per second at the moment. Besides collecting info on the release date of miners, I also noted their weights in kilograms where available. So based on the average of 32 miners, released after March 2014 (so not even including the old cluncky ones) I derived an average weight of 15 grams per GHash/second. Which would mean that to provide those 800 petahashes per second you require 12,000 tonnes of hardware, well over the weight of the Eiffel tower at 10,000 tonnes.  
  
**Disclaimer:** Despite the criticism in the text, the author thinks that the idea of the decentralized network behind the bitcoin digital currency is a very powerful and promising one. He owns about one single bitcoin, two micro-scale bitcoin mining devices and a small cloud-mining contract, thus has a small vested interest in bitcoin. He also emphasizes that scenarios like the ones presented here are by no means predictions of the future, but simply meant as “ *challenging, and relevant stories about how the future might unfold” (*[*UNEP*](http://www.unep.org/maweb/documents/document.326.aspx.pdf)*).* No rights can be drawn from any statement made and interpretation of the text should be made at the reader’s own responsibility. To improve the transparency of the underlying calculations and to enable anyone to understand these numbers better, the calculations are made available in [this spreadsheet](https://docs.google.com/spreadsheets/d/1B0YFtz6aEJwoJwXxAwLtQPmsiaWQTh-_mnashxzGBLM/edit?usp=sharing).