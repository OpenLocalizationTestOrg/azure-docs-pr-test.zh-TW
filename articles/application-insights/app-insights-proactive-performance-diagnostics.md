---
title: "aaaSmart 偵測-效能異常 |Microsoft 文件"
description: "Application Insights 會執行您應用程式遙測的智慧型分析，並且警告您有潛在的問題。 這項功能不需要進行任何設定。"
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>智慧型偵測 - 效能異常

[Application Insights](app-insights-overview.md)自動分析 hello web 應用程式的效能，並警告您有關潛在問題。 您會讀取到此訊息，可能是因為您收到一個我們的智慧型偵測通知。

除了設定您 Application Insights 的應用程式 (在 [ASP.NET](app-insights-asp-net.md) 上、[Java](app-insights-java-get-started.md) 或 [Node.js](app-insights-nodejs.md)，以及在[網頁程式碼](app-insights-javascript.md)中) 以外，這項功能不需要特殊設定。 當您的應用程式產生足夠的遙測時，就會是在作用中。

## <a name="when-would-i-get-a-smart-detection-notification"></a>何時會取得智慧型偵測通知？

Application Insights 偵測 hello 應用程式的效能降低在下列其中一種：

* **回應時間降低**-您的應用程式已開始使用的放慢回應 toorequests。 hello 變更可能已快速，例如因為發生在最新的部署中的迴歸。 或者它可能是逐漸進行的，可能是由於記憶體流失所造成。 
* **相依性持續時間降低**-呼叫 tooa REST API、 資料庫或其他相依性，可讓您的應用程式。 若要使用的放慢回應 hello 相依性。
* **效能變慢模式**-您的應用程式會出現的 toohave 效能問題會影響某些的要求。 例如，頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器；或是某一部特定伺服器服務要求的速度較慢。 目前，我們的演算法會查看頁面載入時間、要求回應時間，和相依性回應時間。  

智慧偵測需要至少 8 天的順序 tooestablish 的一般效能基準線中的可用磁碟區上的遙測資料。 因此，您的應用程式在這段時間內執行之後，任何嚴重的問題都會發出通知。


## <a name="does-my-app-definitely-have-a-problem"></a>我的應用程式絕對有問題嗎？

否，通知並不表示您的應用程式一定有問題。 它是只需有關可能會想要在 toolook 更緊密的東西的建議。

## <a name="how-do-i-fix-it"></a>如何修正問題？

hello 通知包含診斷資訊。 以下是範例：


![以下是伺服器回應時間降低偵測的範例](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **分級**。 hello 通知會顯示您的使用者人數，或多少作業會受到影響。 這可協助您指派優先權 toohello 問題。
2. **範圍**。 Hello 問題會影響所有流量或一些頁面嗎？ 是受限制的 it tooparticular 瀏覽器或位置？ 這項資訊可以取自 hello 通知。
3. **診斷**。 通常，hello hello 通知中的診斷資訊將會建議 hello hello 問題的性質。 例如，如果要求率很高時回應時間變慢，表示您的伺服器或相依性已超載。 

    否則，請開啟 Application Insights 中的 hello 效能刀鋒視窗。 您可以在此處找到[分析工具](app-insights-profiler.md)資料。 擲回例外狀況時，您也可以嘗試 hello[快照偵錯工具](app-insights-snapshot-debugger.md)。



## <a name="configure-email-notifications"></a>設定電子郵件通知

智慧偵測通知是預設啟用，並且會傳送具有 toothose[擁有者、 參與者與讀者存取 toohello Application Insights 資源](app-insights-resources-roles-access-control.md)。 toochange 這按一下**設定**hello 電子郵件通知，或開啟 Application Insights 中的智慧偵測設定。 
  
  ![智慧型偵測設定](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * 您可以使用 hello**取消訂閱**hello 智慧偵測電子郵件 toostop 接收 hello 電子郵件通知中的連結。

智慧偵測效能的異常狀況的相關電子郵件是每天每個 Application Insights 資源有限的 tooone 電子郵件。 只有當至少一個新的問題所偵測到在那一天，將會傳送 hello 電子郵件。 您不會重複收到任何訊息。 

## <a name="faq"></a>常見問題集

* *所以你們會看到我的資料嗎？*
  * 否。 hello 服務是完全自動。 只有您會收到 hello 通知。 您的資料是 [不公開的](app-insights-data-retention-privacy.md)。
* *在分析 Application Insights 所收集的所有 hello 資料嗎？*
  * 目前尚未。 我們目前會分析要求回應時間、相依性回應時間和頁面載入時間。 我們後續的未來展望中將有其他計量的分析。

* 這適用於哪些類型的應用程式？
  * 任何應用程式會產生 hello 適當遙測中偵測到這些衰退。 如果您在 Web 應用程式中安裝了 Application Insights，就會自動追蹤要求及相依性。 但在後端服務或其他應用程式，當您插入呼叫太[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest)或[TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency)，則智慧偵測的作用中 hello 相同的方式。

* 我可以建立自己的異常偵測規則或自訂現有的規則嗎？

  * 還不行，但是您可以︰
    * [設定警示](app-insights-alerts.md)，使其在計量超出臨界值時通知您。
    * [匯出遙測](app-insights-export-telemetry.md)tooa[資料庫](app-insights-code-sample-export-sql-stream-analytics.md)或[tooPowerBI](app-insights-export-power-bi.md)，其中您可以分析它自己。
* *Hello 分析執行頻率為何？*

  * 我們 hello 分析每日 hello 遙測，從執行 hello 前一天 （以 UTC 時區的全天）。
* *那麼，這可以取代[計量警示](app-insights-alerts.md)嗎？*
  * 否。  我們請不要認可 toodetecting 每個您可以考慮異常的行為。


* *如果我沒有進行任何回應 tooa 通知中的項目，我會收到提醒？*
  * 不會，每個問題您只會收到一次訊息。 如果 hello 問題仍存在它將會更新的 hello 智慧偵測摘要刀鋒視窗中。
* *我遺失 hello 電子郵件。其中 hello 入口網站中找到 hello 通知？*
  * 在 hello 的應用程式的 Application Insights 概觀，按一下 hello**智慧偵測**磚。 您會有無法 toofind back up too90 天的所有通知。

## <a name="how-can-i-improve-performance"></a>如何改善效能？
因為您知道從您自己的經驗，速度慢且失敗的回應是 hello 網站使用者的最大麻煩的其中一個。 因此，請務必 tooaddress hello 問題。

### <a name="triage"></a>分級
首先，這很重要嗎？ 如果頁面一律為慢速 tooload，但僅有 1%的站台的使用者永遠在它有 toolook，或許您有更重要的事情 toothink 有關。 在 hello 相反地，如果只有 1%的使用者開啟它，但它可能是值得調查每次擲回例外狀況。

一般方針是，使用 hello 影響陳述式 （受影響的使用者或 %的流量），但請注意，它不會 hello 整個本文。 收集其他的辨識項 tooconfirm。

請考慮 hello 問題的 hello 參數。 如果與地理位置有關，請設定包括該地區的 [可用性測試](app-insights-monitor-web-app-availability.md) ：該地區可能只有網路問題。

### <a name="diagnose-slow-page-loads"></a>診斷頁面載入緩慢
其中是 hello 問題？ 是 hello 伺服器緩慢 toorespond、 hello 網頁很長，或 hello 瀏覽器沒有 toodo 大量工作 toodisplay 它嗎？

開啟 hello 瀏覽器計量刀鋒伺服器。 hello 分割瀏覽器頁面載入時間顯示即將 hello 時間的顯示。 

* 如果**傳送要求時間**是高，可能是 hello 伺服器回應很慢，或 hello 要求是使用大量資料的文章。 查看 hello[效能度量](app-insights-web-monitor-performance.md#metrics)tooinvestigate 回應時間。
* 設定[相依性追蹤](app-insights-asp-net-dependencies.md)toosee hello 緩慢是否到期 tooexternal 服務或您的資料庫。
* 如果 [接收回應]  是主導因素，您的頁面和其相依組件 (JavaScript、CSS 及影像等，而非以非同步方式載入的資料) 會很長。 設定[可用性測試](app-insights-monitor-web-app-availability.md)，而且是確定 tooset hello 選項 tooload 相依組件。 當您取得一些結果時，開啟結果的 hello 詳細資料並將其展開 toosee hello 載入不同的檔案的時間。
* [用戶端處理時間]  過長表示指令碼執行速度很慢。 如果 hello 原因不明顯，請考慮加入一些執行時間程式碼，並傳送 hello 次 trackMetric 呼叫中。

### <a name="improve-slow-pages"></a>改善慢速網頁
沒有完整的建議改善您的伺服器回應和頁面載入時間，所以不會再次嘗試 toorepeat web 它在這裡。 以下是少數的提示，您可能已經了解只 tooget 你想：

* 慢速載入因為大型的檔案： 以非同步方式載入 hello 指令碼和其他組件。 使用指令碼統合。 分成個別載入其資料的 widget hello 主頁面。 不要傳送長資料表純舊 HTML： 指令碼 toorequest hello 資料做為 JSON 或其他精簡的格式，然後再填滿 hello 資料表中的位置。 沒有與這個所有絕佳架構 toohelp。 (當然，也必須承擔大型指令碼)。
* 降低伺服器的相依性： 請考慮 hello 元件的地理位置。 例如，如果您使用 Azure，請確定 hello 網頁伺服器與 hello 資料庫都處於 hello 相同的區域。 查詢是否會擷取超過所需的資訊？ 快取或批次處理是否有所幫助？
* 容量問題： 查看 hello 伺服器的度量資訊的回應時間，並要求計數。 如果回應時間尖峰與要求計數尖峰不成比例，有可能是您的伺服器已被過度使用。


## <a name="server-response-time-degradation"></a>伺服器回應時間降低

hello 回應時間降低通知會告訴您：

* hello 回應時間會比較 toonormal 這項作業的回應時間。
* 受影響的使用者人數。
* 平均回應時間及 90th 百分位數的回應時間 hello 當天 hello 偵測和 7 天前的此作業。 
* 這項作業的計數要求的 hello 偵測的 hello 日期和 7 天前。
* 這項作業之降低與相關相依性之降低間的相互關聯。 
* 連結 toohelp 診斷 hello 問題。
  * 分析工具會追蹤您檢視作業的時間花在哪裡 toohelp （hello 連結是使用這項作業在 hello 偵測期間所收集的 Profiler 追蹤範例）。 
  * 您可以在計量瀏覽器中的效能報告將這項作業的時間範圍/篩選條件進行交叉分析。
  * 這個搜尋呼叫 tooview 特定呼叫屬性。
  * 報告失敗-如果計數 1 >，這表示可能有貢獻 tooperformance 降低此作業中發生失敗。

## <a name="dependency-duration-degradation"></a>相依性持續時間降低

現代應用程式更採用微服務設計的方法，在許多情況下導致 tooheavy 可靠性外部服務。 例如，如果您的應用程式依賴某些資料平台，或您建立您自己 bot 服務您將可能轉送上某些認知的服務提供者 tooenable 多人為方式您 bot toointeract 和一些資料儲存區服務 bot toopull hello來自的答案。  

範例相依性降低通知︰

![以下是相依性持續時間降低偵測的範例](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

請注意，它會告訴您︰

* hello 持續時間會比較 toonormal 這項作業的回應時間
* 受影響的使用者人數
* 平均持續時間和 90th 百分位數持續時間此相依性的 hello 偵測的 hello 日期和 7 天前
* Hello 天數 hello 偵測和 7 天前呼叫的相依性的數目
* 連結 toohelp 診斷 hello 問題
  * 計量瀏覽器中此相依性的效能報告
  * 搜尋此相依性呼叫 tooview 呼叫屬性
  * 失敗 」 報告會-如果計數 > 1 表示已失敗的相依性呼叫期間 hello 偵測可能會有貢獻 tooduration 降級的期間。 
  * 使用計算此相依性持續時間和計數的查詢來開啟分析  

## <a name="smart-detection-of-slow-performing-patterns"></a>效能變慢模式的智慧型偵測 

Application Insights 會尋找可能只會影響某部分使用者，或只在某些情況下影響使用者的效能問題。 例如，通知關於頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器，或特定伺服器服務要求的速度較慢。 它同時可以探索與屬性組合相關的問題，例如在某地區中使用特定作業系統的用戶端，頁面載入速度緩慢的問題。  

這類的異常狀況是很難 toodetect 只是藉由檢查 hello 資料，但比您想像的較常見。 通常只在您的客戶抱怨時才會浮出檯面。 藉由這段時間，很晚： hello 受影響的使用者已切換 tooyour 競爭對手 ！

目前，我們演算法會尋找在頁面載入時間，在 hello 伺服器的要求回應時間和相依性回應時間。  

您尚未 tooset 任何臨界值，或設定規則。 機器學習和資料採礦演算法會使用的 toodetect 的異常模式。

![從 hello 電子郵件警示，按一下 hello 連結 tooopen hello 診斷報告在 Azure 中](./media/app-insights-proactive-performance-diagnostics/03.png)

* **當**顯示偵測到 hello hello 問題的時間。
* [對象] 說明：

  * 所偵測到; hello 問題
  * 我們發現顯示 hello 問題行為的事件集的 hello hello 特性。
* hello 表會比較 hello 佳的資料集的所有其他事件 hello 平均行為。

按一下相關的報告，hello 時間以及 hello 慢速執行設定的屬性篩選 hello 連結 tooopen 度量總管和搜尋。

修改 hello 時間範圍和篩選 tooexplore hello 遙測。

## <a name="next-steps"></a>後續步驟
這些診斷工具可協助您檢查您的應用程式的遙測 hello:

* [分析工具](app-insights-profiler.md) 
* [快照集偵錯工具](app-insights-snapshot-debugger.md)
* [分析](app-insights-analytics-tour.md)
* [分析智慧型診斷](app-insights-analytics-diagnostics.md)

智慧型偵測是完全自動的。 但您可能要 tooset 某些更多的警示嗎？

* [手動設定的度量警示](app-insights-alerts.md)
* [可用性 Web 測試](app-insights-monitor-web-app-availability.md)
