---
layout: post 
title: Remove spaces or any character from a string (Bash)
---

Remove spaces or any character from a string (Bash)

#### Easy / Poor method

Use standard Bash variable / parameter expansion

-   Replace only the first space in a variable

<!-- -->

    test="123 456"
    echo ${test/ /}
    123456
    test="123  456"
    echo ${test/ /}
    123 456

#### tr method

Using tr will remove all spaces but is slightly untidy as it involve
invoking another command

-   Remove all spaces

<!-- -->

    echo "123    456" | tr -d ' '
    123456

#### Best method: advanced parameter expansion

-   Remove all spaces from a variable

<!-- -->

    test="123   456"
    echo ${test//[[:space:]]/}
    123456

This will also remove trailing and leading spaces.

[Category:Bash](Category:Bash "wikilink")
[Category:Linux](Category:Linux "wikilink")
