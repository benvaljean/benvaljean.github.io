---
layout: post 
title: Set default value script/function parameter (Bash)
---

`$1`, `$2` .. `$n` can be used to retrieve parameters passed to Bash
scripts or functions. Default values can be assigned to these variables
without the use of `[ -z $n ] && ...` in the following syntax:

    ${n:-default}

Where:

-   **n** The parameter index value
-   **default** The value that should be assigned if it is null/not set.

#### Example

To create a error handling function in a script that gives a exit code
of 1 if it is not set under \$2:

    fatal()
    {
            exitval=${2:-1}
            echo `date`" - FATAL - $1"
            exit $exitval
    }
