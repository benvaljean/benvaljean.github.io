---
layout: post 
title: Exchange 2007 property cannot be set due to version 0.1 (8.0.535.0) or later required
---

### Symptoms

One of more of the following with regard to an Exchange mailbox:

-   Setting a Managed Folder Mailbox Policy using the
    [EMS](http://www.microsoft.com/downloads/details.aspx?familyid=1dc0f61b-d30f-44a2-882e-12ddd4ee09d2&displaylang=en)
    results in the error below. The Managed Folder Mailbox Policy tick
    box in the
    [EMC](http://technet.microsoft.com/en-us/library/bb123762.aspx) is
    also ghosted / greyed-out.

<!-- -->

    [PS] C:\\>Set-Mailbox -identity user -ManagedFolderMailboxPolicy "example policy"
    Set-Mailbox : Property ManagedFolderMailboxPolicy cannot be set on this object because it requires the object to have version 0.1 (8.0.535.0) or later.
    Current version of the object is 0.0 (6.5.6500.0).
    At line:1 char:12
    + Set-Mailbox  <<<< -identity user -ManagedFolderMailboxPolicy "example policy"

-   Accessing OWA results in an error: \"A problem occurred while trying
    to use your mailbox. Please contact technical support for your
    organization.\"

### Cause

The mailbox is a 2003 / legacy mailbox but Exchange is detecting it as a
2007 mailbox. The error message above is stating that 2007 or later is
required but the object is only 2003, normally this error is trapped
before this point as the interface will state that 2007 or later is
required.

### Resolution

From the
[EMS](http://www.microsoft.com/downloads/details.aspx?familyid=1dc0f61b-d30f-44a2-882e-12ddd4ee09d2&displaylang=en):

    Set-Mailbox user -applymandatoryproperties

### See Also

[Exchange 2007: Exception message: Property Languages cannot be set on
this object because it requires the object to have version 0.1
(8.0.535.0)
later](http://msexchangetips.blogspot.com/2008/04/exchange-2007-exception-message.html)

[Error message when users try to log on to Outlook Web Access in
Exchange 2007: \"A problem occurred while trying to use your
mailbox\"](http://www.digitalsupporttech.com/mskb/941/941146_Error_message_when_users_try_to_log_on_to_Outlook_Web_Access_in_Exchange_2007___quot_A_problem_occurred_while_trying_to_use_your_mailbox_quot_.htm)

[Can\'t open new mailboxes in
OWA](http://episteme.arstechnica.com/eve/forums?a=tpc&s=50009562&f=12009443&m=362006418831&r=606003038831)

[Category:Windows](Category:Windows "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
