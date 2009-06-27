---
layout: post 
title: Disable Group Policy for individual PC locally (Windows)
---

If there is a scenario where it is required to disable the loading of
group policy objects for an individual machine/PC without moving the
computer account, it is possible to do so locally from the PC.

### Method 1

Locate / create the following [Registry](registry "wikilink") DWORD key:

    HKEY_LOCAL_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows\\System\\DisableGPO

Setting for Value Data: \[0 = Default (Enabled) / 1 = Disabled\]

### Method 2

Ensure the user logging on does not have access to the
%systemroot%\\\\system32\\\\GroupPolicy directory.

[Category:Windows](Category:Windows "wikilink")
