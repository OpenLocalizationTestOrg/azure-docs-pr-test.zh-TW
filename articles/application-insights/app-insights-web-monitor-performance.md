---
title: "aaaMonitor 應用程式的健全狀況和使用 Application Insights 的使用方式"
description: "開始使用 Application Insights。 分析內部部署或 Microsoft Azure 應用程式的使用情況、可用性和效能。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>監視 Web 應用程式的效能


確認應用程式的運作狀況良好，以及迅速找出任何失敗。 [Application Insights] [ start]會告訴您有關任何效能問題和例外狀況，以及可協助您尋找並診斷 hello 根本原因。

Application Insights 可以監視 Java 和 ASP.NET Web 應用程式與服務、WCF 服務。 這些服務可以裝載在內部部署、虛擬機器上，或作為 Microsoft Azure 網站。 

Hello 用戶端，Application Insights 可以採取網頁和各種不同的裝置，包括 iOS、 Android 和 Windows 市集應用程式的遙測。

>[!Note]
> 我們讓尋找您的 Web 應用程式中緩慢執行分頁有新的體驗。 如果您沒有存取 tooit，啟用以 hello 設定預覽選項[預覽刀鋒伺服器](app-insights-previews.md)。 了解這個新體驗中[找出並修正與 hello 互動式效能調查的效能瓶頸](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation)。

## <a name="setup"></a>設定效能監視
如果您還沒有加入 Application Insights tooyour （亦即，如果它沒有 ApplicationInsights.config） 專案，選擇下列其中一種 tooget 啟動：

* [ASP.NET Web 應用程式](app-insights-asp-net.md)
  * [加入例外狀況監視](app-insights-asp-net-exceptions.md)
  * [加入相依性監視](app-insights-monitor-performance-live-website-now.md)
* [J2EE Web 應用程式](app-insights-java-get-started.md)
  * [加入相依性監視](app-insights-java-agent.md)

## <a name="view"></a>探索效能度量
在[hello Azure 入口網站](https://portal.azure.com)，瀏覽 toohello 設定您的應用程式的 Application Insights 資源。 hello 概觀刀鋒視窗會顯示基本的效能資料：

按一下詳細資料，因而 toosee 任何圖表 toosee 更長的時間。 例如，按一下 hello 要求磚，然後選取 時間範圍：

![瀏覽 toomore 的資料，並選取時間範圍](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

按一下圖表 toochoose 它會顯示，或將新的圖表，並選取其度量的度量：

![按一下圖形 toochoose 度量](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **取消選取所有 hello 度量**toosee hello 完整選取項目所提供。 hello 度量分成群組。選取任何群組的成員時，只有 hello 該群組的其他成員會出現。

## <a name="metrics"></a>這具有哪些意義？ 效能磚和報告
您可以取用多種效能計量。 讓我們開始與 hello 應用程式 刀鋒視窗預設會出現。

### <a name="requests"></a>Requests
hello 指定期間內收到的 HTTP 要求數。 請比較這上隨著 hello 負載而改變，您的應用程式的行為方式的其他報表 toosee hello 結果。

HTTP 要求包括分頁、資料及映像的所有 GET 或 POST 要求。

按一下特定 Url 的 hello 磚 tooget 計數。

### <a name="average-response-time"></a>平均回應時間
輸入您的應用程式和 hello 回應所傳回的 web 要求之間的量值 hello 時間。

hello 點顯示移動平均。 如果有許多要求，可能會有一些偏離 hello 平均沒有明顯的尖峰或大大 hello 圖形中。

找尋異常的高峰。 一般情況下，預期升高要求與回應時間 toorise。 如果不相稱 hello 上升，您的應用程式可能會達到資源限制，例如 CPU 或 hello 容量的服務，它會使用。

按一下 hello 磚 tooget 時間特定的 url。

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>最慢的要求
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

顯示可能需要進行效能調整的要求。

### <a name="failed-requests"></a>失敗的要求
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

丟出無法攔截之例外狀況的要求計數。

按一下 hello 磚 toosee hello 詳細資料的特定失敗，並選取個別要求 toosee 其詳細資料。 

系統只會針對各項檢查保留一個具代表性的失敗範例。

### <a name="other-metrics"></a>其他度量
toosee 哪些其他度量可以顯示，並按一下圖形，然後取消選取所有 hello 度量 toosee hello 完整可用組。 按一下 (i) toosee 每個度量定義。

![取消選取所有度量 toosee hello 整個組](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

其他不可以出現在選取的任何度量會停用 hello hello 相同的圖表。

## <a name="set-alerts"></a>設定警示
收到的異常值的任何度量，電子郵件通知的 toobe 加入警示。 您可以選擇 toosend hello 電子郵件 toohello 帳戶系統管理員或 toospecific 電子郵件地址。

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

設定前 hello hello 資源的其他屬性。 如果您想 tooset 效能或使用量度量的警示，不要選擇 hello webtest 資源。

能謹慎 toonote hello 單位中，系統會詢問 tooenter hello 臨界值。

*看不見 hello 新增警示 按鈕。* -這是具有唯讀存取權的群組帳戶 toowhich 嗎？ 請檢查與 hello 帳戶系統管理員。

## <a name="diagnosis"></a>診斷問題
以下是幾個尋找及診斷效能問題的訣竅：

* 設定[web 測試][ availability] toobe 如果網站當機，或不正確或速度很慢回應警示。 
* 如果失敗或緩慢的回應相關的 tooload，比較與其他度量 toosee hello 要求計數。
* [插入和搜尋追蹤陳述式][ diagnostic]中程式碼 toohelp 找出問題。
* 使用[即時計量資料流][livestream]監視作業中的 Web 應用程式。
* 擷取您的.Net 應用程式的 hello 狀態[快照偵錯工具][snapshot]。

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>使用互動式效能調查尋找及修正效能瓶頸

您可以使用 hello 新 Application Insights 互動式效能調查 toolocate 您 Web 應用程式的區域會減緩整體效能。 您可以快速地尋找特定頁面的速度變慢，並使用 hello[程式碼剖析工具](app-insights-profiler.md)toosee 如果沒有這些網頁之間的相互關聯。

### <a name="create-a-list-of-slow-performing-pages"></a>建立一份執行緩慢分頁的清單 

hello 尋找效能問題的第一個步驟是 tooget hello 慢回應頁面的清單。 hello 下列螢幕擷取畫面將示範如何使用 hello 效能刀鋒視窗 tooget 潛在頁面 tooinvestigate 進一步的清單。 您可以快速查看從這個頁面時發生 slow-down hello 回應 hello 應用程式時間下午約 6:00，然後又在大約 10 PM。 您也可以查看 hello 取得客戶/詳細資料的作業有一些長時間執行作業中間值回應時間為 507.05 毫秒為單位。 

![Application Insights 互動式效能](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>向下鑽研特定分頁

您有了應用程式效能的快照集之後，您可以取得更多特定執行緩慢作業的詳細資料。 按一下任何作業中 hello 清單 toosee hello 詳細資料如下所示。 從 hello 圖表中，您可以看到 hello 效能為基礎的相依性。 您也可以查看多少使用者經驗的 hello 不同回應時間。 

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>在特定時間週期向下鑽研

識別 tooinvestigate 時間點之後，甚至進一步 toolook 在 hello 特定作業可能會造成 hello 效能 slow-down 的向下鑽研。 當您按一下特定點上的時間就 hello 頁面如下所示的 hello 詳細資料。 在 hello 低於您的範例可以看到 hello 作業列出指定的時段內以及 hello 伺服器回應碼和 hello 作業持續時間。 您也具有開啟 TFS 工作項目，如果您需要此資訊 tooyour 開發團隊 toosend hello url。

![Application Insights 時間配量](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>在特定作業向下鑽研

識別 tooinvestigate 時間點之後，甚至進一步 toolook 在 hello 特定作業可能會造成 hello 效能 slow-down 的向下鑽研。 按一下 hello 清單 toosee hello 作業的詳細資料 hello 如下所示的作業。 在此範例中的 hello 作業失敗，以及 Application Insights 所提供的 hello hello 詳細資料，您可以看到擲回例外狀況 hello 應用程式。 同樣地，您可以從這個刀鋒視窗輕鬆地建立 TFS 工作項目。

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>接續步驟
[Web 測試][ availability] -web 要求傳送 tooyour 應用程式定期從 hello 世界各地。

[擷取和搜尋診斷追蹤][ diagnostic] -插入追蹤呼叫和詳查 hello 結果 toopinpoint 問題。

[流量追蹤][usage] - 了解使用者使用應用程式的情況。

[疑難排解][qna] - 以及問答集



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



