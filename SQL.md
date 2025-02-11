# SQL Cheat sheet

## Hash a password and convert it to base64

```sql
declare @password varchar(50) = 'P@ssw0rd'

set @hb = hashbytes('SHA2_512', @password);
set @h64 = cast(N'' as xml).value('xs:base64Binary(sql:variable("@hb"))', 'varchar(128)');

select @hb, @h64
```

## View backup file information

```sql
-- View database metadata
RESTORE HEADERONLY from disk='D:\Backups\database.bak'
-- View database file list
RESTORE FILELISTONLY from disk='D:\Backups\AR24_sprint75.bak'
```

## View database size

```sql
exec sp_spaceused
```

## Reduce database size

```sql
-- Shrink database to target percentage (if possible)
DBCC SHRINKDATABASE (DatabaseName, 10)
-- Shrink file to target size (do not work with not empty files...)
DBCC SHRINKFILE (db_file_name, 10);
```
## Filter sp_who2 results

```sql
declare @sp_who2 TABLE
(SPID INT, 
Status VARCHAR(1000) NULL, 
Login SYSNAME NULL, 
HostName SYSNAME NULL, 
BlkBy SYSNAME NULL, 
DBName SYSNAME NULL, 
Command VARCHAR(1000) NULL, 
CPUTime INT NULL, 
DiskIO INT NULL, 
LastBatch VARCHAR(1000) NULL, 
ProgramName VARCHAR(1000) NULL, 
SPID2 INT,
REQUESTID INT);

INSERT INTO @sp_who2
EXEC sp_who2;

select * from @sp_who2 where DBName = 'Grants';
```

## Create or update a password

```sql
create login <name> with password=N'<password>'
alter login <name> with password=N'<password>'
```

## List logins and users

```sql
select * from sys.sql_logins
select * from sys.database_principals
```

## Firewall rules

```sql
select * from sys.firewall_rules
select * from sys.database_firewall_rules
exec sp_set_firewall_rule N'<name>', '<start_ip>', '<end_ip>'
```

## Give a server role to a user

```sql
exec sp_addsrvrolemember 'domain\username', 'server_role_name'
```

