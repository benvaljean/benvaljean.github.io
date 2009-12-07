---
layout: post 
title: Error -18597 in Entourage when connecting to Exchange 2007
---

### Symptoms

When attempting a Send/Receive in Entourage when using Exchange 2007 the
following error can appear:

\'\'The mail account is configured incorrectly in Entourage. Review the
mail account settings for typos and incorrect information (including
your own email address). On the Tools menu, click Accounts. In Accounts,
select the mail account and click Edit. The message has been moved to
your Drafts folder.

\'\'Account name: \"Exchange\"

\'\'Entourage is unable to access the mail account you are using with
the mail server configured for that account.

*Error: -18597*

### Cause

The cause could be one of the following:

1.  When connecting to Exchange the user\'s **primary smtp address**
    must be used. If another smtp address is used for the user the above
    error appears. Has a new recipient policy / default email address
    policy been applied?
2.  When installing Exchange 2007 SP2 the \'Require secure channel
    (SSL)\' option is enabled if not already done so. If Entourage is
    set to not use SSL the above error appears.

### Resolution

1.  In the Exchange account settings in Entourage always ensure that the
    primary smtp address of the user\'s mailbox is used. The primary
    smtp address if referred to the reply address in the Exchange 2007
    [EMC](http://technet.microsoft.com/en-us/library/bb123762.aspx). Go
    to the user\'s mailbox properties within \'Recipient Configuration\'
    to ascertain the correct smtp address.
2.  Either disable the forcing of SSL in IIS or setup Entourage to use
    SSL:

#### Disable the forcing of SSL in IIS for OWA

1.  Run %SystemRoot%\\\\system32\\\\inetsrv\\\\iis.msc
2.  For the \'exchange\', \'exchweb\', \'owa\' and \'public\' virtual
    folders: Right-click \> properties \> Directory Security \> Un-tick
    \'Require secure shannel (SSL)\' This configuration is not
    recommended and should never be used if port 80 is facing a WAN.

#### Setup Entourage to use SSL for Exchange

Select \'Use SSL for these Servers\' if creating the acc using the
assistant.

Or within account options ensure SSL is not ticked.

### See Also

-   [Entourage
    errors](http://web.archive.org/web/20080329152232/http://www.entourage.mvps.org/error/page.html)
-   [Entourage Error -18597 When Sending
    Email](http://knowledgebase.its.bethel.edu/articles/433/)
-   [Unable to send mails in entourage 2004 with OS
    X](http://www.tech-archive.net/Archive/Mac/microsoft.public.mac.office.entourage/2006-06/msg00337.html)
-   [Entourage and Exchange Server
    2007](http://benskelton.blogs.com/ben_skeltons_blog/2007/01/entourage_and_e.html)

[Category:Exchange](Category:Exchange "wikilink")
