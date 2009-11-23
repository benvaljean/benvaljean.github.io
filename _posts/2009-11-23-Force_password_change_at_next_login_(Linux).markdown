---
layout: post 
title: Force password change at next login (Linux)
---

When creating a new user it can be necessary to force the user to change
the password for the temporary password given out.

To force a user to change their password upon their next login:

    chage -d 0 user

[Category:Linux](Category:Linux "wikilink")
