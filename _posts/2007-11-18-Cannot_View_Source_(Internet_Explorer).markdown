---
layout: post 
title: Cannot View Source (Internet Explorer)
---

### Symptom

From within Internet Explorer it is not possible to view the source code
to all or a particular web page.

### Causes and Resolution

1\. Temporary Files Full

:   When the Internet Explorer disk cache becomes full it may stop the
    View Source function from working. To resolve, open Internet
    Explorer and click Tools \> Internet Options \> Delete Files.

2\. Cookie Folder Location

:   This issue can also occur if your Cookies folder is located the user
    does not have at least Change permissions for the Cookies folder. To
    resolve, ensure the account has sufficient permissions on the
    Cookies folder.

3\. View Source Restriction

:   The View Source function may have been restricted by your
    Administrator. To resolve, see the \"NoViewSource\" registry value
    in Internet Explorer Restrictions.

4\. Incomplete Page Download

:   Some times if the page download is stopped before it has finished
    Internet Explorer may now show the \"View Source\" item.

5\. Invalid Temporary Directory

:   It is unlikely but possible that this error is due to the path
    specified for the TMP environment variable being invalid. To
    resolve, ensure that the TEMP directory is a valid directory and
    that there is sufficient space on the drive.

6\. Invalid View Source Program

:   The editor that is automatically opened is defined by a registry
    key, this could be invalid. Check the contents of the key in:
    HKEY\_LOCAL\_MACHINE \\\\ SOFTWARE\\\\Microsoft\\\\Internet
    Explorer\\\\View Source Editor\\\\Editor Name. A string value of
    \"%windir%\\\\wordpad.exe\" is suggested.

7\. Right-click disabled by Web Page

:   Some web pages implement a restriction to stop visitors from
    right-clicking on the web page; usually to stop the saving of media.
    The source may still be viewed by using the menu: View \> Source.

8\. Missing Notepad.exe

:   The View Source function uses Notepad to display the HTML, if
    \"notepad.exe\" is missing from the Windows directory then it will
    not work. To resolve, ensure a copy of Notepad.exe is in the Windows
    directory.

[Category: Windows](Category:_Windows "wikilink")
