---
title: "aaaUsing 分析-Azure Application Insights 的 hello 功能強大的搜尋工具 |Microsoft 文件"
description: "使用 hello 的 Application Insights hello 功能強大的診斷搜尋工具，分析。 "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>使用 Application Insights 中的分析
[分析](app-insights-analytics.md)是功能強大的搜尋功能 hello [Application Insights](app-insights-overview.md)。 這些分頁說明 Log Analytics 查詢語言。

* **[請觀看 hello 簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。
* **[測試模擬資料的磁碟機分析](https://analytics.applicationinsights.io/demo)**如果您的應用程式未尚未傳送資料 tooApplication 深入資訊。

## <a name="open-analytics"></a>開啟分析
在 Application Insights 中，從您的應用程式的首頁資源，按一下 [分析]。

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-using/001.png)

hello 內嵌教學課程，可讓您可以執行一些的概念。

[這裡有更廣泛的教學課程](app-insights-analytics-tour.md)。

## <a name="query-your-telemetry"></a>查詢您的遙測
### <a name="write-a-query"></a>撰寫查詢
![結構描述顯示](./media/app-insights-analytics-using/150.png)

開頭為 hello 名稱列出 hello 左側的 hello 資料表的所有 (或 hello[範圍](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html)或[union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html)運算子)。 使用`|`的管線 toocreate[運算子](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html)。 

IntelliSense 會提示您 hello 運算子與 hello 運算式項目，您可以使用。 按一下資訊圖示，hello （或按 CTRL + 空格鍵） tooget 更長的描述和範例如何 toouse 每個項目。

請參閱 hello[分析語言教學課程](app-insights-analytics-tour.md)和[語言參考](app-insights-analytics-reference.md)。

### <a name="run-a-query"></a>執行查詢
![執行查詢](./media/app-insights-analytics-using/130.png)

1. 您可以在查詢中使用單一分行符號。
2. 將內部或結尾 hello hello 查詢想 toorun hello 游標。
3. 請檢查您的查詢 hello 時間範圍。 (您可以變更它，或是在查詢中包含您自己的 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 子句來覆寫它。)
3. 按一下 Go toorun hello 查詢。
4. 請勿在查詢中放置空白行。 您可以用空白行來分隔一個查詢索引標籤中的數個查詢，讓它們保持分離狀態。 具有 hello 游標 hello 查詢執行。

### <a name="save-a-query"></a>儲存查詢
![儲存查詢](./media/app-insights-analytics-using/140.png)

1. 儲存 hello 目前的查詢檔案。
2. 開啟已儲存的查詢檔案。
3. 建立新的查詢檔案。

## <a name="see-hello-details"></a>請參閱 hello 詳細資料
展開任何資料列中 hello 結果 toosee 其完整的屬性清單。 您可以進一步展開任何屬性的結構化的值-例如，自訂維度或 hello 堆疊中例外狀況的清單。

![展開資料列](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>排列 hello 結果
您可以排序、 篩選、 重新編頁，以及 hello 從您的查詢傳回的結果分組。

> [!NOTE]
> 排序、 分組和篩選 hello 瀏覽器中不會重新執行您的查詢。 它們只重新排列 hello 由最後一個查詢所傳回的結果。 
> 
> tooperform hello 伺服器，然後傳回 hello 結果，才能處理這些工作撰寫查詢以 hello[排序](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)，[摘要](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html)和[其中](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)運算子。
> 
> 

挑選 hello 資料行，就如同 toosee，將資料行的標頭 toorearrange，以及調整大小資料行拖曳框線。

![排列資料行](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>排序和篩選項目
按一下 hello 標頭的資料行排序您的結果。 再次按一下 toosort hello 另一種方式，並按一下第三次 toorevert toohello 原始順序由您的查詢。

使用 hello 篩選圖示 toonarrow 您的搜尋。

![排序和篩選資料行](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>將項目分組
toosort 使用一個以上的資料行群組。 第一次啟用它，並接著將資料行標頭拖曳到 hello hello 資料表上方的空間。

![群組](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>遺漏某些結果？

如果您認為您看不到您所預期的所有 hello 結果，有幾個可能的原因。

* **時間範圍篩選**。 根據預設，您只會看到結果 hello 過去 24 小時。 沒有限制的結果與 hello 來源資料表所擷取的 hello 範圍自動篩選。 

    不過，您可以變更 hello 時間範圍篩選器使用 hello 下拉式選單。

    您可以取代 hello 自動範圍包括您自己或者[`where  ... timestamp ...`子句](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)到您的查詢。 例如：

    `requests | where timestamp > ago('2d')`

* **結果限制**。 沒有限制，大約 10 個 k 上的資料列 hello hello 入口網站所傳回的結果。 如果超出 hello 限制會顯示警告。 如果發生這種情況，排序結果 hello 資料表中的不會永遠顯示您所有 hello 實際第一個或最後的結果。 

    它是很好的作法 tooavoid 達到 hello 限制。 使用 hello 時間範圍篩選器，或使用運算子，例如：

  * [top 100 by timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(想要一萬個以上的資料列嗎？ 請考慮改用[連續匯出](app-insights-export-telemetry.md)。 「分析」是設計來進行分析的，不是用來擷取未經處理的資料。)

## <a name="diagrams"></a>圖表
選取您想要的圖表類型 hello:

![選取圖表類型](./media/app-insights-analytics-using/230.png)

如果您有數個資料行的 hello 正確型別時，您可以選擇 hello x 和 y 軸，並依維度 toosplit hello 結果的資料行。

根據預設，結果一開始會顯示為資料表，並手動選取 hello 圖表。 但是您可以使用 hello[呈現指示詞](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html)結尾 hello 查詢 tooselect 圖表。

### <a name="analytics-diagnostics"></a>分析診斷


在 timechart，如果沒有突然出現尖峰或步驟，在您的資料，您可能看到 hello 列上的反白顯示的點。 這表示分析診斷已識別的篩選出 hello 突然變更的屬性組合。 按一下 hello 點 tooget hello 篩選和 toosee hello 篩選的版本的其他詳細資料。 這可協助您識別哪些造成的 hello 變更。 

[深入了解分析診斷](app-insights-analytics-diagnostics.md)


![分析診斷](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Pin toodashboard
您可以釘選的圖表或資料表 tooone 您[共用儀表板](app-insights-dashboards.md)-只要按一下 hello 的 pin。 (您可能需要[升級您的應用程式的定價封裝](app-insights-pricing.md)tooturn 這項功能。) 

![按一下 hello 的 pin](./media/app-insights-analytics-using/pin-01.png)

這表示，當您一起讓您監視 hello 效能或使用 web 服務的儀表板 toohelp，您可以包含相當複雜的分析與 hello 一起其他度量資訊。 

如果有四個或更少的資料行，您可以釘選的資料表 toohello 儀表板。 只有 hello 前七個資料列會顯示。

### <a name="dashboard-refresh"></a>儀表板重新整理
hello 圖表釘選 toohello 儀表板會重新執行 hello 查詢約每小時自動重新整理。 您也可以按一下 hello 重新整理 按鈕。

### <a name="automatic-simplifications"></a>自動簡化

當您將其釘選 tooa 儀表板，某些簡單化會套用的 tooa 圖表。

**時間限制：**查詢會自動限制僅的 toohello 過去 14 天。 hello 效果是 hello 相同時，如果您的查詢包含`where timestamp > ago(14d)`。

**分類收納計數限制：**如果顯示圖表具有許多不連續分類收納 （通常是橫條圖），較少擴展的紙匣會自動分組到單一 「 其他 」 的 hello 分類收納。 例如，下列查詢︰

    requests | summarize count_search = count() by client_CountryOrRegion

在分析中看起來像這樣︰

![具有長尾的圖表](./media/app-insights-analytics-using/pin-07.png)

但是，當您釘選它 tooa 儀表板，它看起來像這樣：

![具有有限長條的圖表](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>匯出 tooExcel
執行查詢之後，您可以下載 .csv 檔案。 按一下 [匯出] > [Excel]。

## <a name="export-toopower-bi"></a>匯出 tooPower BI
Hello 資料指標放在查詢中，然後選擇 **匯出時，Power BI**。

![從分析 tooPower BI 匯出](./media/app-insights-analytics-using/240.png)

您在 Power BI 中執行 hello 查詢。 您可以設定它 toorefresh 的排程。

您可以使用 Power BI 來建立儀表板，將從各種來源的資料結合在一起。

[深入了解匯出 tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>深層連結

取得連結底下**匯出，共用連結**tooanother 使用者，可以傳送。 假設 hello 使用者已[存取 tooyour 資源群組](app-insights-resources-roles-access-control.md)，hello 查詢會在 hello 分析 UI 中開啟。

(在 hello 連結 hello 查詢文字會出現在 「？ q ="、 gzip 壓縮和 base 64 編碼。 您可以撰寫程式碼 toogenerate 深層連結，您必須提供 toousers。 不過，hello 建議的方式 toorun 分析從程式碼是使用 hello [REST API](https://dev.applicationinsights.io/)。)


## <a name="automation"></a>自動化

使用 hello[資料存取 REST API](https://dev.applicationinsights.io/) toorun 分析查詢。 [例如](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (使用 PowerShell)：

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

不同於 hello 分析 UI，hello REST API 不會自動新增的任何時間戳記限制 tooyour 查詢。 請記住 tooadd 自己 where 子句，tooavoid 取得龐大的回覆。



## <a name="import-data"></a>匯入資料

您可以從 CSV 檔案匯入資料。 通常的使用方式為 tooimport 靜態資料，您可以從您的遙測聯結的資料表。 

比方說，如果您遙測中發現已驗證的使用者別名或模糊化的識別碼，您可以匯入別名 tooreal 名稱對應的資料表。 Hello 要求遙測執行聯結，您可以在 hello 分析報表中的實際名稱來識別使用者。

### <a name="define-your-data-schema"></a>定義資料結構描述

1. 按一下 [設定] \(在左上方)，然後按一下 [資料來源]。 
2. 加入資料來源，hello 指示。 您要求 toosupply hello 資料，應該包含至少 10 個資料列的範例。 然後，您會更正 hello 結構描述。

這會定義資料來源，然後您可以使用 tooimport 個別資料表。

### <a name="import-a-table"></a>匯入資料表

1. 從 hello 清單中，開啟您的資料來源定義。
2. 按一下 [上傳]，並遵循 hello 指示 tooupload hello 資料表。 這項作業包括呼叫 tooa REST API，因此容易 tooautomate。 

您的資料表現在已可在「分析」查詢中使用。 它會顯示在「分析」中 

### <a name="use-hello-table"></a>使用 hello 資料表

假設您的資料來源定義稱為 `usermap`，而它包含 `realName` 和 `user_AuthenticatedId` 這兩個欄位。 hello`requests`資料表也有一個名為變數`user_AuthenticatedId`，因此很容易 toojoin 它們：

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
hello 產生資料表的要求有額外的資料行， `realName`。

### <a name="import-from-logstash"></a>從 LogStash 匯入

如果您使用[LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html)，您可以使用分析 tooquery 記錄。 使用 hello[管道到分析資料的外掛程式](https://github.com/Microsoft/logstash-output-application-insights)。 

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

