---
layout: post 
title: DNS Failover / High Availability
---

The native Linux resolver with default settings cannot be relied upon
for HA / failover. By default there are two attempts each with a 5
second timeout. Therefore **every query** has to wait 10 seconds before
the secondary DNS server is queried. Linux does not natively mark a DNS
node is \'dead\' and send all queries to a secondary node, it try the
primary upon every single query.

#### Solutions

-   Use an HA facility that will move the VIP from the primary to the
    secondary if the primary node fails, such as
    \[www.linux-ha.org/wiki/Heartbeat\|Heartbeat\]. All resolv.conf
    nameserver entries point to this VIP.
-   Use a Load-balancer with service-detection - not just layer 3.
-   Use [Name Server Cache Daemon](http://linux.die.net/man/8/nscd) to
    cache the DNS entries and mitigate the risk of a failure. Not
    recommended as adding an extra of complexity (caching on the
    individual servers) may have unpredictable results.
-   Use [Domain Name Relay Daemon](http://dnrd.sourceforge.net/) that
    will allow the DNS client to mark a node as down and not retry it
    until it is back up again. Only the first queries that were sent
    before NSCD marked it as down would be affected by the 10 second
    timeout mentioned above.
-   Tweak the resolv.conf settings to reduce the timeout.

#### Tweaking resolv.conf

Firstly get some stats on how long querys take on your network. BIND
does this natively through
[stats](http://www.zytrax.com/books/dns/ch7/statistics.html%7Crndc).
Once an appropriate maximim query time is defined. The timeout that the
Linux resolver waits for before trying to secondary node can be tweaked,
this is done through the `options timeout:n` directive where *n* isthe
number of seconds.

Another directive `options rotate` can be used to provide
pseudo-load-balancing. It is pseudo-load-balancing as upon testing the
primary node still receives double the queries than the secondary. This
is better than 99% of queries as it is without this directive being
applied. Testing with ping will not proove that it is working as a new
process will restart the round-robin.

##### Example config

    search dc2.uk.eu.company.loca. uk.eu.company.local eu.company.local
    nameserver 1.1.1.1
    nameserver 2.2.2.2
    options timeout:2 rotate

This will give two attempts (default) each with a timeout of 2 seconds =
4 seconds until the secondary is called. A more aggressive config would
be `options timeout:1 attempts:1 rotate` which can be used so long as
there is no recursion in your environment, otherwise queries which may
otherwise have returned may fail.

### References

-   <http://linux.die.net/man/5/resolv.conf>
-   <http://docstore.mik.ua/orelly/networking_2ndEd/dns/ch06_01.htm>

[Category:DNS](Category:DNS "wikilink")
[Category:Linux](Category:Linux "wikilink")
