---
title: "Home"
source: "https://www.facebook.com/"
author:
published:
created: 2026-05-25
description:
tags:
  - "brain_spew"
---
I'm hoping this will be my last post about the toxic storage tanks in Garden Grove, California in danger of exploding or leaking and requiring the evacuation of 50,000 people. Today's headline does not scream happy ending – that the tank cracked and therefore relieved the pressure build up due to the runaway reaction taking place inside. But it is a happy ending and deserves a shout out to the mechanical engineers of the world.

You see, every mechanical engineer learns in probably their first mechanical design class about how to design a pressure vessel such that it will leak before it breaks. It's a concept I remember well – leak before break (LBB). Using the principles of fracture mechanics, engineers are able to tailor the tank design (material, wall thickness, crack arrestment features) such that if a crack does develop and start to grow, it will grow in a stable manner up to a certain length to a point that the material contained in the tank will leak out through the crack, thus relieving the pressure that causes the crack and triggering leak detection systems to shut everything down.

Without this elegant design process, the crack could grow in an unstable manner, meaning that the first increment of crack to develop triggers an even greater increment and again and again such that you end up with an instantaneous, catastrophic failure.

This case was not straightforward, however, and there was definitely some luck involved. LBB techniques are generally meant for repeated pressure cycles at some level well below the maximum pressure capability of the tank. In this case, presumably the tank had seen quite a number of pressure cycles in its lifetime, and then a max pressure exceedance of unknown amount happening in real time. The authorities were correct to evacuate. The tank truly could have blown up.

Very luckily, the pressure build up seems to have been relatively slow. With an unstable, high rate pressure build up, whew, anything could have happened. Kudos to the brave individuals who were there risking their lives monitoring what they could monitor and doing what they could to slow the rate of the uncontrolled cure down.

Finally, with a slower rate of pressure build up, the LLB philosophy seems to have worked. The static overpressure was just one more pressure cycle for this tank, and when it reached a certain level, it triggered crack initiation (usually at some stress concentration where a valve or something penetrates the tank wall) and stable crack growth, to the point that the crack grew enough to relieve the pressure, but not big enough to completely unzip and fail catastrophically.

In my post from yesterday, I said that the chemicals were in charge. They truly were. Everyone was very, very lucky.

For those that want to geek out a little further into the LBB philosophy, here's how engineers go about performing their analysis. In the fourth bullet under step 2, there is a reference to the Paris Law. I was lucky enough to study under Dr. Paul Paris and did a Masters thesis on ductile fracture of nuclear piping systems.

1\. Define Operating & Accident Loads

Identify and quantify all stresses the vessel experiences during normal operation and extreme conditions (e.g., thermal transients, pressure spikes, seismic/earthquake loads, deadweight).

2\. Determine Material Properties

Gather fracture toughness and tensile data for both the base metal and weld materials. Critical properties include:

Stress-strain curves.

Yield and ultimate tensile strengths.

Resistance curves (for ductile tearing).

Fatigue crack growth rates (Paris Law).

3\. Postulate the Initial Flaw (Leakage Crack)

Postulate a through-wall crack at the most highly stressed and susceptible locations (such as weld joints or nozzles).

Flaw Size: The size of this "Leakage-Size Crack" (LSC) is generally chosen based on the minimum detectable leak rate of the facility’s monitoring systems, with an added margin of safety.

4\. Calculate the Crack Opening Area (COA)

Using Elastic-Plastic Fracture Mechanics (EPFM) and finite element analysis (FEA), calculate how much the crack opens under normal operating loads.

5\. Perform Leak Rate Analysis

Calculate the rate of fluid leakage through the crack opening. This involves evaluating two-phase fluid flow, accounting for crack surface roughness, crack length, and the fluid's thermodynamic state.

Criterion: The calculated leak rate must be safely detectable by the plant's leak monitoring systems, with significant margin (often by a factor of 10).

6\. Postulate the Critical Crack Size

Calculate the "Critical Crack Size" , which is the length at which the through-wall defect becomes unstable and would cause catastrophic rupture under combined normal plus maximum accident/seismic loads.

7\. Determine Crack Stability and Margins

Perform tearing stability analyses (using

\-integral tearing theory) to prove that the Leakage-Size Crack will not grow to the Critical Crack Size before operators can detect the leak and safely shut down the vessel. Required margins generally demand that:

Crack size margin: Critical flaw length must be greater than or equal to 1.7 × leakage flaw length.

Load margin: Structural margin of safety is maintained under bounding accident conditions.

See less