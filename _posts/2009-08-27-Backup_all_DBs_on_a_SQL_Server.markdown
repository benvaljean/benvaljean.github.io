---
layout: post 
title: Backup all DBs on a SQL Server
---

This T-SQL script uses a SQL cursor to generate and execute a
`backup database` line for every DB apart from the system DBs. Ammend
`c:\\db backup\\` to match your intended backup destination.

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
        declare @DBFileName varchar(256)    
        set @DBFileName = datename(dw, getdate()) + ' - ' + 
                           replace(replace(@DBName,':','_'),'\\','_')

        exec ('BACKUP DATABASE [' + @DBName + '] TO  DISK = N''c:\\db backup\\' + 
            @DBFileName + ''' WITH NOFORMAT, INIT,  NAME = N''' + 
            @DBName + '-Full Database Backup'', SKIP, NOREWIND, NOUNLOAD,  STATS = 100')

        FETCH NEXT FROM DATABASES_CURSOR INTO @DBName
    END

    CLOSE DATABASES_CURSOR
    DEALLOCATE DATABASES_CURSOR

### Backup all databases and Transaction Logs

The T-SQL scrpt below generates three lines for each non-system DB to
set recovery to full - use Tlogs and backup the DB and Tlog.

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
        declare @DBFileName varchar(256)    
        set @DBFileName = replace(replace(@DBName,':','_'),'\\','_')

        exec ('alter database [' + @DBName + '] set recovery full')
        exec ('BACKUP DATABASE [' + @DBName + '] TO  DISK = N''\\\\server\\share\\' + 
            @DBFileName + '.bak''')
        exec ('BACKUP LOG [' + @DBName + '] TO  DISK = N''\\\\server\\share\\' + 
            @DBFileName + '.log''')
        

        FETCH NEXT FROM DATABASES_CURSOR INTO @DBName
    END

    CLOSE DATABASES_CURSOR
    DEALLOCATE DATABASES_CURSOR

Adapted from
<http://www.geekzilla.co.uk/View487F82A5-C96B-4660-A070-F7C8B7FC4431.htm>

[Category:MSSQL](Category:MSSQL "wikilink")
