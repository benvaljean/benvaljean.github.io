---
layout: post 
title: Background Writer (bgwriter) (PostgreSQL)
---

Bgwriter (background writer) pushes buffers to disk. Backend processes
handling queries never have to wait for a write to occur as bgwriter
will do it first.

#### Settings

bgwriter\_delay: Specifiys how often bgwrite will run.
brwriter\_lru\_maxpages: Sets the maximum number of buffers that may be
flushed to disk in each run. When a buffer is not flushed due to the
maximum pages value being hit the `maxwritten_clean` value in
`pg_stat_bgwriter` is incremented. bgwriter\_lru\_multiplier: Number of
buffers that can be flushed on-demand due to a new backend process
(query), this value is brwriter\_lru\_maxpages \*
bgwriter\_lru\_multiplier .

##### See Also

-   [Checkpoint](Checkpoint_(PostgreSQL) "wikilink")
-   <http://www.postgresql.org/docs/8.4/static/runtime-config-resource.html>

#### pg\_stat\_bgwriter

In PGSQL 8.4 bgwriter and checkpoint is part of the same process -
checkpoint stats are also here

checkpoints\_timed: CPs that have occured due to checkpoint\_timeout
checkpoints\_req: Flushing of buffers due to checkpoint\_segments and
relatively one-off requirements such as when running a drop database
command. maxwritten\_clean: bgwriter did not run due to
brwriter\_lru\_maxpages buffers\_backend: Flushing of buffers due a new
backend process (query).

A snapshot can be run with `select *,now() from pg_stat_bgwriter;`

##### See Also

<http://www.issociate.de/board/post/504631/Details_about_pg_stat_bgwriter.html>

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
