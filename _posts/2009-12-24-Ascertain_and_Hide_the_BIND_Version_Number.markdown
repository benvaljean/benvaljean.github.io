---
layout: post 
title: Ascertain and Hide the BIND Version Number
---

By default BIND will display its version number as a chaos type TXT
record called version.bind .

    host -t TXT -c CHAOS version.bind nameserver
    Using domain server:
    Name: nameserver
    Address: ipaddress#53
    Aliases:

    version.bind descriptive text "version number here"

Hiding the version number will make a nameserver slightly less
vulnerable to attacks from hackers. If a particular vulnerability for a
specific BIND release is announced hackers may try searching numerous
records until a a hit for the exact version is found. Hiding the version
number protects the server from this.

#### Hide BIND Version Number

    options {
        version "Not available";
    }

A reload of the config required for the config change to take effect:
`sudo /etc/init.d/bind9 reload`

[Category:DNS](Category:DNS "wikilink")
[Category:BIND](Category:BIND "wikilink")
