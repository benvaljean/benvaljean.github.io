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
| r--------||400
|-
| rw-------||600
|-
| rw-r-----||640
|-
| rwx------||700
|-
| rwxrwx---||770
|-
| 
|}
===Examples===
<pre>
user@host:~$ chmod 600 test
user@host:~$ lll test
-rw------- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 640 test
user@host:~$ lll test
-rw-r----- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 750 test
user@host:~$ lll test
-rwxr-x--- 1 user group 6 2009-11-25 15:48 test

user@host:~$ chmod 700 test
user@host:~$ lll test
-rwx------ 1 user group 6 2009-11-25 15:48 test
</pre>
[[Category:Linux]]
