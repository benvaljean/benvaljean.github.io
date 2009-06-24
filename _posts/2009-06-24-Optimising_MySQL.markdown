---
layout: post 
title: Optimising MySQL
---

key\_buffer\_size

Index blocks for MyISAM tables are buffered and are shared by all
threads. key\_buffer\_size is the size of the buffer used for index
blocks. The key buffer is also known as the key cache.

table\_cache

The number of open tables for all threads. Increasing this value
increases the number of file descriptors that mysqld requires. You can
check whether you need to increase the table cache by checking the
Opened\_tables status variable.

<http://dev.mysql.com/doc/refman/5.0/en/server-parameters.html>
