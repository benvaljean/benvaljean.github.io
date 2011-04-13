---
layout: post 
title: Swap / Virtual memory
---

### Paging versus Swapping

Paging refers to writing portions, termed pages, of a process\' memory
to disk. Swapping, strictly speaking, refers to writing the entire
process, not just part, to disk. In Linux, true swapping is exceedingly
rare, but the terms paging and swapping often are used interchangeably.

### Paging

When pages are written to disk, the event is called a page-out, and when
pages are returned to physical memory, the event is called a page-in.
Page-ins are common, normal and are not a cause for concern. For
example, when an application first starts up, its executable image and
data are paged-in. This is normal behavior. Page-outs, however, can be a
sign of trouble. When the kernel detects that memory is running low, it
attempts to free up memory by paging out. Though this may happen briefly
from time to time, if page-outs are plentiful and constant, the kernel
can reach a point where it\'s actually spending more time managing
paging activity than running the applications, and system performance
suffers. This woeful state is referred to as thrashing. Using swap space
is not inherently bad. Rather, it\'s intense paging activity that\'s
problematic.

#### Page fault

A page fault occurs when the kernel needs a page, finds it doesn\'t
exist in physical memory because it has been paged-out, and re-reads it
in from disk.

### Vmstat

Vmstat allows monitoring of page-ins and page-outs on Linux. Page-outs
are under the `so` column and page-ins are under the `si` column.

    Vmstat <delay in seconds> <count>

For a 5 second dealy between each output 10 times: `vmstat 5 10`.
Running vmstat with no count runs indefinitely.

-   swpd: The amount of the page file in use
-   free: Memory not in use, same figure that the `free` command gives.
-   buff: Memory used as buffer. When data is used Linux may keep some
    of it in memory as a \'virtual disk\'. Similar to pre-caching in
    Windows, if GIMP is loaded, closed and restarted it will open faster
    the second time if Linux has placed it in the buffer.
-   cache: Memory used as disk-cache. Data that is instended to go to
    disk is placed here to speed up processes, so that they do nto have
    to wait for I/O. data that is re-read can also be retrieved from
    here.
-   si: Data that is swapped in from disk to memory.
-   so: Data that is swapped out from memory to disk - this can indicate
    a system that is eating up its RAM.

[Category:Linux](Category:Linux "wikilink")
