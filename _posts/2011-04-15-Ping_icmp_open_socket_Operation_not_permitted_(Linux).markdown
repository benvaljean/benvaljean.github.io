---
layout: post 
title: Ping: icmp open socket: Operation not permitted (Linux)
---

#### Problem

Unless you are root, ping shows the following error message:

    [user@host]$ ping 1.1.1.1
    ping: icmp open socket: Operation not permitted

#### Cause

On Linux (and other flavours) you have to be root to open up a socket.
The SUID bit must be set in the ping binary to allow it to open sockets.
This issue is common on jailing users as most disto\'s ping binary will
have this set by default.

    [user@host]# ls -la bin/ping
    -rwxr-xr-x 1 root root 41704 2011-04-06 15:13 bin/ping

#### Resolution

Set the SUID bit:

    [user@host]# sudo chmod u+s bin/ping 
    [user@host]# ls -la bin/ping
    -rwsr-xr-x 1 root root 41704 2011-04-06 15:13 bin/ping

[Category:Linux](Category:Linux "wikilink")
