---
title: "應用程式 Insights 遙測相互關聯 aaaAzure |Microsoft 文件"
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
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Application Insights 中的遙測相互關聯

Hello world 的微服務，在每個邏輯作業都需要 hello 服務的各種元件在執行工作。 每個元件都可分別使用 [Application Insights](app-insights-overview.md) 監視。 hello web 應用程式元件會與驗證提供者元件 toovalidate 使用者認證，以及與 hello API 元件 tooget 資料視覺效果。 輪中的 hello API 元件可以查詢資料與其他服務和使用快取提供者元件，並通知 hello 計費的元件，關於此呼叫。 Application Insights 支援分散式遙測相互關聯。 它可讓您 toodetect 哪些元件會負責失敗或效能降低。

本文說明多個元件所傳送的 hello toocorrelate 的 Application Insights 遙測所使用的資料模型。 它涵蓋了 hello 內容傳播技術及通訊協定。 其中也涵蓋 hello hello 相互關聯概念，在不同的語言與平台上實作。

## <a name="telemetry-correlation-data-model"></a>遙測相互關聯資料模型

Application Insights 會定義分散遙測相互關聯的[資料模型](application-insights-data-model.md)。 與 hello 邏輯作業 tooassociate 遙測，每個遙測項目具有名為的內容欄位`operation_Id`。 每個遙測項目共用這個識別碼 hello 分散式追蹤中。 因此即使單一層中遺失遙測，您仍然可以將其他元件所報告的遙測相關聯。

分散式的邏輯作業通常包含一組較小的作業-其中 hello 元件處理要求。 這些作業是由[要求遙測](application-insights-data-model-request-telemetry.md)所定義。 每個要求遙測都有它自己的 `id`，可供全域唯一識別。 所有遙測-追蹤、 例外狀況、 與此要求相關聯的等應該設定 hello `operation_parentId` hello 要求 toohello 值`id`。

每個外寄的作業，例如所表示的 http 呼叫 tooanother 元件[相依性遙測](application-insights-data-model-dependency-telemetry.md)。 相依性遙測也會定義它自己的全域唯一 `id`。 由這個相依性呼叫啟動的要求遙測會使用它作為 `operation_parentId`。

您可以建立使用分散式的邏輯作業的 hello 檢視`operation_Id`， `operation_parentId`，和`request.id`與`dependency.id`。 這些欄位也會定義遙測呼叫 hello 因果順序。

在微服務環境中，從元件的追蹤可能會 toohello 不同儲存體。 每個元件可能會在 Application Insights 中擁有自己的檢測金鑰。 tooget 遙測 hello 邏輯作業，您需要從每個儲存體的 tooquery 資料。 龐大的儲存體的數目時，您需要在何處 toohave 提示 toolook 下一步。

Application Insights 資料模型會定義兩個欄位 toosolve 這個問題：`request.source`和`dependency.target`。 hello 第一個欄位會識別 hello 元件起始 hello 相依性要求，並 hello 第二個識別傳回 hello 回應 hello 相依性呼叫的哪一個元件。


## <a name="example"></a>範例

讓我們顯示 hello 目前市場股票價格使用 hello 外部 API 呼叫的股票 API 應用程式股票價格的範例。 hello 股票價格應用程式有一個頁面`Stock page`hello 用戶端 web 瀏覽器使用來開啟`GET /Home/Stock`。 hello 應用程式查詢所使用的 HTTP 呼叫 hello 股票 API `GET /api/stock/value`。

您可以分析執行查詢的結果遙測︰

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

遙測的所有項目共用 hello 根目錄 hello 結果檢視便箋中`operation_Id`。 當 ajax 呼叫源自 hello 頁面-新的唯一識別碼`qJSXU`是指派的 toohello 相依性遙測，pageView 的識別碼用做`operation_ParentId`。 伺服器要求接著會使用 AJAX 的識別碼作為 `operation_ParentId` 等等。

| itemType   | 名稱                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock 頁面                |              | STYz               | STYz         |
| 相依性 | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| 要求    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| 相依性 | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

現在當 hello 呼叫`GET /api/stock/value`進行 tooan 外部服務想 tooknow hello 識別該伺服器。 所以您可以適當地設定 `dependency.target` 欄位。 當 hello 外部服務不支援監視- `target` toohello hello 服務，例如主機名稱設定`stock-prices-api.com`。 不過如果該服務會將自己識別藉由傳回預先定義的 HTTP 標頭-`target`包含藉由 Application Insights toobuild 分散式追蹤查詢遙測從該服務的 hello 服務身分識別。 

## <a name="correlation-headers"></a>相互關聯標頭

我們正努力在 hello 的 RFC 提案[HTTP 通訊協定的相互關聯](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md)。 此提案會定義兩個標頭︰

- `Request-Id`執行 hello 呼叫 hello 全域唯一識別碼
- `Correlation-Context`-執行 hello 名稱值配對集合 hello 分散式追蹤屬性

hello 標準也會定義兩個結構描述的`Request-Id`產生-平面及階層。 Hello 一般結構描述沒有已知`Id`hello 定義索引鍵`Correlation-Context`集合。

Application Insights 定義 hello[延伸](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md)hello 相互關聯的 HTTP 通訊協定。 它會使用`Request-Context`名稱值組 toopropagate hello hello 立即呼叫端或被呼叫端所使用的屬性集合。 Application Insights SDK 會使用此標頭 tooset`dependency.target`和`request.source`欄位。

## <a name="open-tracing-and-application-insights"></a>Open Tracing 與 Application Insights

[Open Tracing](http://opentracing.io/) 和 Application Insights 的資料模型外觀 

- `request``pageView`太對應**範圍**與`span.kind = server`
- `dependency`對應太**範圍**與`span.kind = client`
- `id``request`和`dependency`太對應**Span.Id**
- `operation_Id`對應太**TraceId**
- `operation_ParentId`對應太**參考**的型別`ChileOf`

如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。

如需 Open Tracing 概念的定義，請參閱[規格](https://github.com/opentracing/specification/blob/master/specification.md)和 [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md)。


## <a name="telemetry-correlation-in-net"></a>.NET 中的遙測相互關聯

經過一段時間.NET 定義數種方式 toocorrelate 遙測和診斷記錄檔。 沒有`System.Diagnostics.CorrelationManager`允許 tootrack [LogicalOperationStack 和 ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx)。 `System.Diagnostics.Tracing.EventSource`與 Windows ETW 定義 hello 方法[SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx)。 `ILogger` 會使用[記錄範圍](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes)。 WCF 與 Http 連接「目前」的內容傳播。

不過這些方法不會啟用自動分散式追蹤支援。 `DiagnosticsSource`是方式 toosupport 自動執行跨機器相互關聯。 .NET 程式庫支援診斷來源，並允許透過 hello 傳輸，例如 http hello 相互關聯內容自動跨機器傳播。

hello[引導 tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)診斷來源中說明的追蹤活動的 hello 基本概念。 

ASP.NET Core 2.0 支援擷取的 Http 標頭，並啟動 hello 新活動。 

`System.Net.HttpClient`版本開始`<fill in>`支援 hello 相互關聯的 Http 標頭和追蹤活動與 hello http 呼叫的自動資料隱碼。

新的 Http 模組[Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) hello ASP.NET 傳統。 此模組會使用 DiagnosticsSource 來實作遙測相互關聯。 它會根據傳入的要求標頭來啟動活動。 它也將遙測 hello 不同階段的要求處理從相互關聯。 即使對於 hello 情況下在 IIS 處理的每個階段會在不同的管理執行緒上執行。

應用程式 Insights SDK 版本開始`2.4.0-beta1`使用 DiagnosticsSource 和活動 toocollect 遙測，並將它與 hello 目前活動產生關聯。 

## <a name="next-steps"></a>後續步驟

- [撰寫自訂遙測](app-insights-api-custom-events-metrics.md)
- 在 Application Insights 上將微服務的所有元件上架。 查看[支援的平台](app-insights-platforms.md)。
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 了解如何太[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。
