---
layout: post 
title: Standby Continuous Replication (Exchange 2007)
---

Exchange Standby Continuous Replication (SCR) is replication in a manual
failover scenario as opposed to Clustered Continuous Replication (CCR)
which incorporates clustering for automatic/hot failover.

    --------------                --------------
    |SCR Source  | -------------> |SCR Target  |
    --------------  T Log Shipped --------------

### Show SCR targets

    Get-StorageGroup "SERVER\\SGName" | fl

### Backup/Restore with SCR

SCR target copies cannot be backed up. An SCR target\'s database headers
will be updated and the log files will be truncated when a supported
backup is taken against the SCR source storage group.

When an SCR source database is replaced with an earlier version of the
database, you must suspend and then resume continuous replication for
the storage group using Suspend-StorageGroupCopy and
Resume-StorageGroupCopy respectively. This process is needed to update
the Microsoft Exchange Replication Service with the correct log
generation information. If continuous replication is not suspended and
resumed, the Replication Service will have outdated log generation
information and will stop replicating log files.

### Log file replication and truncating with SCR

Normally in a Exchange environment Tlogs are not deleted until they have
been backed up and replayed into the copy of the database. This is not
the case with SCR; it allows Tlogs to be deleted at the SCR source as
soon as they are inspected by all SCR target computers. This is due to a
setting called **ReplayLagTime** which states how long a SCR target
should wait until it replays it into its database, default is 1 day.
However, the replay will still lag behind by 50 transaction logs - a
hard-coded limit enforced by SCR that cannot be changed. Another setting
**TruncationLagTime** defines the time Ex should wait to delete/truncate
a log file \'after\' it has been replayed, default is 0. A Tlog on the
SCR target gets deleted after it has been deleted on the source and
after ReplayLagTime + TruncationLagTime.

Once setup using the Enable-StorageGroupCopy command, the ReplayLagTime
and TruncationLagTime cannot be changed without disabling and
re-enabling that SCR relationship for the Storage Group.

#### Ascertain the ReplayLagTime and TruncationLagTime values

    $sg = Get-StorageGroup "MyServer\\MyStorageGroupName"
    $sg.StandbyMachines

#### Alter values

Disable SCR if already enabled:

    Disable-StorageGroupCopy "Storage Group Name" -StandbyMachine "SCR Target Server"

Deleting files on the replica is not required - reseeding is not done.

Enable SCR with new values:

    Enable-StorageGroupCopy "Storage Group Name" -StandbyMachine "SCR Target Server" -ReplayLagTime 1.00:00:00 -TruncationLagTime 2.00:00:00

Get status:

    Get-StorageGroupCopyStatus "SG Name" -StandbyMachine "SCR Target Server"

From:
<http://exchangepedia.com/blog/2007/12/standby-continuous-replication-replay.html>

### Optimise networking settings

Reg vales should be changed to optimise SCR, use [Exchange 2007 Mailbox
Server Role Storage Requirements
Calculator](http://go.microsoft.com/fwlink/?LinkID=84202)

Chimney should also be disabled:

    netsh int ip set chimney DISABLED

From <http://technet.microsoft.com/en-us/library/cc164368.aspx>

### Setting up SCR

Setting up SCR when creating a new Storage Group:

    [PS] C:\\Documents and Settings\\rradmin>New-StorageGroup -Server EX1 -Name "StorageGroup1" -LogFolderPath "g:\\ExchangeMailboxDBTransactionLogs2" -SystemFolderPath "g:\\ExchangeMailboxDBTransactionLogs2" -StandbyMachine ex2.companyabc.local -ReplayLagTime 0.1:0:0 -TruncationLagTime 1.0:0:0

    Name                      Server            Replicated        Recovery
    ----                      ------            ----------        --------
    StorageGroup1             EX1         None              False

In contrast to [SQL
mirroring](Setting_up_Mirroring_in_SQL_Server_(MSSQL) "wikilink"), no
data needs to be created on the SCR Target before SCR is setup. The
database, system and transaction log paths must be pre-created on the
SCR Target and they must be identical to those used on the SCR Source.
Log files are shipped across and the database is created after the 50
log file + ReplayLagTime delay.

### Verify Replication status

    Get-StorageGroupCopyStatus EX1\\StorageGroup1 -Standbymachine EX2|fl

### Failover Testing

-   Dismount Active DB first.

Set the Mirror copy to be active:

    [PS] C:\\Documents and Settings\\user>Restore-StorageGroupCopy EX1\\Storag
    eGroup1 -StandbyMachine EX2
    WARNING: Failed to copy remaining log files (through Exx.log) during
    Restore-StorageGroupCopy operation for storage group copy (StorageGroup1).
    Failure reason: Microsoft Exchange Replication service RPC failed : The storage
     group does not have any passive copies configured..


    Identity               : EX1\\StorageGroup1
    LastLogGenerated       : 1235
    LastLogInspected       : 1235
    LatestAvailableLogTime : 09/04/2009 15:03:15
    LastInspectedLogTime   : 09/04/2009 15:03:15
    IsValid                : True
    ObjectState            : Unchanged

    [PS] C:\\Documents and Settings\\rradmin>Restore-StorageGroupCopy EX1\\Storag
    eGroup1 -StandbyMachine EX2 -force
    WARNING: Performing a Restore-StorageGroupCopy operation on storage group
    'StorageGroup1' with the Force option. Data loss is expected for this storage
    group.

This warning is expected as we do not have a cluster; there is no way
for it to grab extra log files if the DB is dismounted, and it has to be
dismounted for the cmdlet to work.

SCR does not create DBs as far as AD/Exchange is aware of - just the DB
files themselves. Create some vanilla SG and DB \'entries\' on Exchange
and point them to the new files that were being updated via Exchange CR:

    [PS] C:\\Documents and Settings\\rradmin>Move-DatabasePath EX2\\StorageGroup1P
    ort\\MailboxDB1Port -EdbFilePath "d:\\ExchangeMailboxDatabase2\\MailboxDB.edb" -Con
    figurationOnly

    Confirm
    This operation will skip the safety check and make the change to the Active
    Directory directory service directly. Do you want to continue?
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):y

    Confirm
    Are you sure you want to perform this action?
    Moving database path "EX2\\StorageGroup1Port\\MailboxDB1Port".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):Y

Now mount.

According to Microsoft it should auto replay the Tlogs into the DB, but
in practice this does not happen, to replay them, cd to the dir that has
the Tlogs in it and run eseutil:

    G:\\ExchangeMailboxDBTransactionLogs2>c:\\ExchangeServer\\bin\\eseutil /r E02 /A

    Extensible Storage Engine Utilities for Microsoft(R) Exchange Server
    Version 08.01
    Copyright (C) Microsoft Corporation. All Rights Reserved.

    Initiating RECOVERY mode...
        Logfile base name: E02
                Log files: <current directory>
             System files: <current directory>

    Performing soft recovery...
                          Restore Status (% complete)

              0    10   20   30   40   50   60   70   80   90  100
              |----|----|----|----|----|----|----|----|----|----|
              ...................................................



    Operation completed successfully in 218.187 seconds.

E02 in the command refers to the log file prefix, adjust to match the
log file prefix of the Tlogs.

If it mounts ok the next step is to change the User properties in AD to
point to the new DB:

    [PS] C:\\Documents and Settings\\rradmin>Get-Mailbox -Database EX2\\StorageGroup1\\MailboxDB|where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}|Move-Mailbox -ConfigurationOnly -TargetDatabase EX2\\StorageGroup1Port\\MailboxDB1Port

Mailbox access should now be available. Outlook 2003 clients may need
their local outlook profiles altered to reflect the new server unless
the previous Ex server is active, in which case it will redirect
clients. Any AD replication lag will also delay users in being able to
access mailboxes.

### Manually reseeding the database

Upon finally resetting up SCR for production I discovered that despite
log files being shipped over OK, the database was not getting created.
To overcome this I had to manually reseed the SCR Target: First, suspend
SCR:

    Suspend-StorageGroupCopy -Identity "EX1\\StorageGroup1" -StandbyMachine ex2.companyabc.local

On the SCR Target perform reseed:

    [PS] C:\\Documents and Settingsuser>Update-StorageGroupCopy -Identity "EX1
    \\StorageGroup1" -StandbyMachine ex2.companyabc.local

    Confirm
    Continuous replication seeding found an obsolete checkpoint
    'G:\\ExchangeMailboxDBTransactionLogs\\E02.chk' file for storage group copy
    'StorageGroup1'. The checkpoint file will be deleted, and then the database
    will be seeded if you confirm now.
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):y
    WARNING: Replication for storage group 'EX1\\StorageGroup1' is still
    suspended. If needed, you can use the Resume-StorageGroupCopy cmdlet in the
    Exchange Management Shell to resume replication.
    Update-StorageGroupCopy : Seeding failed : Database seeding error: Log files al
    ready exist at 'G:\\ExchangeMailboxDBTransactionLogs'. They must be removed befo
    re storage group seeding or reseeding can be performed. The '-DeleteExistingFil
    es' switch can be used with the 'Update-StorageGroupCopy' task to accomplish th
    is.
    At line:1 char:24
    + Update-StorageGroupCopy  <<<< -Identity "EX1\\StorageGroup1" -StandbyMac
    hine ex2.companyabc.local
    [PS] C:\\Documents and Settings\\user>Update-StorageGroupCopy -Identity "EX1
    \\StorageGroup1" -StandbyMachine ex2.compnyabc.local -DeleteExistingFi
    les

    Confirm
    Continuous replication seeding found an obsolete checkpoint
    'G:\\ExchangeMailboxDBTransactionLogs\\E02.chk' file for storage group copy
    'StorageGroup1'. The checkpoint file will be deleted, and then the database
    will be seeded if you confirm now.
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):y

Then resume SCR from the SCR source:

    Resume-StorageGroupCopy "EX1\\StorageGroup1" -StandbyMachine ex2.companyabc.local

[Category:Exchange](Category:Exchange "wikilink") [Category:Disaster
Recovery](Category:Disaster_Recovery "wikilink")
