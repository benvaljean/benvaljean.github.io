---
layout: post 
title: Visual Basic Scripts
---

### What is Visual Basic?

VB is a third-generation programming language based on BASIC; written by
Microsoft. Its applications inculde scripting for Microsoft Office with
the ability to write significant apps that use Excel and Access. It can
also be used by itself with the [Windows Scripting
Host](http://www.pcsupportadvisor.com/Windows_scripting_host_page1.htm)
bulit into Windows. VB scripts have the `.vbs` extension and file
assocations are setup by default to run the script when double-clicked
although some error messages may not appear unless you run it in cmd:
`cscript scriptname.vbs` .

### Write/Append/Log to a text file

This script will query the user for a particular file and then
create/append the line \"Current time:\" followed by the current time:

    Dim strFile, objFSO, objFile
    strFile = InputBox ("Enter File Name",,"C:\\MyFile.Txt")
    Const ForAppending = 8
    set objFSO = CreateObject("Scripting.FileSystemObject")
    set objFile = objFSO.OpenTextFile(strFile, ForAppending, True)
    objFile.WriteLine("Current time: " & Now)
    objFile.Close
    MsgBox "Done"

In some situations the above code will not work if it is in a loop, the
code below can be used in a loop and writes to a text file the current
time and a log entry

    Dim objLogfile, objFSO, strLogFile
    strFile = "c:\\example.log"
    Set objFSO = CreateObject("Scripting.FileSystemObject")
    For each Item in Example.list
      Set objLogFile = objFSO.OpenTextFile(strLogFile, 8, True)
      objLogFile.Writeline Now & " log entry"
      objLogFile.Close
    Next

### Add Whitelist functonality to Intelligent Message Filter/IMF (Exchange)

See [Add Whitelist functonality to Intelligent Message Filter/IMF
(Exchange)](Add_Whitelist_functonality_to_Intelligent_Message_Filter/IMF_(Exchange) "wikilink")
