---
layout: post 
title: POP3 Connection hangs and other issues (Exchange)
---

This article details various connection issues to [Microsoft
Exchange](http://www.microsoft.com/exchange/default.mspx) via the POP3
protocol and offers solutions.

### Symptoms

-   Unable to connection to POP3 - connection refused
-   A connection is started except it hangs with no server header
    (beginning with +OK) is shown.
-   An incorrect password error is shoen despite is being known that the
    password is correct.

### Resolution

Attempt the following fixes in order, whilst re-attempting the
connection each time.

1.  Ensure that the virtual server/service is running. From cmd type
    `services.msc` and select the \'Microsoft Exchange POP3\' serice and
    ensure that it is started and in particular not disabled.
2.  Restart the POP3 service. From the same window as details above
    right click the \'Microsoft Exchange POP3\' service and choose
    restart.
3.  Eliminate firewalling or other network issues as a possibility. try
    connecting to it locally. From the server itself in cmd type
    `telnet 127.0.0.1 110` where 100 is the port that the service is
    listening to.
