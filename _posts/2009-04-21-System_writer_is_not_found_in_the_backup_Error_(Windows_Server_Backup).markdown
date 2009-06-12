---
layout: post 
title: System writer is not found in the backup Error (Windows Server Backup)
---

yyKuqp <a href="http://cjubfubhhywi.com/">cjubfubhhywi</a>,
\[url=<http://ughyvjhgvqjz.com/%5Dughyvjhgvqjz%5B/url%5D>,
\[link=<http://exzldopjdyzt.com/%5Dexzldopjdyzt%5B/link%5D>,
<http://truuqlxaesdw.com/>

### Causes

Any of the following:

1.  The cryptographic service is failing, a dependancy of the VSS System
    Writer entry which Windows Server Backup uses to backup the data. If
    this entry is missing the data cannot be read.
2.  Incorrect permissions on or within: %windir%\\\\winsxs\\\\filemaps

### Resolution

1\. Issues with cryptographic can onrmally be resolved by restarting the
service. If this does not resolve the issue look for entries in the
event log when the service was restarted.\
2. The correct permissions for %windir%\\\\winsxs\\\\filemaps are:

-   Local administrators, or Domain administrators if a DC: Owner,
    Read&exec, List folder, Read
-   SYSTEM: Permissions as above excluding Owner
-   Local Users, or Domain Users (may not be required): As above
-   TrustedInstaller: Full Control
