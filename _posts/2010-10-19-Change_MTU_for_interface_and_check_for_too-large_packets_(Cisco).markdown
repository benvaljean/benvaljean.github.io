---
layout: post 
title: Change MTU for interface and check for too-large packets (Cisco)
---

#### Check for packets exxeeding MTU

The number of packets exceeding MTU are listed under the `giant` counter
on the interface:

    cloud.net#sh int BVI1 | i giant
         Received 0 broadcasts, 0 runts, 85 giants, 0 throttles

#### Change MTU

    en
    conf t
    int dsl0
    mtu <mtu in bytes>
    exit
    copy running-config startup-config

[Category:Cisco](Category:Cisco "wikilink")
