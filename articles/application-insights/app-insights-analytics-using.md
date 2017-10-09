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
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="15daa-103">使用 Application Insights 中的分析</span><span class="sxs-lookup"><span data-stu-id="15daa-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="15daa-104">[分析](app-insights-analytics.md)是功能強大的搜尋功能 hello [Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="15daa-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="15daa-105">這些分頁說明 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="15daa-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="15daa-106">**[請觀看 hello 簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。</span><span class="sxs-lookup"><span data-stu-id="15daa-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="15daa-107">**[測試模擬資料的磁碟機分析](https://analytics.applicationinsights.io/demo)**如果您的應用程式未尚未傳送資料 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="15daa-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="15daa-108">開啟分析</span><span class="sxs-lookup"><span data-stu-id="15daa-108">Open Analytics</span></span>
<span data-ttu-id="15daa-109">在 Application Insights 中，從您的應用程式的首頁資源，按一下 [分析]。</span><span class="sxs-lookup"><span data-stu-id="15daa-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="15daa-111">hello 內嵌教學課程，可讓您可以執行一些的概念。</span><span class="sxs-lookup"><span data-stu-id="15daa-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="15daa-112">[這裡有更廣泛的教學課程](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="15daa-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="15daa-113">查詢您的遙測</span><span class="sxs-lookup"><span data-stu-id="15daa-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="15daa-114">撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="15daa-114">Write a query</span></span>
![結構描述顯示](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="15daa-116">開頭為 hello 名稱列出 hello 左側的 hello 資料表的所有 (或 hello[範圍](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html)或[union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html)運算子)。</span><span class="sxs-lookup"><span data-stu-id="15daa-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="15daa-117">使用`|`的管線 toocreate[運算子](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html)。</span><span class="sxs-lookup"><span data-stu-id="15daa-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="15daa-118">IntelliSense 會提示您 hello 運算子與 hello 運算式項目，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="15daa-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="15daa-119">按一下資訊圖示，hello （或按 CTRL + 空格鍵） tooget 更長的描述和範例如何 toouse 每個項目。</span><span class="sxs-lookup"><span data-stu-id="15daa-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="15daa-120">請參閱 hello[分析語言教學課程](app-insights-analytics-tour.md)和[語言參考](app-insights-analytics-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="15daa-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="15daa-121">執行查詢</span><span class="sxs-lookup"><span data-stu-id="15daa-121">Run a query</span></span>
![執行查詢](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="15daa-123">您可以在查詢中使用單一分行符號。</span><span class="sxs-lookup"><span data-stu-id="15daa-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="15daa-124">將內部或結尾 hello hello 查詢想 toorun hello 游標。</span><span class="sxs-lookup"><span data-stu-id="15daa-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="15daa-125">請檢查您的查詢 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="15daa-125">Check hello time range of your query.</span></span> <span data-ttu-id="15daa-126">(您可以變更它，或是在查詢中包含您自己的 [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) 子句來覆寫它。)</span><span class="sxs-lookup"><span data-stu-id="15daa-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="15daa-127">按一下 Go toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="15daa-128">請勿在查詢中放置空白行。</span><span class="sxs-lookup"><span data-stu-id="15daa-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="15daa-129">您可以用空白行來分隔一個查詢索引標籤中的數個查詢，讓它們保持分離狀態。</span><span class="sxs-lookup"><span data-stu-id="15daa-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="15daa-130">具有 hello 游標 hello 查詢執行。</span><span class="sxs-lookup"><span data-stu-id="15daa-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="15daa-131">儲存查詢</span><span class="sxs-lookup"><span data-stu-id="15daa-131">Save a query</span></span>
![儲存查詢](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="15daa-133">儲存 hello 目前的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="15daa-133">Save hello current query file.</span></span>
2. <span data-ttu-id="15daa-134">開啟已儲存的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="15daa-134">Open a saved query file.</span></span>
3. <span data-ttu-id="15daa-135">建立新的查詢檔案。</span><span class="sxs-lookup"><span data-stu-id="15daa-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="15daa-136">請參閱 hello 詳細資料</span><span class="sxs-lookup"><span data-stu-id="15daa-136">See hello details</span></span>
<span data-ttu-id="15daa-137">展開任何資料列中 hello 結果 toosee 其完整的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="15daa-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="15daa-138">您可以進一步展開任何屬性的結構化的值-例如，自訂維度或 hello 堆疊中例外狀況的清單。</span><span class="sxs-lookup"><span data-stu-id="15daa-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![展開資料列](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="15daa-140">排列 hello 結果</span><span class="sxs-lookup"><span data-stu-id="15daa-140">Arrange hello results</span></span>
<span data-ttu-id="15daa-141">您可以排序、 篩選、 重新編頁，以及 hello 從您的查詢傳回的結果分組。</span><span class="sxs-lookup"><span data-stu-id="15daa-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="15daa-142">排序、 分組和篩選 hello 瀏覽器中不會重新執行您的查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="15daa-143">它們只重新排列 hello 由最後一個查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="15daa-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="15daa-144">tooperform hello 伺服器，然後傳回 hello 結果，才能處理這些工作撰寫查詢以 hello[排序](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)，[摘要](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html)和[其中](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)運算子。</span><span class="sxs-lookup"><span data-stu-id="15daa-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="15daa-145">挑選 hello 資料行，就如同 toosee，將資料行的標頭 toorearrange，以及調整大小資料行拖曳框線。</span><span class="sxs-lookup"><span data-stu-id="15daa-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![排列資料行](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="15daa-147">排序和篩選項目</span><span class="sxs-lookup"><span data-stu-id="15daa-147">Sort and filter items</span></span>
<span data-ttu-id="15daa-148">按一下 hello 標頭的資料行排序您的結果。</span><span class="sxs-lookup"><span data-stu-id="15daa-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="15daa-149">再次按一下 toosort hello 另一種方式，並按一下第三次 toorevert toohello 原始順序由您的查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="15daa-150">使用 hello 篩選圖示 toonarrow 您的搜尋。</span><span class="sxs-lookup"><span data-stu-id="15daa-150">Use hello filter icon toonarrow your search.</span></span>

![排序和篩選資料行](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="15daa-152">將項目分組</span><span class="sxs-lookup"><span data-stu-id="15daa-152">Group items</span></span>
<span data-ttu-id="15daa-153">toosort 使用一個以上的資料行群組。</span><span class="sxs-lookup"><span data-stu-id="15daa-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="15daa-154">第一次啟用它，並接著將資料行標頭拖曳到 hello hello 資料表上方的空間。</span><span class="sxs-lookup"><span data-stu-id="15daa-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![群組](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="15daa-156">遺漏某些結果？</span><span class="sxs-lookup"><span data-stu-id="15daa-156">Missing some results?</span></span>

<span data-ttu-id="15daa-157">如果您認為您看不到您所預期的所有 hello 結果，有幾個可能的原因。</span><span class="sxs-lookup"><span data-stu-id="15daa-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="15daa-158">**時間範圍篩選**。</span><span class="sxs-lookup"><span data-stu-id="15daa-158">**Time range filter**.</span></span> <span data-ttu-id="15daa-159">根據預設，您只會看到結果 hello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="15daa-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="15daa-160">沒有限制的結果與 hello 來源資料表所擷取的 hello 範圍自動篩選。</span><span class="sxs-lookup"><span data-stu-id="15daa-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="15daa-161">不過，您可以變更 hello 時間範圍篩選器使用 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="15daa-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="15daa-162">您可以取代 hello 自動範圍包括您自己或者[`where  ... timestamp ...`子句](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)到您的查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="15daa-163">例如：</span><span class="sxs-lookup"><span data-stu-id="15daa-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="15daa-164">**結果限制**。</span><span class="sxs-lookup"><span data-stu-id="15daa-164">**Results limit**.</span></span> <span data-ttu-id="15daa-165">沒有限制，大約 10 個 k 上的資料列 hello hello 入口網站所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="15daa-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="15daa-166">如果超出 hello 限制會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="15daa-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="15daa-167">如果發生這種情況，排序結果 hello 資料表中的不會永遠顯示您所有 hello 實際第一個或最後的結果。</span><span class="sxs-lookup"><span data-stu-id="15daa-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="15daa-168">它是很好的作法 tooavoid 達到 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="15daa-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="15daa-169">使用 hello 時間範圍篩選器，或使用運算子，例如：</span><span class="sxs-lookup"><span data-stu-id="15daa-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="15daa-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="15daa-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="15daa-171">take 100</span><span class="sxs-lookup"><span data-stu-id="15daa-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="15daa-172">summarize </span><span class="sxs-lookup"><span data-stu-id="15daa-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="15daa-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="15daa-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="15daa-174">(想要一萬個以上的資料列嗎？</span><span class="sxs-lookup"><span data-stu-id="15daa-174">(Want more than 10k rows?</span></span> <span data-ttu-id="15daa-175">請考慮改用[連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="15daa-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="15daa-176">「分析」是設計來進行分析的，不是用來擷取未經處理的資料。)</span><span class="sxs-lookup"><span data-stu-id="15daa-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="15daa-177">圖表</span><span class="sxs-lookup"><span data-stu-id="15daa-177">Diagrams</span></span>
<span data-ttu-id="15daa-178">選取您想要的圖表類型 hello:</span><span class="sxs-lookup"><span data-stu-id="15daa-178">Select hello type of diagram you'd like:</span></span>

![選取圖表類型](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="15daa-180">如果您有數個資料行的 hello 正確型別時，您可以選擇 hello x 和 y 軸，並依維度 toosplit hello 結果的資料行。</span><span class="sxs-lookup"><span data-stu-id="15daa-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="15daa-181">根據預設，結果一開始會顯示為資料表，並手動選取 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="15daa-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="15daa-182">但是您可以使用 hello[呈現指示詞](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html)結尾 hello 查詢 tooselect 圖表。</span><span class="sxs-lookup"><span data-stu-id="15daa-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="15daa-183">分析診斷</span><span class="sxs-lookup"><span data-stu-id="15daa-183">Analytics diagnostics</span></span>


<span data-ttu-id="15daa-184">在 timechart，如果沒有突然出現尖峰或步驟，在您的資料，您可能看到 hello 列上的反白顯示的點。</span><span class="sxs-lookup"><span data-stu-id="15daa-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="15daa-185">這表示分析診斷已識別的篩選出 hello 突然變更的屬性組合。</span><span class="sxs-lookup"><span data-stu-id="15daa-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="15daa-186">按一下 hello 點 tooget hello 篩選和 toosee hello 篩選的版本的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="15daa-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="15daa-187">這可協助您識別哪些造成的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="15daa-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="15daa-188">深入了解分析診斷</span><span class="sxs-lookup"><span data-stu-id="15daa-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![分析診斷](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="15daa-190">Pin toodashboard</span><span class="sxs-lookup"><span data-stu-id="15daa-190">Pin toodashboard</span></span>
<span data-ttu-id="15daa-191">您可以釘選的圖表或資料表 tooone 您[共用儀表板](app-insights-dashboards.md)-只要按一下 hello 的 pin。</span><span class="sxs-lookup"><span data-stu-id="15daa-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="15daa-192">(您可能需要[升級您的應用程式的定價封裝](app-insights-pricing.md)tooturn 這項功能。)</span><span class="sxs-lookup"><span data-stu-id="15daa-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![按一下 hello 的 pin](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="15daa-194">這表示，當您一起讓您監視 hello 效能或使用 web 服務的儀表板 toohelp，您可以包含相當複雜的分析與 hello 一起其他度量資訊。</span><span class="sxs-lookup"><span data-stu-id="15daa-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="15daa-195">如果有四個或更少的資料行，您可以釘選的資料表 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="15daa-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="15daa-196">只有 hello 前七個資料列會顯示。</span><span class="sxs-lookup"><span data-stu-id="15daa-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="15daa-197">儀表板重新整理</span><span class="sxs-lookup"><span data-stu-id="15daa-197">Dashboard refresh</span></span>
<span data-ttu-id="15daa-198">hello 圖表釘選 toohello 儀表板會重新執行 hello 查詢約每小時自動重新整理。</span><span class="sxs-lookup"><span data-stu-id="15daa-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="15daa-199">您也可以按一下 hello 重新整理 按鈕。</span><span class="sxs-lookup"><span data-stu-id="15daa-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="15daa-200">自動簡化</span><span class="sxs-lookup"><span data-stu-id="15daa-200">Automatic simplifications</span></span>

<span data-ttu-id="15daa-201">當您將其釘選 tooa 儀表板，某些簡單化會套用的 tooa 圖表。</span><span class="sxs-lookup"><span data-stu-id="15daa-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="15daa-202">**時間限制：**查詢會自動限制僅的 toohello 過去 14 天。</span><span class="sxs-lookup"><span data-stu-id="15daa-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="15daa-203">hello 效果是 hello 相同時，如果您的查詢包含`where timestamp > ago(14d)`。</span><span class="sxs-lookup"><span data-stu-id="15daa-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="15daa-204">**分類收納計數限制：**如果顯示圖表具有許多不連續分類收納 （通常是橫條圖），較少擴展的紙匣會自動分組到單一 「 其他 」 的 hello 分類收納。</span><span class="sxs-lookup"><span data-stu-id="15daa-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="15daa-205">例如，下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="15daa-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="15daa-206">在分析中看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="15daa-206">looks like this in Analytics:</span></span>

![具有長尾的圖表](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="15daa-208">但是，當您釘選它 tooa 儀表板，它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="15daa-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![具有有限長條的圖表](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="15daa-210">匯出 tooExcel</span><span class="sxs-lookup"><span data-stu-id="15daa-210">Export tooExcel</span></span>
<span data-ttu-id="15daa-211">執行查詢之後，您可以下載 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="15daa-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="15daa-212">按一下 [匯出] > [Excel]。</span><span class="sxs-lookup"><span data-stu-id="15daa-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="15daa-213">匯出 tooPower BI</span><span class="sxs-lookup"><span data-stu-id="15daa-213">Export tooPower BI</span></span>
<span data-ttu-id="15daa-214">Hello 資料指標放在查詢中，然後選擇 **匯出時，Power BI**。</span><span class="sxs-lookup"><span data-stu-id="15daa-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![從分析 tooPower BI 匯出](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="15daa-216">您在 Power BI 中執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-216">You run hello query in Power BI.</span></span> <span data-ttu-id="15daa-217">您可以設定它 toorefresh 的排程。</span><span class="sxs-lookup"><span data-stu-id="15daa-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="15daa-218">您可以使用 Power BI 來建立儀表板，將從各種來源的資料結合在一起。</span><span class="sxs-lookup"><span data-stu-id="15daa-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="15daa-219">深入了解匯出 tooPower BI</span><span class="sxs-lookup"><span data-stu-id="15daa-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="15daa-220">深層連結</span><span class="sxs-lookup"><span data-stu-id="15daa-220">Deep link</span></span>

<span data-ttu-id="15daa-221">取得連結底下**匯出，共用連結**tooanother 使用者，可以傳送。</span><span class="sxs-lookup"><span data-stu-id="15daa-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="15daa-222">假設 hello 使用者已[存取 tooyour 資源群組](app-insights-resources-roles-access-control.md)，hello 查詢會在 hello 分析 UI 中開啟。</span><span class="sxs-lookup"><span data-stu-id="15daa-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="15daa-223">(在 hello 連結 hello 查詢文字會出現在 「？ q ="、 gzip 壓縮和 base 64 編碼。</span><span class="sxs-lookup"><span data-stu-id="15daa-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="15daa-224">您可以撰寫程式碼 toogenerate 深層連結，您必須提供 toousers。</span><span class="sxs-lookup"><span data-stu-id="15daa-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="15daa-225">不過，hello 建議的方式 toorun 分析從程式碼是使用 hello [REST API](https://dev.applicationinsights.io/)。)</span><span class="sxs-lookup"><span data-stu-id="15daa-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="15daa-226">自動化</span><span class="sxs-lookup"><span data-stu-id="15daa-226">Automation</span></span>

<span data-ttu-id="15daa-227">使用 hello[資料存取 REST API](https://dev.applicationinsights.io/) toorun 分析查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="15daa-228">[例如](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (使用 PowerShell)：</span><span class="sxs-lookup"><span data-stu-id="15daa-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="15daa-229">不同於 hello 分析 UI，hello REST API 不會自動新增的任何時間戳記限制 tooyour 查詢。</span><span class="sxs-lookup"><span data-stu-id="15daa-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="15daa-230">請記住 tooadd 自己 where 子句，tooavoid 取得龐大的回覆。</span><span class="sxs-lookup"><span data-stu-id="15daa-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="15daa-231">匯入資料</span><span class="sxs-lookup"><span data-stu-id="15daa-231">Import data</span></span>

<span data-ttu-id="15daa-232">您可以從 CSV 檔案匯入資料。</span><span class="sxs-lookup"><span data-stu-id="15daa-232">You can import data from a CSV file.</span></span> <span data-ttu-id="15daa-233">通常的使用方式為 tooimport 靜態資料，您可以從您的遙測聯結的資料表。</span><span class="sxs-lookup"><span data-stu-id="15daa-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="15daa-234">比方說，如果您遙測中發現已驗證的使用者別名或模糊化的識別碼，您可以匯入別名 tooreal 名稱對應的資料表。</span><span class="sxs-lookup"><span data-stu-id="15daa-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="15daa-235">Hello 要求遙測執行聯結，您可以在 hello 分析報表中的實際名稱來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="15daa-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="15daa-236">定義資料結構描述</span><span class="sxs-lookup"><span data-stu-id="15daa-236">Define your data schema</span></span>

1. <span data-ttu-id="15daa-237">按一下 [設定] \(在左上方)，然後按一下 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="15daa-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="15daa-238">加入資料來源，hello 指示。</span><span class="sxs-lookup"><span data-stu-id="15daa-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="15daa-239">您要求 toosupply hello 資料，應該包含至少 10 個資料列的範例。</span><span class="sxs-lookup"><span data-stu-id="15daa-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="15daa-240">然後，您會更正 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="15daa-240">You then correct hello schema.</span></span>

<span data-ttu-id="15daa-241">這會定義資料來源，然後您可以使用 tooimport 個別資料表。</span><span class="sxs-lookup"><span data-stu-id="15daa-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="15daa-242">匯入資料表</span><span class="sxs-lookup"><span data-stu-id="15daa-242">Import a table</span></span>

1. <span data-ttu-id="15daa-243">從 hello 清單中，開啟您的資料來源定義。</span><span class="sxs-lookup"><span data-stu-id="15daa-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="15daa-244">按一下 [上傳]，並遵循 hello 指示 tooupload hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="15daa-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="15daa-245">這項作業包括呼叫 tooa REST API，因此容易 tooautomate。</span><span class="sxs-lookup"><span data-stu-id="15daa-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="15daa-246">您的資料表現在已可在「分析」查詢中使用。</span><span class="sxs-lookup"><span data-stu-id="15daa-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="15daa-247">它會顯示在「分析」中</span><span class="sxs-lookup"><span data-stu-id="15daa-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="15daa-248">使用 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="15daa-248">Use hello table</span></span>

<span data-ttu-id="15daa-249">假設您的資料來源定義稱為 `usermap`，而它包含 `realName` 和 `user_AuthenticatedId` 這兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="15daa-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="15daa-250">hello`requests`資料表也有一個名為變數`user_AuthenticatedId`，因此很容易 toojoin 它們：</span><span class="sxs-lookup"><span data-stu-id="15daa-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="15daa-251">hello 產生資料表的要求有額外的資料行， `realName`。</span><span class="sxs-lookup"><span data-stu-id="15daa-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="15daa-252">從 LogStash 匯入</span><span class="sxs-lookup"><span data-stu-id="15daa-252">Import from LogStash</span></span>

<span data-ttu-id="15daa-253">如果您使用[LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html)，您可以使用分析 tooquery 記錄。</span><span class="sxs-lookup"><span data-stu-id="15daa-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="15daa-254">使用 hello[管道到分析資料的外掛程式](https://github.com/Microsoft/logstash-output-application-insights)。</span><span class="sxs-lookup"><span data-stu-id="15daa-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="15daa-255">影片</span><span class="sxs-lookup"><span data-stu-id="15daa-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

