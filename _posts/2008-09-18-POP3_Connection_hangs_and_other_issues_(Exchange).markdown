---
layout: post 
title: POP3 Connection hangs and other issues (Exchange)
---

This article details various connection issues to [Microsoft
Exchange](http://www.microsoft.com/exchange/default.mspx) via the POP3
protocol and offers solutions.

### Symptoms

-   Unable to connection to POP3 - connection refused
-   A connection is started except it hangs with no server banner/header
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
4.  Check that the POP3 virtual server is listening to the correct port:
    Open [Exchange System
    Manager](http://searchexchange.techtarget.com/tip/1,289483,sid43_gci1115770,00.html),
    navigate to the server \> Protocols \> POP3 \> Default POP3 Virtual
    Server and choose properties. Click on the General tab followed by
    Advanced. Ensure that the server is listening to the default port -
    110 - or the port where a connection is being attempted.
5.  Ensure that no other applications are listening to the port that
    POP3 is listening to: From cmd type `netstat -abn` to ascertain
    which applications are listening to which ports. If any apps are
    listening to the same port this would cause the connection to fail
    of course.
6.  Ensure no connection control parameters have been set: From Default
    POP3 Virtual Server properties click on the Access tab followed by
    Connection. If the list is empty and \'Only the list below\' is
    selected this can cause the connection to fail where the connectio
    is started but no server banner/header (beginning +OK) is ever
    displayed.

### See Also

-   [How to enable the POP3 service in Exchange
    Server](http://msmvps.com/blogs/andersonpatricio/pages/AP0035.aspx)
-   [Using Telnet to connect to Exchange 2003 POP3
    mailboxes](http://www.msexchange.org/tutorials/Telnet-Exchange2003-POP3-SMTP-Troubleshooting.html)
-   \[<http://technet.microsoft.com/en-us/library/cc540466(EXCHG.80>).aspx
    How to Connect to an Exchange Mailbox by Using POP3 or IMAP4\]
