---
title: "透過分析 Azure Application Insights 中的 aaaA 教學課程 |Microsoft 文件"
description: "簡短的分析，hello 功能強大的搜尋工具的 Application Insights 中的 hello 主要查詢的範例。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a>Application Insights 中分析的教學課程
[分析](app-insights-analytics.md)是功能強大的搜尋功能 hello [Application Insights](app-insights-overview.md)。 這些分頁說明 Log Analytics 查詢語言。

* **[請觀看 hello 簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。
* **[測試模擬資料的磁碟機分析](https://analytics.applicationinsights.io/demo)**如果您的應用程式未尚未傳送資料 tooApplication 深入資訊。
* **[SQL 使用者 ' 速查表](https://aka.ms/sql-analytics)**轉譯 hello 最常見慣用語。

讓我們逐步啟動一些基本查詢 tooget。

## <a name="connect-tooyour-application-insights-data"></a>Tooyour Application Insights 資料連接
在 Application Insights 中，從 app 的 [概觀刀鋒視窗](app-insights-dashboards.md) 開啟 [分析]：

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)：顯示 n 個資料列
記錄使用者作業的資料點 (通常是 Web 應用程式收到的 HTTP 要求) 會儲存在名為 `requests`的資料表。 每個資料列是來自應用程式中的 hello Application Insights SDK 遙測資料點。

讓我們開始檢查 hello 資料表的一些範例資料列：

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Hello 游標處 hello 陳述式會先置於您按一下 移至。 您可以將陳述式分割成多行，但不要在單一陳述式中放置空白行。 空白的行是很方便的方式 tookeep 數個分隔 hello 視窗中的查詢。
>
>

選擇資料行、加以拖曳，依照資料行分組，以及進行篩選︰

![按一下結果右上方的資料行選取範圍](./media/app-insights-analytics-tour/030.png)

展開任何項目 toosee hello 詳細資料：

![選擇 [資料表]，並使用 [設定資料行]](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> 按一下資料行 toore 順序 hello 可用的結果 hello 網頁瀏覽器中的 hello 開頭。 但是請注意，對於大型結果集，hello 的資料列下載的 toohello 瀏覽器所數目有限。 排序這種方式不一定會顯示您 hello 實際的最高或最低的項目。 toosort 項目可靠地使用 hello`top`或`sort`運算子。
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 和 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`是有用的 tooget 快速範例的結果，但它會顯示 hello 資料表的資料列中沒有特定順序。 tooget 已排序的檢視中，使用`top`（如需範例中） 或`sort`（透過 hello 整個資料表）。

顯示 hello 前 n 個資料列，依特定的資料行：

```AIQL

    requests | top 10 by timestamp desc
```

* 語法︰大部分運算子都有關鍵字參數 (例如 `by`)。
* `desc` = 遞減順序，`asc` = 遞增。

![](./media/app-insights-analytics-tour/260.png)

`top...` 是 `sort ... | take...` 比較有效率的說法。 我們可以撰寫︰

```AIQL

    requests | sort by timestamp desc | take 10
```

hello 結果會是 hello 相同，但它會執行位元速度變慢。 (您也可以撰寫 `order`，這是 `sort` 的別名)。

hello hello 資料表檢視表中的資料行標頭也可以使用的 toosort hello 結果囉 」 畫面上。 當然，如果您曾經使用，但是`take`或`top`tooretrieve 部分的資料表，將只重新排序 hello 記錄了擷取。

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)︰篩選條件

讓我們看一下傳回特定結果碼的要求︰

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

hello`where`運算子會採用布林運算式。 以下是其相關的一些重點︰

* `and`、`or`：布林運算子
* `==`、`<>`、`!=`︰等於和不等於
* `=~`、`!~`︰不區分大小寫的字串等於和不等於。 有更多的字串比較運算子。

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>收到 hello 右類型
尋找失敗的要求︰

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>時間

根據預設，您的查詢會很限制的 toohello 過去 24 小時。 但您可以變更此範圍︰

![](./media/app-insights-analytics-tour/change-time-range.png)

撰寫提及的任何查詢，以覆寫 hello 時間範圍`timestamp`where 子句中。 例如：

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

hello 時間範圍功能是對等 tooa 'where' 子句插入之後的其中一個 hello 來源資料表的每個提及。

`ago(3d)` 表示「三天前」。 其他時間單位包括小時 (`2h`、`2.5h`)、分鐘 (`25m`) 和秒 (`10s`)。

其他範例︰

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

[日期和時間參考](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)。


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)：選取、重新命名和計算資料行
使用[ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick 出只要您想要的 hello 資料行：

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

您也可以將資料行重新命名並定義新的資料行︰

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![結果](./media/app-insights-analytics-tour/270.png)

* 如果資料行名稱是以括號括起來 (如下所示)，就可以包含空格或符號︰`['...']` 或 `["..."]`
* `%`為 hello 一般模數運算子。
* `1d` (這是數字 1，再加上 'd') 是一個時間範圍常值，表示一天。 以下是其他一些時間範圍常值︰`12h`、`30m`、`10s`、`0.01s`。
* `floor`(別名`bin`) 將值四捨五入為最接近您所提供的 hello 基底值的倍數 toohello 關閉。 因此`floor(aTime, 1s)`捨入 toohello 最接近的第二個關閉的時間。

運算式可以包含所有 hello 一般運算子 (`+`， `-`，...)，而且沒有有用的函式的範圍。

## <a name="extend"></a>Extend
如果您只想 tooadd 現有的資料行 toohello，使用[ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

使用[ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html)較不繁複比[ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)如果您想 tookeep 所有 hello 現有的資料行。

### <a name="convert-toolocal-time"></a>將 toolocal 時間轉換

時間戳記一律是 UTC 格式。 因此如果您在 hello 美國太平洋 coast，而其為冬季，您可能會像：

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html)：彙總資料列群組
`Summarize` 會對資料列群組套用指定的「彙總函式」。

您的 web 應用程式所需 toorespond tooa 要求的 hello 時間在 hello 欄位的報告，例如`duration`。 我們來看看 hello 平均回應時間 tooall 要求：

![](./media/app-insights-analytics-tour/410.png)

或者，我們無法將 hello 結果分成不同的名稱的要求：

![](./media/app-insights-analytics-tour/420.png)

`Summarize`收集 hello hello 資料流中的資料點的 hello 分組`by`同樣評估子句。 每個值在 hello`by`運算式-在上述範例中的 hello 中每個作業名稱-產生 hello 結果資料表中的資料列。

或者，我們可以依一天當中的時間將結果分組︰

![](./media/app-insights-analytics-tour/430.png)

請注意我們如何使用 hello`bin`函式 (也稱為`floor`)。 如果我們只使用 `by timestamp`，每個輸入資料列最終都會在它自己的小群組內。 針對任何連續的純量實 like 時間或數字，我們有 toobreak hello 連續範圍可管理的離散值的數目。 `bin`-也就是只 hello 熟悉捨入下`floor`函式-是最簡單方式 toodo hello 的。

我們可以使用 hello 字串的相同技巧 tooreduce 範圍：

![](./media/app-insights-analytics-tour/440.png)

請注意，您可以使用`name=`tooset hello hello 彙總運算式或 hello 依子句的結果資料行名稱。

## <a name="counting-sampled-data"></a>計算取樣的資料
`sum(itemCount)`是 hello 建議彙總 toocount 事件。 在許多情況下，itemCount = = 1，因此 hello 函式就是計算出 hello hello 群組中的資料列的號碼。 但是當[取樣](app-insights-sampling.md)是在作業中，只有一小部份 hello 原始事件仍會保留 Application Insights 中的資料點，您會看到每個資料點，有一些`itemCount`事件。

例如，如果取樣捨棄 75%的 hello 原始事件，然後 itemCount = = 4 hello 保留記錄-也就是針對每個保留的記錄沒有四個原始記錄。

自動調整取樣會造成 itemCount toobe 期間當您的應用程式正在大量使用更高版本。

加總 itemCount 因此提供良好的評估 hello 原始數字的事件。

![](./media/app-insights-analytics-tour/510.png)

另外還有`count()`彙總 （和計數作業），其中您真的想 toocount hello 數目的資料列群組中的案例。

目前提供一系列的 [彙總函式](https://docs.loganalytics.io/learn/tutorials/aggregations.html)。

## <a name="charting-hello-results"></a>圖表 hello 結果
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

根據預設，結果會顯示成資料表︰

![](./media/app-insights-analytics-tour/225.png)

我們可以比 hello 資料表檢視表更好執行。 讓我們看看 hello 圖表檢視中的 hello 結果與 hello 垂直列選項：

![按一下 [圖表]，然後選擇 [直條圖] 並指派 x 和 y 軸](./media/app-insights-analytics-tour/230.png)

請注意，雖然我們未依照時間排序 hello 結果，（因為您可以看到在 hello 資料表顯示）、 hello 圖表顯示永遠會固定顯示正確的順序。


## <a name="timecharts"></a>時間表
顯示每小時有多少個事件︰

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

選取 hello 圖表顯示的選項：

![時間圖](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>多個系列
多個運算式中 hello`summarize`子句會建立多個資料行。

多個運算式中 hello`by`子句會建立多個資料列，一個用於每一個值組合。

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![依小時和位置的要求資料表](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>依據維度分割圖表
如果圖表具有字串資料行和數值資料行 hello 字串的資料表可以使用的 toosplit 成個別的數列的點 hello 數值資料。 如果有一個以上的字串資料行，您可以選擇哪些資料行 toouse 作為 hello 鑑別子。

![分割分析圖表](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>跳出率

轉換布林 tooa 字串 toouse 它當做鑑別子：

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a>顯示多個計量
如果您的圖表中加入 toohello 時間戳記有一個以上的數字資料行的資料表，您可以顯示它們的任何組合。

![分割分析圖表](./media/app-insights-analytics-tour/110.png)

您必須選取 [不分割]，才能選取多個數值資料行。 您無法藉由分割字串資料行在 hello 相同時間做為顯示一個以上的數字資料行。

## <a name="daily-average-cycle"></a>每日平均週期
使用量會透過一天平均 hello 如何改變的？

計數要求 hello 時間模數一天，分類成小時：

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![平均一天的時數折線圖](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> 請注意，我們目前已有 tooconvert 時間持續時間 toodatetimes 順序 toodisplay 在折線圖上。
>
>

## <a name="compare-multiple-daily-series"></a>比較多個每日系列
如何沒有使用量會隨著 hello 時間一天中不同國家 （地區）？

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![依 client_CountryOrRegion 分割](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a>繪製分佈圖
有多少個不同長度的工作階段？

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

hello 的最後一行是必要的 tooconvert toodatetime。 目前 hello x 軸的圖表會顯示為純量，只有當該日期時間。

hello`where`子句排除單次的工作階段 (sessionDuration = = 0) 和集合 hello hello x 軸的長度。

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[百分位數](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
哪些持續時間範圍涵蓋不同的工作階段百分比？

使用上述查詢中，hello 但取代 hello 最後一行：

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

我們也會移除的 hello tooget 順序中的子句，其中修正包括具有多個要求的所有工作階段的數字中的 hello 上限：

![結果](./media/app-insights-analytics-tour/180.png)

我們可以從中看到︰

* 5% 的工作階段的持續時間小於 3 分鐘 34 秒；
* 50% 的工作階段的持續時間小於 36 分鐘；
* 5% 的工作階段的持續時間超過 7 天

tooget 每個國家/地區的個別明細，我們只需要 toobring hello client_CountryOrRegion 資料行分別同時透過彙總運算子：

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a>Join
我們有存取 tooseveral 資料表，包括要求和例外狀況。

toofind hello 例外狀況相關的 tooa 要求傳回錯誤回應，我們可以加入 hello 的資料表上`session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


它是很好的作法 toouse `project` tooselect hello 只是資料行，我們需要在執行之前 hello 聯結。
在 hello 相同的子句，我們重新命名 hello 時間戳記資料行。

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[可讓](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html)： 將結果 tooa 變數指派

使用`let`tooseparate hello 部分的 hello 先前的運算式。 hello 結果維持不變：

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> 在 hello 分析用戶端，不放入空白 hello hello 查詢部分之間的行。 請確定 tooexecute 所有內容。
>

使用`toscalar`tooconvert tooa 單一資料表資料格的值：

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a>Functions

使用*讓*toodefine 函式：

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>存取巢狀物件
巢狀物件可以輕鬆地存取。 例如，hello 例外狀況資料流中，您可以看到結構化的物件，像這樣：

![結果](./media/app-insights-analytics-tour/520.png)

您可以選擇您感興趣的 hello 屬性扁平化它：

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

請注意，您需要 toocast hello 結果 toohello 適當類型。


## <a name="custom-properties-and-measurements"></a>自訂屬性和測量
如果您的應用程式附加[自訂維度 （屬性） 和自訂度量](app-insights-api-custom-events-metrics.md#properties)tooevents，則您會看到它們在 hello`customDimensions`和`customMeasurements`物件。

例如，如果您的應用程式包括︰

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract 這些在分析中的值：

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify 自訂維度是否具有特定型別：

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>儀表板
您可以釘選結果 tooa 儀表板中順序 toobring 一起所有您最重要圖表和資料表。

* [Azure 共用儀表板](app-insights-dashboards.md#share-dashboards)： 按一下 hello 釘選圖示。 執行這項作業之前，您必須具有共用儀表板。 在 hello Azure 入口網站，開啟或建立儀表板，然後按一下 共用。
* [Power BI 儀表板](app-insights-export-power-bi.md)︰按一下 [匯出]、[Power BI 查詢]。 此替代方案的優點是您可以顯示查詢，還有各種來源的其他結果。

## <a name="combine-with-imported-data"></a>與匯入的資料結合

分析報表看起來不錯 hello 儀表板，但有時候您會想 tootranslate hello 資料 tooa 更多容易吸收的表單。 例如，假設您已驗證的使用者識別 hello 遙測中的別名。 在結果中，您會希望的 tooshow 其實際名稱。 toodo，您需要從 hello 別名 toohello 實際名稱對應的 CSV 檔案。

您可以匯入資料檔案，並使用它，就像任何 hello 標準資料表 （要求、 例外狀況，等等）。 單獨查詢它，或是將它與其他資料表聯結。 例如，如果您有資料表，名為 使用者對應，而且它有資料行`realName`和`userId`，則您可以使用它 tootranslate hello `user_AuthenticatedId` hello 要求遙測中的欄位：

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport 資料表，在 hello 結構描述刀鋒視窗中，在**其他資料來源**，遵循 hello 指示 tooadd 新的資料來源上傳您資料的範例。 然後您可以使用此定義 tooupload 資料表。

hello 匯入功能目前為預覽狀態，所以您一開始會看到 「 與我們連絡 」 連結底下 「 其他資料來源。 」 使用此 toosign toohello 預覽程式，並 hello 連結然後將會取代 [新增新的資料來源] 按鈕。


## <a name="tables"></a>資料表
存取多個資料表透過 hello 的遙測資料從您的應用程式收到的資料流。 hello 的內容適用於每個資料表的結構描述會顯示在 hello hello 視窗的左邊。

### <a name="requests-table"></a>要求資料表
計數 HTTP 要求 tooyour web 應用程式，並依頁面名稱的區段：

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-count-requests.png)

尋找失敗大部分的 hello 要求：

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>自訂事件資料表
如果您使用[trackevent （)](app-insights-api-custom-events-metrics.md#trackevent) toosend 您自己的事件，您可以讀取它們從這個資料表。

讓我們舉包含下列程式行的應用程式程式碼為例︰

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

這些事件的顯示 hello 頻率：

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

從 hello 事件中擷取的量值和維度：

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>自訂度量表
如果您使用[trackmetric （)](app-insights-api-custom-events-metrics.md#trackmetric) toosend 您自己的度量值，您會發現它的結果在 hello **customMetrics**資料流。 例如：  

![Application Insights 分析中的自訂度量](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> 在[計量瀏覽器](app-insights-metrics-explorer.md)，附加的 tooany 類型的遙測資料一起出現在以及度量使用傳送 hello 計量刀鋒視窗中的所有自訂度量`TrackMetric()`。 但在 Analytics 中，自訂的度量是仍然附加 toowhichever 類型的遙測資料，它們已存在於-事件或要求，等位時 TrackMetric 所傳送的度量資訊會出現在自己的資料流。
>
>

### <a name="performance-counters-table"></a>效能計數器資料表
[效能計數器](app-insights-performance-counters.md)會對您顯示應用程式的基本系統度量，例如 CPU、記憶體和網路使用率。 您可以設定 hello SDK toosend 其他計數器，包括您自己自訂的計數器。

hello **performanceCounters**結構描述會公開 hello `category`，`counter`名稱，和`instance`每個效能計數器的名稱。 計數器執行個體名稱只適用於 toosome 效能計數器，而且通常會指出 hello 處理程序 toowhich hello 計數 hello 名稱與相關。 在 hello 每個應用程式的遙測，您會看到該應用程式只有 hello 計數器。 例如，toosee 哪些計數器可用：

![Application Insights 分析中的效能計數器](./media/app-insights-analytics-tour/analytics-performance-counters.png)

tooget hello 透過可用的記憶體圖表選取的週期：

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-analytics-tour/analytics-available-memory.png)

類似其他遙測**performanceCounters**也有一個資料行`cloud_RoleInstance`指出 hello 識別您的應用程式執行所在的 hello 主機電腦。 例如，toocompare hello 效能 hello 不同的電腦上的應用程式：

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>例外狀況資料表
此資料表中有提供[應用程式所報告的例外狀況](app-insights-asp-net-exceptions.md)。

toofind hello hello 例外狀況時，您的應用程式所處理的 HTTP 要求，請加入 operation_Id 上：

![在 operation_Id 聯結例外狀況與要求](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>瀏覽器計時資料表
`browserTimings` 會顯示使用者的瀏覽器所收集到的頁面載入資料。

[設定您的應用程式的用戶端遙測](app-insights-javascript.md)中排序 toosee 這些度量。

hello 結構描述包含[指出 hello 長度的不同階段的 hello 頁面載入處理序的度量](app-insights-javascript.md#page-load-performance)。 （這些不代表 hello 您的使用者讀取某個頁面的時間長度）。  

顯示不同的網頁、 hello popularities 和載入速度為每個頁面：

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>可用性結果資料表
`availabilityResults`顯示 hello 的結果您[web 測試](app-insights-monitor-web-app-availability.md)。 每個測試位置每次執行的測試會分開報告。

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>相依性資料表
包含呼叫的結果，您的應用程式會使 toodatabases 和 REST Api 和其他呼叫 tooTrackDependency()。 也包含從 hello 瀏覽器所做的 AJAX 呼叫。

從 hello 瀏覽器的 AJAX 呼叫：

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

相依性呼叫從 hello 伺服器：

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

伺服器端的相依性的結果永遠顯示`success==False`如果 hello Application Insights 的代理程式未安裝。 不過，hello 其他資料正確無誤。

### <a name="traces-table"></a>追蹤資料表
包含使用 tracktrace （），您的應用程式所傳送的 hello 遙測或[其他記錄架構](app-insights-asp-net-trace-logs.md)。

## <a name="video"></a>影片 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

進階查詢：

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>後續步驟
* [分析語言參考](app-insights-analytics-reference.md)
* [SQL 使用者 ' 速查表](https://aka.ms/sql-analytics)轉譯 hello 最常見慣用語。

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
