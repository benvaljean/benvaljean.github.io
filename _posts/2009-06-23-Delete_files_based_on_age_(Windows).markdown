---
layout: post 
title: Delete files based on age (Windows)
---

On Windows this can be achieved using a VB script. The follwing can be
saved with a .vbs extension:

    Dim Fso
    Dim Directory
    Dim Modified
    Dim Files
    Set Fso = CreateObject("Scripting.FileSystemObject")
    Set Directory = Fso.GetFolder("C:\\Program Files\\Exchsrvr\\Mailroot\\vsi 1\\UceArchive")
    Set Files = Directory.Files
    For Each Modified in Files
    If DateDiff("D", Modified.DateLastModified, Now) > 1 Then Modified.Delete

    Next

### Automating

Windows Task scheduler can have problems if the VBS file is referenced
to directly, it is best to create a batch file with the follwing:

    @echo off
    c:\\windows\\system32\\cscript //b script.vbs
    echo %date% %time% Sched ran VB scrupt >>c:\\vbs.log

### Notes

The VB DateDiff() function can be modified to delete in other units.
