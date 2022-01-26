---
title: "DHCP Spoofing Attacks"
date: 2022-01-26
author: "Zachary Robinson"
tags: []
draft: true
---

Dynamic Host Configuration Protocol, or DHCP for short, is one of the most useful protocols for a network admin. For a large network with hundreds or thousands of end-devices, configuring each one manually with an IP Address would be tedious and error prone. DHCP allows admins to define a range of IP Addresses and specify other configuration info for devices to automatically obtain. However, like most protocols, it has a security downfall.

DHCP spoofing is when a malicious actor sets up an alternate DHCP server on a network to provide false addressing and configuration information to clients. After a client sends a DHCP Discover message, it will typically accept a DHCP Offer from whichever server responds to it the fastest. If the rogue server responds faster and the offer is accepted, there are a few incorrect pieces of information that could have negative impacts on clients, and the network as a whole. 

First, the rogue server could create a Denial of Service (DoS) attack by giving clients the incorrect Default Gateway, IP Address, Subnet Mask, or DNS server. If a client requests network resources with any of this incorrect information, they may not have access. Along with that, they could also create a Man-In-The-Middle (MITM) attack by giving clients an alternate Default Gateway that then forwards their packets to the legitimate Default Gateway. If their communication isn't encrypted, then the alternate Default Gateway could intercept their messages and gain information from them. For example, a poorly designed website with HTTP could expose the user's password in their packets, meaning the malicious actor could log in as the client. Last, the rogue server could prove an alternate DNS server that logs DNS queries to gain information about the resources access the most. It could also return an incorrect IP address for a particular domain name, possibly directing a user towards a copy-cat website to gain access to their login credentials.

Thankfully, there is a way to prevent such an attack. DHCP snooping can be enabled on network infrastructure to limit what types of DHCP messages can be sent on certain ports. All access ports that connect to end-users should be marked as untrusted (this is done by default). This means that any DHCP Offer messages will be blocked by the switch they are connected to, preventing them from acting as a DHCP server. On the other hand, ports that connect to other network devices that are managed by the admin should be marked as trusted. This lets any DHCP messages pass through them, allowing the legitimate DHCP server to do its intended function.

At the end of the day, almost all networking protocols can be exploited to damage the network in some way, shape, or form. The Layer 2 of the OSI model is one of the most error prone due to the fact that most of the protocols for that layer were invented before the need for network security became as obvious as it is today. They used to be able to rely on the fact that everyone on the network could be trusted in a closed academic or corporate environment. However, we do not have that same luxury. We can design networks all day long, but if they're not secure, then all that work could just come crumbling down at any second. 

---

*This post was adapted from a project for my Honors Cisco Academy class.*
