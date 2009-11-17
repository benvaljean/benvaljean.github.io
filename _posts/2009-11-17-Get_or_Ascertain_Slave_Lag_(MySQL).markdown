---
layout: post 
title: Get or Ascertain Slave Lag (MySQL)
---

MySQL master servers can handles queries in parallel whereas a slave
must do them in series as otherwise data integrity would be lost due to
cancelled queries and salve restarts, among other things. Due to the
differences in behaviour there can often be a difference between the
master and a slave - the slave does not have the most up to date data as
it has \'lagged\' behind.

### Get Slave lag

#### Check Slave\'s SQL thread

Run the following mysql command on the slave:

    show slave status;

Look for the `Seconds_Behind_Master` value. This is the different
between the two timestamps of the original query-time currently being
processed by the two servers. It can be easily possible to catch up in
an amount of time less than the value stated, and in rare cases it can
also take longer.

#### Check IO Thread

If the lag is not occurring in the slave\'s SQL thread but in the IO
thread the above check will not reveal it. Sometimes the SQL thread can
catch up to the master but the IO thread can still be lagging behind,
although this is fairly rare.

To check the IO thread lag:

Run the following on the master:

    show master status;

Run the following on the slave:

    show slave status;

Compare the master\'s \"File\" and the slave\'s \"Master\_Log\_File\";
and the master\'s \"Position\" and the slave\'s
\"Read\_Master\_Log\_Pos\".

[Category:MySQL](Category:MySQL "wikilink")
