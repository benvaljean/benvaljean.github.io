---
layout: post 
title: Create Database T-SQL script
---

The script below aids the process of migrating multiple databases from
one MSSQL server to another. The cursor will cycle throgh all DBs
excluding the system databases and print out a \'CREATE DATABASE
\[dbname\]\' line for each one. This can then be ran on the destination
server.

    DECLARE @DBName varchar(255)

    DECLARE @DATABASES_Fetch int

    DECLARE DATABASES_CURSOR CURSOR FOR
        select
            DATABASE_NAME   = db_name(s_mf.database_id)
        from
            sys.master_files s_mf
        where
           -- ONLINE
            s_mf.state = 0 

           -- Only look at databases to which we have access
        and has_dbaccess(db_name(s_mf.database_id)) = 1 

            -- Not master, tempdb or model
        and db_name(s_mf.database_id) not in ('Master','tempdb','model')
        group by s_mf.database_id
        order by 1

    OPEN DATABASES_CURSOR

    FETCH NEXT FROM DATABASES_CURSOR INTO @DBName

    WHILE @@FETCH_STATUS = 0
    BEGIN
      

        print ('create DATABASE [' + @DBName + ']')

        FETCH NEXT FROM DATABASES_CURSOR INTO @DBName
    END

    CLOSE DATABASES_CURSOR
    DEALLOCATE DATABASES_CURSOR

[Category: MSSQL](Category:_MSSQL "wikilink")
