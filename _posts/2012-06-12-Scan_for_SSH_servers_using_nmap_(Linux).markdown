---
layout: post 
title: Scan for SSH servers using nmap (Linux)
---

Scan for SSH servers in a subnet whilst outputting the version string in
a format that is easily greppable or parsed into a script of some kind:

    nmap -p22 --open -PN -sV -oG ssh_hosts 10.1.100.0/24

*-PN* states that nmap should not try to ping the host. If it does then
it can detect a host as being down when it is in actual fact up.

[Category:Linux](Category:Linux "wikilink")
