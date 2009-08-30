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

### Redirecting http to https / Force use of SSL

    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

OR

    RewriteCond %{SERVER_PORT} ^80$
    RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]

### Hiding PHP script names

The following will allow <http://www.whatever.com/car_info_v4_5.php> to
be accessed via <http://www.whatever.com/cars/>

    RewriteRule    ^cars/?$ car_info_v4_5.php [NC,L]

### Force the use of the primary hostname

Having multiple ServerName and/or ServerAlias configs will in normal
cases create duplicate sites to serch engines as Apache will serve pages
containing the domain used by the client. It can therefore be preferable
to divert users to a the primary domain of your site, by replacing the
domain of the URL. The below Rewrite rule will replace
www.anydomain.com/anything if the domain is not www.primarydomain.com .

    RewriteCond %{HTTP_HOST} !^www\\.primarydomain\\.com$ [NC]
    RewriteRule ^/($|/.*) http://www.primarydomain.com/$1 [R=301]

### See Also

[Rewrite on IIS](Rewrite_on_IIS_that_actually_works "wikilink")

[Category:Web](Category:Web "wikilink")
[Category:Linux](Category:Linux "wikilink")
