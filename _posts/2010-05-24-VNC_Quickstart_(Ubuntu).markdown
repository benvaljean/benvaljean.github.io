---
layout: post 
title: VNC Quickstart (Ubuntu)
---

This will also probably work on any Debian-based distro.

### Setup

    sudo apt-get install x11vnc
    x11vnc -storepasswd
    x11vnc -forever -usepw &

This sets up VNC to listen on its default port of 5900 for control of
the local console session with the password you entered.

#### Setup with Java console

This will allow you to access your machine through any Java enabled
broswer, incase vncviewer is not available. The Java viewer will be
listening on port 5800.

    sudo apt-get install x11vnc vnc-java
    x11vnc -storepasswd
    x11vnc -forever -usepw -httpdir /usr/share/vnc-java/ -httpport 5800 &

[Category:Linux](Category:Linux "wikilink")
