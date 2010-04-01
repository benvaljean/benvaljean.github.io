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

    Add-IPBlockListProvider -Name bl.spamcop.net -LookupDomain bl.spamcop.net -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://www.spamcop.net/w3m?action=checkblock&ip={0} for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name dnsbl.sorbs.net -LookupDomain dnsbl.sorbs.net -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://www.au.sorbs.net/lookup.shtml for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name zen.spamhaus.org -LookupDomain zen.spamhaus.org -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://www.spamhaus.org/query/bl?ip={0} for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name cbl.abuseat.org -LookupDomain cbl.abuseat.org -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://cbl.abuseat.org/lookup.cgi?ip={0} for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name b.barracudacentral.org -LookupDomain b.barracudacentral.org -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://barracudacentral.org/lookups/ip-reputation for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name spam.dnsbl.sorbs.net -LookupDomain spam.dnsbl.sorbs.net -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://www.au.sorbs.net/lookup.shtml for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name spam.rbl.msrbl.net -LookupDomain spam.rbl.msrbl.net -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://www.msrbl.com/check?ip={0} for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name bl.spamcannibal.org -LookupDomain bl.spamcannibal.org -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://spamcannibal.org/cannibal.cgi for further information. This organization has no control over this RBL (Realtime Block List)."
    Add-IPBlockListProvider -Name psbl.surriel.com -LookupDomain psbl.surriel.com -Enabled $True -RejectionResponse "{1} has blocked your IP address ({0}) using the list '{2}'. Please see http://psbl.surriel.com/listing?ip={0} for further information. This organization has no control over this RBL (Realtime Block List)."

### See Also

[Add-IPBlockListProvider
syntax](http://technet.microsoft.com/en-us/library/bb124358.aspx)

[EMS cmdlet
directory](http://www.powershellcommunity.org/Directories/Cmdlets.aspx)

[Multi RBL check](http://www.anti-abuse.org/multi-rbl-check/)

[Monitor the status of RBL listings for a specific IP address using
Nagios](Nagios#RBL_Status "wikilink")

[Category:Exchange](Category:Exchange "wikilink")
