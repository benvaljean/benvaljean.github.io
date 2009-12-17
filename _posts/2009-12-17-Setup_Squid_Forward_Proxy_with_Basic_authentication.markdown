---
layout: post 
title: Setup Squid Forward Proxy with Basic authentication
---

On Debian/Ubuntu and related distros:

    sudo apt-get install squid3
    sudo vim /etc/squid3/squid.conf

On RHEL/CentOS/Fedora and related distros:

    sudo yum instll squid
    sudo vim /etc/squid/squid.conf

Add the following lines to squid.conf:

    #If you would like Squid to listen to a port other than its default port 3128, add the port no below
    http_port 12121

    #To disable authentication, fill in your network details and un-comment the lines below
    #acl our_networks src 10.1.1.0/24
    #http_access allow our_networks

    visible_hostname proxy.yourcompany.local

    acl require_pass proxy_auth REQUIRED
    http_access allow require_pass

    auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
    auth_param basic children 5
    auth_param basic realm Squid proxy-caching web server
    auth_param basic credentialsttl 2 hours
    auth_param basic casesensitive off

The passwd file, storing your username/password details must noe be
created: `htpasswd -c /etc/squid/passwd username`

Finally start Squid:\
Debian/Ubuntu and related distros: `sudo /etc/init.d/squid3 start`\
RHEL/CentOS/Fedora and related distros: `sudo /etc/init.d/squid start`

[Category:Squid](Category:Squid "wikilink")
[Category:Linux](Category:Linux "wikilink")
