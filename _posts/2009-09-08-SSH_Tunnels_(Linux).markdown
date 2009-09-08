---
layout: post 
title: SSH Tunnels (Linux)
---

\_\_NOTOC\_\_

### Simpler syntax

    ssh -N localhost -L localport:remotemachine:remoteport -f

#### Example

Setup an SSH tunnel on the localhost and taking connections from port
3335 and forwarding them onto port 3306 on a remote machine db02:

    ssh -N localhost -L 3335:db02:3306 -f

This is fairly simple but not that useful as it will only work within in
a network. If a remote SSH server is used then a SSH tunnel can be used
to allow a connection between over two seperate networks; over a WAN for
example.

### Advanced Syntax

    ssh -pnon-standard-port  -N remotesshserver -L localinterface:localport:remotemachine:remoteport -f

If the remotesshserver does not listen on the standard port of 22 it
must be specificed in `-pnon-standard-port`; otherwise it can be
omitted.

#### Example

Setup SSH tunnel using a remote ssh server perimeterssh01 on where SSH
listens on a custom port 2400, taking connections from port 6000 on a
specific local interface of 127.0.0.2 and forwaring them onto port 6002
on remote server 10.10.8.50 in the remote network of perimeterssh01.

    ssh -p2400 -N perimeterssh01 -L 127.0.0.2:6000:10.10.8.50:6002

### See Also

-   [MS Terminal Services (RDP) using mstsc.exe over SSH
    tunnels](http://www.msfn.org/board/ms-terminal-services-rdp-using-mstsc-exe-over-ssh-tunnels-t128735.html)
-   [X11 forwarding over
    SSH](http://my.brandeis.edu/bboard/q-and-a-fetch-msg?msg_id=0000JK)
-   [Access Your MySQL Server Remotely Over SSH :: the How-To
    Geek](http://www.howtogeek.com/howto/ubuntu/access-your-mysql-server-remotely-over-ssh/)
-   [How-To: SSH tunnels for secure network
    access](http://www.engadget.com/2006/03/21/how-to-ssh-tunnels-for-secure-network-access/)

[Category:Linux](Category:Linux "wikilink")
