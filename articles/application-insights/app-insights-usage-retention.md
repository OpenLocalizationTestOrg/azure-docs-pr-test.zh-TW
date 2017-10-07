---
title: "使用 Azure Application Insights web 應用程式的 aaaUser 保留分析 |Microsoft 文件"
description: "多少個使用者傳回 tooyour 應用程式？"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>使用 Application Insights 進行 Web 應用程式的使用者保留期分析

中的 hello 保留功能[Azure Application Insights](app-insights-overview.md)可協助您分析的使用者人數傳回 tooyour 應用程式和頻率執行特定工作或達成目標。 例如，如果您執行遊戲的站台時，無法比較 hello 的使用者之後遺失 hello 數目的遊戲會傳回 toohello 站台成功後，傳回使用者的數字。 這項知識可以協助您改善使用者體驗和商務策略。

## <a name="get-started"></a>開始使用

如果您還沒有看到 hello 保留工具在 hello Application Insights 入口網站中的資料[學習 tooget hello 使用量工具的啟動方式](app-insights-usage-overview.md)。

## <a name="hello-retention-tool"></a>hello 保留工具

![保留期工具](./media/app-insights-usage-retention/retention.png)

1. hello 工具列可讓使用者 toocreate 新保留報表、 開啟現有的保留報表、 儲存目前保留報表或將儲存為、 還原所做的變更 toosaved 報表、 重新整理 hello 在報表上，透過電子郵件或直接連結，並存取 hello 共用報表的資料文件頁面。 
2. 根據預設，保留期會顯示執行任何動作然後回來，並且在一段期間內未執行任何其他動作的所有使用者。 您可以選取事件 toonarrow hello 專注於特定的使用者活動的不同的組合。
3. 在屬性新增一或多個篩選條件。 例如，您可以將重點放在特定國家或區域中的使用者。 按一下**更新**設定 hello 篩選器之後。 
4. hello 整體保留圖表可顯示使用者保留的摘要跨 hello 選取的時間週期。 
5. hello 方格會顯示 hello 人數保留 #2 中的相應 toohello 查詢產生器。 每個資料列都代表使用者的 cohort 期間顯示 hello 時間執行的任何事件。 Hello 資料列中的每個資料格會顯示多少個該 cohort 傳回在更新期間至少一次。 有些使用者可能會在不只一個期間內回來使用。 
6. hello insights 卡顯示前五個起始事件，並前五個傳回事件 toogive 使用者更深入了解其保留報表。 

![保留滑鼠暫留](./media/app-insights-usage-retention/hover.png)

使用者可以將滑鼠停留在 hello 保留工具 tooaccess hello 分析按鈕上的資料格，以及說明哪些 hello 儲存格的工具提示的方法。 hello 分析按鈕會預先填入的查詢 toogenerate 使用者與使用者 toohello 分析工具從 hello 儲存格。 

## <a name="use-business-events-tootrack-retention"></a>使用商務事件 tootrack 保留

tooget hello 最有用保留分析，將量值的事件，代表重要的商務活動。 

比方說，許多使用者可能會開啟網頁應用程式中而不播放，它會顯示 hello 遊戲。 追蹤只 hello 頁面檢視因此會提供不正確的方式有許多人 tooplay hello 遊戲後返回先前享受它估計。 tooget 清楚地了解傳回播放程式，您的應用程式應該傳送自訂事件時使用者實際播放。  

它是很好的作法 toocode 自訂事件，代表關鍵商務動作，並使用這些保留分析。 toocapture hello 遊戲結果，您需要 toowrite 一行程式碼 toosend 自訂事件 tooApplication 深入資訊。 如果您將資料寫入或 Node.JS hello 網頁程式碼中，它看起來像這樣：

```JavaScript
    appinsights.trackEvent("won game");
```

或是以 ASP.NET 伺服器程式碼撰寫：

```C#
   telemetry.TrackEvent("won game");
```

[深入了解撰寫自訂事件](app-insights-api-custom-events-metrics.md#trackevent)。


## <a name="next-steps"></a>後續步驟
- tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。
- 如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。
    - [使用者、工作階段、事件](app-insights-usage-segmentation.md)
    - [漏斗圖](usage-funnels.md)
    - [使用者流程](app-insights-usage-flows.md)
    - [活頁簿](app-insights-usage-workbooks.md)
    - [新增使用者內容](app-insights-usage-send-user-context.md)


