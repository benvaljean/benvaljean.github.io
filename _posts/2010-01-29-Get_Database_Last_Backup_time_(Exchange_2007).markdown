---
layout: post 
title: Get Database Last Backup time (Exchange 2007)
---

Through the use of the
[EMS](http://exchangepedia.com/blog/stuff/ExQuick.htm) the exact time of
the last backup of the Exchange backups can be viewed.

#### View last Full / Incremental / Differential / Copy backup of all Exchange databases in an Organisation

From EMS:

    [PS] C:\\>get-mailboxdatabase -Status |fl Name,Server,*backup*,Mounted

    Name                           : MailboxDB
    Server                         : EX1
    BackupInProgress               : False
    SnapshotLastFullBackup         : False
    SnapshotLastIncrementalBackup  :
    SnapshotLastDifferentialBackup :
    SnapshotLastCopyBackup         :
    LastFullBackup                 : 28/01/2010 21:00:07
    LastIncrementalBackup          :
    LastDifferentialBackup         :
    LastCopyBackup                 :
    RetainDeletedItemsUntilBackup  : False
    Mounted                        : True

    Name                           : SpamQandCatchAll
    Server                         : EX1
    BackupInProgress               : False
    SnapshotLastFullBackup         : False
    SnapshotLastIncrementalBackup  :
    SnapshotLastDifferentialBackup :
    SnapshotLastCopyBackup         :
    LastFullBackup                 : 29/01/2010 04:00:10
    LastIncrementalBackup          :
    LastDifferentialBackup         :
    LastCopyBackup                 :
    RetainDeletedItemsUntilBackup  : False
    Mounted                        : True

    Name                           : MailboxDB
    Server                         : EX2
    BackupInProgress               : False
    SnapshotLastFullBackup         : False
    SnapshotLastIncrementalBackup  :
    SnapshotLastDifferentialBackup :
    SnapshotLastCopyBackup         :
    LastFullBackup                 : 28/01/2010 21:00:23
    LastIncrementalBackup          :
    LastDifferentialBackup         :
    LastCopyBackup                 :
    RetainDeletedItemsUntilBackup  : False
    Mounted                        : True

[Category:Exchange](Category:Exchange "wikilink")
