---
layout: post 
title: Calculate Sum and Average using Awk (Linux)
---

Awk can be used to caclulate the sum and average of a particular field:

    awk '{ s += $15 } END { print "sum: ", s, " average: ", s/NR, " samples: ", NR }' logfile.log

[Category:Linux](Category:Linux "wikilink")
