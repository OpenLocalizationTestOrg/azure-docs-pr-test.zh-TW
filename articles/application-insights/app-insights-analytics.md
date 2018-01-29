---
title: "Analytics - Azure Application Insights 強大的搜尋和查詢工具 | Microsoft Docs"
description: "分析概觀，強大的 Application Insights 診斷搜尋工具。 "
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: mbullwin
ms.openlocfilehash: adda6335b702470cd491f07d750236c368325a9e
ms.sourcegitcommit: 21a58a43ceceaefb4cd46c29180a629429bfcf76
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="analytics-in-application-insights"></a>Application Insights 中的分析
Analytics 是 [Application Insights](app-insights-overview.md) 強大的搜尋和查詢工具。 Analytics 是 web 工具，不需要設定。 如果已經為您的其中一個應用程式設定 Application Insights，則您可以從應用程式的[概觀刀鋒視窗](app-insights-dashboards.md)開啟 Analytics 來分析應用程式的資料。

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics/001.png)

您也可以使用 [Analytics 遊樂場](https://go.microsoft.com/fwlink/?linkid=859557)，這是含有大量範例資料的免費示範環境。
<br>
<br>
> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

## <a name="query-data-in-analytics"></a>在 Analytics 中查詢資料
查詢通常以資料表名稱開頭，後面接著一連串以 `|` 隔開的「運算子」。
例如，讓我們查明應用程式在過去 3 小時內從不同國家/地區收到多少要求：
```AIQL
requests
| where timestamp > ago(3h)
| summarize count() by client_CountryOrRegion
| render piechart
```

我們從資料表名稱 *requests* 開始，並視需要新增管道元素。  首先，我們定義時間篩選條件，只檢閱過去 3 小時的資料列。
接著，我們計算每個國家/地區的資料列數目 (此資料在 *client_CountryOrRegion* 資料行中)。 最後，我們將結果呈現在圓形圖中。
<br>

![查詢結果](./media/app-insights-analytics/030.png)

這個語言具有許多吸引人的功能︰

* [篩選](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 未經處理的應用程式遙測，包括您的自訂屬性和計量。
* [加入](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) 多個資料表 – 將要求與頁面檢視、相依性呼叫、例外狀況和記錄追蹤相互關聯。
* 功能強大的統計 [彙總](https://docs.loganalytics.io/docs/Learn/Tutorials/Aggregation-functions)。
* 立即且功能強大的視覺效果。
* [REST API](https://dev.applicationinsights.io/)，可讓您以程式設計方式 (例如從 PowerShell) 執行查詢。

[完整語言參考](https://go.microsoft.com/fwlink/?linkid=856079)詳述每個支援的命令，並更新定期。

## <a name="next-steps"></a>後續步驟
* 開始使用 [Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)
* 開始[撰寫查詢](https://go.microsoft.com/fwlink/?linkid=856078)
* 檢閱 [SQL 使用者的速查表](https://aka.ms/sql-analytics)，以取得最常見慣用語的翻譯。
* 如果您的應用程式還未將資料傳送至 Application Insights，請在我們的[遊樂場](https://analytics.applicationinsights.io/demo)上試用 Analytics。
* 觀看[簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)。