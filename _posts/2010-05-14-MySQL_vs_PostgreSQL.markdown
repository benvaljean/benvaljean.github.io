---
layout: post 
title: MySQL vs PostgreSQL
---

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''MySQL'''
| align="center" style="background:#f0f0f0;"|'''Postgres'''
|-
| SHOW DATABASES;||\\l
|-
| \\u db||\\c db 
|-
| SHOW GRANTS;||\\du
|-
| SHOW TABLES;||\\dt
|-
| SHOW COLUMNS;||\\d table
|-
| DESC tblname;||\\d foo
|-
| USE dbname;||\\c dbname
|-
| SHOW PROCESSLIST;||SELECT * FROM pg_stat_activity;
|-
| describe table;||\\d+ table;
|-
| show schemas;||\\dn OR select * from pg_namespace;
|-
| \\G (one time effect)||\\x (toggle for all queries)
|-
| \\P pager||$PAGER
|-
| \\T file||\\o | tee file
| show create table tablename;||pg_dump --schema-only -t tablename (may not always
|}

===Identical commands===
\\e  Edit buffer in external editor; vim by default.
\\!  Execute shell command
[[Category:PostgreSQL]]
