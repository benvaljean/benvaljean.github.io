---
layout: post 
title: Installing Perl Modules (Linux)
---

A lot of distros have packages for many perl modules that allow many
modules to be installed automatically. However the every distro has its
own naming convention for the modules and it can therefore be difficult
to find the right package name. Using the CPAN module avoids this as the
generic MODULE::Name syntax can be used, this remains the same no matter
which distro is used as it Perl\'s syntax rather than the distro\'s
syntax.

### Install perl modules using CPAN

    sudo perl -MCPAN -e shell

Answer no to configure it automatically and follow the menus to select
an appropriate mirror. Within the CPAN shell perl modules can be
installed by typing `install MODULE::Name` . For example:

    install Archive::Zip

[Category:Linux](Category:Linux "wikilink")
