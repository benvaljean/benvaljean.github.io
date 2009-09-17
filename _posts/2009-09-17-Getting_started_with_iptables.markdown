---
layout: post 
title: Getting started with iptables
---

[iptables](http://www.netfilter.org) is the native firewall for Linux.

To view the current FW rules in place:

    iptables -L

The iptables command can be used to append/modify rules but it is a lot
easier to use an iptables script. This is a text file with all your
rules.

Example iptables script with lots of examples, modify for your own
needs:

    #The NAT portion of the ruleset. Used for Network Address Transalation.
    #Usually not needed on a typical web server, but it's there if you need it.
    *nat
    :PREROUTING ACCEPT [127173:7033011]
    :POSTROUTING ACCEPT [31583:2332178]
    :OUTPUT ACCEPT [32021:2375633]
    COMMIT

    #The Mangle portion of the ruleset. Here is where unwanted packet types get dropped.
    #This helps in making port scans against your server a bit more time consuming and difficult, but not impossible.
    *mangle
    :PREROUTING ACCEPT [444:43563]
    :INPUT ACCEPT [444:43563]
    :FORWARD ACCEPT [0:0]
    :OUTPUT ACCEPT [402:144198]
    :POSTROUTING ACCEPT [402:144198]
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG FIN,PSH,URG -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags SYN,RST SYN,RST -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN FIN,SYN -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG FIN,PSH,URG -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags SYN,RST SYN,RST -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN FIN,SYN -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG FIN,PSH,URG -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags SYN,RST SYN,RST -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN FIN,SYN -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG FIN,PSH,URG -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags SYN,RST SYN,RST -j DROP
    -A PREROUTING -p tcp -m tcp --tcp-flags FIN,SYN FIN,SYN -j DROP
    COMMIT

    #The FILTER section of the ruleset is where we initially drop all packets and then selectively open certain ports.
    #We will also enable logging of all dropped requests.
    *filter
    :INPUT DROP [1:242]
    :FORWARD DROP [0:0]
    :OUTPUT DROP [0:0]
    :LOG_DROP - [0:0]
    :LOG_ACCEPT - [0:0]
    :icmp_packets - [0:0]

    #First, we cover the INPUT rules, or the rules for incoming requests.
    #Note how at the end we log any incoming packets that are not accepted.
    -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 20 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 21 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 22 -j LOG_ACCEPT
    #-A INPUT -p tcp -m tcp --dport 25 -j LOG_ACCEPT
    #-A INPUT -p tcp -m tcp --dport 43 -j ACCEPT
    #-A INPUT -p udp -m udp --dport 53 -j ACCEPT
    #allow everything inbound port 80
    -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 110 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 143 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 993 -j ACCEPT
    #-A INPUT -p tcp -m tcp --dport 3306 -j ACCEPT
    #allow traffic inbound all ports from 2.2.2.2
    -A INPUT -s 2.2.2.2 -j ACCEPT

    -A INPUT -s 127.0.0.1 -j ACCEPT
    -A INPUT -p icmp -j icmp_packets
    -A INPUT -j LOG_DROP

    #Next, we cover the OUTPUT rules, or the rules for all outgoing traffic.
    #Note how at the end we log any outbound packets that are not accepted.
    -A OUTPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 20 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 21 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 22 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 2400 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 23 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 25 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 43 -j ACCEPT
    -A OUTPUT -p udp -m udp --dport 53 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 53 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 80 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 110 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 143 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 443 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 1863 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 993 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 3306 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 18983 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 24601 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 1075 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 2654 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport 1433 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --dport  5123 -j ACCEPT
    -A OUTPUT -d 127.0.0.1 -j ACCEPT
    #allow traffic outbound all ports to 2.2.2.2
    -A OUTPUT -d 2.2.2.2 -j ACCEPT
    -A OUTPUT -p icmp -j icmp_packets
    -A OUTPUT -j LOG_DROP

    #Here we have 2 sets of logging rules. One for dropped packets to log all dropped requests and one for accepted packets, should we wish to log any accepted requesets.
    -A LOG_DROP -j LOG --log-prefix "[IPTABLES DROP] : " --log-tcp-options --log-ip-options
    -A LOG_DROP -j DROP

    -A LOG_ACCEPT -j LOG --log-prefix "[IPTABLES ACCEPT] : " --log-tcp-options --log-ip-options
    -A LOG_ACCEPT -j ACCEPT

    #And finally, a rule to deal with ICMP requests. We drop all ping requests except from our own server.
    # Make sure you replace 1.2.3.4 with the IP address of your server.
    -A icmp_packets -p icmp -m icmp --icmp-type 0 -j ACCEPT
    -A icmp_packets -s 1.2.3.4 -p icmp -m icmp --icmp-type 8 -j ACCEPT
    -A icmp_packets -p icmp -m icmp --icmp-type 8 -j DROP
    -A icmp_packets -p icmp -m icmp --icmp-type 3 -j ACCEPT
    -A icmp_packets -p icmp -m icmp --icmp-type 11 -j ACCEPT
    COMMIT

To apply the FW rules:

    iptables-restore <iptabless-script>

[Category:Linux](Category:Linux "wikilink")
