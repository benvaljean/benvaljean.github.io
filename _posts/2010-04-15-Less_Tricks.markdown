---
layout: post 
title: Less Tricks
---

To edit a file based on the VISUAL or EDITOR variables, or Vi by
default:

    v

Run a shell command, a `%` is substituted by the name of the file being
viewed:

    !command

To mark a position in a text file demoted by any single character:

    m<any single character>

To go back to a mark type a single apostrphe followed by the same single
character:

    '<any single character>

Go to to top of file:

    g

Go to bottom of file:

    G

Disable word wrap: *useful for big-column DB queries, -S is also a
parameter*

    -S

#### Searching tricks

To search for text that matches the pattern:

    /pattern

To search for lines that does NOT match the pattern:

    /!pattern

To only highlight text that matches the pattern and not move the
location of the first match (\^K means Ctrl-K) :

    /^Kpattern

To search BACKWARDS in a file for the pattern:

    ?pattern

Repeat last search:

    /

Repeat last search in the previous direction:

    N

[Category:Linux](Category:Linux "wikilink")
