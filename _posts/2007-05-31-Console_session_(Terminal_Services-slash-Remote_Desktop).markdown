---
layout: post 
title: Console session (Terminal Services/Remote Desktop)
---

Windows Server 2003 allows remote connection to the console session of a
server resulting in 3 connections made available when connecting via
Terminal services / remote desktop. In Windows 2000 Server terminal
services could not connect to the console session.

#### Benefit

It is always possible to connect to the console session even if the
following message appears on the standard sessions: \"The terminal
server has exceeded the maximum number of allowed connections.\" Note:
Use Terminal Services Manager to log off un-used sessions remotely.

#### Remote Desktop Client Versions

To be able to connect to the console session Remote Desktop client V5.1
or higher is required. XP ships with V5.1 .

Windows Server 2003 ships with RDP client V5.2 which has an
auto-reconnect option as well as other new features. It can be
downloaded from:
<http://www.microsoft.com/downloads/details.aspx?FamilyID=a8255ffc-4b4a-40e7-a706-cde7e9b57e79&DisplayLang=en>
Unlike the previous version it can be installed from 95 and up -
although advanced features such as mapping local drives will not be
supported pre XP.

#### How to connect to the console session

To connect to the console session start the client from a command prompt
(or create a shortcut) or directly under Start Menu -\> Run with the
following command:

`  mstsc /console`

The server name can be selected as usual when the client starts.

mstsc is located in: %Windir%\\\\System32\\\\mstsc and the 5.2 download
installs in: %ProgramFiles%\\\\Remote Desktop\\\\mstsc

The RDP client V5.2 installer does not update the 5.1 client and the new
directory is not added to %path% .

#### Implementation Considerations

Be warned that if a user is already logged on to the console session
different from the user trying to logon they will be force logged off
and any unsaved data will be lost. This is in contrast to logging on
with the same account where the session will be resumed for when it was
last used and anybody currently using the session - whether physically
at the terminal or via RDP - will be disconnected.

#### Managing Remote Connections

Once logged on to the console (or any other session) you can right click
on the taskbar and select \"Task Manager\". When in a session you get a
tab here called \"Users\". You can now choose to log off or disconnect
the other sessions that might have become orphan or are still being open
on a computer at work or something. You could connect to those sessions
as well to see if any files are open in them first or even remote
control them to interact with them.

You will notice in the terminal service manager that the console session
always have sessionid = 0. You still see both a remote connection with
sessionid = 0 and a \"console\" object as well. The \"console object\"
will always be there as well but to identify which session is connected
to it look for the one with sessionid = 0.

#### Session Shadowing

Other cool stuff is that you can remote control other sessions on the
computer to interact with them (right click on them -\> Remote Control).
I don\'t remember if that was possible in Windows 2000. In other words
the \"connect\" option takes the session directly, while the \"Remote
Control\" option will interact with the session, two at the same time.

By default the current user of the session gets a message telling
him/her that another connection is incoming for Remote Control. You can
select Yes or No to this. If you are the only one using the server then
you can disable this message under policies but on the other hand you
could just \"connect\" instead of remote control the sessions in that
case.

#### Contrast to XP

This concept of console session is different compared to the remote
desktop service built-in in Windows XP. In Windows XP you only have one
session which is the console session and that\'s the one you always
connect to. With Windows 2003 in Remote Administration mode you have the
console session and two other \"standard\" sessions as in Windows 2000
Server, where the console never is the default one unless you use one of
the methods mentioned above.

### See Also

-   [Windows Server 2003 Terminal
    Services](http://www.microsoft.com/windowsserver2003/technologies/terminalservices/default.mspx)
-   [Remote Desktop Connection Client for
    Windows](http://support.microsoft.com/kb/925876)

[Category:Windows](Category:Windows "wikilink")
