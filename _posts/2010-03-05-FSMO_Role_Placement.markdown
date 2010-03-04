---
layout: post 
title: FSMO Role Placement
---

[FSMO Roles](FSMO_Roles "wikilink") should be assigned to ensure the
best recoverability and operation of your Domain Controllers. If there
is only one DC in an environment then all the roles will be on the same
server of course. Only the smallest environments of 20 or less users can
be recommended to have only one DC else at least two DCs must be created
and the placement of [FSMO](FSMO_Roles "wikilink") roles becomes an
issue.

Two DCs are recommended for environments of up to \~200 users and the
FSMO role placement best practices below apply to an environment with 2
DCs.

### DR planning

It is important to not have the Domain Naming Master on the same server
as the RID Master or the PDC Master as if it were to stop working it
would be more difficult to create a new DC to replace the failed DC as
the Domain Naming Master must be live to use promote/create a new DC.
The PDC Master and RID Master are the roles that have the biggest
initial impact on the environment if lost to both users and Systems
Administrators.

### Global Catalogue planning

All DCs can be a GC when there are two DCs. When every DC is a GC it
does increase the replication work load however this has minimal impact
and speeds up the performance of AD.

### FSMO role placement

#### First DC: \'DC1\'

-   Domain naming master
-   Schema master
-   Infrastructure master

#### Second DC: \'DC2\'

-   RID pool master
-   PDC master

In this setup if DC1 were to fail there would be no impact to users and
there would be relatively-large amount of time available to recover it.
If DC2 were to failed could not be recovered we could relatively easily
add a new DC to the domain and give it the RID and PDC roles.

### Recovering following loss of DC

If DC1 fails build a new DC and seize (force transfer) the Domain naming
master and Schema master roles, if DC2 fails the RID and PDC roles must
be seized (force transferred) immediately.

To seize roles use the `ntdsutil` command with the following the syntax:

    C:\\WINDOWS>ntdsutil
    ntdsutil: roles
    fsmo maintenance: help

     ?                             - Show this help information
     Connections                   - Connect to a specific domain controller
     Help                          - Show this help information
     Quit                          - Return to the prior menu
     Seize domain naming master    - Overwrite domain role on connected server
     Seize infrastructure master   - Overwrite infrastructure role on connected server
     Seize PDC                     - Overwrite PDC role on connected server
     Seize RID master              - Overwrite RID role on connected server
     Seize schema master           - Overwrite schema role on connected server

### See Also

[FSMO Roles](FSMO_Roles "wikilink")

[Category:Windows](Category:Windows "wikilink") [Category:Domain
Controllers](Category:Domain_Controllers "wikilink")
