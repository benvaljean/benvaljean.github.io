---
layout: post 
title: Exmerge Error CADRoutines::GetNamingContextData (Exchange)
---

![Forcing an update to the Exchange Recipient Update
Service](RUS.JPG "fig:Forcing an update to the Exchange Recipient Update Service"){width="500"}
When attempting to either import a PST file into an Exchange mailbox; or
exporting data to a PST file through using Exmerge the following error
can occur:

**CADRoutines::GetNamingContextData**

To troubleshoot this issue:

-   Check that the user attempting the Exmerge has the appropriate
    permissions: [Exmerge error 0x8004011d
    (Exchange)](Exmerge_error_0x8004011d_(Exchange) "wikilink")
-   Ensure both the mailboxes are visible in the
    [GAL](Global_Address_List_(Exchange) "wikilink") - this is most
    likely to be the cause

If the issue still occurs the Recipient Update Service may need to be
manually updated:

1.  Open **Exchange System Manager**
2.  Under **Recipient Update Services** choose the Recipient Update
    Service for your domain.
3.  Right click and choose **Update now**.

If the above does not work try Rebulid. In a large environment it may be
required to Update/Rebulid the enterprise Recipient Update Service.

[Category:Windows](Category:Windows "wikilink")
