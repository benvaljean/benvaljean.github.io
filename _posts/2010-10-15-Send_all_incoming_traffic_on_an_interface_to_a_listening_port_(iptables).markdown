---
layout: post 
title: Send all incoming traffic on an interface to a listening port (iptables)
---

Send all incoming TCP traffic on interface eth1 to port 3128 on any
interface:

    sudo iptables -A PREROUTING -i eth1 -p tcp -j REDIRECT --to-ports 3128

iptables output should look like:

    # iptables -t nat -nvL PREROUTING
    Chain PREROUTING (policy ACCEPT 516K packets, 51M bytes)
     pkts bytes target     prot opt in     out     source               destination   
    ....      
    xxxK  xxxM REDIRECT   tcp  --  eth1   *       0.0.0.0/0            0.0.0.0/0           redir ports 3128 

[Category:Networking](Category:Networking "wikilink")
[Category:Linux](Category:Linux "wikilink")
[Category:iptables](Category:iptables "wikilink")
