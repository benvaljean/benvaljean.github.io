---
layout: post 
title: Monitoring Exchange 2007 using Nagios
---

[Nagios](Nagios "wikilink") is a free open-source monitoring
software/platform.

### Services

#### Mailbox servers

    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex AD Topology
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeADTopology
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex IS
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeIS
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Mail Submission
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeMailSubmission
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Mailbox Assistants
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeMailboxAssistants
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex DB Replication
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeRepl
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Search Indexing
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeSearch
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Service Hosting
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeServiceHost
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex System Attendant
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeSA
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Remote Transport Log Search
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeTransportLogSearch
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex DB Engine for Ex Search
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l msftesql-Exchange
            }

#### CAS and Hub Transport servers

    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex AD Topology
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeADTopology
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex Anti-spam Update
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeAntispamUpdate
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex File Distribution
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeFDS
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex POP3
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangePOP3
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex Service Hosting
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeServiceHost
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex Transport
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeTransport
            }
    define service{
            use                     generic-service
    hostgroup_name  ex-cashub-servers
            service_description     Ex Transport Log Search
            check_command           check_nt!SERVICESTATE!-d SHOWALL -l MSExchangeTransportLogSearch
            }

### Replication Health / Status

If SCR, LCR or CCR is deployed in your organisation its status can be
checked through use of Nagios monitoring its perfmon counter:

    #This does not work as for some reason check_nt does not work with counters where the data has been presented as an argument:
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex SCR
            check_command           check_nt!COUNTER!-l "\\\\MSExchange Replication(_total)\\Failed","Replication failure status (0 = OK): %.f" -c 1
            }

    #A dedicated command must be created per counter that needs to be monitored:
    define command{
            command_name ex-wmi-replication
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Replication(_total)\\Failed","SCR Failure status: %.f" -c 1
    }

    #Then referenced directly with a service config like the following
    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex SCR
            check_command           ex-wmi-replication
            }

### Connectivity of Mailbox server to Hub Transport server(s)

The Hub servers in retry counter indicates any servers that are not
accessable from any of the mailbox servers. In Exchange 2007 if a Hub
transport server were to die and there was no monitoring, users in
cached exchange mode would not notice any issues a emails will still
leave their Outbox. Online users in this scenario would have thier
emails wait in Outbox.

    define service{
            use                     generic-service
    hostgroup_name  ex-be-servers
            service_description     Ex Hub Server in Retry State
            check_command           ex-wmi-hub-in-retry
            }

    define command {
            command_name ex-wmi-hub-in-retry
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchangeMailSubmission(msexchangemailsubmission)\\Hub Servers in Retry","Hub Servers in Retry state: %.f" -c 1
    }

### Database Health

#### Database Transaction Log Generation Checkpoint Depth

If a particular process stops working, crashes or otherwise fails then
Exchange must undo/redo work in order to prevent a partial-transaction
in the DB. This counter tracks the work involved in rolling any work
back if it is required. Normally 20 - 30, should not exceed 500.

    define service {
            use                     generic-service
            hostgroup_name          ex-be-servers
            service_description     Ex DB TLog gen chkpt lgth
            check_command           ex-wmi-tlog-gen-chkpt-length

    }
    define command {
            command_name ex-wmi-tlog-gen-chkpt-length
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Database ==> Instances(Information Store/_Total)\\Log Generation Checkpoint Depth","Ex transaction log generation checkpoint depth: %.f" -w 35 -c 500
    }

#### Database Page fault stalls / sec

Each time the DB cache manageer allocates a new page from the DB cache
this counter is incremented and should normally read 0. Persistent
values suggest that unused/dirty pages are not being removed quickly
enough and probably relate to an IO bottleneck or simply a spike in
usage.


    define service {
            use                     generic-service
            hostgroup_name          ex-be-servers
            service_description     Ex DB Page Flt Stalls/sec
            check_command           ex-wmi-db-pagefault-stallspersec
    }
    define command {
            command_name ex-wmi-db-pagefault-stallspersec
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Database(Information Store)\\Database Page Fault Stalls/sec","Ex DB Page Fault stalls / sec: %.f" -w 1 -c 3
    }

#### Version Buckets

Version buckets are the number of uncommitted changes in memory that
have yet to be written to the log. In general this can go up to 12000
and not be a problem but it is best to get a base-line and then adjust
the thresholds accordingly. A high value could be due to a large
attachment being sent or an IO bottleneck.

    define service {
            use                     generic-service
            hostgroup_name          ex-be-servers
            service_description     Ex DB Version Buckets
            check_command           ex-wmi-db-version-buckets-allocated
    }
    define command {
            command_name ex-wmi-db-version-buckets-allocated
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Database(Information Store)\\Version buckets allocated","Ex DB Version Buckets allocated: %.f" -w 5000 -c 12000
    }

#### Database Transaction Log Record Stalls / sec

This counter states how many log records Exchange was unable to write to
the log buffers each second because the buffers are full. This counter
should remain at 0 for most of the time. Spikes up to 100 are OK, an
average of 10 or more can indicate high IO write latencies.

    define service {
            use                     generic-service
            hostgroup_name          ex-be-servers
            service_description     Ex DB TLog Rec stalls/sec
            check_command           ex-wmi-db-log-rec-stallspersec
    }
    define command {
            command_name ex-wmi-db-log-rec-stallspersec
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Database(Information Store)\\Log Record Stalls/sec","Ex DB transaction log record stalls / sec: %.f" -w 5000 -c 12000
    }

#### Database Cache Hit Ratio

Simply the number of DB file page requests that are done without
requiring a file oprtation - accessing memory instead. With most users
in Outlook cached-exchange-mode this counter should not fall below 99%.
If most users do not use Outlook or use Outlook in \'online\' mode this
should not fall below 90%. As Ex2007 uses up as much RAM as it can do
with the DB cache a low ratio is a good indication of the server
requiring more RAM.

    define service {
            use                     generic-service
            hostgroup_name          ex-be-servers
            service_description     Ex DB Cache Hit Percent
            check_command           ex-wmi-db-cache-percent-hitrate
    }

    #No warnings set as this can flap to 0% at times.
    define command {
            command_name ex-wmi-db-cache-percent-hitrate
            command_line $USER1$/check_nt -H $HOSTADDRESS$ -p 12489 -v COUNTER -d SHOWALL -l "\\\\MSExchange Database(Information Store)\\Database Cache % Hit","Ex DB cache hit percent: %.f (0 dp)"
    }

#### See Also

[Track Exchange 2007 mailbox server health using database
counters](http://searchexchange.techtarget.com/generic/0,295582,sid43_gci1362447,00.html?track=NL-359&ad=716575&asrc=EM_NLT_8754745&uid=8701479)

[Category:Nagios](Category:Nagios "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
