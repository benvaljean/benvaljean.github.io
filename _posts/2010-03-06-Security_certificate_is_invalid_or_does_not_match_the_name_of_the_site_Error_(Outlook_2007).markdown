---
layout: post 
title: Security certificate is invalid or does not match the name of the site Error (Outlook 2007)
---

#### Symptom

Outlook 2007 users utilise \'autodiscover\' and consequently get a SSL
certificate error relating to a mismatch between the name on the SSL
certificate and the host name used to access Exchange:

    Information you exchange with this site cannot be viewed or changed by others.
    However, there is a problem with the site's security certificate.
       X   The name of the security certificate is invalid or does not match the name of the site

#### Cause

As Outlook is accessing SSL via an internal hostname such as
exchange-cas.companyabc.local on SSL that is setup for an external host
name such as webmail.companyabc.com the host names do not match and the
above error occurs.

#### Solution

The best solution for this is to change the InternalURL property for
various functions and also to set an internal DNS record for the
external host name, in this example webmail.companyabc.com . After which
the following must be done in EMS:

    Get-ClientAccessServer -Identity Ex-CAS-Server| FL
    Set-ClientAccessServer -Identity Ex-CAS-Server -AutoDiscoverServiceInternalUri https://webmail.companyabc.com/Autodiscover/Autodiscover.xml

    Get-WebServicesVirtualDirectory -Identity  “Ex-CAS-Server\\EWS (Default Web Site)”
    Set-WebServicesVirtualDirectory -Identity “Ex-CAS-Server\\EWS (Default Web Site)” -InternalURL https://webmail.companyabc.com/EWS/Exchange.asmx -BasicAuthentication:$true

    Get-OabVirtualDirectory -Identity "Ex-CAS-Server\\OAB (Default Web Site)"
    Set-OabVirtualDirectory -Identity "Ex-CAS-Server\\OAB (Default Web Site)" -InternalURL https://webmail.companyabc.com/OAB

-   SSL must be enabled on any the respective IIS subfolders, all have
    it enabled by default apart from OAB. 128-bit is required by the
    autodiscover app.
-   The Autodiscover dir must also have anon access un-ticked, else
    clients do not bother to authenticate and consequently hit the
    permissions which do not allow anon access.

[Category:Outlook](Category:Outlook "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
