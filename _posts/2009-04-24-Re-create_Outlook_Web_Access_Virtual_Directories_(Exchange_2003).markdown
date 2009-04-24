---
layout: post 
title: Re-create Outlook Web Access Virtual Directories (Exchange 2003)
---

To re-create the Outlook Web Access (OWA) virtual directories in
Microsoft Exchange 2003 they should be deleted follwed by restarting the
IS and System attendant Exchange services. This can be perform with the
following commands:

    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/Exadmin
    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/Exchange
    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/ExchWeb
    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/Microsoft-Server-ActiveSync
    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/OMA
    cscript %windir%\\system32\\iisvdir.vbs /delete w3svc/1/root/Public
    cscript %systemdrive%\\inetpub\\adminscripts\\adsutil.vbs delete ds2mb
    net stop "microsoft exchange information store"
    net stop "microsoft exchange system attendant"
    net start "microsoft exchange system attendant"
    net start "microsoft exchange information store"
