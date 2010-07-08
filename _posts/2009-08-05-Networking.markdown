---
layout: post 
title: Networking
---

==Protocol suite==
Six layers of protocols work together and are collectively known as the 'stack' or more formally the OSI reference model.
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Layer'''
| align="center" style="background:#f0f0f0;"|'''Name'''
| align="center" style="background:#f0f0f0;"|'''Description'''
| align="center" style="background:#f0f0f0;"|'''Popular examples'''
| align="center" style="background:#f0f0f0;"|'''Other examples'''
|-
|1||Physical layer||The actual physical infrastructure connecting devices together: Cabling and interfaces.||Ethernet, 802.11g||Token ring, T-Bone connectors
|-
|2||Link layer||Conversion between physical hardware with other forms of addressing.||ARP, PPP||SLIP
|-
|3||Network layer||Delivers and routes packets of data||IP, ICMP, Ipsec||IGMP
|-
|4||Transport layer||Formats/encodes/decodes data for transportation over a network||TCP, UDP, PPTP||L2TP
|-
|5||Session layer||Not always used: Facilitates a temporary session between two nodes/hosts.||NetBIOS||
|-
|6||Presentation layer||Not always used: Facilitates further formatting of data for the application layer of necessary.||MIME||
|-
|7||Application layer||The protocol that the application itself uses - the reason why all the previous layers have performed the function!||HTTP, SMB, DNS, FTP, SSH, SMTP, RDP||NTP, SNMP, NNTP, Gopher
|-
| 
|}
==Data link frame==
All data on a network is sent/received in packets, all packets are sent within data link frames:

{| {{table}}
| align="center" style="background:#b0f080;"|'''Layer 1/Ethernet/MAC Destination Address'''<br>48 bits
| align="center" style="background:#b0f080;"|'''Layer 1/Ethernet/MAC Source Address'''<br>48 bits
| align="center" style="background:#b0f080;"|'''Layer 3/IP Source Address'''<br>32 bits
| align="center" style="background:#b0f080;"|'''Layer 3/IP Source Address'''<br>32 bits
| align="center" style="background:#b0f080;"|'''Data'''
| align="center" style="background:#b0f080;"|'''PCB'''<br>32 bits
|-
| ||<--------------------------------||IP datagram||---------------||--->||
|-
| <--------------------------------||---------------------------------||Ethernet data link frame||--------------------||-----||-->
|-
| 
|}
*The layer 3 source/destination never change along the entire routing of the packet.
*The layer 1 source/destination will change from each hop to the next.

==See Also==
[http://www.soi.asia/pkg1/06/1.html Introduction to routing]
