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

Show interface names, VLANs and
connection-status[1](http://www.cisco.com/en/US/products/hw/switches/ps700/products_tech_note09186a008015bfd6.shtml#conno)
:

    sh int status

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
