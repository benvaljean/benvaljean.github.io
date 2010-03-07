---
layout: post 
title: Setting up Mirroring in SQL Server (MSSQL)
---

### Allowing .NET 1.1 sites to recognise failover

.NET 1.1 sites do not have the failover partner parameter in the SQL
connection string as it natively uses an older version of SQLClient and
not the ODBC route as defined in .NET 2.0+ . Natively a .net 1.1 site
cannot automatically recognise the failover and will still try to
connect to the principal.

One way around this is to create a SQL agent alert on the mirror server
to listen for a 1440 in the Application log. 1440 indicates that it is
now the principal - indicating that a failover has occurred. This alert
runs a job which runs a cmdexec step that can run a BAT script that
substitutes the configuration file that contains your connection string
with a file that points to the mirror.

#### Mechanics of auto failover: Principal to Mirror

1.  The SQLMirror has a SQL agent alert that listens for an event ID
    that indicates that any database has failed over to SQLMirror from
    SQLPrincipal.
2.  The SQL agent runs a job which has a cmdexec step that runs a bat
    file on SQLMirror:
    \\\\\\\\sqlmirror\\\\c\$\\\\webConfigtosqlmirror.bat

This bat file substitutes the web.config files for all the sites. This
script must be updated when new sites are created.

##### Notes

The SQL agent will trigger the script once per database as mirroring is
at the database (not instace) level. In order to stop the
IBConfigtoMinnie.bat script being run \~30 times the script iself only
allows itself to be run once, as per this extract:

    If exist BlockwebConfigFailovers.txt goto eof
    if not exist BlockwebConfigFailovers.txt (
     echo Block future web.config failovers, delete me to undo >>BlockwebConfigFailovers.txt
    )

**In order for the failover script to be re-enabled the
BlockwebConfigFailovers.txt file must be deleted.** Accidentally not
deleting this file post a manual failover back to SQLPrincipal following
an outage will disable the automatic failover.

### WebConfigtosqlmirror.bat script

    @echo off
    If exist BlockwebConfigFailovers.txt goto eof
    if not exist BlockwebConfigFailovers.txt (
     echo Block future web.config failovers, delete me to undo >>BlockwebConfigFailovers.txt
    )


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
