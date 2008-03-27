---
layout: post 
title: Squid Stuff
---

<font color=red>Do not have the Squid disk-cache on a RAIDed volume, or
a RAIDed LUN on a SAN if not just RAID 0</font>

<http://wiki.squid-cache.org/ConfigExamples> includes OWA reverse proxy

<http://meta.wikimedia.org/wiki/Squid_caching>

[Squid-Cache Wiki: FAQ](http://wiki.squid-cache.org/SquidFaq/) Very Good

:   [Operating
    Squid](http://wiki.squid-cache.org/SquidFaq/OperatingSquid) Flush
    whole cahe, or one object and other stuff.
:   [Proxy
    Authentication](http://wiki.squid-cache.org/SquidFaq/ProxyAuthentication)
    Important if you want uses to seamlessly authenticate using NTLM (on
    a Windows domain) without typing in a pass
:   [Reverse Proxy](http://wiki.squid-cache.org/SquidFaq/ReverseProxy)
    Very good page about having several sites (virtual or otherwise)
    being reverse proxied though the same squid server. Also gives
    details on how squid can pass-through authentication.
:   [Squid Logs Guide](http://wiki.squid-cache.org/SquidFaq/SquidLogs)
