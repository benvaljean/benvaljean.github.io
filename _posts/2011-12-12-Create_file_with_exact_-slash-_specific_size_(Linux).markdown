---
layout: post 
title: Create file with exact / specific size (Linux)
---

Create a 250MB (MegaByte) file with random characters:

    dd if=/dev/random of=250MB-file bs=1024 count=$((250*1024))

[Category:Linux](Category:Linux "wikilink")
