---
layout: post 
title: Force Password Authentication on SSH (Linux)
---

If a server does not have your public key on it but you are connecting
through a forwarding agent or simply so not wish to temporarily rename
your private key there is an option to disable public key authentication
even if a public key is present, thereby forcing password
authentication:

    ssh -o PubkeyAuthentication=no <followed by usual arguments>

[Category:Linux](Category:Linux "wikilink")
