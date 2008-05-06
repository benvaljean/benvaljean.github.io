---
layout: post 
title: Difference between Quick Format and a normal/long Format
---

### Similarities

Both types recreate the file system structures. Depending on the
platform this will include the file allocation table or the master file
table.

### Difference

The only noteworthy difference between the two is that a long format
will check every sector on the disk for errors.

### When to do a quick format

For workstations where you are installing an OS on a known-good drive,
or when rebuliding a PC on a drive that was previously used as a OS with
no hard drive problems. A quick format is also usually required when
using a third-party device to allocate space on the hard dribes - such
as a RAID array. Usually the long format will fail as the OS will not be
able to \'see\' every sector on the disk.

### When to do a long format

For workstations where the hard drive is brand new / has never been
previously used or when the hard drive is going to be used in a server
but NOT in a RAID array.
