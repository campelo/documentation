```
MicrosoftHealthcareApisAuditLogs
| where ResultType !contains "Started" //and FhirResourceType == "ServiceRequest" 
//and (OperationName == "Microsoft.HealthcareApis/services/fhir-R4/update" 
//    or OperationName == "Microsoft.HealthcareApis/services/fhir-R4/create")
| extend Hour = bin(TimeGenerated, 10m)
| where Hour >= ago(1000m)
| summarize 
    Count = count(), 
    MaxProcessingDurationUnder10s = maxif(tolong(Properties["processingDurationMs"]), tolong(Properties["processingDurationMs"]) <= 10000),
    CountOver1Sec = countif(tolong(Properties["processingDurationMs"]) > 1000),
    MaxProcessingDuration = max(tolong(Properties["processingDurationMs"])),
    AvgProcessingDuration = avg(tolong(Properties["processingDurationMs"])),
    MedianProcessingDuration = percentiles(tolong(Properties["processingDurationMs"]), 50)
    by Hour
| order by Hour desc, Count desc
```

```
MicrosoftHealthcareApisAuditLogs
| where ResultType !contains "Started" //and FhirResourceType == "ServiceRequest" 
and OperationName == "Microsoft.HealthcareApis/services/fhir-R4/read" 
| extend Hour = bin(TimeGenerated, 1h)
| where Hour >= ago(12h)
| summarize 
    Count = count(), 
    MaxProcessingDurationUnder50s = maxif(tolong(Properties["processingDurationMs"]), tolong(Properties["processingDurationMs"]) <= 50000),
    CountOver1Sec = countif(tolong(Properties["processingDurationMs"]) > 1000),
    MaxProcessingDuration = max(tolong(Properties["processingDurationMs"])),
    AvgProcessingDuration = avg(tolong(Properties["processingDurationMs"])),
    MedianProcessingDuration = percentiles(tolong(Properties["processingDurationMs"]), 50)
    by Hour, RequestUri
| summarize 
    Count = sum(Count),
    MaxRequestUri = arg_max(Count, RequestUri),
    MaxProcessingDurationUnder50s = max(MaxProcessingDurationUnder50s),
    CountOver1Sec = sum(CountOver1Sec),
    MaxProcessingDuration = max(MaxProcessingDuration),
    AvgProcessingDuration = avg(AvgProcessingDuration),
    MedianProcessingDuration = avg(MedianProcessingDuration)
    by Hour
| order by Hour desc, Count desc
```