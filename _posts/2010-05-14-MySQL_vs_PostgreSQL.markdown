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
|}

[[Category:PostgreSQL]]
