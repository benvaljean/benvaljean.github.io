---
layout: post 
title: System writer is not found in the backup Error (Windows Server Backup)
---

### Symptoms

When attempting to perform a system state backup using Windows Server
Backup in Server 2008 the following error can occur:

    C:\\Users\\administrator>wbadmin start systemstatebackup -backuptarget:g:
    wbadmin 1.0 - Backup command-line tool
    (C) Copyright 2004 Microsoft Corp.

    Starting System State Backup [21/04/2009 11:04]
    Retrieving volume information...

    This would backup the system state from volume(s) Local Disk(C:) to g:.
    Do you want to start the backup operation?
    [Y] Yes [N] No y

    Creating the shadow copy of volumes requested for backup.

    System writer is not found in the backup.

Other symptoms can include the following enter in the event log:

    Log Name:      Application
    Source:        Microsoft-Windows-CAPI2
    Date:          21/04/2009 06:00:02
    Event ID:      513
    Task Category: None
    Level:         Error
    Keywords:      Classic
    User:          N/A
    Computer:      DC2.company.local
    Description:
    Cryptographic Services failed while processing the OnIdentity() call in the System Writer Object.

    Details:
    AddCoreCsiFiles : BeginFileEnumeration() failed.

    System Error:
    Access is denied.

### Causes

Any of the following:

1.  The cryptographic service is failing, a dependancy of the VSS System
    Writer entry which Windows Server Backup uses to backup the data. If
    this entry is missing the data cannot be read.
2.  Incorrect permissions on or within: %windir%\\\\winsxs\\\\filemaps

### Resolution

1.  Issues with cryptographic can onrmally be resolved by restarting the
    service. If this does not resolve the issue look for entries in the
    event log when the service was restarted.
2.  The correct permissions for %windir%\\\\winsxs\\\\filemaps are:

-   Local administrators, or Domain administrators if a DC: Owner,
    Read&exec, List folder, Read
-   SYSTEM: Permissions as above excluding Owner
-   Local Users, or Domain Users (may not be required): As above
-   TrustedInstaller: Full Control
