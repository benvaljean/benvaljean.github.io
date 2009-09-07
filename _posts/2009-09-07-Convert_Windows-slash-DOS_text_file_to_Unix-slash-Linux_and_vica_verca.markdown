---
layout: post 
title: Convert Windows/DOS text file to Unix/Linux and vica verca
---

A text-file created in Windows/DOS may appear incorrectly on Unix/Linux
depending on how it transferred - some systems do the conversion
automatically.

    tr -d '\\15\\32' < dosfile.txt > unixfile.txt

[Category:Linux](Category:Linux "wikilink")
