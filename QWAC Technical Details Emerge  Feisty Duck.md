---
title: QWAC Technical Details Emerge | Feisty Duck
source: https://www.feistyduck.com/newsletter/issue_122_qwac_technical_details_emerge
author: 
published: 
created: 2025-02-28
description: 
tags:
  - secpar
---
### [Cryptography & Security Newsletter](https://www.feistyduck.com/bulletproof-tls-newsletter/)

> Feisty Duck’s Cryptography & Security Newsletter is a periodic dispatch bringing you commentary and news surrounding cryptography, security, privacy, SSL/TLS, and PKI. It's designed to keep you informed about the latest developments in this space. Enjoyed every month by more than 50,000 subscribers. **Written by [Ivan Ristić](https://blog.ivanristic.com/).**

Remember the European Union’s qualified website authentication certificates (QWACs)? Back in 2022 and 2023, browsers and the EU got into a fight over who controls website authentication; we [covered the topic extensively](https://www.feistyduck.com/newsletter/issue_107_european_union_presses_ahead_with_article_45). A document released recently ([ETSI TS 119 411-5 V2.1.1](https://www.etsi.org/deliver/etsi_ts/119400_119499/11941105/02.01.01_60/ts_11941105v020101p.pdf)) gives some information about how QWACs might be implemented by browsers.

There are two options for the integration, called *one quack* and *two quacks* (or 1-QWACs and 2-QWACs, if you prefer their actual names). The first option is essentially extending the existing TLS certificates with additional information needed, as per the QWAC requirements. With this approach, QWACs are TLS certificates and therefore they would also be compliant with the existing standards, such as CA/Browser Forum’s [Baseline Requirements](https://cabforum.org/working-groups/server/baseline-requirements/documents/). They would also have to comply with any additional requirements imposed by root programs, just like everyone else.

And then there is the second option (2-QWACs), which is much more involved. This approach keeps the TLS and QWAC ecosystems separate. For this reason, complying would require two certificates—one standard TLS, one QWAC—with a cryptographic binding to connect them. The information about the binding has to be delivered via an HTTP Link header, but the binding itself is a JSON file that’s signed using the private key for which the QWAC certificate is issued. One binding can endorse multiple TLS certificates, which is good news for those who wish to support multiple certificates at the same time.

#### Subscribe to the Cryptography & Security Newsletter

This subscription is just for the newsletter; we won't send you anything else.

### One or Two QWACs?

Whereas the first approach is straightforward and easy, the second is anything but. For browsers, it’s much more work, as they need to handle a new HTTP header, add code to fetch the binding, and implement a new signature (using JSON Advanced Electronic Signatures \[JAdES\]) and binding verification. For website operators, it’s also much more work, as they need to get multiple certificates, create and configure bindings, and make sure their HTTP caching is correctly configured so as not to advertise the bindings past the certificate expiration dates. It’s also a problem for third parties who are providing hosting services, which would need to augment their certificate issuance pipelines to add support for all of the above. In time, ACME clients will need to be extended to generate the bindings after each certificate change.

### Why Two Approaches?

It’s really not clear why ETSI is proposing two approaches. There is no explanation in the document; there’s only a recommendation in one of the appendixes that browsers implement both options. But that’s a very slippery slope, as we may end up with some browsers implementing one approach and some the other, leading to a situation in which site operators have to support both options if they want their QWAC status to be recognized.

### Do We Want More Public CAs?

From a purely technical perspective, the first option—in which QWAC essentially extends TLS certificates—is an easy choice, with most of the world continuing about its business without having to do anything.

However, if we consider why the second option might have been introduced, we may realize that the organizations authorized to issue QWACs are not the same as the CAs currently recognized by major root stores. Therein lies the problem. For option 1 to work, all these organizations (called *qualified trust service providers* \[QTSPs\]) must become public CAs. I suspect that many of them are not keen, and the root stores are even less so.

The second approach keeps the two sides separate and makes it easier for browsers to comply with less politics, but there’s a lot of pain attached to the compromise that anyone wanting or needing to support QWACs will have to endure.

## No Advanced Data Protection for the UK

You may have heard by now that Apple decided to [pull the plug](https://support.apple.com/en-us/122234) on its Advanced Data Protection (ADP) program in the UK. Why? Well, the company hasn’t said, which seems unusual for such a big decision. It did say something else: “We \[Apple\] have never built a backdoor or master key to any of our products or services and we never will.”

There is a reason for this coy language. On February 7, [the *Washington Post* reported](https://archive.is/jjeiC) that Apple had been ordered by the UK government to create a backdoor that would give access to the ADP data of any Apple user globally. Can the UK do this? Yes, thanks to the Investigatory Powers Act of 2016. Apple is also not allowed to talk about this demand, which is why it hasn’t explained the choice to turn off ADP in the UK.

This is a developing story; we’ll keep you up to date. Will the UK now blink, or will Apple be exiting the UK market? In the meantime, this is a good reason to familiarize yourself with [how much of your data is encrypted](https://support.apple.com/en-gb/102651) and what you’d be getting by enabling ADP. Perhaps you might even consider enabling it—unless you live in the UK, that is.

## Short News

Here are some things that caught our attention since the previous newsletter:

- We start with something completely different from the usual programming: a talk from Peter Gutmann, who thinks that post-quantum cryptography is a waste of time. The talk is titled [Why Quantum Cryptanalysis Is Bollocks](https://www.cs.auckland.ac.nz/~pgut001/pubs/bollocks.pdf). You just know it’s going to be a lot of fun! Peter does make a good point, which is that we don’t actually know if it is possible to build a proper, working, cryptographically relevant quantum computer. That is, unless some people—those who are pushing this through—do know, but don’t want to say. In any case, if you’ve been experiencing quantum fatigue recently, you’ll be happy to know that you’re not alone.
- Proving Peter’s points, perhaps—have you heard about the recent, biggest-ever, cryptocurrency heist, with $1.4 billion stolen? The attackers compromised an S3 bucket, then [injected malicious JavaScript](https://docsend.com/view/s/rmdi832mpt8u93s7) just where they needed it to be.
- PKI Consortium’s 2025 PQC conference took place in Austin in January, and it advanced the post-quantum conversation with [interesting presentations](https://pkic.org/events/2025/pqc-conference-austin-us/). If you’re looking for a starting point, try these [key takeaways](https://pkic.org/2025/01/30/key-takeaways-of-the-pqc-conference-in-austin/) first.
- Microsoft [announced a new quantum chip](https://news.microsoft.com/source/features/innovation/microsofts-majorana-1-chip-carves-new-path-for-quantum-computing/) built on a new technology called *topoconductor*. In the company’s words, Microsoft wants to build a transistor for the quantum age. This is possibly a promising direction, but there’s nothing remotely practical to see yet. Scott Aaronson [looked into these claims](https://scottaaronson.blog/?p=8669).