---
layout: post 
title: Python script fails with ": command not found"
---

#### Problem

When running a Python script it fails with the following output:

    : command not found

#### Cause

as it appears - this is a path issue. Python scripts have a tendency to
have no [shebang](http://en.wikipedia.org/wiki/Shebang_(Unix)) at the
top and consequently your script may be being executed by your standard
shell instead of python.

#### Resolution

-   Try running the script with python interpreter directly:

<!-- -->

    python script.py

[Category:Programming](Category:Programming "wikilink")
