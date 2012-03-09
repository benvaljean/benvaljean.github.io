---
layout: post 
title: Get Database Schema and Table Sizes (PostgreSQL)
---

#### Get Database size

    SELECT pg_size_pretty(pg_database_size('db_name_here')) As fulldbsize;

#### Get size of all tables in a schema

    select pg_size_pretty(CAST((SELECT
    SUM(pg_total_relation_size(table_schema || '.' || table_name) )
    FROM information_schema.tables
    WHERE table_schema = 'schema_name_here') As bigint) )  As tables_schema_size;

#### Get sizes of a table

Full\_size = Size of table, its toasted tables and indexes\
Table\_only = Size of the table only

    SELECT pg_size_pretty(pg_total_relation_size('table_name_here')) as Full_size, pg_size_pretty(pg_relation_size('table_name_here')) as Table_only;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
