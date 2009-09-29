---
layout: post 
title: Couldn't open /dev/null Error (Linux)
---

### Symptom

1\. When using any command or application (such as ssh or scp) that
writes to /dev/null the following error could occur:

    Couldn't open /dev/null

2\. When attempting to ssh the following error is given, even when SSHing
to localhost:

    Host key verification failed.

When running `ssh -vvv user@localhost` the exact debug line relating to
this issue is:
`debug1: read_passphrase: can't open /dev/tty: Permission denied`.

### Cause

The permissions for the /dev/null device/special file do not allow
writing to it.

### Resolution

Alter the permissions using chmod, as root:

    chmod a+rw /dev/tty

[Category:Linux](Category:Linux "wikilink")
