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

### Rewrite the base-URL (only) for a specific hostname

In Apache the first line would not be required if a vhost configuration
is being used. In IIRF the rewrites cannot be encapsulated within vhosts
as this configuration does not exist of course. This will rewrite the
base-url (only) to <http://www.example.com/test> when the hostname is
\'www.testing.com\':

    RewriteCond %{HTTP_HOST} ^www\\.testing\\.com$
    RedirectRule ^/$ http://www.example.com/test [R]

### Rewrite all URLs for a domain to a holding page

A situation can arise where all URLs on a domain need to be
diverted/rewritten to the same URL, such as a holding page.

    RewriteCond %{HTTP_HOST} ^test\\.jgpskills\\.co\\.uk$
    RedirectRule ^/(.*)$ /

This does not cause a rewrite loop as the pattern-match is for a \"/\"
and one or more characters but not for only the \"/\".

### Rewrite all domains to SSL, excluding one domain

    RewriteCond %{SERVER_PORT} ^80$
    RewriteCond %{HTTP_HOST} ^(?!nosslsite\\.company\\.co\\.uk)(.+)$
    RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]

### Avoid SSL certificate errors for non-canonical hostnames

If you employ a rewrite rule to force use of SSL you will find that any
non-canonical/main hostnames cause an SSL certifciate error. This can be
avoided by chaning together a rewrite rule with the \[R\] flag a visibly
redirect the client to the preferred/advertised/main hostname first,
before redirecting to SSL:

    #Rewrite all compancyabc domains to "www.compancyabc.me" before SSL rewrite to avoid cert error
    #IIRF does not support proper regex so in order to catch <anything>compancyabc... I had to put
    #"(^|.*)" before each condition
    RewriteCond %{HTTP_HOST} (^|.*)compancyabc\\.co\\.uk$ [OR]
    RewriteCond %{HTTP_HOST} (^|.*)compancyabc\\.org\\.uk$ [OR]
    RewriteCond %{HTTP_HOST} (^|.*)compancyabc\\.com$ [OR]
    RewriteCond %{HTTP_HOST} (^|.*)compancyabc\\.eu$
    RedirectRule ^/($|.*) http://www.compancyabc.me/$1 [R=301]

    #Rewrite everything to SSL apart from the root page and apart from demo sites
    RewriteCond %{SERVER_PORT} ^80$
    RewriteCond %{HTTP_HOST} ^(?!(^|.*)demo\\.compancyabc\\.co\\.uk)(.+)$
    RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]

### See Also

-   [Apache Rewrite](Apache_Rewrite "wikilink")
-   [URL rewriting with
    IIS6/7](http://stackoverflow.com/questions/550505/url-rewriting-with-iis-6-7-rewriting-host-name-httphost)

[Category:Windows](Category:Windows "wikilink")
[Category:Web](Category:Web "wikilink")
