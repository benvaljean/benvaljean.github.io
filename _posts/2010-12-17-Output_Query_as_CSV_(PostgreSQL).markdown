---
layout: post 
title: Output Query as CSV (PostgreSQL)
---

Use the following to output a query a CSV. Offending characters like
new-lines and conmmas are automatically stripped:

    COPY ( select * from table ) to '/var/tmp/query.csv' with csv header;

OR the following also outputs as CSV but offending characters are
stripped:

    psql -F, -A -q -h 1.1.1.1 db user

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
