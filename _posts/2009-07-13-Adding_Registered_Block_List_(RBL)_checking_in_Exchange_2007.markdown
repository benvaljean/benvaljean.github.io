---
layout: post 
title: Adding Registered Block List (RBL) checking in Exchange 2007
---

### Using the Exchange Management Console

Go to Orginization config \> Hub Transport \> Anti-spam tab \> IP Block
List Providers

### Using the Exchange Management Shell

Use the text below to add the most popular RBLs in bulk with customised
rejection responces. The default responce is not always helpful to a
non-technical user.

    Add-IPBlockListProvider -Name bl.spamcop.net -LookupDomain bl.spamcop.net -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://bl.spamcop.net . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name dnsbl.sorbs.net -LookupDomain zen.spamhaus.org -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.sorbs.net . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name zen.spamhaus.org -LookupDomain zen.spamhaus.org -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.spamhaus.org . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name cbl.abuseat.org -LookupDomain cbl.abuseat.org -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email systems IP address from your company is blacklisted at http://cbl.abuseat.org . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name b.barracudacentral.org -LookupDomain b.barracudacentral.org -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://b.barracudacentral.org . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name spam.dnsbl.sorbs.net -LookupDomain spam.dnsbl.sorbs.net -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.sorbs.net . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name spam.rbl.msrbl.net -LookupDomain spam.rbl.msrbl.net -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.msrbl.net . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name bl.spamcannibal.org -LookupDomain bl.spamcannibal.org -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.spamcannibal.org . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name psbl.surriel.com -LookupDomain psbl.surriel.com -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://psbl.surriel.com . Company ABC has no control over this RBL - Registered Block List."
    Add-IPBlockListProvider -Name ubl.unsubscore.com -LookupDomain ubl.unsubscore.com -AnyMatch $True -Enabled $True -RejectionResponse "An outbound email system IP address from your company is blacklisted at http://www.lashback.com/ubl.htm . Company ABC has no control over this RBL - Registered Block List."

### See Also

[Add-IPBlockListProvider
syntax](http://technet.microsoft.com/en-us/library/bb124358.aspx)

[EMS cmdlet
directory](http://www.powershellcommunity.org/Directories/Cmdlets.aspx)

[Multi RBL check](http://www.anti-abuse.org/multi-rbl-check/)

[Nagios](Nagios "wikilink")
