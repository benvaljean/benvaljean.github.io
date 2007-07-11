---
layout: post 
title: Context Menu Handler (Explorer)
---

Right-click is slow or weird behavior caused by context menu handlers

### Symptoms

1.  When you right-click a file/folder, there may be a huge delay before
    Windows displays the context menu.
2.  When you try to empty Recycle Bin (from Common Tasks), it opens
    Quick Finder instead.
3.  When you click Play All in the Music or Videos folder Common Tasks,
    nothing may happen.
4.  When you select multiple files and right click and open / print
    nothing happens. Whereas, selecting a single file in explorer and
    right click and open / print, it works fine.
5.  When you right-click a folder in the Start Menu and choose Open or
    Explore, nothing may happen. (Whereas, it works fine in Windows
    Explorer.)
6.  Error message \"Windows Explorer has encountered a problem and needs
    to close. We are sorry for the inconvenience\" when you right-click
    a folder.
7.  Right-click is extremely slow only when the network card is enabled.
8.  When you right-click on a folder and choose Properties, nothing may
    happen.
9.  Your image editing program does not start when you click the Edit
    button in Windows Picture and Fax Viewer.
10. Data Execution Prevention (DEP) error occurs when Windows Explorer
    or Control Panel is launched.
11. Nothing happens when you click Slideshow or Print in the Tasks pane
    in Windows Vista.

### Cause

These problems are caused by a bad context menu handler. A context menu
handler is a shell extension handler that adds commands to an existing
context menu (Example: cut, copy, paste, print, Scan with Norton etc). A
poorly coded context menu handler may be causing any of the above
symptoms. As context menu handlers can be added in different areas (file
class, folder, allfilesystemobjects, HKCR\\\\\* registry keys), it\'s a
difficult task for an end-user to pinpoint which shell extension is
causing the problem.

### Resolution

#### Method 1

First, isolate the problem. Observe when the problem occurs. While
right-clicking a particular file type? While right-clicking Folders?
While right-clicking all file types? As said earlier, context menu
handlers can load from any of these areas:

Registry Key\    Description\    \
HKCR \\\\\*\\\\shellex\\\\contextmenuhandlers\    Files\
\     HKCR\\\\AllFileSystemObjects\\\\shellex\\\\
contextmenuhandlers\    Files and file folders\    \
HKCR\\\\Folder\\\\shellex\\\\contextmenuhandlers\    Folders\    \
HKCR\\\\Directory\\\\shellex\\\\contextmenuhandlers\    File Folders\    \
HKCR\\\\<ProgID>\\\\shellex\\\\contextmenuhandlers\    File class\    \
HKCR\\\\Directory\\\\Background\\\\shellex\\\\ContextMenuHandlers\    Desktop\
If any of the symptoms occur when you deal with a folder, then you may
need to inspect the context menu handlers loaded in these areas
(AllFileSystemObjects, Folder, Directory). If it\'s only for a .txt
file, inspect the file class of .txt file (HKCR\\\    xtfile). Open
Registry Editor and backup the selected branch, delete the context menu
handlers one-by-one.

#### Method 2

ShellExView (by Nir Sofer) is an excellent tool to view and manage all
installed shell extensions. If available, it displays the description,
as well as version details, company information, location, file name and
more. You can optionally disable/enable any item, which can be very
useful to disable an extension, that you don t need or that has been
left behind in your right click menu from a previous software install.

[ShellExView](http://www.nirsoft.net/utils/shexview.html)

### See Also

[Slow right click](http://windowsxp.mvps.org/slowrightclick.htm)

[Manage the context-menu entries for folders, drives and Namespace
objects](http://windowsxp.mvps.org/context_folders.htm)

[Category:Windows](Category:Windows "wikilink")
