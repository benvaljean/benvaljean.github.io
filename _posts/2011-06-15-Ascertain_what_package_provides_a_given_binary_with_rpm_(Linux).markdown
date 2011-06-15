---
layout: post 
title: Ascertain what package provides a given binary with rpm (Linux)
---

On Redhat-based systems the *rpm* command can show the package that
installs a given binary. This is useful when a given binary is not
present on a server and `yum search` is not finding the package.

    rpm -q --whatprovides /usr/bin/command

[Category:Linux](Category:Linux "wikilink")
