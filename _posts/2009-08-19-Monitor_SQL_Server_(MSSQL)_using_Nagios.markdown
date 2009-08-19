---
layout: post 
title: Monitor SQL Server (MSSQL) using Nagios
---

[Nagios](Nagios "wikilink") is a free open-source monitoring
software/platform.

### Service

For a non-renamed instance the following can be used:

    define service{
            use                     service
            hostgroup_name  sql-servers
            service_description     SQL Svc
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSSQLSERVER
            }

If the instance has been rewnamed the service will have a dollar-sign
(\"\$\") as part of it, for instance an instance called \"MAIN\" will be
called \"MSSQL\$MAIN\". Dollar-signs indicate variables to Nagios so the
character must be escaped. Escaping characters invovles repeating it and
encapsulating it within quotation marks, see below:

    define service{
            use                     service
            hostgroup_name  sql-servers
            service_description     SQL Svc PROD
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSSQL"$$"MAIN
            }

### Default port is open

Default port for SQL is 1433, adjust as required. Ensure the
[check\_tcp](http://nagiosplugins.org/man/check_tcp) plugin is
installed.

    define service{
            use                     service
            hostgroup_name  sql-servers-old
            service_description     SQL Connectivity 1433
            check_command           check_tcp!1433
    }

### Connection check

The following will allow Nagios to connect to the SQL server with a
given username and password.

The plugin check\_mssql.sh is already in the contrib/ direcory of the
nagios-plugins release. If it is not available it can be downloaded
here: <http://ben.goodacre.name/nagios/check_mssql.sh> . The script
requires [FreeTDS](http://www.freetds.org) installed and setup.

#### Installing FreeTDS

    wget ftp://ftp.ibiblio.org/pub/Linux/ALPHA/freetds/stable/freetds-stable.tgz
    tar zxf freetds-stable.tgz
    cd freetds-stable/
    ./configure
    make
    sudo make install

-   Edit the /usr/local/etc/freetds.conf file to include your SQL server
    hostname and port. This is important as the \"-S\" parameter refers
    to the configuration entry here and not the hostname itself.
-   Test the config:
    `tsql -S config-entry-in-square-brackets -U username -P password` If
    you connect and see a `1>` prompt it is working ok.
-   SQL authentication will need to be enabled, as well as connect
    privilidges on the default database - usually \'master\'.

#### Test the plugin

    user@server:~/nagios-plugins-1.4.11/contrib$ ./check_mssql.sh config-entry-in-square-brackets nagios passwordhere 2000
    OK - MS SQL Server 2000 has 2 user(s) connected: 1 nagios, 1 (1rowaffected).

Now copy the check\_mssql.sh file to your /usr/local/nagios/libexec and
the plugin can be used in the following service and command config:

    define service{
            use                     service
            host_name          sql1
            service_description     SQL Connection Check
            check_command           check_mssql_sql1
    }
    #Due to the way that Nagios expends the $HOSTNAME$ variable it does not work, so an individual check_command must be created per server. If somebody knows the correct way to do this, please add it to discussion.
    define command{
            check_command           check_mssql_sql1
            command_line            $USER1$/check_mssql.sh sql1 nagios Rogerrabbit45! 2000
    }

See also:
<http://serverfault.com/questions/15557/testing-that-sql-server-2005-is-listening-for-freetds>

### Load/health monitoring

Below check\_nt is used to monitor WMI counters. The WMI syntax is
different if a named instance is used as opposed to the default
\'MSSQLSERVER\'

    #Monitoring with a non-named instance:
    define service{
            use                     service
            hostgroup_name          sql-servers-old
            service_description     SQL DB Allocated Pages
            check_command           sql-wmi-totalpages
    }
    define command{
            command_name sql-wmi-totalpages
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\SQLServer:Buffer Manager\\Total pages","Total allocated pages in memory: %.f"
    }
    define service{
            use                     service
            hostgroup_name          sql-servers-old
            service_description     SQL DB Batch requests/sec
            check_command           sql-wmi-batchreqs
    }
    define command{
            command_name sql-wmi-batchreqs
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\SQLServer:SQL Statistics\\Batch Requests/sec","Batch requests/sec: %.f" -w 50 -c 250
    }
    define service{
            use                     service
            hostgroup_name          sql-servers-old
            service_description     SQL DB Log flushes/sec
            check_command           sql-wmi-logflushes
    }
    define command{
            command_name sql-wmi-logflushes
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\SQLServer:Databases(_Total)\\Log Flushes/sec","Log flushes/sec: %.f" -w 50 -c 250
    }

    #Monitoring a named instance called PROD:
    define service{
            use                     service
            hostgroup_name          sql-servers-new
            service_description     SQL DB Allocated Pages2
            check_command           sql-wmi-totalpages2
    }
    define command{
            command_name sql-wmi-totalpages2
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\MSSQL\\$PROD:Buffer Manager\\Total pages","Total allocated pages in memory: %.f"
    }
    define service{
            use                     service
            hostgroup_name          sql-servers-new
            service_description     SQL DB Batch requests/sec2
            check_command           sql-wmi-batchreqs2
    }
    define command{
            command_name sql-wmi-batchreqs2
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\MSSQL\\$PROD:SQL Statistics\\Batch Requests/sec","Batch requests/sec: %.f" -w 50 -c 250
    }
    define service{
            use                     service
            hostgroup_name          sql-servers-new
            service_description     SQL DB Log flushes/sec2
            check_command           sql-wmi-logflushes2
    }
    define command{
            command_name sql-wmi-logflushes2
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\MSSQL\\$PROD:Databases(_Total)\\Log Flushes/sec","Log flushes/sec: %.f" -w 50 -c 250
    }

### Connection time

Through use of the check\_mssql\_health plugin the time to a sucessful
connection to SQL can be monitored.

-   Install the plugin: [temp](temp "wikilink")
-   The service configuration could look like this:

<!-- -->

    define service{
            use                             service
            hostgroup_name                  sql-servers
            service_description             SQL Connection time
            check_command                   check_mssql_health!connection-time
            }

### I/O Busy

Busy I/O should be monitored as it is an indicator of a busy server and
can again be monitored though the check\_mssql\_health plugin.

-   Install the plugin: [temp](temp "wikilink")
-   Append the following service config :

<!-- -->

    define service{
            use                             service
            hostgroup_name                  sql-servers-new
            service_description             IO Busy
            check_command                   check_mssql_health!io-busy
            }

### Installing the check\_mssql\_health plugin

-   Download the plugin: [check\_mssql\_health plugin homepage
    (translated from
    German)](http://babelfish.yahoo.com/translate_url?doit=done&tt=url&intl=1&fr=bf-home&trurl=http%3A%2F%2Fwww.consol.de%2Fopensource%2Fnagios%2Fcheck-mssql-health%2F&lp=de_en&btnTrUrl=Translate)
    \-- [Original
    page](http://www.consol.de/opensource/nagios/check-mssql-health/) in
    German
-   Copy to your /usr/local/nagios/libexec dir.
-   The plugin requires [FreeTDS](http://www.freetds.org/) to be
    installed: [Installing
    FreeTDS](http://www.rogerrabbit.net/w/index.php?title=Monitor_SQL_Server_%28MSSQL%29_using_Nagios&action=submit#Installing_FreeTDS)
    The plugin can utilise a freetds.conf file that is not in the
    location it would be expected to reside in, even if FreeTDS is
    currently installed. Check `/usr/share/libct3/freetds.conf` ,
    `/usr/local/etc/freetds.conf` and `/etc/freetds/freetds.conf`
-   Append the following to your commands.cfg:

<!-- -->

    define command{
            command_name            check_mssql_health
            command_line            $USER1$/check_mssql_health -server $HOSTNAME$ -username usernamehere -password passhere --mode $ARG1$
    }

#### See Also

\[<http://translate.google.com/translate?hl=en&sl=de&u=http://www.nagios-portal.org/wbb/index.php%3Fpage%3DThread%26threadID%3D14926&ei=f5CBSu75NtirjAfVyKH2CQ&sa=X&oi=translate&resnum=1&ct=result&prev=/search%3Fq%3D%253Bport%253D1433%2527,%2527nagios%2527>,\...)%2Bfailed:%2B(no%2Berror%2Bstring)%2Bat%2B/usr/local/nagios/libexec/check\_mssql\_health%2Bline%2B1897%26hl%3Den%26client%3Dopera%26rls%3Den-GB%26hs%3DSqt
check\_mssql\_health connect to server\] Translated from German

### Monitor mirroring health and availability

Through effective monitoring of WMI counters the queue of data on the
master (called principal by Microsoft) awaiting to be sent to the slave
(called mirror by Microsoft) can be monitored, called the send queue.
Delays in waiting for the mirror to commit a transaction as well as the
tlogs that remain to be applied to the mirror to roll it forwards can
also be checked, called the transaction-dealy and the redo queue
respectively.

    #This monitors a named instance called PROD:

    #Send queue / principal queue
    define service{
            use                     service
            hostgroup_name          sql-principal
            service_description     SQL Mirroring TLog Send queue KB
            check_command           sql-wmi-mir-tlogqueue
    }
    define command{
            command_name sql-wmi-mir-tlogqueue
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\MSSQL\\$PROD:Database Mirroring(_Total)\\Log Send Queue KB","Mirroring TLog Send queue in KB: %.f" -w 50 -c 100
    }

    #Redo queue / mirror queue
    define service{
            use                     service
            hostgroup_name          sql-mirror
            service_description     SQL Mirroring Redo queue KB
            check_command           sql-wmi-mir-redoqueue
    }
    define command{
            command_name sql-wmi-mir-redoqueue
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d SHOWALL -l "\\\\MSSQL\\$PROD:Database Mirroring(_Total)\\Redo Queue KB","Mirroring TLog Redo queue in KB: %.f" -w 50 -c 100
    }

    #Transaction delay
    define service{
            use                     service
            hostgroup_name          sql-servers-new
            service_description     SQL Mirroring Transaction Delay
            check_command           sql-wmi-mir-tdelay
    }
    define command{
            command_name sql-wmi-mir-tdelay
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 24601 -s orange26# -v COUNTER -d
     SHOWALL -l "\\\\MSSQL\\$PROD:Database Mirroring(_Total)\\Transaction Delay","Delay in transac
    tion termination acknowledgement: %.f" -w 1000 -c 15000
    }

#### See Also

Using the monitoring counters defined should covery all scenarios.
However mirroring can be monitored using the [Database mirrroing
monitor](http://msdn.microsoft.com/en-us/library/ms365786.aspx). Alerts
to the event log can be setup for various thresholds and these entries
in the event log can be watched for by the use of a SQL Agent Alert.

Another method to monitor monitored is vto use system stored procedures:
[Using Warning Thresholds and Alerts on Mirroring Performance
Metrics](http://msdn.microsoft.com/en-us/library/ms408393.aspx)

### Resources

-   [Monitoring MS SQL from \*nix (Yes, it really
    works!)](http://forums.cacti.net/viewtopic.php?t=27763&highlight=works)
    A perl script for creating Nagios config
-   [Configuring Nagios to read WMI
    information](http://www.experts-exchange.com/Networking/Linux_Networking/Q_24049447.html)

<!-- -->

-   [Probing the depths - Windows
    Monitoring](http://nordicmeetonnagios.op5.org/op5media/nmn2009/presentations/Michael%20Medin%20Probing%20the%20depths%20of%20Windows.pdf)

[Category:Nagios](Category:Nagios "wikilink")
