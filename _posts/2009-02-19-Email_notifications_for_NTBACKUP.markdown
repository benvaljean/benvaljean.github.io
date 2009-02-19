---
layout: post 
title: Email notifications for NTBACKUP
---

The native backup software with Windows is useful to use when no
paid-alternatives are available and in many ways remains the arguably
most reliable method for backing up Exchange, however it cannot natively
send emails notifying a system administrator whether or not a backup has
completed. Even in well-funded environments it is recommended to have a
secondary backup contingency in case the primary setup fails upon
restore.

Email notifications for NTBACKUP are achieved by using a VBS script
which is scheduled to be run straight after the backup has finished.
This utilises a command-line SMTP mailer programme to send an email from
the most recent NTBACKUP log file.

### Setup

1\. Install the command line email **Blat**: <http://www.blat.net/> Its
location can be anywhere but the path already in the VBS script is
C:\\\\BackupNotify\\\\full\\\\blat.exe\
2. Setup initial details for blat:
`blat -install `<smtp server>` `<from address> For
example:`blat exchange.company.local backups@company.local`\
3. Save the below script to the PC where backups are performed as
NTBackupNotify.vbs and adjust the variables as necessary:

    'NTBackupNotify.vbs
    'Adapted from a script by Gary Thorne http://www.halsys.com/help/default.htm
    'www.rogerrabbit.net/wiki/Email_notifications_for_NTBACKUP
    '
    'Schedule this script to run straight after an NTBACKUP finishes, uses Blat www.blat.net to send out emails.
    '
    Const strLogDir = "C:\\Documents and Settings\\schedadmin\\Local Settings\\Application Data\\Microsoft\\Windows NT\\NTBackup\\data\\"
    Const strMailSender = "backups@company.local"
    Const strMailRecipient = "admin@company.local"
    Const strBlat = "C:\\BackupNotify\\full\\blat.exe"
    Const strBlatLog = "C:\\backupnotify\
    tbackuphandler.log"
    Const strsubject = "Backup report"

    Sub Main()
        Dim fso, WshShell, fldLogs, filLog, strCmd, sFileBuffer, strfail

        Set fso = CreateObject("Scripting.FileSystemObject")
        Set WshShell = WScript.CreateObject("WScript.Shell")
        Set fldLogs = fso.GetFolder(strLogDir)
        For Each filLog In fldLogs.Files
            If DateDiff("n", filLog.DateLastModified, Now) < 5 Then
                strCmd = "cmd /c type " & Chr(34) & filLog.Path & Chr(34) & "|" & strBlat & " -subject " & Chr(34) & strsubject & Chr(34) & " -f " & strMailSender & " -to " & strMailRecipient & " -log " & strBlatLog
                Wscript.echo strCmd

                WshShell.Run strCmd

            End If
        Next
                
        Set fldLogs = Nothing
        Set WshShell = Nothing
        Set fso = Nothing
    End Sub

    Main

4\. Create a new BAT file which runs the command line that was previously
scheduled to be run by itself followed by the NTBackupNotify.vbs script.
For instance:

    @echo off
    rem BAT script to run NTBackupNotify.vbs script after previous command has completed.
    rem AD-hoc backup
    xcopy c:\\files\\*.* c:\\filesbackup
    cscript c:\\
    c:\\backupnotify\\NTBackupNotify.vbs

NTBACKUP will cause the shell to wait until it has finished as the
process is not run in the background; always ensuring that the VBS
script is run after NTBACKUP has finished.\
5. Create schedule as required.
