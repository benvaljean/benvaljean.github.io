---
layout: post 
title: Bounce when Sending Meeting Request (Outlook)
---

### Symptom

When sending a meeting request in an environment that uses Microsoft
Outlook with Exchange to a sent or when the accept or deny it a bounce
is returned to the person who sent the meeting request. The option in
Outlook that allows other users to receive meeting requests and
accpet/reject them on another user\'s behalf is called
[delegates](https://exchange.sandi.net/info/pdf/How%20to%20configure%20Outlook%20delegates%20in%20windows.pdf).
This delgates option in Outlook is either ghosted - suggesting that no
delegates actually exist.

### Cause

The back-end of delgates is setup through a hidden server-side rule in
Outlook. As this is not monitored by Active Directory if the user that
was a delgate leaves the company and is subsequently deleted the rule
will still exist but not be picked up by the Outlook interface - the
area appears ghosted. However the rule in the back-end still exists and
meeting requested are still forwarded resulting in a 5.1.1 Non-Delivery
Report / Bounce being received by the user who sent the request - this
is known as an **orphaned delegate**.

### Resolution

1.  Open up delgates by going to **Tools** \> **Options** menu and
    clicking on the **Delegates** tab.
2.  Click add and add any user at all to be a delegate - I would
    recommend of course that this if you are in IT Support and fixing
    this for another user. This is only temporary and will allow a
    required option to become un-ghosted.
3.  Click OK back to the main Outlook window and restart Outlook. Ensure
    that the process is not running in the background before it is
    reatarted. To do this:
    1.  Press Ctrl+Alt+Delete and click on Task Manager. Task Managert
        may appear automatically after pressing Ctrl+Alt+Del depending
        on your setup.
    2.  Look for **OUTLOOK.EXE**; if it is present highlight it and
        click **End Process**.
4.  When restarting Outlook go back to the delegates window and uncheck
    **Send meeting requests and responses only to my delegates, not to
    me**.
5.  The delegate that was added can now be removed.
6.  Click OK back to the main window and restarted Outlook again and
    test.
7.  If the issue still remains the entry will need to be manually
    deleted using the message store utility viewer **MDBVU32.exe** that
    is on the Exchange CD.

### Deleting manually using mdbvu32

<font color=red>Performing these steps incorrectly can cause serious
damage to your Exchange server.</font>

1.  Ensure that Outlook is not running on any machine for the user who
    has the orphaned delegate.
2.  Start the Mdbvu32.exe utility, and then click OK in the first dialog
    box, to log on.
3.  Go to the **MDB** \> **OpenMessageStore** menu
4.  Click the relevant mailbox, and then click Open to start the store.
5.  Go to the **MDB** \> **Open Root Folder** menu
6.  Double-click Top of Information Store in the Child Folders area.
7.  Double-click Inbox in the Child Folders area to view the properties
    of the Inbox folder.
8.  Locate the Associated Message in FLD: pane of the MAPI\_FOLDER-Inbox
    window. Notice the items that start with \*pb EF 00 00 00 19 82 62.
    Each of these is a rule that is set up on the Inbox. The user can
    set up some of the rules. Other rules are for things like using the
    Out of Office Assistant or forwarding meeting responses to a
    delegate.
9.  Double-click each of the rules in turn, to open the rule and examine
    the rule to determine which rule is the delegate rule. Check the
    Message Property 0x65EB. The delegate rule should have the
    Schedule + EMS Interface for this property.
10. When you find the corresponding rule, check the message property
    **0x65EF**, which is a long, double-byte string of characters. If
    the string starts with 02, the rule states, \"Send meeting requests
    and responses only to my delegates, not to me.\" If the string
    starts with 01, the rule states, \"Delegate receives copies of
    meeting-related messages sent to me.\" If either of these options is
    set in Outlook, and there is no message or rule under Associated
    Message in FLD:, the rule no longer exists, which explains why the
    requests and responses are not being forwarded. You can also delete
    the delegate rule from here.
11. After you identify the delegate rule, select the rule in the
    Associated Message in FLD: pane of the MAPI\_FOLDER-Inbox window.
12. In the Operations available box, click **lpFld-\>DeleteMessages()**,
    and then click Call Function.
13. When the **MAPI\_FOLDER-Inbox-\>DeleteMessages()** window appears,
    click OK to delete the message.
14. Quit Mdbvu32.exe by closing all windows until you return to the MDB
    Viewer Test Application window.
15. Go to MDB \> Store Logoff.
16. Click OK in the LOGOFF\_COMPLETE window.
17. Close the MDB Viewer Test Application window.

### See Also

[Non-Delivery Report (NDR) / Bounce Codes
(Email)](Non-Delivery_Report_(NDR)_/_Bounce_Codes_(Email) "wikilink")\
[Meeting request to user produces bounce message from a deleted user
(Experts-Exchange)](http://www.experts-exchange.com/Software/Server_Software/Email_Servers/Exchange/Q_23340488.html)\
[Delegates
issues](http://winzenz.blogspot.com/2006/10/outlook-delegates-issues.html)\
[Granting delegate access to
email](http://ittraining.lse.ac.uk/Documentation/OnlineGuides/Delegate-Access.htm)

[Category:Exchange](Category:Exchange "wikilink")
[Category:Outlook](Category:Outlook "wikilink")
