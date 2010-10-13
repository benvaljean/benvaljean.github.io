---
layout: post 
title: Find and replace - regexp replace (PostreSQL)
---

The regexp\_replace function allow \'find and replace\' functionality
within fields in Postgres.

Syntax: regexp\_replace( field, E\'regex-string\', \'new-string\');

#### Example

    update table set field=regexp_replace(field, E'old-text', 'new-text');

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
