---
title: "aaaAzure 應用程式 Insights 遙測資料模型 |Microsoft 文件"
description: "Application Insights 資料模型概觀"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Application Insights 遙測資料模型

[Azure 的 Application Insights](app-insights-overview.md)傳送遙測從您的 web 應用程式 toohello Azure 入口網站，讓您可以分析 hello 效能和您的應用程式的使用方式。 hello 遙測模型已標準化，使其可能 toocreate 平台和語言無關的監視。 

Application Insights 所收集的資料會建立一般應用程式執行模式的模型︰

![Application Insights 應用程式模型](./media/application-insights-data-model/application-insights-data-model.png)

hello 下列類型的遙測資料會使用的 toomonitor hello 執行您的應用程式。 hello 下列三種類型通常會自動收集由 hello Application Insights SDK 從 hello web 應用程式架構：

* [**要求**](application-insights-data-model-request-telemetry.md) -產生 toolog 您應用程式所收到的要求。 例如，hello Application Insights web SDK 會自動產生每個 web 應用程式接收的 HTTP 要求的要求遙測項的目。 

    **作業**是 hello 執行執行緒的處理要求。 您也可以[撰寫程式碼](app-insights-api-custom-events-metrics.md#trackrequest)toomonitor 其他類型的作業，例如 「 喚醒 」 中的 web 工作，或函式，會定期處理資料。  每個作業都有識別碼。 這個識別碼可能是使用的 too[group]((application-insights-correlation.md) 所有遙測都產生您的應用程式正在處理 hello 要求時。 每個作業可能會成功或失敗，而且有持續時間。
* [**例外狀況**](application-insights-data-model-exception-telemetry.md) -通常表示導致作業 toofail 例外狀況。
* [**相依性**](application-insights-data-model-dependency-telemetry.md) -代表呼叫從您的應用程式 tooan 外部服務或儲存體，例如 REST API 或 SQL。 在 ASP.NET 中，所定義相依性呼叫 tooSQL `System.Data`。 呼叫 tooHTTP 端點會由`System.Net`。 

Application Insights 針對自訂遙測提供三種其他資料類型：

* [追蹤](application-insights-data-model-trace-telemetry.md)-請直接使用，或透過配接器 tooimplement 診斷記錄的使用是很熟悉 tooyou，例如 instrumentation framework`Log4Net`或`System.Diagnostics`。
* [事件](application-insights-data-model-event-telemetry.md)-通常是使用與您的服務 tooanalyze 習慣 toocapture 使用者互動。
* [公制](application-insights-data-model-metric-telemetry.md)-使用 tooreport 週期性的純量度量。

每個遙測項目可以定義 hello[內容資訊](application-insights-data-model-context.md)像應用程式版本或使用者工作階段識別碼。內容是一組在某些情況下會解除封鎖的強型別欄位。 正確初始化應用程式版本之後，Application Insights 可以偵測與重新部署相互關聯的應用程式行為中是否有新模式。 工作階段識別碼可以是使用的 toocalculate hello 中斷或使用者問題影響。 計算特定失敗相依性、錯誤追蹤或重大例外狀況之工作階段識別碼值的相異計數，即可充分了解影響。

Application Insights 遙測模型定義的方式太[相互關聯](application-insights-correlation.md)遙測 toohello 作業，它是在其中一部分。 例如，要求會發出 SQL Database 呼叫，並記錄診斷資訊。 您可以設定遙測項目，將它連接後 toohello 要求遙測 hello 相互關聯內容。

## <a name="schema-improvements"></a>結構描述的增強功能

應用程式的 Insights 資料模型是簡單和基本但功能強大的方式 toomodel 您應用程式遙測。 我們致力於 tookeep hello 模型簡單和輕薄 toosupport 重要案例，並允許 tooextend hello 結構描述，供進階使用。

tooreport 資料模型或結構描述問題，以及建議使用 GitHub [ApplicationInsights 首頁](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema)儲存機制。

## <a name="next-steps"></a>後續步驟

- [撰寫自訂遙測](app-insights-api-custom-events-metrics.md)
- 了解如何太[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。
- 使用[取樣](app-insights-sampling.md)的遙測的 toominimize 數量取決於資料模型。
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
