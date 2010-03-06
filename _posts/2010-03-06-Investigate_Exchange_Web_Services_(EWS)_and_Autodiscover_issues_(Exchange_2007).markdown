---
layout: post 
title: Investigate Exchange Web Services (EWS) and Autodiscover issues (Exchange 2007)
---

EWS refers to the functions of IIS on a CAS Server that are used by the
Outlook client, this is separate to OWA. EWS handles Free/busy,OOO,OAB
and RPC.

Right-clicking on the Outlook 2007 tray icon and choosing Test email
Autoconfig tests general autodiscover connectivity. It does not test
EWS.

The [EMS](http://technet.microsoft.com/en-us/library/bb123778.aspx)
command Test-OutlookWebServices tests EWS.

Usage is Test-OutlookWebServices -identity user\|fl Example of correct
output:

    PS C:\\Program Files\\Microsoft\\Exchange Server\\Bin> Test-OutlookWebServices -identity
    benjaming|fl


    Id      : 1003
    Type    : Information
    Message : About to test AutoDiscover with the e-mail address benjaming@companyabc.com
              .

    Id      : 1006
    Type    : Information
    Message : Contacted AutoDiscover at https://ivy.jgp.co.uk/Autodiscover/Autodiscover.
              xml.

    Id      : 1016
    Type    : Success
    Message : [EXCH]-Successfully contacted the AS service at https://webmail.companyabc.com/EWS/
              Exchange.asmx.

    Id      : 1015
    Type    : Success
    Message : [EXCH]-Successfully contacted the OAB service at https://webmail.companyabc.com/EWS
              /Exchange.asmx.

    Id      : 1005
    Type    : Error
    Message : When accessing https://ex-cas.companyabc.local/UnifiedMessaging/Service.as
              mx the error "RemoteCertificateNameMismatch:CN=ivy.jgp.co.uk, OU=IT, O=Job
              s Go Public, L=London, S=London, C=GB" was reported.

    Id      : 1014
    Type    : Success
    Message : [EXCH]-Successfully contacted the UM service at https://ex-cas.companyabc.local
              /UnifiedMessaging/Service.asmx.

    Id      : 1016
    Type    : Success
    Message : [EXPR]-Successfully contacted the AS service at https://webmail.companyabc.com/EWS/
              Exchange.asmx.

    Id      : 1015
    Type    : Success
    Message : [EXPR]-Successfully contacted the OAB service at https://webmail.companyabc.com/EWS
              /Exchange.asmx.

    Id      : 1014
    Type    : Information
    Message : [EXPR]-The UM is not configured for this user.

    Id      : 1017
    Type    : Success
    Message : [EXPR]-Successfully contacted the RPC/HTTP service at https://webmail.companyabc.com
              /Rpc.

    Id      : 1006
    Type    : Success
    Message : Successfully tested AutoDiscover.

The [Your Out of Office settings cannot be
displayed](Your_Out_of_Office_settings_cannot_be_displayed_Error_(Outlook_2007) "wikilink")
issue presented a 401 error occurring, leading to the solution detailed
above.

[Category:Exchange](Category:Exchange "wikilink")
