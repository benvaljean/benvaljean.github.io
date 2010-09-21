---
layout: post 
title: Free up space from deleted files that are still in use (Linux)
---

In Linux a discrepancy between `df` and `du` can occur when a file is
deleted but remains in use by a process. This is because df reports file
system usage and du reports on directory contents - when a file is
deleted it is no longer reported as part of the directory but until the
file is deleted the space is still used by the file system.

Not finished
