---
layout: post 
title: Allow Out of Office replies to external addresses (Exchange 2003)
---

![Allowing external Out of Office
replies](AllowOOOExternal.JPG "fig:Allowing external Out of Office replies"){width="500"}
Contrary to popular belief, by default Out of Office auto replies will
only be sent to internal email addresses of the domain - not to
addresses outside of the organisation. To allow Out of Office auto
replies to be sent to external addresses:

1.  Open
    \[<http://technet.microsoft.com/en-us/library/aa995785(EXCHG.65>).aspx
    Exchange System Manager\]: Go to Start \> Programs \> Microsoft
    Exchange \> System Manager.
2.  Expand **Global Settings** and click on **Internet Message formats**
3.  Choose the entry for your domain or choose **Default**, right click
    and go to **Properties**.
4.  Go to the Advanced tab, and tick **Allow out of office responses**.

Please note: This setting will only apply to **new** Out of office
messages set; for this to apply to users currenty set to out of office
it will need to be turned off and back on.

### See Also

-   \[Limit Out of Office auto replies to specific senders/external
    users (Outlook)\]
-   [1](http://www.smallbizserver.net/Default.aspx?tabid=53&forumid=5&postid=55615&view=topic)

[Category:Windows](Category:Windows "wikilink")
