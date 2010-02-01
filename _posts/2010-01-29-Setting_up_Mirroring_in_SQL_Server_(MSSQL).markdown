---
layout: post 
title: Setting up Mirroring in SQL Server (MSSQL)
---

SQL Mirroring is a native replication feature of SQL Server 2005 SP2+ which can setup two SQL servers in a automatic/hot failover capacity and thereby giving redundancy to each server.

===Definition of Terms===
The definition of terms for mirroring that Microsoft use are slightly different for that used by other systems. An example of this is shown with a comparison of Mirroring terms with MySQL:
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''SQL Server Mirroring'''
| align="center" style="background:#f0f0f0;"|'''MySQL'''
|-
| Principal ||Master
|-
| Mirror||Slave
|-
| Witness||Management
|-
| Log||Transaction/Binary Log
|-
| 
|}
==Failover mechanism==
The principal server answers queries as usual. A mirror server which is a standby/slave server which will become the principal should the principal stop working. A witness server which monitors the state of the principal server and will automatically setup the mirror server to become a principal on-the-fly.
==Hardware required==
To achieve automatic/hot failover three servers are required:

1 x '''Principal'''
<br>1 x '''Mirror'''
<br>1 x '''Witness'''

As mirroring is at the database level and not the instance level it is possible to mix principal databases and mirror instances on the same SQL Server instance and indeed the witness instance could be on either the principal or mirror but this would be meaningless given the witness' function of providing hot failover.

==Setting up SQL Mirroring==
===Create databases on the Principal server and the Mirror server===
It is recommended to create databases with the database and transaction log locations specifically stated as to avoid having to use a <tt>WITH MOVE</tt> context when restoring databases to either server. Full recovery (use transaction logs) must be enabled as mirroring itself utilises transaction logs to replicate data.
<pre>
USE [master]
GO
CREATE DATABASE [ExampleDB] ON  PRIMARY 
( NAME = N'Data', FILENAME = N'D:\\SQLDatabases\\ExampleDB.mdf' , SIZE = 68544KB , MAXSIZE = UNLIMITED, FILEGROWTH = 10%)
 LOG ON 
( NAME = N'Log', FILENAME = N'C:\\SQLTransactionLogs\\ExampleDB.ldf' , SIZE = 1024KB , MAXSIZE = UNLIMITED, FILEGROWTH = 10%)
GO
alter database [ExampleDB] set recovery full</pre>
===Migrate existing data===
Migrate the exisitng data in any preferred manner, an example of which is shown below.
<pre>
restore database [ExampleDB] from disk='\\\\server\\share\\ExampleDB.bak' with replace</pre>
===Backup Database and Transaction Logs===
Each database that will be a principal needs to be backed up. The backups used to migrate data to it initially cannot be used to migrate (restore) data to the mirror. Else errors relating to to the transaction logs on the remote copy either not being rolled forward to a point in time that is encompassed in the local copy of the transaction log or or being rolled forward to a point in time that beyond reach of the transaction log. The transaction logs needed to be backed up as otherwise when the data is restored to the mirror SQL will change the recovery model backup model back to 'simple.' It is recommended to backup the data to a share on the mirror, as shown below:
<pre>
backup database [ExampleDB] to disk='\\\\SQLMirror\\share\\ExampleDB.bak'
backup log [ExampleDB] to disk='\\\\SQLMirror\\share\\ExampleDB.log'
</pre>

===Restore with no recovery and replace===
The restore of DBs and transaction logs to the mirror server must be done without the rolling forward of any transaction logs or brought back online else it will be in a different state from the principal database. The replace option is required as MSSQL will refuse the restore as the backup is from a different server.
<pre>
restore database [ExampleDB] from disk='\\\\SQLMirror\\share\\ExampleDB.bak' with norecovery, replace
restore log [ExampleDB] from disk='\\\\SQLMirror\\share\\ExampleDB.log' with norecovery, replace 
</pre>
The database when viewed in [http://msdn.microsoft.com/en-us/library/ms174173.aspx Management Studio] it will be shown as a <tt>Restoring...</tt> state.
====Troubleshooting====
Errors referring to the transaction logs either not being rolled forward to a point in time that is encompassed in the transaction log or or being rolled forward to a point in time that beyond reach of the transaction log are usually due to the backup and restore being done too far apart. The longer the amount of time between the principal being backed up and the restore done to the mirror the greater the chance of a problem occurring. In some cases just retrying the backup and restore can allow it to work. Always ensure that the backups are deleted before re-backing up further to setting up mirroring as if SQL has to overwrite files it can cause problems.

===Create Endpoints===

Mirroring cannot use the existing endpoint(s), a dedicated endpoint for mirroring must be configured. 

Execute the following T-SQL on both the mirror, principal and witness:
<pre>
CREATE ENDPOINT Mirroring
    STATE=STARTED 
    AS TCP ( LISTENER_PORT = 5123 ) 

    FOR DATABASE_MIRRORING 
    ( AUTHENTICATION = WINDOWS NTLM, ENCRYPTION = REQUIRED, ROLE = ALL

    )
</pre>
The port number, in this case <tt>5123</tt> can of course be any non-privileged or already in use port.
<br>See also: [http://msdn.microsoft.com/en-us/library/ms190456.aspx How to: Create a Mirroring Endpoint for Windows Authentication (Transact-SQL)]

===Enable Mirroring===
Mirroring is configured through setting up a 'partner' on each database. The mirror databases' will have the principal as its partner and vica-verca. Each database also has the witness configured. The 'partner' parameter has no option to specify whether it is the principal or the mirror in the mirroring configuration, it is the order in which the T-SQL is applied that determines this. The first to receive the <tt>alter database</tt> command will become the mirror, the second will become the master.

An FQDN must be used as shown in the following T-SQL statements. The preferable way to achieve this is to setup the necessary internal DNS records. The hosts file can be used as an alternative but the default domain DNS suffix is not referenced by these commands.

<pre>
--Run the following on the mirror:
ALTER DATABASE [ExampleDB] SET PARTNER = 'TCP://SQLPrincipal.company.local:5123'
ALTER DATABASE [ExampleDB] SET WITNESS = 'TCP://SQLWitness.company.local:5123'
--Run the following on the principal:
ALTER DATABASE [ExampleDB] SET PARTNER = 'TCP://SQLMirror.company.local:5123'
ALTER DATABASE [ExampleDB] SET WITNESS = 'TCP://SQLWitness.company.local:5123'
</pre>

The principal database when viewed in [http://msdn.microsoft.com/en-us/library/ms174173.aspx Management Studio] will be shown as a <tt>Principal, Synchronized</tt> state. The mirror will be shown as a <tt>Mirror, Synchronized / Restoring...</tt> state.

====Troubleshooting====
=====Error 1=====
<tt>Database Mirroring Transport is disabled in the endpoint configuration.</tt>
<br>The mirroring endpoint has not been created, check your configuration 
=====Error 2=====
<pre>
An error occurred while starting mirroring.
------------------------------
ADDITIONAL INFORMATION:
Alter failed for Database 'basildondemo'.  (Microsoft.SqlServer.Smo)

For help, click: http://go.microsoft.com/fwlink?ProdName=Microsoft+SQL+Server&ProdVer=9.00.4035.00&EvtSrc=Microsoft.SqlServer.Management.Smo.ExceptionTemplates.FailedOperationExceptionText&EvtID=Alter+Database&LinkId=20476
------------------------------
An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo)
------------------------------
The server network address "TCP://SQLMirror.jobsgopublic.local:5123" can not be reached or does not exist. Check the network address name and that the ports for the local and remote endpoints are operational. (Microsoft SQL Server, Error: 1418)
For help, click: http://go.microsoft.com/fwlink?ProdName=Microsoft+SQL+Server&ProdVer=09.00.4035&EvtSrc=MSSQLServer&EvtID=1418&LinkId=20476
</pre>
Check firewalling, but this is usually not an issue with making a connection on the specified port. If you use the exact statements to create the endpoints as shown in this article there should be know problem. Check the application log on the machine that cannot be connected to.
=====Error 3=====
In the application log

<pre>
Database Mirroring login attempt failed with error: 'Connection handshake failed.
There is no compatible encryption algorithm. State 22.'.  [CLIENT: 2.2.2.2]
</pre>

This occurs when one endpoint is setup to do encryption and the other is not, or the algorhythems are setup differently. The endpoint encryption configuration for both endpoints must match.



[[Category:MSSQL]]
