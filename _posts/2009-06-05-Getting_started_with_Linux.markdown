---
layout: post 
title: Getting started with Linux
---

Copy all files inc subdirs:

    cp -a /usr/local/foo/* /var/temp/bar

Find files:

    updatedb
    locate filename

Search for packages that contain a certain file

    apt-file search filename

Delete everything older than 7 days:

    find /directoryname -type f -mtime +7 -exec rm {} \\;
