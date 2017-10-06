---
title: "aaaAzure Insights 遙測資料模型的應用程式的例外狀況遙測 |Microsoft 文件"
description: "例外狀況遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>例外狀況遙測：Application Insights 資料模型

在[Application Insights](app-insights-overview.md)，例外狀況的執行個體代表 hello 受監視應用程式執行期間發生的處理或未處理例外狀況。

## <a name="problem-id"></a>問題識別碼

已在程式碼中擲回 hello 例外狀況的識別項。 用於例外狀況群組。 一般例外狀況類型的組合和 hello 函式的呼叫堆疊。

最大長度︰1024 個字元

## <a name="severity-level"></a>嚴重性層級

追蹤嚴重性層級。 值可為 `Verbose`、`Information`、`Warning`、`Error`、`Critical`。

## <a name="exception-details"></a>例外狀況詳細資料

(toobe 擴充)

## <a name="custom-properties"></a>自訂屬性

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>自訂度量

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>後續步驟

- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 了解如何太[診斷使用 Application Insights web 應用程式中的例外狀況](app-insights-asp-net-exceptions.md)。
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
