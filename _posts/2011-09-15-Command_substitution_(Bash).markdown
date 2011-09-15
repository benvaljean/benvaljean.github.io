---
layout: post 
title: Command substitution (Bash)
---

Command substitution involves substituting a command with its output.
This can either be directly replaced as variable substitution on the
command-line or piped into a virtual file as file substitution. The
latter is useful when using command substition with a command that is
expecting a filename eg. cat.

#### Variable Subtitution

In **variable subtition** the output of the command directly replaces
the command.

-   Syntax: `$(command with arguments)`

<!-- -->

    $ echo Most recent file is: $(ls -ltr|tail -1)
    $ Most recent file is : -rwxr-xr-x 1 benyg benyg 4820 Sep 13 09:22 test.sh

#### File substitution

In **file substitution** the output of the command is inserted in a
virtual file and is substituting an argument that requires a filename.

-   Syntax: `<(command with arguments)`

<!-- -->

    $ echo $(date)
    Thu Sep 15 09:10:22 BST 2011
    $ cat $(date)
    cat: Thu: No such file or directory
    cat: Sep: No such file or directory
    cat: 15: No such file or directory
    cat: 09:10:28: No such file or directory
    cat: BST: No such file or directory
    cat: 2011: No such file or directory
    $ cat <(date)
    Thu Sep 15 09:10:37 BST 2011

[Category:Linux](Category:Linux "wikilink")
[Category:BASH](Category:BASH "wikilink")
