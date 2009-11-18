---
layout: post 
title: Domain Controller is not advertising as a time server Error in dcdiag (Windows)
---

### Symptom

When performing a `dcdiag` on a Windows domain controller the following
error can appear:

    Starting test: Advertising
       The DC DC1 is advertising itself as a DC and having a DS.
       The DC DC1 is advertising as an LDAP server
       The DC DC1 is advertising as having a writeable directory
       The DC DC1 is advertising as a Key Distribution Center
       Warning: DC1 is not advertising as a time server.
       The DS DC1 is advertising as a GC.
       ......................... DC1 failed test Advertising

The exact command run to produce this test is:
`dcdiag /v /test:advertising`

### Cause

The dcdiag tool detects that the time service is either not running or
is running but not announcing itself as a reliable time server.

### Resolution

Try each of these solutions one step at a time, re-testing after
completing each step until the problem is resolved.

1.  Ensure the Windows Time service is running. On a DC is does far more
    than just synchronise time. It is also involved and required for AD
    replication.
        net start w32time

2.  Restart the Windows time service
        net stop w32time && net start w32time

3.  Check that Network problems are not stopping NTP form functioning.
    Note that Windows clients do not synchronise with the DCs via NTP,
    this only tests the ability for DC themselves to check an external
    time source:
        w32tm /stripchart /computer:time.windows.com /samples:2 /dataonly

    Error 0x800705B4 is a network timeout on the port - 123.
    `Time.winfows.com` should be replaced with the external time server
    you are using for a more complete test.

4.  Try:
         netdiag /fix

    `Netdiag` is part of [Windows Server 2003 Service Pack 1 Support
    Tools](http://support.microsoft.com/kb/892777). This can also be
    used on Server 2008.

5.  If you received the error message: `The service name is invalid`
    earlier the Windows Time service is not even registered.
    Re-registering the W32time service can also fix some issues so
    perform these steps anyway: [Re-registering the Windows Time
    Service](Domain_Controller_is_not_advertising_as_a_time_server_Error_in_dcdiag_(Windows)#Re-registering_the_Windows_Time_Service "wikilink")
6.  Try:
        w32tm /resync /redisscover

7.  Check that the DC has the PDC role:
        netdom query fsmo

    If it is run the following command:

        w32tm /config /manualpeerlist:time.windows.com /syncfromflags:manual /reliable:yes /update

    Microsoft\'s own free NTP server can be used as shown here, but I
    would recommend using one in your country if not in thr US. For the
    UK I can recommend `ntp2d.mcc.ac.uk` but there are many others.

8.  Ensure that the DC is announcing itself correctly through changing
    the `AnnounceFlags` are set correctly in the
    [Registry](Registry "wikilink"). Edit the
    `[HKLM\\SYSTEM\\CurrentControlSet\\Services\\w32time\\Config\\AnnounceFlags]`
    key to `a` (the letter a) in hexidecimal. To allow the w32time
    service read the config change:
        w32tm /config /update

#### Re-registering the Windows Time Service

    w32tm /unregister
    rem Ignore Access denied message if it appears and repeat
    w32tm /unregister
    w32tm /register
    rem Before the re-register command will work you may have to reboot.

This gives a vanilla set of settings, after which the service can be
restarted:

    net start w32time

If you receive an error message regarding SIDs then DC will need to be
rebooted again.

### See Also

-   \[<http://technet.microsoft.com/en-us/library/cc786897(WS.10>).aspx
    Configure the Windows Time service on the PDC emulator\]
-   [Windows Time Service Tools and
    Settings](http://go.microsoft.com/fwlink/?LinkId=42984)
-   [Windows Time Server -
    AnnounceFlags](http://www.experts-exchange.com/Hardware/Servers/Q_23905283.html)
