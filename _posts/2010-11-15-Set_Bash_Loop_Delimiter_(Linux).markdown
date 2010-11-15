---
layout: post 
title: Set Bash Loop Delimiter (Linux)
---

BASH loops use a space as a delimiter by default but this is not useful
when iterating through lines in a text file for instance. The
environment variable `$IFS` sets the delimiter.

-   Be careful not to break any scripts that use a bash loop in the
    default way.

Set the bash loop delimiter to a new line:

    IFS=$'\
    '

[Category:Linux](Category:Linux "wikilink")
