---
layout: post 
title: SQL Log shipping (Database Server)
---

Microsoft SQL Server Log shipping is a mathod of implementing **manual
failover/redundancy/high-availability** to a database server and has
been around since SQL Server 2000 Enterprise.

### Manual failover versus Automatic failover

Automatic failover is when services such as databases can be
automatically accessed from a standby/secondary server should the
primary server fail for any reason without any intervention from a
systems administrator. It either has a shared-nothing model where both
servers have all the data they need on its own server or both servers
share a storage device that is seperate to both the primary and
standby/secondary servers; such as a NAS ([Network Attached
Storage)](http://www.bestpricecomputers.co.uk/reviews/advice/network-attached-storage.htm).

Manual failover is when a secondary/standby server exists and has an
exact or recent copy of all the data required but a systems
administrator is required to perform some relatively painless and brief
actions to allow the services offered by the primary server to be
accessed by the secondary/standby server.

### Methodology

1.  Full database backup of primary is done and restored to the
    secondary.
2.  Transaction logs from the primary need to be stored on a network
    drive accesable to both servers - it is usually not a good idea to
    automatically place the primary\'s transaction logs on the
    secondary.
3.  Secondary server\'s SQL server agent must have access to the
    location of the primary\'s transaction logs.
4.  Transaction logs from the primary are applied to the secondary
    periodically.

-   Either the primary, secondary or a seperate server can be used for
    monitoring log shipping.
-   Secondary\'s databases are always in read-only mode until the
    failover - apart from when it is updated with new data from the
    primary on a periodic basis.

### Actions required when a fail-over occurs

1.  Perform one last backup on the primary if possible.
2.  Copy primary\'s transaction logs to the secondary and apply them in
    the same order as they were created. Restore the last transaction
    log with the WITH RECOVERY clause to allow it to become operational.
3.  Re-create any logins required.

Because Log shipping is manual failover and relies on periodic
transaction logsfor data recovery it is unsuitable for many live
environments. With the advent of NLB (Network Load Balancing) coming
with Server 2003 and with clustering easier to implement then it used to
be its popularity is decreasing.

### See Also

-   [SQL Clustering](SQL_Clustering_(Database_Server) "wikilink")
-   [Log Shipping in Microsoft SQL Server
    2000](http://www.microsoft.com/technet/prodtechnol/sql/2000/reskit/part4/c1361.mspx)
-   [Setting up, reconfiguring, and monitoring log shipping part
    1](http://www.microsoft.com/technet/prodtechnol/sql/2000/maintain/logship1.mspx)
-   [Setting up, reconfiguring, and monitoring log shipping part
    2](http://www.microsoft.com/technet/prodtechnol/sql/2000/maintain/logship2.mspx)
-   [Log Shipping with SQL Server
    2005](http://sqlserveruniverse.com/content/ADMN0100111132007LogShipping.aspx)
-   [Log shipping using Red Gate SQL Backup on Microsoft SQL
    Server](http://www.yohz.com/logship.html)
