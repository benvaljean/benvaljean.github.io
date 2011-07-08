---
layout: post 
title: Extract IP address from string using grep
---

`-o` option tells grep to only print the parts that match the grep

    $ host yahoo.com | grep -Eo '([0-9]{1,3}\\.){3}[0-9]{1,3}'
    209.191.122.70
    67.195.160.76
    69.147.125.65
    72.30.2.43
    98.137.149.56

[Category:Linux](Category:Linux "wikilink")
