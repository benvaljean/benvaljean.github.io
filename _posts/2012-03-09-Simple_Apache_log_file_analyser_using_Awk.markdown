---
layout: post 
title: Simple Apache log file analyser using Awk
---

Show counts of status codes:

    awk '{count[$9]++}END{for(j in count) print j," "count[j]" request(s)"}' access.log

You may need to be change the column number - \$9 - depending on your
log file format.

[Category:Web](Category:Web "wikilink")
