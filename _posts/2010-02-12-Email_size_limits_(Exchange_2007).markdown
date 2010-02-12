---
layout: post 
title: Email size limits (Exchange 2007)
---

The maximum size of an email that can be sent or received can be set
either a Global, Connector, Server or indeed the individual user\'s
level. For most purposes it is best to set the limits at the Global
level to avoid confusion. The default global limit is 20Mb.

### Get/Set Global message limit

[EMS](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=01a441b9-4099-4c0f-b8e0-0831d4a2ca86):

    Get-TransportConfig

Look for the **MaxReceiveSize** and the **MaxSendSize**.

To set the global send and receive limits to 15Mb:

    Set-TransportConfig –maxsendsize "15Mb"
    Set-TransportConfig –maxreceivesize "15Mb"

[Category:Exchange](Category:Exchange "wikilink")
