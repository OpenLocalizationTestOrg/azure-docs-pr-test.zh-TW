---
title: "Application Insights 遙測相互關聯 | Microsoft Docs"
description: "Application Insights 遙測相互關聯"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: mbullwin
ms.openlocfilehash: e821a640d3d75e712c022bd681eb07b83da91911
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Application Insights 中的遙測相互關聯

在微服務的世界裡，每個邏輯作業都需要在服務的各種元件中完成工作。 每個元件都可分別使用 [Application Insights](app-insights-overview.md) 監視。 Web 應用程式元件會與驗證提供者元件進行通訊以驗證使用者認證，並透過 API 元件取得視覺效果的資料。 API 元件本身可以查詢其他服務中的資料，並使用快取提供者元件及向計費元件通知這個呼叫。 Application Insights 支援分散式遙測相互關聯。 它可讓您偵測造成失敗或效能衰退的元件。

本文說明 Application Insights 所使用的資料模型，以關聯多個元件所傳送的遙測。 它涵蓋內容傳播技巧和通訊協定。 它還包括實作不同語言和平台上的相互關聯概念。

## <a name="telemetry-correlation-data-model"></a>遙測相互關聯資料模型

Application Insights 會定義分散遙測相互關聯的[資料模型](application-insights-data-model.md)。 為了將遙測與邏輯作業相關聯，每個遙測項目都有稱為 `operation_Id` 的內容欄位。 每個遙測項目會在分散式追蹤內共用這個識別碼。 因此即使單一層中遺失遙測，您仍然可以將其他元件所報告的遙測相關聯。

分散式邏輯作業通常包含一組較小的作業 - 要求由其中一個元件處理。 這些作業是由[要求遙測](application-insights-data-model-request-telemetry.md)所定義。 每個要求遙測都有它自己的 `id`，可供全域唯一識別。 與這個要求關聯的所有遙測 - 追蹤、例外狀況等都應該將 `operation_parentId` 設定為 `id` 的要求值。

每個外寄的作業 (例如 http) 都會呼叫由[相依性遙測](application-insights-data-model-dependency-telemetry.md)所代表的另一個元件。 相依性遙測也會定義它自己的全域唯一 `id`。 由這個相依性呼叫啟動的要求遙測會使用它作為 `operation_parentId`。

您可以將 `operation_Id`、`operation_parentId` 和 `request.id` 與 `dependency.id` 搭配使用，建置分散式邏輯作業的檢視。 這些欄位也會定義遙測呼叫的因果順序。

在微服務環境中，來自元件的追蹤可能會移至不同的儲存體。 每個元件可能會在 Application Insights 中擁有自己的檢測金鑰。 若要取得邏輯作業的遙測，您需要查詢每個儲存體中的資料。 當儲存體的數目很龐大時，您需要接下來要在何處尋找的相關提示。

Application Insights 資料模型會定義兩個欄位來解決這個問題：`request.source` 和 `dependency.target`。 第一個欄位會識別起始相依性要求的元件，而第二個欄位會識別傳回相依性呼叫回應的元件。


## <a name="example"></a>範例

讓我們以 STOCK PRICES 這個應用程式為例，它會使用稱為 STOCKS API 的外部 API 來顯示目前股票的市場價格。 STOCK PRICES 應用程式的 `Stock page` 頁面，是由用戶端網頁瀏覽器使用 `GET /Home/Stock` 所開啟。 應用程式會使用 HTTP 呼叫 `GET /api/stock/value` 來查詢 STOCK API。

您可以分析執行查詢的結果遙測︰

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

在結果檢視中，請注意所有遙測項目都會共用根目錄 `operation_Id`。 從此頁面發出 AJAX 呼叫時 - 會將新的唯一識別碼 `qJSXU` 指派給相依性遙測，並使用 pageView 的識別碼作為 `operation_ParentId`。 伺服器要求接著會使用 AJAX 的識別碼作為 `operation_ParentId` 等等。

| itemType   | 名稱                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock 頁面                |              | STYz               | STYz         |
| 相依性 | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| 要求    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| 相依性 | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

現在，當您向外部服務發出呼叫 `GET /api/stock/value` 時，您想要知道該伺服器的身分識別。 所以您可以適當地設定 `dependency.target` 欄位。 當外部服務不支援監視時 - `target` 會設定為服務的主機名稱，例如 `stock-prices-api.com`。 不過，如果該服務是透過傳回預先定義的 HTTP 標頭來識別其本身 - `target` 包含的服務識別可讓 Application Insights 透過查詢該服務的遙測來建置分散式追蹤。 

## <a name="correlation-headers"></a>相互關聯標頭

我們正在進行[相互關聯 HTTP 通訊協定](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md)的 RFC 提案。 此提案會定義兩個標頭︰

- `Request-Id` 包含呼叫的全域唯一識別碼
- `Correlation-Context` - 包含分散式追蹤屬性的名稱值組集合

標準也定義了 `Request-Id` 產生的兩個結構描述 - 平面及階層。 利用一般的結構描述，會針對 `Correlation-Context` 集合定義已知的 `Id` 金鑰。

Application Insights 會定義相互關聯 HTTP 通訊協定的[延伸](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md)。 它會使用 `Request-Context` 名稱值組，來傳播立即呼叫端或被呼叫端所使用的屬性集合。 Application Insights SDK 會使用此標頭來設定 `dependency.target` 和 `request.source` 欄位。

## <a name="open-tracing-and-application-insights"></a>Open Tracing 與 Application Insights

[Open Tracing](http://opentracing.io/) 和 Application Insights 的資料模型外觀 

- `request`、`pageView` 會使用 `span.kind = server` 對應至**範圍**
- `dependency` 會使用 `span.kind = client` 對應至**範圍**
- `request` 和 `dependency` 的 `id` 會對應至 **Span.Id**
- `operation_Id` 會對應至 **TraceId**
- `operation_ParentId` 會對應至 `ChildOf` 類型的**參考**

如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。

如需 Open Tracing 概念的定義，請參閱[規格](https://github.com/opentracing/specification/blob/master/specification.md)和 [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md)。


## <a name="telemetry-correlation-in-net"></a>.NET 中的遙測相互關聯

經過一段時間，.NET 定義了數種相互關聯遙測和診斷記錄的方式。 `System.Diagnostics.CorrelationManager` 讓您可以追蹤 [LogicalOperationStack 和 ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx)。 `System.Diagnostics.Tracing.EventSource` 與 Windows ETW 會定義 [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx) 方法。 `ILogger` 會使用[記錄範圍](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes)。 WCF 與 Http 連接「目前」的內容傳播。

不過這些方法不會啟用自動分散式追蹤支援。 `DiagnosticsSource` 是能夠支援自動跨電腦相互關聯的方法。 .NET 程式庫支援 Diagnostics Source，並允許透過如 http 的傳輸自動跨電腦傳播相互關聯內容。

Diagnostics Source 中的[活動指南](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)會說明追蹤活動的基本概念。 

ASP.NET Core 2.0 支援擷取 Http 標頭和啟動新的活動。 

`System.Net.HttpClient` 起始版本 `<fill in>` 支援自動插入相互關聯 Http 標頭及追蹤 http 呼叫作為 Activity。

ASP.NET Classic 有新的 Http 模組 [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/)。 此模組會使用 DiagnosticsSource 來實作遙測相互關聯。 它會根據傳入的要求標頭來啟動活動。 還會將不同要求處理階段的遙測相互關聯。 即使是當 IIS 處理的每個階段在不同管理執行緒上執行時也一樣。

Application Insights SDK 起始版本 `2.4.0-beta1` 會使用 DiagnosticsSource 和 Activity 來收集遙測，並將它與目前活動產生關聯。 

## <a name="next-steps"></a>後續步驟

- [撰寫自訂遙測](app-insights-api-custom-events-metrics.md)
- 在 Application Insights 上將微服務的所有元件上架。 查看[支援的平台](app-insights-platforms.md)。
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 了解如何[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。
