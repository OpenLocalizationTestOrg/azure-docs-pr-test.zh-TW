---
title: "aaaSmart Detection in Azure Application Insights |Microsoft 文件"
description: "Application Insights 會自動深入分析您的 App 遙測，並且警告您有潛在的問題。"
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Application Insights 中的智慧型偵測
 「智慧型偵測」會自動警告您 Web 應用程式中的可能效能問題。 它會執行的應用程式傳送太 hello 遙測的主動式分析[Application Insights](app-insights-overview.md)。 如果失敗率急遽上升或是用戶端或伺服器效能出現異常模式，您就會收到警示。 這項功能不需要進行任何設定。 只要您的應用程式傳送的遙測足夠，它就能發揮作用。

您可以在 hello 電子郵件收到，和從 hello 智慧偵測刀鋒視窗存取智慧偵測警示。

## <a name="review-your-smart-detections"></a>檢閱智慧型偵測
您可以透過兩種方式探索偵測︰

* **接收來自 Application Insights 的電子郵件** 。 以下是典型範例︰
  
    ![電子郵件警示](./media/app-insights-proactive-diagnostics/03.png)
  
    按一下 hello 大按鈕 tooopen hello 入口網站中的更多詳細資料。
* **hello 智慧偵測磚**在您的應用程式概觀刀鋒視窗會顯示最近的警示計數。 按一下 hello 磚 toosee 一份最近的警示。

![檢視最近的偵測](./media/app-insights-proactive-diagnostics/04.png)

選取警示的 toosee 其詳細資料。

## <a name="what-problems-are-detected"></a>可偵測到哪些問題？
共有三種偵測︰

* [智慧型偵測 - 失敗異常](app-insights-proactive-failure-diagnostics.md)。 我們使用機器學習服務失敗的要求，您的應用程式中，然後再建立相互關聯使用負載和其他因素 tooset hello 預期率。 如果 hello 失敗率 hello 預期信封外，我們會傳送警示。
* [智慧型偵測 - 效能異常](app-insights-proactive-performance-diagnostics.md)。 如果作業或相依性的持續時間的回應時間變慢 toohistorical 比較的基準或我們識別異常的模式中回應時間或頁面載入時間，您會收到通知。   
* [智慧型偵測 - Azure 雲端服務問題](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/)。 如果您的應用程式裝載於 Azure 雲端服務，而且角色執行個體有啟動失敗、經常回收或執行階段損毀等現象，您便會收到警示。

（每個通知中的 hello 說明連結需要您 toohello 相關文章）。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟
這些診斷工具可協助您檢查您的應用程式的遙測 hello:

* [計量瀏覽器](app-insights-metrics-explorer.md)
* [搜尋總管](app-insights-diagnostic-search.md)
* [分析 - 功能強大的查詢語言](app-insights-analytics-tour.md)

「智慧型偵測」是全自動的。 但您可能要 tooset 某些更多的警示嗎？

* [手動設定的度量警示](app-insights-alerts.md)
* [可用性 Web 測試](app-insights-monitor-web-app-availability.md) 

