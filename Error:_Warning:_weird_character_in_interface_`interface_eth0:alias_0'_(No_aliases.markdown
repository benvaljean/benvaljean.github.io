---
layout: post 
title: Error: Warning: weird character in interface `interface eth0:alias 0' (No aliases
---

Benjamin Goodacre,f1\@goodacre.name,==Symptom== When adding a new
iptables rule the following error can appear:

    Warning: weird character in interface `eth0:1' (No aliases, :, ! or *).

Where `eth0` is your interface and `1` is the alias or virtual
interface.

### Cause

Aliases / virtual interfaces are not allowed in iptables. Aliases have
offically been depreciated in favour of using the `ip` command but they
are still widely used.

### Resolution

Depending on the type of rule the `-s` (source) or `-d` (destination)
parameter can be used to limit the rule to a specific interface.

    #Only allow interfaces with ips 1.1.1.1 and 2.2.2.2 to accept pings
    -A icmp_packets -d 1.1.1.1 -p icmp -m icmp --icmp-type 8 -j ACCEPT
    -A icmp_packets -d 2.2.2.2 -p icmp -m icmp --icmp-type 8 -j ACCEPT
    #Deny pings on interface with ip 3.3.3.3
    -A icmp_packets -d 3.3.3.3 -p icmp -m icmp --icmp-type 8 -j DROP

    #Block port 80 on interface with ip 1.1.1.1
    -A INPUT -d 1.1.1.1 -p tcp -m tcp --dport 80 -j ACCEPT

    #Unless you have a specific binding order there is normally no need to limit
    #which interfaces can make out going connections.

    #Only allow interface with ip 2.2.2.2 to perform DNS queries
    -A OUTPUT -s 2.2.2.2 -p udp -m tcp --dport 53 -j ACCEPT

    #Only allow interface with ip 3.3.3.3 to perform AXFRs
    -A OUTPUT -s 3.3.3.3 -p tcp -m tcp --dport 53 -j ACCEPT

[Category:Linux](Category:Linux "wikilink")
[Category:Networking](Category:Networking "wikilink")
