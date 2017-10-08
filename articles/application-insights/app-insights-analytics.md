---
title: "aaaAnalytics-Azure Application Insights 的 hello 功能強大的搜尋工具 |Microsoft 文件"
description: "分析、 Application Insights 的 hello 功能強大的診斷搜尋工具的概觀。 "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Application Insights 中的分析
[分析](app-insights-analytics.md)是功能強大的搜尋功能 hello [Application Insights](app-insights-overview.md)。 這些分頁說明 Log Analytics 查詢語言。 

* **[請觀看 hello 簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。
* **[測試模擬資料的磁碟機分析](https://analytics.applicationinsights.io/demo)**如果您的應用程式未尚未傳送資料 tooApplication 深入資訊。
* **[SQL 使用者 ' 速查表](https://aka.ms/sql-analytics)**轉譯 hello 最常見慣用語。
* **[語言參考](app-insights-analytics-reference.md)**深入了解如何 toouse 所有 hello hello 記錄分析查詢語言的強大功能。


## <a name="queries-in-analytics"></a>分析中的查詢功能
標準的查詢是一個「來源」資料表，後面接著一系列由 `|` 隔開的「運算子」。 

例如，讓我們了解天 hello 公民 Hyderabad 的什麼時間，請嘗試我們的 web 應用程式。 而且，雖然我們有，我們來看看哪些結果碼會傳回 tootheir HTTP 要求。 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

我們計數不同的用戶端 IP 位址，群組它們 hello hello 一天的每小時透過 hello 過去 7 天。 

> [!NOTE]
> tooget 結果之外 hello 前一個 24 小時，請在查詢中，明確地包含 'timestamp' 或使用 hello 時間範圍下拉式選單。
>

讓我們來顯示以 hello 圖表展示檔，從不同的回應碼選擇 toostack hello 結果列 hello 結果：

![選擇橫條圖、X 和 Y 軸，然後分割](./media/app-insights-analytics/020.png)

看來我們的應用程式在海德拉巴的午休時間及就寢時間最受歡迎。 (而且我們應該調查那些 500 的代碼。)

也有強大的統計運算功能︰

![統計查詢的結果](./media/app-insights-analytics/025.png)

hello 語言有許多吸引人的功能：


* [篩選](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 未經處理的應用程式遙測，包括您的自訂屬性和計量。
* [加入](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) 多個資料表 – 將要求與頁面檢視、相依性呼叫、例外狀況和記錄追蹤相互關聯。
* 功能強大的統計 [彙總](https://docs.loganalytics.io/learn/tutorials/aggregations.html)。
* 就功能一樣強大 SQL，但更複雜的查詢： 而不是巢狀陳述式，您使用管線傳送 hello 資料從一個基本作業 toohello 下一步。
* 立即且功能強大的視覺效果。
* [釘選圖 tooAzure 儀表板](app-insights-analytics-using.md#pin-to-dashboard)。
* [匯出查詢 tooPower BI](app-insights-analytics-using.md#export-to-power-bi)。
* 沒有[REST API](https://dev.applicationinsights.io/) ，您可以使用 toorun 查詢以程式設計的方式，例如從 Powershell。


## <a name="connect-tooyour-application-insights-data"></a>Tooyour Application Insights 資料連接
在 Application Insights 中，從 app 的 [概觀刀鋒視窗](app-insights-dashboards.md) 開啟 [分析]： 

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics/001.png)


## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>查詢範例

請嘗試使用分析這些逐步解說 tooillustrate hello 電源：

 *  [自動診斷要求持續時間中的突增和步驟跳躍 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [以時間序列分析對效能降低進行分析 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [以 autocluster 和 diffpatterns 分析應用程式失敗 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [搭配時間序列分析的進階圖形偵測 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [使用滑動視窗作業 tooanalyze 應用程式使用方式 （輪換 MAU/DAU 等等）](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [根據偵錯記錄檔的分析來偵測服務中斷 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true)，以及[這篇 (英文)](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics) 相對應的部落格文章。
 *  [使用簡單的偵錯記錄檔來分析應用程式的效能 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true)，以及[這篇 (英文)](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/) 相對應的部落格文章
 *  [測量每個步驟，您使用簡單的偵錯記錄檔的程式碼流程中的 hello 持續時間](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true)和比對的部落格文章[這裡](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [使用簡單的偵錯記錄檔來分析並行 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true)，以及[這篇 (英文)](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/) 相對應的部落格文章



## <a name="next-steps"></a>後續步驟
* 我們建議您以 hello 開頭[語言教學課程](app-insights-analytics-tour.md)。 
* 深入了解如何[使用分析](app-insights-analytics-using.md)。 
* [語言參考](app-insights-analytics-reference.md)。 
