---
layout: post 
title: Stop Producing Backscatter Spam (Exchange 2003/2007)
---

### Introduction

[Back-scatter](http://en.wikipedia.org/wiki/Backscatter_(e-mail)) spam
is when a server generates a bounce NDR email that is sent to a forged
email address in responce to receving spam-email sent to an email
address that does not exist, usually intentionally.

### Disable the sending of NDRs and bounce incorrectly addressed emails at the MTA level

Perform the steps below and a server that attempts to send email to your
server with an incorrect to-address will be rejected during the SMTP
session (at the MTA level) and no NDR/bounce will be generated:

1.  Open
    \[<http://technet.microsoft.com/en-us/library/aa995785(EXCHG.65>).aspx
    Exchange System Manager\]: Go to Start \> Programs \> Microsoft
    Exchange \> System Manager.
2.  Expand **Global Settings**, right-click **Message Delivery** and
    choose **Properties**.
3.  Under the **Recipient** tab check the **Filter recipients who are
    not in the Directory** check-box.

To ensure your SMTP server applies these settings:

1.  Expand the Exchange server that send emails to the internet under
    **Administrative Groups**, **First Administrative Group**,
    **Servers**
2.  Expand **Protocols**, **SMTP**, right-click **Default Virtal SMTP
    Server** and choose **Properties**.
3.  Under the **General** tab click **Advanced**.
4.  Click **Edit** and check the **Apply Recipient Filter** check-box
5.  Restart the SMTP service:
    1.  Start \> Run \> cmd
    2.  net stop \"Simple Mail Transfer Protocol (SMTP)\"
    3.  net start \"Simple Mail Transfer Protocol (SMTP)\"

### See Also

[1](http://spamlinks.net/prevent-secure-backscatter.htm)

[Backscatter: What is it? How do I stop
it?](http://www.spamresource.com/2007/02/backscatter-what-is-it-how-do-i-stop-it.html)
