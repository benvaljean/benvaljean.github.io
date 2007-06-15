---
layout: post 
title: Restore/Repair My Documents (Windows)
---

#### Restore My Documents

If the My Documents icon and entry within file dialogs becomes hidden
run this:

` rundll32 mydocs.dll,RestoreMyDocsFolder`

#### Repair My Documents

If the registry entries for My Documents become corrupt crashes can
occur and changes to the path do not occur in file dialogs, this script
fixes that issue:

    'SetMyDocs.vbs
    'Set the path to My Documents.
    'Used when User Shell Folder\\Personal is blank (the UI doesn't accept changes)
    '
    'Serenity Macros     http://www.angelfire.com/biz/serenitymacros 
    'David Candy    davidc@sia.net.au
    '
    On Error Resume Next
    strExplain="SetMyDocs displays and changes the My Documents path." & vbCRLF & "Used when their is a blank value for Personal in the User Shell Folders key" & vbCRLF & vbCRLF
    strTitle="Set MyDocuments Path"

    Dim Sh
    Set Sh = WScript.CreateObject("WScript.Shell")
    ReportErrors "Creating Shell"
    MyDocsPath1=Sh.RegRead("HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\Shell Folders\\Personal")
    MyDocsPath2=Sh.RegRead("HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\User Shell Folders\\Personal")
    If Err.Number=-2147024894 then Err.Clear

    If MsgBox (strExplain & "Shell Folders" & vbtab & MydocsPath1 & vbCRLF & "User Shell Folders" & vbtab & MydocsPath2 & vbCRLF & vbCRLF & "Continue?", vbYesNo + vbInformation, strTitle) = 6 then
        Dim bffShell
        Dim bff
        Set bffShell = WScript.CreateObject("Shell.Application")
        Set bff = bffShell.BrowseForFolder(0, "Select the My Documents folder", 1)
        If Err.number<>0 Then
            ReportErrors("Setting up Browse for Folder")
        Else
            A = bff.ParentFolder.ParseName(bff.Title).Path
            If err.number=424 then err.clear
        End If


        If A<>"" then 
            Sh.RegWrite "HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\Shell Folders\\Personal", A
            Sh.RegWrite "HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\User Shell Folders\\Personal", A
            If Err.number<>0 Then
                ReportErrors("Writing to the registry")
            Else
                MsgBox "My Documents folder has been changed to " & A & vbCRLF & vbCRLF & "Edit the path of the My Documents folder by right clicking the icon and choosing properties. Windows may need to be restarted before the My Documents icon works properly.",  vbInformation, strTitle
            End If
        Else
            MsgBox "A blank value was entered or the dialog box was canceled, no changes made",  vbInformation, strTitle
        End If
    End If
    ReportErrors "SettingPath"

    VisitSerenity

    Sub ReportErrors(strModuleName)
        If err.number<>0 then Msgbox "Error occured in " & strModuleName & " module of " & err.number& " - " & err.description & " type" , vbCritical + vbOKOnly, "Something unexpected"
        Err.clear
    End Sub

    Sub VisitSerenity
        If MsgBox("This program came from the Serenity Macros Web Site" & vbCRLF & vbCRLF & "Would you like to visit Serenity's Web Site now?", vbQuestion + vbYesNo + vbDefaultButton2, "Visit Serenity Macros") =6 Then
            sh.Run "http:\\\\www.angelfire.com\\biz\\serenitymacros"
        End If
    End Sub

### See Also

[Registry](Registry "wikilink")
