---
title: "Practical Power Beaming Gets Real"
source: "https://spectrum.ieee.org/power-beaming?utm_medium=inbody_related"
author:
  - "[[Paul Jaffe]]"
published: 2022-05-21
created: 2025-07-25
description: "A century later, Nikola Tesla’s dream comes true"
tags:
  - "clippings"
---
![This nighttime outdoor image, with city lights in the background, shows a narrow beam of light shining on a circular receiver that is positioned on the top of a pole.](https://spectrum.ieee.org/media-library/this-nighttime-outdoor-image-with-city-lights-in-the-background-shows-a-narrow-beam-of-light-shining-on-a-circular-receiver-th.png?id=29809843&width=3600&height=2815)

A power-beaming system developed by PowerLight Technologies conveyed hundreds of watts of power during a 2019 demonstration at the Port of Seattle.

PowerLight Technologies

Yellow

**Wires have a lot** going for them when it comes to moving around, but they have their drawbacks too. Who, after all, hasn’t tired of having to plug in and unplug their phone and other rechargeable gizmos? It’s a nuisance.

Wires also challenge electric utilities: These companies must take pains to boost the voltage they apply to their transmission cables to very high values to avoid dissipating most of the power along the way. And when it comes to powering public , including electric trains and trams, wires need to be used in tandem with rolling or [sliding contacts](https://en.wikipedia.org/wiki/Pantograph_\(transport\)), which are troublesome to maintain, can spark, and in some settings will generate problematic contaminants.

---

Many people are hungry for solutions to these issues—witness the widespread adoption over the past decade of , mostly for portable [consumer electronics](https://spectrum.ieee.org/topic/consumer-electronics/) but [also for vehicles](https://spectrum.ieee.org/cars-that-think/transportation/advanced-cars/wireless-charging-tech-to-keep-evs-on-the-go). While a wireless charger saves you from having to connect and disconnect cables repeatedly, the distance over which energy can be delivered this way is quite short. Indeed, it’s hard to recharge or [power a device](https://spectrum.ieee.org/transportation/mass-transit/a-critical-look-at-wireless-power) when the air gap is just a few centimeters, much less a few meters. Is there really no practical way to send power over greater distances without wires?

To some, the whole notion of transmission evokes images of Nikola Tesla with high-voltage coils spewing miniature bolts of lightning. This wouldn’t be such a silly connection to make. Tesla had indeed pursued the idea of somehow using the ground and atmosphere as a conduit for long-distance , a plan that went nowhere. But his dream of sending electric power over great distances without wires has persisted.

To underscore how safe the system was, the host of the science program “ [Bang Goes the Theory](https://www.bbc.co.uk/programmes/b00lwxj1) ” stuck his face fully into a power beam.

Guglielmo Marconi, who was Tesla’s contemporary, figured out how to use “Hertzian waves,” or , as we call them today, to send signals over long distances. And that advance brought with it the possibility of using the same kind of waves to carry energy from one place to another. This is, after all, how all the energy stored in wood, coal, oil, and natural gas originally got here: It was transmitted 150 million kilometers through space as electromagnetic waves—sunlight—most of it millions of years ago.

Can the same basic physics be harnessed to replace wires today? My colleagues and I at the U.S. [Naval Research Laboratory](https://www.nrl.navy.mil/), in Washington, D.C., think so, and here are some of the reasons why.

There have been sporadic efforts over the past century to use electromagnetic waves as a means of , but these attempts produced mixed results. Perhaps the golden year for research on wireless power transmission was 1975, when William Brown, who worked for [Raytheon](https://www.rtx.com/), and Richard Dickinson of NASA’s [Jet Propulsion Laboratory](https://www.jpl.nasa.gov/) (now retired) used to beam power across a lab with greater than 50 percent end-to-end efficiency. In a separate demonstration, they were able to deliver more than 30 kilowatts over a distance of about a mile (1.6 kilometers).

These demonstrations were part of a larger and [U.S. Department of Energy](https://www.energy.gov/) campaign to explore [the feasibility of solar-power satellites](https://spectrum.ieee.org/green-tech/solar/how-japan-plans-to-build-an-orbital-solar-farm), which, it was proposed, would one day harvest sunlight in space and beam the energy down to Earth as microwaves. But because this line of research was motivated in large part by the energy crisis of the 1970s, interest in solar-power satellites waned in the following decades, at least in the

Although researchers revisit the idea of solar-power satellites with some regularity, those performing actual demonstrations of have struggled to surpass the high-water mark for efficiency, distance, and power level reached in 1975. But that situation is starting to change, thanks to various recent advances in transmission and reception technologies.

![In this image, a narrow purple beam shines across a darkened room.](https://spectrum.ieee.org/media-library/in-this-image-a-narrow-purple-beam-shines-across-a-darkened-room.png?id=29810106&width=1000&quality=85)

During a 2019 demonstration at the Naval Surface Warfare Center in Bethesda, Md., this safely conveyed 400 watts over a distance of 325 meters.

Most early efforts to beam power were confined to microwave frequencies, the same part of the electromagnetic spectrum that today teems with , , and various other wireless signals. That choice was, in part, driven by the simple fact that efficient microwave transmitting and receiving equipment was readily available.

But there have been improvements in efficiency and increased availability of devices that operate at much higher frequencies. Because of limitations imposed by the atmosphere on the effective transmission of energy within certain sections of the electromagnetic spectrum, researchers have focused on microwave, millimeter-wave, and optical frequencies. While microwave frequencies have a slight edge when it comes to efficiency, they require larger antennas. So, for many applications, millimeter-wave or optical links work better.

For systems that use microwaves and millimeter waves, the transmitters typically employ solid-state electronic and phased-array, parabolic, or metamaterial antennas. The receiver for microwaves or millimeter waves uses an array of elements called rectennas. This word, a portmanteau of *rectifier* and *antenna*, reflects how each element converts the electromagnetic waves into direct-current electricity.

Any system designed for optical power transmission would likely use a laser—one with a tightly confined beam, such as a fiber laser. The receivers for optical power transmission are specialized cells designed to convert a single wavelength of light into electric power with very high efficiency. Indeed, efficiencies can exceed 70 percent, more than double that of a typical solar cell.

At the U.S. Naval Research Laboratory, we have spent the better part of the past 15 years looking into different options for power beaming and investigating potential applications. These include extending the flight times and payload capacities of drones, powering satellites in orbit when they are in darkness, powering rovers operating in permanently shadowed regions of the , sending energy to Earth’s surface from space, and distributing energy to troops on the battlefield.  

You might think that a device for sending large amounts of energy through the air in a narrow beam sounds like a death ray. This gets to the heart of a critical consideration: . Different power densities are technically possible, ranging from too low to be useful to high enough to be dangerous. But it’s also possible to find a happy medium between these two extremes. And there are also clever ways to permit beams with high power densities to be used safely. That’s exactly what a team I was part of did in 2019, and we’ve successfully extended this work since then.

One of our industry partners, [PowerLight Technologies](https://powerlighttech.com/), formerly known as , has been developing laser-based power-beaming systems for more than a decade. Renowned for winning the [NASA Power Beaming Challenge](https://www.nasa.gov/) in 2009, this company has not only achieved success in powering robotic tether climbers, quadcopters, and fixed-wing drones, but it has also delved deeply into the challenges of safely beaming power with . That’s key, because many research groups have demonstrated laser power beaming over the years—including teams at the Naval Research Laboratory, [Kindai University](https://www.kindai.ac.jp/english/), the [Beijing Institute of Technology](https://english.bit.edu.cn/), the [University of Colorado Boulder](https://www.colorado.edu/), [JAXA](https://global.jaxa.jp/), [Airbus](https://www.airbus.com/), and others—but only a few have accomplished it in a fashion that is truly safe under every plausible circumstance.

![This diagram shows the peak power levels and distance achieved in 11 power-beaming demonstrations carried out between 1975 and 2021](https://spectrum.ieee.org/www.w3.org/2000/svg'%20viewBox='0%200%201195%201557'%3E%3C/svg%3E)

There have been many demonstrations of power beaming over the years, using either microwaves \[blue\] or lasers \[red\], with the peak-power record having been set in 1975 \[top\]. In 2021, the author and his colleagues took second and third place for the peak-power level achieved in such experiments, having beamed more than a kilowatt over distances that exceeded a kilometer, using much smaller antennas.

Perhaps the most dramatic demonstration of safe laser power beaming prior to our team’s effort was by the company [Lighthouse Dev](https://www.lhdev.com/) in 2012. To underscore how safe the system was, the host of the BBC science program “ [Bang Goes the Theory](https://www.bbc.co.uk/programmes/b00lwxj1) ” stuck his face fully into a power beam sent between buildings at the [University of Maryland](https://www.umd.edu/). This particular demonstration took advantage of the fact that some infrared wavelengths are an order of magnitude safer for your eyes than other parts of the infrared spectrum.  

That strategy works for relatively low-power systems. But as you push the level higher, you soon get to power densities that raise safety concerns regardless of the wavelength used. What then? Here’s where the system we’ve demonstrated sets itself apart. While sending more than 400 watts over a distance that exceeded 300 meters, the beam was contained within a virtual enclosure, one that could sense an object impinging on it and trigger the equipment to cut power to the main beam before any damage was done. Other testing has shown how transmission distances can exceed a kilometer.

Careful testing (for which no BBC science-program hosts were used) verified to our satisfaction the functionality of this feature, which also passed muster with the Navy’s Laser Safety Review Board. During the course of our demonstration, the system further proved itself when, on several occasions, birds flew toward the beam, shutting it off—but only momentarily. You see, the system monitors the volume the beam occupies, along with its immediate surroundings, allowing the power link to automatically reestablish itself when the path is once again clear. Think of it as a more sophisticated version of a garage-door safety sensor, where the interruption of a guard beam triggers the motor driving the door to shut off.

The 400 watts we were able to transmit was, admittedly, not a huge amount, but it was sufficient to brew us some coffee.

For our demonstrations, observers in attendance were able to walk around between the transmitter and receiver without needing to wear laser-safety eyewear or take any other precautions. That’s because, in addition to designing the system so that it can shut itself down automatically, we took care to consider the possible effects of from the receiver or the scattering of light from particles suspended in the air along the path of the beam.

![](https://spectrum.ieee.org/www.w3.org/2000/svg'%20viewBox='0%200%202500%201664'%3E%3C/svg%3E)

![](https://spectrum.ieee.org/www.w3.org/2000/svg'%20viewBox='0%200%202500%201664'%3E%3C/svg%3E)

![This set of three images shows a large white parabolic dish at the top, a gold-colored square in the middle, and a tall metal tower at the bottom.](https://spectrum.ieee.org/www.w3.org/2000/svg'%20viewBox='0%200%202100%203156'%3E%3C/svg%3E)

Last year, the author and his colleagues carried out a demonstration at the U.S. Army’s Blossom Point test facility south of Washington, D.C. They used 9.7-gigahertz microwaves to send 1,649 watts (peak power) from a transmitter outfitted with a 5.4-meter diameter parabolic dish \[top\] over a distance of 1,046 meters to a 2-by-2-meter “rectenna” \[middle\] mounted on a tower \[bottom\], which transformed the beam into usable electric power.

The 400 watts we were able to transmit was, admittedly, not a huge amount, but it was sufficient to brew us some coffee, continuing what’s become de rigueur in this line of experimentation: making a hot beverage. (The Japanese researchers who started this tradition in 2015 prepared themselves some tea.)

Our next goal is to apply power beaming, with fully integrated safety measures, to mobile platforms. For that, we expect to increase the distance covered and the amount of power delivered.

But we’re not alone: Other governments, established companies, and around the world are working to develop their own power-beaming systems. Japan has long been a leader in microwave and laser power beaming, and China has closed the gap if not pulled ahead, as has

At the consumer-electronics level, there are many players: [Powercast](https://www.powercastco.com/), [Ossia](https://www.ossia.com/), [Energous](https://energous.com/), [GuRu](https://guru.inc/), and [Wi-Charge](https://www.wi-charge.com/) among them. And the multinational technology giant power beaming for smartphone charging within “two or three \[phone\] generations.”

For industrial applications, companies like [Reach Labs](https://reachlabs.co/), [TransferFi](https://www.transferfi.com/), [MH GoPower](https://www.mhgopower.com/mhmain.html), and [MetaPower](https://www.metapower.co/) are making headway in employing power beaming to solve the thorny problem of keeping for robots and sensors, in warehouses and elsewhere, topped off and ready to go. At the grid level, [Emrod](https://emrod.energy/) and others are attempting to scale power beaming to new heights.

On the R&D front, our team demonstrated within the past year safe microwave wireless power transmission of [1.6 kilowatts over a distance of a kilometer.](https://ieeexplore.ieee.org/document/9662403) Companies like [II-VI Aerospace & Defense](https://ii-vi.com/aerospace-defense/), [Peraton Labs](https://www.peratonlabs.com/), Lighthouse Dev, and others have also recently made impressive strides. Today, ambitious startups like [Solar Space Technologies](https://www.solarspacetechnologies.com.au/), [Solaren](https://www.solarenspace.com/), [Virtus Solis](https://www.virtussolis.space/), and others operating in stealth mode are working hard to be the first to achieve practical power beaming from space to Earth.

As such companies establish proven track records for safety and make compelling arguments for the utility of their systems, we are likely to see whole new architectures emerge for sending power from place to place. Imagine drones that can fly for indefinite periods and electrical devices that never need to be plugged in—ever—and being able to provide people anywhere in the world with energy when hurricanes or other natural disasters ravage the local . Reducing the need to transport fuel, batteries, or other forms of stored energy will have far-reaching consequences. It’s not the only option when you can’t string wires, but my colleagues and I expect, within the set of possible technologies for providing electricity to far-flung spots, that power beaming will, quite literally, shine.

*This article appears in the June 2022 print issue as “Spooky Power at a Distance.”*