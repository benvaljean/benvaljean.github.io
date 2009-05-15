---
layout: post 
title: WINS Lookup tool
---

There is no tool with Windows that can perform WINS lookups in order to
test a WINS server, in contrary to DNS where `nslookup` can be used. On
linux there is a tool called `nmblookup`. On Debian it can be installed
by typing:

    sudo apt-get install nmblookup

The usage is:

    nmblookup -U <WINSserver> -R <nametolookup>
