---
layout: post 
title: Squid Stuff
---

<font color=red>Do not have the Squid disk-cache on a RAIDed volume, or
a RAIDed LUN on a SAN if not just RAID 0</font> test

#### Useful Sites

<http://wiki.squid-cache.org/ConfigExamples>

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

[Six Things First-Time Squid Administrators Should
Know](http://www.onlamp.com/pub/a/onlamp/2004/02/12/squid.html)

#### Using Squid to Reverse Proxy Outlook Web Access

Placing an [Exchange
server](http://en.wikipedia.org/wiki/Microsoft_Exchange_Server) on the
DMZ or even port forwarding 443 only is arguably a security hazard.
Squid can be used as a reverse proxy in order to minimise the security
risks. When setup Squid faces the internet instead of Exchange and the
requests are relayed from Squid back to the Exchange server.

Due to failures of the OWA application this can be more then a little
tricky and a search for \"Squid reverse proxy owa\" (or other proxies
for that matter) will yield many results. OWA acts as if HTTP(S) were
not a stateless protocol; causing issues with passing the authentication
through correctly after logging on for every component. In addition
Public folders can never be reverse proxied without work to rewrite the
links through Squid as the OWA application inserts direct links to the
exchange server in the HTML so any attempt to access public folders will
result in a direct connection with the exchange server. Lastly,
host-headers are not processed according to RFC standards which will
cause problems if anything runs on a non-standard port - on WAN or LAN
side.

Of all the configuration examples out there I recommend the one below:

[Squid-cache.org Squid And Outlook Web
Access](http://wiki.squid-cache.org/ConfigExamples/SquidAndOutlookWebAccess)

Exchange needs to be configured to allow a Front-end server to handle
the SSL: <http://technet.microsoft.com/en-us/library/bb124604.aspx>

### Removing objects from the cache

squidclient -p 80 -m PURGE <http://fullurl>
