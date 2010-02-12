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

This occurs when one endpoint is setup to do encryption and the other is not, or the algorithms are setup differently. The endpoint encryption configuration for both endpoints must match.
=====Error 4=====
When performing the final ALTER statement on the Principal:

<pre>
Msg 1412, Level 16, State 0, Line 1
The remote copy of database "ExampleDB" has not been rolled forward to a point in time that is encompassed in the 
local copy of the database log.
</pre>
This when the LSN (Log Sequence Number) of the mirror DB is less than the LSN of the principal. - If this were a DR scenario we would refer to it as a gap in the log chain. Ensure that the restore is done straight after the backup and that you backing up your transaction log to a different file name!

==Testing==
<pre>
--Run on current principal
USE master
GO
ALTER DATABASE [ExampleDB] SET SAFETY FULL
GO
ALTER DATABASE [ExampleDB] SET PARTNER FAILOVER
GO

--Run on new principal
USE master
GO
ALTER DATABASE [ExampleDB] SET SAFETY OFF
GO
</pre>
This will setup the mirror as a principal.
==Forced failover==
If the principal has died and the witness for whatever reason has not setup the mirror to become a principal this can be done manually:
<pre>
--Run on mirror if principal isn't available
USE
master
GO
ALTER DATABASE [ExampleDB] SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS
GO
</pre>
This is not as gruesome as it sounds as it is rare for data loss to occur when issuing this T-SQL. - So long as mirroring was working up to the point that the principal died.
==Failover database back to the principal following an outage finishing==
DBs are never automatically failed back from the old-mirror-now-master following an outage finishing.
<pre>
--Run on old-mirror-now-master
alter database [ExampleDB] set partner failover</pre>
As this has to be run on every database individually it can be quicker to create a cursor loop. There are better ways of using a cursor though. Presuming that all of your DBs are setup for mirroring the following can be used:
<pre>
Declare @mirrordbs table (dbname char(100))
Declare @fetcher as char(100)
Insert @mirrordbs
select name from sys.databases where name <> 'master' and name <> 'tempdb' and name <> 'msdb' and name <> 'tempdb' and name <> 'model'

DECLARE reader CURSOR FOR SELECT dbname FROM @mirrordbs
OPEN reader
FETCH NEXT FROM reader INTO @fetcher
WHILE @@FETCH_STATUS=0
BEGIN
  exec('alter database '+@fetcher+'set partner failover')
FETCH NEXT FROM reader INTO @fetcher
END
</pre>
==Troubleshooting==
===Orphaned User mapping===
Symptom:
<pre>
Error 15023: User already exists in current database.</pre>
User mapping setup was incorrect which resulted in orphaned permissions for some of the databases. This was fixed by:
<pre>
USE [ExampleDB]
GO
EXEC sp_change_users_login 'Report'
EXEC sp_change_users_login 'Auto_Fix', 'user', NULL, 'pass'
EXEC sp_change_users_login 'update_one', 'user', 'user'
GO
</pre>
http://blog.sqlauthority.com/2007/02/15/sql-server-fix-error-15023-user-already-exists-in-current-database/
===Cannot open database requested by the login. The login failed.===
If you are not using domain accs this problem could affect you: Despite having the same login details for both servers the credentials fail when the mirror is setup as a principal as the SID gets cached, and is normally randomly generated. Use different usernames for the two server to resolve this or create the login using a T-SQL command where the SID can be specified:
<pre>
CREATE LOGIN WITH PASSWORD ="password",SID ="sid for same login on principal server" </pre>
To retrieve the SID for each login from the principal server query the sys.sql_logins catalog view.

http://deepakrangarajan.blogspot.com/2008/02/failover-in-database-mirroring.html

http://bradmarsh.net/index.php/2008/07/29/sql-2005-mirroring-automatic-failover/
==Config ASP.net 2.0+ applications to utilise Mirroring==
The failover mechanism will not automatically change the database server your applications use. The <tt>failover partner</tt> parameter must be used in your connection string:
<pre>
<Setting Name="ConnectionString" Value="data source=SQLPrincipal\\PROD; failover Partner=SQLMirror\\PROD; Initial Catalog=ExampleDB;uid=user;pwd=pass" /></pre>

http://www.connectionstrings.com/sql-server-2005

The Initial catalog parameter must be used in preference to the database parameter as 'database' is not recognised by the ActiveX Data Objects (ADO) SQL driver. 

By configuring your application to use these settings, when the application makes a request to the database and the Principal server is not available, .NET will automatically send the request to the mirrored server. This should happen transparently so your website user should not notice any outage. Sessions should also be kept alive, depending upon your application.

If you're using .NET 1.1, this Failover Partner is not present, so you'll need to roll your own code to transfer the client. This could be a simple try...catch around the database connection, and in the catch, it retries using the mirrored server. Or use a script to substitute your connection string as shown below.
===Failover mechanism===
*The Principal server goes down. 
*The Witness server or your monitoring service detects the Principal database in unavailable. 
*The Witness server or your monitoring service forces the failover to your mirrored server, which becomes the new Principal. 
*ADO.NET attempts connection to the principal, (witness only informs mirror to become principal, not the ADO.NET access provider - but the success is cached)) this fails and the partner/mirror is tried, if this fails the principal is tried one more time.

http://msdn.microsoft.com/en-us/library/ms366348.aspx
==Allowing .NET 1.1 sites to recognise failover==
.NET 1.1 sites do not have the failover partner parameter in the SQL connection string as it natively uses an older version of SQLClient and not the ODBC route as defined in .NET 2.0+ . Natively a .net 1.1 site cannot automatically recognise the failover and will still try to connect to the principal.

One way around this is to create a SQL agent alert on the mirror server to listen for a 1440 in the Application log. 1440 indicates that it is now the principal - indicating that a failover has occurred. This alert runs a job which runs a cmdexec step that can run a BAT script that substitutes the configuration file that contains your connection string with a file that points to the mirror.

===Example===
web.configToMirror.bat:
<pre>
rem @echo off
if not exist g:\\maptester.txt (
  net use g: \\\\1.1.1.1\\WebConfigs
  if not exist g:\\maptester.txt (
    echo %date% %time% Tried to map drive but could not find g:\\maptester.txt on web1 >>web.configToMirror.log
    goto eof
  )
)

if not exist h:\\maptester.txt (
  net use h: \\\\2.2.2.2\\IBConfigs
  if not exist h:\\maptester.txt (
    echo %date% %time% Tried to map drive but could not find h:\\maptester.txt on web2 >>web.configToMirror.log
    goto eof
  )
)


call :checkfiles g:\\client1\\Config
call :checkfiles g:\\client2\\Config
call :checkfiles g:\\client3\\Config

call :checkfiles h:\\client1\\Config
call :checkfiles h:\\client2\\Config
call :checkfiles h:\\client3\\Config


goto eof


:checkfiles
if not exist %1\\webSQLMirror.config (
  echo %date% %time% Cannot find webSQLMirror.config for %1 >>web.configToMirror.log
)


if not exist %1\\webSQLPrincipal.config (
  echo %date% %time% Cannot find IBMinnie.config for %1 >>web.configToMirror.log
)
if exist %1\\webSQLMirror.config (
  del %1\\web.config
  copy %1\\webSQLMirror.config %1\\web.config
  echo %date% %time% Setup web.config for SQLMirror for %1 >>web.configToMirror.log
)

:eof
</pre>

==See Also==
[[Monitor SQL Server (MSSQL) using Nagios|Monitor SQL Server using Nagios]] Show perfmon counters for Mirroring that can be monitored.

==Links==
*[http://technet.microsoft.com/en-us/library/aa995867.aspx How to Align Exchange I/O with Storage Track Boundaries]
*[http://www.microsoft.com/technet/prodtechnol/sql/2005/physdbstor.mspx#_RAID Physical storage database design]
*[http://www.codeproject.com/KB/database/sqlmirroring.aspx SQL mirroring]
*[http://msdn.microsoft.com/en-us/library/ms187752.aspx SQL Server field types]
*[http://support.microsoft.com/kb/231282 IIS stress tools]

[[Category:MSSQL]]
