---
layout: post 
title: Set Default Schema / search path (PostgreSQL)
---

When schema names are omitted the default public schema is searched
first, followed by the a schema entitled by the current username. If you
would like to use another default schema it can be changed as follows:

    SET search_path TO new_schema, public;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
