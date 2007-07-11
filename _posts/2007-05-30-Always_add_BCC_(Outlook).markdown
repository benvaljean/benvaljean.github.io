---
layout: post 
title: Always add BCC (Outlook)
---

There is no function to always add a BCC entry to every email you
receive within the interface of Outlook although it can be programmed.

Add the code below to \'ThisOutlookSession\' in the VBA console, which
can be activated by pressing Alt+11:

    Private Sub Application_ItemSend(ByVal Item As Object, Cancel As Boolean)
    Dim objRecip As Recipient
    Dim strMsg As String
    Dim res As Integer
    Dim strBcc as String
    ' #### USER OPTIONS ####
    ' address for Bcc -- must be SMTP address or resolvable
    ' to a name in the address book
    strBcc = "someone@somewhere.dom"
    On Error Resume Next
    Set objRecip = Item.Recipients.Add(strBcc)
    ' handle case of user canceling Outlook security dialog
    If Err = 287 Then
    strMsg = "Could not add a Bcc recipient " & _
    "because the user said No to the security prompt." & _
    " Do you want still to send the message?"
    res = MsgBox(strMsg, vbYesNo + vbDefaultButton1, _
    "Security Prompt Cancelled")
    If res = vbNo Then
    Cancel = True
    Else
    objRecip.Delete
    End If
    Err.Clear
    Else
    objRecip.Type = olBCC
    objRecip.Resolve
    If Not objRecip.Resolved Then
    strMsg = "Could not resolve the Bcc recipient. " & _
    "Do you want still to send the message?"
    res = MsgBox(strMsg, vbYesNo + vbDefaultButton1, _
    "Could Not Resolve Bcc Recipient")
    If res = vbNo Then
    Cancel = True
    End If
    End If
    End If
    Set objRecip = Nothing
    End Sub

[Category:Outlook](Category:Outlook "wikilink")
