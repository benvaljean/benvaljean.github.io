---
layout: post 
title: Settings permission for an Exchange database / Granting access to all mailboxes (Exchange 2007)
---

In [Microsoft Exchange
2007](http://technet.microsoft.com/en-us/library/bb124558.aspx) it is
often a requirement to grant access at the database level - granting
access to all mailboxes and all subsequent mailboxes that are created.
Unlike Exchange 2003, there is no ability to use the GUI to achieve
this.

There are numerous pages online giving details on how to achieve this -
but none of which worked for me so I thought I should write my own.
Start with method 1 and continue if it does not work.

### Method 1: Use cmdlets in the Exchange Management Shell

The
[EMS](http://blogs.msdn.com/exchangefaqs/archive/2008/01/23/exchange-management-shell.aspx)
has a command to set AD permissions:

    Get-MailboxDatabase|Set-ADPermission -user "domain\\user" -ExtendedRights right1 right2 etc.

To ascertain what permissions to add it is possible to get the
permissions of the domain admin user:

    Get-MailboxDatabase|Get-ADPermission -user "domain\\administrator"

    Identity             User           Deny  Inherited Rights
    --------             ----           ----  --------- ------
    EX11\\First Storag... domain\\Admi... True  True      Send-As
    EX11\\First Storag... domain\\Admi... True  True      Receive-As
    EX11\\First Storag... domain\\Admi... True  True      CreateChild, Delet...
    EX11\\First Storag... domain\\Admi... False True      GenericAll

This indicates that
`Get-MailboxDatabase|Set-ADPermission -user "domain\\user" -ExtendedRights GenericAll`
should work but for an unkmown reason this did not work in my
environment.

*Note:* If there is \>1 mailbox database on the server the -identity
parameter can be used:
`-identity "server\\first storage group\\mailbox database"`

### Method 2: Use ADSI Editor or AD Explorer

Download
[ADSIEdit](http://computerperformance.co.uk/ScriptsGuy/adsi.zip) or [AD
Explorer](http://technet.microsoft.com/en-us/sysinternals/bb963907.aspx).
AD Explorer is better but requires .NET .

1.  Navigate to Configuration\\\\Services\\\\Microsoft
    Exchange\\\\organization-name\\\\Administrative Groups\\\\Exchange
    Administrative Group\\\\SERVERNAME.
2.  Go to the properties of this \'folder\' and choose the security tab.
    Add the user you wish to have access to all databases on this
    server, giving them full control rights. Ensure there are no deny
    attributes being inherited at the administrative group or
    organization level. By default Exchange administrators have deny
    rights applied.

It is not possible to give permissions to just a single database using
this method as if security is applied at a child level the option to
apply to child objects is disabled as ADSIEdit does not see the child
mailboxes.

### Links

[Can\'t use the Add-ADPermission cmdlet in Exchange
2007](http://social.technet.microsoft.com/forums/en-US/exchangesvradmin/thread/3b9615e2-6bdb-4ee6-8483-e78a4db702b1/)

[ADSI
Edit](http://computerperformance.co.uk/w2k3/utilities/adsi_edit.htm)

[Setting permission for a mailbox
database](http://www.petri.co.il/forums/archive/index.php/t-21233.html)

[Grant full mailbox access to all Exchange 2007 mailboxes (Experts
Exchange)](http://www.experts-exchange.com/Software/Server_Software/Email_Servers/Exchange/Q_23648247.html)

[Category:Exchange](Category:Exchange "wikilink")
