---
layout: post 
title: Get Last Logon Time
---

Benjamin Goodacre,f1\@goodacre.name,This feature was removed from the
Exchange 2007 UI.

From the [Exchange Management
shell](http://technet.microsoft.com/en-us/library/bb123778.aspx):

    Get-MailboxStatistics | Select-Object DisplayName, LastLogonTime, LastLogOffTime | Format-Table

The item count and mailbox size can also be obtained:

    Get-MailboxStatistics | Select-Object DisplayName, ItemCount, TotalItemSize | Format-Table
