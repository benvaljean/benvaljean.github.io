---
layout: post 
title: Access rights/Privileges/Grants (MySQL)
---

The `GRANTS` part in MySQL is where the access rights/privileges as to
what actions the MySQL users can perform. For inatance a MySQL user may
only be able to read certain databases or indeed it may be required to
create a user that can read all databases.

### View the current users/grants

Login to MySQL by typing `mysql -u root -p` at the command prompt. If
this is a new installation or have previously been able to login as root
without a password just press enter. Ensure you set a root password.
Type `select User,Host from mysql.user;` to get a list of all the
current users the host they can connect from using this account. To get
more information type `select * from mysql.user;` instead.

To view information on the specific grants for a particular user type:
`SHOW GRANTS FOR user@host;`

For example to see the grants/access rights for root type:

    mysql> show grants for root@localhost;
    +----------------------------------------------------------------------------------------------------------------------------------------+
    | Grants for root@localhost                                                                                                              |
    +----------------------------------------------------------------------------------------------------------------------------------------+
    | GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY PASSWORD '*HASHOFPASSWORDHERE' WITH GRANT OPTION |
    +----------------------------------------------------------------------------------------------------------------------------------------+
    1 row in set (0.00 sec)

### Creating users and giving access to databases

To create a new user with complete access to all databases for testing
purposes:

    mysql> GRANT ALL PRIVILEGES ON *.* TO 'yourusername'@'localhost' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;

To create a new user with complete access to a database called
\'maroon1\':

    mysql> GRANT ALL PRIVILEGES ON maroon1.* TO 'yourusername'@'localhost' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;

To specifify access to specific tables specificy the table name after
the full-stop following the database name in the form of
`databasename.tablename` To create a user with standard read/write
access to a database called \'maroon2\':

    mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON maroon2.* TO 'yourusername'@'localhost' IDENTIFIED BY 'yourpassword';

### Deleting accounts

<font color=red>Be careful!</font> To delete a user called rabbit who is
connecting from localhost:

    DELETE FROM mysql.user WHERE User='rabbit' and host='localhost';

### Removing/Revoking access to a database/table

The bottom line here is that the syntax is exactly the same except
`GRANT` is replaced with `REVOKE` for nearly all situations.

### Setting a root password

Login to MySQL as root and enter the followng:

    SET PASSWORD for root@localhost=PASSWORD('yourpasswordhere');
