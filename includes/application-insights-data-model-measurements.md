自訂度量的集合。 使用此集合 tooreport，名為 hello 遙測項目相關聯的度量。 一般使用案例如下：
- 相依性遙測裝載 hello 大小
- hello 佇列處理的項目數由要求遙測
- 時間該客戶花費 toocomplete hello 步驟的精靈步驟完成事件遙測。

您可以在應用程式分析中查詢[自訂度量](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H)︰

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > 自訂的度量是其所屬的 hello 遙測項目相關聯。 它們是主體 toosampling 與包含這些度量的 hello 遙測項目。 tootrack 獨立於其他遙測類型，使用值的度量單位[度量遙測](../articles/application-insights/app-insights-api-custom-events-metrics.md)。

最大金鑰長度︰150
