---
layout: post 
title: Sourcing variables from other files using Source command (Bash)
---

When a child process is started from a BASH script any evironment
variables are lost created or changed in the child are *lost*. If the
process or script is called using the source command (abbreviated to a
full-stop) a child process is created and variable changes or additions
are *not lost*.

bg1.sh:

    place=Monaco

bg2.sh:

    bg1.sh
    echo "Place is: $place"
    # Outputs "Place is: "   as the variable was set in a different (child) process
    . bg1.sh
    echo "Place is: $place"
    # Outputs "Place is: Monaco" as the variable was set in the same process.

[Category:Linux](Category:Linux "wikilink")
