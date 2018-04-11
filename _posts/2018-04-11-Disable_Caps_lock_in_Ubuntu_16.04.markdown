---
layout: post 
title: Disable Caps lock in Ubuntu 16.04
---

Disable you Caps lock key in Ubuntu, tested on 16.04:

    sudo apt-get install dconf-tools
    setxkbmap -option "caps:none"

[Category:Linux](Category:Linux "wikilink")
