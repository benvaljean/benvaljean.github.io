---
layout: post 
title: Chmod codes (Linux)
---

First charater: User permissions<br>
Second chracter: Group permissions<br>
Last character: Other permissions<br>

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''ls listing'''
| align="center" style="background:#f0f0f0;"|'''chmod code'''
|-
| <tt>r--------</tt>||400
|-
| <tt>rw-------</tt>||600
|-
| <tt>rw-r-----</tt>||640
|-
| <tt>rwx------</tt>||700
|-
| <tt>rwxrwx---</tt>||770
|-
| 
|}
===Examples===
<pre>
user@host:~$ chmod 600 test
user@host:~$ ls -l test
-rw------- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 640 test
user@host:~$ ls -l test
-rw-r----- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 750 test
user@host:~$ ls -l test
-rwxr-x--- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 700 test
user@host:~$ ls -l test
-rwx------ 1 user group 6 2009-11-25 15:48 test
</pre>
[[Category:Linux]]
