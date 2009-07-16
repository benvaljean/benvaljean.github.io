---
layout: post 
title: One or more users currently use a mailbox store on this server Error (Exchange 2003)
---

### Symptom

When trying to uninstall Exchange 2003 the following error can appear:

    One or more users currently use a mailbox store on this server

This can occur even if there are no mailboxes on the server, or even if
the mailbox stire itself is no longer present.

### Cause

In checking whether or not any mailboxes exist an AD lookup is
performed. If there is a user acc that has the Exchange Home Server ADSI
attribute (msExchHomeServerName) set to the Exchange server you wish to
uninstall the error above appears. The user acc may not even offically
have any Exchange attributes.

### Resolution

From a machine that has Exchange AD installed:

1.  Right click the Domain, choose find. On the Exchange tab ensure that
    \'Show only Exchange recipients **IS NOT TICKED**.
2.  Click Find.
3.  View \> Choose Columns, select \'Exchange Home Server\'. This lists
    data in the msExchHomeServerName attribute.
4.  Click the Exchange home Server column to sort and find the acc(s).
5.  If you do not need the user(s) delete them. If you do, navigate to
    the user using
    \[<http://technet.microsoft.com/en-us/library/bb124152(EXCHG.65>).aspx
    ADSI Edit\] or
    [<http://technet.microsoft.com/en-us/sysinternals/bb963907.aspx>](http://technet.microsoft.com/en-us/sysinternals/bb963907.aspx)
    and clear the msExchHomeServerName AD attribute.

### See Also

[The ADSI Edit
Utility](http://windowsitpro.com/article/articleid/19626/the-adsi-edit-utility.html)
\[<http://technet.microsoft.com/en-us/library/bb124152(EXCHG.65>).aspx
Using ADSI Edit to Edit Active Directory Attributes\]
