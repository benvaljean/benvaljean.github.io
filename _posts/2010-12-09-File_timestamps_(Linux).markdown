---
layout: post 
title: File timestamps (Linux)
---

#### Last modified time

-   Shown by default from `ls`, with `ls -l`

#### Last accessed time

-   Shown with `ls -lu`

#### Inode change time

-   Show with `ls -lc`
-   Often incorrectly reported as the creation time. It *can* refer to
    the creation time but the inode will be \'re-created\' by other
    operations such as chown, chmod, chgrp and mv.

[Category:Linux](Category:Linux "wikilink")
