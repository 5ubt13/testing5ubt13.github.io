---
layout: post
title:  "Firewalls and IDSs"
description: "Types of Firewalls and Intrusion Detection Systems"
author: 0x5ubt13
date:   2020-11-17 16:00:00 +0000
categories: Blog
---

November 24th, 2020 - Blog post. Last edited: November 29th, 2020.

# Firewalls and Intrusion Detection Systems

### Table of contents:



|           Key                         |                      Content                        |
|:------------------------------------- |:----------------------------                        |
| <a href="#firewall">1.</a>            | What is a firewall                                  |
| <a href="#types">1.1</a>              | Types of firewall                                   |
| <a href="#filter">1.1.1</a>           | Packet-filtering firewalls                          |
| <a href="#gateways"> 1.1.2 </a>       | Circuit-level gateways                              |
| <a href="#stateful">1.1.3</a>         | Stateful inspection firewalls                       |
| <a href="#app">1.1.4</a>              | Application-level gateways (a.k.a. proxy firewalls) |
| <a href="#next">1.1.5</a>             | Next-gen firewalls                                  |
| <a href="#ids">2.</a>                 | What is an Intrusion Detection System (IDS)?        |
| <a href="#refs">3.</a>                | References                                          |

---

 

## <a id="firewall"></a> What is a firewall:
A firewall is a type of cybersecurity tool, either a hardware device or a utility program, that is used to monitor a network, by accepting, rejecting or dropping packets passing through it in any way, either incoming or outgoing. If the firewall deems the packets are suspicious, it will block it regardless of its procedence. Firewalls can be used to separate network nodes from external traffic sources, internal traffic sources, or even specific applications. 

Firewalls can be software, hardware, or cloud-based, with each type of firewall having its own unique pros and cons. I like the analogy of it being like the high wall around a castle, blocking out the invading hordes, whilst still allowing friendly citizens in and out through its drawbridge. The firewall basically do the same, with the slight difference it also blocks suspicious activity from going outside, like a burglar after a bank heist that gets stopped right before passing the border trying to escape to a different country.

Therefore, we can say the primary goal of a firewall is to block malicious traffic requests and data packets while allowing legitimate traffic through.

There are 2 kinds of firewalls, software-based and hardware-based firewalls.

### Software firewall vs Hardware firewall:

The main difference between the hardware firewall and the software firewall is that the hardware firewall is an actual physical device that will sit between your local area network and the internet. Whereas the software firewall will be installed on each individual device.
This means the hardware firewall can stop bad data from ever entering the network, while software firewalls can offer closer controls over specific devices and how they interact with the network and internet.

There are a few different techniques that firewalls use to filter data, which I will try and cover in this blog post.

## <a id="types"></a> Types of firewall:
Depending on their general structure and approach of operation, firewalls can be divided in the following categories:

- <a href="#filter">Packet-filtering firewalls</a>
- <a href="#gateways">Circuit-level gateways</a>
- <a href="#stateful">Stateful inspection firewalls</a>
- <a href="#app">Application-level gateways (a.k.a. proxy firewalls)</a>
- <a href="#next">Next-gen firewalls</a>

### <a id="filter"></a> Packet-filtering Firewalls
With packet filtering, the firewall inspects each packet of data and compares it to pre-defined security rules (known as the firewall policy, or ruleset). If the packet is flagged by the rules, then it is prevented from passing through the firewall. This is the most basic and precursor of other firewall architectures. These firewalls aren't resource-intensive, so you can plant them in any system regadless of the requisites. The con is they are easy to circumvent, compared to more modern ones.

### <a id="gateways"></a> Circuit-level Gateways

[The Techopedia](https://www.techopedia.com/definition/24780/circuit-level-gateway) defines Circuit-Level gateways as follows:

>A circuit-level gateway is a firewall that provides User Datagram Protocol (UDP) and Transmission Control Protocol (TCP) connection security, and works between an Open Systems Interconnection (OSI) network model’s transport and application layers such as the session layer. Unlike application gateways, circuit-level gateways monitor TCP data packet handshaking and session fulfillment of firewall rules and policies.

These firewalls check by verifying the TCP handshake. They are very efficient regarding resources but they don't check the packet, therefore, if the packet contains malware and had the right handshake, it would go through regardless, so you would need to add another layer of security.


### <a id="stateful"></a> Stateful inspection Firewalls:
Using the 2 previous technologies, packet inspection and TCP handshake verification, we can use them and combine them together to conceive a superior protection than the two of them alone.
These firewalls combine both packet inspection technology and TCP handshake verification to create a level of protection greater than either of the previous two architectures could provide alone.

The con with these firewalls is that they put more of a strain on computing resources as well. This may slow down the transfer of legitimate packets compared to the other solutions in exchange for better security.


### <a id="app"></a> Application-level Gateways (a.k.a. Proxy Firewalls / Cloud Firewalls)
As their name suggests, they operate at the application layer to filter the traffic sitting in between your network and the outter network that the packet comes from. They are managed via a cloud-based solution or another proxy device. The proxy firewall inspects the incoming data packets and then allows them through. This kind of Firewalls is very similar to the category explored above this one, but application layer gateways can also perform deep-layer packet inspections


### <a id="next"></a> Next-gen firewalls:
Although there isn't a general consensus about what a Next-Gen firewall is, the majority of the most recently-released products are branded after this etiquette. A next-gen Firewall must include:

- Standard firewall capabilities like stateful inspection
- Integrated intrusion prevention
- Application awareness and control to see and block risky apps
- Upgrade paths to include future information feeds
- Techniques to address evolving security threats

 

## <a id="ids"></a> Intrusion Detection Systems:
They are devices or applications that like a Firewall, as seen above, monitor the network they are implemented in for suspicious activity. If they detect a malicious activity or a policy violation, these are reported or collected centrally using a security information and event management system. The most common classifications of IDS are:

- Network intrusion detection systems (NIDS): 
Systems like firewalls that analyze incoming network traffic.

- Host-based intrusion detection systems (HIDS): 
Systems like antivirus software that monitor important operating system files.


 

# <a id="refs"></a> References:

Anon., 2020. Cisco - "What Is a Firewall?" [Online] \
[https://www.cisco.com/c/en_uk/products/security/firewalls/what-is-a-firewall.html](https://www.cisco.com/c/en_uk/products/security/firewalls/what-is-a-firewall.html) \
[Last accessed Nov 29th, 2020]

Eric Dosal, 26/11/2019. Compuquip - "What is a Firewall? The Different Firewall Types & Architectures" [Online] \
[https://www.compuquip.com/blog/the-different-types-of-firewall-architectures](https://www.compuquip.com/blog/the-different-types-of-firewall-architectures) \
[Last accessed Nov 29th, 2020]

Eric Dosal, 17/09/2019. Compuquip - "Which of the Following Are Characteristics of a Circuit-Level Gateway?" [Online] \
[https://www.compuquip.com/blog/characteristics-of-a-circuit-level-gateway](https://www.compuquip.com/blog/characteristics-of-a-circuit-level-gateway) \
[Last accessed Nov 29th, 2020]

Anon., 2020. Techopedia - "Circuit-Level Gateway" [Online] \
[https://www.techopedia.com/definition/24780/circuit-level-gateway](https://www.techopedia.com/definition/24780/circuit-level-gateway) \
[Last accessed Nov 29th, 2020]

Anon., 2020. Barracuda - "What is a Intrusion Detection System?" [Online] \
[https://www.barracuda.com/glossary/intrusion-detection-system](https://www.barracuda.com/glossary/intrusion-detection-system)
[Last accessed Nov 29th, 2020]

 

---

 

[Previous blog post](https://0x5ubt13.github.io/blog/2020/11/17/encrypted-mail.html)

[All blog posts](https://0x5ubt13.github.io/)

[My GitHub profile](https://github.com/0x5ubt13)

 

---

