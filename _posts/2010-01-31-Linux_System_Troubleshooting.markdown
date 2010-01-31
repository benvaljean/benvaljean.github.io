---
layout: post 
title: Linux System Troubleshooting
---

This page shows various commands to ascertain how a Linux system is performing and why it may be running slowly if there are other problems.
==vmstat==
Details that amount pages-in and pages-out every x seconds among other information. See [[Swap / Virtual memory#Vmstat|Vmstat]].
==top==
Shows continuously-updating information for processes. Processes are sorted in CPU usage descending by default.

Load averages are shown for the last 1, 5 and 15 minutes. Every system is different but as a guide a single CPU system should normally not have a 15 minute load average over 2.

===Interactive commands===
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Command'''
| align="center" style="background:#f0f0f0;"|'''Function'''
|-
| A||Displays 4 windows: <br>Window 1: Sorted by CPU descending. <br>Window 2: Sorted by PID descending - shows newest porcesses. <br>Window 3: Sorted by Memory usage descending. <br>Window 4: Shows your processes.
|-
| Space||Update now
|-
| P||Sort by CPU usage descending
|-
| M||Sort by Memory usage descending
|-
| T||Sort by cumulative time
|-
| f||Show/Hide fields
|-
| o||Change column order
|-
| 
|}
==ps==
To show all processes including their command-lines:
<pre>ps aux</pre>
==free==
To show the current free and in-use physical RAM and swapped with low/high values in MB:
<pre>free -ml</pre>
==iostat==
Iostat gives statistics on I/O and CPU usage. <tt>iostat</tt> without any arguments displays transfers per second since boot as 'tps' although a single logical transfer could be any size and can therefore be misleading. The number of blocks read and written since boot and the blocks read and written per second 'since boot.' <tt>iostat -x</tt> gives more information, but this again is not very useful as it only shows the total since boot.

Iostat is more useful when it is giving repeating output as each output after the first output shows stats 'since the last output' rather than since boot. <tt>iostat 1 5</tt> will give 5 outputs with a 1 second delay. The 2nd - 5th output will look different to the first for this reason.

Get extended IO statistics, updating once per second:<pre>iostat 1 -x</pre>The column that will indicate a bottleneck in the I/O are shown below:
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Column'''
| align="center" style="background:#f0f0f0;"|'''Definition'''
|-
| avgqu-sz||The  average size (in sectors) of the requests that were issued to the device.
|-
| await||The average time spent servicing I/O requests, including the time spent in a queue.
|-
| %util||CPU utilisation of the device when requests were issued.
|-
| 
|}
==tcpdump==
Tcpdump gives detailed verbose network traffic output. Some examples are shown below, which all refer to the interface eth0. Use <tt>ifconfig -a</tt> to find all interfaces.

Show HTTP traffic:
<pre>tcpdump -i eth0 'tcp port 80'</pre>
Show DNS traffic:<pre>tcpdump -i eth1 'udp port 53'</pre>
Show DNS traffic, and HTTP traffic on ports and 80, 81 and 82:
<pre>tcpdump -i eth0 udp port 53 or tcp \\( 80 or 81 or 82 \\)</pre>
Show traffic on port 80 for 1.1.1.1:<pre>
tcpdump -i eth0 dst 10.168.28.22 and tcp port 80</pre>
Show traffic on port 80 for 1.1.1.1 with an increased sniff size of 1024 bytes:
<pre>tcpdump -i eth0 -s 1024 dst 10.168.28.22 and tcp port 80</pre>
===Send output to a pcap file===
The <tt>-w</tt> parameter captures the output to a file that can be viewed later.

Capture SSH traffic for 2.2.2.2 and output to a pcap file named ssh.pcap:
<pre>tcpdump -i eth0 -w ssh.pcap tcp port 22</pre>

This output can then be viewed later:
<pre>tcpdump -ttttnnr ssh.pcap</pre>
===See Also===
*[http://danielmiessler.com/study/tcpdump/ A tcpdump Tutorial / Primer]
*[http://www.alexonlinux.com/tcpdump-for-dummies tcpdump for Dummies]
*[http://www.dslreports.com/faq/tcpdump/5._Some_simple_scripts#8443 Useful tcpdump scripts]
==strace==
If the server for some reason is not logging what you need or there is a need to debug software at system call level, strace can help. Try <tt>strace echo hello</tt>. Strace becomes more useful when it monitors the system calls for a process already running.

Monitor system calls for pid 12345:
<pre>strace -p 12345</pre>


[[Category:Linux]]
