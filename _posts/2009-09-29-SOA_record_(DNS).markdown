---
layout: post 
title: SOA record (DNS)
---

Instead of the standard \'TTL\' for a zone/dns record - known as simply
\'TTL\' - there are additional TTLs that are configured within the SOA
record:

Refresh --- This is the number of seconds between update requests from
secondary and slave name servers.

Retry --- This is the number of seconds the secondary or slave will wait
before retrying when the last attempt has failed.

Expire --- This is the number of seconds a master or slave will wait
before considering the data stale if it cannot reach the primary name
server.

Minimum --- Previously used to determine the minimum TTL, this is used
for negative caching. This is the default TTL if the domain does not
specify a TTL.

TTL (time to live) - The number of seconds a domain name is cached
locally before expiration and return to authoritative nameservers for
updated information.

[Category:Web](Category:Web "wikilink")
[Category:DNS](Category:DNS "wikilink")
