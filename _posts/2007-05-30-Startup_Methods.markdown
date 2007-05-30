---
layout: post 
title: Startup Methods
---

### Directories

\%windir%\\\\Start Menu\\\\Programs\\\\StartUp (English)

\%windir%\\\\All Users\\\\Start Menu\\\\Programs\\\\StartUp (English)

\%windir%\\\\Menu Démarrer\\\\Programmes\\\\Démarrage (French)

\%windir%\\\\All Users\\\\Menu Iniciar\\\\Programas\\\\Iniciar
(Portuguese, Brasilian)

Any file or shortcut in the directories above will start when Windows is
booted.

### Registry

This Autostart Directory is stated in these keys:

-   **HKEY\_CURRENT\_USER**
-   Software\\\\Microsoft\\\\Windows\\\\CurrentVersion\\\\Explorer
    -   Shell Folders
        -   Startup: (string) All files and shortcuts in the dir
            referenced here are started on booting.
        -   Common Startup: (string) as above.
    -   User Shell Folders
        -   Startup: (string) All files and shortcuts in the dir
            referenced here are started on booting.
        -   Common Startup: (string) as above.

### Config Files (Windows 9x)

#### system.ini

Another way to start a file is use the shell method. The file name
following explorer.exe will start whenever Windows starts:

`  %windir%\\system.ini: Shell=explorer.exe example.exe`

#### win.ini

load= line

run= line

This is a autostart method that trojan authors have been using for
years. You need to be sure that the \'load=\' line in
%windir%\\\\win.ini (without the quotes) has no other file names next to
it. Such as \'load= pic.exe\', if you see a file name next to the load=
you\'d better delete it. File names can be hidden by placing them to the
far right of one of these lines. Some AOL password capture parograms do
that.

### See Also

[Registry](Registry "wikilink")
