---
layout: post 
title: NATing (iptables)
---

Forward connectons on WAN IP 1.1.1.1 to a machine on the the local
network of 192.168.1.1 on port 80:

    sudo iptables -D PREROUTING -t nat -d 1.1.1.1/32 -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.1:80

[Category:iptables](Category:iptables "wikilink")
[Category:Networking](Category:Networking "wikilink")
