---
layout: post 
title: Get Motherboard / Manufacturer information from the command line (Linux)
---

These commands can be useful if you need to ascertain the manufacturer
of a server or the motherboard when there is no easy way to physically
access the PC:

RHEL/CentOS/Fedora:

    sudo dmidecode|less

Debian/Ubuntu:

    sudo apt-get install hwinfo ; sudo hwinfo

[Category:Linux](Category:Linux "wikilink")
