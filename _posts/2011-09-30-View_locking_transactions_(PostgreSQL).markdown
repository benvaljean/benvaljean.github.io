---
layout: post 
title: View locking transactions (PostgreSQL)
---

    SELECT pg_class.relname, pg_locks.transactionid, pg_locks.mode, pg_locks.granted as "g",
    substr(pg_stat_activity.current_query,1,30), pg_stat_activity.query_start,
    age(now(),pg_stat_activity.query_start) as "age", pg_stat_activity.procpid
    FROM pg_stat_activity,pg_locks
    left outer join pg_class on
    (pg_locks.relation = pg_class.oid)
    WHERE pg_locks.pid=pg_stat_activity.procpid;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
