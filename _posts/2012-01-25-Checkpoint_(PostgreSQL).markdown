---
layout: post 
title: Checkpoint (PostgreSQL)
---

Checkpoint flushes all buffers to disk and deletes xlogs

#### Settings

checkpoint\_timeout: Maximum allowed time since the last checkpoint.
checkpoint\_completion\_target: Target length of the checkpoint. Instead
of using all possible I/O in a short time it is spread across the target
value to avoid high spikes in I/O, the value is
checkpoint\_completion\_target \* checkpoint\_timeout
checkpoint\_segments: When xlogs hit this qty a checkpoint is triggered.

Most CPs should be due to timeout.

#### See Also

-   [Background Writer
    (bgwriter)](Background_Writer_(bgwriter)_(PostgreSQL) "wikilink")
-   <http://www.postgresql.org/docs/8.3/static/wal-configuration.html>
-   <http://www.postgresql.org/docs/8.3/static/runtime-config-wal.html#GUC-CHECKPOINT-TIMEOUT>

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
