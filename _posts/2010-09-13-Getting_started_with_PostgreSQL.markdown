---
layout: post 
title: Getting started with PostgreSQL
---

### Installation Debian / Ubuntu

    sudo apt-get install postgresql

### Installation RHEL / CentOS / Fedora

    yum install postgresql postgresql-server
    chkconfig postgresql on
    service postgresql start

### Initial Setup

Connect to the template1 DB using the postgres user:

    sudo -u postgres psql template1

Set a pass for the \'postgres\' user. Users in postgres are called
\'roles\':

    alter user postgres with password 'passhere';
    \\q

Create DB:

    sudo -u postgres createdb dbnamehere

Re-enter the psql terminal:

    sudo -u postgres psql dbnamehere

Create a user and give it full permissions to the DB:

    create user with login username with password 'passhere';
    GRANT ALL PRIVILEGES ON DATABASE dbnamehere to username;

By default the psql terminal uses your shell username for the user, in
which case the following command can be used to connect to your new DB:

    psql dbnamehere

### Allow remote connections

Add/uncomment the following line in your *postgresql.conf* file. Located
as */var/lib/pgsql/data/postgresql.conf* or
*/etc/postgresql/8.1/main/postgresql.conf* in most packages.

    listen_addresses = '*'
    port = 5432

Edit your *pg\_hba.conf* to allow remote connections from this user.
Located as */var/lib/pgsql/data/pg\_hba.conf* or
*/etc/postgresql/8.1/main/pg\_hba.conf*. Add the following line,
replacing the network range with your network:

    host   dbnamehere   username  10.0.0.0/24

Restart server to apply changes: Debian / Ubuntu:
`sudo /etc/init.d/postgresql restart` RHEL / CentOS /
Fedora:`sudo service postgresql restart`

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
