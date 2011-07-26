---
layout: post 
title: Remove sticky tags (CVS)
---

CVS can use sticky tags, which has similar functionality to a branch in
that it creates a separate working copy to each revision. It can cause
an error:

    cvs commit: sticky tag 'BG' for file xxx is not a branch

This happens when attempting to check in data against a tag - which is
not possible.

#### Remove a sticky tag

Backup any modified files that cannot be checked in due to the error
above and update the repo to the latest version of trunk:

    $ cd path/to/repo
    $ cvs update -A

[Category:Linux](Category:Linux "wikilink")
