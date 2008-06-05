---
layout: post 
title: Reset Root password (MySQL)
---

If the root password for a MySQL server is lost, unknown or cannot be
recovered it can be reset so long as you have root (Linux) or
Local/Domain Admin (Windows) access on the MySQL server.

### Procedure

1.  Locate your `my.conf` file - the MySQL configuration file. On Linux
    it is normally `/etc/mysql/my.cnf` and it can be located through
    typing `locate my.cnf` depnding on what distro you have.
2.  Stop the MySQL server: `/etc/init.d/mysql stop`
3.  Edit the `my.cnf` file and place the following line after the
    \[mysqld\] section:
        skip-grant-tables

4.  Start the MySQL server: `/etc/init.d/mysql start`
5.  Now you can connect without a password; all grant commands will not
    work though. Type the following:\
    `$ mysql -u root`\
    `mysql> use mysql;`\
    `mysql> update mysql.user set Password=password('newpassword') where User='root';`\
6.  Stop the MySQL server: `/etc/init.d/mysql stop`
7.  Remove or comment-out the `skip-grant-tables` line.
8.  Start the MySQL server: `/etc/init.d/mysql start`

[Category:MySQL](Category:MySQL "wikilink")
