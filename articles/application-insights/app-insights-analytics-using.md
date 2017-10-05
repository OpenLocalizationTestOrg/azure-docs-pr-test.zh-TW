---
title: "使用分析 - 強大的 Azure Application Insights 搜尋工具 | Microsoft Docs"
description: "使用分析，這是強大的 Application Insights 診斷搜尋工具。 "
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
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="68007-103">使用 Application Insights 中的分析</span><span class="sxs-lookup"><span data-stu-id="68007-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="68007-104">[分析](app-insights-analytics.md)是 [Application Insights](app-insights-overview.md) 的強大搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="68007-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="68007-105">這些分頁說明 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="68007-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="68007-106">**[觀看簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。</span><span class="sxs-lookup"><span data-stu-id="68007-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="68007-107">如果您的應用程式還未將資料傳送至 Application Insights，則**[在我們的模擬資料上測試分析](https://analytics.applicationinsights.io/demo)**。</span><span class="sxs-lookup"><span data-stu-id="68007-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="68007-108">開啟分析</span><span class="sxs-lookup"><span data-stu-id="68007-108">Open Analytics</span></span>
<span data-ttu-id="68007-109">在 Application Insights 中，從您的應用程式的首頁資源，按一下 [分析]。</span><span class="sxs-lookup"><span data-stu-id="68007-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="68007-111">內嵌教學課程會提供您一些可執行作業的概念。</span><span class="sxs-lookup"><span data-stu-id="68007-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="68007-112">[這裡有更廣泛的教學課程](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="68007-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="68007-113">查詢您的遙測</span><span class="sxs-lookup"><span data-stu-id="68007-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="68007-114">撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="68007-114">Write a query</span></span>
![結構描述顯示](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="68007-116">以任何列在左側的資料表名稱 (或 [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) 或 [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) 運算子) 開頭。</span><span class="sxs-lookup"><span data-stu-id="68007-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="68007-117">使用 `|` 建立 [運算子](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html)的直立線符號。</span><span class="sxs-lookup"><span data-stu-id="68007-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="68007-118">IntelliSense 會向您提示您可使用的運算子和運算式元素。</span><span class="sxs-lookup"><span data-stu-id="68007-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="68007-119">按一下資訊圖示 (或按 CTRL+Space)，即可獲得更長的描述和每個元素的使用方式範例。</span><span class="sxs-lookup"><span data-stu-id="68007-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="68007-120">請參閱[分析語言教學課程](app-insights-analytics-tour.md)和[語言參考](app-insights-analytics-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="68007-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="68007-121">執行查詢</span><span class="sxs-lookup"><span data-stu-id="68007-121">Run a query</span></span>
![執行查詢](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="68007-123">您可以在查詢中使用單一分行符號。</span><span class="sxs-lookup"><span data-stu-id="68007-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="68007-124">將游標放在您要執行的查詢內部或結尾。</span><span class="sxs-lookup"><span data-stu-id="68007-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="68007-125">檢查查詢的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="68007-125">Check the time range of your query.</span></span> <span data-ttu-id="68007-126">(您可以變更它，或是在查詢中包含您自己的 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 子句來覆寫它。)</span><span class="sxs-lookup"><span data-stu-id="68007-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="68007-127">按一下 [執行] 來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="68007-128">請勿在查詢中放置空白行。</span><span class="sxs-lookup"><span data-stu-id="68007-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="68007-129">您可以用空白行來分隔一個查詢索引標籤中的數個查詢，讓它們保持分離狀態。</span><span class="sxs-lookup"><span data-stu-id="68007-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="68007-130">只會執行游標所在的查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="68007-131">儲存查詢</span><span class="sxs-lookup"><span data-stu-id="68007-131">Save a query</span></span>
![儲存查詢](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="68007-133">儲存目前的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="68007-133">Save the current query file.</span></span>
2. <span data-ttu-id="68007-134">開啟已儲存的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="68007-134">Open a saved query file.</span></span>
3. <span data-ttu-id="68007-135">建立新的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="68007-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="68007-136">請參閱詳細資料</span><span class="sxs-lookup"><span data-stu-id="68007-136">See the details</span></span>
<span data-ttu-id="68007-137">展開結果中的任何資料列，以查看其完整屬性清單。</span><span class="sxs-lookup"><span data-stu-id="68007-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="68007-138">您可以進一步展開任屬於何結構化值的屬性 - 例如，自訂維度或例外狀況中的堆疊清單。</span><span class="sxs-lookup"><span data-stu-id="68007-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![展開資料列](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="68007-140">排列結果</span><span class="sxs-lookup"><span data-stu-id="68007-140">Arrange the results</span></span>
<span data-ttu-id="68007-141">您可以排序、篩選、分頁和分組查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="68007-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="68007-142">在瀏覽器中排序、分組和篩選不會重新執行查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="68007-143">這些作業只會重新排列最後一個查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="68007-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="68007-144">若要在傳回結果之前，在伺服器中執行這些工作，請使用 [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)、[summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 和 [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 運算子撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="68007-145">挑選您想要查看的資料行，拖曳資料行標頭進行重新排列，然後拖曳其框線以調整資料行的大小。</span><span class="sxs-lookup"><span data-stu-id="68007-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![排列資料行](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="68007-147">排序和篩選項目</span><span class="sxs-lookup"><span data-stu-id="68007-147">Sort and filter items</span></span>
<span data-ttu-id="68007-148">按一下資料行的標頭來排序結果。</span><span class="sxs-lookup"><span data-stu-id="68007-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="68007-149">再次按一下以其他方式排序，而第三次按一下即可還原成查詢所傳回的原始順序。</span><span class="sxs-lookup"><span data-stu-id="68007-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="68007-150">使用篩選圖示縮小搜尋範圍。</span><span class="sxs-lookup"><span data-stu-id="68007-150">Use the filter icon to narrow your search.</span></span>

![排序和篩選資料行](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="68007-152">將項目分組</span><span class="sxs-lookup"><span data-stu-id="68007-152">Group items</span></span>
<span data-ttu-id="68007-153">若要依照多個資料行排序，請使用群組。</span><span class="sxs-lookup"><span data-stu-id="68007-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="68007-154">請先啟用它，接著將資料行標頭拖曳到資料表上方的空間。</span><span class="sxs-lookup"><span data-stu-id="68007-154">First enable it, and then drag column headers into the space above the table.</span></span>

![群組](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="68007-156">遺漏某些結果？</span><span class="sxs-lookup"><span data-stu-id="68007-156">Missing some results?</span></span>

<span data-ttu-id="68007-157">如果您認為沒有看到所預期的全部結果，則有一些可能的原因。</span><span class="sxs-lookup"><span data-stu-id="68007-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="68007-158">**時間範圍篩選**。</span><span class="sxs-lookup"><span data-stu-id="68007-158">**Time range filter**.</span></span> <span data-ttu-id="68007-159">根據預設，您只會看到過去 24 小時內的結果。</span><span class="sxs-lookup"><span data-stu-id="68007-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="68007-160">系統提供一個自動篩選，會限制從來源資料表中擷取的結果範圍。</span><span class="sxs-lookup"><span data-stu-id="68007-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="68007-161">不過，您可以使用下拉式功能表來變更時間範圍篩選。</span><span class="sxs-lookup"><span data-stu-id="68007-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="68007-162">或是在查詢中包含您自己的 [`where  ... timestamp ...` 子句](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)來覆寫自動範圍。</span><span class="sxs-lookup"><span data-stu-id="68007-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="68007-163">例如：</span><span class="sxs-lookup"><span data-stu-id="68007-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="68007-164">**結果限制**。</span><span class="sxs-lookup"><span data-stu-id="68007-164">**Results limit**.</span></span> <span data-ttu-id="68007-165">從入口網站所傳回的結果有大約 1 萬個資料列的限制。</span><span class="sxs-lookup"><span data-stu-id="68007-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="68007-166">如果超過此限制，就會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="68007-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="68007-167">如果發生這種情況，排序資料表中的結果不一定會顯示所有實際的第一個或最後一個結果。</span><span class="sxs-lookup"><span data-stu-id="68007-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="68007-168">最好避免達到限制。</span><span class="sxs-lookup"><span data-stu-id="68007-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="68007-169">請使用時間範圍篩選或使用運算子，例如：</span><span class="sxs-lookup"><span data-stu-id="68007-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="68007-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="68007-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="68007-171">take 100</span><span class="sxs-lookup"><span data-stu-id="68007-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="68007-172">summarize </span><span class="sxs-lookup"><span data-stu-id="68007-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="68007-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="68007-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="68007-174">(想要一萬個以上的資料列嗎？</span><span class="sxs-lookup"><span data-stu-id="68007-174">(Want more than 10k rows?</span></span> <span data-ttu-id="68007-175">請考慮改用[連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="68007-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="68007-176">「分析」是設計來進行分析的，不是用來擷取未經處理的資料。)</span><span class="sxs-lookup"><span data-stu-id="68007-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="68007-177">圖表</span><span class="sxs-lookup"><span data-stu-id="68007-177">Diagrams</span></span>
<span data-ttu-id="68007-178">選取您想要的圖表類型︰</span><span class="sxs-lookup"><span data-stu-id="68007-178">Select the type of diagram you'd like:</span></span>

![選取圖表類型](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="68007-180">如果您有數個正確類型的資料行，您可以選擇 x 和 y 軸，以及一個資料行的維度來據以分割結果。</span><span class="sxs-lookup"><span data-stu-id="68007-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="68007-181">根據預設，結果一開始會顯示為資料表，而您會手動選取圖表。</span><span class="sxs-lookup"><span data-stu-id="68007-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="68007-182">但您可以在查詢結尾使用 [Render 指示詞](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) 以選取圖表。</span><span class="sxs-lookup"><span data-stu-id="68007-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="68007-183">分析診斷</span><span class="sxs-lookup"><span data-stu-id="68007-183">Analytics diagnostics</span></span>


<span data-ttu-id="68007-184">在時間圖表上，如果您的資料突然激增或升級，您可能會在線上看到反白顯示的點。</span><span class="sxs-lookup"><span data-stu-id="68007-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="68007-185">這表示分析診斷已識別出可將突然變更篩選掉的屬性組合。</span><span class="sxs-lookup"><span data-stu-id="68007-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="68007-186">按一下點可取得篩選條件的詳細資料，以及查看篩選的版本。</span><span class="sxs-lookup"><span data-stu-id="68007-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="68007-187">這可能有助於您找出造成變更的原因。</span><span class="sxs-lookup"><span data-stu-id="68007-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="68007-188">深入了解分析診斷</span><span class="sxs-lookup"><span data-stu-id="68007-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![分析診斷](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="68007-190">釘選到儀表板</span><span class="sxs-lookup"><span data-stu-id="68007-190">Pin to dashboard</span></span>
<span data-ttu-id="68007-191">您可以將圖表或資料表釘選至您的其中一個[共用儀表板](app-insights-dashboards.md) - 只要按一下 [釘選]。</span><span class="sxs-lookup"><span data-stu-id="68007-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="68007-192">(您可能需要[升級應用程式的資費套餐](app-insights-pricing.md)才能開啟此功能。)</span><span class="sxs-lookup"><span data-stu-id="68007-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![按一下 [釘選]](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="68007-194">這表示，當您組建出儀表板來協助您監控 Web 服務的效能或使用量時，您可以在其中加入相當複雜的分析以及其他度量。</span><span class="sxs-lookup"><span data-stu-id="68007-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="68007-195">如果資料表有四個或更少的資料行，即可將該資料表釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="68007-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="68007-196">只會顯示前七個資料列。</span><span class="sxs-lookup"><span data-stu-id="68007-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="68007-197">儀表板重新整理</span><span class="sxs-lookup"><span data-stu-id="68007-197">Dashboard refresh</span></span>
<span data-ttu-id="68007-198">釘選到儀表板的圖表大約每小時會重新執行一次查詢，來自動重新整理。</span><span class="sxs-lookup"><span data-stu-id="68007-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="68007-199">您也可以按一下 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="68007-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="68007-200">自動簡化</span><span class="sxs-lookup"><span data-stu-id="68007-200">Automatic simplifications</span></span>

<span data-ttu-id="68007-201">當您將圖表釘選到儀表板時，圖表會套用某些簡化效果。</span><span class="sxs-lookup"><span data-stu-id="68007-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="68007-202">**時間限制：**查詢會自動限制為過去 14 天。</span><span class="sxs-lookup"><span data-stu-id="68007-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="68007-203">效果就像您的查詢包含 `where timestamp > ago(14d)` 一樣。</span><span class="sxs-lookup"><span data-stu-id="68007-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="68007-204">**量化計數限制：**如果您顯示的是有許多不連續量化的圖表 (通常是長條圖)，所佔比例較少的量化會自動分組到單一的「其他」量化。</span><span class="sxs-lookup"><span data-stu-id="68007-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="68007-205">例如，下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="68007-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="68007-206">在分析中看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="68007-206">looks like this in Analytics:</span></span>

![具有長尾的圖表](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="68007-208">但是，當您將它釘選到儀表板時，它看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="68007-208">but when you pin it to a dashboard, it looks like this:</span></span>

![具有有限長條的圖表](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="68007-210">匯出至 Excel</span><span class="sxs-lookup"><span data-stu-id="68007-210">Export to Excel</span></span>
<span data-ttu-id="68007-211">執行查詢之後，您可以下載 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="68007-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="68007-212">按一下 [匯出] > [Excel]。</span><span class="sxs-lookup"><span data-stu-id="68007-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="68007-213">匯出至 Power BI</span><span class="sxs-lookup"><span data-stu-id="68007-213">Export to Power BI</span></span>
<span data-ttu-id="68007-214">將游標放在查詢中，然後選擇 [匯出] > [Power BI]。</span><span class="sxs-lookup"><span data-stu-id="68007-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![從分析匯出至 Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="68007-216">您可在 Power BI 中執行查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-216">You run the query in Power BI.</span></span> <span data-ttu-id="68007-217">您可以將它設定為依照排程重新整理。</span><span class="sxs-lookup"><span data-stu-id="68007-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="68007-218">您可以使用 Power BI 來建立儀表板，將從各種來源的資料結合在一起。</span><span class="sxs-lookup"><span data-stu-id="68007-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="68007-219">深入了解如何匯出至 Power BI</span><span class="sxs-lookup"><span data-stu-id="68007-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="68007-220">深層連結</span><span class="sxs-lookup"><span data-stu-id="68007-220">Deep link</span></span>

<span data-ttu-id="68007-221">在 [匯出] > [共用連結] 底下取得您可以傳送給另一位使用者的連結。</span><span class="sxs-lookup"><span data-stu-id="68007-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="68007-222">如果該使用者[能夠存取您的資源群組](app-insights-resources-roles-access-control.md)，該查詢就會在「分析」UI 中開啟。</span><span class="sxs-lookup"><span data-stu-id="68007-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="68007-223">(在該連結中，查詢文字會顯示在 "?q=" 之後，以 gzip 格式壓縮並採用 Base-64 編碼。</span><span class="sxs-lookup"><span data-stu-id="68007-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="68007-224">您可以撰寫程式碼來產生要提供給使用者的深層連結。</span><span class="sxs-lookup"><span data-stu-id="68007-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="68007-225">不過，建議的方式是使用 [REST API](https://dev.applicationinsights.io/) 從程式碼執行「分析」。)</span><span class="sxs-lookup"><span data-stu-id="68007-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="68007-226">自動化</span><span class="sxs-lookup"><span data-stu-id="68007-226">Automation</span></span>

<span data-ttu-id="68007-227">請使用[資料存取 REST API](https://dev.applicationinsights.io/) 來執行「分析」查詢。</span><span class="sxs-lookup"><span data-stu-id="68007-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="68007-228">[例如](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (使用 PowerShell)：</span><span class="sxs-lookup"><span data-stu-id="68007-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="68007-229">與「分析」UI 不同，REST API 並不會在您的查詢中自動新增任何時間戳記限制。</span><span class="sxs-lookup"><span data-stu-id="68007-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="68007-230">請記得新增您自己的 where 子句，以避免收到大量回應。</span><span class="sxs-lookup"><span data-stu-id="68007-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="68007-231">匯入資料</span><span class="sxs-lookup"><span data-stu-id="68007-231">Import data</span></span>

<span data-ttu-id="68007-232">您可以從 CSV 檔案匯入資料。</span><span class="sxs-lookup"><span data-stu-id="68007-232">You can import data from a CSV file.</span></span> <span data-ttu-id="68007-233">典型的用法是從您的遙測匯入可以與資料表聯結的靜態資料。</span><span class="sxs-lookup"><span data-stu-id="68007-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="68007-234">例如，如果已驗證的使用者在您的遙測中是由別名或經混淆處理的識別碼識別，則您可以匯入一個將別名與真名對應的資料表。</span><span class="sxs-lookup"><span data-stu-id="68007-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="68007-235">透過對要求遙測執行聯結，您就可以在「分析」報表中依使用者的真名來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="68007-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="68007-236">定義資料結構描述</span><span class="sxs-lookup"><span data-stu-id="68007-236">Define your data schema</span></span>

1. <span data-ttu-id="68007-237">按一下 [設定] \(在左上方)，然後按一下 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="68007-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="68007-238">依照指示，新增資料來源。</span><span class="sxs-lookup"><span data-stu-id="68007-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="68007-239">系統會要求您提供資料範例，此範例應該至少包含 10 個資料列。</span><span class="sxs-lookup"><span data-stu-id="68007-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="68007-240">接著，您需更正結構描述。</span><span class="sxs-lookup"><span data-stu-id="68007-240">You then correct the schema.</span></span>

<span data-ttu-id="68007-241">這定義了資料來源，您可以接著使用它來匯入個別資料表。</span><span class="sxs-lookup"><span data-stu-id="68007-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="68007-242">匯入資料表</span><span class="sxs-lookup"><span data-stu-id="68007-242">Import a table</span></span>

1. <span data-ttu-id="68007-243">從清單中開啟您的資料來源定義。</span><span class="sxs-lookup"><span data-stu-id="68007-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="68007-244">按一下 [上傳]，然後依照指示將資料表上傳。</span><span class="sxs-lookup"><span data-stu-id="68007-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="68007-245">這包含對 REST API 的呼叫，因此相當容易自動化。</span><span class="sxs-lookup"><span data-stu-id="68007-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="68007-246">您的資料表現在已可在「分析」查詢中使用。</span><span class="sxs-lookup"><span data-stu-id="68007-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="68007-247">它會顯示在「分析」中</span><span class="sxs-lookup"><span data-stu-id="68007-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="68007-248">使用資料表</span><span class="sxs-lookup"><span data-stu-id="68007-248">Use the table</span></span>

<span data-ttu-id="68007-249">假設您的資料來源定義稱為 `usermap`，而它包含 `realName` 和 `user_AuthenticatedId` 這兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="68007-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="68007-250">`requests` 資料表也有一個名為 `user_AuthenticatedId` 的欄位，因此可以很容易將它們聯結：</span><span class="sxs-lookup"><span data-stu-id="68007-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="68007-251">產生的要求資料表會有一個額外的資料行 `realName`。</span><span class="sxs-lookup"><span data-stu-id="68007-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="68007-252">從 LogStash 匯入</span><span class="sxs-lookup"><span data-stu-id="68007-252">Import from LogStash</span></span>

<span data-ttu-id="68007-253">如果您使用 [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html)，您就可以使用「分析」來查詢您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="68007-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="68007-254">請使用[透過管道將資料傳送到分析的外掛程式](https://github.com/Microsoft/logstash-output-application-insights)。</span><span class="sxs-lookup"><span data-stu-id="68007-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="68007-255">影片</span><span class="sxs-lookup"><span data-stu-id="68007-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

