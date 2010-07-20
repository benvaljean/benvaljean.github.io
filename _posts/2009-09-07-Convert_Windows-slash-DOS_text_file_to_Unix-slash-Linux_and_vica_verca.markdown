---
layout: post 
title: Convert Windows/DOS text file to Unix/Linux and vica verca
---

A text-file created in Windows/DOS may appear incorrectly on Unix/Linux
depending on how it transferred - some programmes do the conversion
automatically. Convert Windows/DOS text file to Unix/Linux:

    tr -d '\\15\\32' < dosfile.txt > unixfile.txt

Convert Unix/Linux text file to Windows/DOS:

    sed 's/$'"/`echo \\\\\\r`/" unixfile.txt > dosfile.txt

[Category:Linux](Category:Linux "wikilink")
