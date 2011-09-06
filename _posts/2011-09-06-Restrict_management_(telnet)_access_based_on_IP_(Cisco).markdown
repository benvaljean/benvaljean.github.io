---
layout: post 
title: Restrict management (telnet) access based on IP (Cisco)
---

-   Restrict management access to only 10.1.1.0/24 and 10.10.10.0/23

<!-- -->

    telnet access-group 20
    access-list 20 permit 10.10.1.0 0.0.0.255
    access-list 20 permit 10.10.10.0 0.0.1.255
    access-list 20 deny any

#### See Also

[Configuring
ACLs](http://www.cisco.com/en/US/products/sw/secursw/ps1018/products_tech_note09186a00800a5b9a.shtml#topic2)

[Category:Cisco](Category:Cisco "wikilink")
