---
layout: post 
title: Block / Ban MAC address in dhcpd (Linux)
---

Add to dhcpd.conf:

    host badguy {
    hardware ethernet 0:c0:c3:11:90:23;
    deny booting;
    }

[Category:Linux](Category:Linux "wikilink")
