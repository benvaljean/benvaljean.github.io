---
layout: post 
title: Exchange 2007 CAS/Hub Transport Notes
---

See [Exchange 2007 Server Roles](Exchange_2007_Server_Roles "wikilink")

### AntiSpam Mail-flow

<http://wiki.jobsgopublic.local/images/Exchange2007AntiSpamMailFlow.gif>

1.  A SMTP server connects to Exchange 2007 and initiates an SMTP
    session.
2.  Connection filtering
3.  Sender filtering
4.  Recipient filtering
5.  Sender ID filtering (not implemented at JGP)
6.  Content filtering
7.  Attachment filtering
8.  Antivirus scanning (not implemented at JGP)

### Logging

Turn on SMTP protocol logging:
<http://exchangepedia.com/blog/2007/05/exchange-server-2007-logging-smtp.html>

Details the 15 logs on Ex2007:
<http://exchangepedia.com/blog/2007/11/exchange-server-2007-how-many-logs-hath.html>

### Whitelist

Install anti-spam agents on hub transport server if not using edge trans
server:

<http://www.exchangepedia.com/blog/2006/09/how-to-install-anti-spam-agents-on-hub.html>

Whitelist a sender:

    Set-ContentFilterConfig -BypassedSenders foo@somedomain.com,foo2@somedomain.com

Whitelist a sending domain:

    Set-ContentFilterConfig -BypassedSenderDomains somedomain.com,someotherdomain.com

</pre>

These parameters do not append the list - previous addresses must be
entered. </strike> It is preferable to use a GUI to edit the whitelist:
<http://gsexdev.blogspot.com/2009/02/content-filtering-system-whitelist-gui.html>

### Recipient whitelist

Bypass anti-spam checking for certain recipients:

    Set-ContentFilterConfig -BypassedRecipients sales@yourdomain.com,info@yourdomain.com

<http://exchangepedia.com/blog/2007/01/exchange-2007-content-filter-whitelist.html>

### Anti spam status check

    Get-AgentLog -StartDate "23/02/2009" | group action | ft name,count -Autosize

### Allow Specifc IP(s) to relay

<http://technet.microsoft.com/en-us/library/bb232021.aspx>

### Set the Anti-spam Junk Threshold

There is nowhere in the GUI to set this.

    Set-OrganizationConfig -SCLJunkThreshold 6

### Enable auto update Anti-spam

Enable-AntispamUpdates -SpamSignatureUpdatesEnabled \$true -UpdateMode
Automatic

### Get/Change Transport role server config

Including smtp log/pick up folder locations:

    Get-TransportServer ROSE|fl

For extended back-end info: (recommend piping to less)

    Get-TransportServer ROSE|fc

To change something:

    set-transportserver Ex1 -property "parameter"

Change log locations:

    Set-TransportServer ExHubTransport1 -SendProtocolLogPath "g:\\ExchangeUsageLogs\\SMTPSend"
    Set-TransportServer ExHubTransport1 -RoutingTableLogPath "g:\\exchangeusagelogs\\Routing"
    Set-TransportServer ExHubTransport1 -MessageTrackingLogPth "g:\\ExchangeUsageLogs\\MessageTracking"
    Set-TransportServer ExHubTransport1 -ConnectivityLogPath"g:\\ExchangeUsageLogs\\Connectivity"
    Set-TransportServer ExHubTransport1 -ConnctivityLogPath "g:\\ExchangeUsageLogs\\Connectivity"
    Set-TransportServer ExHubTransport1 -ReceiveProtocolLogPath "g:\\exchangeusagelogs\\SMTPReceive"

Setup rotating of logs:

    Set-TransportServer ExHubTransport1 -MessageTrackingLogMaxAge "90.00:00:00"
    Set-TransportServer ExHubTransport1 -MessageTrackingLogMaxDirectorySize "1024Mb"
    Set-TransportServer ExHubTransport1 -ReceiveProtocolLogMaxAge "90.00:00:00"
    Set-TransportServer ExHubTransport1 -ReceiveProtocolLogMaxDirectorySize 2048Mb
    Set-TransportServer ExHubTransport1 -SendProtocolLogMaxAge 90.00:00:00
    Set-TransportServer ExHubTransport1 -SendProtocolLogMaxDirectorySize 1024Mb
    Set-TransportServer ExHubTransport1 -RoutingTableLogMaxAge "7.00:00:00"
    Set-TransportServer ExHubTransport1 -RoutingTableLogMaxDirectorySize 250Mb

### Aggregate mailbox safe list into Exchange-side whitelist

This aggregates what has been set at the client-end into a non-viewable
whitelist at the Exchange-end.

    get-mailbox|update-safelist -type safesenders

This aggregates every mailbox in the Ex org. To do a particular mailbox
use the `-identity mailboxalias` parameter. To script it:

    @echo off
    :: Aggregates the safe lists / white list in an individual's mailbox at the Exchange relay level
    :: http://technet.microsoft.com/en-us/library/aa998280.aspx
    C:\\WINDOWS\\system32\\windowspowershell\\v1.0\\powershell.exe -PSConsoleFile "C:\\ExchangeServerBinaries\\bin\\exshell.psc1" -command "get-mailbox|update-safelist -type safesenders"

[Category:Internal IT](Category:Internal_IT "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
