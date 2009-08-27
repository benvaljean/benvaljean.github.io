---
layout: post 
title: SQL Clustering (Database Server)
---

A cluster is a two-or-greater-node failover solution, using a
shared-nothing model (i.e., each server owns and manages its own
devices). A cluster isn't a fault-tolerant solution but rather a
high-availability solution; that is, it minimizes downtime instead of
eliminating it.

The two nodes in a cluster work in either an active/active (i.e., both
servers perform meaningful work all the time) or an active/passive
(i.e., one server performs no meaningful work or performs work but
doesn't run the same application at the same time as the other server)
mode. Some applications can use the active/active mode (e.g., Microsoft
SQL Server and File Services), but others must use an active/passive
configuration (e.g., Exchange Server).

A key part of cluster is the shared-storage subsystem. The external
storage devices must be based on SCSI. The connections to the devices
can be based on either SCSI or SCSI over fibre channel (the cluster uses
SCSI commands to reserve and release devices and to reset SCSI buses)

If a service or machine in a back-end cluster fails, another in the
cluster takes control and handles all the requests (unlike a
load-balanced configuration, where several machines share the requests).
In essence, a back-end cluster is more reliable than a front-end
cluster; it\'s just not as scalable. Windows 2000 Advanced Server
allowed an MSCS cluster with two nodes; in Win2k3, you can have up to
four nodes per cluster.

### Pseudo Active/active clustering

Active/Active Clustered SQL is not quite what it means - the
active/active means that both nodes are serving SQL but usually serve
different DBs. For example DBs 1-3 in most cases go to node 1 and DBs
4-6 in most cases go to node 2. You split the backend disk between the
nodes and load share. Should a fail-over occur then all 1-6 databases in
this example can be accessed from just the one node.

### See Also

-   [Setting up a SQL
    Cluster](http://articles.techrepublic.com.com/5100-10878_11-5157575.html)
-   [Setting up a reboot cycle for an active/passive SQL
    cluster](http://www.databasejournal.com/features/mssql/article.php/3457551/Setting-up-a-reboot-cycle-for-ActivePassive-Cluster-SQL-Server.htm)

[Category:MSSQL](Category:MSSQL "wikilink")
