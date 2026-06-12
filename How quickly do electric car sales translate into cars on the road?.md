---
title: "How quickly do electric car sales translate into cars on the road?"
source: "https://hannahritchie.substack.com/p/ev-fleet-transition?publication_id=1199196&post_id=201553323&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Hannah Ritchie]]"
published: 2026-06-11
created: 2026-06-12
description: "And other insights from the electric car rollout in 2025."
tags:
  - "brain_spew"
---
Last month, the International Energy Agency (IEA) published its estimates of electric car sales data for 2025. I updated all of this data in our [charts on Our World in Data](https://ourworldindata.org/electric-car-sales), if you want to dive into more detail.

Here, I wanted to share just a few headline figures, then go on to tackle the question of how long it takes for electric car *sales* to translate into cars *on the road*.

First, the interesting figures from the new data.

#### 1\. One-in-four new cars sold globally was electric. That’s up from one-in-five the year before.

![](https://substackcdn.com/image/fetch/$s_!KZ3D!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcb34a7f8-a817-4b42-8e61-1355f75b944d_2048x1556.png)

#### 2\. China passed the 50% mark, although the year-on-year growth was a bit slower than the year before.

![](https://substackcdn.com/image/fetch/$s_!Q60r!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb9fda8de-de77-4f65-a3ad-5f25312d3beb_2048x1556.png)

#### 3\. Essentially all cars sold in Norway are now electric. I’m guessing that if you buy a combustion car there, people now think you’re a bit odd. A lesser-known example of the EV rollout is Denmark: in 2025, over 70% of new cars were electric.

![](https://substackcdn.com/image/fetch/$s_!fZ1v!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff385b3ce-69f0-4e35-91c2-c4d40829f008_2048x1629.png)

#### 4\. Electric cars continue to grow across Europe, but there was no growth in the United States in 2025.

Its EV share has been stuck on 10% for several years. This is also true for the total [number of electric car sales](https://ourworldindata.org/grapher/electric-car-sales?tab=line&country=~USA&mapSelect=~USA): in 2025, it was 1.5 million, the same as the year before.

![](https://substackcdn.com/image/fetch/$s_!3_vp!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fea59f8a6-965a-4622-8f86-8bdaa382c9e8_2048x1629.png)

#### 5\. There are huge differences in the rate of adoption across countries.

Here is just a selection; you can find data for more [here](https://ourworldindata.org/grapher/electric-car-sales-share?tab=discrete-bar&time=latest&country=OWID_WRL~NOR~GBR~OWID_EU27~CHN~USA~DEU~ZAF~IND~SWE).

![](https://substackcdn.com/image/fetch/$s_!9hep!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc322cbf2-ba2c-4c70-89c6-1986dfd0cc28_2048x1707.png)

#### 6\. The world is well past the peak of combustion engine car sales. These sales peaked in 2017.

![](https://substackcdn.com/image/fetch/$s_!cf6A!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F747ec7b1-d57f-473c-8c5a-6e9c3fc6d5cc_1620x1620.png)

---

A lot of the data on the rollout of new electric car sales seems very promising for the energy transition. But it’s hard to get a sense of how quickly this filters through to cars on the road.

How long before half of the cars on China’s roads are electric? What about all of them? And how sensitive are these timelines to specific factors around car ownership?

For my own curiosity, I built [a quick, simple tool](https://hannahritchie.github.io/ev-fleet-transition/) that attempts to model this. I thought I’d share it here in case you want to play with it.

It seems like there’s a lot going on, but the inputs and outputs are quite simple. Pick a given country. The chart on the left show electric car *sales*. The chart on the right shows how this filters through to cars *on the road*.

You can adjust three inputs:

- How quickly the EV sales share increases. This is a very simple model, so you can’t adjust this for individual years.
- The average lifetime of cars: how long people keep their cars for. If people ditch them after 10 years, electric cars will take over faster than it they hold on to them for 15 or 20 years.
- How quickly the car fleet is growing. In low- and middle-income countries, total car sales are still increasing a lot. In high-income countries, they’re pretty much stagnant; this means EVs are essentially replacing petrol ones, rather than meeting additional new demand, too.

![](https://substackcdn.com/image/fetch/$s_!jIUI!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0d98bd28-bdec-493f-b494-d2cdba95b1f4_1756x1620.png)

As a quick example: if China’s EV sales share were to grow at 5 percentage points each year, it would reach 100% sales in 2035.

How would this translate into cars on the road?

Today, 14% of cars on the road are electric. If the average lifespan of a car is 15 years, and the fleet is still growing strongly at around 6% per year, this would pass 50% by 2032, and 90% in the early 2040s.

If the car lifespan were 10 years, it would reach 90% in the late 2030s. You can play with these options for a range of different countries to see how sensitive the outcomes are.