---
title: "aaaUsing Azure Insights 中搜尋應用程式 |Microsoft 文件"
description: "搜尋和篩選 Web 應用程式傳送的原始遙測。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>在 Application Insights 中使用搜尋
搜尋是一項功能[Application Insights](app-insights-overview.md)您使用 toofind 和瀏覽個別的遙測項目，例如網頁檢視，例外狀況，或 web 要求。 而您可以檢視所編寫的記錄追蹤和事件。

(若要對您的資料執行更複雜的查詢，請使用[分析](app-insights-analytics-tour.md)。)

## <a name="where-do-you-see-search"></a>「搜尋」在哪裡？
### <a name="in-hello-azure-portal"></a>在 hello Azure 入口網站
您可以從您的應用程式的 hello Application Insights 概觀刀鋒視窗的明確開啟診斷搜尋：

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

在您逐一點選某些圖表和格線項目時，它也會開啟。 在此情況下，其會預先設定篩選 toofocus hello 您選取的項目類型上。 

例如，在上 hello 概觀刀鋒視窗中，沒有橫條圖的項目分類的回應時間的要求。 按一下所有效能範圍 toosee 一份個別要求的回應時間範圍：

![點選要求效能](./media/app-insights-diagnostic-search/07-open-from-filters.png)

hello 診斷搜尋的主要內文是清單遙測項目-伺服器要求的頁面上檢視、 您撰寫的自訂事件等等。 在 hello hello 清單的頂端是摘要圖表，顯示經過一段時間的事件計數。

按一下 重新整理 tooget 新事件。

### <a name="in-visual-studio"></a>在 Visual Studio 中

在 Visual Studio 中，也有 [Application Insights 搜尋] 視窗。 它是最適合用於顯示您要偵錯 hello 應用程式所產生的遙測事件。 但是，它也可以顯示 hello 收集在 hello Azure 入口網站應用程式已發行的事件。

開啟 Visual Studio 中的 hello 搜尋視窗：

![Visual Studio 開啟 Application Insights 搜尋](./media/app-insights-diagnostic-search/32.png)

hello 搜尋視窗具有功能類似 toohello web 入口網站：

![Visual Studio Application Insights 搜尋視窗](./media/app-insights-diagnostic-search/34.png)

當您開啟的要求或頁面檢視使用 hello 追蹤作業 索引標籤。 '作業' 是 tooa 單一要求或頁面檢視相關聯的事件序列。 例如，相依性呼叫、例外狀況、追蹤記錄檔和自訂事件可能都是單一作業的一部分。 hello 追蹤作業索引標籤會顯示以圖形方式 hello 時間控制，以及關聯 toohello 要求或網頁檢視中的這些事件的持續時間。 

## <a name="inspect-individual-items"></a>檢查個別項目
選取任何遙測項目 toosee 索引鍵欄位和相關項目。 如果您想 toosee hello 一組完整的欄位，按一下"…"。 

![按一下 [新增工作項目、 編輯 hello 欄位，然後按一下確定]。](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>篩選事件類型
開啟 hello 篩選刀鋒視窗，然後選擇 hello 事件類型與您想 toosee。 (如果更新版本中，您會想 toorestore hello 篩選開啟 hello 刀鋒視窗中，按一下 重設)。

![選擇篩選器並選取遙測類型](./media/app-insights-diagnostic-search/02-filter-req.png)

hello 事件類型為：

* **追蹤** - [診斷記錄](app-insights-asp-net-trace-logs.md)，包括 TrackTrace、log4Net、NLog 和 System.Diagnostic.Trace 呼叫。
* **要求** - 伺服器應用程式收到的 HTTP 要求，包括頁面、指令碼、影像、樣式檔案和資料。 這些事件是使用的 toocreate hello 要求和回應概觀圖表。
* **頁面檢視** - [hello web 用戶端傳送遙測](app-insights-javascript.md)，使用 toocreate 頁面檢視報表。 
* **自訂事件**-如果您呼叫 tooTrackEvent() 依照順序插入太[監視使用量](app-insights-api-custom-events-metrics.md)，這裡搜尋。
* **例外狀況**-無法攔截[hello 伺服器中的例外狀況](app-insights-asp-net-exceptions.md)，以及您所使用之 trackexception （） 記錄。
* **相依性** - [從伺服器應用程式呼叫](app-insights-asp-net-dependencies.md)tooother 服務 REST Api 或資料庫，例如，從 AJAX 呼叫您[用戶端程式碼](app-insights-javascript.md)。
* **可用性** - [可用性測試](app-insights-monitor-web-app-availability.md)的結果。

## <a name="filter-on-property-values"></a>依據屬性值篩選
您可以篩選 hello 及其屬性的值上的事件。 hello 可用的屬性取決於您選取的 hello 事件類型。 

例如，找出具有特定回應代碼的要求。 

![展開屬性並選擇值](./media/app-insights-diagnostic-search/03-response500.png)

選擇任何特定屬性的值具有相同效果與選擇的所有值的 hello。 這樣會關掉該屬性的篩選功能。

### <a name="narrow-your-search"></a>縮小搜尋
請注意該 hello 計算 toohello hello 篩選值的右邊顯示多少相符的項目有 hello 目前的篩選集內。 

在此範例中，會清除該 hello 'Rpt/員工' 要求會導致大部分的 hello '500' 錯誤：

![展開屬性並選擇值](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>尋找活動與 hello 相同的屬性
尋找所有 hello 的項目 hello 相同屬性值：

![以滑鼠右鍵按一下屬性](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>搜尋 hello 資料

> [!NOTE]
> toowrite 更複雜的查詢，開啟[**分析**](app-insights-analytics-tour.md)從 hello hello 搜尋刀鋒視窗的頂端。
> 

您可以搜尋中任何 hello 屬性值的詞彙。 如果您已編寫具有屬性值的[自訂事件](app-insights-api-custom-events-metrics.md)，這特別實用。 

您可能想的 tooset 時間範圍為較短的範圍內的搜尋速度較快。 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

請搜尋完整單字，而不是子字串。 使用引號 tooenclose 特殊字元。

| 字串 | 這樣「找不到」 | 這樣找得到 |
| --- | --- | --- |
| HomeController.About |home<br/>controller<br/>out | homecontroller<br/>about<br/>"homecontroller.about"|
|美國|Uni<br/>ted|united<br/>states<br/>united AND states<br/>"united states"

以下是您可以使用 hello 搜尋運算式：

| 範例查詢 | 效果 |
| --- | --- |
| `apple` |尋找其欄位包含 hello 單字"apple"hello 時間範圍內的所有事件 |
| `apple AND banana` |尋找同時含有這兩個字的事件。 請使用大寫 "AND"，而不是 "and"。 |
| `apple OR banana`<br/>`apple banana` |尋找含有任一單字的事件。 請使用 "OR"，而不是 "or"。<br/>簡短格式。 |
| `apple NOT banana` |尋找包含一個字，但不是 hello 其他的事件。 |



## <a name="sampling"></a>取樣
如果您的應用程式會產生大量的遙測 (而且您正使用 ASP.NET 的 SDK 版本 2.0.0-beta3 hello 或更新版本)，hello 調整取樣模組會自動將所傳送的 toohello 入口網站傳送事件代表分數 hello 磁碟區。 不過，事件是相關的 toohello 相同的要求會選取或取消選取此選項為群組，如此您可以瀏覽相關的事件之間。 

[了解取樣](app-insights-sampling.md)。



## <a name="create-work-item"></a>建立工作項目
您可以建立錯誤 GitHub 或 Visual Studio Team Services 中的 hello 詳細資料，從任何遙測項目。 

![按一下 [新增工作項目、 編輯 hello 欄位，然後按一下確定]。](./media/app-insights-diagnostic-search/42.png)

hello 第一次，這樣做，系統會要求您 tooconfigure 連結 tooyour Team Services 帳戶和專案。

![填入 hello URL，您的 Team Services 伺服器與 hello 專案名稱，並按一下 授權](./media/app-insights-diagnostic-search/41.png)

（您也可以設定 hello 連結 hello 工作項目 刀鋒視窗。）

## <a name="save-your-search"></a>儲存搜尋
當您已設定您想要所有 hello 篩選器時，您可以儲存為我的最愛的 hello 搜尋。 如果您使用組織帳戶，您可以選擇是否 tooshare 它與其他小組成員。

![按一下 我的最愛，設定 hello 名稱，按一下 儲存](./media/app-insights-diagnostic-search/08-favorite-save.png)

同樣地，toosee hello 搜尋**移 toohello 概觀刀鋒視窗**並開啟 [我的最愛]:

![我的最愛磚](./media/app-insights-diagnostic-search/09-favorite-get.png)

如果您儲存與相對的時間範圍，hello 重新開啟刀鋒視窗中會有 hello 最新的資料。 如果您儲存在絕對時間範圍內，您會看見 hello 每次相同的資料。 （如果 'Relative' 時無法使用您想要 toosave 我的最愛，hello 標題中按一下 時間範圍，將未自訂範圍的時間範圍）。

## <a name="send-more-telemetry-tooapplication-insights"></a>傳送多個遙測 tooApplication Insights
在 加入 Application Insights SDK 所傳送的方塊外遙測 toohello，您可以：

* 在 [.NET](app-insights-asp-net-trace-logs.md) 或 [Java](app-insights-java-trace-logs.md) 中，從您最喜愛的紀錄架構擷取記錄追蹤。 這表示您可以搜尋您的記錄追蹤，並將它們與頁面檢視、例外狀況和其他事件相互關聯。 
* [撰寫程式碼](app-insights-api-custom-events-metrics.md)toosend 自訂事件、 頁面檢視和例外狀況。 

[了解 toosend 記錄的方式，以及自訂遙測 tooApplication Insights](app-insights-asp-net-trace-logs.md)。

## <a name="questions"></a>問與答
### <a name="limits"></a>保留多少資料？

請參閱 hello[限制摘要](app-insights-pricing.md#limits-summary)。

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>我如何查看我的伺服器要求中的 POST 資料？
我們不會自動記錄 hello 張貼資料，但是您可以使用[TrackTrace 或記錄檔呼叫](app-insights-asp-net-trace-logs.md)。 將 hello 張貼資料放在 hello 訊息參數。 您無法篩選 hello 中的 hello 訊息的相同方式來篩選屬性，但 hello 大小限制較長。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>接續步驟
* [在分析中撰寫複雜的查詢](app-insights-analytics-tour.md)
* [傳送記錄檔和自訂遙測 tooApplication Insights](app-insights-asp-net-trace-logs.md)
* [設定可用性和回應性測試](app-insights-monitor-web-app-availability.md)
* [疑難排解](app-insights-troubleshoot-faq.md)
