---
layout: post 
title: Copy table structure only (PostgreSQL)
---

Create a copy of a table but with no data inside it:

    create table table2 ( like table1 INCLUDING DEFAULTS INCLUDING CONSTRAINTS INCLUDING INDEXES );

OR with older versions use a piped pg\_dump output with sed:

    pg_dump -t table1 | sed 's/table1/tabble2/g' | psql

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
