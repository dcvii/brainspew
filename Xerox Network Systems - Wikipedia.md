---
title: "Xerox Network Systems - Wikipedia"
source: "https://en.wikipedia.org/wiki/Xerox_Network_Systems"
author:
  - "[[Contributors to Wikimedia projects]]"
published: 2002-03-13
created: 2025-02-21
description:
tags:
  - "Xerox"
---
Suite of computer network protocols developed by Xerox

<table><caption>XNS</caption><tbody><tr><td colspan="2"><a href="https://en.wikipedia.org/wiki/Protocol_stack">Protocol stack</a></td></tr><tr><th scope="row">Purpose</th><td><a href="https://en.wikipedia.org/wiki/LAN">LAN</a></td></tr><tr><th scope="row">Developer(s)</th><td><a href="https://en.wikipedia.org/wiki/Xerox">Xerox</a></td></tr><tr><th scope="row">Introduction</th><td>1977<span>; 48&nbsp;years ago</span><span>&nbsp;(<span>1977</span>)</span></td></tr><tr><th scope="row">Influenced</th><td><a href="https://en.wikipedia.org/wiki/3%2BShare">3+Share</a>, Net/One, <a href="https://en.wikipedia.org/wiki/IPX/SPX">IPX/SPX</a>, <a href="https://en.wikipedia.org/wiki/Banyan_VINES">VINES</a></td></tr><tr><th scope="row">Hardware</th><td><a href="https://en.wikipedia.org/wiki/Ethernet">Ethernet</a></td></tr></tbody></table>

**Xerox Network Systems** (**XNS**) is a [computer networking](https://en.wikipedia.org/wiki/Computer_network "Computer network") [protocol suite](https://en.wikipedia.org/wiki/Protocol_suite "Protocol suite") developed by [Xerox](https://en.wikipedia.org/wiki/Xerox "Xerox") within the **Xerox Network Systems Architecture**. It provided general purpose network communications, internetwork [routing](https://en.wikipedia.org/wiki/Routing "Routing") and packet delivery, and higher level functions such as a [reliable stream](https://en.wikipedia.org/wiki/Reliable_stream "Reliable stream"), and [remote procedure calls](https://en.wikipedia.org/wiki/Remote_procedure_call "Remote procedure call"). XNS predated and influenced the development of the [Open Systems Interconnection](https://en.wikipedia.org/wiki/Open_Systems_Interconnection "Open Systems Interconnection") (OSI) networking model, and was very influential in [local area networking](https://en.wikipedia.org/wiki/Local_area_networking "Local area networking") designs during the 1980s.

XNS was developed by the Xerox Systems Development Department in the early 1980s, who were charged with bringing [Xerox PARC](https://en.wikipedia.org/wiki/Xerox_PARC "Xerox PARC")'s research to market. XNS was based on the earlier (and equally influential) [PARC Universal Packet](https://en.wikipedia.org/wiki/PARC_Universal_Packet "PARC Universal Packet") (PUP) suite from the late 1970s. Some of the protocols in the XNS suite were lightly modified versions of the ones in the Pup suite. XNS added the concept of a network number, allowing larger networks to be constructed from multiple smaller ones, with routers controlling the flow of information between the networks.

The protocol suite specifications for XNS were placed in the [public domain](https://en.wikipedia.org/wiki/Public_domain "Public domain") in 1977. This helped XNS become the canonical [local area networking](https://en.wikipedia.org/wiki/Local_area_network "Local area network") protocol, copied to various degrees by practically all networking systems in use into the 1990s. XNS was used unchanged by [3Com](https://en.wikipedia.org/wiki/3Com "3Com")'s [3+Share](https://en.wikipedia.org/wiki/3%2BShare "3+Share") and [Ungermann-Bass](https://en.wikipedia.org/wiki/Ungermann-Bass "Ungermann-Bass")'s Net/One. It was also used, with modifications, as the basis for [Novell NetWare](https://en.wikipedia.org/wiki/Novell_NetWare "Novell NetWare"), and [Banyan VINES](https://en.wikipedia.org/wiki/Banyan_VINES "Banyan VINES"). XNS was used as the basis for the [AppleNet](https://en.wikipedia.org/wiki/AppleNet "AppleNet") system, but this was never commercialized; a number of XNS's solutions to common problems were used in AppleNet's replacement, [AppleTalk](https://en.wikipedia.org/wiki/AppleTalk "AppleTalk").

In comparison to the [OSI model](https://en.wikipedia.org/wiki/OSI_model "OSI model")'s 7 layers, XNS is a five-layer system,[^footnotestephens198915-1] like the later [Internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite "Internet protocol suite").

The Physical and Data Link layers of the OSI model correspond to the Physical layer (layer 0) in XNS, which was designed to use the transport mechanism of the underlying hardware and did not separate the data link. Specifically, XNS's Physical layer is really the [Ethernet](https://en.wikipedia.org/wiki/Ethernet "Ethernet") [local area network](https://en.wikipedia.org/wiki/Local_area_network "Local area network") system, also being developed by Xerox at the same time, and a number of its design decisions reflect that fact.[^footnotestephens198915-1] The system was designed to allow Ethernet to be replaced by some other system, but that was not defined by the protocol (nor had to be).

The primary part of XNS is its definition of the Internal Transport layer (layer 1), which corresponds to OSI's Network layer, and it is here that the primary internetworking protocol, IDP, is defined. XNS combined the OSI's Session and Transport layers into the single Interprocess Communications layer (layer 2). Layer 3 was Resource Control, similar to the OSI's Presentation.[^footnotestephens198915-1][^footnotecisco-2]

Finally, on top of both models, is the Application layer, although these layers were not defined in the XNS standard.[^footnotestephens198915-1]

### Basic internetwork protocol

The main [internetwork](https://en.wikipedia.org/wiki/Internetwork "Internetwork") layer [protocol](https://en.wikipedia.org/wiki/Network_protocol "Network protocol") is the **Internet Datagram Protocol** (**IDP**). IDP is a close descendant of Pup's [internetwork protocol](https://en.wikipedia.org/wiki/PARC_Universal_Packet#Basic_internetwork_protocol "PARC Universal Packet"), and roughly corresponds to the [Internet Protocol](https://en.wikipedia.org/wiki/Internet_Protocol "Internet Protocol") (IP) layer in the Internet protocol suite.[^footnotestephens198915-1]

IDP uses Ethernet's 48-bit address as the basis for its own [network addressing](https://en.wikipedia.org/wiki/Network_address "Network address"), generally using the machine's [MAC address](https://en.wikipedia.org/wiki/MAC_address "MAC address") as the primary unique identifier. To this is added another 48-bit address section provided by the networking equipment; 32 bits are provided by [routers](https://en.wikipedia.org/wiki/Router_\(computing\) "Router (computing)") to identify the network number in the internetwork, and another 16 bits define a socket number for service selection within a single host. The network number portion of the address also includes a special value which meant "this network", for use by hosts which did not (yet) know their network number.[^footnotecisco-2]

Unlike TCP/IP, socket numbers are part of the full network address in the IDP header, so that upper-layer protocols do not need to implement demultiplexing; IDP also supplies packet types (again, unlike IP). IDP also contains a checksum covering the entire packet, but it is optional, not mandatory. This reflects the fact that LANs generally have low-error rates, so XNS removed error correction from the lower-level protocols in order to improve performance. Error correction could be optionally added at higher levels in the protocol stack, for instance, in XNS's own SPP protocol. XNS was widely regarded as faster than IP due to this design note.[^footnotestephens198915-1]

In keeping with the low-latency LAN connections it runs on, XNS uses a short packet size, which improves performance in the case of low error rates and short turnaround times. IDP packets are up to 576 bytes long, including the 30 byte IDP [header](https://en.wikipedia.org/wiki/Header_\(computing\) "Header (computing)").[^footnotecisco-2] In comparison, IP requires all hosts to support at *least* 576, but supports packets of up to 65K bytes. Individual XNS host pairs on a particular network might use larger packets, but no XNS router is required to handle them, and no mechanism is defined to discover if the intervening routers support larger packets. Also, packets can not be fragmented, as they can in IP.

The [Routing Information Protocol](https://en.wikipedia.org/wiki/Routing_Information_Protocol "Routing Information Protocol") (RIP), a descendant of Pup's *Gateway Information Protocol*, is used as the router information-exchange system, and (slightly modified to match the syntax of addresses of other protocol suites), remains in use today in other protocol suites, such as the Internet protocol suite.[^footnotecisco-2]

XNS also implements a simple echo protocol at the internetwork layer, similar to IP's [ping](https://en.wikipedia.org/wiki/Ping_\(networking_utility\) "Ping (networking utility)"), but operating at a lower level in the networking stack. Instead of adding the ICMP data as payload in an IP packet, as in ping, XNS's echo placed the command directly within the underlying IDP packet.[^footnotecisco-2] The same might be achieved in IP by expanding the ICMP [Protocol](https://en.wikipedia.org/wiki/IPv4#Protocol "IPv4") field of the IP header.

### Transport layer protocols

There are two primary transport layer protocols, both very different from their Pup predecessor:

- **Sequenced Packet Protocol** (**SPP**) is an acknowledgment transport protocol, with a 3-way handshake analogous to [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol "Transmission Control Protocol"); one chief technical difference is that the sequence numbers count packets, and not the bytes as in TCP and PUP's BSP; it is the direct antecedent to [Novell's](https://en.wikipedia.org/wiki/Novell_NetWare "Novell NetWare") [IPX/SPX](https://en.wikipedia.org/wiki/IPX/SPX "IPX/SPX").
- **Packet Exchange Protocol** (**PEP**) is a connectionless non-reliable protocol similar in nature to [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol "User Datagram Protocol") and the antecedent to [Novell's](https://en.wikipedia.org/wiki/Novell_NetWare "Novell NetWare") PXP.

XNS, like Pup, also uses **EP**, the *Error Protocol*, as a reporting system for problems such as dropped packets. This provided a unique set of packets which can be filtered to look for problems.[^footnotecisco-2]

### Application protocols

In the original Xerox concept, application protocols such as remote printing, filing, and mailing, etc., employed a [remote procedure call](https://en.wikipedia.org/wiki/Remote_procedure_call "Remote procedure call") protocol named **Courier**. Courier contained primitives to implement most of the features of Xerox's [Mesa programming language](https://en.wikipedia.org/wiki/Mesa_\(programming_language\) "Mesa (programming language)") function calls. Applications had to manually serialize and de-serialize function calls in Courier; there was no automatic facility to translate a function activation frame into an RPC (i.e. no "RPC compiler" was available). Because Courier was used by all applications, the XNS application protocol documents specified only courier function-call interfaces, and module+function binding tuples. There was a special facility in Courier to allow a function call to send or receive bulk data.[^footnotecisco-2]

Initially, XNS service location was performed via broadcasting remote procedure-calls using a series of expanding ring broadcasts (in consultation with the local router, to get networks at increasing distances.) Later, the Clearinghouse Protocol 3-level directory service was created to perform service location, and the expanding-ring broadcasts were used only to locate an initial Clearinghouse.[^footnotecisco-2]

Due to its tight integration with Mesa as an underlying technology, many of the traditional higher-level protocols were not part of the XNS system itself. This meant that vendors using the XNS protocols all created their own solutions for [file sharing](https://en.wikipedia.org/wiki/File_sharing "File sharing") and [printer](https://en.wikipedia.org/wiki/Printer_\(computing\) "Printer (computing)") support. While many of these 3rd party products theoretically could talk to each other at a packet level, there was little or no capability to call each other's application services. This led to complete fragmentation of the XNS market, and has been cited as one of the reasons that IP easily displaced it.[^footnotestephens198915-1]

The XNS protocols also included an Authentication Protocol and an Authentication Service to support it. Its "Strong credentials" were based on the same [Needham–Schroeder protocol](https://en.wikipedia.org/wiki/Needham%E2%80%93Schroeder_protocol "Needham–Schroeder protocol") that was later used by [Kerberos](https://en.wikipedia.org/wiki/Kerberos_\(protocol\) "Kerberos (protocol)"). After contacting the authentication service for credentials, this protocol provided a lightweight way to digitally sign Courier procedure calls, so that receivers could verify the signature and authenticate senders over the XNS internet, without having to contact the Authentication service again for the length of the protocol communication session.[^xsis098404-3]

Xerox's printing language, [Interpress](https://en.wikipedia.org/wiki/Interpress "Interpress"), was a binary-formatted standard for controlling laser printers. The designers of this language, John Warnock and Chuck Geschke, later left Xerox PARC to start [Adobe Systems](https://en.wikipedia.org/wiki/Adobe_Systems "Adobe Systems"). Before leaving, they realized the difficulty of specifying a binary print language, where functions to serialize the print job were cumbersome and which made it difficult to debug errant printing jobs. To realize the value of specifying both a programmable and easily debug-able print job in ASCII, Warnock and Geschke created the Postscript language as one of their first products at Adobe.

#### Remote Debug Protocols

Because all 8000+ machines in the Xerox corporate Intranet ran the Wildflower architecture (designed by Butler Lampson), there was a remote-debug protocol for microcode. Basically, a peek and poke function could halt and manipulate the microcode state of a C-series or D-series machine, anywhere on earth, and then restart the machine.

Also, there was a remote debug protocol for the world-swap debugger.[^4] This protocol could, via the debugger "nub", freeze a workstation and then peek and poke various parts of memory, change variables, and continue execution. If debugging symbols were available, a crashed machine could be remote debugged from anywhere on earth.

### Origins in Ethernet and PUP

In his final year at [Harvard University](https://en.wikipedia.org/wiki/Harvard_University "Harvard University"), [Bob Metcalfe](https://en.wikipedia.org/wiki/Robert_Metcalfe "Robert Metcalfe") began interviewing at a number of companies and was given a warm welcome by [Jerry Elkind](https://en.wikipedia.org/wiki/Jerome_I._Elkind "Jerome I. Elkind") and [Bob Taylor](https://en.wikipedia.org/wiki/Robert_Taylor_\(computer_scientist\) "Robert Taylor (computer scientist)") at [Xerox PARC](https://en.wikipedia.org/wiki/Xerox_PARC "Xerox PARC"), who were beginning to work on the networked computer workstations that would become the [Xerox Alto](https://en.wikipedia.org/wiki/Xerox_Alto "Xerox Alto"). He agreed to join PARC in July, after defending his thesis. In 1970, while [couch surfing](https://en.wikipedia.org/wiki/Couch_surfing "Couch surfing") at [Steve Crocker](https://en.wikipedia.org/wiki/Steve_Crocker "Steve Crocker")'s home while attending a conference, Metcalfe picked up a copy [Proceedings of the Fall Joint Computer Conference](https://en.wikipedia.org/wiki/Joint_Computer_Conference "Joint Computer Conference") off the table with the aim of falling asleep while reading it. Instead, he became fascinated by an article on [ALOHAnet](https://en.wikipedia.org/wiki/ALOHAnet "ALOHAnet"), an earlier wide-area networking system. By June he had developed his own theories on networking and presented them to his professors, who rejected it and he was "thrown out on my ass."[^footnotepelkey20076.7-5]

Metcalfe was welcomed at PARC in spite of his unsuccessful thesis, and soon started development of what was then referred to as "ALOHAnet in a wire". He teamed up with [David Boggs](https://en.wikipedia.org/wiki/David_Boggs "David Boggs") to help with the electronic implementation, and by the end of 1973 they were building working hardware at 3 Mbit/s. The pair then began working on a simple protocol that would run on the system. This led to the development of the [PARC Universal Packet](https://en.wikipedia.org/wiki/PARC_Universal_Packet "PARC Universal Packet") (Pup) system, and by late 1974 the two had Pup successfully running on Ethernet. They filed a patent on the concepts, with Metcalfe adding several other names because he believed they deserved mention, and then submitted a paper on the concept to [Communications of the ACM](https://en.wikipedia.org/wiki/Communications_of_the_ACM "Communications of the ACM") on "Ethernet: Distributed Packet Switching for Local Computer Networks", published in July 1976.[^footnotepelkey20076.7-5]

By 1975, long before PUP was complete, Metcalfe was already chafing under the stiff Xerox management. He believed the company should immediately put Ethernet into production, but found little interest among upper management. A seminal event took place when professors from [MIT](https://en.wikipedia.org/wiki/MIT "MIT")'s famed [Artificial Intelligence Laboratory](https://en.wikipedia.org/wiki/MIT_Computer_Science_and_Artificial_Intelligence_Laboratory "MIT Computer Science and Artificial Intelligence Laboratory") approached Xerox in 1974 with the intention of buying Ethernet for use in their lab. Xerox management declined, believing Ethernet was better used to help sell their own equipment. The AI Lab would then go on to make their own version of Ethernet, [Chaosnet](https://en.wikipedia.org/wiki/Chaosnet "Chaosnet").[^footnotepelkey20076.8-6]

Metcalfe eventually left Xerox November 1975 for Transaction Technology, a division of [Citibank](https://en.wikipedia.org/wiki/Citibank "Citibank") tasked with advanced product development. However, he was lured back to Xerox seven months later by [David Liddle](https://en.wikipedia.org/wiki/David_Liddle "David Liddle"), who had recently organized the Systems Development Division within Xerox specifically to bring PARCs concepts to market. Metcalfe immediately began re-designing Ethernet to work at 20 Mbit/s and started an effort to re-write Pup in a production quality version. Looking for help on Pup, Metcalfe approached [Yogen Dalal](https://en.wikipedia.org/wiki/Yogen_Dalal "Yogen Dalal"), who was at that time completing his PhD thesis under [Vint Cerf](https://en.wikipedia.org/wiki/Vint_Cerf "Vint Cerf") at [Stanford University](https://en.wikipedia.org/wiki/Stanford_University "Stanford University"). Dalal was also being heavily recruited by [Bob Kahn](https://en.wikipedia.org/wiki/Bob_Kahn "Bob Kahn")'s [ARPANET](https://en.wikipedia.org/wiki/ARPANET "ARPANET") team (working on TCP/IP), but when Cerf left to join [DARPA](https://en.wikipedia.org/wiki/DARPA "DARPA"), Dalal agreed to move to PARC and started there in 1977.[^footnotepelkey20076.9-7]

Dalal built a team including [William Crowther](https://en.wikipedia.org/wiki/William_Crowther_\(programmer\) "William Crowther (programmer)") and Hal Murray, and started with a complete review of Pup. Dalal also attempted to remain involved in the TCP efforts underway at DARPA, but eventually gave up and focussed fully on Pup. Dalal combined his experience with ARPANET with the concepts from Pup and by the end of 1977 they had published the first draft of the Xerox Network System specification. This was essentially a version of Pup with absolute 48-bit host IDs, and TCP's 3-Way handshake in the Sequenced Packet Protocol.[^footnotepelkey20076.10-8]

By early 1978 the new system was working, but management was still not making any move to commercialize it. As Metcalfe put it:

> When I came back to Xerox in 1976, we were about two and a half years from product shipment and in 1978 we were about two and a half years from product shipment.[^footnotepelkey20076.9-7]

When no further action was forthcoming, Metcalfe left the company at the end of 1978.[^footnotepelkey20076.9-7]

Last used by Xerox for communication with the [DocuTech](https://en.wikipedia.org/wiki/DocuTech "DocuTech") 135 Publishing System, XNS is no longer in use, due to the ubiquity of IP. However, it played an important role in the development of networking technology in the 1980s, by influencing software and hardware vendors to seriously consider the need for computing platforms to support more than one network protocol stack simultaneously.

A wide variety of proprietary networking systems were directly based on XNS or offered minor variations on the theme. Among these were Net/One, 3+,[^footnotestephens198915-1] [Banyan VINES](https://en.wikipedia.org/wiki/Banyan_VINES "Banyan VINES")[^9] and Novell's [IPX/SPX](https://en.wikipedia.org/wiki/IPX/SPX "IPX/SPX").[^10] These systems added their own concepts on top of the XNS addressing and routing system; VINES added a [directory service](https://en.wikipedia.org/wiki/Directory_service "Directory service") among other services, while [Novell NetWare](https://en.wikipedia.org/wiki/Novell_NetWare "Novell NetWare") added a number of user-facing services like printing and file sharing. [AppleTalk](https://en.wikipedia.org/wiki/AppleTalk "AppleTalk") used XNS-like routing, but had incompatible addresses using shorter numbers.

XNS also helped to validate the design of the [4.2BSD](https://en.wikipedia.org/wiki/BSD "BSD") network subsystem by providing a second protocol suite, one which was significantly different from the Internet protocols; by implementing both stacks in the same kernel, [Berkeley researchers](https://en.wikipedia.org/wiki/UC_Berkeley_College_of_Engineering#Research_units "UC Berkeley College of Engineering") demonstrated that the design was suitable for more than just IP.[^11] Additional BSD modifications were eventually necessary to support the full range of [Open Systems Interconnection](https://en.wikipedia.org/wiki/Open_Systems_Interconnection "Open Systems Interconnection") (OSI) protocols.

*Xerox Network Systems Architecture Introduction to Xerox Network Systems* (XNSG 058504) is "a general discussion meant for those who want to know how office people can become more effective and productive by using the Xerox Network Systems."[^litcat-12] 

The components of Xerox Network Systems Architecture are briefly described in *Xerox Network Systems Architecture General Information Manual* (XNSG 068504).[^xnsg068504-13]

A series of sixteen individual protocol descriptions are listed in the *Xerox Systems Institute Literature Catalog*.[^litcat-12] Possibly more recent versions of these standards are:

- *Authentication Protocol* (XSIS 098404)[^xsis098404-3]
- *Bulk Data Transfer (Appendix f to Courier)*, April 1984 (XNSS 038112/XSIS 038112)
- *Character Code Standard*, May 1986 (XNSS 058605)
- *Clearinghouse Protocol*, April 1984 (XNSS 078404/XSIS 078404)
- *Clearinghouse Entry Formats*, April 1984 (XNSS 168404/XSIS 168404)[^xnss168404-14]
- *Courier: The Remote Procedure Call Protocol*, December 1981 (XNSS 038112/XSIS 038112)[^snss038112-15]
- *The Ethernet. A Local Area Network: Data Link Layer and Physical Layer Specifications* (Blue Book, Version 2.0), November 1982 (XNSS 018211/XSIS 018211)[^16]
- *Filing Protocol*, May 1986 (XNSS 108605)[^xnss108605-17]
- *Font Interchange Standard*, December 1985 (XNSS 238512)[^xnss238512-18]
- *Internet Transport Protocols*, December 1981 (XNSS 028112/XSIS 028112)[^xnss028112-19]
- *Interpress Electronic Printing Standard, Version 3.0*, January 1986 (XNSS 048601)[^xnss048601-20]
- *Print Service Integration Standard*, June 1985 (XNSS 198506)
- *Printing Protocol*, April 1984 (XNSS 118404/XSIS 118404)
- *Raster Encoding Standard*, June 1985 (XNSS 178506)
- *Synchronous Point-to-Point Protocol*, December 1984 (XNSS 158412)
- *Time Protocol*, April 1984 (XNSS 088404/XSIS 088404)

- [Protocol Wars](https://en.wikipedia.org/wiki/Protocol_Wars "Protocol Wars")

- [Xerox Character Code Standard](https://en.wikipedia.org/wiki/Xerox_Character_Code_Standard "Xerox Character Code Standard")

Citations

[^footnotestephens198915-1]: [Stephens 1989](https://en.wikipedia.org/wiki/#CITEREFStephens1989), p. 15.

[^footnotecisco-2]: [cisco](https://en.wikipedia.org/wiki/#CITEREFcisco).

[^xsis098404-3]: Xerox Corporation (April 1984). [*Xerox System Integration Standard Authentication Protocol*](http://www.bitsavers.org/pdf/xerox/xns/standards/XSIS_098404_Authentication_Protocol_Apr1984.pdf) (PDF). Retrieved July 20, 2023.

[^4]: ["World-stop debuggers"](https://people.ece.ubc.ca/gillies/pages/note1.html). 1999-01-25. Retrieved 2013-07-05.

[^footnotepelkey20076.7-5]: [Pelkey 2007](https://en.wikipedia.org/wiki/#CITEREFPelkey2007), 6.7.

[^footnotepelkey20076.8-6]: [Pelkey 2007](https://en.wikipedia.org/wiki/#CITEREFPelkey2007), 6.8.

[^footnotepelkey20076.9-7]: [Pelkey 2007](https://en.wikipedia.org/wiki/#CITEREFPelkey2007), 6.9.

[^footnotepelkey20076.10-8]: [Pelkey 2007](https://en.wikipedia.org/wiki/#CITEREFPelkey2007), 6.10.

[^9]: [Banyan VINES](http://docwiki.cisco.com/wiki/Banyan_VINES), cisco

[^10]: [NetWare Protocols](http://www.cisco.com/cpress/cc/td/cpress/fund/ith2nd/it2431.htm), cisco

[^11]: Larus, James (1983). ["On the performance of Courier Remote Procedure Calls under 4.1c BSD"](http://www.eecs.berkeley.edu/Pubs/TechRpts/1983/CSD-83-123.pdf) (PDF). UC Berkeley ECE Department. Retrieved 2013-07-05.

[^litcat-12]: Xerox Corporation. [*Xerox Systems Institute Literature Catalog*](http://www.bitsavers.org/pdf/xerox/xns/XSI_Literature_Catalog.pdf) (PDF). Retrieved July 20, 2023.

[^xnsg068504-13]: Xerox Corporation (April 1985). [*Xerox Network Systems General Information Manual*](http://www.bitsavers.org/pdf/xerox/xns/XNSG_068504_Xerox_System_Network_Architecture_General_Information_Manual_Apr85.pdf) (PDF). Retrieved July 20, 2023.

[^xnss168404-14]: Xerox Corporation (April 1984). [*Clearinghouse Entry Formats*](http://www.bitsavers.org/pdf/xerox/xns/standards/XSIS_168404_Clearinghouse_Entry_Formats_Apr1984.pdf) (PDF). Retrieved July 20, 2023.

[^snss038112-15]: Xerox Corporation (December 1981). [*Courier: The Remote Procedure Call Protocol*](http://www.bitsavers.org/pdf/xerox/xns/standards/XSIS_038112_Courier_The_Remote_Procedure_Call_Pr). Retrieved July 20, 2023.

[^16]: Digital Equipment Corporation; Intel Corporation; Xerox Corporation (November 1982). [*The Ethernet A Local Area Network Data Link Layer and Physical Layer Specifications*](http://bitsavers.org/pdf/xerox/ethernet/Ethernet_Rev2.0_Nov1982.pdf) (PDF). Retrieved July 20, 2023.

[^xnss108605-17]: Xerox Corporation (May 1986). [*Filing Protocol*](http://www.bitsavers.org/pdf/xerox/xns/standards/SNSS_108605_Filing_Protocol_May1986.pdf) (PDF). Retrieved July 20, 2023.

[^xnss238512-18]: Xerox Corporation (December 1985). [*Font Interchange Standard*](http://www.bitsavers.org/pdf/xerox/xns/standards/XNSS_238512_Font_Interchange_Standard_Ver_1.0_Dec1985.pdf) (PDF). Retrieved July 20, 2023.

[^xnss028112-19]: Xerox Corporation (December 1981). [*Internet Transport Protocols*](http://www.bitsavers.org/pdf/xerox/xns/standards/XSIS_028112-Internet_Transport_Protocols_198112.pdf) (PDF). Retrieved July 20, 2023.

[^xnss048601-20]: Xerox Corporation (January 1986). [*lnterpress Electronic Printing Standard*](http://bitsavers.org/pdf/xerox/interpress/610P72582A_XNSS_048601_Interpress_Electronic_Printing_Standard_198601.pdf) (PDF). Retrieved July 20, 2023.

Bibliography

- Stephens, Mark (6 March 1989). ["OSI Layer 3 Differentiates System Software"](https://books.google.com/books?id=GzoEAAAAMBAJ&pg=PT15). *InfoWorld*: 15.
- cisco. ["Xerox Network Systems"](http://docwiki.cisco.com/wiki/Xerox_Network_Systems). *cisco.com*.
- Pelkey, James (2007). ["Entrepreneurial Capitalism and Innovation: A History of Computer Communications 1968-1988"](http://www.historyofcomputercommunications.info/).
- Oppen, D.C., and Dalal, Y.K., The Clearinghouse: A Decentralized Agent for Locating Named Objects in a Distributed Environment. Palo Alto: Xerox Corporation, Office Systems Division, 1981 October: Tech Report OSD-T8103.
- Israel, J.E, and Linden, T.A, Authentication in Xerox's Star and Network Systems. Palo Alto: Xerox Corporation, Office Systems Division, 1982 May: Tech Report OSD-T8201.
- *Office Systems Technology - a look into the world of the Xerox 8000 Series Products: Workstations, Services, Ethernet, and Software Development", (Edited by Ted Linden and Eric Harslem), Tech Report Xerox OSD-R8203, November 1982. A compendium of 24 papers describing all aspects of the Xerox STAR Workstation and Networking Protocols, most of them were reprints of journal and conference publications.*

- [Xerox Network Systems Architecture: Introduction to Xerox Network Systems](http://bitsavers.trailing-edge.com/pdf/xerox/xns/XNSG058504_XNS_Introduction.pdf)
- [Xerox Network Systems Architecture: General Information Manual](http://bitsavers.trailing-edge.com/pdf/xerox/xns/XNSG_068504_Xerox_System_Network_Architecture_General_Information_Manual_Apr85.pdf)
- [Example of an actual implementation in kernel space](http://fxr.watson.org/fxr/source/netns/?v=NETBSD3)