---
title: "aaaAzure Insights 遙測資料模型的應用程式-要求遙測 |Microsoft 文件"
description: "要求遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>要求遙測：Application Insights 資料模型

要求遙測項目 (在[Application Insights](app-insights-overview.md)) 代表 hello 觸發 tooyour 應用程式外部要求所執行的邏輯順序。 依唯一識別每個要求執行`ID`和`url`包含所有 hello 執行中參數。 您可以依邏輯分組要求`name`並定義 hello`source`這項要求。 程式碼執行可能會導致 `success` 或 `fail`，並且有特定 `duration`。 成功和失敗的執行都可以進一步以 `resultCode` 分組。 開始 hello 要求遙測 hello 信封層級上定義的時間。

要求遙測支援使用自訂的 hello 標準的擴充性模型`properties`和`measurements`。

## <a name="name"></a>名稱

Hello 要求名稱表示程式碼採取路徑 tooprocess hello 要求。 較低的基數值 tooallow 更好的要求分組。 代表 HTTP 要求的 hello HTTP 方法和 URL 路徑範本，例如`GET /values/{id}`沒有實際的 hello`id`值。

應用程式 Insights web SDK 會與相關事宜 tooletter 案例傳送要求 「 現狀 」 的名稱。 在 UI 上的群組會區分大小寫因此`GET /Home/Index`分開計算從`GET /home/INDEX`即使它們通常會在 hello 相同控制器與動作執行。 hello，原因是 url 通常會[區分大小寫](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)。 如果要將所有可能會想要 toosee`404`發生 hello url 為大寫。 您可以讀取多個在要求名稱集合的 ASP.Net Web SDK 在 hello[部落格文章](http://apmtips.com/blog/2015/02/23/request-name-and-url/)。

最大長度︰1024 個字元

## <a name="id"></a>ID

要求呼叫執行個體的識別碼。 用於要求和其他遙測項目之間的相互關聯。 識別碼必須是全域唯一的。 如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。

最大長度︰128 個字元

## <a name="url"></a>Url

包含所有查詢字串參數的要求 URL。

最大長度︰2048 個字元

## <a name="source"></a>來源

Hello 要求來源。 範例包括 hello 呼叫端的 hello 檢測金鑰或 hello 呼叫端的 hello ip 位址。 如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。

最大長度︰1024 個字元

## <a name="duration"></a>持續時間

要求持續時間格式為︰`DD.HH:MM:SS.MMMMMM`。 必須是正數且小於 `1000` 天。 因為要求遙測代表 hello 與 hello 開頭和結尾 hello 的作業，此欄位為必要。

## <a name="response-code"></a>Response code

要求執行的結果。 HTTP 要求的 HTTP 狀態碼。 可能是 `HRESULT` 值或其他要求類型的例外狀況類型。

最大長度︰1024 個字元

## <a name="success"></a>成功

表示成功或失敗的呼叫。 這是必填欄位。 當未明確設定太`false`-視為 toobe 成功的要求。 將此值設定為太`false`如果作業已因例外狀況或傳回錯誤結果碼。

Hello web 應用程式，Application Insights 定義要求為失敗 hello 回應程式碼時較少的 hello`400`或太等於`401`。 不過一些情況下這個預設對應不符合 hello hello 應用程式的語意。 回應碼 `404` 可能表示「沒有記錄」，這可能是一般流程的一部分。 它也可能表示中斷的連結。 Hello 中斷連結，您甚至可以實作更進階的邏輯。 只有當那些連結位於相同站台藉由分析 url 查閱者 hello 時，您可以中斷的連結標示為失敗。 或將它們標示為失敗時從 hello 公司的行動應用程式存取。 同樣地`301`和`302`表示失敗時從不支援重新導向的 hello 用戶端存取。

部分接受的內容 `206` 可能表示整體要求失敗。 例如，Application Insights 端點會接收一批遙測項目作為單一要求。 它會傳回`206`當 hello 批次中的某些項目未處理成功。 遞增的速率`206`表示需要 toobe 調查的問題。 類似的邏輯適用於太`207`多重狀態可能 hello 成功 hello 最差的個別的回應碼。

您可以讀取多個開啟的要求結果的程式碼和狀態碼 hello[部落格文章](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/)。

## <a name="custom-properties"></a>自訂屬性

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>自訂度量

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>後續步驟

- [撰寫自訂要求遙測](app-insights-api-custom-events-metrics.md#trackrequest)
- 如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。
- 了解如何太[設定 ASP.NET Core](app-insights-asp-net.md)使用 Application Insights 應用程式。
- 查看 Application Insights 支援的[平台](app-insights-platforms.md)。
