---
layout: post 
title: Capture DHCP packets using Tcpdump (Linux)
---

Change `eth0` to match your service interface:

    sudo tcpdump -i eth0 port bootps -v -n

[Category:Linux](Category:Linux "wikilink")
