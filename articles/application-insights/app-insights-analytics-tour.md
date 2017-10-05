---
title: "Azure Application Insights 中分析的完整教學課程 | Microsoft Docs"
description: "分析 (Application Insights 的強大搜尋工具) 中所有主要查詢的簡短範例。"
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
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="5d303-103">Application Insights 中分析的教學課程</span><span class="sxs-lookup"><span data-stu-id="5d303-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="5d303-104">[分析](app-insights-analytics.md)是 [Application Insights](app-insights-overview.md) 的強大搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="5d303-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5d303-105">這些分頁說明 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="5d303-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="5d303-106">**[觀看簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。</span><span class="sxs-lookup"><span data-stu-id="5d303-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="5d303-107">如果您的應用程式還未將資料傳送至 Application Insights，則**[在我們的模擬資料上測試分析](https://analytics.applicationinsights.io/demo)**。</span><span class="sxs-lookup"><span data-stu-id="5d303-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="5d303-108">**[SQL 使用者的功能提要](https://aka.ms/sql-analytics)**會翻譯成最常見的習慣用語。</span><span class="sxs-lookup"><span data-stu-id="5d303-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="5d303-109">讓我們逐步解說可讓您快速入門的一些基本查詢。</span><span class="sxs-lookup"><span data-stu-id="5d303-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="5d303-110">連接到您的 Application Insights 資料</span><span class="sxs-lookup"><span data-stu-id="5d303-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="5d303-111">在 Application Insights 中，從 app 的 [概觀刀鋒視窗](app-insights-dashboards.md) 開啟 [分析]：</span><span class="sxs-lookup"><span data-stu-id="5d303-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="5d303-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)：顯示 n 個資料列</span><span class="sxs-lookup"><span data-stu-id="5d303-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="5d303-114">記錄使用者作業的資料點 (通常是 Web 應用程式收到的 HTTP 要求) 會儲存在名為 `requests`的資料表。</span><span class="sxs-lookup"><span data-stu-id="5d303-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="5d303-115">每個資料列都是從應用程式中的 Application Insights SDK 接收的遙測資料點。</span><span class="sxs-lookup"><span data-stu-id="5d303-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="5d303-116">讓我們先檢查資料表的幾個範例資料列︰</span><span class="sxs-lookup"><span data-stu-id="5d303-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="5d303-118">先將游標置於陳述式中的某處，再按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="5d303-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="5d303-119">您可以將陳述式分割成多行，但不要在單一陳述式中放置空白行。</span><span class="sxs-lookup"><span data-stu-id="5d303-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="5d303-120">空白行可方便您在視窗中保有數個不同的查詢。</span><span class="sxs-lookup"><span data-stu-id="5d303-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="5d303-121">選擇資料行、加以拖曳，依照資料行分組，以及進行篩選︰</span><span class="sxs-lookup"><span data-stu-id="5d303-121">Choose columns, drag them, group by columns, and filter:</span></span>

![按一下結果右上方的資料行選取範圍](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="5d303-123">展開任何項目以查看詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="5d303-123">Expand any item to see the detail:</span></span>

![選擇 [資料表]，並使用 [設定資料行]](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="5d303-125">按一下資料行的標頭，以重新排列網頁瀏覽器中可用的結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="5d303-126">但請注意，對大型結果集而言，下載至瀏覽器的資料列數目有限。</span><span class="sxs-lookup"><span data-stu-id="5d303-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="5d303-127">以這種方式排序並不一定會顯示實際的最高或最低項目。</span><span class="sxs-lookup"><span data-stu-id="5d303-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="5d303-128">若要可靠地將項目排序，請使用 `top` 或 `sort` 運算子。</span><span class="sxs-lookup"><span data-stu-id="5d303-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="5d303-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 和 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="5d303-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="5d303-130">`take` 可用來取得快速的結果範例，但它不會依特定順序顯示資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="5d303-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="5d303-131">若要取得已排序的檢視，請使用 `top` (適用於某個範例) 或 `sort` (整個資料表)。</span><span class="sxs-lookup"><span data-stu-id="5d303-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="5d303-132">顯示前 n 個資料列 (依特定資料行排序)︰</span><span class="sxs-lookup"><span data-stu-id="5d303-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="5d303-133">語法︰大部分運算子都有關鍵字參數 (例如 `by`)。</span><span class="sxs-lookup"><span data-stu-id="5d303-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="5d303-134">`desc` = 遞減順序，`asc` = 遞增。</span><span class="sxs-lookup"><span data-stu-id="5d303-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="5d303-135">`top...` 是 `sort ... | take...` 比較有效率的說法。</span><span class="sxs-lookup"><span data-stu-id="5d303-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="5d303-136">我們可以撰寫︰</span><span class="sxs-lookup"><span data-stu-id="5d303-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="5d303-137">結果會相同，但執行速度比較慢一點 </span><span class="sxs-lookup"><span data-stu-id="5d303-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="5d303-138">(您也可以撰寫 `order`，這是 `sort` 的別名)。</span><span class="sxs-lookup"><span data-stu-id="5d303-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="5d303-139">資料表檢視中的資料行標頭也可用來排序畫面上的結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="5d303-140">當然，如果您已使用 `take` 或 `top` 只擷取部分的資料表，您只會重新排列您所擷取的記錄。</span><span class="sxs-lookup"><span data-stu-id="5d303-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="5d303-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)︰篩選條件</span><span class="sxs-lookup"><span data-stu-id="5d303-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="5d303-142">讓我們看一下傳回特定結果碼的要求︰</span><span class="sxs-lookup"><span data-stu-id="5d303-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="5d303-143">`where` 運算子會採用布林運算式。</span><span class="sxs-lookup"><span data-stu-id="5d303-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="5d303-144">以下是其相關的一些重點︰</span><span class="sxs-lookup"><span data-stu-id="5d303-144">Here are some key points about them:</span></span>

* <span data-ttu-id="5d303-145">`and`、`or`：布林運算子</span><span class="sxs-lookup"><span data-stu-id="5d303-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="5d303-146">`==`、`<>`、`!=`︰等於和不等於</span><span class="sxs-lookup"><span data-stu-id="5d303-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="5d303-147">`=~`、`!~`︰不區分大小寫的字串等於和不等於。</span><span class="sxs-lookup"><span data-stu-id="5d303-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="5d303-148">有更多的字串比較運算子。</span><span class="sxs-lookup"><span data-stu-id="5d303-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="5d303-149">取得合適的類型</span><span class="sxs-lookup"><span data-stu-id="5d303-149">Getting the right type</span></span>
<span data-ttu-id="5d303-150">尋找失敗的要求︰</span><span class="sxs-lookup"><span data-stu-id="5d303-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="5d303-151">時間</span><span class="sxs-lookup"><span data-stu-id="5d303-151">Time</span></span>

<span data-ttu-id="5d303-152">根據預設，查詢會受限於最近 24 小時。</span><span class="sxs-lookup"><span data-stu-id="5d303-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="5d303-153">但您可以變更此範圍︰</span><span class="sxs-lookup"><span data-stu-id="5d303-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="5d303-154">在 where 子句中撰寫任何提及 `timestamp` 的查詢，以覆寫時間範圍。</span><span class="sxs-lookup"><span data-stu-id="5d303-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="5d303-155">例如：</span><span class="sxs-lookup"><span data-stu-id="5d303-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="5d303-156">時間範圍功能相當於在每個提到的其中一個來源資料表之後插入 'where' 子句。</span><span class="sxs-lookup"><span data-stu-id="5d303-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="5d303-157">`ago(3d)` 表示「三天前」。</span><span class="sxs-lookup"><span data-stu-id="5d303-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="5d303-158">其他時間單位包括小時 (`2h`、`2.5h`)、分鐘 (`25m`) 和秒 (`10s`)。</span><span class="sxs-lookup"><span data-stu-id="5d303-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="5d303-159">其他範例︰</span><span class="sxs-lookup"><span data-stu-id="5d303-159">Other examples:</span></span>

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

<span data-ttu-id="5d303-160">[日期和時間參考](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html)。</span><span class="sxs-lookup"><span data-stu-id="5d303-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="5d303-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html)：選取、重新命名和計算資料行</span><span class="sxs-lookup"><span data-stu-id="5d303-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="5d303-162">使用 [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) ，只挑出您想要的資料行：</span><span class="sxs-lookup"><span data-stu-id="5d303-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="5d303-163">您也可以將資料行重新命名並定義新的資料行︰</span><span class="sxs-lookup"><span data-stu-id="5d303-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="5d303-165">如果資料行名稱是以括號括起來 (如下所示)，就可以包含空格或符號︰`['...']` 或 `["..."]`</span><span class="sxs-lookup"><span data-stu-id="5d303-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="5d303-166">`%` 是很常見的模數運算子。</span><span class="sxs-lookup"><span data-stu-id="5d303-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="5d303-167">`1d` (這是數字 1，再加上 'd') 是一個時間範圍常值，表示一天。</span><span class="sxs-lookup"><span data-stu-id="5d303-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="5d303-168">以下是其他一些時間範圍常值︰`12h`、`30m`、`10s`、`0.01s`。</span><span class="sxs-lookup"><span data-stu-id="5d303-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="5d303-169">`floor` (別名 `bin`) 會將一個值無條件捨去為您提供之基值的最近倍數。</span><span class="sxs-lookup"><span data-stu-id="5d303-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="5d303-170">所以 `floor(aTime, 1s)` 會將時間無條件捨去為最接近的秒數。</span><span class="sxs-lookup"><span data-stu-id="5d303-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="5d303-171">運算式可以包含所有常見的運算子 (`+`、`-`...)，而且有一系列的實用函式。</span><span class="sxs-lookup"><span data-stu-id="5d303-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="5d303-172">Extend</span><span class="sxs-lookup"><span data-stu-id="5d303-172">Extend</span></span>
<span data-ttu-id="5d303-173">如果您只要將資料行加入現有的資料行，請使用 [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html)：</span><span class="sxs-lookup"><span data-stu-id="5d303-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="5d303-174">如果您要保留所有現有的資料行，使用 [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) 比 [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) 精簡。</span><span class="sxs-lookup"><span data-stu-id="5d303-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="5d303-175">轉換為當地時間</span><span class="sxs-lookup"><span data-stu-id="5d303-175">Convert to local time</span></span>

<span data-ttu-id="5d303-176">時間戳記一律是 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="5d303-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="5d303-177">所以如果您位於美國西岸且正好是冬季，則可能如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5d303-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="5d303-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html)：彙總資料列群組</span><span class="sxs-lookup"><span data-stu-id="5d303-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="5d303-179">`Summarize` 會對資料列群組套用指定的「彙總函式」。</span><span class="sxs-lookup"><span data-stu-id="5d303-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="5d303-180">例如，Web 應用程式回應要求所花的時間會在 `duration`欄位中報告。</span><span class="sxs-lookup"><span data-stu-id="5d303-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="5d303-181">我們來看看所有要求的平均回應時間︰</span><span class="sxs-lookup"><span data-stu-id="5d303-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="5d303-182">或者，我們可以將結果分成不同名稱的要求︰</span><span class="sxs-lookup"><span data-stu-id="5d303-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="5d303-183">`Summarize` 會將串流中的資料點收集到 `by` 子句評估為相同的群組中。</span><span class="sxs-lookup"><span data-stu-id="5d303-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="5d303-184">`by` 運算式中的每個值 (即上述範例中的各個運算名稱) 會在結果資料表中各產生一個資料列。</span><span class="sxs-lookup"><span data-stu-id="5d303-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="5d303-185">或者，我們可以依一天當中的時間將結果分組︰</span><span class="sxs-lookup"><span data-stu-id="5d303-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="5d303-186">請注意我們如何使用 `bin` 函式 (也稱為 `floor`)。</span><span class="sxs-lookup"><span data-stu-id="5d303-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="5d303-187">如果我們只使用 `by timestamp`，每個輸入資料列最終都會在它自己的小群組內。</span><span class="sxs-lookup"><span data-stu-id="5d303-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="5d303-188">針對任何連續純量，例如時間或數字，我們必須將連續範圍分割成合理數量的離散值。</span><span class="sxs-lookup"><span data-stu-id="5d303-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="5d303-189">`bin` - 只是熟悉的 `floor` 捨去函式 - 這是最簡單的做法。</span><span class="sxs-lookup"><span data-stu-id="5d303-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="5d303-190">我們可以使用相同的技巧來減少字串的範圍︰</span><span class="sxs-lookup"><span data-stu-id="5d303-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="5d303-191">請注意，您可以在彙總運算式或 by 子句中使用 `name=` 設定結果資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d303-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="5d303-192">計算取樣的資料</span><span class="sxs-lookup"><span data-stu-id="5d303-192">Counting sampled data</span></span>
<span data-ttu-id="5d303-193">`sum(itemCount)` 是用來計算事件的建議彙總。</span><span class="sxs-lookup"><span data-stu-id="5d303-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="5d303-194">在許多情況下，itemCount==1，因此函式只會計算群組中的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="5d303-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="5d303-195">但在進行[取樣](app-insights-sampling.md)時，只有一小部分的原始事件會保留作為 Application Insights 中的資料點，因此您看到的每一個資料點會有 `itemCount` 個事件。</span><span class="sxs-lookup"><span data-stu-id="5d303-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="5d303-196">例如，如果取樣捨棄了 75%的原始事件，則在保留的記錄中 itemCount==4 - 也就是，針對每筆保留的記錄，會有四筆原始記錄。</span><span class="sxs-lookup"><span data-stu-id="5d303-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="5d303-197">調適性取樣在您的應用程式大量使用期間會導致 itemCount 變得更高。</span><span class="sxs-lookup"><span data-stu-id="5d303-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="5d303-198">因此，加總 itemCount 可正確估算事件的原始數目。</span><span class="sxs-lookup"><span data-stu-id="5d303-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="5d303-199">另外還有 `count()` 彙總 (以及計數運算)，適用於您確實想要計算群組中的資料列數目的情況。</span><span class="sxs-lookup"><span data-stu-id="5d303-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="5d303-200">目前提供一系列的 [彙總函式](https://docs.loganalytics.io/learn/tutorials/aggregations.html)。</span><span class="sxs-lookup"><span data-stu-id="5d303-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="5d303-201">製作結果圖表</span><span class="sxs-lookup"><span data-stu-id="5d303-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="5d303-202">根據預設，結果會顯示成資料表︰</span><span class="sxs-lookup"><span data-stu-id="5d303-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="5d303-203">有比資料表檢視更好的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="5d303-203">We can do better than the table view.</span></span> <span data-ttu-id="5d303-204">讓我們使用直條圖選項來看看圖表檢視中的結果︰</span><span class="sxs-lookup"><span data-stu-id="5d303-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![按一下 [圖表]，然後選擇 [直條圖] 並指派 x 和 y 軸](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="5d303-206">請注意，雖然我們並未依時間排序結果 (如資料表顯示中所示），但圖表顯示一律會以正確的順序顯示日期時間。</span><span class="sxs-lookup"><span data-stu-id="5d303-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="5d303-207">時間表</span><span class="sxs-lookup"><span data-stu-id="5d303-207">Timecharts</span></span>
<span data-ttu-id="5d303-208">顯示每小時有多少個事件︰</span><span class="sxs-lookup"><span data-stu-id="5d303-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="5d303-209">選取圖表顯示選項：</span><span class="sxs-lookup"><span data-stu-id="5d303-209">Select the Chart display option:</span></span>

![時間圖](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="5d303-211">多個系列</span><span class="sxs-lookup"><span data-stu-id="5d303-211">Multiple series</span></span>
<span data-ttu-id="5d303-212">`summarize` 子句中的多個運算式會建立多個資料行。</span><span class="sxs-lookup"><span data-stu-id="5d303-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="5d303-213">`by` 子句中的多個運算式會建立多個資料列，每個值組合各有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="5d303-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![依小時和位置的要求資料表](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="5d303-215">依據維度分割圖表</span><span class="sxs-lookup"><span data-stu-id="5d303-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="5d303-216">如果您將具有字串資料行和數值資料行的資料表繪製成圖表，此字串可用於將數值資料分割成不同的點系列。</span><span class="sxs-lookup"><span data-stu-id="5d303-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="5d303-217">如果有一個以上的字串資料行，您可以選擇哪個資料行要做為鑑別子。</span><span class="sxs-lookup"><span data-stu-id="5d303-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![分割分析圖表](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="5d303-219">跳出率</span><span class="sxs-lookup"><span data-stu-id="5d303-219">Bounce rate</span></span>

<span data-ttu-id="5d303-220">將布林值轉換成字串，將它當作鑑別子︰</span><span class="sxs-lookup"><span data-stu-id="5d303-220">Convert a boolean to a string to use it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="5d303-221">顯示多個計量</span><span class="sxs-lookup"><span data-stu-id="5d303-221">Display multiple metrics</span></span>
<span data-ttu-id="5d303-222">如果您將具有多個數值資料行的資料表繪製成圖表，除了時間戳記以外，您可以顯示任何的數值資料行組合。</span><span class="sxs-lookup"><span data-stu-id="5d303-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![分割分析圖表](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="5d303-224">您必須選取 [不分割]，才能選取多個數值資料行。</span><span class="sxs-lookup"><span data-stu-id="5d303-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="5d303-225">您無法依字串資料行分割又同時顯示多個數值資料行。</span><span class="sxs-lookup"><span data-stu-id="5d303-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="5d303-226">每日平均週期</span><span class="sxs-lookup"><span data-stu-id="5d303-226">Daily average cycle</span></span>
<span data-ttu-id="5d303-227">平均一天的使用量如何變化？</span><span class="sxs-lookup"><span data-stu-id="5d303-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="5d303-228">依時間模數一天計算要求 (分類收納成數小時)︰</span><span class="sxs-lookup"><span data-stu-id="5d303-228">Count requests by the time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="5d303-230">請注意，我們目前必須將持續時間轉換成日期時間，才能顯示於折線圖上。</span><span class="sxs-lookup"><span data-stu-id="5d303-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="5d303-231">比較多個每日系列</span><span class="sxs-lookup"><span data-stu-id="5d303-231">Compare multiple daily series</span></span>
<span data-ttu-id="5d303-232">在不同國家/地區內一天當中的使用量如何變化？</span><span class="sxs-lookup"><span data-stu-id="5d303-232">How does usage vary over the time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="5d303-234">繪製分佈圖</span><span class="sxs-lookup"><span data-stu-id="5d303-234">Plot a distribution</span></span>
<span data-ttu-id="5d303-235">有多少個不同長度的工作階段？</span><span class="sxs-lookup"><span data-stu-id="5d303-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="5d303-236">需要最後一行才能轉換成 datetime。</span><span class="sxs-lookup"><span data-stu-id="5d303-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="5d303-237">目前只有圖表的 x 軸是 datetime 時才會顯示為純量。</span><span class="sxs-lookup"><span data-stu-id="5d303-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="5d303-238">`where` 子句會排除單次發生的工作階段 (sessionDuration==0)，並設定 x 軸的長度。</span><span class="sxs-lookup"><span data-stu-id="5d303-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="5d303-239">百分位數</span><span class="sxs-lookup"><span data-stu-id="5d303-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="5d303-240">哪些持續時間範圍涵蓋不同的工作階段百分比？</span><span class="sxs-lookup"><span data-stu-id="5d303-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="5d303-241">使用上述查詢，但取代最後一行︰</span><span class="sxs-lookup"><span data-stu-id="5d303-241">Use the above query, but replace the last line:</span></span>

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

<span data-ttu-id="5d303-242">我們也移除 where 子句中的上限，以便取得正確的數據，包括有多個要求的所有工作階段︰</span><span class="sxs-lookup"><span data-stu-id="5d303-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![結果](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="5d303-244">我們可以從中看到︰</span><span class="sxs-lookup"><span data-stu-id="5d303-244">From which we can see that:</span></span>

* <span data-ttu-id="5d303-245">5% 的工作階段的持續時間小於 3 分鐘 34 秒；</span><span class="sxs-lookup"><span data-stu-id="5d303-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="5d303-246">50% 的工作階段的持續時間小於 36 分鐘；</span><span class="sxs-lookup"><span data-stu-id="5d303-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="5d303-247">5% 的工作階段的持續時間超過 7 天</span><span class="sxs-lookup"><span data-stu-id="5d303-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="5d303-248">若要取得每個國家/地區的個別分解圖，我們只需透過兩個 summarize運算子個別地帶入 client_CountryOrRegion 資料行︰</span><span class="sxs-lookup"><span data-stu-id="5d303-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="5d303-249">Join</span><span class="sxs-lookup"><span data-stu-id="5d303-249">Join</span></span>
<span data-ttu-id="5d303-250">我們可以存取數個資料表，包括要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5d303-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="5d303-251">若要尋找傳回失敗回應之要求的相關例外狀況，我們可以聯結 `session_Id`上的資料表：</span><span class="sxs-lookup"><span data-stu-id="5d303-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="5d303-252">在執行聯結之前，使用 `project` 只選取我們需要的資料行是相當好的做法。</span><span class="sxs-lookup"><span data-stu-id="5d303-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="5d303-253">在相同的子句中，我們會將時間戳記資料行重新命名。</span><span class="sxs-lookup"><span data-stu-id="5d303-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="5d303-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html)︰將結果指派給變數</span><span class="sxs-lookup"><span data-stu-id="5d303-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="5d303-255">使用 `let` 來分隔前一個運算式的各個部分。</span><span class="sxs-lookup"><span data-stu-id="5d303-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="5d303-256">結果不變：</span><span class="sxs-lookup"><span data-stu-id="5d303-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="5d303-257">在分析用戶端中，不要在查詢的各個部分之間插入空白行。</span><span class="sxs-lookup"><span data-stu-id="5d303-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="5d303-258">務必執行所有一切。</span><span class="sxs-lookup"><span data-stu-id="5d303-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="5d303-259">使用 `toscalar` 將單一表格儲存格轉換為值：</span><span class="sxs-lookup"><span data-stu-id="5d303-259">Use `toscalar` to convert a single table cell to a value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="5d303-260">Functions</span><span class="sxs-lookup"><span data-stu-id="5d303-260">Functions</span></span>

<span data-ttu-id="5d303-261">使用 Let 來定義函式︰</span><span class="sxs-lookup"><span data-stu-id="5d303-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="5d303-262">存取巢狀物件</span><span class="sxs-lookup"><span data-stu-id="5d303-262">Accessing nested objects</span></span>
<span data-ttu-id="5d303-263">巢狀物件可以輕鬆地存取。</span><span class="sxs-lookup"><span data-stu-id="5d303-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="5d303-264">例如，在例外狀況串流中，您可能會看到如下的結構化物件︰</span><span class="sxs-lookup"><span data-stu-id="5d303-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![結果](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="5d303-266">您可以選擇您感興趣的屬性來將它平面化︰</span><span class="sxs-lookup"><span data-stu-id="5d303-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="5d303-267">請注意，您必須轉換到適當類型。</span><span class="sxs-lookup"><span data-stu-id="5d303-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="5d303-268">自訂屬性和測量</span><span class="sxs-lookup"><span data-stu-id="5d303-268">Custom properties and measurements</span></span>
<span data-ttu-id="5d303-269">如果您的應用程式要將[自訂維度 (屬性) 和自訂測量](app-insights-api-custom-events-metrics.md#properties)附加到事件，則您會在 `customDimensions` 和 `customMeasurements` 物件看到它們。</span><span class="sxs-lookup"><span data-stu-id="5d303-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="5d303-270">例如，如果您的應用程式包括︰</span><span class="sxs-lookup"><span data-stu-id="5d303-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="5d303-271">若要在分析中擷取這些值︰</span><span class="sxs-lookup"><span data-stu-id="5d303-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="5d303-272">若要驗證自訂維度是否為特定類型︰</span><span class="sxs-lookup"><span data-stu-id="5d303-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="5d303-273">儀表板</span><span class="sxs-lookup"><span data-stu-id="5d303-273">Dashboards</span></span>
<span data-ttu-id="5d303-274">您可以將結果釘選至儀表板，以便結合所有最重要的圖表和資料表。</span><span class="sxs-lookup"><span data-stu-id="5d303-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="5d303-275">[Azure 共用儀表板](app-insights-dashboards.md#share-dashboards)：按一下釘選圖示。</span><span class="sxs-lookup"><span data-stu-id="5d303-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="5d303-276">執行這項作業之前，您必須具有共用儀表板。</span><span class="sxs-lookup"><span data-stu-id="5d303-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="5d303-277">在 Azure 入口網站中，開啟或建立儀表板並按一下 [共用]。</span><span class="sxs-lookup"><span data-stu-id="5d303-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="5d303-278">[Power BI 儀表板](app-insights-export-power-bi.md)︰按一下 [匯出]、[Power BI 查詢]。</span><span class="sxs-lookup"><span data-stu-id="5d303-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="5d303-279">此替代方案的優點是您可以顯示查詢，還有各種來源的其他結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="5d303-280">與匯入的資料結合</span><span class="sxs-lookup"><span data-stu-id="5d303-280">Combine with imported data</span></span>

<span data-ttu-id="5d303-281">儀表板上的分析報告看起來很不錯，但有時候您想要將資料轉譯為更容易消化的表單。</span><span class="sxs-lookup"><span data-stu-id="5d303-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="5d303-282">例如，假設已驗證的使用者在遙測中是依照別名識別。</span><span class="sxs-lookup"><span data-stu-id="5d303-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="5d303-283">您想要在結果中顯示其真實名稱。</span><span class="sxs-lookup"><span data-stu-id="5d303-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="5d303-284">若要這樣做，您只需要有 CSV 檔案從別名對應至真實名稱。</span><span class="sxs-lookup"><span data-stu-id="5d303-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="5d303-285">您可以匯入資料檔案，並且就像任何標準資料表 (要求、例外狀況等等) 一樣使用它。</span><span class="sxs-lookup"><span data-stu-id="5d303-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="5d303-286">單獨查詢它，或是將它與其他資料表聯結。</span><span class="sxs-lookup"><span data-stu-id="5d303-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="5d303-287">例如，如果您有名為 usermap 的資料表，且其中包含 `realName` 和 `userId` 資料行，您即可使用它來轉譯要求遙測中的 `user_AuthenticatedId` 欄位︰</span><span class="sxs-lookup"><span data-stu-id="5d303-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="5d303-288">若要匯入資料表，請在 [結構描述] 刀鋒視窗的 [其他資料來源] 下，依指示上傳資料樣本來新增資料來源。</span><span class="sxs-lookup"><span data-stu-id="5d303-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="5d303-289">然後，您可以使用此定義來上傳資料表。</span><span class="sxs-lookup"><span data-stu-id="5d303-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="5d303-290">匯入功能目前為預覽狀態，所以在 [其他資料來源] 下，您最初會看到 [與我們連絡] 連結。</span><span class="sxs-lookup"><span data-stu-id="5d303-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="5d303-291">請利用此連結來註冊預覽方案，之後，連結會換成 [新增資料來源] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d303-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="5d303-292">資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-292">Tables</span></span>
<span data-ttu-id="5d303-293">從應用程式收到的遙測串流可透過數個資料表來存取。</span><span class="sxs-lookup"><span data-stu-id="5d303-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="5d303-294">每個資料表可用的屬性結構描述會顯示在視窗左邊。</span><span class="sxs-lookup"><span data-stu-id="5d303-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="5d303-295">要求資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-295">Requests table</span></span>
<span data-ttu-id="5d303-296">計算 Web 應用程式的 HTTP 要求數量並依頁面名稱分割︰</span><span class="sxs-lookup"><span data-stu-id="5d303-296">Count HTTP requests to your web app and segment by page name:</span></span>

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="5d303-298">尋找最失敗的要求︰</span><span class="sxs-lookup"><span data-stu-id="5d303-298">Find the requests that fail most:</span></span>

![計算要求數量，依名稱分割](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="5d303-300">自訂事件資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-300">Custom events table</span></span>
<span data-ttu-id="5d303-301">如果您使用 [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) 傳送您自己的事件，則可以從這個資料表查看事件。</span><span class="sxs-lookup"><span data-stu-id="5d303-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="5d303-302">讓我們舉包含下列程式行的應用程式程式碼為例︰</span><span class="sxs-lookup"><span data-stu-id="5d303-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="5d303-303">顯示這些事件的頻率︰</span><span class="sxs-lookup"><span data-stu-id="5d303-303">Display the frequency of these events:</span></span>

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="5d303-305">擷取事件的度量值和維度︰</span><span class="sxs-lookup"><span data-stu-id="5d303-305">Extract measurements and dimensions from the events:</span></span>

![顯示自訂事件的速率](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="5d303-307">自訂度量表</span><span class="sxs-lookup"><span data-stu-id="5d303-307">Custom metrics table</span></span>
<span data-ttu-id="5d303-308">如果您使用 [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) 傳送您自己的度量值，您會在 **customMetrics** 串流中發現它的結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="5d303-309">例如：</span><span class="sxs-lookup"><span data-stu-id="5d303-309">For example:</span></span>  

![Application Insights 分析中的自訂度量](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="5d303-311">在[計量瀏覽器](app-insights-metrics-explorer.md)中，附加到任何遙測類型的所有自訂度量，會連同使用 `TrackMetric()` 傳送的計量一起出現在 [計量] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="5d303-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="5d303-312">但在分析中，自訂度量仍會附加到其所執行的任何一種遙測類型 (事件或要求等)，而且 TrackMetric 所傳送的度量會出現在自己的串流中。</span><span class="sxs-lookup"><span data-stu-id="5d303-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="5d303-313">效能計數器資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-313">Performance counters table</span></span>
<span data-ttu-id="5d303-314">[效能計數器](app-insights-performance-counters.md)會對您顯示應用程式的基本系統度量，例如 CPU、記憶體和網路使用率。</span><span class="sxs-lookup"><span data-stu-id="5d303-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="5d303-315">您可以設定 SDK 來傳送其他計數器，包括您自己的自訂計數器。</span><span class="sxs-lookup"><span data-stu-id="5d303-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="5d303-316">**PerformanceCounters** 結構描述會公開每個效能計數器的 `category`、`counter` 名稱和 `instance` 名稱。</span><span class="sxs-lookup"><span data-stu-id="5d303-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="5d303-317">計數器執行個體名稱只適用於某些效能計數器，而且通常會指出與計數相關的處理程序名稱。</span><span class="sxs-lookup"><span data-stu-id="5d303-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="5d303-318">在每個應用程式的遙測中，您只會看到該應用程式的計數器。</span><span class="sxs-lookup"><span data-stu-id="5d303-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="5d303-319">例如，若要查看哪些計數器可用︰</span><span class="sxs-lookup"><span data-stu-id="5d303-319">For example, to see what counters are available:</span></span>

![Application Insights 分析中的效能計數器](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="5d303-321">若要取得所選期間的可用記憶體圖表︰</span><span class="sxs-lookup"><span data-stu-id="5d303-321">To get a chart of available memory over the selected period:</span></span>

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="5d303-323">和其他遙測一樣，**performanceCounters** 也有 `cloud_RoleInstance` 資料行會指出應用程式執行所在主機機器的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5d303-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="5d303-324">例如，若要比較不同機器上的應用程式效能︰</span><span class="sxs-lookup"><span data-stu-id="5d303-324">For example, to compare the performance of your app on the different machines:</span></span>

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="5d303-326">例外狀況資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-326">Exceptions table</span></span>
<span data-ttu-id="5d303-327">此資料表中有提供[應用程式所報告的例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="5d303-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="5d303-328">若要尋找例外狀況引發時應用程式正在處理的 HTTP 要求，請聯結 operation_Id︰</span><span class="sxs-lookup"><span data-stu-id="5d303-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![在 operation_Id 聯結例外狀況與要求](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="5d303-330">瀏覽器計時資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-330">Browser timings table</span></span>
<span data-ttu-id="5d303-331">`browserTimings` 會顯示使用者的瀏覽器所收集到的頁面載入資料。</span><span class="sxs-lookup"><span data-stu-id="5d303-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="5d303-332">[為應用程式設定用戶端遙測](app-insights-javascript.md)才能看到這些度量。</span><span class="sxs-lookup"><span data-stu-id="5d303-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="5d303-333">結構描述包含[指出頁面載入處理程序之不同階段長度的度量](app-insights-javascript.md#page-load-performance)</span><span class="sxs-lookup"><span data-stu-id="5d303-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="5d303-334">(這些度量不會指出使用者讀取頁面的時間長度)。</span><span class="sxs-lookup"><span data-stu-id="5d303-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="5d303-335">顯示不同頁面的熱門度以及每個頁面的載入時間︰</span><span class="sxs-lookup"><span data-stu-id="5d303-335">Show the popularities of different pages, and load times for each page:</span></span>

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="5d303-337">可用性結果資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-337">Availability results table</span></span>
<span data-ttu-id="5d303-338">`availabilityResults` 會顯示 [Web 測試](app-insights-monitor-web-app-availability.md)的結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="5d303-339">每個測試位置每次執行的測試會分開報告。</span><span class="sxs-lookup"><span data-stu-id="5d303-339">Each run of your tests from each test location is reported separately.</span></span>

![分析中的頁面載入時間](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="5d303-341">相依性資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-341">Dependencies table</span></span>
<span data-ttu-id="5d303-342">包含應用程式對資料庫和 REST API 所發出呼叫的結果，以及對 TrackDependency() 所發出的其他呼叫結果。</span><span class="sxs-lookup"><span data-stu-id="5d303-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="5d303-343">也包含從瀏覽器進行的 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="5d303-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="5d303-344">從瀏覽器進行的 AJAX 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="5d303-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="5d303-345">從伺服器進行的相依性呼叫︰</span><span class="sxs-lookup"><span data-stu-id="5d303-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="5d303-346">如果未安裝 Application Insights 代理程式，則伺服器端相依性結果一律顯示 `success==False`。</span><span class="sxs-lookup"><span data-stu-id="5d303-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="5d303-347">不過，其他資料都正確。</span><span class="sxs-lookup"><span data-stu-id="5d303-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="5d303-348">追蹤資料表</span><span class="sxs-lookup"><span data-stu-id="5d303-348">Traces table</span></span>
<span data-ttu-id="5d303-349">包含應用程式使用 TrackTrace() 或[其他記錄架構](app-insights-asp-net-trace-logs.md)傳送的遙測。</span><span class="sxs-lookup"><span data-stu-id="5d303-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="5d303-350">影片</span><span class="sxs-lookup"><span data-stu-id="5d303-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="5d303-351">進階查詢：</span><span class="sxs-lookup"><span data-stu-id="5d303-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="5d303-352">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d303-352">Next steps</span></span>
* [<span data-ttu-id="5d303-353">分析語言參考</span><span class="sxs-lookup"><span data-stu-id="5d303-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="5d303-354">[SQL 使用者的功能提要](https://aka.ms/sql-analytics)會翻譯成最常見的習慣用語。</span><span class="sxs-lookup"><span data-stu-id="5d303-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
