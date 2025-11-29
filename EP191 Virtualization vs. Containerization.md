---
title: "EP191: Virtualization vs. Containerization"
source: "https://blog.bytebytego.com/p/ep191-virtualization-vs-containerization?publication_id=817132&post_id=180197534&isFreemail=true&r=of68&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2025-11-29
created: 2025-11-29
description: "Before containers simplified deployment, virtualization changed how we used hardware. Both isolate workloads, but they do it differently."
tags:
  - "clippings"
---

## Virtualization vs. Containerization

Before containers simplified deployment, virtualization changed how we used hardware. Both isolate workloads, but they do it differently.

![Image](https://substackcdn.com/image/fetch/$s_!SfCa!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F55ac4874-04fc-4ea7-a083-bde8f6f99cf5_2360x2960.png)

- Virtualization (Hardware-level isolation): Each virtual machine runs a complete operating system, Windows, Fedora, or Ubuntu, with its own kernel, drivers, and libraries. The hypervisor (VMware ESXi, Hyper-V, KVM) sits directly on hardware and emulates physical machines for each guest OS.
	This makes VMs heavy but isolated. Need Windows and Linux on the same box? VMs handle it easily. Startup time for a typical VM is in minutes because you’re booting an entire operating system from scratch.
- Containerization (OS-level isolation): Containers share the host operating system’s kernel. No separate OS per container. Just isolated processes with their own filesystem and dependencies.
	The container engine (Docker, containerd, CRI-O, Podman) manages lifecycle, networking, and isolation, but it all runs on top of a single shared kernel. Lightweight and fast. Containers start in milliseconds because you’re not booting an OS, just launching a process.
	But here’s the catch: all containers on a host must be compatible with that host’s kernel. Can’t run Windows containers on a Linux host (without nested virtualization tricks).

Over to you: What’s your go-to setup: containers in VMs, bare metal containers, or something else?

---

## 5 REST API Authentication Methods

![Image](https://substackcdn.com/image/fetch/$s_!zlUS!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F156acc80-7588-4fc1-8f43-7fa1458d646c_2360x2770.png)

1. Basic Authentication: Clients include a Base64-encoded username and password in every request header, which is simple but insecure since credentials are transmitted in plaintext. Useful in quick prototypes or internal services over secure networks.
2. Session Authentication: After login, the server creates a session record and issues a cookie. Subsequent requests send that cookie so the server can validate user state. Used in traditional web-apps.
3. Token Authentication: Clients authenticate once to receive a signed token, then present the token on each request for stateless authentication. Used in single-page applications and modern APIs that require scalable, stateless authentication.
4. OAuth-Based Authentication: Clients obtain an access token via an authorization grant from an OAuth provider, then use that token to call resource servers on the user’s behalf. Used in cases of third-party integrations or apps that need delegated access to user data.
5. API Key Authentication: Clients present a predefined key (often in headers or query strings) with each request. The server verifies the key to authorize access. Used in service-to-service or machine-to-machine APIs where simple credential checks are sufficient.

Over to you: Which other API Authentication method have you seen?

---

## How do AirTags work?

![Image](https://substackcdn.com/image/fetch/$s_!aFSg!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff57fe834-624f-4345-b54c-60997e0656f9_2560x3328.jpeg)

AirTags work by leveraging a combination of Bluetooth technology and the vast network of Apple devices to help you locate your lost items.  
Here’s a breakdown of how they function:

1. Bluetooth Signal: Each AirTag emits a secure Bluetooth signal that can be detected by nearby Apple devices (iPhones, iPads, etc.) within the Find My network.
2. Find My Network: When an AirTag comes within range of an Apple device in the Find My network, that device anonymously and securely relays the AirTag’s location information to iCloud.
3. Location Tracking: You can then use the Find My app on your own Apple device to see the approximate location of your AirTag on a map.

Limitations:  
Please note that AirTags rely on Bluetooth technology and the presence of Apple devices within the Find My network. If your AirTag is in an area with few Apple devices, its location may not be updated as frequently or accurately.

---

## What is a Firewall?

Every time you connect to the Internet, a firewall quietly decides what can come in and what must stay out. A firewall is your network’s first line of defense. It filters traffic based on rules you define, by IP address, protocol, port, program, or even keywords. Every packet that tries to enter or leave your network passes through this checkpoint.

![Image](https://substackcdn.com/image/fetch/$s_!CYiE!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5eb76d35-fba8-48de-84d1-228060740d89_2360x2960.png)

There are two main types:

1. Network Firewall: Sits at the network edge between your infrastructure and the internet. Can be physical hardware, virtualized software, or cloud-deployed service. Operates at Layer 3-4 of the OSI model. Filters traffic based on IP addresses, protocols, and ports before it ever reaches your internal network.  
	  
	Protects the entire network at once. This is your first line of defense. Internet traffic hits the network firewall before it reaches your router, before it touches any internal systems.
2. Host-based Firewall: This runs as software on individual devices, like your laptop or a server. It works at Layer 3–7, inspecting packets more deeply and protecting only that specific device.  
	  
	Your desktop has its own host firewall. Your server has its own. Each one is configured independently. It’s your last layer of defense in case something slips past the network firewall.  
	  
	Together, they form a layered shield, keeping unwanted traffic out while letting legitimate communication flow freely.

Over to you: Have you ever had to troubleshoot a misconfigured firewall rule that accidentally blocked something critical? What was it, and how long did it take to find?

---

## Modem vs. Router

Most people think their WiFi router gives them internet. It doesn’t. Your router is just managing traffic inside your home. The actual internet connection comes from the modem.

![Image](https://substackcdn.com/image/fetch/$s_!fKIx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7278af0a-b8cb-4b72-bd48-341e92286b1b_2360x2960.png)

Here’s what each one actually does:

- Modem: The modem connects you to your Internet Service Provider (ISP). It translates signals between your ISP’s network and your home network. Depending on the service type, the digital link may use coaxial cable, fiber optic, or cellular connections. The modem converts those signals into data your devices can understand.  
	  
	It provides one public IP address, meaning one connection to the internet. If you plug a single device directly into a modem via Ethernet, that device gets internet access with a public IP.
- Router: The router creates a private network inside your home. It takes that single public IP from the modem and shares it across multiple devices using Network Address Translation (NAT). Every device on your network gets a private IP address, usually something like 192.168.1.x. The router keeps track of which device requested what data and routes responses back to the right device.  
	  
	DHCP assigns those private IPs automatically. Your phone connects to WiFi, the router gives it an IP address, and suddenly it can talk to the internet through the router.

Modern devices often combine both functions, a modem-router combo, but understanding the distinction helps when you’re troubleshooting slow speeds or network drops.

Over to you: What’s your go-to trick to quickly diagnose whether the modem or router is to blame for slow Internet?

---

## SPONSOR US

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **sponsorship@bytebytego.com.**