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

## Reduce database size

```sql
-- Shrink database to target percentage (if possible)
DBCC SHRINKDATABASE (DatabaseName, 10)
-- Shrink file to target size (do not work with not empty files...)
DBCC SHRINKFILE (db_file_name, 10);
```
