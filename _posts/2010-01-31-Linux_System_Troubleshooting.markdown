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
===Ascertain what config files are read on startup===
This is useful for ascertaining why a particular config file is not being read from the location it should be in your experience and where it could be reading it from instead. The <tt>-e</tt> parameter allows the displaying of a particular system call only. 

For example the SQL query tool tsql refused to read its configuration on a monitoring server when it worked fine on another. The command below opens tsql and captured all the open system calls:
<pre>strace -e open tsql -S testconfig -U test -P test</pre>
[[Linux System Troubeshooting:Example strace output|View the output]]
Line 45 shows that it tries to open the /home/exampleusername/.freetds.conf, finds that it does not exist and then line 46 shows the /usr/local/etc/freetds.conf file being read. The file that I had been editing was /etc/freetds.conf .

This can be expanded to see whether or not a programme has access to a file by viewing the access system call too for a particular filename:
<pre>strace -e open,access executable | grep filename.conf</pre>
===Ascertain what a process is doing===
If a particular process is using a lot of CPU or I/O log files along may give no information as to what is causing the problem. The <tt>-p</tt>parameter described above achieve this.
===Ascertain what system calls are being used the most===
Statistics on what system calls are being used can be shown with the <tt>-c</tt> parameter. This can more easily show why a process is using high CPU or I/O by showing which system calls are being used the most.

Show systems calls by the <tt>ls /</tt> command<pre>[user@host /]$ strace -c ls /usr >/dev/null
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 55.00    0.000055           3        17           read
 45.00    0.000045           2        19           fstat64
  0.00    0.000000           0         1           write
  0.00    0.000000           0        19           open
  0.00    0.000000           0        25           close
  0.00    0.000000           0         1           execve
  0.00    0.000000           0         2         1 access
  0.00    0.000000           0         3           brk
  0.00    0.000000           0         3         3 ioctl
  0.00    0.000000           0         8           munmap
  0.00    0.000000           0         1           uname
  0.00    0.000000           0         6           mprotect
  0.00    0.000000           0         2           readv
  0.00    0.000000           0         2           rt_sigaction
  0.00    0.000000           0         1           rt_sigprocmask
  0.00    0.000000           0         1           getrlimit
  0.00    0.000000           0        33           mmap2
  0.00    0.000000           0         1           stat64
  0.00    0.000000           0         2           getdents64
  0.00    0.000000           0        13           fcntl64
  0.00    0.000000           0         1           futex
  0.00    0.000000           0         1           set_thread_area
  0.00    0.000000           0         1           set_tid_address
  0.00    0.000000           0         1           set_robust_list
  0.00    0.000000           0         5           socket
  0.00    0.000000           0         5         4 connect
  0.00    0.000000           0         1           sendmsg
------ ----------- ----------- --------- --------- ----------------
100.00    0.000100                   175         8 total
</pre>
Instead of capturing statistics in an end-to-end manner a snapshot can be taken strace attaching itself to a currently running process, until Ctrl+C is used. The example below captures statistics for [[Nagios]]:<pre>
[user@host /]$ ps aux|grep nagios
nagios    1071  0.0  0.3  12988  1616 ?        Ssl   2009  57:35 /usr/local/nagios/bin/nagios -d /usr/local/nagios/etc/nagios.cfg
benyg    28856  0.0  0.1   3912   672 pts/6    R+   15:50   0:00 grep nagios
[user@host /]$ sudo strace -c -p 1071
Password:
Process 1071 attached - interrupt to quit
Process 1071 detached
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 51.61    0.000048          48         1           waitpid
 48.39    0.000045           1        46           gettimeofday
  0.00    0.000000           0         1           restart_syscall
  0.00    0.000000           0        12           write
  0.00    0.000000           0         3           open
  0.00    0.000000           0         3           close
  0.00    0.000000           0        77           time
  0.00    0.000000           0         1           rename
  0.00    0.000000           0         2           umask
  0.00    0.000000           0         2           munmap
  0.00    0.000000           0         1           fchmod
  0.00    0.000000           0         1         1 fsync
  0.00    0.000000           0         1           clone
  0.00    0.000000           0         2           _llseek
  0.00    0.000000           0         2           getdents
  0.00    0.000000           0        32           nanosleep
  0.00    0.000000           0         2           mmap2
  0.00    0.000000           0         1           stat64
  0.00    0.000000           0         3           fstat64
  0.00    0.000000           0         3           fcntl64
------ ----------- ----------- --------- --------- ----------------
100.00    0.000093                   196         1 total
</pre>
This shows that in the 5 seconds whilst strace was running Nagios spent most of its time waiting, followed by getting the time of day.

[[Category:Linux]]
