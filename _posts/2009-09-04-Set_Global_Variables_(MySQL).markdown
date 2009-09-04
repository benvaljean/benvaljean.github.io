---
layout: post 
title: Set Global Variables (MySQL)
---

Knowledge of global variables principally allows the alteration of
various setings that would otherwise require a restart of mysql.

To list current variables:

    show variables;

To list current variables with \'slow\' anywhere in the name:

    show variables like '%slow%';

To set a global variables, this example to increase
max\_connect\_errors:

    set global max_connect_errors = 20;
    Query OK, 0 rows affected (0.00 sec)

[Category:MySQL](Category:MySQL "wikilink")
