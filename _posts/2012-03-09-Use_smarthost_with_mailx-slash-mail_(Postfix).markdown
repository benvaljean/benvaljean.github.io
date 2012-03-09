---
layout: post 
title: Use smarthost with mailx/mail (Postfix)
---

The client mailer mail /
[mailx](http://pubs.opengroup.org/onlinepubs/009604499/utilities/mailx.html)
with Postfix by default will contact the MTA directly from a MX record
lookup. If you are behind a firewall or otherwise cannot contact
external servers and require the user of an ISP of company-provided
relay the following syntax can be used:

    cat email_body | mail -s "subject" -S smtp=smtp.company.net -r from@address.com to@address.com

#### References

<http://superuser.com/questions/137461/does-mailx-send-mail-using-an-smtp-relay-or-does-it-directly-connect-to-the-targ>

[Category:Linux](Category:Linux "wikilink")
[Category:Postfix](Category:Postfix "wikilink")
