---
title: "aaaAzure Application Insights for JavaScript web 應用程式 |Microsoft 文件"
description: "取得頁面檢視和工作階段計數、Web 用戶端資料，並追蹤使用量模式。 Detect exceptions and performance issues in JavaScript web pages."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>適用於網頁的 Application Insights
了解 hello 效能和網頁或應用程式的使用方式。 如果您將加入[Application Insights](app-insights-overview.md) tooyour 頁面指令碼，取得頁面載入和 AJAX 呼叫、 計數和瀏覽器例外狀況和 AJAX 失敗，以及使用者和工作階段計數的詳細資料的執行時間。 這些項目可以依據頁面、用戶端作業系統和瀏覽器版本、地區位置和其他維度分割。 您可以對失敗計數或緩慢頁面載入設定警示。 並在 JavaScript 程式碼中插入追蹤呼叫，您可以追蹤 hello 的網頁應用程式的不同功能使用方式。

Application Insights 可以使用於任何網頁 - 您剛剛新增 JavaScript 的簡短片段。 如果您的 Web 服務是 [Java](app-insights-java-get-started.md) 或 [ASP.NET](app-insights-asp-net.md)，您可以整合來自您的伺服器和用戶端的遙測。

![在 portal.azure.com 中，開啟您的應用程式資源，然後按一下 [瀏覽器]](./media/app-insights-javascript/03.png)

您需要訂用帳戶[Microsoft Azure](https://azure.com)。 如果您的小組有組織的訂用帳戶，詢問您 Microsoft 帳戶 tooit hello 擁有者 tooadd。 開發和小規模的使用不需要任何成本。

## <a name="set-up-application-insights-for-your-web-page"></a>為您的網頁設定 Application Insights
加入 hello 載入器程式碼片段 tooyour 網頁，如下所示。

### <a name="open-or-create-application-insights-resource"></a>開啟或建立 Application Insights 資源
hello Application Insights 資源是其中會顯示網頁的效能和使用方式的相關資料。 

登入 [Azure 入口網站](https://portal.azure.com)。

如果您已經設定 hello 伺服器端應用程式的監視，您已經擁有的資源：

![選擇 [瀏覽]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-find.png)

如果您沒有資源，請建立資源：

![選擇 [新增]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-create.png)

*已經有問題了嗎？* [建立資源的詳細資訊](app-insights-create-new-resource.md)訂用帳戶。

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>新增 hello SDK 指令碼 tooyour 應用程式或 web 網頁
在 快速入門中，取得網頁 hello 指令碼：

![在您的應用程式概觀刀鋒視窗中，選擇 [快速啟動]，取得程式碼 toomonitor 我的網頁。 複製 hello 指令碼。](./media/app-insights-javascript/02-monitor-web-page.png)

插入 hello 指令碼之前 hello`</head>`標記要 tootrack 的每一頁。 如果您的網站有主版頁面，您可以那里出 hello 指令碼。 例如：

* 在 ASP.NET MVC 專案中，可放在 `View\Shared\_Layout.cshtml`
* 在 SharePoint 網站上 hello [控制台] 中，開啟[站台設定 / 主版頁面](app-insights-sharepoint.md)。

hello 指令碼包含 hello 將導向 hello 資料 tooyour Application Insights 資源的檢測金鑰。 

([Hello 指令碼的所需的深入說明。](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(如果您使用的是已知網頁架構，請在 Application Insights 配接器附近尋找。例如，有 [AngularJS 模組](http://ngmodules.org/modules/angular-appinsights)。)*

## <a name="detailed-configuration"></a>詳細組態
您可以設定數種 [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) ，但是在大部分情況下，您應該不需要這麼做。 比方說，您可以停用或限制 hello Ajax 呼叫每個頁面檢視 （tooreduce 流量） 報告的數目。 或者，您可以設定偵錯模式 toohave 遙測逐一快速 hello 管線，而不在批次。

tooset 這些參數中，尋找在 hello 程式碼片段中，這一行，並在它之後新增多個以逗號分隔的項目：

    })({
      instrumentationKey: "..."
      // Insert here
    });

hello[可用參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)包括：

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>執行您的應用程式
執行您 web 應用程式，請使用它時 toogenerate 遙測，並稍候幾秒鐘的時間。 您可以執行使用 hello **F5**您的開發電腦上的主要或將它發行，並且讓使用者開始處理它。

如果您想 toocheck hello 遙測 web 應用程式正在傳送 tooApplication 深入資訊，請使用您的瀏覽器偵錯工具 (**F12**許多瀏覽器上)。 資料會傳送 toodc.services.visualstudio.com。

## <a name="explore-your-browser-performance-data"></a>探索瀏覽器效能資料
從使用者的瀏覽器開啟 hello 瀏覽器刀鋒視窗 tooshow 彙總的效能資料。

![在 portal.azure.com 中，開啟您的應用程式資源然後按一下 [設定]、[瀏覽器]。](./media/app-insights-javascript/03.png)

*仍沒有資料？按一下**重新整理**hello 頁面頂端的 hello。仍然沒有嗎？請參閱[疑難排解](app-insights-troubleshoot-faq.md)。*

hello 瀏覽器刀鋒視窗是[計量瀏覽器刀鋒視窗](app-insights-metrics-explorer.md)預設篩選器與圖表選項。 如果您想要並儲存為我的最愛的 hello 結果，您可以編輯 hello 時間範圍、 篩選和圖表組態。 按一下**還原成預設值**tooget 後 toohello 原始刀鋒視窗中設定。

## <a name="page-load-performance"></a>頁面載入效能
在 hello top 將不分割的頁面載入時間圖表。 hello 總 hello 圖表高度表示從您的應用程式使用者的瀏覽器中的 hello 的平均時間 tooload 和顯示頁面。 hello 時間的測量從 hello 瀏覽器傳送 hello 初始 HTTP 要求，直到所有同步已處理的事件，包括版面配置和執行指令碼的負載。 不包含例如從 AJAX 呼叫載入 Web 組件的非同步工作。

hello 圖表 hello 總頁面載入時間分成 hello [W3C 所定義的標準時間](http://www.w3.org/TR/navigation-timing/#processing-model)。 

![](./media/app-insights-javascript/08-client-split.png)

請注意該 hello*網路連接*時間通常是比您所料，因為它是從 hello 瀏覽器 toohello 伺服器的所有要求的平均值。 許多個別的要求有連接時間為 0，因為已經有使用中連接 toohello 伺服器。

### <a name="slow-loading"></a>載入緩慢？
頁面載入緩慢是您的使用者不滿的主要來源。 如果 hello 圖表表示慢速網頁載入時，很容易 toodo 一些診斷研究。

hello 圖表可顯示應用程式中的所有載入頁面的 hello 平均值。 toosee 如果 hello 問題侷 tooparticular 頁面，進一步向下 hello 刀鋒視窗的外觀，其中有是區隔的方格頁面 URL:

![](./media/app-insights-javascript/09-page-perf.png)

請注意 hello 頁面檢視計數和標準差。 如果非常低 hello 頁面計數，然後 hello 問題不會影響使用者很多。 高標準差 （比較 toohello 平均本身），表示大量的個別度量之間的變化。

**放大某個 URL 和整頁檢視。** 按一下任何頁面名稱 toosee 刀鋒視窗中的瀏覽器圖表篩選只 toothat URL;然後執行個體上的頁面檢視。

![](./media/app-insights-javascript/35.png)

按一下`...`的事件屬性的完整清單，或檢查 hello Ajax 呼叫和相關的事件。 速度較慢的 Ajax 呼叫影響 hello 整體頁面載入時間，如果不同步。 相關的事件包括 hello 的伺服器要求相同的 URL （如果您已設定 web 伺服器上的 Application Insights）。

**經過一段時間的網頁效能。** 回在 hello 瀏覽器刀鋒視窗中，變更 hello 網頁檢視載入時間格線行圖表 toosee 在特定時間尖峰一樣：

![按一下 hello hello 方格標頭，然後選取新的圖表類型](./media/app-insights-javascript/10-page-perf-area.png)

**依據其他維度來分段。** 或許您的網頁會慢 tooload 上特定瀏覽器、 用戶端作業系統或使用者的位置？ 將新的圖表和試驗 hello **Group by**維度。

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>AJAX 效能
請確定您的網頁中的任何 AJAX 呼叫執行狀況良好。 這些通常是頁面的您使用的 toofill 部分以非同步的方式。 Hello 整體頁面可能會載入迅速，雖然您的使用者可能被搖頭由盯著空白 web 組件，等候中的資料 tooappear。

AJAX 呼叫從您網頁會顯示 hello 瀏覽器刀鋒視窗上，做為相依性。

有 hello 的 hello 刀鋒視窗的上半部中的摘要圖表：

![](./media/app-insights-javascript/31.png)

在下方有詳細方格：

![](./media/app-insights-javascript/33.png)

按一下任何資料列以取得特定詳細資料。

> [!NOTE]
> 如果您刪除 hello hello 刀鋒視窗上的瀏覽器篩選時，伺服器和 AJAX 相依性會包含在這些圖表中。 按一下 還原成預設值 tooreconfigure hello 篩選器。
> 
> 

**執行失敗的 Ajax 呼叫 toodrill**向 toohello 相依性失敗方格中，捲動，然後按一下資料列的 toosee 特定執行個體。

![](./media/app-insights-javascript/37.png)


按一下`...`Ajax 呼叫 hello 完整遙測。

### <a name="no-ajax-calls-reported"></a>未報告任何 Ajax 呼叫？
Ajax 呼叫包含從您網頁的 hello 指令碼進行的任何 HTTP/HTTPS 呼叫。 如果您沒有看到這些報告，請檢查該 hello 程式碼片段不會設定 hello`disableAjaxTracking`或`maxAjaxCallsPerView`[參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。

## <a name="browser-exceptions"></a>瀏覽器例外狀況
在 hello 瀏覽器刀鋒視窗中，沒有例外狀況的摘要圖表，以及一個例外狀況類型的進一步向下 hello 刀鋒視窗中的方格。

![](./media/app-insights-javascript/39.png)

如果看不到瀏覽器例外狀況的報告，請檢查該 hello 程式碼片段不會設定 hello `disableExceptionTracking` [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。

## <a name="inspect-individual-page-view-events"></a>檢查個別的頁面檢視事件

頁面檢視遙測資料一般是由 Application Insights 進行分析，而您只會看見以所有使用者為單位平均計算的累積報告。 然而在偵錯時，您也可以查看個別的頁面檢視事件。

在 hello 診斷搜尋刀鋒視窗中，設定篩選 tooPage 檢視。

![](./media/app-insights-javascript/12-search-pages.png)

選取任何事件 toosee 更多詳細資料。 在 [hello 詳細資料] 頁面上，按一下"…"toosee 更多詳細資料。

> [!NOTE]
> 如果您使用[搜尋](app-insights-diagnostic-search.md)，通知您有全字拼寫須相符 toomatch: 「 關於 」 和 「 記載"不符合 「 關於 」。
> 
> 

您也可以使用 hello 強大[記錄分析查詢語言](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table)toosearch 頁面檢視。

### <a name="page-view-properties"></a>頁面檢視屬性
* **頁面檢視持續時間** 
  
  * 根據預設，hello 次採用 tooload hello 頁面上，從用戶端要求 toofull 負載 （包括但不包括非同步工作，例如 Ajax 呼叫的輔助檔案）。 
  * 如果您設定`overridePageViewDuration`在 hello[頁面設定](#detailed-configuration)，第一次 hello hello 的用戶端要求 tooexecution 間隔`trackPageView`。 如果您可以從其一般位置移動 trackPageView hello 初始化 hello 指令碼之後，它會反映不同的值。
  * 如果`overridePageViewDuration`組和持續時間在 hello 提供引數則是`trackPageView()`呼叫，則會改為使用 hello 引數值。 

## <a name="custom-page-counts"></a>自訂頁面計數
根據預設，頁面計數，就會發生每個新的頁面載入 hello 用戶端瀏覽器的時間。  但是，您可能想 toocount 額外的頁面檢視。 例如，頁面可能會顯示其內容索引標籤中，且想 toocount 頁面時 hello 使用者切換索引標籤。 或 hello 頁面中的 JavaScript 程式碼可能會載入新的內容，而不需要變更 hello 瀏覽器的 URL。

Hello 適當點，用戶端程式碼中插入 JavaScript 呼叫像這樣：

    appInsights.trackPageView(myPageName);

hello 頁面名稱只能包含的 hello 相同字元做為 URL，但任何項目之後"#"或"？"會被忽略。

## <a name="usage-tracking"></a>使用情況追蹤
想出您的使用者利用您的應用程式執行 toofind 嗎？

* [深入了解使用情況追蹤](app-insights-web-track-usage.md)
* [深入了解自訂事件和計量 API](app-insights-api-custom-events-metrics.md)。

## <a name="video"></a> 影片


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> 後續步驟
* [追蹤流量](app-insights-web-track-usage.md)
* [自訂事件和計量](app-insights-api-custom-events-metrics.md)
* [Build-measure-learn](app-insights-web-track-usage.md)

