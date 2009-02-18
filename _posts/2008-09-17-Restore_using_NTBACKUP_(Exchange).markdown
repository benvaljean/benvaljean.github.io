---
layout: post 
title: Restore using NTBACKUP (Exchange)
---

### Background

This page details the process of restoring a Microsoft Exchange database
using NTBACKUP and replaying the log files back into the database whilst
overcoming some common errors. The guide below already presumes the user
has some knowledge of Exchange and that the replacement server has been
rebuilt, and Exchange installed. The server must have the same service
pack update as the server where the database was originally hosted.

### The process

1.  Rename the mailbox store to match the name of the mailbox store on
    server whose database is being restored - even if it includes the
    hostname of the previous server. NTBackup identifies which store to
    restore to based on this string.
2.  From
    \[<http://technet.microsoft.com/en-us/library/aa995785(EXCHG.65>).aspx
    Exchange System Manager\], open properties of the information
    store(s) where a restore is being attempted and tick \'this database
    can be overwritten by a restore.\'
3.  In NTBackup, catalogue the BKF file and highlight Logs and mailbox
    store as a minimum. Only restore the public folder store if the
    previous server is dead or will never be booted whilst connected to
    the same forest/domain; otherwise public folder and GAL replication
    issues among others are likely to occur. Choose an empty temporary
    directory to work from and remember it.
4.  Choose the appropriate destination server but do not choose log file
    replay even if this is the last backup set - it is better to do it
    manually as there are no verbose-logging of it if it fails when it
    is performed by NTBackup.
5.  When the backup has finished check the temporary directory for a
    file - restore.env. If it is not present the restore will need to be
    retried as it is vital to restore the Exchange DB to the point just
    before it failed. - Retry the restore in the first instance and if
    an error occurs that prevents a decent restore.env file from being
    created or none at all see When Log file replay/hard recovery is not
    available.
6.  Copy all the log files available as they are without renaming the
    files to the same directory as the IS database files.
7.  Cd to the eseutil folder, c:\\\\program files\\\\exchsvr\\\\bin by
    default; and type **eseutil /cc \"path to temporary dir containing
    restore.env\"** This replays the transactions logs back into the
    database without checking the checkpoint file as it is likely to
    have been lost anyhow. If you receive a JET errBadLogVersion error
    see: [Error -514 JET errBadLogVersion when using
    Eseutil](Error_-514_JET_errBadLogVersion_when_using_Eseutil_(Exchange) "wikilink")
8.  The process normally takes minutes and if the readout states that
    there are no errors go on to the next step; else look at When Log
    file replay/hard recovery is not available.
9.  From Exchange System Manager go to the mailbox store and the
    mailboxes should all be seen. Right click a blank area and choose
    Run Clean-up agent. All the mailboxes should now have a red-cross on
    them as they are currently not associated/connected to a user
    account in AD. An Exchange mailbox must be connected to a user
    account before it can be opened. Right-click the mailbox and choose
    reconnect. If the following error appears: \"The operation cannot be
    performed because this mailbox was already connected to another user
    ID no: c1034ad6\" see Cannot reconnect mailboxes.
10. Once the mailbox is reconnected it can be opened as usual.

#### See Also

-   [Exchange 2003 Backup and Restore with
    NTBACKUP](http://www.msexchange.org/tutorials/Exchange-2003-Backup-Restore-NTBACKUP.html)
-   [Exchange 2007 restore using
    NTBackup](http://davehope.co.uk/Blog/exchange-2007-restore-ntbackup/)
-   [NTBACKUP caveat for Exchange and system state
    backups](http://searchexchange.techtarget.com/tip/0,289483,sid43_gci1138776,00.html?track=fg_ntbackup)
-   [Backup Operation Fails When You Back Up Exchange Server 2003
    Databases and System State Information at the Same
    Time](http://support.microsoft.com/default.aspx?scid=kb;en-us;820272)

### When Log file replay/hard recovery is not available

Depending on how log file replay has failed the simplest possible method
to allow it to work is to truncate the logs:

1.  Initially delete E00.tmp if it exists and try again - this is the
    name of the log that Exchange is/was currently writing to and is
    likley to be corrupt in this scenario.
2.  Delete E00.log and try again - this was the last log that Exchange
    finished writing to.
3.  Delete the next 10 most recent logs and try again. In some scenarios
    it is required to rename the latest log file to E00.log .

If this still fails try the following:

**Eseutil /ml <log file>** verifies a log file and can give info that
can be googled that when applied could allow a log file replay to
partially work. **eseutil /k <log file>** as above but checks headers
only

##### Repairing log files

Log file repair should only be attempted if all of the above has been
tried. If a repair of the log files is attempted it can make the
scenario worse. - To save having to do a re-restore perform an offline
backup - copy the files elsewhere. Never try this on a live server
without performing an offline backup. If existing transaction log files
are not found by Eseutil when it tries to run recovery or they are
cannot be recovered, it will create a new transaction log file, and try
to attach the database to it. If the database is Inconsistent or in
Dirty Shutdown state, the database will not be made startable. If the
database is in a consistent state, it will be attached and then detached
from the new log file. - In either of these cases you risk making
changes to the database or adding log files to the server that will
result in the database becoming unstartable or that will confuse further
recovery troubleshooting.

Type: **eseutil /r E00 /i**

If log file reapir states it was a success this does not necessarily
mean there was a success. Recovery succeeds whenever all available
transaction log data that is currently available has been applied to the
database files. Recovery success says nothing about whether the
available data was sufficient to restore the databases to consistency.

##### Repairing the database

The last attempt to enable log file replay to work is to perform a /p on
the database - repair mode. DBs who have a /p applied should never be
placed into production for an extended period of time. Normally a /p
gives no more then restoring a DB and not attempting log file replay
however it can allow log file replay to work - but only in a very
tentative state. Always move mailboxes to another store even if this
works.

Type: **eseutil /p priv1.edb**

If a streaming miss-match occurs try again with the /i switch also.

After this you must run **eseutil /d** to defrag the DB followed by
**isinteg -fix** . Only if you intend to use the repaired database for
salvage only can you skip these extra steps. Skipping them means that
you may salvage less data than if you completed them, but it can also
mean saving several hours of recovery time.

#### See Also

-   \[<http://technet.microsoft.com/en-us/library/bb218118(EXCHG.80>).aspx
    Database engine is unable to replay log file sequence due to fatal
    error\]
-   [Eseutil
    guide](http://www.computerperformance.co.uk/exchange2007/exchange2007_eseutil.htm)

### Cannot reconnect mailboxes

When reconnecting mailboxes from a recently restored database the
orphaned mailbox can still be associated with the original user account
even though it appears to be disconnected. To resolve this: Use [ADSI
Edit](http://www.computerperformance.co.uk/w2k3/utilities/adsi_edit.htm)
to change the `legacyExchangeDN` attribute for the active user for the
mailbox you wish to reconnect as System manager look for users with this
attribute before reconnecting. When disconnecting a mailbox from a user
this attribute would normally cleared and would not be an issue. I would
recommend adding a suffix to the end of the attribute rather than
removing it. Normally, changing this attribute would cause email for the
user to stop working until reverted.

If this fails to work remove the Exchange attributes for the user: Right
click the user in AD, choose Exchange tasks followed by Remove Exchange
attributes. The mailbox can now be reconnected.

#### See Also

-   [ADSI
    FAQ](http://itknowledgeexchange.techtarget.com/itanswers/tag/adsiedit/)
-   [ADSI Edit
    guide](http://www.computerperformance.co.uk/w2k3/utilities/adsi_edit.htm)
-   [AD Explorer: Alternative to ADSI
    edit](http://exchangepedia.com/blog/2007/11/ad-explorer-better-adsiedit-than.html)

[Category:Exchange](Category:Exchange "wikilink")
