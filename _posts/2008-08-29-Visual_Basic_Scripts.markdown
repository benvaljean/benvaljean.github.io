---
layout: post 
title: Visual Basic Scripts
---

### What is Visual Basic?

VB is a third-generation programming language basic on BASIC; written by
Microsoft. Its applications inculde scripting for Microsoft Office with
the ability to write significant apps that use Excel and Access. It can
also be used by itself with the [Windows Scripting
Host](http://www.pcsupportadvisor.com/Windows_scripting_host_page1.htm)
bulit into Windows. VB scripts have the `.vbs` extension and file
assocations are setup by default to run the script when double-clicked
although some error messages may not appear unless you run it in cmd:
`cscript scriptname.vbs` .

### Append/Log to a text file

This script will query the user for a particular file and then
create/append the line \"Current time:\" followed by the current time:

    strFile = InputBox ("Enter File Name",,"C:\\MyFile.Txt")
    Const ForAppending = 8
    set objFSO = CreateObject("Scripting.FileSystemObject")
    set objFile = objFSO.OpenTextFile(strFile, ForAppending, True)
    objFile.WriteLine("Current time: " & Now)
    objFile.Close
    MsgBox "Done"
