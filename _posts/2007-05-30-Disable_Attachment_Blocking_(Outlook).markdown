---
layout: post 
title: Disable Attachment Blocking (Outlook)
---

Outlook by default blocks certain attachments (file-types) from being
viewed for security reasons. Once blocked the file cannot be
\'un-quarantined\' and it can be more useful to disable the blocking at
the client-level and establish filtering at another level.

To disable blocking on a per-extension basis:

Locate the following key, where <version> is your version of Outlook:

`    [HKEY_CURRENT_USER\\Software\\Microsoft\\Office\\`<version>`\\Outlook\\Security]`

Create a new string key called \"Level1Remove\" and add the extnsion(s)
you wish to allow; seperating them with commas.

### See Also

[Attachments blocked by
Outlook](http://office.microsoft.com/en-us/outlook/HP030850041033.aspx)

[Registry](Registry "wikilink")

[Category:Outlook](Category:Outlook "wikilink")
