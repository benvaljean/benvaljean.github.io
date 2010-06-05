---
layout: post 
title: Can't open /dev/tty: No such device or address Error (Linux)
---

### Symptoms

1\. When attempting a command which requires input from the console the
following error could occur:

:   can't open /dev/tty: No such device or address

2\. When attempting to ssh the following error is given, even when SSHing
to localhost:

:   Host key verification failed.

:   When running `ssh -vvv user@localhost` the exact debug line relating
    to this issue is:
    `debug1: read_passphrase: can't open /dev/tty: No such device or address`.

3\. SFTP fails with the following error in auth.log:

    error: open /dev/tty failed - could not set controlling tty: No such file or directory

### Cause

The /dev/tty \'special file\' has been removed.

### Solution

    mknod -m 644 /dev/tty c 5 0

This creates /dev/tty but only allows root to use it, run
`chmod a+rw /dev/tty`

[Category:Linux](Category:Linux "wikilink")
