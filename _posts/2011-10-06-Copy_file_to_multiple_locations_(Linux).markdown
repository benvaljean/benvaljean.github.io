---
layout: post 
title: Copy file to multiple locations (Linux)
---

#### Background

Top copy a single file to multple destinations the following might be
attempted:

    $ cp file */
    cp: omitting directory: `subdir1/'
    cp: omitting directory: `subdir2/'
    cp: omitting directory: `subdir3/'

This happens because when expends it it looks like this:

    cp file subdir1/file subdir2/file subdir3/file 

This causes an error as there are multiple sources and the last
paramater is not a directory. - Multiple destinations is not supported
by `cp`.

#### Solution

Create a loop:

    for dest in $(find . -mindepth 1 -maxdepth 1 -type d);do; cp file $dest;done

[Category:Linux](Category:Linux "wikilink")
[Category:Bash](Category:Bash "wikilink")
