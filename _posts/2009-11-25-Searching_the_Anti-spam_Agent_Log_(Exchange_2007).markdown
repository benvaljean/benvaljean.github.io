---
layout: post 
title: Searching the Anti-spam Agent Log (Exchange 2007)
---

### Using the DOS shell

The easiest way is to cd to the dir where the anti-spam agent is
located: (Exchange install folder)\\\\TransportRoles\\\\Logs\\\\AgentLog
and use find to search for whatever string you require, whether it be IP
or smtp address.

To search within all files in the current dir for \"example\@jgp.co.uk\"

    C:\\ExchangeServer\\TransportRoles\\Logs\\AgentLog>find "example@address.com" *

The second parameter states the files that should be searched, the
asterisk referring to all file in the current dir.

### Using Exchange cmdlets

Using the
[EMS](http://blogs.msdn.com/exchangefaqs/archive/2008/01/23/exchange-management-shell.aspx):

To filter the log to show messages to a particular recipient:

    Get-AgentLog -StartDate "4/16/2007" -EndDate "4/17/2007" | where {$_.recipients -like "foo@yourdomain.com"}

To search for messages from a particular sender:

    Get-AgentLog -StartDate "4/16/2007" -EndDate "4/17/2007" | where {$_.P1FromAddress -like "aqe@easymoney2u.com" -or $_.P2FromAddresses -like "aqe@easymoney2u.com"}

To search for messages from a particular domain:

    Get-AgentLog -StartDate "4/16/2007" -EndDate "4/17/2007" | where {$_.P1FromAddress -like "*somedomain.com" -or $_.P2FromAddress -like "*somedomain.com"}

To filter by the anti-spam agent that acted on a message, e.g.
Connection Filtering Agent:

    Get-AgentLog -StartDate "4/15/2007" -EndDate "4/17/2007" | where {$_.Agent -eq "Connection Filtering Agent"}

Similarly, you can filter by other agents that write to the agent logs:

-   Content Filter Agent
-   SenderID agent
-   Sender Filter agent
-   Recipient Filter agent
-   Edge Rules agent

To filter agent logs by the sending host\'s IP address, use the
following command:

    Get-AgentLog -StartDate "4/15/2007" -EndDate "4/17/2007" | where {$_.IPAddress -eq "72.46.133.113"}

To fliter by the criteria that blocked the message, in the example RBL /
BlockListProvider:

    Get-AgentLog -StartDate "4/15/2007" -EndDate "4/17/2007" | where {$_.Reason -eq "BlockListProvider"}

[Category:Exchange](Category:Exchange "wikilink")
