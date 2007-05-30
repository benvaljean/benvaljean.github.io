---
layout: post 
title: Registry (Windows)
---

### Structure

-   **HKEY\_CLASSES\_ROOT**: Contains software settings about
    drag-and-drop operations, handles shortcut information, and other
    user interface information. There is a subkey here for every file
    association that has been defined.
    -   AllFilesystemObjects\\\\shellex
        -   ContextMenuHandlers
            -   Copy To: Create this key to add a useful \"Copy to..\"
                entry for all files/folders, set the defautl value to
                {C2FBB630-2971-11d1-A18C-00C04FD75D13} .
            -   Move To: As above except the default value must be
                {C2FBB631-2971-11d1-A18C-00C04FD75D13} .
        -   CLSID
            -   {87D62D94-71B3-4b9a-9489-5FE6850DC73E} This class ID
                relates to the data-extraction from AVIs for previewing
                data within them in an Explorer view. Sometimes Explorer
                goes mad and tries to extract the whole file in tiny
                segments and hangs Explorer until it is done. You can
                avoid this by playing a \"-\" in fornt of the class ID
                and disable the feature. When you see those notes about
                backing up the reg before editing it they are talking
                about keys like this, so ensure you get the right one.

<!-- -->

-   **HKEY\_CURRENT\_USER**: Contains settings regarding the currently
    logged-on user.
    -   AppEvents: Settings for assigned sounds to play for system and
        applications sound events.
    -   Control Panel: Control Panel settings, similar to those defined
        in System.ini, Win.ini and Control.ini in Windows 3.xx.
        -   Desktop
            -   MaxMinClose: (0 or 1) Set to 0 to disable the
                max/min/close tooltips.
            -   MenuShowDelay: (delay in ms 0-999) The delay between
                clicking the menu/right clicking and the menu appearing,
                it is useful to set this to 0.
            -   WindowMetrics
                -   MinAnimate: (string value: 0 or 1) Allows you to
                    disable the title-bar animation when you minimise a
                    window.
    -   InstallLocationsMRU: Contains the paths for the Startup folder
        programs.
    -   Keyboard layout: Specifies current keyboard layout.
    -   Network: Network connection information.
    -   RemoteAccess: Current log-on location information, if using
        Dial-Up Networking.
    -   Software: Software configuration settings for the currently
        logged-on user.
    -   Policies
        -   Microsoft\\\\Internet Explorer\\\\Control Panel: This key
            contains details on whether settings can be changed by the
            user or whether they are ghosted. For each key below 0=user
            can edit settings, 1=appears ghosted/unavilable. All are
            DWORD.
            -   HomePage
            -   Cache
            -   History
            -   Colors
            -   Links
            -   Fonts
            -   Languages
            -   Accessibility
            -   Certificates
            -   Profiles
            -   Wallet
            -   Connection Wizard
            -   Connection Settings
            -   Proxy
            -   Autoconfig
            -   Messaging
            -   CalendarContact
            -   Check\_If\_Default
            -   Advanced
            -   ConnWiz Admin Lock
            -   SecurityTab
            -   AdvancedTab
            -   ConnectionsTab
            -   ProgramsTab
    -   \\\\Microsoft\\\\Office\\\\\<9.0\|10.0\|11.0\>\\\\Outlook\\\\Security
        -   Level1Remove: (string) Specify extensions to not be blocked
            by the internal blocking function within Outlook, seperated
            by semi-colons. See also Unblock Outlook attachment blocking
    -   \\\\Microsoft\\\\Windows\\\\CurrentVersion
        -   Internet Settings
            -   ProxyServer: Address for a proxy server for the Internet
                API
            -   ProxyEnable: (0 or 1)
            -   ProxyOveride: Exculded addreses
        -   Explorer
            -   Advanced
                -   Hidden (1 = show 2 = do not show) Display hidden
                    files.
                -   ShowSuperHidden: (0 = hide files 1= show files) As
                    above but for files when are hidden and system.
                -   Intellimenus: (0 or 1) Set to 0 to disable the
                    hiding of rarely used menu items until you select
                    the down-arrows.
                -   StartMenuScrollPrograms (\"yes\" or \"no\") Allow
                    scrolling of programs in the start menu.
            -   CabinetState
                -   \"Use Search Asst\": Set to \"no\" to enable the
                    Win2k search interface, inculde the spaces in the
                    key name.
    -   \\\\Microsoft\\\\Windows CE Services\\\\Partners\\\\<Device ID>
        \\\\Services\\\\Synchronization: Settings in realtion to
        PDAs/smartphone, typically with regard to ActiveSync. Note the
        US spelling.
        -   Briefcase Creation: States when the synchronisation was
            setup in secondd from 12:00 AM 0/0/0
        -   ResetPartner: (0 or 1) Set to 1 to force the reset of a
            partnership.
    -   \\\\Microsoft\\\\Windows NT\\\\Curent Version
        -   Program Manager\\\\Restrictions: Allows manipulation
            restrictions; usually set by Group Policy.
            -   NoRun: (0 or 1)
            -   NoFileMenu: (0 or 1)
            -   NoClose: (0 or 1) Why would a sysadmin want to restrict
                the closing of Task Manager?
        -   Winlogon
            -   BuildNumber: You can have great fun with this if you are
                bored.
            -   ParseAutoexec: Force Windows to parse the autoexec.bat
                file.
