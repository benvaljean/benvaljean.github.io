---
layout: post 
title: ActiveSync Error 0x85010005 (Outlook Mobile Access)
---

When attempting to syncronise all or part of a mailbox in ActiveSync on
a Windows Mobile based phone through the use of a wireless connection
the following error can occur:

**The server could not be reached. This can be caused by temporary
network conditions. Support code: 0x85010005**

Contrary to the statement above the server **can be reached** but is
giving a 404 Not found error for the OMA virtual directory on the web
server that the hostname entered for the server is on. The most likely
candidates for this error are:

1.  An incorrect hostname/server name has been entered that is a web
    server but does not host Outlook Mobile Access (OMA) on it.
2.  The server entered no longer has Exchange or Outlook Mobile Access
    installed on it.
3.  If using [SSL Explorer](http://3sp.com/showSslExplorerCommunity.do)
    on the free/community license and this has suddenly started occuring
    the trail version has expired. - OMA among other features is only
    available on the Enterprise addition.
4.  The OMA virtual directory has been accidentally deleted on the
    [Internet Information
    Services](http://www.microsoft.com/windowsserver2003/iis/default.mspx)
    server that OMA is hosted. By default this is the first Exchange
    server in your enterprise. If this is the case the OMA directories
    will need to be re-created: [Recreating IIS virtual directories for
    OWA, OMA and Exchange
    ActiveSync](http://searchexchange.techtarget.com/tip/0,289483,sid43_gci1240016,00.html)
5.  Firewall configuration has been changed causing the IP address
    resolved from the server entered pointing to the wrong server on the
    DMZ/LAN.

### See Also

[ActiveSync Errors
Guide](http://www.shijaz.com/exchange/activesync_errors.htm)

[Category:Windows](Category:Windows "wikilink")
[Category:Exchange](Category:Exchange "wikilink")
