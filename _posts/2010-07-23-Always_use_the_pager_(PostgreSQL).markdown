---
layout: post 
title: Always use the pager (PostgreSQL)
---

Setting the pager to always and using the S command (if it is set to
less) can be easier than using \\\\o . The pager is normally only used
when the query hits \~30 records, to always use it:

    \\pset pager always

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
