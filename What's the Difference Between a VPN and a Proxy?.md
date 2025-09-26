---
title: What's the Difference Between a VPN and a Proxy?
source: https://www.howtogeek.com/247190/whats-the-difference-between-a-vpn-and-a-proxy/
author:
  - "[[Jason Fitzpatrick]]"
published: 2016-07-25
created: 2025-02-16
description: A proxy connects you to a remote computer and a VPN connects you to a remote computer so they must be, more or less, the same thing, right? Not exactly.
tags:
  - clippings
  - southwall/homelab
---
### Quick Links

- [Selecting the Right Tool Is Critical](https://www.howtogeek.com/247190/whats-the-difference-between-a-vpn-and-a-proxy/#selecting-the-right-tool-is-critical)

- [Proxies Hide Your IP Address](https://www.howtogeek.com/247190/whats-the-difference-between-a-vpn-and-a-proxy/#proxies-hide-your-ip-address)

- [Virtual Private Networks Encrypt Your Connection](https://www.howtogeek.com/247190/whats-the-difference-between-a-vpn-and-a-proxy/#virtual-private-networks-encrypt-your-connection)

A proxy connects you to a remote computer and a VPN connects you to a remote computer so they must be, more or less, the same thing, right? Not exactly. Let's look at when might you want to use each, and why proxies are a poor substitute for VPNs.

Practically every other week there's a major news story about encryption, leaked data, snooping, or other digital privacy concerns. Many of these articles talk about the importance of beefing up the security of your Internet connection, like using a VPN (Virtual Private Network) when you're on public coffee shop Wi-Fi, but they're often light on the details. How exactly do the proxy servers and VPN connections we keep hearing about actually work? If you're going to invest the time and energy in improving security you want to be sure you're selecting the right tool for the right job.

## Proxies Hide Your IP Address

A proxy server is a server that acts as a middleman in the flow of your internet traffic, so that your internet activities appear to come from somewhere else. Let's say for example you are physically located in New York City and you want to log into a website that is geographically restricted to only people located in the United Kingdom. You could connect to a proxy server located within the United Kingdom, then connect to that website. The traffic from your web browser would appear to originate from the remote computer and not your own.

Proxies are great for low-stakes tasks like watching region-restricted YouTube videos, bypassing simple content filters, or bypassing IP-based restrictions on services.

For example: Several people in our household play an online game where you get a daily in-game bonus for voting for the game server on a server ranking website. However, the ranking website has a one-vote-per-IP policy regardless of whether different player names are used. Thanks to proxy servers each person can log their vote and get the in-game bonus because each person's web browser appears to be coming from a different IP address.

![img_56f57e1899a0f](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2016/03/img_56f57e1899a0f.png)

Anyone with access to the stream of data (your ISP, your government, a guy sniffing the Wi-Fi traffic at the airport, etc.) can snoop on your traffic. Further, certain exploits, like malicious Flash or JavaScript elements in your web browser, can reveal your true identity. This makes proxy servers unsuitable for serious tasks like preventing the operator of a malicious Wi-FI hotspot from stealing your data.

Finally, proxy server connections are configured on an application-by-application basis, not computer-wide. You don't configure your entire computer to connect to the proxy--you configure your web browser, your BitTorrent client, or other proxy-compatible application. This is great if you just want a single application to connect to the proxy (like our aforementioned voting scheme) but not so great if you wish to redirect your entire internet connection.

The two most common proxy server protocols are HTTP and SOCKS.

### HTTP Proxies

If you're using an HTTP proxy to connect to any sort of sensitive service, like your email or bank, it is critical you use a browser with SSL enabled, and connect to a web site that supports SSL encryption. As we noted above, proxies do not encrypt any traffic, so the only encryption you get when using them is the encryption you provide yourself.

### SOCKS Proxies

The SOCKS proxy system is a useful extension of the HTTP proxy system in that SOCKS is indifferent to the type of traffic that passes through it.

Where HTTP proxies can only handle web traffic, a SOCKS server will simply pass along any traffic it gets, whether that traffic is for a web server, an FTP server, or BitTorrent client. In fact, in [our article on securing your BitTorrent traffic](https://www.howtogeek.com/76801/how-to-anonymize-and-encrypt-your-bittorrent-traffic/), we recommend the use of [BTGuard](http://btguard.com/?a=J295J359), an anonymizing SOCKS proxy service based out of Canada.

The downside to SOCKS proxies is that they are slower than pure HTTP proxies because they have more overhead and, like HTTP proxies, they offer no encryption beyond what you personally apply to the given connection.

### How to Select a Proxy

While there are stand-alone commercial services out there like aforementioned [BTGuard](http://btguard.com/?a=J295J359),  the rise of faster computers and mobile devices coupled with faster connections (both of which reduce the impact of encryption overhead) the proxy has largely fallen out of favor as more and more people opt to use superior VPN solutions.

## Virtual Private Networks Encrypt Your Connection

Virtual Private Networks, like proxies, make your traffic appear as if it comes from a remote IP address. But that's where the similarities end. VPNs are set up at the operating system level, and the VPN connection captures the entire network connection of the device it is configured on. This means that unlike a proxy server, which simply acts as a man-in-the-middle server for a single application (like your web browser or BitTorrent client), VPNs will capture the traffic of every single application on your computer, from your web browser to your online games to even Windows Update running in the background.

![/wordpress/wp-content/uploads/2016/03/img_56f58615dd0a3.png](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2016/03/img_56f58615dd0a3.png)

Even if you're not currently on a business trip in rural Africa, you can still benefit from using a VPN. With a VPN enabled, you never have to worry about crappy Wi-Fi/network security practices at coffee shops or that the free internet at your hotel is full of security holes.

Although VPNs are fantastic, they are not without their downsides. What you get in whole-connection-encryption, you pay for in money and computing power. Running a VPN requires good hardware and, as such, good VPN services are not free (although some providers, like [TunnelBear](https://www.anrdoezrs.net/links/3607085/type/dlg/sid/UUhtgUeUpU218837/https://www.tunnelbear.com/b/vpn-yearly?utm_source=affiliate&utm_medium=cj&ref_id=mkt_aff-cj-prem&cjevent=18c53609708d11ef801843c50a82b838&aff_id=2786910&utm_campaign=Valnet+Inc.&clickid=18c53609708d11ef801843c50a82b838), do offer a very spartan free package). Expect to pay at least a few dollars a month for a robust VPN service [like the solutions we recommend in our VPN guide](https://www.howtogeek.com/221929/how-to-choose-the-best-vpn-service-for-your-needs/), [StrongVPN](http://strongvpn.com/) and [ExpressVPN](https://go.expressvpn.com/c/156932/1330033/16063?subId1=UUhtgUeUpU218837&subId2=ehtg&u=https%3A%2F%2Fwww.expressvpn.com%2F).

The other cost associated with VPN's is performance. Proxy servers simply pass your information along. There is no bandwidth cost and only a little extra latency when you use them. VPN servers, on the other hand, chew up both processing power and bandwidth on account of the overhead introduced by the encryption protocols. The better the VPN protocol and the better the remote hardware, the less overhead there is.

---

In summary, proxies are great for hiding your identity during trivial tasks (like "sneaking" into another country to watch a sports match) but when it comes to more series tasks (like protecting yourself from snooping) you need a VPN.