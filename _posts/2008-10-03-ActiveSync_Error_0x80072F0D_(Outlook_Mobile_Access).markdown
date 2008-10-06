---
layout: post 
title: ActiveSync Error 0x80072F0D (Outlook Mobile Access)
---

When attempting to syncronise all or part of a mailbox in ActiveSync on
a Windows Mobile based phone through the use of a wireless connection
the following error can occur:

    The security certificate on the server is invalid. 
    Contact you exchange server administrator or ISP to install a valid certificate on the server.
    Support code 0x80072F0D

<font color=green>In the first instance contact the person who manages
your Exchange Server or the IT Helpdesk in your company if you have one
and ask them to put the SSL security certificate on your phone.</font>

Contrary to the error message in almost all cases this refers to an
issue at the client/mobile phone end of the session. All Activesync
communications are SSL by default and should not be set to not use SSL
for security reasons. SSL communications require the use of certificates
and these are trusted by a Certificate Authority (CA) such as Verisign.
The Windows Mobile based phone only trusts limited list of CAs by
default; as does Internet Explorer and other browsers. If your
certificate is self-signed and therefore not purchased from a CA the
Windows Mobile based phone will not use it for security reasons. In this
scenario on a PC it is possible to add an exception to use the
certificate anyway, however this option is not available on the phone
and the certificate must be installed onto the device.

To export the certificate from IIS:

1.  Run **iis.msc**
2.  Right-click the website and choose **Properties**; click the
    **Directory Secutity** tab and choose **View Certificate**.
3.  Click the **Certification Path** tab and choose the
    root-certificate; this is at the rop of the list and should equal
    the name of the domain of the website used to access Outlook
    Web/Mobile Access. Do not choose \"OWA SSL Certificate\".
4.  Click **View Certificate**; followed by the **Details** tab and
    click on **Copy to file**.
5.  Leave the Export file format as the default and choose a filename.

To add the file to your device either email it using POP3 or IMAP or
install ActiveSync on a PC and click Explore and drag the file to your
phone.

To install the certificate on the phone open File Explorer and simply
click on the file.

ActiveSync will now no longer result in this error.

### See Also

\     [How to install root certificates on a Windows Mobile-based device
(Microsoft)](http://support.microsoft.com/kb/915840/en-us)\
\     [0x80072F0D in Mobile Active Sync Device (Experts
Exchange)](http://www.experts-exchange.com/Networking/Email_Groupware/Exchange_Server/Q_21905403.html)\
[ActiveSync Errors
Guide](http://www.shijaz.com/exchange/activesync_errors.htm)

[Category:Windows](Category:Windows "wikilink")
