---
layout: post 
title: Recovering Active Directory
---

### Backup

Natively AD is backed up by backing up the \'System State\'. Pre-Windows
2008 this is achieved through
[NTBACKUP](http://www.microsoft.com/downloads/details.aspx?FamilyID=7da725e2-8b69-4c65-afa3-2a53107d54a7).
On Windows 2008 onwards it is achieved though \'Windows Backup\'.

The AD restore procedure involves building a new DC as the first DC in a
forest (organisation) and then performing an authoritative restore on
it. <font color=Red>The loss of a DC should always be recovered by
rebuilding the DC if there are other live DCs in the environment.</font>

### Disaster Recovery of Active Directory

If there are no DCs available for a domain: Rebuild a DC as the first DC
in the domain or forest, whichever is appropriate. An authoritative AD
Restore must then be performed.

#### Authoritative AD Restore

##### Important Notes

-   An AD (system state) backup that is \>60 days old cannot be restored
    as the tombstone interval will have expired.
-   This should only be attempted in the event that \*ALL\* DCs are
    lost. If non-authoritative/authoritative restore is attempted in an
    existing forest major replication problems will occur.
-   Perform the restore process whilst NOT connected the to the network,
    and only reconnect when mentioned below.
-   No previous DCs should be connected to the network post this
    procedure.

1.  Restart DC in Directory Services Restore Mode
2.  Restore System State through NTBackup ensuring that network adapter
    details, drive letters, computer name and SYSVOL data locations are
    identical to the server that the system state backup was taken from.
3.  Once finished, again reboot into Directory Services Restore Mode and
    verify the following regkey:
    HKEY\_LOCAL\_MACHINE\\\\SYSTEM\\\\CurrentControlSet\\\\Services\\\\NTDSRestoreInProgress
    . If should be set to \"1\" despite the process having finished in
    reality. This key indicates to NTDS that the AD data is invalid due
    to it being out of date further to a restore and to instruct it to
    perform the required steps make it usable. It some scenarios it
    could be set to \"0\" but the primary requirement is that the key
    exists. If it does not then the restore has failed and must be
    re-attempted.
4.  Set the AD DB to be the authoritative for the forest:
    1.  Reboot into Directory Services Restore Mode
    2.  Start \> Run \> ntdsutil
    3.  authoritative restore <enter>
    4.  Restore database <enter>
5.  Reboot into normal and connect to the network and pray.

[Category:Windows](Category:Windows "wikilink") [Category:Disaster
Recovery](Category:Disaster_Recovery "wikilink")
