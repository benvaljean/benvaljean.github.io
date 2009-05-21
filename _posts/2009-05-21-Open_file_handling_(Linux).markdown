---
layout: post 
title: Open file handling (Linux)
---

View current open files for all processes:

    lsof -n

Therefore: To list number of files open for all procs:

    lsof -n|wc -l

To list for just a particular process:

    lsof -p pid

To view the maximum number of files that any single process can open:

    ulimit -n

To change the maximum number of files that any single process can open,
append the following lines to /etc/security/limits.conf

    *                soft    nofile          65535
    *                hard    nofile          65535

This will give a hard and soft limit of 65535.

To change the maximum number of files that the entire OS can have open,
append the following line to /etc/sysctl.conf

    fs.file-max = 100000
