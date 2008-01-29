---
layout: post 
title: Registry (Windows)
---

### Structure

SK/UK = System key/User key: This key can be used as a user key under
HKEY\_CURRENT\_USER or as system key affecting all users on the machine
under HKEY\_CURRENT\_USER. Unless otherwise stated all keys are DWORD, 0
disables the feature and 1 enables it.

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
            -   {20D04FE0-3AEA-1069-A2D8-08002B30309D} This class ID
                relates to the My Computer icon on the desktop.
                -   LocalisedString: (string) The text that appears for
                    the My Computer icon can be manipulated here to make
                    it more useful. For instance Environment variables
                    can be inserted to read: %username% on
                    %computername%. If IE5.5 or earlier or pre XP alter
                    the part of key that reads \"My Computer\" for
                    instance it could read
                    \"\@C:\\\\WINNT\\\\system32\\\\shell32.dll,-9216\@1033,%USERNAME%
                    on %COMPUTERNAME%\". If IE6+ or XP then the key
                    simply reads the actual name under the icon itself,
                    for example: \"%USERNAME% on %COMPUTERNAME%\".

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
                -   \"Shell Icon BPP: (no of bytes as string) This key
                    details the bit-depth (number of colours) for the
                    icons. In nearly all cases this should equal the
                    bit-depth of your screen. If this setting is too
                    high Windows will default to 4 bit/16 colour icons.
                    See also: [Icon problem: Low colour icons (4 bits/16
                    colours) even with 16/32 bit screen mode
                    (Windows)](Icon_problem:_Low_colour_icons_(4_bits/16_colours)_even_with_16/32_bit_screen_mode_(Windows) "wikilink")
    -   InstallLocationsMRU: Contains the paths for the Startup folder
        programs.
    -   Keyboard layout: Specifies current keyboard layout.
    -   Network: Network connection information.
    -   RemoteAccess: Current log-on location information, if using
        Dial-Up Networking.
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
    -   Software: Software configuration settings for the currently
        logged-on user.
        -   Microsoft\\\\Office\\\\\<9.0\|10.0\|11.0\>
            -   Word\\\\Options
                -   SQLSecurityCheck: (0 or 1) Set this to 0 to disable
                    the \"Opening this document will run the following
                    SQL command\" prompt when opeing the Word doc that
                    runs a SQL query.
            -   Outlook\\\\Security
                -   Level1Remove: (string) Specify extensions to not be
                    blocked by the internal blocking function within
                    Outlook, seperated by semi-colons. See also [Disable
                    Attachment Blocking
                    (Outlook)](Disable_Attachment_Blocking_(Outlook) "wikilink")
        -   Microsoft\\\\Windows\\\\CurrentVersion
            -   Policies
                -   Explorer
                    -   NoResolveTrack: (0 or 1) If a shortcut is broken
                        when double-clicked Windows will try to find it
                        be default; set to 1 to disable this feature.
                    -   NoInternetIcon: (0= IE icon appears on desktop
                        1=IE icon not on desktop) SK/UK
                    -   NoSMConfigurePrograms: (0 or 1) Set to 1 to
                        remove to remove the Set Program Access and
                        Defaults icon on the start menu. SK/UK
                    -   MaxRecentDocs: (no of documents as DWORD) The
                        setting dictates the number of documents to be
                        displayed in Recent Documents. SK/UK
            -   Internet Settings
                -   ProxyServer: Address for a proxy server for the
                    Internet API
                -   ProxyEnable: (0 or 1)
                -   ProxyOveride: Exculded addreses
            -   Explorer
                -   link: (binary) 00 00 00 00 = no \"Shortcut to\"
                    prefix on shortuts. SK/UK
                -   Desktop
                    -   DesktopProcess: (1=seperate process 0=default)
                        Windows will normally use the same process for
                        the Desktop, takebar and directory-windows.
                        Should any one of these crash then the taskbar
                        and Desktop will need to restart as well.
                        Setthis key to 1 to put your desktop and taskbar
                        in a seperate process. Note: Active Desktop, IE
                        pre 5.5 cannot be used with this key set to 1.
                    -   CleanupWiz
                        -   \"Days between clean up\"
                        -   NoRun: (0 or 1) Set to disable the desktop
                            cleanup wizard
                -   Shell Folders
                    -   Personal: (string) Location of the \'My
                        Documents\' folder. See also: [Restore/Repair My
                        Documents
                        (Windows)](Restore/Repair_My_Documents_(Windows) "wikilink")
                -   User Shell Folders
                    -   Personal: (string) Location of the \'My
                        Documents\' folder - some apps check this key
                        instead of \'Shell Folders\'. See also:
                        [Restore/Repair My Documents
                        (Windows)](Restore/Repair_My_Documents_(Windows) "wikilink")
                -   Advanced
                    -   Hidden (1 = show 2 = do not show) Display hidden
                        files.
                    -   ShowSuperHidden: (0 = hide files 1= show files)
                        As above but for files when are hidden and
                        system.
                    -   Intellimenus: (0 or 1) Set to 0 to disable the
                        hiding of rarely used menu items until you
                        select the down-arrows.
                    -   StartMenuScrollPrograms (\"yes\" or \"no\")
                        Allow scrolling of programs in the start menu.
                    -   EnableBalloonTips: (0 or 1) Set to 0 to disable
                        balloon tips for example print notifications and
                        the tour.
                    -   TaskbarSizeMove: (0 = locked 1 = unlocked) If
                        context menus on the start menu have been
                        disabled than the start menu position can still
                        be locked/unlocked with this key.
                    -   TaskbarGlomming: (0 = not groups/Win2k style 1 =
                        grouped) This key controls taskbar item
                        grouping.
                    -   NoTrayContextMenu: (0 = disabled 1 = enabled)
                        This key controls context menus for the start
                        menu.
                -   CabinetState
                    -   \"Use Search Asst\": Set to \"no\" to enable the
                        Win2k search interface, inculde the spaces in
                        the key name.
                -   RunMRU: The cached entries for Run commands in the
                    start menu are stored hereandcan be safely deleted
                    if required.
    -   Microsoft\\\\Windows CE Services\\\\Partners\\\\<Device ID>
        \\\\Services\\\\Synchronization: Settings in realtion to
        PDAs/smartphone, typically with regard to ActiveSync. Note the
        US spelling.
        -   Briefcase Creation: States when the synchronisation was
            setup in seconds from 12:00 AM 0/0/0
        -   ResetPartner: (0 or 1) Set to 1 to force the reset of a
            partnership.
    -   Microsoft\\\\Windows NT\\\\Curent Version
        -   Program Manager\\\\Restrictions: Allows manipulation
            restrictions; usually set by Group Policy.
            -   NoRun: (0 or 1)
            -   NoFileMenu: (0 or 1)
            -   NoClose: (0 or 1)
        -   Winlogon
            -   BuildNumber: You can have great fun with this if you are
                bored.
            -   ParseAutoexec: Force Windows to parse the autoexec.bat
                file.

<!-- -->

-   **HKEY\_LOCAL\_MACHINE**: Contains information about the hardware
    and software settings that are generic to all users of this
    particular computer.
    -   Hardware: Information regarding hardware of the system,
        populated by NTDETECT.COM, loaded by NTLDR, at the very
        beginning of the boot process.
    -   Security: Network security settings.
    -   Software: Software specific information/settings, often by make
        first
        -   Microsoft\\\\Windows\\\\CurrentVersion
            -   ProgramFilesDir: Change the default dir for new programs
                here.
            -   Sourcepath: (string) Windows uses this key or the one
                under the Setup key below as a source for the
                Windows CD. Copy your i386 dir on your Windows CD and
                set this key accordingly and you will no longer have to
                insert your Windows CD when Windows requires files from
                it.
            -   Setup
                -   Sourcepath: (string) Some apps use the key here
                    instead of the one detailed above; set both to
                    reflect you i386 folder location.
            -   CommonFilesDir: Location of the Common files dir.
                Default is c:\\\\program files\\\\Common files
            -   Netcache: Settings relating to offline folders; entries
                here are often put there by Group Policy in Computer
                Configuration\\\\Administrative
                Templates\\\\Network\\\\Offline Files folder.
                -   Enabled: (0 or 1) Disables or enables and restricts
                    the user from changing the setting.
                -   NoCacheViewer: (0 or 1) Disables the \'Offline
                    Files\' folder although it is still enabled through
                    using the network drives offline.
                -   NoReminders: (0 or 1) Disables reminders to
                    synchronise. Ensure this is set to 1 if you have it
                    disabled it via editing the registry - it can cause
                    problems otherwise.
                -   FormatDatabase: (1) If there is corruption in the
                    offline files/CSC database and the Offline Files tab
                    cannot be accesed, create this key. The actual value
                    is ignored; upon rebooting Windows will clear the
                    CSC database and del the key.
            -   DateTime\\\\Servers: Time server for synchronising your
                time are set here, use sub-keys with the names or 1,2,3,
                etc to set preference.
        -   Explorer
            -   Desktop\\\\NameSpace: Listed here GUIDS for CLASS IDs
                for icons/functions to appear on the Desktop. These are
                usually used by Windows itself, for example My Documents
                is listed here. See also: [Create custom System Folder
                on Desktop/My Computer
                (Windows)](Create_custom_System_Folder_on_Desktop/My_Computer_(Windows) "wikilink")
            -   MyComputer\\\\Namespace: Listed here GUIDS for CLASS IDs
                for icons/functions to appear within My Compurer. For
                example Control Panel has an entry here. See also:
                [Create custom System Folder on Desktop/My Computer
                (Windows)](Create_custom_System_Folder_on_Desktop/My_Computer_(Windows) "wikilink")
            -   EnableBalloonTips: (0 or 1)
            -   FolderContentsInfoTip: (0 or 1) Disable folder stats on
                mouse hover.
            -   StartButtonBalloonTip: (0 or 1) Disable Start Menu mouse
                hover tips.
            -   InternetOpenWith: (0 or 1) Allows the disabling of the
                web service dialog when a file of an unknown type is
                opened - opening with Open With dialog instead. SK/UK
            -   PersistBrowsers: (0 or 1) With this enabled Windows will
                reopen and directories that were open when shutting
                down. - A little like sesion saving with X Window but
                for directory listings only.
            -   ThumbnailSize: (height in pixels) This settings
                specifies the size of the thumbnails in the thumbnail
                view - this is useful if you have a large screen
                resolution and your thumbnails are too small. Windows
                may need to be restarted for the changes make to take
                effect.
            -   ThumbnailQuality: (percent) Setting this will decrease
                the thumbnail size by (100-thumbnail\_quality)% and blow
                it up to the size in the ThumbnailSize key. Pixelation
                is blurred.
            -   AlwaysUnloadDLL: (0 or 1) Windows caches DLLs in use by
                a programme after it has quit for a while. It benefit is
                lost on low-memory for heavy-load systems, disable it by
                setting the key to 1.
        -   Policies:
            -   DontDisplayLastUserName: (0 or 1) Set this to 1 and upon
                relogging in the last user name to do will not be shown.
            -   VerboseStatus: (0 or 1) When enababled this will show
                verbose information when logging on or off or booting up
                or shutting down. Useful for dignosing slow startups.
            -   Explorer:
                -   ClassicShell: (0 or 1) Set to 1 to disable most of
                    the Windows 98+ features in Explorer. Features
                    including Active Desktop, Web & thumbnail views will
                    be disabled. SK/UK
                -   NoDriveTypeAutoRun: dword:000000ff Disable autorun
                    for CDs.
                -   NoSaveSettings: (0 or 1) Check this key if your
                    profile is not saving, or use it under HKCU for a
                    standardised login/layout.
                -   MemCheckBoxInRunDlg: (0 or 1) Show the run in
                    seperate memory space option in the run dialog box.
                    This is useful if you fdind your 16-bit apps have
                    never run properly from Win2k onwards as running the
                    virtual DOS machine in sandbox mode might allow it
                    run properly.
        -   OptimalLayout
            -   EnableAutoLayout: (0 or 1) Auto moves data on your disk
                when idle so that frequently used drivers/programmes are
                quicker to access.
        -   Microsoft\\\\Windows CE Services: Settings in realtion to
            PDAs/smartphone, typically with regard to ActiveSync.
            -   GuestOnly: (0 or 1) Set to 1 to disable the ability to
                create new partnerships.
            -   AppMgr
                -   SilentInstall: (0 or 1) Set to 0 to stop the
                    ActiveSyncinstalling whenever the device is
                    connected, also delete the key below:
            -   AutoStartOnConnect
                -   CEAppMgr: (string) Use this key if you wish to set a
                    third-party app back to use the PDA/smartphone after
                    ActiveSync has installed itself over the top.
        -   Microsoft\\\\Windows NT\\\\CurrentVersion
            -   Setup
                -   Diagnostics: *Read this if you intend to apply these
                    keys to Windows Server 2003: [MS KB
                    889088](http://support.microsoft.com/kb/889088)*
                    -   RunDiagnosticLoggingGlobal: Enable user
                        environment event logging
                    -   RunDiagnosticLoggingGroupPolicy: Enable event
                        logging for group policies only
                    -   RunDiagnosticLoggingAppDeploy: Enable event
                        logging for GPO application deployment only
                    -   RunDiagnosticLoggingIntelliMirror: Enable event
                        logging for remote boot only
                -   RecoveryConsole
                    -   SetCommand: (0=disallow 1=allow) Allow access to
                        HDs and floppy drive from the recovery console.
            -   Winlogon
                -   PasswordExpiryWarning: (no of days in DWORD)
                -   LogonType: (0 or 1) This value is 0 by default for
                    Win2k/XP Pro and 1 for XP Home. If you have XP Home
                    but miss the Ctrl+Alt+Del functions of XP Pro then
                    this is a good key to know.
                -   AllowMultipleTSSessions: (0 or 1) Enables fast user
                    switching thus without having to close any
                    programmes.
                -   Welcome: (string) Use this key to append text to the
                    end of the logon and security dialog titles.
                -   ForceAutoLogon: (0 or 1) With the auto logon feature
                    enabled it can be disabled on a per-session basis my
                    holding shift - this key disables that ability.
                -   LegalNoticeText: (string) create a dialog box before
                    logging on that the users have to click past, whch
                    can be used for legal notices but is also used for
                    system announcements in some environments.
                -   LegalNoticeCaption: (string) Set the title for the
                    legal notice window.
                -   ScreenSaverGracePeriod: (string inseconds) This
                    setting determines how many seconds after the
                    screensaver appears that the machine should be
                    locked if it is enabled.
            -   WPAEvents
                -   OOBETimer: (binary) This key is a hash of your
                    Windows product key. Tools which can read the
                    product key on your PC decode this. Change one of
                    the values in this key to deactivate Windows to
                    allow a new key to be entered. See also: [Change
                    Product Key (Windows
                    XP)](Change_Product_Key_(Windows_XP) "wikilink")
        -   Policies:
            -   System
                -   ReadOnlyProfile: (0 or 1) Disables the saving of the
                    profile.
    -   System: Contains information on which device drivers should be
        loaded at startup, it is populated from
        systemroot\\\\System32\\\\Config\\\\System. NTLDR uses this hive
        to ascertain which device drivers need to be loaded during
        startup. Each configuration of device drivers is stored under
        ControlSetxxx. Other subkeys include:
        -   CurrentControlSet: A pointer to a ControlSetxxx - the one
            currently in use.
            -   Control
                -   FileSystem
                    -   NtfsDisable8dot3NameCreation: (0 or 1) 2000/XP
                        still creates 8dot3 filenames for backwards
                        compatibility with apps that do not support
                        Windows 95+. If none of your apps are that old
                        set this key to 1 to improve performance.
                    -   NtfsDisableLastAccessUpdate: (0 or 1) Disable
                        updating of the last accessed timestamp to
                        improve performance. Updating of other
                        timestamps is unaffected.
                -   Class\\\\{36FC9E60-C465-11CF-8056-444553540000}\\\\0000
                    -   IdleEnable: (0 or 1) Set this to one to increase
                        the USB polling inerval. This is useful for
                        laptops as it allows a better standby.
                -   Terminal Server
                    -   Winstations
                        -   RDP-Tcp
                            -   Portnumber: The default port for
                                terminal services / remote desktop;
                                useful for hardening security by
                                changing the standard port, 3389. See
                                also: [Change Remote Desktop listening
                                port
                                (MyDigitalLife)](http://www.mydigitallife.info/2006/12/04/modify-and-change-remote-desktop-listening-port/)
            -   Session Manager
                -   SafeDllSearchMode: Change the search order for a
                    required DLL for a pgoramme. 1 = search Windows dirs
                    first, 0 = current dir first.
                -   Memory Management
                    -   SystemPages: This key relfects the number of
                        page table entries, if you find your system is
                        crashing under heavy I/O loads this could fix
                        it.
                    -   DisablePagingExecutive: (0 or 1) Systems with a
                        large amount of RAM can easily incrase system
                        performance by forcing Windows to not page its
                        core systems - the Windows Executive.
                    -   ClearPageFileAtShutdown: (0 or 1) Heavy load
                        systems will benefit from a fresh page file and
                        it makes it harder for hackers to try and mine
                        passwords from it.
                    -   LargeSystemCache: (DWORD 0=desktops 1=servers)
                        Control the memory dedicated for file caching.
                        Desktops tend to be optimal when more memory is
                        for apps - the reverse is true for servers
                        although setting this value to 1 on a desktop
                        could speed it up.
                -   Subsystems
                    -   Optional: The session manager loads OS/2 and
                        Posix when they are rarely used. You can disable
                        both sub systems from removing \"Posix\" from
                        the key. Leave \"OS/2\" in the key if it is
                        there.
        -   Services
            -   Tcpip
                -   Parameters
                    -   DisableTaskOffload: (0 or 1) Set this to 0 to
                        use the CPU within your NIC if it has one; this
                        slightly reduces the load on your CPU.
        -   Select: Information on which ControlSet is chosen when:
            -   Default: The CS that will be used/attempted on the next
                bootup
            -   Current
            -   Failed: If 0 then no fail has ever occured - otherwise
                this states a config that has previously failed.
            -   LastKnownGood: Points to the CS that was used during the
                last user session.
-   **HKEY\_USERS:** Contains all user profiles stored by their SID, you
    should only require use of this key if you want to edit the registry
    of a user whilst not logged on as the user. HKEY\_CURRENT\_USER
    points to the SID of the user currently logged on and
    HKEY\_CLASSES\_ROOT points to the \"<SID>\_Classes\" key (along with
    HKEY\_LOCAL\_MACHINE\\\\SOFTWARE\\\\Classes.)
    -   .DEFAULT: The profile windows uses at the login prompt/GINA
        chain and the default profile when new users are created.

[Category:Windows](Category:Windows "wikilink")
