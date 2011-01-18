---
layout: post 
title: Increase simultaneous/concurrent TCP connections (Linux)
---

#### Symptom

/var/log/messages states that packets are being dropped due to the limit
being reached. The default limit is 65536 connections.

#### Cause

Unless you are using the Linux box as a router then an application is
probably misbehaving. The limit is placed to ensure that bad
applications cannot cause havok on networks, investigate hy the
application is doing this first.

-   The current limit can be viewed by `cat`ing one of these files, the
    exact file can vary based on distro:

<!-- -->

    /proc/sys/net/netfilter/nf_conntrack_max
    /proc/sys/net/ipv4/netfilter/ip_conntrack_max

If the file cannot be found try:

    find /proc -name '*conntrack_max*'

#### Resolution

If the connections are legitamate the limit can be increased by echoing
the number to the `conntrack_max` file as shown below:

    cat 250000 >/proc/sys/net/netfilter/nf_conntrack_max

To make the changes permanent edit the /etc/sysctl.conf file and edit or
add a line based on the location of the /proc file in your distro:

    net.netfilter.nf_conntrack_max = 250000

[Category:Linux](Category:Linux "wikilink")
