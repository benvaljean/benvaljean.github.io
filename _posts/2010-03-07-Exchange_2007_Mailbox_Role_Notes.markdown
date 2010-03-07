---
layout: post 
title: Exchange 2007 Mailbox Role Notes
---

See [Exchange 2007 Server Roles](Exchange_2007_Server_Roles "wikilink")

### List mailboxes on a server

    Get-Mailbox -Database "EX1\\MailboxDB"

### Setup Message Tracking

    Set-MailboxServer EX1 -MessageTrackingLogPath c:\\ExchangeUsageLogs\\MessageTracking
    Set-MailboxServer EX1 -MessageTrackingLogMaxAge "90.00:00:00"
    Set-MailboxServer EX1 -MessageTrackingLogMaxDirectorySize 1GB
    Set-MailboxServer EX1 -MessageTrackingLogMaxFileSize 10MB
    Set-MailboxServer EX1 -MessageTrackingLogSubjectLoggingEnabled $true
    Set-MailboxServer ex2 -MessageTrackingLogPath c:\\ExchangeUsageLogs\\MessageTracking
    Set-MailboxServer ex2 -MessageTrackingLogMaxAge "90.00:00:00"
    Set-MailboxServer ex2 -MessageTrackingLogMaxDirectorySize 1GB
    Set-MailboxServer ex2 -MessageTrackingLogMaxFileSize 10MB
    Set-MailboxServer ex2 -MessageTrackingLogSubjectLoggingEnabled $true

### Get Database settings

    Get-MailboxDatabase MailboxDB|fl

### Resource Mailboxes

New feature to Ex2007 are resource mailboxes, which can be used to book
rooms for instance. Their use is predominantly available to Outlook 2007
users only.

Change existing mailbox to room mailbox:

    Set-Mailbox "Conference Room 1" -Type Room

Setup auto accept:

    Set-MailboxCalendarSettings roomtest1 -AutomateProcessing AutoAccept

<http://help.outlook.com/en-us/140/dd569933(loband).aspx>

<http://msexchangeteam.com/archive/2007/05/14/438944.aspx>

### Mailbox quotas

Ascertain who is over their quota:

    get-MailboxStatistics | where {"IssueWarning","ProhibitSend","MailboxDisabled" -contains $_.StorageLimitStatus} | format-Table DisplayName,TotalItemSize

[Category:Exchange](Category:Exchange "wikilink")
