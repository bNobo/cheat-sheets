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

## filter with regex

Find a guid in a path.

```kusto
requests
| where resultCode in (500, 404) and name matches regex @"^GET \/path\/\w{8}-\w{4}-\w{4}-\w{4}-\w{12}$"
| order by timestamp asc
| project timestamp, name, resultCode, application_Version
```

Use ASCII instead of unicode to improve perf.

```kusto
requests
| where resultCode in (500, 404) and name matches regex @"^GET \/forward\/[[:word:]]{8}-[[:word:]]{4}-[[:word:]]{4}-[[:word:]]{4}-[[:word:]]{12}$"
| order by timestamp asc
| project timestamp, name, resultCode, application_Version
```
