---
layout: post 
title: SOA record (DNS)
---

SOA record metrics:

**Refresh**: This is the number of seconds between update requests from
secondary and slave name servers. If notifies are enabled this is a
fairly redundant feature.

**Retry**: This is the number of seconds the secondary or slave will
wait before retrying when the last attempt has failed.

**Expire**: This is the number of seconds a master or slave will wait
before considering the data stale if it cannot reach the primary name
server.

**Minimum**: Previously used to determine the minimum TTL, this is used
for negative caching. This is the default TTL if the domain does not
specify a TTL.

**DNS Client TTL** (time to live) - The number of seconds any DNS record
is cached on a DNS server that queries your NS before expiration and
return to your (authoritative) nameservers for updated information. This
is also in theory the number of seconds a local DNS Client will keep
queries cached before re-performing the query although it is largely not
followed by browsers.

#### References

<http://www.simplefailover.com/outbox/dns-caching.pdf>

<http://support.microsoft.com/kb/163971>

[Category:BIND](Category:BIND "wikilink")
[Category:DNS](Category:DNS "wikilink")
