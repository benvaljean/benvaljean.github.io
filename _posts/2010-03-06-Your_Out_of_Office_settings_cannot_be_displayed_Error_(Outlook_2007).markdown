---
layout: post 
title: Your Out of Office settings cannot be displayed Error (Outlook 2007)
---

#### Symptom

Outlook 2007 users on Exchange 2007 can receive the following when
attempting to access the Out of Office settings:

    Your Out of Office settings cannot be displayed, because the server is currently unavailable. Try again Later.

#### Cause

This error can occur due to one or both of the following causes:

1.  The permissions are incorrect on the /EWS virtual directory.
2.  A mismatch between the host name used to access the website and the
    host name on the SSL certificate itself.

#### Resolution

Cause 1: Anonymous access must be disabled on the /EWS virtual
directory.

Cause 2: See [Security certificate is invalid or does not match the name
of the site Error (Outlook
2007)\#Solution](Security_certificate_is_invalid_or_does_not_match_the_name_of_the_site_Error_(Outlook_2007)#Solution "wikilink")

[Category:Outlook](Category:Outlook "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
