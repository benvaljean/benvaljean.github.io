---
layout: post 
title: Apache Rewrite
---

Rewrite might not always be required, changing one static URL to another
Redirect can be used:

    #Redirect the base-URL (only) to https
    Redirect permanent / https://mydomain.com
    #Redirect a particular uri to another url
    Redirect permanent /foo http://www.foobar.com/bar

### Redirecting to https / Force use of SSL

    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

This works great with Apache but not ISAPI\_Rewrite, the following must
be used:

    RewriteCond  %HTTPS (?!on).*
    RewriteCond Host: (.*)
    RewriteRule (.*) https\\://$1$2 [I,RP]

This can be expanded to rewrite all URLs apart from a given two:

    RewriteCond  %HTTPS (?!on).*
    RewriteCond Host: test\\.test\\.co\\.uk
    RewriteRule (.*) http\\://test\\.test.co.uk$1 [I,RP,L]

    RewriteCond  %HTTPS (?!on).*
    RewriteCond Host: demo\\.test\\.co\\.uk
    RewriteRule (.*) http\\://demo\\.test.co.uk$1 [I,RP,L]

    RewriteCond  %HTTPS (?!on).*
    RewriteCond Host: (.*)
    RewriteRule (.*) https\\://$1$2 [I,RP]

### Hiding PHP script names

The following will allow <http://www.whatever.com/car_info_v4_5.php> to
be accessed via <http://www.whatever.com/cars/>

    RewriteRule    ^cars/?$ car_info_v4_5.php [NC,L]

### See Also

[Rewrite on IIS](Rewrite_on_IIS_that_actually_works "wikilink")

[Category:Web](Category:Web "wikilink")
[Category:Linux](Category:Linux "wikilink")
