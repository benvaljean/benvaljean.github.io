---
layout: post 
title: Verify SSH server host key
tags: Linux
---

If when SSHing to a server you receive an alert that the host dsa key
for the SSH server does not match the fingerprint listed in
\~/known\_hosts, the finger print can be checked providing you have
physical access to the server or another connection is already open:

    ssh-keygen -l -f /etc/ssh/ssh_host_dsa_key.pub

Run this on the server you are trying to connect TO and compare the
output to that given from the ssh client.

[Category:Linux](Category:Linux "wikilink")
