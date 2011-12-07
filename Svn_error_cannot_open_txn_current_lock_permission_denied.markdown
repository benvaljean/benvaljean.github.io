---
layout: post 
title: Svn: Can't open file '/mnt/svn/dns/db/txn-current-lock': Permission denied Error (SVN)
---

#### Symptom

When attempting to commit to a [SVN](SVN "wikilink") repo with svnserve
the following error can occur:

    svn: Can't open file 'db/txn-current-lock': Permission denied

#### Cause

The `txn-current-lock` file has the incorrect permissions - usually only
readable by root, or whatever user to ran the `svnadmin create` command
with.

#### Resolution

`txn-current-lock` probably needs to be writeable by user `svn` but if
you use xinet.d the user can be checked by examining `/etc/xinet.d/svn`.
Paths may vary depending on your package/distro.

-   To correct permissions if the user is `svn`

<!-- -->

    # chown root:svn db/txn-current-lock
    # chmod g+rw db/txn-current-lock

[Category: Linux](Category:_Linux "wikilink")
