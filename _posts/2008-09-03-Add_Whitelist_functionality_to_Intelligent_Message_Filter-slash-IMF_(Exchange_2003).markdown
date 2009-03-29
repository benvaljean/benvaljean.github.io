---
layout: post 
title: Add Whitelist functionality to Intelligent Message Filter/IMF (Exchange 2003)
---

### Background

[Intelligent Message
Filter](http://technet.microsoft.com/en-us/exchange/bb288484.aspx) is a
sever-side anti-apam technology bundled with [Microsoft
Exchange](http://www.microsoft.com/exchange/evaluation/default.mspx).
The version with Exchange 2007 is more robust however the version with
Exchange 2003 is arguably still in its beta stage as it can cause
stability issues and is definitely not a replacement for a
SpamAssain/MTA/Razor/DCC solution or a dedicated device such as the
[Barracuda Spam
Firewall](http://www.barracudanetworks.com/ns/?L=en_emea).

One of the reasons why IMF is not a replacement for such a solution is
that the version with Exchange 2003 has no whitelist functonality. It is
possible to setup IMF Custom Weighting however it cannot filter based on
headers (cannot whitelist based on sender) and can only filter based on
the body or subject of an email - not always useful. In addition the
custom weighting itself has been proven not to work properly in many
installations by this article\'s author. Another method involves the
usage of 3rd-party tools such as IMF Companion.

If the IP address of the server sending the email that needs to be
whitelisted is known and unlikely to change its IP address can be added
to the Global Accept List as seen here:
[1](http://forums.msexchange.org/m_1800440876/mpage_1/key_/tm.htm#1800440876)

### The script

None of the options above replace a whitelist based on sender smtp
address. When the below [visual basic](Visual_Basic_Scripts "wikilink")
script is configured with the appropriate folders and set to run every 5
minutes in Schedulted Tasks it will give full whitelist functonality.
IMF must be set to archive email messages for the script to work. The
script searches an input list of email address or domains and then
searches all the archived messages for any hits. With each hit the
archived email is copied to the Pickup folder on Exchange and
immediately gets delivered.

The below script is a modified version of the one
[here](http://www.experts-exchange.com/Software/Internet_Email/Q_22461861.html).
The version below adds a log-file and places all emails post-scanning in
a \'scanned\' folder where they can be deleted.

    Option Explicit

    '-----------------------------------------------------------------------
    'The following script was developed to work with MS Exchange Server's
    'Intelligent Message Filter when UCE messages are archived.  This script
    'was developed as simply and plainly as possible so that non-developers
    'can apply it to their own environment.
    '
    'This script is provided to help Exchange admins.  It may or may not be
    'helpful to you and, depending on your environment may adversely affect
    'your mail delivery.  It is strongly recommended that you review this
    'script in its entirety and, if possible, apply it to a test environment
    'before using it on your production server.
    '
    'Standard disclaimer: This script is not guaranteed or warrantied. You
    'are on your own.
    '
    'Installation:
    'Just copy this script some place on your Exchange Server.  It is
    'recommended you put this script underneath the UCEArchive folder for
    'easy locating and to avoid accidental deletion.  It is recommended
    'that you keep the Whitelist file in the same location.
    '
    'Running:
    'Just double-click the VBS file to run it. After the inital run, the
    'script should only take a few seconds to process, and therefore you can
    'schedule it in your Task Scheduler to run every 5 minutes for instance.
    '
    'The format for the Whitelist text file is very simple: one email
    'address (user@domain.com) or domain wildcard (*@domain.com) per line.
    'These are valid senders, not recipients.  To specify internal recipients
    'that should not have IMF rules applied to them, use the Connection
    'Filtering|Exceptions option in IMF.
    '
    '
    'If the X-Sender field does not match any whitelist entry, the email
    'is considered UCE.  To avoid re-scanning, the message is moved to a
    'another folder.
    '
    '-----------------------------------------------------------------------

    Dim objFSO, objArchiveFolder, objFile, objUCE, objWhiteList, objNewFolder, objLogfile
    Dim strServerPath, strArchivePath, strPickupPath, strWhiteListName, strLogFile
    Dim strWhiteList, strReadLine, strXSender, strXSenderDomain
    Dim bMatchSender, bMatchDomain, dtYear, dtWeek, strScanned

    'Set variables. Make sure paths have a trailing '\\'

       strServerPath = "d:\\Program Files\\Exchsrvr\\Mailroot\\vsi 1\\"
       strArchivePath = "d:\\Program Files\\Exchsrvr\\Mailroot\\vsi 1\\UCEArchive\\"
       strPickupPath = "d:\\Program Files\\Exchsrvr\\Mailroot\\vsi 1\\Pickup\\"
       strWhiteListName = "d:\\Program Files\\Exchsrvr\\WhiteList.txt"
       strLogFile = "d:\\Program Files\\Exchsrvr\\WhiteList.log"
       strScanned = "Scanned"

    'Set the FilesystemObject variable, set the folder variable
       Set objFSO = CreateObject("Scripting.FileSystemObject")
       Set objArchiveFolder = objFSO.GetFolder(strArchivePath)

    'Read the entire WhiteList file into a single string for easy searching
       Set objWhiteList = objFSO.OpenTextFile(strWhiteListName, 1)
       strWhiteList = objWhiteList.ReadAll

    'Run through the archive folder.  Process each email (.EML)
       For Each objFile in objArchiveFolder.Files

          If Right(objFile,3) = "EML" then

             'Email found
             Set objUCE = objFSO.OpenTextFile(strArchivePath  & objFile.Name, 1)

             'Read the first line of the file (should be X-Sender line)
             strReadLine = objUCE.Readline

             'Parse the line to only get the X-Sender value
             strXSender = Right(strReadLine,Len(strReadLine)-10)

             'Use the In String function to find the X-Sender value in the WhiteList string
             bMatchSender = InStr(1,strWhiteList,strXSender,1)

             'If bMatchSender is greater than zero, then a match was found
             If bMatchSender > 0 then
                    'Close the email, move it to the Pickup folder for mail server processing
                    objUCE.close
                    set objUCE = objFSO.getfile(strArchivePath  & objFile.Name)
                    objUCE.Move(strPickupPath)
                    Set objLogFile = objFSO.OpenTextFile(strLogFile, 8, True)
                    objLogFile.Writeline Now & "," & strXsender
                    objLogFile.Close

             Else
                    'Sender match failed, so look for wildcard domain match
                    'Extract domain value from X-Sender string
                    strXSenderDomain = Right(strXSender,Len(strXSender)-Instr(1,strXSender,"@",1))

                    'Use the In String function to find a wildcard domain entry in the WhileList string
                    'A wildcard domain entry is represented by *@ in front of the domain name.
                    bMatchDomain = Instr(1,strWhiteList,"*@" & strXSenderDomain,1)

                    'If bMatchDomain is greater than zero, then a match was found
                    If bMatchDomain > 0 then
                       'Close the email, move it to the Pickup folder for mail server processing
                       objUCE.close
                       set objUCE = objFSO.getfile(strArchivePath  & objFile.Name)
                       objUCE.Move(strPickupPath)
                    Set objLogFile = objFSO.OpenTextFile(strLogFile, 8, True)
                    objLogFile.Writeline Now & "," & strXsender
                    objLogFile.Close
                    Else

                       'Has failed both sender and sender domain match
                       'Close the email, move it to a folder named for the Year and week number of the year
                       'This cleans up the Archive folder so the messages are continuously scanned.
                       objUCE.close
                        'Move to scanned folder
                        strScanned = "Scanned"
                        Set objUCE = objFSO.GetFile(strArchivePath  & objFile.Name)

                        'Create scanned folder id required
                       If Not objFSO.FolderExists(strArchivePath & strScanned & "\\") Then
                          Set objNewFolder = objFSO.CreateFolder(strArchivePath & strScanned & "\\")
                       End If  'end of folder check

                        objUCE.Move(strArchivePath & strScanned & "\\")

                    End If  'end of domain match check

             End If  'end of sender match check

          End If  'end of email check

       Next 'get next file in folder
       

### See Also

-   [Visual Basic Scripts](Visual_Basic_Scripts "wikilink")
-   [Exchange 2007 Content FIlter: The Whitelist Is
    Here!](http://exchangepedia.com/blog/2007/01/exchange-2007-content-filter-whitelist.html)
-   [MSExchange: IMF
    v2](http://www.msexchange.org/tutorials/Intelligent-Message-Filter-version-2-IMF-v2.html)
-   [Caveats in
    IMF](http://blogs.mcbsys.com/mark/post/Exchange-IMF-and-Custom-Weight-Lists.aspx)
-   [Exclude a particular recipient from anti-spam
    filtering](http://support.microsoft.com/?id=912587)
