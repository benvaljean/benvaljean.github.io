---
layout: post 
title: Change Product Key (Windows XP)
---

If Windows Update or Genuine check is complaining about an non-genuine
install of Windows and you have a legit key it can be changed by
following these steps:

1.  Change one of the values in this key to deactivate Windows:
    HKLM\\\\Software\\\\Microsoft\\\\WindowsNT\\\\CurrentVersion\\\\WPAEvents
2.  Run this command-line to force a reactivation:
    %systemroot%\\\\system32\\\\oobe\\\\msoobe.exe /a
3.  Choose the option: Yes, I want to telephone a customer service
    representative to activate Windows
4.  Click: Change Product key, after which the programme can be closed -
    the wizard does not have to finish.

You may need to reboot before you can start using Windows Update etc.

### See Also

[KB328874](http://support.microsoft.com/kb/328874) \[test\|Change
Product Key (Windows XP)\]
