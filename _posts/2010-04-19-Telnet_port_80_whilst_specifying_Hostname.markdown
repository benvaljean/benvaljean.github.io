---
layout: post 
title: Telnet port 80 whilst specifying Hostname
---

Telnetting to port 80 is very useful in diagnosing whether or not a
website is running in more discrete terms than using a browser however
if you need to specify a specific hostname telnet cannot do this of
course as there is no ability to mention a hostname in the GET
statement. [Curl](http://curl.haxx.se/) can do this of course but if you
are on a machine that does have it installed you can achieve this by
using the HTTP 1.1 syntax within telnet.

#### Example

This example views the 301 redirect from goodacre.name to
ben.goodacre.name :

    benyg@tcuk-029:~$ telnet ben.goodacre.name 80
    Trying 67.223.225.228...
    Connected to goodacre.name.
    Escape character is '^]'.
    GET / HTTP/1.1
    Host: goodacre.name

    HTTP/1.0 301 Moved Permanently
    Date: Mon, 19 Apr 2010 10:49:13 GMT
    Server: Apache/2.2.4 (Ubuntu) PHP/5.2.3-1ubuntu6.3
    Location: http://ben.goodacre.name/
    Content-Length: 332
    Content-Type: text/html; charset=iso-8859-1
    X-Cache: MISS from localhost
    X-Cache-Lookup: MISS from localhost:80
    Via: 1.0 localhost (squid/3.0.PRE6)
    Connection: close

    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
    <html><head>
    <title>301 Moved Permanently</title>
    </head><body>
    <h1>Moved Permanently</h1>
    <p>The document has moved <a href="http://ben.goodacre.name/">here</a>.</p>
    <hr>
    <address>Apache/2.2.4 (Ubuntu) PHP/5.2.3-1ubuntu6.3 Server at goodacre.name Port 80</address>
    </body></html>
    Connection closed by foreign host.

Note: Enter must be pressed twice after specifying the
`Host: domain.com` line.

[Category:Web](Category:Web "wikilink")
