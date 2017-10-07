---
title: "aaaAzure 應用程式 Insights 遙測資料模型的度量遙測 |Microsoft 文件"
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
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>計量遙測：Application Insights 資料模型

[Application Insights](app-insights-overview.md) 支援兩種類型的計量遙測：單一測量和預先彙總的計量。 單一度量只有名稱與值。 預先彙總的度量會指定在 hello 彙總間隔和它的標準差 hello 標準最小和最大值。

預先彙總的計量遙測會假設該彙總期間為一分鐘。

Application Insights 支援數個已知的計量名稱。 

代表系統和程序計數器的計量︰

| **.NET 名稱**             | **平台無從驗證的名稱** | **REST API 名稱** | **說明**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | 進行中... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | 電腦 CPU 總數
| `\Memory\Available Bytes`                 | 進行中... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | 磁碟上可用的記憶體
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | 進行中... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | Hello 裝載 hello 應用程式的處理程序的 CPU
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | 進行中... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | hello 裝載 hello 應用程式的處理程序所使用的記憶體
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | 進行中... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | 裝載 hello 應用程式的處理序所執行的 I/O 作業速率
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | 進行中... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | 應用程式處理要求的速率 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | 進行中... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | 應用程式擲回例外狀況的速率
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | 進行中... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | 平均要求執行時間
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | 進行中... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | 等候處理佇列中的 hello 的要求數目

## <a name="name"></a>名稱

名稱的 hello 度量您想要在 Application Insights 入口網站和 UI 中的 toosee。 

## <a name="value"></a>值

度量的單一值。 Hello 彙總的個別度量值的總和。

## <a name="count"></a>Count

衡量標準權數 hello 的彙總度量。 不應該為度量設定。

## <a name="min"></a>Min

Hello 彙總的度量最小值。 不應該為度量設定。

## <a name="max"></a>max

彙總的 hello 標準的最大值。 不應該為度量設定。

## <a name="standard-deviation"></a>標準差

彙總的 hello 標準的標準差。 不應該為度量設定。

## <a name="custom-properties"></a>自訂屬性

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>後續步驟

- 深入了解如何 toouse[應用程式的自訂事件和度量的 Insights API](app-insights-api-custom-events-metrics.md#trackmetric)。
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
