---
layout: post 
title: Disk Partition alignment (Windows)
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

1\. Partition offset: Save the following as GetPartitionOffsets.vbs and
run it:

    'GetPartitionOffsets.vbs
    'By Joe Chang
    strComputer = "." 
    Set objWMIService = GetObject("winmgmts:\\\\" & strComputer & "\\root\\CIMV2") 
    Set colItems = objWMIService.ExecQuery( _
        "SELECT * FROM Win32_DiskPartition",,48) 
    'Wscript.Echo "-----------------------------------"
    Wscript.Echo "Win32_DiskPartition instance"
    For Each objItem in colItems 
        Wscript.Echo "DiskIndex: " & objItem.DiskIndex & "  -- Name: " & objItem.Name & "  --  StartingOffset: " & objItem.StartingOffset
    Next

Look for the offset of the first partition \'partition \#0\' of the
volume that needs to be aligned.

2\. Cluster size:\
Intall the [Windows Server 2003 resource
kit](http://www.microsoft.com/downloads/details.aspx?familyid=9d467a69-57ff-4ae7-96ee-b18c4790cffd)
Type the following and look for the bytes per cluster value:

    fsutil fsinfo ntfsinfo driveletter:

For the RAID stripe size, refer to your controller\'s documentation. For
HP, install the Array Configuration Utility, part of the Proliant
Support Pack.

### How to create partitions that are aligned

Do not create partitions using [Disk
Management](http://www.microsoft.com/technet/prodtechnol/windows2000serv/reskit/deploy/dgbj_sto_csmg.mspx).\
From the [Windows Server 2003 resource
kit](http://www.microsoft.com/downloads/details.aspx?familyid=9d467a69-57ff-4ae7-96ee-b18c4790cffd)
use the DiskPart tool:

    diskpart
    list disk
    select disk <DiskNumber>
    create partition primary align=<Offset_in_KB> size=<Size_in_MB>
    assign letter=<DriveLetter>
    format fs=<file-system> label=<"label"> unit=<FileAllocationUnitSize> nowait

### See Also

-   [Disk Partition alignment
    (Linux)](Disk_Partition_alignment_(Linux) "wikilink")
-   [Performance impact of disk
    misalignment](http://sqlblog.com/blogs/linchi_shea/archive/2007/02/01/performance-impact-of-disk-misalignment.aspx)
-   [Storage performance for SQL
    Server](http://sqlblog.com/blogs/joe_chang/archive/2008/03/04/storage-performance-for-sql-server.aspx)
-   [MS KB article stating partition alignment as a fix for slow
    performance](http://support.microsoft.com/default.aspx?scid=kb;EN-US;929491)

[Category:Windows](Category:Windows "wikilink")
