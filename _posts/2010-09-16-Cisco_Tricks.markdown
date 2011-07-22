---
layout: post 
title: Cisco Tricks
---

Show interfaces:

    sh ip int brief

Do not use the pager (more):

    terminal length 0

Show VRFs:

    show ip vrf

#### Show failover config

`sh ip int brief` will not show VIPs, to show this:

    sh standby

#### Restart VPN tunnel

Initiate config mode, and \'cd\' to the tunnel interface:

    conf t
    int Tunnelxxxxxx

Stop tunnel:

    shutdown

Bring tunnel back up:

    no shutdown

[Category:Networking](Category:Networking "wikilink")
