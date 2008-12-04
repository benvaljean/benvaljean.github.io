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

Look at [this link](http://vyaskn.tripod.com/sqlsps.htm) to ascertain
which service pack (if any) is installed from the version/revision
number.

To run a query on a SQL server you could for instance open [SQL Server
Management
Studio](http://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796),
right-click the instance from within object exporer and choose new
query.
