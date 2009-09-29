---
layout: post 
title: Couldn't open /dev/null Error (Linux)
---

### Symptom

When using any command or application (such as ssh or scp) that writes
to /dev/null the following error could occur:

    Couldn't open /dev/null

### Cause

The permissions for the /dev/null device/special file do not allow
writing to it.

### Resolution

Alter the permissions using chmod, as root:

    chmod a+rw /dev/tty

[Category:Linux](Category:Linux "wikilink")
