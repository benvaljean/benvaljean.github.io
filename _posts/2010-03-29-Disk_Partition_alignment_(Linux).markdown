---
layout: post 
title: Disk Partition alignment (Linux)
---

Disk partition alignment involves setting the partition offset of the
first partition on a logical or physical hard-drive whilst taking into
account the intended cluster size and any RAID striping of the volume.
Aligning a partition correctly can have significant performance gains.

### Rules for aligning

Both of following calculations must produce integers in order for the
first partition on a disk (and therefore all subsequent partitions) to
be correctly aligned:

1.  Partition\_offset divided by Stripe\_size
2.  Stripe\_size divided by Cluster\_size

For example a partition with offset of 64k, cluster size 64k and RAID
stripe size of 64k (if applicable) will be correctly aligned. These
settings will work best with disks that will contain databases. - The
performance degradation of unaligned partition occurs during intensive
I/O workloads rather than on those with low to moderate I/O activity.

### How to ascertain these values

1\. Partition offset:\
For SCSI:

    fdisk -lu /dev/sd<x>

For IDE:

    fdisk -lu /dev/hd<x>

where <x> is the device suffix.

Look for the \'Start\' value for the partition that needs to be aligned.
The values shown are in sectors, not cylinders.

2\. Cluster size / File Allocation Unit size:\
As root, type the following:

    /sbin/dumpe2fs /dev/hda1 | grep 'Block size'

Replace /dev/hda1 as applicable

For the RAID stripe size, refer to your controller\'s documentation. For
HP, install the Array Configuration Utility, part of the Proliant
Support Pack.

### How to create partitions that are aligned

Use fdisk: \'replace /dev/hda1 as applicable\'

-   `fdisk /dev/hda1`
-   `n` create a new partition
-   `p` create a primary partition
-   `l` create partition number 1
-   Select the defaults to use the whole disk or specify your required
    size.
-   `t` set the partitions system ID as appropriate
-   `x` go into expert mode
-   `b` adjust the starting block number
-   `1` to choose the first partition
-   Type in the offset in sectors. For example a 64k RAID stripe size
    and a 64k cluster size type in `64`.

### See Also

-   [Disk Partition alignment
    (Windows)](Disk_Partition_alignment_(Windows) "wikilink")
-   [Performance impact of disk
    misalignment](http://sqlblog.com/blogs/linchi_shea/archive/2007/02/01/performance-impact-of-disk-misalignment.aspx)
-   [Storage performance for SQL
    Server](http://sqlblog.com/blogs/joe_chang/archive/2008/03/04/storage-performance-for-sql-server.aspx)
-   [MS KB article stating partition alignment as a fix for slow
    performance](http://support.microsoft.com/default.aspx?scid=kb;EN-US;929491)

[Category:Linux](Category:Linux "wikilink")
