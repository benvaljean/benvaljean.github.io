---
layout: post 
title: Create custom System Folder on Desktop/My Computer (Windows)
---

Follow the steps below to create a custom folder on the Desktop or My
Computer which cannot be renamed for deleted, like My Documents for
instance. A unique GUID is referred to in these steps as
\"{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\" - this is just an example and
can be anything you want so long as it is unique on your PC.

1.  Create new key:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}
    and set \"(Default)\" to the name of the folder, for example \"My
    Games.\"
2.  Create new subkey:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\DefaultIcon
    . Set \"(Default)\" to be the .ico file for the icon
3.  Create new subkey:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\InProcServer32
    . Set \"(Default)\" = shell32.dll
4.  Create new string value:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\ThreadingModel
    = \"Apartment\" . Do not create the string value under the
    DefaultIcon subkey but under the GUID key itself.
5.  Create subkeys for this path:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\Shell\\\\Open
    My Menu\\\\Command . Set \"(Default)\" to be the command when double
    clicked, for example \"explorer /root,c:\\\\MyGames\"
6.  Create subkeys for this path:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\ShellEx\\\\PropertySheetHandlers\\\\{FD4DF9E0-E3DE-11CE-BFCF-ABCD1DE12345}
    .
7.  Create new key:
    HKEY\_CLASSES\_ROOT\\\\CLSID\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}\\\\ShellFolder
    . Create a new binary value here called \"Attributes\" and set it to
    \"00 00 00 00\".

**To place the folder onto the Desktop:** Create new key:\
\*HKEY\_LOCAL\_MACHINE

-   -   SOFTWARE
        -   Microsoft\\\\Windows\\\\CurrentVersion
            -   Explorer
                -   Desktop\\\\NameSpace\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}

**To place the folder in My Computer:** Create new key:\
\*HKEY\_LOCAL\_MACHINE

-   -   SOFTWARE
        -   Microsoft\\\\Windows\\\\CurrentVersion
            -   Explorer
                -   MyComputer\\\\NameSpace\\\\{BG3DF9E0-E3DA-21TE-BFDD-DFGH1WE45678}

After this is done the only way to remove the icon is to remove the keys
under the Desktop or My Computer namespace.

### See Also

[Registry](Registry "wikilink")
