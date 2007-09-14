---
layout: post 
title: Reinitialise database (Arcserve)
---

![Reinitialise database
(Arcserve)](Reinit_Arcserve.GIF "fig:Reinitialise database (Arcserve)")
**<font color="red">Reinitialising the databases will clear ALL rotation
job data as well as session information</font>**

To reinitialise the ARCserve database:

1.  Open the ARCserve Manager, usually located at: C:\\\\Program
    Files\\\\CA\\\\BrightStor ARCserve Backup\\\\BrightStorMgr.exe
2.  Select Quickstart \> Server Admin menu item
3.  Select Operation \> Initialise Database\... menu item
4.  Select the databases to reinitialise and click Initialise.

If reinitialising due to [database
corruption](Database_Corruption_(Arcserve) "wikilink") in the first
instance only reinitialise the astpsdat and asobject database. These are
the largest databases as they contain session data. Consequently
corruption is usually in one of these databases and reinitialising these
only will keep the media pool / rotation information.

#### Troubleshooting

If a EC-1 error is given: \"Server x failed to authenticate the user
caroot (EC=-1)\" check that the Brightstor services are running.

[Category:Arcserve](Category:Arcserve "wikilink")
