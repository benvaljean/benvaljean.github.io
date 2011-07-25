---
layout: post 
title: Find duplicate PTRs in a zone file
---

For any RFC compliant reverse zone file including BIND / named, where
the first field is the last octet:

    for i in `egrep '^[0-9]{1,3}' reverse.rev | awk '{print $1}' | sort -n | uniq -d` ; do egrep ^${i} reverse.rev;done

As `awk` is used it will still work if spaces or tabs are used. Please
feel free to [contact](User:Benyg "wikilink") me if you find an instance
where it does not work.

[Category:DNS](Category:DNS "wikilink")
[Category:Linux](Category:Linux "wikilink")
