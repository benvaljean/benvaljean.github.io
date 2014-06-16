---
layout: post 
title: Force Password Authentication on SSH (Linux)
---

Disable use of public key authentication such as provided by your ssh
agent:

    ssh -o PubkeyAuthentication=no <followed by usual arguments>

[Category:Linux](Category:Linux "wikilink")
