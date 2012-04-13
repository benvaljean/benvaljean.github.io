---
layout: post 
title: Error: mount: wrong fs type
---

Benjamin Goodacre,f1\@goodacre.name,When mounting a NFS share on Ubuntu
(and probably Debian) for the first time the following error can appear:

    benyg@host:/mnt$ sudo mount -t nfs 10.x.x.x:/vol/vol1/rrd /mnt
    mount: wrong fs type, bad option, bad superblock on 10.x.x.x:/vol/vol1/rrd,
           missing codepage or helper program, or other error
           (for several filesystems (e.g. nfs, cifs) you might
           need a /sbin/mount.<type> helper program)
           In some cases useful info is found in syslog - try
           dmesg | tail  or so

This usually occurs occurs because the nfs-common package needs to be
installed:

-   Debian / Ubuntu `sudo apt-get install nfs-common`
-   Redhat/CentOS/Fedora `sudo yum install nfs-common`
-   Mandriva `urpmi nfs-common`
-   Gentoo `emerge nfs-common`

The NFS export can now be mounted:

    sudo mount -t nfs 10.x.x.x:/vol/vol1/rrd /mnt

Ensure that the mountpoint is an empty folder that already exists.

[Category:Linux](Category:Linux "wikilink")
