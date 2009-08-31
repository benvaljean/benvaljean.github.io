---
layout: post 
title: Exchange 2007 Server Roles
---

### Client access role

Very similar to FE role in Ex2000/2003. Handles OWA, POP3/IMAP and OMA.
Does not handle inbound/outbound smtp nor IMF.

### Edge transport role

Essentially a FE SMTP relay server to be placed in a DMZ and also does
anti-spam. Has to either not be a member of the domain or member of a
seperate domain then the other Exchange servers. If you use Postfix or
some other relay server than this role does not need to be implemented.

### Hub Transport role

This role does the traditional categorizer lookups for message flow that
used to be part of the BE role in Ex2000/2003. The server side part of
MAPI has been changed and is now called the \"(information) store
driver\". New feature message compliance allows native archiving
policies and among other features system-wide footers/disclaimers to be
added. The Edge transport agent can be installed to allow it to also act
as a FE SMTP relay server also.

### Mailbox server role

As BE server role in Ex2003 but can now be a true DB-only server.

### Unified Messaging role

Uses a PABX to provide additional telephone features such as accessing
emails and cancelling meeting requests etc. over the phone and emailing
VMs to users. This feature is about 5 - 10 years late as most users now
have emails on thier phones and a lot of companies deploy PBXs that
already send VMs via email.

### See also

<http://technet.microsoft.com/en-us/library/aa996319.aspx>

[Category:Exchange](Category:Exchange "wikilink")
