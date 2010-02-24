---
layout: post 
title: MySQL Troubleshooting
---

### Get current processes and queries

    mysql> show processlist;

### Get number of queries currently running

    mysql> show status like 'Threads_connected';

### Get number of queries since the server was started

    mysql> show status like 'Threads_created';

### See Also

[Linux Troubleshooting](Linux_System_Troubleshooting "wikilink")

[Category:MySQL](Category:MySQL "wikilink")
