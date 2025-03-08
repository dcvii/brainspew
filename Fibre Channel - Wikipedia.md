---
title: "Fibre Channel - Wikipedia"
source: "https://en.wikipedia.org/wiki/Fibre_Channel"
author:
  - "[[Contributors to Wikimedia projects]]"
published: 2002-11-02
created: 2025-02-16
description:
tags:
  - "clippings"
---
From Wikipedia, the free encyclopedia

Computer storage networking technology

<table><tbody><tr><th colspan="2"><a>Fibre Channel</a></th></tr><tr><th colspan="2">Layer&nbsp;4.&nbsp;Protocol mapping</th></tr><tr><td colspan="2"><a href="https://en.wikipedia.org/wiki/Logical_Unit_Number_Masking">LUN masking</a></td></tr><tr><th colspan="2">Layer&nbsp;3.&nbsp;Common services</th></tr><tr><th colspan="2">Layer&nbsp;2.&nbsp;Network</th></tr><tr><td colspan="2"><a href="https://en.wikipedia.org/wiki/Fibre_Channel_fabric">Fibre Channel fabric</a><br><a href="https://en.wikipedia.org/wiki/Fibre_Channel_zoning">Fibre Channel zoning</a><br><a href="https://en.wikipedia.org/wiki/Registered_state_change_notification">Registered state change notification</a></td></tr><tr><th colspan="2">Layer&nbsp;1.&nbsp;Data link</th></tr><tr><td colspan="2"><a href="https://en.wikipedia.org/wiki/Fibre_Channel_8b/10b_encoding">Fibre Channel 8b/10b encoding</a></td></tr><tr><th colspan="2">Layer&nbsp;0.&nbsp;Physical</th></tr></tbody></table>

**Fibre Channel** (**FC**) is a high-speed data transfer protocol providing in-order, lossless[^fibrechannel.org-1] delivery of raw block data.[^2] Fibre Channel is primarily used to connect [computer data storage](https://en.wikipedia.org/wiki/Computer_data_storage "Computer data storage") to [servers](https://en.wikipedia.org/wiki/Server_\(computing\) "Server (computing)")[^preston-3][^riabov-4] in [storage area networks](https://en.wikipedia.org/wiki/Storage_area_network "Storage area network") (SAN) in commercial [data centers](https://en.wikipedia.org/wiki/Data_center "Data center").

Fibre Channel networks form a [switched fabric](https://en.wikipedia.org/wiki/Switched_fabric "Switched fabric") because the switches in a network operate in unison as one big switch. Fibre Channel typically runs on [optical fiber](https://en.wikipedia.org/wiki/Optical_fiber "Optical fiber") cables within and between data centers, but can also run on copper cabling.[^preston-3][^riabov-4] Supported data rates include 1, 2, 4, 8, 16, 32, 64, and 128 [gigabit per second](https://en.wikipedia.org/wiki/Gigabit_per_second "Gigabit per second") resulting from improvements in successive technology generations. The industry now notates this as Gigabit Fibre Channel (GFC).

There are various upper-level protocols for Fibre Channel, including two for block storage. [Fibre Channel Protocol](https://en.wikipedia.org/wiki/Fibre_Channel_Protocol "Fibre Channel Protocol") (FCP) is a protocol that transports [SCSI](https://en.wikipedia.org/wiki/Small_Computer_System_Interface "Small Computer System Interface") commands over Fibre Channel networks.[^preston-3][^riabov-4] [FICON](https://en.wikipedia.org/wiki/FICON "FICON") is a protocol that transports [ESCON](https://en.wikipedia.org/wiki/ESCON "ESCON") commands, used by [IBM mainframe](https://en.wikipedia.org/wiki/IBM_mainframe "IBM mainframe") computers, over Fibre Channel. Fibre Channel can be used to transport data from storage systems that use solid-state [flash memory](https://en.wikipedia.org/wiki/Flash_memory "Flash memory") storage medium by transporting [NVMe](https://en.wikipedia.org/wiki/NVM_Express "NVM Express") protocol commands.

When the technology was originally devised, it ran over optical fiber cables only and, as such, was called "Fiber Channel". Later, the ability to run over copper cabling was added to the specification. In order to avoid confusion and to create a unique name, the industry decided to change the spelling and use the [British English](https://en.wikipedia.org/wiki/British_English "British English") *fibre* for the name of the standard.[^tate-5]

Fibre Channel is standardized in the [T11 Technical Committee](https://en.wikipedia.org/wiki/Technical_Committee_T11 "Technical Committee T11") of the International Committee for Information Technology Standards ([INCITS](https://en.wikipedia.org/wiki/INCITS "INCITS")), an [American National Standards Institute](https://en.wikipedia.org/wiki/American_National_Standards_Institute "American National Standards Institute") (ANSI)-accredited standards committee. Fibre Channel started in 1988, with ANSI standard approval in 1994, to merge the benefits of multiple physical layer implementations including [SCSI](https://en.wikipedia.org/wiki/SCSI_connector "SCSI connector"), [HIPPI](https://en.wikipedia.org/wiki/HIPPI "HIPPI") and [ESCON](https://en.wikipedia.org/wiki/ESCON "ESCON").

Fibre Channel was designed as a [serial interface](https://en.wikipedia.org/wiki/Serial_communication "Serial communication") to overcome limitations of the SCSI and HIPPI physical-layer parallel-signal copper wire interfaces. Such interfaces face the challenge of, among other things, maintaining signal timing coherence across all the data-signal wires (8, 16 and finally 32 for SCSI, 50 for HIPPI) so that a receiver can determine when all the electrical signal values are "good" (stable and valid for simultaneous reception sampling). This challenge becomes evermore difficult in a mass-manufactured technology as data signal frequencies increase, with part of the technical compensation being ever reducing the supported connecting copper-parallel cable length. See [Parallel SCSI](https://en.wikipedia.org/wiki/Parallel_SCSI "Parallel SCSI"). FC was developed with leading-edge [multi-mode optical fiber](https://en.wikipedia.org/wiki/Multi-mode_optical_fiber "Multi-mode optical fiber") technologies that overcame the speed limitations of the ESCON protocol. By appealing to the large base of SCSI disk drives and leveraging mainframe technologies, Fibre Channel developed [economies of scale](https://en.wikipedia.org/wiki/Economies_of_scale "Economies of scale") for advanced technologies and deployments became economical and widespread.

Commercial products were released while the standard was still in draft.[^zg940168-6] By the time the standard was ratified lower speed versions were already growing out of use.[^7] Fibre Channel was the first serial storage transport to achieve gigabit speeds[^8] where it saw wide adoption, and its success grew with each successive speed. Fibre Channel has doubled in speed every few years since 1996.

In addition to a modern physical layer, Fibre Channel also added support for any number of "upper layer" protocols, including [ATM](https://en.wikipedia.org/wiki/Asynchronous_Transfer_Mode "Asynchronous Transfer Mode"), [IP](https://en.wikipedia.org/wiki/Internet_Protocol "Internet Protocol") ([IPFC](https://en.wikipedia.org/wiki/IPFC "IPFC")) and [FICON](https://en.wikipedia.org/wiki/FICON "FICON"), with [SCSI](https://en.wikipedia.org/wiki/SCSI "SCSI") ([FCP](https://en.wikipedia.org/wiki/Fibre_Channel_Protocol "Fibre Channel Protocol")) being the predominant usage.

Fibre Channel has seen active development since its inception, with numerous speed improvements on a variety of underlying transport media. The following tables shows the progression of native Fibre Channel speeds:[^9]

| Name | Line-rate ([gigabaud](https://en.wikipedia.org/wiki/Baud "Baud")) | Line coding | Nominal throughput per direction (MB/s) | Market availability |
| --- | --- | --- | --- | --- |
| 133 Mbit/s | 0.1328125 | [8b10b](https://en.wikipedia.org/wiki/8b/10b_encoding "8b/10b encoding") | 12.5 | 1993 |
| 266 Mbit/s | 0.265625 | 8b10b | 25 | 1994[^zg940168-6] |
| 533 Mbit/s | 0.53125 | 8b10b | 50 | ? |
| 1GFC (Gen 1) | 1.0625 | 8b10b | 100 | 1997 |
| 2GFC (Gen 2) | 2.125 | 8b10b | 200 | 2001 |
| 4GFC (Gen 3) | 4.25 | 8b10b | 400 | 2004 |
| 8GFC (Gen 4) | 8.5 | 8b10b | 800 | 2008 |
| 16GFC (Gen 5) | 14.025 | [64b66b](https://en.wikipedia.org/wiki/64b/66b_encoding "64b/66b encoding") | 1,600 | 2011 |
| 32GFC (Gen 6) | 28.05 | 256b257b | 3,200 | 2016[^g620release-11] |
| 64GFC (Gen 7) | 28.9 | 256b257b (FC-FS-5) | 6,400 | 2020 |
| 128GFC (Gen 8) | 56.1[^12] | 256b257b | 12,800 | Planned 2025 |

FC used throughout all applications for Fibre Channel infrastructure and devices, including edge and ISL interconnects. Each speed maintains backward compatibility at least two previous generations (I.e., 32GFC backward compatible to 16GFC and 8GFC)

| Name | Line-rate ([gigabaud](https://en.wikipedia.org/wiki/Baud "Baud")) | Line coding | Nominal throughput per direction (MB/s) | Market availability |
| --- | --- | --- | --- | --- |
| 10GFC | 10.51875 | 64b66b | 1,200 | 2009 |
| 128GFC (Gen 6) | 28.05 × 4 | 256b257b | 12,800 | 2016[^g620release-11] |
| 256GFC (Gen 7) | 28.9 × 4 | 256b257b | 25,600 | 2020 |

Inter-Switch Links, ISLs, are usually multi-lane interconnects used for non-edge, core connections, and other high speed applications demanding maximum bandwidth. ISL’s utilize high bit-rates to accommodate the funneling of edge connections. Some ISL solutions are vendor-proprietary.

Two major characteristics of Fibre Channel networks are in-order delivery and lossless delivery of raw block data. Lossless delivery of raw data block is achieved based on a credit mechanism.[^fibrechannel.org-1]

There are three major Fibre Channel topologies, describing how a number of [ports](https://en.wikipedia.org/wiki/Computer_port_\(software\) "Computer port (software)") are connected together. A *port* in Fibre Channel terminology is any entity that actively communicates over the network, not necessarily a [hardware port](https://en.wikipedia.org/wiki/Computer_port_\(hardware\) "Computer port (hardware)"). This port is usually implemented in a device such as disk storage, a Host Bus Adapter ([HBA](https://en.wikipedia.org/wiki/Host_bus_adapter "Host bus adapter")) network connection on a server or a [Fibre Channel switch](https://en.wikipedia.org/wiki/Fibre_channel_switch "Fibre channel switch").[^preston-3]

![Point-to-Point topology connection using N ports](https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Point-to-Point_topology.svg/320px-Point-to-Point_topology.svg.png)

Topology diagram of a Fibre Channel point-to-point connection

- **Point-to-point** (see *FC-FS-3*). Two devices are connected directly to each other using [N\_ports](https://en.wikipedia.org/wiki/#Ports). This is the simplest topology, with limited connectivity.[^preston-3] The bandwidth is dedicated.
- **[Arbitrated loop](https://en.wikipedia.org/wiki/Arbitrated_loop "Arbitrated loop")** (see *FC-AL-2*). In this design, all devices are in a loop or ring, similar to [Token Ring](https://en.wikipedia.org/wiki/Token_Ring "Token Ring") networking. Adding or removing a device from the loop causes all activity on the loop to be interrupted. The failure of one device causes a break in the ring. Fibre Channel hubs exist to connect multiple devices together and may bypass failed ports. A loop may also be made by cabling each port to the next in a ring.
- A minimal loop containing only two ports, while appearing to be similar to point-to-point, differs considerably in terms of the protocol.
- Only one pair of ports can communicate concurrently on a loop.
- Maximum speed of 8GFC.
- Arbitrated Loop has been rarely used after 2010 and its support is being discontinued for new gen switches.
- **[Switched Fabric](https://en.wikipedia.org/wiki/Fibre_Channel_fabric "Fibre Channel fabric")** (see *FC-SW-6*). In this design, all devices are connected to [Fibre Channel switches](https://en.wikipedia.org/wiki/Fibre_channel_switch "Fibre channel switch"), similar conceptually to modern [Ethernet](https://en.wikipedia.org/wiki/Ethernet "Ethernet") implementations. Advantages of this topology over point-to-point or Arbitrated Loop include:
- The Fabric can scale to tens of thousands of ports.
- The switches manage the state of the Fabric, providing optimized paths via Fabric Shortest Path First (FSPF) data routing protocol.
- The traffic between two ports flows through the switches and not through any other ports like in Arbitrated Loop.
- Failure of a port is isolated to a link and should not affect operation of other ports.
- Multiple pairs of ports may communicate simultaneously in a Fabric.

| Attribute | Point-to-point | Arbitrated loop | Switched fabric |
| --- | --- | --- | --- |
| Max ports | 2 | 127 | ~16777216 (2<sup>24</sup>) |
| Address size | — | 8-[bit](https://en.wikipedia.org/wiki/Bit "Bit") ALPA | 24-bit port ID |
| Side effect of port failure | Link fails | Loop fails (until port bypassed) | — |
| Access to medium | Dedicated | Arbitrated | Dedicated |

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/Fibre_Channel_layers.svg/220px-Fibre_Channel_layers.svg.png)

Fibre Channel is a layered technology that starts at the physical layer and progresses through the protocols to the upper-level protocols like SCSI and SBCCS.

Fibre Channel does not follow the [OSI model](https://en.wikipedia.org/wiki/OSI_model "OSI model") layering, and is split into five layers:

- **FC-4** – Protocol-mapping layer, in which upper-level protocols such as [NVM Express](https://en.wikipedia.org/wiki/NVM_Express "NVM Express") (NVMe), [SCSI](https://en.wikipedia.org/wiki/SCSI "SCSI"), IP, and [FICON](https://en.wikipedia.org/wiki/FICON "FICON") are encapsulated into Information Units (IUs) for delivery to FC-2. Current FC-4s include FCP-4, FC-SB-5, and [FC-NVMe](https://en.wikipedia.org/wiki/NVMe#NVMe-oF "NVMe").
- **FC-3** – Common services layer, a thin layer that could eventually implement functions like [encryption](https://en.wikipedia.org/wiki/Encryption "Encryption") or [RAID](https://en.wikipedia.org/wiki/RAID "RAID") redundancy algorithms; multiport connections;
- **FC-2** – Signaling Protocol, defined by the *Fibre Channel Framing and Signaling* standard, consists of the low level [Fibre Channel network protocols](https://en.wikipedia.org/wiki/Fibre_Channel_network_protocols "Fibre Channel network protocols"); port to port connections;
- **FC-1** – Transmission Protocol, which implements [line coding](https://en.wikipedia.org/wiki/Line_coding "Line coding") of signals;
- **FC-0** – [physical layer](https://en.wikipedia.org/wiki/Physical_layer "Physical layer"), defined by *Fibre Channel Physical Interfaces* standard, includes cabling, [connectors](https://en.wikipedia.org/wiki/Fibre_channel_electrical_interface "Fibre channel electrical interface") etc.;

Fibre Channel products are available at 1, 2, 4, 8, 10, 16 and 32 and 128 Gbit/s; these protocol flavors are called accordingly 1GFC, 2GFC, 4GFC, 8GFC, 10GFC, 16GFC, 32GFC or 128GFC. The 32GFC standard was approved by the INCITS T11 committee in 2013, and those products became available in 2016. The 1GFC, 2GFC, 4GFC, 8GFC designs all use [8b/10b encoding](https://en.wikipedia.org/wiki/8b/10b_encoding "8b/10b encoding"), while the 10GFC and 16GFC standard uses [64b/66b encoding](https://en.wikipedia.org/wiki/64B/66B_encoding "64B/66B encoding"). Unlike the 10GFC standards, 16GFC provides backward compatibility with 4GFC and 8GFC since it provides exactly twice the throughput of 8GFC or four times that of 4GFC.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/68/Fibre_Channel_Topologies.svg/220px-Fibre_Channel_Topologies.svg.png)

FC topologies and port types: This diagram shows how N\_Ports can be connected to a fabric or to another N\_Port. A Loop Port (L\_Port) communicates through a shared loop and is rarely used anymore.

Fibre Channel ports come in a variety of logical configurations. The most common types of ports are:

- **N\_Port (Node port)** An N\_Port is typically an HBA port that connects to a switch's F\_Port or another N\_Port. Nx\_Port communicating through a PN\_Port that is not operating a Loop Port State Machine.[^fc-fs-4-13]
- **F\_Port (Fabric port)** An F\_Port is a switch port that is connected to an N\_Port.[^fc-sw-6-14]
- **E\_Port (Expansion port)** Switch port that attaches to another E\_Port to create an Inter-Switch Link.[^fc-sw-6-14]

Fibre Channel Loop protocols create multiple types of Loop Ports:

- **L\_Port (Loop port)** FC\_Port that contains Arbitrated Loop functions associated with the Arbitrated Loop topology.[^fc-sw-6-14]
- **FL\_Port (Fabric Loop port)** L\_Port that is able to perform the function of an F\_Port, attached via a link to one or more NL\_Ports in an Arbitrated Loop topology.[^fc-sw-6-14]
- **NL\_Port (Node Loop port)** PN\_Port that is operating a Loop port state machine.[^fc-sw-6-14]

If a port can support loop and non-loop functionality, the port is known as:

- **Fx\_Port** switch port capable of operating as an F\_Port or FL\_Port.[^fc-fs-4-13]
- **Nx\_Port** end point for Fibre Channel frame communication, having a distinct address identifier and Name\_Identifier, providing an independent set of FC-2V functions to higher levels, and having the ability to act as an Originator, a Responder, or both.[^fc-fs-4-13]

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/FC-platform-vnode.svg/360px-FC-platform-vnode.svg.png)

A Port has a physical structure as well as logical or virtual structure. This diagram shows how a virtual port may have multiple physical ports and vice versa.

Ports have virtual components and physical components and are described as:

- **PN\_Port** entity that includes a Link\_Control\_Facility and one or more Nx\_Ports.[^fc-sw-6-14]
- **VF\_Port (Virtual F\_Port)** instance of the FC-2V sublevel that connects to one or more VN\_Ports.[^fc-sw-6-14]
- **VN\_Port (Virtual N\_Port)** instance of the FC-2V sublevel. VN\_Port is used when it is desired to emphasize support for multiple Nx\_Ports on a single Multiplexer (e.g., via a single PN\_Port).[^fc-fs-4-13]
- **VE\_Port (Virtual E\_Port)** instance of the FC-2V sublevel that connects to another VE\_Port or to a B\_Port to create an Inter-Switch Link.[^fc-sw-6-14]

The following types of ports are also used in Fibre Channel:

- **A\_Port (Adjacent port)** combination of one PA\_Port and one VA\_Port operating together.[^fc-sw-6-14]
- **B\_Port (Bridge Port)** Fabric inter-element port used to connect bridge devices with E\_Ports on a Switch.[^fc-fs-4-13]
- **D\_Port (Diagnostic Port)** A configured port used to perform diagnostic tests on a link with another D\_Port.[^bcfa_nutshell-15]
- **EX\_Port** A type of E\_Port used to connect to an FC router fabric.[^bcfa_nutshell-15]
- **G\_Port (Generic Fabric port)** Switch port that may function either as an E\_Port, A\_Port, or as an F\_Port.[^fc-sw-6-14]
- **GL\_Port (Generic Fabric Loop port)** Switch port that may function either as an E\_Port, A\_Port, or as an Fx\_Port.[^fc-sw-6-14]
- **PE\_Port** LCF within the Fabric that attaches to another PE\_Port or to a B\_Port through a link.[^fc-fs-4-13]
- **PF\_Port** LCF within a Fabric that attaches to a PN\_Port through a link.[^fc-fs-4-13]
- **TE\_Port (Trunking E\_Port) A trunking expansion port that** expands the functionality of E ports to support VSAN trunking, Transport quality of service (QoS) parameters, and Fibre Channel trace (fctrace) feature.[^16]
- **U\_Port** **(Universal port)** A port waiting to become another port type[^bcfa_nutshell-15]
- **VA\_Port (Virtual A\_Port)** instance of the FC-2V sublevel of Fibre Channel that connects to another VA\_Port.[^fc-sw-6-14]
- **VEX\_Port** VEX\_Ports are no different from EX\_Ports, except underlying transport is IP rather than FC.[^bcfa_nutshell-15]

| [![](https://upload.wikimedia.org/wikipedia/en/thumb/6/6c/Wiki_letter_w.svg/44px-Wiki_letter_w.svg.png)](https://en.wikipedia.org/wiki/File:Wiki_letter_w.svg) | This section **is missing information** about legacy copper interfaces. Please expand the section to include this information. Further details may exist on the [talk page](https://en.wikipedia.org/wiki/Talk:Fibre_Channel "Talk:Fibre Channel"). *(November 2023)* |
| --- | --- |

| ![Exclamation mark with arrows pointing at each other](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/Ambox_contradict.svg/38px-Ambox_contradict.svg.png) | This section **appears to contradict itself**. Please see the [talk page](https://en.wikipedia.org/wiki/Talk:Fibre_Channel "Talk:Fibre Channel") for more information. *(November 2023)* |
| --- | --- |

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/Fibre_Channel_Media_and_Modules.png/220px-Fibre_Channel_Media_and_Modules.png)

Fibre Channel predominantly uses SFP or SFP+ modules with LC connector and duplex cabling, but 128GFC uses QSFP28 modules with MPO connectors and ribbon cabling.

The Fibre Channel physical layer is based on serial connections that use fiber optics to copper between corresponding pluggable modules. The modules may have a single lane, dual lanes or quad lanes that correspond to the SFP, SFP-DD and QSFP form factors. Fibre Channel does not use 8- or 16-lane modules (like CFP8, QSFP-DD, or COBO used in 400GbE) and there are no plans to use these expensive and complex modules.

The [small form-factor pluggable transceiver](https://en.wikipedia.org/wiki/Small_form-factor_pluggable_transceiver "Small form-factor pluggable transceiver") (SFP) module and its enhanced version SFP+, SFP28 and SFP56 are common form factors for Fibre Channel ports. SFP modules support a variety of distances via multi-mode and [single-mode optical fiber](https://en.wikipedia.org/wiki/Single-mode_optical_fiber "Single-mode optical fiber") as shown in the table below. SFP modules use duplex fiber cabling with LC connectors.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ce/SFP-DD_SMT_17c.png/220px-SFP-DD_SMT_17c.png)

SFP-DD modules are used in high-density applications that need to double the throughput of traditional SFP ports.

SFP-DD modules are used for high-density applications that need to double the throughput of an SFP Port. SFP-DD is defined by the SFP-DD MSA and enables breakout to two SFP ports. Two rows of electrical contacts enable doubling the throughput of SFP modules in a similar fashion as QSFP-DD.

The [quad small form-factor pluggable](https://en.wikipedia.org/wiki/QSFP "QSFP") (QSFP) module began being used for switch inter-connectivity and was later adopted for use in 4-lane implementations of Gen-6 Fibre Channel supporting 128GFC. QSFP uses either LC connectors for 128GFC-CWDM4 or MPO connectors for 128GFC-SW4 or 128GFC-PSM4. MPO cabling uses 8- or 12-fiber cabling infrastructure that connects to another 128GFC port or may be broken out into four duplex LC connections to 32GFC SFP+ ports. Fibre Channel switches use either SFP or QSFP modules.

<table><thead><tr><th>Fiber type</th><th>Speed <span>(MB/s)</span></th><th>Transmitter<sup><a href="https://en.wikipedia.org/wiki/#cite_note-17"><span>[</span>17<span>]</span></a></sup></th><th>Medium variant</th><th>Distance</th></tr></thead><tbody><tr><th rowspan="17">Single-mode fiber (SMF)</th><td rowspan="2">12,800</td><td>1,310&nbsp;nm longwave light</td><td>128GFC-PSM4</td><td>0.5m - 0.5&nbsp;km</td></tr><tr><td>1,270, 1,290, 1,310 and 1,330&nbsp;nm longwave light</td><td>128GFC-CWDM4</td><td>0.5 m – 2&nbsp;km</td></tr><tr><td>6,400</td><td>1,310&nbsp;nm longwave light</td><td>64GFC-LW</td><td>0.5m - 10&nbsp;km</td></tr><tr><td>3,200</td><td>1,310&nbsp;nm longwave light</td><td>3200-SM-LC-L</td><td>0.5 m - 10&nbsp;km</td></tr><tr><td rowspan="2">1,600</td><td>1,310&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_6.3-18"><span>[</span>ITS 1<span>]</span></a></sup></td><td>1600-SM-LC-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.1-19"><span>[</span>ITS 2<span>]</span></a></sup></td><td>0.5&nbsp;m&nbsp;– 10&nbsp;km</td></tr><tr><td>1,490&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_6.3-18"><span>[</span>ITS 1<span>]</span></a></sup></td><td>1600-SM-LZ-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.1-19"><span>[</span>ITS 2<span>]</span></a></sup></td><td>0.5&nbsp;m&nbsp;– 2&nbsp;km</td></tr><tr><td rowspan="2">800</td><td rowspan="2">1,310&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_6.3-20"><span>[</span>ITS 3<span>]</span></a></sup></td><td>800-SM-LC-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.1-21"><span>[</span>ITS 4<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 10&nbsp;km</td></tr><tr><td>800-SM-LC-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.1-21"><span>[</span>ITS 4<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 1.4&nbsp;km</td></tr><tr><td rowspan="3">400</td><td rowspan="3">1,310&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_6.3-20"><span>[</span>ITS 3<span>]</span></a></sup><sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH-2_lists_1300nm_(see_clause_6.1_and_8.1)-22"><span>[</span>ITS 5<span>]</span></a></sup></td><td>400-SM-LC-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_clause_8.1-23"><span>[</span>ITS 6<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 10&nbsp;km</td></tr><tr><td>400-SM-LC-M<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.1-21"><span>[</span>ITS 4<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 4&nbsp;km</td></tr><tr><td>400-SM-LL-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH-2_clause_8.1-24"><span>[</span>ITS 7<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 2&nbsp;km</td></tr><tr><td rowspan="3">200</td><td>1,550&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_11-25"><span>[</span>ITS 8<span>]</span></a></sup></td><td>200-SM-LL-V<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_11-25"><span>[</span>ITS 8<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 50&nbsp;km</td></tr><tr><td rowspan="2">1,310&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH-2_lists_1300nm_(see_clause_6.1_and_8.1)-22"><span>[</span>ITS 5<span>]</span></a></sup><sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_6.3-20"><span>[</span>ITS 3<span>]</span></a></sup></td><td>200-SM-LC-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_clause_8.1-23"><span>[</span>ITS 6<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 10&nbsp;km</td></tr><tr><td>200-SM-LL-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH-2_clause_8.1-24"><span>[</span>ITS 7<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 2&nbsp;km</td></tr><tr><td rowspan="3">100</td><td>1,550&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_11-25"><span>[</span>ITS 8<span>]</span></a></sup></td><td>100-SM-LL-V<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_11-25"><span>[</span>ITS 8<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 50&nbsp;km</td></tr><tr><td rowspan="2">1,310&nbsp;nm longwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-26"><span>[</span>ITS 9<span>]</span></a></sup><sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_6.3-20"><span>[</span>ITS 3<span>]</span></a></sup></td><td>100-SM-LL-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH_Clause_8.1-27"><span>[</span>ITS 10<span>]</span></a></sup><br>100-SM-LC-L<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_clause_8.1-23"><span>[</span>ITS 6<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 10&nbsp;km</td></tr><tr><td>100-SM-LL-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PH_Clause_8.1-27"><span>[</span>ITS 10<span>]</span></a></sup></td><td>2&nbsp;m&nbsp;– 2&nbsp;km</td></tr><tr><th rowspan="23">Multi-mode fiber (MMF)</th><td>12,800</td><td rowspan="23">850&nbsp;nm shortwave light<sup><a href="https://en.wikipedia.org/wiki/#cite_note-28"><span>[</span>ITS 11<span>]</span></a></sup><sup><a href="https://en.wikipedia.org/wiki/#cite_note-29"><span>[</span>ITS 12<span>]</span></a></sup><sup><a href="https://en.wikipedia.org/wiki/#cite_note-30"><span>[</span>ITS 13<span>]</span></a></sup></td><td>128GFC-SW4</td><td>0–100&nbsp;m</td></tr><tr><td>6,400</td><td>64GFC-SW</td><td>0–100&nbsp;m</td></tr><tr><td>3,200</td><td>3200-SN</td><td>0–100&nbsp;m</td></tr><tr><td rowspan="4">1,600</td><td>1600-M5F-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.2-31"><span>[</span>ITS 14<span>]</span></a></sup></td><td>0.5–125&nbsp;m</td></tr><tr><td>1600-M5E-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.2-31"><span>[</span>ITS 14<span>]</span></a></sup></td><td>0.5–100&nbsp;m</td></tr><tr><td>1600-M5-SN-S<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.2-31"><span>[</span>ITS 14<span>]</span></a></sup></td><td>0.5–35&nbsp;m</td></tr><tr><td>1600-M6-SN-S<sup><a href="https://en.wikipedia.org/wiki/#cite_note-32"><span>[</span>ITS 15<span>]</span></a></sup></td><td>0.5–15&nbsp;m</td></tr><tr><td rowspan="4">800</td><td>800-M5F-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.2-31"><span>[</span>ITS 14<span>]</span></a></sup></td><td>0.5–190&nbsp;m</td></tr><tr><td>800-M5E-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.2-33"><span>[</span>ITS 16<span>]</span></a></sup></td><td>0.5–150&nbsp;m</td></tr><tr><td>800-M5-SN-S<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.2-33"><span>[</span>ITS 16<span>]</span></a></sup></td><td>0.5–50&nbsp;m</td></tr><tr><td>800-M6-SN-S<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.2-33"><span>[</span>ITS 16<span>]</span></a></sup></td><td>0.5–21&nbsp;m</td></tr><tr><td rowspan="4">400</td><td>400-M5F-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-5_Clause_8.2-31"><span>[</span>ITS 14<span>]</span></a></sup></td><td>0.5–400&nbsp;m</td></tr><tr><td>400-M5E-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.2-33"><span>[</span>ITS 16<span>]</span></a></sup></td><td>0.5–380&nbsp;m</td></tr><tr><td>400-M5-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_Clause_8.2-34"><span>[</span>ITS 17<span>]</span></a></sup></td><td>0.5–150&nbsp;m</td></tr><tr><td>400-M6-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_Clause_8.2-34"><span>[</span>ITS 17<span>]</span></a></sup></td><td>0.5–70&nbsp;m</td></tr><tr><td rowspan="3">200</td><td>200-M5E-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI-4_Clause_8.2-33"><span>[</span>ITS 16<span>]</span></a></sup></td><td>0.5–500&nbsp;m</td></tr><tr><td>200-M5-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_Clause_8.2-34"><span>[</span>ITS 17<span>]</span></a></sup></td><td>0.5–300&nbsp;m</td></tr><tr><td>200-M6-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-FC-PI_Clause_8.2-34"><span>[</span>ITS 17<span>]</span></a></sup></td><td>0.5–150&nbsp;m</td></tr><tr><td rowspan="5">100</td><td>100-M5E-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-35"><span>[</span>ITS 18<span>]</span></a></sup></td><td>0.5–860&nbsp;m</td></tr><tr><td>100-M5-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-PC-PI_Clause_8.2-36"><span>[</span>ITS 19<span>]</span></a></sup></td><td>0.5–500&nbsp;m</td></tr><tr><td>100-M6-SN-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-PC-PI_Clause_8.2-36"><span>[</span>ITS 19<span>]</span></a></sup></td><td>0.5–300&nbsp;m</td></tr><tr><td>100-M5-SL-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-PC-PI_Clause_8.2-36"><span>[</span>ITS 19<span>]</span></a></sup></td><td>2–500&nbsp;m</td></tr><tr><td>100-M6-SL-I<sup><a href="https://en.wikipedia.org/wiki/#cite_note-37"><span>[</span>ITS 20<span>]</span></a></sup></td><td>2–175&nbsp;m</td></tr></tbody><tfoot></tfoot></table>

| Multi-mode fiber | Fiber diameter | FC media designation |
| --- | --- | --- |
| OM1 | 62.5 μm | M6 |
| OM2 | 50 μm | M5 |
| OM3 | 50 μm | M5E |
| OM4 | 50 μm | M5F |
| OM5 | 50 μm | N/A |

Modern Fibre Channel devices support [SFP+](https://en.wikipedia.org/wiki/Small_form-factor_pluggable_transceiver "Small form-factor pluggable transceiver") transceiver, mainly with [LC](https://en.wikipedia.org/wiki/Optical_fiber_connector "Optical fiber connector") (Lucent Connector) fiber connector. Older 1GFC devices used [GBIC](https://en.wikipedia.org/wiki/GBIC "GBIC") transceiver, mainly with [SC](https://en.wikipedia.org/wiki/Optical_fiber_connector "Optical fiber connector") (Subscriber Connector) fiber connector.

## Storage area networks

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Fibre_Channel_Storage_Area_Network.png/220px-Fibre_Channel_Storage_Area_Network.png)

The Fibre Channel SAN connects servers to storage via Fibre Channel switches.

The goal of Fibre Channel is to create a [storage area network](https://en.wikipedia.org/wiki/Storage_area_network "Storage area network") (SAN) to connect servers to storage.

The SAN is a dedicated network that enables multiple servers to access data from one or more storage devices. [Enterprise storage](https://en.wikipedia.org/wiki/Enterprise_storage "Enterprise storage") uses the SAN to backup to secondary storage devices including [disk arrays](https://en.wikipedia.org/wiki/Disk_arrays "Disk arrays"), [tape libraries](https://en.wikipedia.org/wiki/Tape_library "Tape library"), and other backup while the storage is still accessible to the server. Servers may access storage from multiple storage devices over the network as well.

SANs are often designed with dual fabrics to increase fault tolerance. Two completely separate fabrics are operational and if the primary fabric fails, then the second fabric becomes the primary.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d8/Fibre_Channel_Director.jpg/200px-Fibre_Channel_Director.jpg)

Fibre Channel director with SFP+ modules and LC [optical fiber connectors](https://en.wikipedia.org/wiki/Optical_fiber_connector "Optical fiber connector") with Optical Multimode 3 (OM3) fiber (aqua)

Fibre Channel switches can be divided into two classes. These classes are not part of the standard, and the classification of every switch is a marketing decision of the manufacturer:

- **Directors** offer a high port-count in a modular (slot-based) chassis with no single point of failure (high availability).
- **Switches** are typically smaller, fixed-configuration (sometimes semi-modular), less redundant devices.

A fabric consisting entirely of one vendors products is considered to be *homogeneous*. This is often referred to as operating in its "native mode" and allows the vendor to add proprietary features which may not be compliant with the Fibre Channel standard.

If multiple switch vendors are used within the same fabric it is *heterogeneous*, the switches may only achieve adjacency if all switches are placed into their interoperability modes. This is called the "open fabric" mode as each vendor's switch may have to disable its proprietary features to comply with the Fibre Channel standard.

Some switch manufacturers offer a variety of interoperability modes above and beyond the "native" and "open fabric" states. These "native interoperability" modes allow switches to operate in the native mode of another vendor and still maintain some of the proprietary behaviors of both. However, running in native interoperability mode may still disable some proprietary features and can produce fabrics of questionable stability.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/QLogic_QLE2562_8Gb_FC_HBA.jpg/200px-QLogic_QLE2562_8Gb_FC_HBA.jpg)

Dual port 8 Gb FC host bus adapter card

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Qlogic_qle2672-ck.jpg/200px-Qlogic_qle2672-ck.jpg)

Dual port 16 Gb FC host bus adapter card

Fibre Channel [HBAs](https://en.wikipedia.org/wiki/Host_adapter "Host adapter"), as well as [CNAs](https://en.wikipedia.org/wiki/Converged_network_adapter "Converged network adapter"), are available for all major [open systems](https://en.wikipedia.org/wiki/Open_system_\(computing\) "Open system (computing)"), computer architectures, and buses, including [PCI](https://en.wikipedia.org/wiki/Peripheral_Component_Interconnect "Peripheral Component Interconnect") and [SBus](https://en.wikipedia.org/wiki/SBus "SBus"). HBAs connect servers to the Fibre Channel network and are part of a class of devices known as translation devices. Some are OS dependent. Each HBA has a unique [World Wide Name](https://en.wikipedia.org/wiki/World_Wide_Name "World Wide Name") (WWN), which is similar to an Ethernet [MAC address](https://en.wikipedia.org/wiki/MAC_address "MAC address") in that it uses an [Organizationally Unique Identifier](https://en.wikipedia.org/wiki/Organizationally_Unique_Identifier "Organizationally Unique Identifier") (OUI) assigned by the [IEEE](https://en.wikipedia.org/wiki/IEEE "IEEE"). However, WWNs are longer (8 [bytes](https://en.wikipedia.org/wiki/Byte "Byte")). There are two types of WWNs on an HBA; a [World Wide Node Name](https://en.wikipedia.org/wiki/World_Wide_Node_Name "World Wide Node Name") (WWNN), which can be shared by some or all ports of a device, and a [World Wide Port Name](https://en.wikipedia.org/wiki/World_Wide_Port_Name "World Wide Port Name") (WWPN), which is necessarily unique to each port. Adapters or routers can connect Fibre Channel networks to IP or Ethernet networks.[^38]

- [8b/10b encoding](https://en.wikipedia.org/wiki/8b/10b_encoding "8b/10b encoding"), [64b/66b encoding](https://en.wikipedia.org/wiki/64b/66b_encoding "64b/66b encoding")
- [Fabric Application Interface Standard](https://en.wikipedia.org/wiki/Fabric_Application_Interface_Standard "Fabric Application Interface Standard")
- [Fibre Channel zoning](https://en.wikipedia.org/wiki/Fibre_Channel_zoning "Fibre Channel zoning")
- [Registered State Change Notification](https://en.wikipedia.org/wiki/Registered_State_Change_Notification "Registered State Change Notification")
- [Virtual Storage Area Network](https://en.wikipedia.org/wiki/Vsan "Vsan")
- [Fibre Channel frame](https://en.wikipedia.org/wiki/Fibre_Channel_frame "Fibre Channel frame")
- [Fibre Channel network protocols](https://en.wikipedia.org/wiki/Fibre_Channel_network_protocols "Fibre Channel network protocols")
- [Fibre Channel over Ethernet](https://en.wikipedia.org/wiki/FCoE "FCoE") (FCoE)
- [Fibre Channel over IP](https://en.wikipedia.org/wiki/Fibre_Channel_over_IP "Fibre Channel over IP") (FCIP), contrast with [Internet Fibre Channel Protocol](https://en.wikipedia.org/wiki/Internet_Fibre_Channel_Protocol "Internet Fibre Channel Protocol") (iFCP)
- [Gen 5 Fibre Channel](https://en.wikipedia.org/wiki/Gen_5_Fibre_Channel "Gen 5 Fibre Channel")
- [Host Bus Adapter](https://en.wikipedia.org/wiki/Host_Bus_Adapter "Host Bus Adapter") (HBA)
- [Interconnect bottleneck](https://en.wikipedia.org/wiki/Interconnect_bottleneck "Interconnect bottleneck")
- [FATA](https://en.wikipedia.org/wiki/FATA_\(hard_drive\) "FATA (hard drive)"), [IDE](https://en.wikipedia.org/wiki/Integrated_Drive_Electronics "Integrated Drive Electronics"), [ATA](https://en.wikipedia.org/wiki/Advanced_Technology_Attachment "Advanced Technology Attachment"), [SATA](https://en.wikipedia.org/wiki/SATA "SATA"), [SAS](https://en.wikipedia.org/wiki/Serial_Attached_SCSI "Serial Attached SCSI"), [AoE](https://en.wikipedia.org/wiki/ATA_over_Ethernet "ATA over Ethernet"), [SCSI](https://en.wikipedia.org/wiki/SCSI "SCSI"), [iSCSI](https://en.wikipedia.org/wiki/ISCSI "ISCSI"), [PCI Express](https://en.wikipedia.org/wiki/PCI_Express "PCI Express")
- [IP over Fibre Channel](https://en.wikipedia.org/wiki/IPFC "IPFC") (IPFC)
- [N\_Port ID Virtualization](https://en.wikipedia.org/wiki/NPIV "NPIV")
- [World Wide Name](https://en.wikipedia.org/wiki/World_Wide_Name "World Wide Name")

[^fibrechannel.org-1]: ["Fibre Channel Performance: Congestion, Slow Drain, and Over Utilization, Oh My!"](http://fibrechannel.org/wp-content/uploads/2018/02/FCIA_Fibre_Channel_Performance_Congestion_Slowdrain_and_Over_Utilization_Final.pdf) (PDF). Fibre Channel Industry Association. February 6, 2018. [Archived](https://web.archive.org/web/20180301164420/http://fibrechannel.org/wp-content/uploads/2018/02/FCIA_Fibre_Channel_Performance_Congestion_Slowdrain_and_Over_Utilization_Final.pdf) (PDF) from the original on 2018-03-01. Retrieved 2018-02-28.

[^2]: ["Fibre Channel Basics"](https://images.apple.com/server/docs/Fibre_Channel_Basics_TB_v10.4.pdf) (PDF). Apple. [Archived](https://web.archive.org/web/20170829075557/http://images.apple.com/server/docs/Fibre_Channel_Basics_TB_v10.4.pdf) (PDF) from the original on 2017-08-29. Retrieved 2018-03-22.

[^preston-3]: Preston, W. Curtis (2002). ["Fibre Channel Architecture"](https://books.google.com/books?id=JUodwAQdMGcC&pg=PA19). *Using SANs and NAS*. Sebastopol, CA: [O'Reilly Media](https://en.wikipedia.org/wiki/O%27Reilly_Media "O'Reilly Media"). pp. 19–39\. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-0-596-00153-7](https://en.wikipedia.org/wiki/Special:BookSources/978-0-596-00153-7 "Special:BookSources/978-0-596-00153-7"). [OCLC](https://en.wikipedia.org/wiki/OCLC_\(identifier\) "OCLC (identifier)") [472853124](https://search.worldcat.org/oclc/472853124).

[^riabov-4]: Riabov, Vladmir V. (2004). ["Storage Area Networks (SANs)"](https://books.google.com/books?id=5W3f6IyIBQcC&pg=PA329). In Bidgoli, Hossein (ed.). *The Internet Encyclopedia. Volume 3, P-Z*. Hoboken, NJ: [John Wiley & Sons](https://en.wikipedia.org/wiki/John_Wiley_%26_Sons "John Wiley & Sons"). pp. 329–338\. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-0-471-68997-3](https://en.wikipedia.org/wiki/Special:BookSources/978-0-471-68997-3 "Special:BookSources/978-0-471-68997-3"). [OCLC](https://en.wikipedia.org/wiki/OCLC_\(identifier\) "OCLC (identifier)") [55610291](https://search.worldcat.org/oclc/55610291).

[^tate-5]: "Fibre Channel internals". *Introduction to Storage Area Networks*. [IBM](https://en.wikipedia.org/wiki/IBM "IBM"). 2016. p. 33.

[^zg940168-6]: [IBM 7319 Model 100 Fibre Channel Switch 16/266 and IBM Fibre Channel Adapter/266](https://www-01.ibm.com/common/ssi/rep_ca/8/877/ENUSZG94-0168/index.html)

[^7]: Fibre Channel Physical and Signaling Interface (FC-PH) Rev 4.3, June 1, 1994

[^8]: [Tom Clark, Designing Storage Area Networks: A Practical Reference for Implementing Fibre Channel and IP SANs](https://www.pearsonhighered.com/assets/samplechapter/0/3/2/1/0321136500.pdf)

[^9]: ["Roadmaps"](https://fibrechannel.org/roadmap/). Fibre Channel Industry Association. Retrieved 2023-03-05.

[^fibre_channel_speedmap-10]: [Fibre Channel Speedmap](https://fibrechannel.org/roadmap/)

[^g620release-11]: Brocade 32Gb platform released, Storagereview.com ["Brocade G620 Gen 6 Fibre Channel Switch Released"](http://www.storagereview.com/brocade_g620_gen_6_fibre_channel_switch_released). March 2016. [Archived](https://web.archive.org/web/20160404014046/http://www.storagereview.com/brocade_g620_gen_6_fibre_channel_switch_released) from the original on 2016-04-04. Retrieved 2016-04-04.

[^12]: [128GFC: A Preview of the New Fibre Channel Speed](https://fibrechannel.org/wp-content/uploads/2023/06/FCIA-128GFC-Webcast-Final-v1.pdf)

[^fc-fs-4-13]: [Fibre Channel - Framing and Signaling - 4 (FC-FS-4)](https://webstore.ansi.org/standards/incits/incits4882016)

[^fc-sw-6-14]: Fibre Channel - Switch Fabric 6 (FC-SW-6)

[^bcfa_nutshell-15]: ["BCFA in a Nutshell Study Guide for Exam"](https://www.brocade.com/content/dam/common/documents/content-types/education-study-tools/brocade-bcfa-nutshell-certification-study-tools.pdf) (PDF). Brocade Communications, Inc. February 2014. [Archived](https://web.archive.org/web/20150907185312/http://www.brocade.com/content/dam/common/documents/content-types/education-study-tools/brocade-bcfa-nutshell-certification-study-tools.pdf) (PDF) from the original on September 7, 2015. Retrieved June 28, 2016.

[^16]: ["Cisco MDS 9000 Family Fabric Manager Configuration Guide, Release 4.x"](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/mds9000/sw/4_1/configuration/guides/fm_4_1/fmguide.html). Cisco Systems, Inc. November 11, 2013. [Archived](https://web.archive.org/web/20160821064642/https://www.cisco.com/c/en/us/td/docs/switches/datacenter/mds9000/sw/4_1/configuration/guides/fm_4_1/fmguide.html) from the original on August 21, 2016. Retrieved June 28, 2016.

[^17]: Transmitter values listed are the currently specified values for the variant listed. Some older versions of the FC standards listed slightly different values (however, the values listed here fall within the +/− variance allowed). Individual variations for each specification are listed in the references associated with those entries in this table. FC-PH = X3T11 Project 755D; FC-PH-2 = X3T11 Project 901D; FC-PI-4 = INCITS Project 1647-D; FC-PI-5 = INCITS Project 2118D. Copies are available from [INCITS](http://www.incits.org/) [Archived](https://web.archive.org/web/20100915022630/http://www.incits.org/) 2010-09-15 at the [Wayback Machine](https://en.wikipedia.org/wiki/Wayback_Machine "Wayback Machine").

[^38]: ["Hardware"](https://fibrechannel.org/hardware/). 25 September 2012.

[^fc-pi-5_clause_6.3-18]: FC-PI-5 Clause 6.3

[^fc-pi-5_clause_8.1-19]: FC-PI-5 Clause 8.1

[^fc-pi-4_clause_6.3-20]: FC-PI-4 Clause 6.3

[^fc-pi-4_clause_8.1-21]: FC-PI-4 Clause 8.1

[^fc-ph-2_lists_1300nm_(see_clause_6.1_and_8.1)-22]: FC-PH-2 lists 1300nm (see clause 6.1 and 8.1)

[^fc-pi_clause_8.1-23]: FC-PI clause 8.1

[^fc-ph-2_clause_8.1-24]: FC-PH-2 clause 8.1

[^fc-pi-4_clause_11-25]: FC-PI-4 Clause 11

[^26]: FC-PH lists 1300nm (see clause 6.1 and 8.1)

[^fc-ph_clause_8.1-27]: FC-PH Clause 8.1

[^28]: FC-PI-5 Clause 6.4

[^29]: FC-PI-4 Clause 6.4

[^30]: The older FC-PH and FC-PH-2 list 850nm (for 62.5μm cables) and 780nm (for 50μm cables)(see clause 6.2, 8.2, and 8.3)

[^fc-pi-5_clause_8.2-31]: FC-PI-5 Clause 8.2

[^32]: FC-PI-5 Annex A

[^fc-pi-4_clause_8.2-33]: FC-PI-4 Clause 8.2

[^fc-pi_clause_8.2-34]: FC-PI Clause 8.2

[^35]: PC-PI-4 Clause 8.2

[^pc-pi_clause_8.2-36]: PC-PI Clause 8.2

[^37]: FC-PH Annex C and Annex E

- Clark, T. *Designing Storage Area Networks*, Addison-Wesley, 1999. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [0-201-61584-3](https://en.wikipedia.org/wiki/Special:BookSources/0-201-61584-3 "Special:BookSources/0-201-61584-3")

- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [2625](https://datatracker.ietf.org/doc/html/rfc2625) – IP and ARP over Fibre Channel
- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [2837](https://datatracker.ietf.org/doc/html/rfc2837) – Definitions of Managed Objects for the Fabric Element in Fibre Channel Standard
- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [3723](https://datatracker.ietf.org/doc/html/rfc3723) – Securing Block Storage Protocols over IP
- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [4044](https://datatracker.ietf.org/doc/html/rfc4044) – Fibre Channel Management [MIB](https://en.wikipedia.org/wiki/Management_information_base "Management information base")
- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [4625](https://datatracker.ietf.org/doc/html/rfc4625) – Fibre Channel Routing Information MIB
- [RFC](https://en.wikipedia.org/wiki/RFC_\(identifier\) "RFC (identifier)") [4626](https://datatracker.ietf.org/doc/html/rfc4626) – MIB for Fibre Channel's Fabric Shortest Path First (FSPF) Protocol

- [Fibre Channel Industry Association](http://www.fibrechannel.org/) (FCIA)
- [INCITS technical committee responsible for FC standards(T11)](http://www.t11.org/index.html)
- [IBM SAN Survival Guide](http://www.redbooks.ibm.com/redbooks.nsf/0/f98c75e7c6b5a4ca88256d0c0060bcc0?OpenDocument)
- [Introduction to Storage Area Networks](http://www.redbooks.ibm.com/abstracts/sg245470.html?Open)
- [Fibre Channel overview](http://hsi.web.cern.ch/HSI/fcs/spec/overview.htm)
- [Fibre Channel tutorial](http://www.iol.unh.edu/training/fc/tutorials/fc_tutorial.php) (UNH-IOL)
- [Storage Networking Industry Association](http://www.snia.org/) (SNIA)
- [Virtual fibre Channel in Hyper V](http://thetechnologychronicle.blogspot.in/2013/12/virtual-fibre-channel-in-hyper-v.html)