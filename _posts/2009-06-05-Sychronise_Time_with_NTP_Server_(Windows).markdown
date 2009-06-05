---
layout: post 
title: Sychronise Time with NTP Server (Windows)
---

The Windows Time Service is an NTP client that can synchronise time
based on the value retrieved from an NTP server. The settings are in the
reg:
\[HKEY\_LOCAL\_MACHINE\\\\SYSTEM\\\\CurrentControlSet\\\\Services\\\\W32Time\]

For the UK, the NTP server of the Univerity of Manchester is used below:

    Windows Registry Editor Version 5.00

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time]
    "Description"="Maintains date and time synchronization on all clients and servers in the network. If this service is stopped, date and time synchronization will be unavailable. If this service is disabled, any services that explicitly depend on it will fail to start.

    "
    "DisplayName"="Windows Time"
    "ErrorControl"=dword:00000001
    "FailureActions"=hex:05,00,00,00,00,00,00,00,00,00,00,00,02,00,00,00,64,00,20,\\
      00,01,00,00,00,60,ea,00,00,01,00,00,00,60,ea,00,00
    "Group"=""
    "ImagePath"=hex(2):25,00,53,00,79,00,73,00,74,00,65,00,6d,00,52,00,6f,00,6f,00,\\
      74,00,25,00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,73,\\
      00,76,00,63,00,68,00,6f,00,73,00,74,00,2e,00,65,00,78,00,65,00,20,00,2d,00,\\
      6b,00,20,00,4c,00,6f,00,63,00,61,00,6c,00,53,00,65,00,72,00,76,00,69,00,63,\\
      00,65,00,00,00
    "Objectname"="NT AUTHORITY\\\\LocalService"
    "Start"=dword:00000002
    "Type"=dword:00000020

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time\\Config]
    "LastClockRate"=dword:0002625a
    "MinClockRate"=dword:000260d4
    "MaxClockRate"=dword:000263e0
    "FrequencyCorrectRate"=dword:00000004
    "PollAdjustFactor"=dword:00000005
    "LargePhaseOffset"=dword:02faf080
    "SpikeWatchPeriod"=dword:00000384
    "HoldPeriod"=dword:00000005
    "LocalClockDispersion"=dword:0000000a
    "EventLogFlags"=dword:00000002
    "PhaseCorrectRate"=dword:00000001
    "MinPollInterval"=dword:0000000a
    "MaxPollInterval"=dword:0000000f
    "MaxNegPhaseCorrection"=dword:ffffffff
    "MaxPosPhaseCorrection"=dword:ffffffff
    "UpdateInterval"=dword:00007530
    "AnnounceFlags"=dword:0000000a
    "MaxAllowedPhaseOffset"=dword:0000012c

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time\\Parameters]
    "ServiceMain"="SvchostEntry_W32Time"
    "ServiceDll"=hex(2):43,00,3a,00,5c,00,57,00,49,00,4e,00,44,00,4f,00,57,00,53,\\
      00,5c,00,73,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,77,00,33,00,\\
      32,00,74,00,69,00,6d,00,65,00,2e,00,64,00,6c,00,6c,00,00,00
    "Type"="NTP"
    "NtpServer"="ntp2d.mcc.ac.uk,0x1"

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time\\TimeProviders]

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time\\TimeProviders\\NtpClient]
    "Enabled"=dword:00000001
    "InputProvider"=dword:00000001
    "AllowNonstandardModeCombinations"=dword:00000001
    "CrossSiteSyncFlags"=dword:00000002
    "ResolvePeerBackoffMinutes"=dword:0000000f
    "ResolvePeerBackoffMaxTimes"=dword:00000007
    "CompatibilityFlags"=dword:80000000
    "EventLogFlags"=dword:00000001
    "LargeSampleSkew"=dword:00000003
    "DllName"="C:\\\\WINDOWS\\\\system32\\\\w32time.dll"
    "SpecialPollTimeRemaining"=hex(7):6e,00,74,00,70,00,32,00,64,00,2e,00,6d,00,63,\\
      00,63,00,2e,00,61,00,63,00,2e,00,75,00,6b,00,2c,00,37,00,61,00,65,00,38,00,\\
      39,00,33,00,61,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\\
      00,00,00,00,00
    "SpecialPollInterval"=dword:00000e10

    [HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\W32Time\\TimeProviders\\NtpServer]
    "InputProvider"=dword:00000000
    "AllowNonstandardModeCombinations"=dword:00000001
    "DllName"="C:\\\\WINDOWS\\\\system32\\\\w32time.dll"
    "Enabled"=dword:00000000

Other UK time servers:

    NTP Server Hostname      IP Address      Use DNS      Location      NTP Server Synchronisation
    chronos.csr.net     194.35.252.7     Yes     Computing Systems Research Ltd. UK     NTP V4 primary (Odetics GPS), Sun/Sparc Solaris 2.6
    ntp.my-inbox.co.uk     81.168.77.149     No     Falmouth, Cornwall, UK     NTP V4.2.0 primary (MSF Radio Clock Receiver), Trustix Linux 

    ntp2.sandvika.net      194.164.127.6      No      Telehouse Europe, London E14 UK      NTP V4 secondary Sun UltraSPARC Solaris 8
    ntp2d.mcc.ac.uk     130.88.203.12     Yes     University of Manchester, Manchester, UK     NTP secondary (S2), SGI/Irix
    ntp2c.mcc.ac.uk     130.88.200.4     Yes     University of Manchester, Manchester, UK     NTP secondary (S2), PC/FreeBSD
    ntp.exnet.com     194.207.34.9     Yes     ExNet Ltd, London, UK     NTP secondary (stratum 2), Sun-4/Unix
    audaxsystems.co.uk     193.201.200.83     Yes     Interhouse London E14 UK     NTP V4, SuSE 9.0 (Stratum 1)
    ntp1.sandvika.net     194.164.127.5     No     

    Telehouse Europe, London E14 UK
        NTP V4 secondary Sun UltraSPARC Solaris 8
    ntp.cis.strath.ac.uk           Yes     University of Strathclyde, Glasgow, UK     NTP V4 secondary
    ntp0.sandvika.net     194.164.127.4     No     Telehouse Europe, London E14 UK     NTP V4 secondary Sun UltraSPARC Solaris 8 

From
<http://www.atomic-clock.galleon.eu.com/ntp-servers/time/ntp-servers-uk.html>

### See Also

<http://support.microsoft.com/kb/816042>
