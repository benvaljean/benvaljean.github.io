---
layout: post 
title: Database login problems / Cannot run VLDB utilities / -2005 error (Arcserve)
---

### Symptom

When attempting to run one of the **V**ery **L**arge **D**ata**B**ase
utilities for Computer Associates Brightstor ARCServe the following
error appears:

` Failed to log into server 'casdb', username 'USERID': error -2005`

### Cause

1.  Incorrect login credentials provided
2.  Database engine service not running
3.  Temporary checkpoint files causing issues
4.  Check syntax

### Resolution

These resolutions correspond to the numbers above. Try them one at a
time, retrying the vldb-utility command after each one.

1\. Check that the login credentials are correct. For **every**
installation of Arcserve the credentials are **always the same** even if
you are using a SQL server as your database:

` Database name: "casdb"`\
` Login: "admin"`\
` Password: "secret"`

![All services stopped apart from the database
engine](ARCServe_Services.GIF "fig:All services stopped apart from the database engine")
2. For correct operation of the VLDB utilities every service should not
be running apart from the Database engine. To do this run services.msc ,
find the services beginning with CA Brightstor and stop all of them
apart from \"CA Database Engline.\"

3\. Remove temporary files

:\#Ensure the database engine is not running. Check that rds.exe is not
running - if it is kill it. If you are unable to kill it due to an
\"access denied\" message in task manager set the service to disabled
and reboot.

:\# Delete \*.tmp in <arcservedir>/temp

:\# Delete r\*.\* in <arcservedir>/database

4\. Sometimes an incorrect syntax can produce an error like the one
documented here or similar to it. When specifying the database name do
not supply the whole filename - Arcserve only requires the common name
of the database itself and not the exact filenames. For instance:

` dbfix -a -L casdb;admin;secret astpsdat`

This will perform all the checks on the astpsdat database. Arcserve will
check the astpsdat.001; astpsdat.002 \... files in turn. Supplying
\"astpsdat.001\" as a parameter will not work.

If performing a dbfix on all the databases does nothing the only option
is to [Reinitialise the
database](Reinitialise_database_(Arcserve) "wikilink").

[Category:Arcserve](Category:Arcserve "wikilink")
