---
layout: post 
title: Prevent brute-force attack by rate-limiting connections (iptables)
---

A quick an easy way to prevent or dramatically-hinder brute-force
attacks to limit the rate of new connections.

Allow a maximum of 3 SSH connections per minute:

    -A INPUT -p tcp --dport 22 -m state --state NEW -m limit --limit 3/min --limit-burst 3 -j ACCEPT

Ensure this rule is above the rule that allows your SSH connections

[Category:Linux](Category:Linux "wikilink")
[Category:Iptables](Category:Iptables "wikilink")
