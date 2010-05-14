---
layout: post 
title: List tables in all schemas (PostgreSQL)
---

Depending on how your search order is configured it can be easier to
simply to list every table in ever schema:

    select schemaname,tablename from pg_tables;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
