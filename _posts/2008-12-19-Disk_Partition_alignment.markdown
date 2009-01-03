---
layout: post 
title: Disk Partition alignment
---

Not finished

Disk partition alignment involves setting the partition offset of the first partition on a logical or physical hard-drive whilst taking into account the intended cluster size and any RAID striping of the volume. Aligning a partition correctly can have significant performance gains. [http://sqlblog.com/blogs/linchi_shea/archive/2007/02/01/performance-impact-of-disk-misalignment.aspx]

==Rules for aligning==
Both of following calculations must produce integers in order for the first partition (and therefore all subsequent partitions) to be correctly aligned:
#Partition_offset divided by Stripe_size
#Stripe_size divided by Cluster_size

For example a partition with offset of 64k, cluster size 64k and RAID stripe size of 64k (if applicable) will be correctly aligned. These settings will work best with disks that will contain databases.
==How to ascertain these values==
===On Windows===
1. Partition offset:
Save the following as GetPartitionOffsets.vbs and run it:
<pre>
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
</pre>
Look for the offset of the first partition 'partition #0' of the volume you wish to align.

2. Cluster size:<br>
Intall the [http://www.microsoft.com/downloads/details.aspx?familyid=9d467a69-57ff-4ae7-96ee-b18c4790cffd Windows Server 2003 resource kit]
Type the following and look for the bytes per cluster value:
<pre>fsutil fsinfo ntfsinfo driveletter:</pre>

===On Linux===
1. Partition offset:<br>
For SCSI:
<pre>fdisk -l /dev/sd*</pre>
For IDE:
<pre>fdisk -l /dev/hd*</pre>

Look for the 'Start' value for the partition you wish to align. The values shown are in bytes, for instance 64k = 65536.

2. Cluster size / File Allocation Unit size:<br>
As root, type the following:
<pre>/sbin/dumpe2fs /dev/hda1 | grep 'Block size'</pre>  Replace /dev/hda1 as applicable


For the RAID stripe size, refer to your controller's documentation. For HP, install the Array Configuration Utility, part of the Proliant Support Pack.
==How to create partitions that are aligned==
===On Windows===
Do not create partitions using [http://www.microsoft.com/technet/prodtechnol/windows2000serv/reskit/deploy/dgbj_sto_csmg.mspx Disk Management].<br>

From the [http://www.microsoft.com/downloads/details.aspx?familyid=9d467a69-57ff-4ae7-96ee-b18c4790cffd Windows Server 2003 resource kit] use the DiskPart tool:
<pre>
diskpart
list disk
select disk <DiskNumber>
create partition primary align=<Offset_in_KB> size=<Size_in_MB>
assign letter=<DriveLetter>
format fs=<file-system> label=<"label"> unit=<FileAllocationUnitSize> nowait
</pre>
===On Linux===
Use parted:
<pre>
parted /dev/hda1
mkpart primary ext3 1024 2048


==See Also==
[http://sqlblog.com/blogs/joe_chang/archive/2008/03/04/storage-performance-for-sql-server.aspx Storage performance for SQL Server]
