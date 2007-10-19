---
layout: post 
title: Apache Stuff
---

owa reverse proxy
-----------------

ExtFilterDefine fixowa mode=output
cmd=\"/bin/seds/http:\\\\\\\\/\\\\\\\\/tsct.phrihawaii.org/https:\\\\\\\\/\\\\\\\\/tsct.phrihawaii.org/g\"
Header unset \"WWW-Authenticate: NTLM\" Header add WWW-Authenticate
\"Basic realm=tsct.phrihawaii.org\"

Header set Host owaproxy.domainname.tld RequestHeader set Host
owaproxy.domainname.tld

------------------------------------------------------------------------

Hirantha,

You\'re 90% there. Remove your /etc/hosts entry:

192.168.100.1 webmail.exchange.com webmail

And add this to your httpd.conf:

ProxyPreserveHost On

This works with Exchange 2003; I\'m not sure if it will work with
Exchange 20 00.

Karnov

ps - you might need to move the :443 Virtual host to ssl.conf

In article \<e78bb4db.0406290221.4bbabac3\@posting.google.com\>,
Hirantha says\... \> \>Dear karnov, \> \>I\'m struggling to setup to
publish my Exchange 2000 OWA in Apache2 \>with Reveres Proxy.
Unfortunately still I couldn't achieve it. \>If don\'t you mind would
you like to help with your configurations, how \>to configure Apache
server & relevant objects. The following is my \>current setup \>I have
Apache-2.0.40-21 \> Openssl-0.9.7a-2 \> Mod\_ssl-2.0.40-21 rpm
installed. \>Exchange server on 192.168.100.1 mail.exchange.com ;;
exchange 2000 \>sever \>Apache2 server on 192.168.100.2
apache2.exchange.com ;; RedHat Linux \>v9 \> \>In Apache2 \>/etc/hosts
file \>192.168.100.2 apache2.exchange.com \>192.168.100.1
webmail.exchange.com webmail \> \>My httpd.conf is. \> \>\<VirtualHost
192.168.100.2:80\> \>ServerName webmail.exchange.com \>DocumentRoot
/var/www/html/html.webmail \>RedirectMatch \^/(index.html?)\$
<https://mail.exchange.com/exchange/> \>RedirectMatch \^/exchange\$
<https://mail.exchange.com/exchange/> \></VirtualHost> \>
\>\<VirtualHost 192.168.100.2:443\> \>ServerName webmail.exchange.com
\>DocumentRoot /var/www/html/html.webmail \>RedirectMatch
\^/(index.html?)\$ <https://mail.exchange.com/exchange/> \>RedirectMatch
\^/exchange\$ <https://mail.exchange.com/exchange/> \>ProxyPass /public/
<https://mail.exchange.com/public/> \>ProxyPassReverse /public/
<https://mail.exchange.com/public/> \>ProxyPass /exchweb/
<https://mail.exchange.com/exchweb/> \>ProxyPassReverse /exchweb/
<https://mail.exchange.com/exchweb/> \>ProxyPass /exchange/
<https://mail.exchange.com/exchange/> \>ProxyPassReverse /exchange/
<https://mail.exchange.com/exchange/> \></VirtualHost>

------------------------------------------------------------------------
