---
title: "Azure 搜尋服務的搜尋流量分析 | Microsoft Docs"
description: "啟用 Azure 搜尋服務 (Microsoft Azure 上裝載的雲端搜尋服務) 的搜尋流量分析，來深入分析您的使用者與資料。"
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="b80a5-103">什麼是搜尋流量分析</span><span class="sxs-lookup"><span data-stu-id="b80a5-103">What is search traffic analytics</span></span>
<span data-ttu-id="b80a5-104">搜尋流量分析是一種模式，可用來實作搜尋服務的意見反應管道。</span><span class="sxs-lookup"><span data-stu-id="b80a5-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="b80a5-105">這個模式描述必要的資料，以及如何使用監視多平台服務中的業界領導者 Application Insights 來加以收集。</span><span class="sxs-lookup"><span data-stu-id="b80a5-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="b80a5-106">搜尋流量分析可讓您掌握您的搜尋服務，並深入分析您的使用者及其行為。</span><span class="sxs-lookup"><span data-stu-id="b80a5-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="b80a5-107">擁有使用者選擇項目的相關資料，您所做的決定就能夠進一步改善搜尋體驗，並且在結果不如預期時予以中斷。</span><span class="sxs-lookup"><span data-stu-id="b80a5-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="b80a5-108">Azure 搜尋服務所提供的遙測解決方案可整合 Azure Application Insights 和 Power BI，以提供深入的監視和追蹤。</span><span class="sxs-lookup"><span data-stu-id="b80a5-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="b80a5-109">因為只能透過 API 與 Azure 搜尋服務進行互動，必須遵循這個頁面中的指示，由開發人員使用搜尋將遙測進行實作。</span><span class="sxs-lookup"><span data-stu-id="b80a5-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="b80a5-110">識別相關的搜尋資料</span><span class="sxs-lookup"><span data-stu-id="b80a5-110">Identify the relevant search data</span></span>

<span data-ttu-id="b80a5-111">如需取得實用的搜尋計量，就必須從搜尋應用程式的使用者記錄一些訊號。</span><span class="sxs-lookup"><span data-stu-id="b80a5-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="b80a5-112">這些訊號代表使用者感興趣且認為與其需求相關的內容。</span><span class="sxs-lookup"><span data-stu-id="b80a5-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="b80a5-113">搜尋流量分析需要兩個訊號︰</span><span class="sxs-lookup"><span data-stu-id="b80a5-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="b80a5-114">使用者產生的搜尋事件︰僅使用者所起始的搜尋查詢才有趣。</span><span class="sxs-lookup"><span data-stu-id="b80a5-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="b80a5-115">用來填入 Facet、其他內容或任何內部資訊的搜尋要求並不重要，而且還會扭曲和偏差結果。</span><span class="sxs-lookup"><span data-stu-id="b80a5-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="b80a5-116">使用者產生的點選事件︰透過此文件中的點選，我們意指選取搜尋查詢所傳回之特定搜尋結果的使用者。</span><span class="sxs-lookup"><span data-stu-id="b80a5-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="b80a5-117">點選通常表示文件為特定搜尋查詢的相關結果。</span><span class="sxs-lookup"><span data-stu-id="b80a5-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="b80a5-118">使用相互關聯的識別碼將搜尋和點選事件進行連結，就可以分析您應用程式上的使用者行為。</span><span class="sxs-lookup"><span data-stu-id="b80a5-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="b80a5-119">僅使用搜尋流量記錄並無法取得這些搜尋深入分析。</span><span class="sxs-lookup"><span data-stu-id="b80a5-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="b80a5-120">如何實作搜尋流量分析</span><span class="sxs-lookup"><span data-stu-id="b80a5-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="b80a5-121">必須從搜尋應用程式收集前一節所述的訊號，因為使用者會與其進行互動。</span><span class="sxs-lookup"><span data-stu-id="b80a5-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="b80a5-122">Application Insights 是可延伸的監視解決方案，適用於多個平台，並具有彈性的檢測選項。</span><span class="sxs-lookup"><span data-stu-id="b80a5-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="b80a5-123">使用 Application Insights 可讓您充分利用 Azure 搜尋服務所建立的 Power BI 搜尋報告，使資料分析更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="b80a5-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="b80a5-124">在 Azure 搜尋服務的[入口網站](https://portal.azure.com)頁面中，搜尋流量分析刀鋒視窗包含了遵循此遙測模式的小祕技。</span><span class="sxs-lookup"><span data-stu-id="b80a5-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="b80a5-125">您也可以選取或建立 Application Insights 資源，並查看必要的資料，這些全都放在同一個位置。</span><span class="sxs-lookup"><span data-stu-id="b80a5-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![搜尋流量分析指示][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="b80a5-127">1.選取 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="b80a5-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="b80a5-128">如果您還沒有 Application Insights 資源，則必須選取 Application Insights 資源後，才可以加以使用或建立。</span><span class="sxs-lookup"><span data-stu-id="b80a5-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="b80a5-129">您可以使用已在使用中的資源，才可記錄必要的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="b80a5-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="b80a5-130">在建立新的 Application Insights 資源時，所有應用程式類型都適用於這種情況。</span><span class="sxs-lookup"><span data-stu-id="b80a5-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="b80a5-131">選取最適合您所使用平台的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="b80a5-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="b80a5-132">您需要檢測金鑰來建立您應用程式的遙測用戶端。</span><span class="sxs-lookup"><span data-stu-id="b80a5-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="b80a5-133">您可以從 Application Insights 入口網站儀表板取得，或可以在搜尋流量分析頁面上，選取您想要使用的執行個體來加以取得。</span><span class="sxs-lookup"><span data-stu-id="b80a5-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="b80a5-134">2.檢測應用程式</span><span class="sxs-lookup"><span data-stu-id="b80a5-134">2. Instrument your application</span></span>

<span data-ttu-id="b80a5-135">在此階段中，您可以使用上述步驟中建立的 Application Insights 資源，將自己的搜尋應用程式進行檢測。</span><span class="sxs-lookup"><span data-stu-id="b80a5-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="b80a5-136">這個程序有四個步驟︰</span><span class="sxs-lookup"><span data-stu-id="b80a5-136">There are four steps to this process:</span></span>

<span data-ttu-id="b80a5-137">**I.建立用戶端遙測** 這是將事件傳送至 Application Insights 資源的物件。</span><span class="sxs-lookup"><span data-stu-id="b80a5-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="b80a5-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="b80a5-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="b80a5-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b80a5-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="b80a5-140">如需了解其他語言和平台，請參閱完整的[清單](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)。</span><span class="sxs-lookup"><span data-stu-id="b80a5-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="b80a5-141">**II.要求相互關聯的搜尋識別碼** 若要透過點選將搜尋要求相互關聯，則必須擁有與這兩個不同事件相關的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="b80a5-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="b80a5-142">當您使用標頭進行要求時，Azure 搜尋服務會為您提供搜尋識別碼︰</span><span class="sxs-lookup"><span data-stu-id="b80a5-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="b80a5-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="b80a5-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="b80a5-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b80a5-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="b80a5-145">**III.記錄搜尋事件**</span><span class="sxs-lookup"><span data-stu-id="b80a5-145">**III. Log Search events**</span></span>

<span data-ttu-id="b80a5-146">每當使用者發出搜尋要求時，您應該將其記錄為搜尋事件，並包含下列關於 Application Insights 自訂事件的結構描述︰</span><span class="sxs-lookup"><span data-stu-id="b80a5-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="b80a5-147">**ServiceName**：(字串) 搜尋服務名稱 **SearchId**：(GUID) 搜尋查詢的唯一識別碼 (包含在搜尋回應中) **IndexName**︰(字串) 要查詢的搜尋服務索引 **QueryTerms**：(字串) 使用者所輸入的搜尋詞彙 **ResultCount**︰(int) 所傳回的文件數目 (包含在搜尋回應中) **ScoringProfile**︰(字串) 所使用的評分設定檔名稱 (如果有)</span><span class="sxs-lookup"><span data-stu-id="b80a5-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="b80a5-148">將 $count=true 新增至搜尋查詢，要求使用者所產生查詢的計數。</span><span class="sxs-lookup"><span data-stu-id="b80a5-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="b80a5-149">請在[這裡](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)參閱詳細資訊</span><span class="sxs-lookup"><span data-stu-id="b80a5-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="b80a5-150">請記得，務必只記錄使用者所產生的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="b80a5-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="b80a5-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="b80a5-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="b80a5-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b80a5-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="b80a5-153">**IV.記錄點選事件**</span><span class="sxs-lookup"><span data-stu-id="b80a5-153">**IV. Log Click events**</span></span>

<span data-ttu-id="b80a5-154">每當使用者點選文件時，必須記錄這個訊號才可進行搜尋分析。</span><span class="sxs-lookup"><span data-stu-id="b80a5-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="b80a5-155">使用 Application Insights 自訂事件，記錄包含下列結構描述的這些事件：</span><span class="sxs-lookup"><span data-stu-id="b80a5-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="b80a5-156">**ServiceName**：(字串) 搜尋服務名稱 **SearchId**：(GUID) 相關搜尋查詢的唯一識別碼 **DocId**：(字串) 文件識別碼 **Position**(int) 文件在搜尋結果頁面中的排名</span><span class="sxs-lookup"><span data-stu-id="b80a5-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="b80a5-157">位置是指您應用程式中的基本順序。</span><span class="sxs-lookup"><span data-stu-id="b80a5-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="b80a5-158">您可以自由地設定這個數字 (只要它一律相同) 以便進行比較。</span><span class="sxs-lookup"><span data-stu-id="b80a5-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="b80a5-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="b80a5-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="b80a5-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b80a5-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="b80a5-161">3.使用 Power BI Desktop 進行分析</span><span class="sxs-lookup"><span data-stu-id="b80a5-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="b80a5-162">在您完成檢測您的應用程式，並確認您的應用程式正確地連線至 Application Insights 之後，可以使用 Azure 搜尋服務針對 Power BI Desktop 所建立的預先定義範本。</span><span class="sxs-lookup"><span data-stu-id="b80a5-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="b80a5-163">此範本包含圖表和資料表，可幫助您制定更明智的決策，以改善您的搜尋效能和相關性。</span><span class="sxs-lookup"><span data-stu-id="b80a5-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="b80a5-164">若要將 Power BI Desktop 範本具現化，您需要三項 Application Insights 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b80a5-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="b80a5-165">當您選取要使用的資源時，可在搜尋流量分析頁面上找到這項資料</span><span class="sxs-lookup"><span data-stu-id="b80a5-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![搜尋流量分析刀鋒視窗中的 Application Insights 資料][2]

<span data-ttu-id="b80a5-167">Power BI Desktop 範本中所包含的計量︰</span><span class="sxs-lookup"><span data-stu-id="b80a5-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="b80a5-168">點選率 (CTR)：點選特定文件的使用者數與總搜尋數的比率。</span><span class="sxs-lookup"><span data-stu-id="b80a5-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="b80a5-169">無點選搜尋︰註冊無點選的熱門查詢詞彙</span><span class="sxs-lookup"><span data-stu-id="b80a5-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="b80a5-170">最多點選的文件︰過去 24 小時、7 天和 30 天內，依識別碼排序最多點選的文件。</span><span class="sxs-lookup"><span data-stu-id="b80a5-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="b80a5-171">常用的詞彙文件組︰依點選排序，造成點選相同文件的詞彙。</span><span class="sxs-lookup"><span data-stu-id="b80a5-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="b80a5-172">點選的時間︰自搜尋查詢起按照時間分組的點選</span><span class="sxs-lookup"><span data-stu-id="b80a5-172">Time to click: clicks bucketed by time since the search query</span></span>

![從 Application Insights 讀取的 Power BI 範本][3]


## <a name="next-steps"></a><span data-ttu-id="b80a5-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b80a5-174">Next Steps</span></span>
<span data-ttu-id="b80a5-175">檢測您的搜尋應用程式，取得搜尋服務的強大且詳細相關資料。</span><span class="sxs-lookup"><span data-stu-id="b80a5-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="b80a5-176">您可以在[這裡](https://go.microsoft.com/fwlink/?linkid=842905)找到 Application Insights 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b80a5-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="b80a5-177">若要深入了解其不同的服務層，請瀏覽 Application Insights [定價頁面](https://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="b80a5-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="b80a5-178">深入了解如何建立令人讚嘆的報告。</span><span class="sxs-lookup"><span data-stu-id="b80a5-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="b80a5-179">如需詳細資訊，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="b80a5-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
