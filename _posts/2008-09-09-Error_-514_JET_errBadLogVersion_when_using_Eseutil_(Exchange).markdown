---
layout: post 
title: Error -514 JET errBadLogVersion when using Eseutil (Exchange)
---

### Symptom

When either using the `ESEUTIL` in an operation the following error can
occur:

    Operation terminated with error -514 (JET_errBadLogVersion, Version of log file is not compatible with Jet version) after x seconds.

This error refers to a mismatch of the version of the server that the
log files were created (SP1, SP2 etc.) and the version of the server
itself. For this reason it is always important to perform a full backup
before and after upgrading the Service Pack version of Exchange.

It can occur when using the `eseutil /k` command to check for file
header damage or or the `eseutil /cc` command to begin hard recovery/log
file replay when restoring an exchange database or any other operation.

### Cause

Primary causes are:

1.  Particularly when resotirng an Exchange database to a new server;
    ensure that that both the service pack version on the source and
    destination server match. For instance if the server that had the
    Exchange database originally was SP2 the new one **must also have
    SP2 installed.**
2.  No full backup has been performed since the Service Pack version was
    upgraded.
3.  A specific error relating to transaction log files created before
    SP1 on a server that has SP1 installed: [MSKB
    890056](http://support.microsoft.com/kb/890056)
4.  When attempting to perform an operation normally associated on a log
    file but on a database file (.edb) or streaming database (.stm). For
    instance `eseutil /ml priv1.edb` will generate this error.

### See Also

-   [Exchange JET engine error
    codes](http://www.dtidata.com/exchange_recovery/Exchange_error_codes.htm)
-   [Exchange Server Error
    Codes](http://www.innovativetechnologyconcepts.com/Exchange_Server_Error_Codes.htm)
-   \[<http://technet.microsoft.com/en-us/library/bb123621(EXCHG.65>).aspx
    Reference for Common Eseutil Errors (Microsoft Technet)\]
