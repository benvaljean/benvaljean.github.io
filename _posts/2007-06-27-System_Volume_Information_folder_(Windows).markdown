---
layout: post 
title: System Volume Information folder (Windows)
---

From Windows 2000 onwards a folder called \'System Volume Information\'
resides in the root of the Windows inatallation partition, usually
C:\\\\ . The directory security is set so that not even Administrators
can access it, although this can be changed. Files in thie folder if
changed/deleted could cause certain functions to fail.

### Folder Contents

-   System Restore points: All beginning with \"\_restore\" .
-   Distributed Link Tracking Service databases: This service tries to
    repair broken shortcuts.
-   File Indexes: Databases for the native file indexer.
-   Volume Snapshot Service databases: Used to allow volume shadowing -
    this allows previous versions of files to be restored on the same
    hard drive allowing restores to be done by users so long as it is
    not deleted.
-   WinFS databases: Longhorn only

### Accessing the folder

If the folder is not in the C:\\\\ listing it is being hidden, to
disable this:

1.  From within Explorer go to Tools \> Folder Options
2.  Go to the view tab, then ensure **Show hidden files and folders** is
    clicked and that **Hide protected operating system files
    (Recommended)** is unchecked. Click Yes to the confirmation.

After which go back to C:\\\\:

1.  Right click the System Volume Information folder
2.  Select properties, click on the security tab
3.  Click add and typ in the username that requires access - usually
    your own in this case.
4.  Check Full Control, click OK and then OK again.

### See Also

[Distributed Link Tracking
Service](http://www.microsoft.com/technet/prodtechnol/winxppro/reskit/prkc_fil_ngyp.asp)

[File indexing
Service](http://msdn.microsoft.com/library/en-us/dnanchor/html/indexserv.asp)

[Volume Snapshot
Service](http://msdn.microsoft.com/msdnmag/issues/01/12/XPKernel/default.aspx)

[KB309531](http://support.microsoft.com/kb/309531)

[Category:Windows](Category:Windows "wikilink")
