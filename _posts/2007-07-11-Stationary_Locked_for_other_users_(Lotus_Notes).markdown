---
layout: post 
title: Stationary Locked for other users (Lotus Notes)
---

![Stationary Locked for other
users](Stationarylocked_LotusNotes.JPG "Stationary Locked for other users")

### Symptom

When using a database in a business environment - a shared database - if
stationary is used by a particular user it will no longer be accessable
to other users until that database is closed; displaying the error
message to the right.

### Cause

This is the default behavious for Lotus Notes - it is by design.

### Resolution

Insert the line below into notes.ini:

    EDIT_NO_SOFT_LOCKS=1

### See Also

[Stationary remains locked until client close database (Notes
Forum)](http://www-1.ibm.com/support/docview.wss?rs=475&context=SSKTWP&context=SSKTMJ&q1=stationary+locked&uid=swg1LO08853&loc=en_US&cs=utf-8&lang=en)

\_\_NOTOC\_\_

[Category:Lotus Notes](Category:Lotus_Notes "wikilink")
