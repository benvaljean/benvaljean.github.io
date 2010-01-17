---
layout: post 
title: Delete files based on age (Windows)
---

On Windows this can be achieved using a VB script. The VBS script below
deletes files which are more than 1 day old:

    Dim Fso
    Dim Directory
    Dim Modified
    Dim Files
    Dim Folder
    If (Wscript.Arguments.Count < 1) Then 
      Wscript.Echo "Required Parameter missing"  
    Wscript.Quit
    End If
    Folder = Wscript.Arguments(0)
    Set Fso = CreateObject("Scripting.FileSystemObject")
    Set Directory = Fso.GetFolder(Folder)
    Set Files = Directory.Files
    For Each Modified in Files
    If DateDiff("D", Modified.DateLastModified, Now) > 1 Then Modified.Delete

    Next

The parameter is the folder where you want to perform the deletion
operation.

### Automating

Windows Task scheduler can have problems if the VBS file is referenced
to directly, it is best to create a batch file with the follwing:

    @echo off
    c:\\windows\\system32\\cscript //b script.vbs
    echo %date% %time% Sched ran VB scrupt >>c:\\vbs.log

### Notes

The VB DateDiff() function can be modified to delete in other units.

[Category:Windows](Category:Windows "wikilink")
