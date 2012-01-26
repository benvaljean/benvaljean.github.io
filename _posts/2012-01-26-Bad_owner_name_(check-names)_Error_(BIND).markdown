---
layout: post 
title: Bad owner name (check-names) Error (BIND)
---

#### Problem

When attempting to load a xone file this error can occur:

    pop.company.net.zone:313: blah.pop.company.net: bad owner name (check-names)
    zone pop.company.net/IN: loading from master file pop.company.net failed: bad owner name (check-names)
    zone pop.company.net/IN: not loaded due to errors.

#### Cause

BIND does not permit underscores \"\_\" unless you specificy the whole
domain name.

#### Resolution

Do not use the suffix supplied with `$ORIGIN`, use
`blah.pop.company.net.` instead of `blah` in this example.

This is probably a bug, underscores are officially allowed although not
rarely used excluding Microsoft AD environments.

[Category:DNS](Category:DNS "wikilink")
[Category:BIND](Category:BIND "wikilink")
