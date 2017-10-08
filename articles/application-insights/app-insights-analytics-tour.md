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
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="808f9-103">Application Insights 中分析的教學課程</span><span class="sxs-lookup"><span data-stu-id="808f9-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="808f9-104">[分析](app-insights-analytics.md)是功能強大的搜尋功能 hello [Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="808f9-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="808f9-105">這些分頁說明 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="808f9-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="808f9-106">**[請觀看 hello 簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。</span><span class="sxs-lookup"><span data-stu-id="808f9-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="808f9-107">**[測試模擬資料的磁碟機分析](https://analytics.applicationinsights.io/demo)**如果您的應用程式未尚未傳送資料 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="808f9-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="808f9-108">**[SQL 使用者 ' 速查表](https://aka.ms/sql-analytics)**轉譯 hello 最常見慣用語。</span><span class="sxs-lookup"><span data-stu-id="808f9-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="808f9-109">讓我們逐步啟動一些基本查詢 tooget。</span><span class="sxs-lookup"><span data-stu-id="808f9-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="808f9-110">Tooyour Application Insights 資料連接</span><span class="sxs-lookup"><span data-stu-id="808f9-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="808f9-111">在 Application Insights 中，從 app 的 [概觀刀鋒視窗](app-insights-dashboards.md) 開啟 [分析]：</span><span class="sxs-lookup"><span data-stu-id="808f9-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="808f9-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)：顯示 n 個資料列</span><span class="sxs-lookup"><span data-stu-id="808f9-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="808f9-114">記錄使用者作業的資料點 (通常是 Web 應用程式收到的 HTTP 要求) 會儲存在名為 `requests`的資料表。</span><span class="sxs-lookup"><span data-stu-id="808f9-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="808f9-115">每個資料列是來自應用程式中的 hello Application Insights SDK 遙測資料點。</span><span class="sxs-lookup"><span data-stu-id="808f9-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="808f9-116">讓我們開始檢查 hello 資料表的一些範例資料列：</span><span class="sxs-lookup"><span data-stu-id="808f9-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="808f9-118">Hello 游標處 hello 陳述式會先置於您按一下 移至。</span><span class="sxs-lookup"><span data-stu-id="808f9-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="808f9-119">您可以將陳述式分割成多行，但不要在單一陳述式中放置空白行。</span><span class="sxs-lookup"><span data-stu-id="808f9-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="808f9-120">空白的行是很方便的方式 tookeep 數個分隔 hello 視窗中的查詢。</span><span class="sxs-lookup"><span data-stu-id="808f9-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="808f9-121">選擇資料行、加以拖曳，依照資料行分組，以及進行篩選︰</span><span class="sxs-lookup"><span data-stu-id="808f9-121">Choose columns, drag them, group by columns, and filter:</span></span>

![按一下結果右上方的資料行選取範圍](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="808f9-123">展開任何項目 toosee hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="808f9-123">Expand any item toosee hello detail:</span></span>

![選擇 [資料表]，並使用 [設定資料行]](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="808f9-125">按一下資料行 toore 順序 hello 可用的結果 hello 網頁瀏覽器中的 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="808f9-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="808f9-126">但是請注意，對於大型結果集，hello 的資料列下載的 toohello 瀏覽器所數目有限。</span><span class="sxs-lookup"><span data-stu-id="808f9-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="808f9-127">排序這種方式不一定會顯示您 hello 實際的最高或最低的項目。</span><span class="sxs-lookup"><span data-stu-id="808f9-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="808f9-128">toosort 項目可靠地使用 hello`top`或`sort`運算子。</span><span class="sxs-lookup"><span data-stu-id="808f9-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="808f9-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 和 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="808f9-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="808f9-130">`take`是有用的 tooget 快速範例的結果，但它會顯示 hello 資料表的資料列中沒有特定順序。</span><span class="sxs-lookup"><span data-stu-id="808f9-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="808f9-131">tooget 已排序的檢視中，使用`top`（如需範例中） 或`sort`（透過 hello 整個資料表）。</span><span class="sxs-lookup"><span data-stu-id="808f9-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="808f9-132">顯示 hello 前 n 個資料列，依特定的資料行：</span><span class="sxs-lookup"><span data-stu-id="808f9-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="808f9-133">語法︰大部分運算子都有關鍵字參數 (例如 `by`)。</span><span class="sxs-lookup"><span data-stu-id="808f9-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="808f9-134">`desc` = 遞減順序，`asc` = 遞增。</span><span class="sxs-lookup"><span data-stu-id="808f9-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="808f9-135">`top...` 是 `sort ... | take...` 比較有效率的說法。</span><span class="sxs-lookup"><span data-stu-id="808f9-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="808f9-136">我們可以撰寫︰</span><span class="sxs-lookup"><span data-stu-id="808f9-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="808f9-137">hello 結果會是 hello 相同，但它會執行位元速度變慢。</span><span class="sxs-lookup"><span data-stu-id="808f9-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="808f9-138">(您也可以撰寫 `order`，這是 `sort` 的別名)。</span><span class="sxs-lookup"><span data-stu-id="808f9-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="808f9-139">hello hello 資料表檢視表中的資料行標頭也可以使用的 toosort hello 結果囉 」 畫面上。</span><span class="sxs-lookup"><span data-stu-id="808f9-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="808f9-140">當然，如果您曾經使用，但是`take`或`top`tooretrieve 部分的資料表，將只重新排序 hello 記錄了擷取。</span><span class="sxs-lookup"><span data-stu-id="808f9-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="808f9-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)︰篩選條件</span><span class="sxs-lookup"><span data-stu-id="808f9-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="808f9-142">讓我們看一下傳回特定結果碼的要求︰</span><span class="sxs-lookup"><span data-stu-id="808f9-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="808f9-143">hello`where`運算子會採用布林運算式。</span><span class="sxs-lookup"><span data-stu-id="808f9-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="808f9-144">以下是其相關的一些重點︰</span><span class="sxs-lookup"><span data-stu-id="808f9-144">Here are some key points about them:</span></span>

* <span data-ttu-id="808f9-145">`and`、`or`：布林運算子</span><span class="sxs-lookup"><span data-stu-id="808f9-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="808f9-146">`==`、`<>`、`!=`︰等於和不等於</span><span class="sxs-lookup"><span data-stu-id="808f9-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="808f9-147">`=~`、`!~`︰不區分大小寫的字串等於和不等於。</span><span class="sxs-lookup"><span data-stu-id="808f9-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="808f9-148">有更多的字串比較運算子。</span><span class="sxs-lookup"><span data-stu-id="808f9-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="808f9-149">收到 hello 右類型</span><span class="sxs-lookup"><span data-stu-id="808f9-149">Getting hello right type</span></span>
<span data-ttu-id="808f9-150">尋找失敗的要求︰</span><span class="sxs-lookup"><span data-stu-id="808f9-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="808f9-151">時間</span><span class="sxs-lookup"><span data-stu-id="808f9-151">Time</span></span>

<span data-ttu-id="808f9-152">根據預設，您的查詢會很限制的 toohello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="808f9-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="808f9-153">但您可以變更此範圍︰</span><span class="sxs-lookup"><span data-stu-id="808f9-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="808f9-154">撰寫提及的任何查詢，以覆寫 hello 時間範圍`timestamp`where 子句中。</span><span class="sxs-lookup"><span data-stu-id="808f9-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="808f9-155">例如：</span><span class="sxs-lookup"><span data-stu-id="808f9-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="808f9-156">hello 時間範圍功能是對等 tooa 'where' 子句插入之後的其中一個 hello 來源資料表的每個提及。</span><span class="sxs-lookup"><span data-stu-id="808f9-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="808f9-157">`ago(3d)` 表示「三天前」。</span><span class="sxs-lookup"><span data-stu-id="808f9-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="808f9-158">其他時間單位包括小時 (`2h`、`2.5h`)、分鐘 (`25m`) 和秒 (`10s`)。</span><span class="sxs-lookup"><span data-stu-id="808f9-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="808f9-159">其他範例︰</span><span class="sxs-lookup"><span data-stu-id="808f9-159">Other examples:</span></span>

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

<span data-ttu-id="808f9-160">[日期和時間參考](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)。</span><span class="sxs-lookup"><span data-stu-id="808f9-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="808f9-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)：選取、重新命名和計算資料行</span><span class="sxs-lookup"><span data-stu-id="808f9-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="808f9-162">使用[ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick 出只要您想要的 hello 資料行：</span><span class="sxs-lookup"><span data-stu-id="808f9-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="808f9-163">您也可以將資料行重新命名並定義新的資料行︰</span><span class="sxs-lookup"><span data-stu-id="808f9-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="808f9-165">如果資料行名稱是以括號括起來 (如下所示)，就可以包含空格或符號︰`['...']` 或 `["..."]`</span><span class="sxs-lookup"><span data-stu-id="808f9-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="808f9-166">`%`為 hello 一般模數運算子。</span><span class="sxs-lookup"><span data-stu-id="808f9-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="808f9-167">`1d` (這是數字 1，再加上 'd') 是一個時間範圍常值，表示一天。</span><span class="sxs-lookup"><span data-stu-id="808f9-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="808f9-168">以下是其他一些時間範圍常值︰`12h`、`30m`、`10s`、`0.01s`。</span><span class="sxs-lookup"><span data-stu-id="808f9-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="808f9-169">`floor`(別名`bin`) 將值四捨五入為最接近您所提供的 hello 基底值的倍數 toohello 關閉。</span><span class="sxs-lookup"><span data-stu-id="808f9-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="808f9-170">因此`floor(aTime, 1s)`捨入 toohello 最接近的第二個關閉的時間。</span><span class="sxs-lookup"><span data-stu-id="808f9-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="808f9-171">運算式可以包含所有 hello 一般運算子 (`+`， `-`，...)，而且沒有有用的函式的範圍。</span><span class="sxs-lookup"><span data-stu-id="808f9-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="808f9-172">Extend</span><span class="sxs-lookup"><span data-stu-id="808f9-172">Extend</span></span>
<span data-ttu-id="808f9-173">如果您只想 tooadd 現有的資料行 toohello，使用[ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="808f9-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="808f9-174">使用[ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html)較不繁複比[ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)如果您想 tookeep 所有 hello 現有的資料行。</span><span class="sxs-lookup"><span data-stu-id="808f9-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="808f9-175">將 toolocal 時間轉換</span><span class="sxs-lookup"><span data-stu-id="808f9-175">Convert toolocal time</span></span>

<span data-ttu-id="808f9-176">時間戳記一律是 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="808f9-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="808f9-177">因此如果您在 hello 美國太平洋 coast，而其為冬季，您可能會像：</span><span class="sxs-lookup"><span data-stu-id="808f9-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="808f9-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html)：彙總資料列群組</span><span class="sxs-lookup"><span data-stu-id="808f9-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="808f9-179">`Summarize` 會對資料列群組套用指定的「彙總函式」。</span><span class="sxs-lookup"><span data-stu-id="808f9-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="808f9-180">您的 web 應用程式所需 toorespond tooa 要求的 hello 時間在 hello 欄位的報告，例如`duration`。</span><span class="sxs-lookup"><span data-stu-id="808f9-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="808f9-181">我們來看看 hello 平均回應時間 tooall 要求：</span><span class="sxs-lookup"><span data-stu-id="808f9-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="808f9-182">或者，我們無法將 hello 結果分成不同的名稱的要求：</span><span class="sxs-lookup"><span data-stu-id="808f9-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="808f9-183">`Summarize`收集 hello hello 資料流中的資料點的 hello 分組`by`同樣評估子句。</span><span class="sxs-lookup"><span data-stu-id="808f9-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="808f9-184">每個值在 hello`by`運算式-在上述範例中的 hello 中每個作業名稱-產生 hello 結果資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="808f9-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="808f9-185">或者，我們可以依一天當中的時間將結果分組︰</span><span class="sxs-lookup"><span data-stu-id="808f9-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="808f9-186">請注意我們如何使用 hello`bin`函式 (也稱為`floor`)。</span><span class="sxs-lookup"><span data-stu-id="808f9-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="808f9-187">如果我們只使用 `by timestamp`，每個輸入資料列最終都會在它自己的小群組內。</span><span class="sxs-lookup"><span data-stu-id="808f9-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="808f9-188">針對任何連續的純量實 like 時間或數字，我們有 toobreak hello 連續範圍可管理的離散值的數目。</span><span class="sxs-lookup"><span data-stu-id="808f9-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="808f9-189">`bin`-也就是只 hello 熟悉捨入下`floor`函式-是最簡單方式 toodo hello 的。</span><span class="sxs-lookup"><span data-stu-id="808f9-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="808f9-190">我們可以使用 hello 字串的相同技巧 tooreduce 範圍：</span><span class="sxs-lookup"><span data-stu-id="808f9-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="808f9-191">請注意，您可以使用`name=`tooset hello hello 彙總運算式或 hello 依子句的結果資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="808f9-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="808f9-192">計算取樣的資料</span><span class="sxs-lookup"><span data-stu-id="808f9-192">Counting sampled data</span></span>
<span data-ttu-id="808f9-193">`sum(itemCount)`是 hello 建議彙總 toocount 事件。</span><span class="sxs-lookup"><span data-stu-id="808f9-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="808f9-194">在許多情況下，itemCount = = 1，因此 hello 函式就是計算出 hello hello 群組中的資料列的號碼。</span><span class="sxs-lookup"><span data-stu-id="808f9-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="808f9-195">但是當[取樣](app-insights-sampling.md)是在作業中，只有一小部份 hello 原始事件仍會保留 Application Insights 中的資料點，您會看到每個資料點，有一些`itemCount`事件。</span><span class="sxs-lookup"><span data-stu-id="808f9-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="808f9-196">例如，如果取樣捨棄 75%的 hello 原始事件，然後 itemCount = = 4 hello 保留記錄-也就是針對每個保留的記錄沒有四個原始記錄。</span><span class="sxs-lookup"><span data-stu-id="808f9-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="808f9-197">自動調整取樣會造成 itemCount toobe 期間當您的應用程式正在大量使用更高版本。</span><span class="sxs-lookup"><span data-stu-id="808f9-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="808f9-198">加總 itemCount 因此提供良好的評估 hello 原始數字的事件。</span><span class="sxs-lookup"><span data-stu-id="808f9-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="808f9-199">另外還有`count()`彙總 （和計數作業），其中您真的想 toocount hello 數目的資料列群組中的案例。</span><span class="sxs-lookup"><span data-stu-id="808f9-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="808f9-200">目前提供一系列的 [彙總函式](https://docs.loganalytics.io/learn/tutorials/aggregations.html)。</span><span class="sxs-lookup"><span data-stu-id="808f9-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="808f9-201">圖表 hello 結果</span><span class="sxs-lookup"><span data-stu-id="808f9-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="808f9-202">根據預設，結果會顯示成資料表︰</span><span class="sxs-lookup"><span data-stu-id="808f9-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="808f9-203">我們可以比 hello 資料表檢視表更好執行。</span><span class="sxs-lookup"><span data-stu-id="808f9-203">We can do better than hello table view.</span></span> <span data-ttu-id="808f9-204">讓我們看看 hello 圖表檢視中的 hello 結果與 hello 垂直列選項：</span><span class="sxs-lookup"><span data-stu-id="808f9-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![按一下 [圖表]，然後選擇 [直條圖] 並指派 x 和 y 軸](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="808f9-206">請注意，雖然我們未依照時間排序 hello 結果，（因為您可以看到在 hello 資料表顯示）、 hello 圖表顯示永遠會固定顯示正確的順序。</span><span class="sxs-lookup"><span data-stu-id="808f9-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="808f9-207">時間表</span><span class="sxs-lookup"><span data-stu-id="808f9-207">Timecharts</span></span>
<span data-ttu-id="808f9-208">顯示每小時有多少個事件︰</span><span class="sxs-lookup"><span data-stu-id="808f9-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="808f9-209">選取 hello 圖表顯示的選項：</span><span class="sxs-lookup"><span data-stu-id="808f9-209">Select hello Chart display option:</span></span>

![時間圖](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="808f9-211">多個系列</span><span class="sxs-lookup"><span data-stu-id="808f9-211">Multiple series</span></span>
<span data-ttu-id="808f9-212">多個運算式中 hello`summarize`子句會建立多個資料行。</span><span class="sxs-lookup"><span data-stu-id="808f9-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="808f9-213">多個運算式中 hello`by`子句會建立多個資料列，一個用於每一個值組合。</span><span class="sxs-lookup"><span data-stu-id="808f9-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![依小時和位置的要求資料表](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="808f9-215">依據維度分割圖表</span><span class="sxs-lookup"><span data-stu-id="808f9-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="808f9-216">如果圖表具有字串資料行和數值資料行 hello 字串的資料表可以使用的 toosplit 成個別的數列的點 hello 數值資料。</span><span class="sxs-lookup"><span data-stu-id="808f9-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="808f9-217">如果有一個以上的字串資料行，您可以選擇哪些資料行 toouse 作為 hello 鑑別子。</span><span class="sxs-lookup"><span data-stu-id="808f9-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![分割分析圖表](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="808f9-219">跳出率</span><span class="sxs-lookup"><span data-stu-id="808f9-219">Bounce rate</span></span>

<span data-ttu-id="808f9-220">轉換布林 tooa 字串 toouse 它當做鑑別子：</span><span class="sxs-lookup"><span data-stu-id="808f9-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="808f9-221">顯示多個計量</span><span class="sxs-lookup"><span data-stu-id="808f9-221">Display multiple metrics</span></span>
<span data-ttu-id="808f9-222">如果您的圖表中加入 toohello 時間戳記有一個以上的數字資料行的資料表，您可以顯示它們的任何組合。</span><span class="sxs-lookup"><span data-stu-id="808f9-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![分割分析圖表](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="808f9-224">您必須選取 [不分割]，才能選取多個數值資料行。</span><span class="sxs-lookup"><span data-stu-id="808f9-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="808f9-225">您無法藉由分割字串資料行在 hello 相同時間做為顯示一個以上的數字資料行。</span><span class="sxs-lookup"><span data-stu-id="808f9-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="808f9-226">每日平均週期</span><span class="sxs-lookup"><span data-stu-id="808f9-226">Daily average cycle</span></span>
<span data-ttu-id="808f9-227">使用量會透過一天平均 hello 如何改變的？</span><span class="sxs-lookup"><span data-stu-id="808f9-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="808f9-228">計數要求 hello 時間模數一天，分類成小時：</span><span class="sxs-lookup"><span data-stu-id="808f9-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="808f9-230">請注意，我們目前已有 tooconvert 時間持續時間 toodatetimes 順序 toodisplay 在折線圖上。</span><span class="sxs-lookup"><span data-stu-id="808f9-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="808f9-231">比較多個每日系列</span><span class="sxs-lookup"><span data-stu-id="808f9-231">Compare multiple daily series</span></span>
<span data-ttu-id="808f9-232">如何沒有使用量會隨著 hello 時間一天中不同國家 （地區）？</span><span class="sxs-lookup"><span data-stu-id="808f9-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="808f9-234">繪製分佈圖</span><span class="sxs-lookup"><span data-stu-id="808f9-234">Plot a distribution</span></span>
<span data-ttu-id="808f9-235">有多少個不同長度的工作階段？</span><span class="sxs-lookup"><span data-stu-id="808f9-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="808f9-236">hello 的最後一行是必要的 tooconvert toodatetime。</span><span class="sxs-lookup"><span data-stu-id="808f9-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="808f9-237">目前 hello x 軸的圖表會顯示為純量，只有當該日期時間。</span><span class="sxs-lookup"><span data-stu-id="808f9-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="808f9-238">hello`where`子句排除單次的工作階段 (sessionDuration = = 0) 和集合 hello hello x 軸的長度。</span><span class="sxs-lookup"><span data-stu-id="808f9-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="808f9-239">百分位數</span><span class="sxs-lookup"><span data-stu-id="808f9-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="808f9-240">哪些持續時間範圍涵蓋不同的工作階段百分比？</span><span class="sxs-lookup"><span data-stu-id="808f9-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="808f9-241">使用上述查詢中，hello 但取代 hello 最後一行：</span><span class="sxs-lookup"><span data-stu-id="808f9-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="808f9-242">我們也會移除的 hello tooget 順序中的子句，其中修正包括具有多個要求的所有工作階段的數字中的 hello 上限：</span><span class="sxs-lookup"><span data-stu-id="808f9-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![結果](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="808f9-244">我們可以從中看到︰</span><span class="sxs-lookup"><span data-stu-id="808f9-244">From which we can see that:</span></span>

* <span data-ttu-id="808f9-245">5% 的工作階段的持續時間小於 3 分鐘 34 秒；</span><span class="sxs-lookup"><span data-stu-id="808f9-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="808f9-246">50% 的工作階段的持續時間小於 36 分鐘；</span><span class="sxs-lookup"><span data-stu-id="808f9-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="808f9-247">5% 的工作階段的持續時間超過 7 天</span><span class="sxs-lookup"><span data-stu-id="808f9-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="808f9-248">tooget 每個國家/地區的個別明細，我們只需要 toobring hello client_CountryOrRegion 資料行分別同時透過彙總運算子：</span><span class="sxs-lookup"><span data-stu-id="808f9-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="808f9-249">Join</span><span class="sxs-lookup"><span data-stu-id="808f9-249">Join</span></span>
<span data-ttu-id="808f9-250">我們有存取 tooseveral 資料表，包括要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="808f9-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="808f9-251">toofind hello 例外狀況相關的 tooa 要求傳回錯誤回應，我們可以加入 hello 的資料表上`session_Id`:</span><span class="sxs-lookup"><span data-stu-id="808f9-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="808f9-252">它是很好的作法 toouse `project` tooselect hello 只是資料行，我們需要在執行之前 hello 聯結。</span><span class="sxs-lookup"><span data-stu-id="808f9-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="808f9-253">在 hello 相同的子句，我們重新命名 hello 時間戳記資料行。</span><span class="sxs-lookup"><span data-stu-id="808f9-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="808f9-254">[可讓](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html)： 將結果 tooa 變數指派</span><span class="sxs-lookup"><span data-stu-id="808f9-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="808f9-255">使用`let`tooseparate hello 部分的 hello 先前的運算式。</span><span class="sxs-lookup"><span data-stu-id="808f9-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="808f9-256">hello 結果維持不變：</span><span class="sxs-lookup"><span data-stu-id="808f9-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="808f9-257">在 hello 分析用戶端，不放入空白 hello hello 查詢部分之間的行。</span><span class="sxs-lookup"><span data-stu-id="808f9-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="808f9-258">請確定 tooexecute 所有內容。</span><span class="sxs-lookup"><span data-stu-id="808f9-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="808f9-259">使用`toscalar`tooconvert tooa 單一資料表資料格的值：</span><span class="sxs-lookup"><span data-stu-id="808f9-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="808f9-260">Functions</span><span class="sxs-lookup"><span data-stu-id="808f9-260">Functions</span></span>

<span data-ttu-id="808f9-261">使用*讓*toodefine 函式：</span><span class="sxs-lookup"><span data-stu-id="808f9-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="808f9-262">存取巢狀物件</span><span class="sxs-lookup"><span data-stu-id="808f9-262">Accessing nested objects</span></span>
<span data-ttu-id="808f9-263">巢狀物件可以輕鬆地存取。</span><span class="sxs-lookup"><span data-stu-id="808f9-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="808f9-264">例如，hello 例外狀況資料流中，您可以看到結構化的物件，像這樣：</span><span class="sxs-lookup"><span data-stu-id="808f9-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![結果](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="808f9-266">您可以選擇您感興趣的 hello 屬性扁平化它：</span><span class="sxs-lookup"><span data-stu-id="808f9-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="808f9-267">請注意，您需要 toocast hello 結果 toohello 適當類型。</span><span class="sxs-lookup"><span data-stu-id="808f9-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="808f9-268">自訂屬性和測量</span><span class="sxs-lookup"><span data-stu-id="808f9-268">Custom properties and measurements</span></span>
<span data-ttu-id="808f9-269">如果您的應用程式附加[自訂維度 （屬性） 和自訂度量](app-insights-api-custom-events-metrics.md#properties)tooevents，則您會看到它們在 hello`customDimensions`和`customMeasurements`物件。</span><span class="sxs-lookup"><span data-stu-id="808f9-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="808f9-270">例如，如果您的應用程式包括︰</span><span class="sxs-lookup"><span data-stu-id="808f9-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="808f9-271">tooextract 這些在分析中的值：</span><span class="sxs-lookup"><span data-stu-id="808f9-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="808f9-272">tooverify 自訂維度是否具有特定型別：</span><span class="sxs-lookup"><span data-stu-id="808f9-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="808f9-273">儀表板</span><span class="sxs-lookup"><span data-stu-id="808f9-273">Dashboards</span></span>
<span data-ttu-id="808f9-274">您可以釘選結果 tooa 儀表板中順序 toobring 一起所有您最重要圖表和資料表。</span><span class="sxs-lookup"><span data-stu-id="808f9-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="808f9-275">[Azure 共用儀表板](app-insights-dashboards.md#share-dashboards)： 按一下 hello 釘選圖示。</span><span class="sxs-lookup"><span data-stu-id="808f9-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="808f9-276">執行這項作業之前，您必須具有共用儀表板。</span><span class="sxs-lookup"><span data-stu-id="808f9-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="808f9-277">在 hello Azure 入口網站，開啟或建立儀表板，然後按一下 共用。</span><span class="sxs-lookup"><span data-stu-id="808f9-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="808f9-278">[Power BI 儀表板](app-insights-export-power-bi.md)︰按一下 [匯出]、[Power BI 查詢]。</span><span class="sxs-lookup"><span data-stu-id="808f9-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="808f9-279">此替代方案的優點是您可以顯示查詢，還有各種來源的其他結果。</span><span class="sxs-lookup"><span data-stu-id="808f9-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="808f9-280">與匯入的資料結合</span><span class="sxs-lookup"><span data-stu-id="808f9-280">Combine with imported data</span></span>

<span data-ttu-id="808f9-281">分析報表看起來不錯 hello 儀表板，但有時候您會想 tootranslate hello 資料 tooa 更多容易吸收的表單。</span><span class="sxs-lookup"><span data-stu-id="808f9-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="808f9-282">例如，假設您已驗證的使用者識別 hello 遙測中的別名。</span><span class="sxs-lookup"><span data-stu-id="808f9-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="808f9-283">在結果中，您會希望的 tooshow 其實際名稱。</span><span class="sxs-lookup"><span data-stu-id="808f9-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="808f9-284">toodo，您需要從 hello 別名 toohello 實際名稱對應的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="808f9-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="808f9-285">您可以匯入資料檔案，並使用它，就像任何 hello 標準資料表 （要求、 例外狀況，等等）。</span><span class="sxs-lookup"><span data-stu-id="808f9-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="808f9-286">單獨查詢它，或是將它與其他資料表聯結。</span><span class="sxs-lookup"><span data-stu-id="808f9-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="808f9-287">例如，如果您有資料表，名為 使用者對應，而且它有資料行`realName`和`userId`，則您可以使用它 tootranslate hello `user_AuthenticatedId` hello 要求遙測中的欄位：</span><span class="sxs-lookup"><span data-stu-id="808f9-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="808f9-288">tooimport 資料表，在 hello 結構描述刀鋒視窗中，在**其他資料來源**，遵循 hello 指示 tooadd 新的資料來源上傳您資料的範例。</span><span class="sxs-lookup"><span data-stu-id="808f9-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="808f9-289">然後您可以使用此定義 tooupload 資料表。</span><span class="sxs-lookup"><span data-stu-id="808f9-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="808f9-290">hello 匯入功能目前為預覽狀態，所以您一開始會看到 「 與我們連絡 」 連結底下 「 其他資料來源。 」</span><span class="sxs-lookup"><span data-stu-id="808f9-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="808f9-291">使用此 toosign toohello 預覽程式，並 hello 連結然後將會取代 [新增新的資料來源] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="808f9-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="808f9-292">資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-292">Tables</span></span>
<span data-ttu-id="808f9-293">存取多個資料表透過 hello 的遙測資料從您的應用程式收到的資料流。</span><span class="sxs-lookup"><span data-stu-id="808f9-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="808f9-294">hello 的內容適用於每個資料表的結構描述會顯示在 hello hello 視窗的左邊。</span><span class="sxs-lookup"><span data-stu-id="808f9-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="808f9-295">要求資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-295">Requests table</span></span>
<span data-ttu-id="808f9-296">計數 HTTP 要求 tooyour web 應用程式，並依頁面名稱的區段：</span><span class="sxs-lookup"><span data-stu-id="808f9-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="808f9-298">尋找失敗大部分的 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="808f9-298">Find hello requests that fail most:</span></span>

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="808f9-300">自訂事件資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-300">Custom events table</span></span>
<span data-ttu-id="808f9-301">如果您使用[trackevent （)](app-insights-api-custom-events-metrics.md#trackevent) toosend 您自己的事件，您可以讀取它們從這個資料表。</span><span class="sxs-lookup"><span data-stu-id="808f9-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="808f9-302">讓我們舉包含下列程式行的應用程式程式碼為例︰</span><span class="sxs-lookup"><span data-stu-id="808f9-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="808f9-303">這些事件的顯示 hello 頻率：</span><span class="sxs-lookup"><span data-stu-id="808f9-303">Display hello frequency of these events:</span></span>

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="808f9-305">從 hello 事件中擷取的量值和維度：</span><span class="sxs-lookup"><span data-stu-id="808f9-305">Extract measurements and dimensions from hello events:</span></span>

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="808f9-307">自訂度量表</span><span class="sxs-lookup"><span data-stu-id="808f9-307">Custom metrics table</span></span>
<span data-ttu-id="808f9-308">如果您使用[trackmetric （)](app-insights-api-custom-events-metrics.md#trackmetric) toosend 您自己的度量值，您會發現它的結果在 hello **customMetrics**資料流。</span><span class="sxs-lookup"><span data-stu-id="808f9-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="808f9-309">例如：</span><span class="sxs-lookup"><span data-stu-id="808f9-309">For example:</span></span>  

![Application Insights 分析中的自訂度量](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="808f9-311">在[計量瀏覽器](app-insights-metrics-explorer.md)，附加的 tooany 類型的遙測資料一起出現在以及度量使用傳送 hello 計量刀鋒視窗中的所有自訂度量`TrackMetric()`。</span><span class="sxs-lookup"><span data-stu-id="808f9-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="808f9-312">但在 Analytics 中，自訂的度量是仍然附加 toowhichever 類型的遙測資料，它們已存在於-事件或要求，等位時 TrackMetric 所傳送的度量資訊會出現在自己的資料流。</span><span class="sxs-lookup"><span data-stu-id="808f9-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="808f9-313">效能計數器資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-313">Performance counters table</span></span>
<span data-ttu-id="808f9-314">[效能計數器](app-insights-performance-counters.md)會對您顯示應用程式的基本系統度量，例如 CPU、記憶體和網路使用率。</span><span class="sxs-lookup"><span data-stu-id="808f9-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="808f9-315">您可以設定 hello SDK toosend 其他計數器，包括您自己自訂的計數器。</span><span class="sxs-lookup"><span data-stu-id="808f9-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="808f9-316">hello **performanceCounters**結構描述會公開 hello `category`，`counter`名稱，和`instance`每個效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="808f9-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="808f9-317">計數器執行個體名稱只適用於 toosome 效能計數器，而且通常會指出 hello 處理程序 toowhich hello 計數 hello 名稱與相關。</span><span class="sxs-lookup"><span data-stu-id="808f9-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="808f9-318">在 hello 每個應用程式的遙測，您會看到該應用程式只有 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="808f9-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="808f9-319">例如，toosee 哪些計數器可用：</span><span class="sxs-lookup"><span data-stu-id="808f9-319">For example, toosee what counters are available:</span></span>

![Application Insights 分析中的效能計數器](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="808f9-321">tooget hello 透過可用的記憶體圖表選取的週期：</span><span class="sxs-lookup"><span data-stu-id="808f9-321">tooget a chart of available memory over hello selected period:</span></span>

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="808f9-323">類似其他遙測**performanceCounters**也有一個資料行`cloud_RoleInstance`指出 hello 識別您的應用程式執行所在的 hello 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="808f9-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="808f9-324">例如，toocompare hello 效能 hello 不同的電腦上的應用程式：</span><span class="sxs-lookup"><span data-stu-id="808f9-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="808f9-326">例外狀況資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-326">Exceptions table</span></span>
<span data-ttu-id="808f9-327">此資料表中有提供[應用程式所報告的例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="808f9-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="808f9-328">toofind hello hello 例外狀況時，您的應用程式所處理的 HTTP 要求，請加入 operation_Id 上：</span><span class="sxs-lookup"><span data-stu-id="808f9-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![在 operation_Id 聯結例外狀況與要求](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="808f9-330">瀏覽器計時資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-330">Browser timings table</span></span>
<span data-ttu-id="808f9-331">`browserTimings` 會顯示使用者的瀏覽器所收集到的頁面載入資料。</span><span class="sxs-lookup"><span data-stu-id="808f9-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="808f9-332">[設定您的應用程式的用戶端遙測](app-insights-javascript.md)中排序 toosee 這些度量。</span><span class="sxs-lookup"><span data-stu-id="808f9-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="808f9-333">hello 結構描述包含[指出 hello 長度的不同階段的 hello 頁面載入處理序的度量](app-insights-javascript.md#page-load-performance)。</span><span class="sxs-lookup"><span data-stu-id="808f9-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="808f9-334">（這些不代表 hello 您的使用者讀取某個頁面的時間長度）。</span><span class="sxs-lookup"><span data-stu-id="808f9-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="808f9-335">顯示不同的網頁、 hello popularities 和載入速度為每個頁面：</span><span class="sxs-lookup"><span data-stu-id="808f9-335">Show hello popularities of different pages, and load times for each page:</span></span>

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="808f9-337">可用性結果資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-337">Availability results table</span></span>
<span data-ttu-id="808f9-338">`availabilityResults`顯示 hello 的結果您[web 測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="808f9-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="808f9-339">每個測試位置每次執行的測試會分開報告。</span><span class="sxs-lookup"><span data-stu-id="808f9-339">Each run of your tests from each test location is reported separately.</span></span>

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="808f9-341">相依性資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-341">Dependencies table</span></span>
<span data-ttu-id="808f9-342">包含呼叫的結果，您的應用程式會使 toodatabases 和 REST Api 和其他呼叫 tooTrackDependency()。</span><span class="sxs-lookup"><span data-stu-id="808f9-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="808f9-343">也包含從 hello 瀏覽器所做的 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="808f9-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="808f9-344">從 hello 瀏覽器的 AJAX 呼叫：</span><span class="sxs-lookup"><span data-stu-id="808f9-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="808f9-345">相依性呼叫從 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="808f9-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="808f9-346">伺服器端的相依性的結果永遠顯示`success==False`如果 hello Application Insights 的代理程式未安裝。</span><span class="sxs-lookup"><span data-stu-id="808f9-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="808f9-347">不過，hello 其他資料正確無誤。</span><span class="sxs-lookup"><span data-stu-id="808f9-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="808f9-348">追蹤資料表</span><span class="sxs-lookup"><span data-stu-id="808f9-348">Traces table</span></span>
<span data-ttu-id="808f9-349">包含使用 tracktrace （），您的應用程式所傳送的 hello 遙測或[其他記錄架構](app-insights-asp-net-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="808f9-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="808f9-350">影片</span><span class="sxs-lookup"><span data-stu-id="808f9-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="808f9-351">進階查詢：</span><span class="sxs-lookup"><span data-stu-id="808f9-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="808f9-352">後續步驟</span><span class="sxs-lookup"><span data-stu-id="808f9-352">Next steps</span></span>
* [<span data-ttu-id="808f9-353">分析語言參考</span><span class="sxs-lookup"><span data-stu-id="808f9-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="808f9-354">[SQL 使用者 ' 速查表](https://aka.ms/sql-analytics)轉譯 hello 最常見慣用語。</span><span class="sxs-lookup"><span data-stu-id="808f9-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
