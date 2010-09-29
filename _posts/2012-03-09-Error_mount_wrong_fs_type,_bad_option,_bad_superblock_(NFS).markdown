---
layout: post 
title: Error: mount: wrong fs type, bad option, bad superblock (NFS)
---

When mounting a NFS share on Ubuntu
(and probably Debian) for the first time the following error can appear:

    benyg@host:/mnt$ sudo mount -t nfs 10.x.x.x:/vol/vol1/rrd /mnt/rrd
    mount: wrong fs type, bad option, bad superblock on 10.x.x.x:/vol/vol1/rrd,
           missing codepage or helper program, or other error
           (for several filesystems (e.g. nfs, cifs) you might
           need a /sbin/mount.<type> helper program)
           In some cases useful info is found in syslog - try
           dmesg | tail  or so

#### NFS Utilities

This usually occurs occurs because the nfs-common package needs to be
installed:

-   Debian / Ubuntu `sudo apt-get install nfs-common`
-   Redhat/CentOS/Fedora `sudo yum install nfs-common`
-   Mandriva `urpmi nfs-common`
-   Gentoo `emerge nfs-common`

<!-- -->

-   Depending on distro `nfs-utils` and `nfs-utils-lib` may also need to
    be installed.

#### Portmap

Ensure portmap is running:

    [benyg@host:~] $ rpcinfo -p
       program vers proto   port  service
        100000    4   tcp    111  portmapper
        100000    3   tcp    111  portmapper
        100000    2   tcp    111  portmapper
        100000    4   udp    111  portmapper
        100000    3   udp    111  portmapper
        100000    2   udp    111  portmapper
        100000    4     0    111  portmapper
        100000    3     0    111  portmapper
        100000    2     0    111  portmapper
        100024    1   udp  57055  status
        100024    1   tcp  51056  status

Output if it is not running:

    [benyg@host:~] $ rpcinfo -p
    rpcinfo: can't contact portmapper: RPC: Remote system error - No such file or directory

-   Install it through the `rpcbind` package and start it.

[Category:Linux](Category:Linux "wikilink")
