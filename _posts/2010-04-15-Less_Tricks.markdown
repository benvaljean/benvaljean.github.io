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

Go 50% into the file:

    50p

Disable word wrap: *useful for big-column DB queries, -S is also a
parameter*

    -S

Show/hide line numbers:

    -N

Show new lines, \'forever\' mode, similar to \'tail -f\':

    F

#### Using multiple files

Less can open mutliple files at once, where additional features can be
utilised:

    less file1 file2 file3

Go to next file: `:n`\
Go to previous file:`:p`\
Search across multiple files:

    /*pattern

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

#### Add a useful prompt

Add the following to your .bashrc for a more useful prompt with
additional information:

    alias less='less -P "?f%f .?m(file %i of %m) .?ltlines %lt-%lb?L/%L. . byte %bB?s/%s. ?e(END) :?pB%pB\\%..%t"'

#### See Also

[About.com: less](http://linux.about.com/library/cmd/blcmdl1_less.htm)

[Category:Linux](Category:Linux "wikilink")
