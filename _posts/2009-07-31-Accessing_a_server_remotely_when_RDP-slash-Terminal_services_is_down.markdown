---
layout: post 
title: Accessing a server remotely when RDP/Terminal services is down
---

If RDP/Terminal services is down it is impossible to access the server
using a GUI. Telnet is insecure and is disabled by default - as it
should be - and there is no native command-line remote-access facility
natively installed. There are many SSH servers for Windows available,
however these can only be installed if the server can be sucessfully
remotely managed of course. A tool from
[Sysinternals](http://www.sysinternals.com) called `psexec` can be used
to run `cmd` remotely, effectively giving telnet access to the server.

1.  Download
    [psexec](http://technet.microsoft.com/en-us/sysinternals/bb897553.aspx)
2.  Run the following command: `psexec \\\\hostname -u username cmd`

### See Also

[Performing functions via the command
line](Performing_functions_via_the_command_line_(Windows) "wikilink")

[Category:Windows](Category:Windows "wikilink")
