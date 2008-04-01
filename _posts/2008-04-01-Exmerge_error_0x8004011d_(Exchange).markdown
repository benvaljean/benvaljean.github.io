---
layout: post 
title: Exmerge error 0x8004011d (Exchange)
---

When attempting to either import a PST file into an Exchange mailbox; or
exporting data to a PST file through using Exmerge the following error
is not uncommon:

**Error opening message store (EMS). Verify that the Microsoft Exchange
Information Store service is running and that you have the correct
permissions to log on. - 0x8004011d**

Before troubleshooting this error check the following:

1.  The Information Store Service is running and the relavant mailbox
    store is mounted.
2.  If extracting to/importing from a mailbox in the Recovery Storage
    group ensure the mailbox has not been moved.

If the above potential issues have been ruled out the most likely cause
is that the user performing the Exmerge does not have the necessary
permissions to read/write to the mailbox. **Contrary to popular opinion,
by default Exchange Full Administrators cannot read every mailbox in a
domain.**

To setup the required permissions it is reccomened to create a new user
for this purpose as:

:\#Depending on the internal metrics of your organisation it may not the
appropriate to allow all users of the Domain Admins or Enterprise Admins
group access to all the mailboxes.

:\#By default, the Enterprise Admins and Domain Admins group have Allow
and Deny rights for Send As and Receive As permissions on the Mailbox
store(s). These rights are required for Exmerge to function and it may
not be a good idea to alter the default, inherited permissions.

To create a new account and give it access to all mailboxes:

1.  Create a normal account, do not add it to any administrative groups.
2.  Give the account Full Control to the mailbox store:
    1.  From **Exchange System Manager** right-click the relavant
        mailbox store, choose properties and the **Security** tab.
    2.  Add the new user and give it Full Control to the database,
        ensure that Send As and Receive As are ticked, under **Allow**.

Depending on the configuration of your network changes made can take up
to 15 minutes totake effect.
