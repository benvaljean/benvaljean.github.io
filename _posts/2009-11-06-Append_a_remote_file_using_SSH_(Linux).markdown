---
layout: post 
title: Append a remote file using SSH (Linux)
---

scp cannot be used to append to a remote file, only replace it.

The line below will allow appending of a remote file with a local file
over an SSH connection:

    cat localfile | ssh user@host "cat >>remotefile"

This also allows the transfer of files onto a machine where scp is not
installed or broken.

[Category:Linux](Category:Linux "wikilink")
