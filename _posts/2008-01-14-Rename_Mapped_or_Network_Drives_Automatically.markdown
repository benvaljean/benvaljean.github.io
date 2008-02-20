---
layout: post 
title: Rename Mapped or Network Drives Automatically
---

Renaming of mapped drives on a per-user basis is easily done through
right-clicking it and choosing Rename. What if you wish to rename the
share for all users on a network?

Create a VBS script in the NETLOGON share:

    mDrive = "N:\\"
    Set oShell = CreateObject("Shell.Application")
    oShell.NameSpace(mDrive).Self.Name = "New drive name here"

Replace N:\\\\ with the appropriate drive name, save it as
renamedrive.vbs for instance.

Next, add the following line to the login script:

    wscript //b renamedrive.vbs

[Category:Windows](Category:Windows "wikilink")
