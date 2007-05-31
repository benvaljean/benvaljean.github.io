---
layout: post 
title: Console session (Terminal Services/Remote Desktop)
---

With Windows 2003 you can now connect to the console session of a server
meaning you actually have 3 connections available when running in
\"Remote Administration\" mode. This was not possible with Windows 2000.

You can always connect to the console session even if you get the
following message on the standard sessions: \"The terminal server has
exceeded the maximum number of allowed connections.\" Note: Use Terminal
Services Manager to log off un-used sessions remotely.

To be able to connect to the console session you need a Remote Desktop
client using the RDP protocol 5.1 or higher. The one with Windows XP is
5.1 and works fine. The one from Windows 2000 does not work. It does not
support a console option.

A new client for 2003 exists as well that uses RDP 5.2 (it has a
re-connect option if the connection is dropped and some other stuff):
<http://www.microsoft.com/downloads/details.aspx?FamilyID=a8255ffc-4b4a-40e7-a706-cde7e9b57e79&DisplayLang=en>
Unlike the previous version it can be installed from 95 and up -
although advanced features such as mapping local drives will not be
supported pre XP.

To connect to the console session you start the client from a command
prompt (or create a shortcut) or directly under Start Menu -\> Run with
the following command:

`  mstsc /console`

The server name can be selected as usual when the client starts.

mstsc is located in: \"%Windows%\\\\System32\\\\mstsc\" and the 5.2
download installs in: \"%ProgramFiles%\\\\Remote Desktop\\\\mstsc\"

If the 5.2 dir is not added to the \"PATH\" variable the one in system32
will be run by default the default mstsc client is not upgraded.

The \"Remote Desktop Management Console\" (MMC) snap-in. This has a
checkbox for console session which is on by default.

Be warned that if you do not connect to the console session with the
same account as the one currently logged in, all open files in the
console session will be lost as the console session is force logged off.
You get a big warning message about this though if you try and log in
with another account. If you log in with the same account you directly
take control over the console session and any other person connected on
the console session gets disconnected. All files/apps will still be
running.

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

Note that if you have set a timeout limit on sessions to disconnect or
remove them this might apply to the console session as well. I haven\'t
verified this yet. In other words if you will be running cmd windows or
other apps don\'t set a time limit. Leave it at default which is
umlimited.

This concept of console session is different compared to the remote
desktop service built-in in Windows XP. In Windows XP you only have one
session which is the console session and that\'s the one you always
connect to. With Windows 2003 in Remote Administration mode you have the
console session and two other \"standard\" sessions as in Windows 2000
Server, where the console never is the default one unless you use one of
the methods mentioned above.

*Full credit to
[Argyle](http://forums.theplanet.com/index.php?s=17fbd90104cc8defc9bde032fcf52158&showuser=38621)*
