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

      115  lsof -n|grep deleted
      116  lsof -n
      117  ps aux|grep pams
      118  cd /proc/31131
      119  ls
      120  cd fd
      121  ls
      122  ls -l
      123  tail -f 7
      124  echo hello >7
      125  tail -f 7
      126  df -h
      127  sync
      128  df -h
      129  kill -USR1 31131
      130  sync
      131  df -h
