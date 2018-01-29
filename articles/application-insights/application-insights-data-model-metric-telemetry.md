---
title: "Azure Application Insights 遙測資料模型 - 計量遙測 | Microsoft Docs"
description: "計量遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: bd09e2a21c25097fa4b378cb2dbe2787edbb1967
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>計量遙測：Application Insights 資料模型

[Application Insights](app-insights-overview.md) 支援兩種類型的計量遙測：單一測量和預先彙總的計量。 單一度量只有名稱與值。 預先彙總的計量會指定彙總間隔中計量的最小值和最大值以及它的標準差。

預先彙總的計量遙測會假設該彙總期間為一分鐘。

Application Insights 支援數個已知的計量名稱。 這些計量會置入 performanceCounters 資料表。

代表系統和程序計數器的計量︰

| **.NET 名稱**             | **平台無從驗證的名稱** | **REST API 名稱** | **說明**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | 進行中... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | 電腦 CPU 總數
| `\Memory\Available Bytes`                 | 進行中... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | 磁碟上可用的記憶體
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | 進行中... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | 裝載應用程式之處理序的 CPU
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | 進行中... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | 裝載應用程式之處理序所使用的記憶體
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | 進行中... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | 裝載應用程式之處理序執行的 I/O 作業速率
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | 進行中... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | 應用程式處理要求的速率 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | 進行中... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | 應用程式擲回例外狀況的速率
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | 進行中... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | 平均要求執行時間
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | 進行中... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | 佇列中等候處理的要求數目

## <a name="name"></a>名稱

您想要在 Application Insights 入口網站和 UI 中看到的計量名稱。 

## <a name="value"></a>值

度量的單一值。 個別彙總度量的總和。

## <a name="count"></a>Count

彙總計量的計量權數。 不應該為度量設定。

## <a name="min"></a>Min

彙總計量的最小值。 不應該為度量設定。

## <a name="max"></a>max

彙總計量的最大值。 不應該為度量設定。

## <a name="standard-deviation"></a>標準差

彙總計量的標準差。 不應該為度量設定。

## <a name="custom-properties"></a>自訂屬性

將自訂屬性 `CustomPerfCounter` 設為 `true` 的計量，會顯示出該計量代表 Windows 效能計數器。 這些計量會置入 performanceCounters 資料表。 而不會置入 customMetrics。 另外也會剖析此計量名稱，以擷取分類、計數器，以及執行個體名稱。

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>後續步驟

- 了解如何使用[自訂事件和計量的 Application Insights API](app-insights-api-custom-events-metrics.md#trackmetric)。
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
