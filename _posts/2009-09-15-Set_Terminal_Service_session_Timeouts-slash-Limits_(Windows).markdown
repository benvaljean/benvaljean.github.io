---
layout: post 
title: Set Terminal Service session Timeouts/Limits (Windows)
---

I order to prevent all your terminal service sessions being used and
thereby blocking access to a server, `tsadmin` can be used to log users
off remotely or session timeouts / limits can be imposed.

Add the following Registry entries, creating a 1 hour disconnected
session limit and a 2 hour idle session limit:

    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp]
    "MaxDisconnectionTime"=dword:0036ee80
    "MaxIdleTime"=dword:006ddd00

To add the entries save as whatever.reg and double-click.

[Category:Windows](Category:Windows "wikilink")
