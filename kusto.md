# Kusto cheat sheet

## summarize by bin

```kusto
requests 
| where name startswith "OPTIONS" and resultCode == 404
| summarize count() by bin(timestamp, 1d), name
| order by timestamp asc
```
