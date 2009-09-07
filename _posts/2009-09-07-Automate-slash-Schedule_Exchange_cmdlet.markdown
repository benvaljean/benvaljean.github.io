---
layout: post 
title: Automate/Schedule Exchange cmdlet
---

To automate the running of a [Microsoft Exchange
cmdlet](http://www.msexchange.org/articles-tutorials/exchange-server-2007/management-administration/user-administration-exchange-2007-powershell-cmdlets.html)
in Scheduled Tasks (for instance) an additional parameter must be
supplied along with `-command` when calling `powershell` from within a
BAT file.

The syntax is:

    powershell -PSConsoleFile "C:\\ExchangeServer\\bin\\exshell.psc1" -command ". 'exchange-cmdlet-here'"

Replace c:\\\\exchangeserver with your Exchange Server path.

For example you may with to test your replication health and output it
to a text file for further processing:

    powershell -PSConsoleFile "C:\\ExchangeServer\\bin\\exshell.psc1" -command ". 'Test-ReplicationHealth'" >c:\\SCRStatus.txt

It is always recommended to save your command to a BAT file and have
scheduled tasks run this, instead of entering the command line as a
Scheduled Tasks.

[Category:Exchange](Category:Exchange "wikilink")
