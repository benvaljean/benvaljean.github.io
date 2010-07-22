---
layout: post 
title: Virtual IPs/Multiple IPs on one Network Interface (Debian/Ubuntu)
---

To add additional IPs to a single network interface add the example
config below to your `/etc/network/interfaces` file:

    auto eth0:0
    iface eth0:0 inet static
    address 192.168.40.200
    netmask 255.255.255.0
    network 192.168.40.0
    broadcast 192.168.40.255
    gateway 192.168.40.1

    auto eth0:1
    iface eth0:1 inet static
    address 192.168.50.200
    netmask 255.255.255.0
    network 192.168.50.0
    broadcast 192.168.50.255
    gateway 192.168.50.1

This presumes that your existing interface is called `eth0`. It can be
checked by running the `ifconfig` command. Ensure that your virtual
interfaces start with a 0 and not a 1.

[Category:Linux](Category:Linux "wikilink")
