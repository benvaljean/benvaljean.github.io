---
layout: post 
title: High availability IIS & SQL using NLB & Clustering
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

### Clustering Basics

Win2k3 offers several types of clustering services; for this article,
we\'ll focus on the simple NLB cluster scenario.

Businesses typically cluster their servers into two parts: a front-end
cluster and a back-end cluster. NLB is ideal for a front-end cluster
configuration, and Microsoft Cluster Service (MSCS) is commonly used for
a back-end cluster configuration.

#### Front-End Cluster Configuration

Think of the front end as what the user first encounters when reaching a
Web site that has been clustered. The process goes something like this:

1.  The user issues a static request---that is, a request for a Web page
    with static content (content that\'s not generated dynamically, such
    as from a database).
2.  The NLB front-end clustered server group routes the user\'s request
    to an available Internet Information Services (IIS) server.
3.  The server handles the request.
4.  The process is repeated with each subsequent request, but with a
    different server in the group handling the new request.
5.  Because the requests are divided among the group of clustered
    servers, thus improving both performance and availability of the Web
    site, the cluster is said to be load balanced.

All these processes are transparent to the user, and it appears that
just one machine is handling the requests; therefore, the set of
clustered servers is often referred to as a virtual server.

##### NLB is best used for Front-end only

NLB is good for a front-end Web cluster configuration because it handles
such TCP/IP requests and distributes them across several machines at the
network layer, but it\'s not ideal for a back-end clustered
configuration.

Suppose a machine in this front-end cluster must be taken off the
network to add new hardware or for maintenance. The NLB cluster won\'t
route requests to that machine while it\'s offline, instead using the
other servers in the group to handle requests. When you plug the machine
back into the network, NLB detects it.

All well and good. But what happens if a service, such as IIS, is no
longer functioning on a machine in the cluster? NLB can\'t detect that
the service isn\'t running; instead, the NLB cluster keeps sending
requests to a machine that no longer has the Web server running. Not
only will this error cause a performance penalty, but the user who
happens to get that machine will get a \"Page cannot be displayed\"
message. Therefore, you shouldn\'t use NLB for mission-critical services
such as messaging or database services.

#### Back-End Cluster Configuration

Think of the back end as the requests that come from your Web
sites---for example, requests to an email server or a database
server---in a process something like this:

1.  The user issues a dynamic request---that is, a request for a Web
    page with dynamic content generated from a database.
2.  The NLB front-end clustered server group routes the user\'s request
    to an available IIS server.
3.  IIS processes the request with a call to a database server on the
    MSCS configured back-end cluster.

The two clustered configurations---front end and back end---work
together to create a \"layered\" cluster using the two types of
clustering services. Makes sense, doesn\'t it? You have to access the
front end to reach the back end.

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
4-6 in most cases go to node number 2. You split the backend disk
between the nodes and load share. Should a fail-over occur then all 1-6
databases in this example can be accessed from just the one node.

[Category:MSSQL](Category:MSSQL "wikilink")
