---
layout: post 
title: Scan for SSH servers using nmap (Linux)
---

Scan for SSH servers in a subnet whilst outputting the version string in
a format that is easily greppable or parsed into a script of some kind:

    nmap -p22 --open -PN -sV -oG ssh_hosts 10.1.100.0/24

Or another way, this presents a list if IPs that have SSH up:

    nmap -p 22 10.44.46.0/27|awk '/scan report for/ {print $0}'|grep -Eo '[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}'

[Category:Linux](Category:Linux "wikilink")
