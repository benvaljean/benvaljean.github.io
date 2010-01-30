---
layout: post 
title: Linux System Troubleshooting
---

This page shows various commands to ascertain how a Linux system is performing and why it may be running slowly if there are other problems.
==vmstat==
Details that amount pages-in and pages-out every x seconds among other information. See [[Swap / Virtual memory#Vmstat|Vmstat]].
==Top==
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

[[Category:Linux]]
