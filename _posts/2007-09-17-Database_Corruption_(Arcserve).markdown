---
layout: post 
title: Database Corruption (Arcserve)
---

Database corruption affects detailed session records even if a merge is
done on the tape. Consequently restore by session/tree/query does not
work but the backed up data itself is unaffected. For a quick work
around to enable the restoration of data without investigating/fixing
database corruption choose **Restore by Media**. This does not rely on a
Arcserve database but a whole particular session will have to be
restored, although file filters (such as \*.doc) can be specified.

### Symptoms

Symptoms can be any or all of the following:

-   Asterixes (\*) appear next to the job ID in the activity log;
    indicating issues updating the database in the job the *last* time
    it was run.
-   Backup job hanging at 99% complete
-   rds.exe (Arcserve database engine process) utilising as much CPU as
    it can - typically 99%.
-   E3073 Unable to login as user (User=xxx EC=xxx). Although this error
    could be incorrect caching of the login details. Try re-entering the
    system account in Server Admin and then restarting the Arcserve
    services.
-   \*.cat files in the <Arcserve dir>\\\\TEMP directory when no jobs
    are running. This is session data that should have merged into the
    database.
-   E4101 Unable to login to database engine (DATABASE=CASDB, EC=-2005)
    Do not confuse this error with the one outlined in [Cannot login to
    VLDB Utilites](Cannot_run_VLDB_Utilities_(Arcserve) "wikilink");
    which could be completely different.

### Cause

-   Not running regular maintenance: Utilities such as dgfix, dbdefrag
    and keybuild.
-   Shutdown/Server crash whilst the database is bring written to.
-   Server runs out of disk space
-   Database size limit reached: The maximum size is 360m records -
    \~36Gb of data. Each file backed up uses \~80 bytes of data in the
    database.
-   Database prune time: Prune jobs running whilst a backup or restore
    is done on a regular basis has been known to cause corruption. The
    default time for the prune job as midnight. This is the worst time
    to do this as usually backups are occurring at this time. A daily
    prune job for midday is recommended.

### Resolution

Corruption is usually in the astpsdat database as this contains session
data and therefore the bulk of data associated with Arcserve; therefore
it is prudent to start here. Like all Arcserve databases it can be
presented in chunks to the filesystem itself (.001, .002 etc.) but the
database name as a whole is always supplied to the VLDB utilities.

1.  For correct operation of the VLDB utilities every service should not
    be running apart from the Database engine. To do this run
    services.msc , find the services beginning with CA Brightstor and
    stop all of them apart from \"CA Brightstor Database Engline.\"
2.  Open a commend prompt and change to the Arcserve directory, type:
    dbdefrag -a -L casdb;admin;secret astpsdat
3.  Followed by: keybuild -k -L casdb;admin;secret astpsdat

These commands can reduce the size of the database and therefore reduce
the time for checks on the database if required. Test whether the issue
is resolved, if the issue is resolved, you do not have to follow the
remaining steps. If the issue is not resolved, go to step 3, and then
follow the remaining steps.

:   4\. dbfix -a -L casdb;admin;secret astpsdat

Depending on the amount of corruption and the size of the database this
usually takes 12 hours or even several days. If it is still running
after 48 hours or if the above command does not fix the corruption the
next step is to [reinitialise the
database](Reinitialise_database_(Arcserve) "wikilink").
