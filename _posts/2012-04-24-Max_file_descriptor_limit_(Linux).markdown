---
layout: post 
title: Max file descriptor limit (Linux)
---

#### Get current limit

    $ cat /proc/sys/fs/file-max
    205076

#### Get current number of open files

    lsof|wc -l

#### Increase the max file descriptor limit

-   Edit /etc/sysctl.conf

<!-- -->

    fs.file-max = 331287

[Category:Linux](Category:Linux "wikilink")
