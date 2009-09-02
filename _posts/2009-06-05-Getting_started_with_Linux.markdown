---
layout: post 
title: Getting started with Linux
---

Copy all files inc subdirs:

    cp -a /usr/local/foo/* /var/temp/bar

Delete all files inc subdirs:

    rm -rf folder

Find files with indexer:

    updatedb
    locate filename

Find files without indexer:

    find /dir -name filename
    find /dir -name '*part of file name*'

Search for packages that contain a certain file

    apt-file search filename

Delete everything older than 7 days:

    find /directoryname -type f -mtime +7 -exec rm {} \\;

Search text within files and print the lines:

    find /dir -type f -exec grep "textinfile" {} \\; -print

Search text within files and print only the filenames:

    find /dir -type f -print | xargs grep -li "textinfile"

Setup SSH tunnel using ssh server on custom port 2400 to listen on local
port 3335 parsing to db02:3306

    ssh -p2400 -N localhost -L 3335:db02:3306 -f
