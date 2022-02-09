# SQL Cheat sheet

## Hash a password and convert it to base64

```sql
declare @password varchar(50) = 'P@ssw0rd'

set @hb = hashbytes('SHA2_512', @password);
set @h64 = cast(N'' as xml).value('xs:base64Binary(sql:variable("@hb"))', 'varchar(128)');

select @hb, @h64
```
