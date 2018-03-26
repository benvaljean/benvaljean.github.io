---
layout: post 
title: Access denied for root when granting privileges
---

#### Symptom

When attempting to add a grant for all databases for a non-root user the
following error appears:

    mysql> GRANT ALL ON *.* to 'user'@'%';
    ERROR 1045 (28000): Access denied for user 'root'@'%' (using password: YES)

#### Cause

This syntax implies every database/table, inclusing mysql.users and
generally only root can see this.

#### Solution

Presuming that the mysql db is not needed and the user just needs full
access to every databasem without the ability to amend grants the
following should be fine:

    mysql> GRANT ALL ON `%`.* to 'rmt'@'%';

[Category:MySQL](Category:MySQL "wikilink")
