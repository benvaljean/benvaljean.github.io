---
layout: post 
title: Obtain Service pack details (SQL Server)
---

To ascertain what level of service pack is installed run this query on
the server:

    SELECT SERVERPROPERTY('productversion'), SERVERPROPERTY ('productlevel'), SERVERPROPERTY ('edition')

Older versions of SQL will not have this properties, in which case the
following query can be used as an alternative:

    SELECT @@version

Or look at the bottom panel in SQL Management Studio.

[Category:MSSQL](Category:MSSQL "wikilink")
