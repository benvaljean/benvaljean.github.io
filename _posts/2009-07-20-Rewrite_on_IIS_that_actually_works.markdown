---
layout: post 
title: Rewrite on IIS that actually works
---

It is amazing to think that before IIS7 (Server 2008 / Vista) there was
no native rewrite URL support for IIS.

### mod\_rewrite for IIS

There are many tools available to give rewrite functionality for IIS,
most of which I have tried and do not work properly or do not fully
support [regex](http://www.regular-expressions.info/). The best tool I
have found for the job is [IIRF](http://www.codeplex.com/IIRF). Like
other tools available of this type it loads through an ISAPI filter
extension - but unlike others **it actually works**. There are a few
nuances to be aware of though.

### Installation

1.  Download and extract to any location eg. C:\\\\Rewrite:
    <http://iirf.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=29936#DownloadId=74545>
2.  Load IIS console: Start \> Run \>
    %SystemRoot%\\\\system32\\\\inetsrv\\\\iis.msc
3.  Right-click \'Web sites\' \> ISAPI Filters \> Add
4.  Type a name to recognise it by under \'Filter name\' and select the
    IsapiRewrite4.dll file inside the lib folder of the extracted
    archive under \'Executable\'. The filter may not appear to have
    loaded OK straight away, this is OK.
5.  Go to \'Web service extensions\' in the main window.
6.  Click \'Add a new Web Service extension\...\'
7.  Type in the same details as before, ensure the allow checkbox is
    ticked.
8.  The config file is not created for you, the rewriter looks for a
    file called IsapiRewrite4.ini in the same folder as the
    IsapiRewrite4.dll file itself.

### Notes

-   The rewriter watches for changes in the ini file - no need to
    restart IIS.
-   The rewrite log filename must be set to iirfLog.out and NOT in a
    root folder else it will not log anything.
-   Use the TestParse.exe programme inside the bin directory to test
    your configuration first. The file must be in the same dir as
    IsapiRewrite4.dll .
-   It is not 100% copy of mod\_rewrite - such a thing does not exist.
    This is the nearest I have found. For instance
    `RewriteCond %{SERVER_PORT} !^443$`will not hit the appropriate rule
    if the port is 80, which of course it should do. I worked around
    this by using `RewriteCond %{SERVER_PORT} ^80$`instead as our server
    only needs to listen on port 80.

### Example working configuration of IIRF on IIS on Windows

    #Enable rewrite logging, very useful. 5 is very verbose, set to 3 unless troubleshooting.
    RewriteLog  c:\    emp\\iirfLog.out
    RewriteLogLevel 5

    #testing
    #redirects /misc/anything to /misctest/anything
    #will not redirect /misc to /misctest due to the tailing slash
    RewriteRule ^/misc/(.*)$ /misctest/$1 [I]

    #Rewrite all traffic to SSL
    RewriteCond %{SERVER_PORT} ^80$
    RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]

[Category:Windows](Category:Windows "wikilink")
[Category:Web](Category:Web "wikilink")
