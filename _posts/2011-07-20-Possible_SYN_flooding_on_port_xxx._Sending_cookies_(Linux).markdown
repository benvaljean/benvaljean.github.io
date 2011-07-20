---
layout: post 
title: Possible SYN flooding on port xxx. Sending cookies (Linux)
---

#### Symptom

`dmesg` shows that possible SYN flooding is occurring:

    $ dmesg
    .......
    possible SYN flooding on port xxx. Sending cookies.
    possible SYN flooding on port xxx. Sending cookies.
    possible SYN flooding on port yyy. Sending cookies.
    possible SYN flooding on port yyy. Sending cookies.
    possible SYN flooding on port xxx. Sending cookies.
    possible SYN flooding on port xxx. Sending cookies.
    possible SYN flooding on port xxx. Sending cookies.

#### Cause

-   This could be a form of DOS attack on the box.
-   It is likely to be TCP backlog queue maximum size has been reached.
    To ascertain the current maximum size:

<!-- -->

    $ cat /proc/sys/net/ipv4/tcp_max_syn_backlog 
    1024

#### Resolution

Adjust the size, `4096` is recommended unless the box has a minute
amount of memory in modern standards (\<1Gb).

    # echo "4096" >/proc/sys/net/ipv4/tcp_max_syn_backlog

-   Check `dmesg` to see if the problem reoccurs.

#### See Also

[tcp\_max\_syn\_backlog \|
LinuxInsight](http://www.linuxinsight.com/proc_sys_net_ipv4_tcp_max_syn_backlog.html)

[Category:Linux](Category:Linux "wikilink")
