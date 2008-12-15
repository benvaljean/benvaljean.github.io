---
layout: post 
title: NIC Bonding / Teaming on Debian
---

NIC Bonding / teaming refers to redundant NICS - setting up two NICs on
the same machine in a way so that if one fails, the other can perform
without any interpuption. It allows both NICS to have the same IP and
MAC address.

There are numerous guides on the internet showing how to accomplish
this, however this is what worked for myself on Debian:

Install ifenslave:

    apt-get install ifensalve

Add the lines below to the bottom of /etc/modprobe.d/aliases

    alias bond0 bonding
    alias eth0 e100
    alias eth1 e100
    options bonding mode=0 miimon=100

Add the lines below to the bottom of /etc/modprobe.d/arch/i386

    alias bond0 bonding
    options bonding mode=0 miimon=100 downdelay=200 updelay=200

Edit /etc/network/interfaces and comment out everything that refers to
the exisitng interfaces - eth0 and eth1 in the scenario. Then configure
the new bond0 interface like this for example:

    iface bond0 inet static
       address 192.168.10.10
       netmask 255.255.255.0
       network 192.168.10.0
       broadcast 192.168.10.255
       gateway 192.168.10.1
       hwaddress ether 00:03:B3:48:50:2D
       post-up ifenslave bond0 eth0 eth1

Now perform the following commands for the config to take affect:

    load-lodules
    modprobe bonding
    /etc/init.d/networking restart

Some strange behaviour may occur initially, like duplicate pings being
reported for instance. Wait 15 mins before testing the setup.
