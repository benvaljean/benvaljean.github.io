---
layout: post 
title: Global Address List not updating (Outlook)
---

### Symptom

The GAL (Global Address List) does not update on a Outlook client
despite changes/new addresses appearing on other machines.

### Cause

Outlook is not updating the OAL (Offline Address List) with the new data
from the GAL.

### Resolution

-   Ensure cached exchange mode is not enabled, if it is then changes to
    the Offline Address List (wich is used as the GAL in cached Mode) is
    just updated once every 24 hours and in most cases early in the
    morning. When the Offline Address List is updated it has to be
    downloaded by Outlook for you to see the changes, and that is also
    just done automatically once every 24 hours, making a total of 48
    hours in some cases.

<!-- -->

-   Another option is to set the
    HKCU\\\\software\\\\policies\\\\microsoft\\\\office\\\\<version>\\\\outlook\\\\cached
    mode\\\\DownloadOAB setting to 0 on the client. This will prevent
    the OAB from being downloaded to the client and i belive outlook
    2003 in cached mode will hit the GAL if no OAB is available.

<!-- -->

-   **OR**: [Manually Update Your Local Copy of The Global Address
    List](http://www.depts.ttu.edu/helpcentral/directions/update_gal.php)

[Category:Outlook](Category:Outlook "wikilink")
