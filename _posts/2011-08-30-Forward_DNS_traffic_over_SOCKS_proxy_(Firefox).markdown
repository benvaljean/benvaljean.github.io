---
layout: post 
title: Forward DNS traffic over SOCKS proxy (Firefox)
---

By default Firefox when using a socks proxy will still use the local DNS
configuration before forwarding traffic to the proxy. This can have some
drawbacks:

-   Site being accessed is part of a corporate intranet or production
    network and the DNS records do not face the internet and are
    consequently not in local DNS.
-   Internet censorship at the DNS level prevents use of SOCKS proxy.

Firefox can be configured to use the SOCKS proxy for DNS by changing the
following setting in <about:config> :

    network.proxy.socks_remote_dns

Set this value to **true** to route DNS traffic to the SOCKS proxy.

[Category:Web](Category:Web "wikilink")
[Category:Linux](Category:Linux "wikilink")
[Category:Windows](Category:Windows "wikilink")
