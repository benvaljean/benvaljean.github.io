---
layout: post 
title: Linux Web Troubleshooting
---

### Telnet port 80

Allows all output to be seen for easier troubleshooting.

    [user@host ~]$ telnet google.com 80
    Trying 209.85.229.99...
    Connected to google.com.
    Escape character is '^]'.
    GET /
    HTTP/1.0 302 Found
    Location: http://www.google.co.uk/
    Cache-Control: private
    Content-Type: text/html; charset=UTF-8
    Set-Cookie: PREF=ID=aca7ce20b11489b5:TM=1273490037:LM=1273490037:S=efOcyW5HLidr1H2B; expires=Wed, 09-May-2012 11:13:57 GMT; path=/; domain=.google.com
    Date: Mon, 10 May 2010 11:13:57 GMT
    Server: gws
    Content-Length: 221
    X-XSS-Protection: 1; mode=block

    <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
    <TITLE>302 Moved</TITLE></HEAD><BODY>
    <H1>302 Moved</H1>
    The document has moved
    <A HREF="http://www.google.co.uk/">here</A>.
    </BODY></HTML>
    Connection closed by foreign host.

#### See Also

-   [Telnet port 80 whilst specifying
    Hostname](Telnet_port_80_whilst_specifying_Hostname "wikilink")
-   [cURL](http://curl.haxx.se/download.html)

### OpenSSL s\_client for telnet-like troubleshooting for SSL connections

Ensure that [openssl](http://www.topology.org/linux/openssl.html) is
installed.

    openssl s_client -connect hostname:port

Normal GET and HEAD etc. statements can now be typed in as if it was a
normal HTTP session.

### View packets in tcpdump

If networking needs to be eliminated from troubleshooting.\
Run this on a client:

    sudo tcpdump -s 0 -A 'tcp dst port 80'

And/or the following on a server:

    sudo tcpdump -s 0 -A 'tcp host client.ip.address'

This will show the full ASCII packet. Obviously this will not work for
SSL connections.

[Category:Linux](Category:Linux "wikilink")
[Category:Web](Category:Web "wikilink")
