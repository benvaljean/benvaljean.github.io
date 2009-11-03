---
layout: post 
title: Debian Vs Enterprise Linux
---

A comparison of commands and packages in Ubuntu/Debian and their equivalent in Redhat/CentOS

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Debian/Ubuntu'''
| align="center" style="background:#f0f0f0;"|'''CentOS'''
|-
| apt-get install build-essential||yum install gcc gcc-c++ kernel-devel
|-
| dpkg -l||yum list installed
|-
| apt-get install apache2||yum install httpd
|-
| dpkg -i package.deb||rpm -i package.rpm
|-
| apt-get install bind|| yum install bind bind-devel caching-nameserver
|-
| apt-get install dns-utils|| yum install bind-utils
|-
| adduser username|| /usr/sbin/adduser username;passwd username
|-
| ||
|-
| ||
|}


[[Category:Linux]]
