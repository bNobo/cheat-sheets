# Kusto cheat sheet

## summarize by bin

```kusto
requests 
| where name startswith "OPTIONS" and resultCode == 404
| summarize count() by bin(timestamp, 1d), name
| order by timestamp asc
```

## join requests with traces

```kusto
requests 
| where name startswith "OPTIONS" and resultCode == 404
| project operation_Id, timestamp, name, url
| join kind=leftouter (traces | project operation_Id, operation_Name, message) on operation_Id
| order by timestamp desc
```
