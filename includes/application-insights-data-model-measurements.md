<span data-ttu-id="8b725-101">自訂度量的集合。</span><span class="sxs-lookup"><span data-stu-id="8b725-101">Collection of custom measurements.</span></span> <span data-ttu-id="8b725-102">使用此集合 tooreport，名為 hello 遙測項目相關聯的度量。</span><span class="sxs-lookup"><span data-stu-id="8b725-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="8b725-103">一般使用案例如下：</span><span class="sxs-lookup"><span data-stu-id="8b725-103">Typical use cases are:</span></span>
- <span data-ttu-id="8b725-104">相依性遙測裝載 hello 大小</span><span class="sxs-lookup"><span data-stu-id="8b725-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="8b725-105">hello 佇列處理的項目數由要求遙測</span><span class="sxs-lookup"><span data-stu-id="8b725-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="8b725-106">時間該客戶花費 toocomplete hello 步驟的精靈步驟完成事件遙測。</span><span class="sxs-lookup"><span data-stu-id="8b725-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="8b725-107">您可以在應用程式分析中查詢[自訂度量](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H)︰</span><span class="sxs-lookup"><span data-stu-id="8b725-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="8b725-108">自訂的度量是其所屬的 hello 遙測項目相關聯。</span><span class="sxs-lookup"><span data-stu-id="8b725-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="8b725-109">它們是主體 toosampling 與包含這些度量的 hello 遙測項目。</span><span class="sxs-lookup"><span data-stu-id="8b725-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="8b725-110">tootrack 獨立於其他遙測類型，使用值的度量單位[度量遙測](../articles/application-insights/app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="8b725-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="8b725-111">最大金鑰長度︰150</span><span class="sxs-lookup"><span data-stu-id="8b725-111">Max key length: 150</span></span>
