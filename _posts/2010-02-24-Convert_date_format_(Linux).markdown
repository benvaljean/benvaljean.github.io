---
layout: post 
title: Convert date format (Linux)
---

Convert a date expressed in `mm/dd/yyyy` format to
`Longday dd LongMonth yyyy` format with GNU date:

    date -d "02/24/2010" "+%A %d %B %Y"
    Wednesday 24 February 2010

The last parameter defines the format as shown here. Typing
`date --help` shows the elemwnts that can be used to set the format.

[Category:Linux](Category:Linux "wikilink")
