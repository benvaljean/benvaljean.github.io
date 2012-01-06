---
layout: post 
title: TCP Connection Termination (Networking)
---

===Normal Connection Termination===

Each side closes the connection independantly by sending a FIN packet and waiting for an ACK, 4 packets are exchanged.
<pre>
-------------- FIN --------------> 
<------------- ACK ---------------
<------------- FIN ---------------
-------------- ACK ------------->
</pre>
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Connection status'''
| align="center" style="background:#f0f0f0;"|'''Description'''
|-
| FIN_WAIT1||Closer wishing to close a connection and has sent a FIN packet but has not yet received and ACK packet back from the closee.
|-
| CLOSE_WAIT||Closee receives FIN packet and send an ACK packet, it must wait for the app using it to be told the end is closing so the app here can finish properly.
|-
| FIN_WAIT2||Closer has now received ACK packet back from the client and is now waiting for the closee\\'s FIN.
|-
| LAST_ACK||The closee\\'s receives notice that the app has finished and it sends its FIN to the closer and is now waiting for the closer\\'s ACK. It is waiting for the \\'last ack\\'.
|-
| TIME_WAIT||Closer receives the FIN packet and sends back an ACK packet. This is the very last packet sent in the TCP closing process. The closer reserves the port for twice the maximum segment lifetime (by default) to ensure no stray packets are receives by another process that might use the same port afterwards.
|-
| CLOSED||Closee receives the ACK packet from the closer.
|-
| CLOSED||Closer reservation of the port expires.
|}

===Simultaneous Close===
Each side closes its connection simultaneously, 4 packets are still exchanged.
<pre>
-------------- FIN -------------->
<------------- FIN ---------------
-------------- ACK ------------->
<------------- ACK ---------------
</pre>
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Connection Status'''
| align="center" style="background:#f0f0f0;"|'''Description'''
|-
| FIN_WAIT1||Closer sends a FIN packet and is waitng for the closee\\'s ACK as normal.
|-
| FIN_WAIT1||The other machine also wishes to end the connection and sends back a FIN simultaneously. TCP close becomes and active close.
|-
| CLOSING||Both machines receives a FIN packet and sends an ACK packet back to each other. They are in this state until they recieve each others respective ACK packet.
|-
| TIME_WAIT||Each machine enters this state once they have recieved the other machines ACK. The port is reserved for twice the maximum segment lifetime (by default) to ensure no stray packets are receives by another process that might use the same port afterwards.
|}

===References===
http://www.tcpipguide.com/free/t_TCPConnectionTermination-2.htm<br>
http://ttcplinux.sourceforge.net/documents/one/tcpstate/tcpstate.html

[[Category:Networking]]
