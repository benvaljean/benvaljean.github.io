---
layout: post 
title: FSMO Roles
---

Flexible Single Master Operation (FSMO) roles are key points in
functionality for your Domain Controllers. For advice on how to assign
FSMO roles and the best practices for assigning roles see [FSMO Role
Placement](FSMO_Role_Placement "wikilink").

### FSMO Roles

#### PDC Emulator

The DC holding this role is a PDC for any legacy Windows NT machines
that may still be running. However it also acts as a \'password master\'
to ensure no conflicts can occur when passwords are changed as well as
handling password changes. It also enforces account lockout and
synchronises time for all DCs in the domain. DCs will set their time
according to the time on the DC with the PDC Emulator role. Only the PDC
role DC needs to be setup with NTP.

##### Impact on loss of DC with this FSMO role

Loss of this role will have the biggest impact to users. Passwords could
no longer be changed and account lock-outs will behave unexpectedly.
Group policy changes will also fail as well as time-synchronising
between the DCs and clients which could result in a DC not being able to
log users onto the domain.

#### RID Master

Every object in AD that has a security tab in its properties has a
unique number assigned to it. This way for instance if a group is
renamed its connections with other objects is not lost as the unique
identifier is referred to, not the \'friendly\' name. When such an
object is created in AD the unique identifier (SID) for the new object
is constructed from the domain SID and a relative ID (RID) selected from
a private pool that each DC has. These private pools are replenished by
the RID master.

##### Impact on loss of DC with this FSMO role

No new AD objects can be created by a DC once its private RID pool has
run out.

#### Infrastructure Master

In environments that have \>1 domain this role holder will ensure that
cross-domain references are handled.

##### Impact on loss of DC with this FSMO role

Cross-domain referencing of objects will not work, affecting
functionality with any AD object that has entries from another domain.

#### Domain Naming Master

The Adding new DCs to the environment is handled by this role holder -
changes to the name space.

##### Impact on loss of DC with this FSMO role

No new DCs can be promoted/created.

#### Schema Master

Changes to the AD database schema are handled by this role. Exchange for
instance makes alterations to the AD DB schema.

##### Impact on loss of DC with this FSMO role

Any installation that requires an alteration to the AD DB schema would
fail.

[Category:Windows](Category:Windows "wikilink")
