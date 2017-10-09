---
title: "Azure 搜尋服務流量分析 aaaSearch |Microsoft 文件"
description: "針對 Azure 搜尋中，在 Microsoft Azure，toounlock 深入了解您的使用者和您的資料上裝載的雲端搜尋服務中啟用搜尋服務流量分析。"
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
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="ec716-103">什麼是搜尋流量分析</span><span class="sxs-lookup"><span data-stu-id="ec716-103">What is search traffic analytics</span></span>
<span data-ttu-id="ec716-104">搜尋流量分析是一種模式，可用來實作搜尋服務的意見反應管道。</span><span class="sxs-lookup"><span data-stu-id="ec716-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="ec716-105">此模式描述 hello 必要的資料和 toocollect 使用 Application Insights，監視業界領導者 services 如何在多個平台。</span><span class="sxs-lookup"><span data-stu-id="ec716-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="ec716-106">搜尋流量分析可讓您掌握您的搜尋服務，並深入分析您的使用者及其行為。</span><span class="sxs-lookup"><span data-stu-id="ec716-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="ec716-107">有關於使用者的選擇的資料，是進一步改善您的搜尋經驗和 tooback hello 結果並不是所關閉的可能 toomake 決策。</span><span class="sxs-lookup"><span data-stu-id="ec716-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="ec716-108">Azure 搜尋會提供整合 Azure Application Insights 和 Power BI tooprovide 深入了解監視和追蹤的遙測解決方案。</span><span class="sxs-lookup"><span data-stu-id="ec716-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="ec716-109">因為與 Azure 搜尋之間的互動是只能透過 Api，必須實作 hello 遙測 hello 開發人員所使用的搜尋，此頁面中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="ec716-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="ec716-110">識別 hello 相關搜尋資料</span><span class="sxs-lookup"><span data-stu-id="ec716-110">Identify hello relevant search data</span></span>

<span data-ttu-id="ec716-111">toohave 實用的搜尋度量資訊，它是必要 toolog 某些訊號 hello hello 搜尋應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="ec716-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="ec716-112">這些信號表示使用者感興趣，而且這些考量相關 tootheir 需要的內容。</span><span class="sxs-lookup"><span data-stu-id="ec716-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="ec716-113">搜尋流量分析需要兩個訊號︰</span><span class="sxs-lookup"><span data-stu-id="ec716-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="ec716-114">使用者產生的搜尋事件︰僅使用者所起始的搜尋查詢才有趣。</span><span class="sxs-lookup"><span data-stu-id="ec716-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="ec716-115">搜尋使用要求 toopopulate facet，其他內容或任何內部的資訊，並不重要，而且它們會扭曲並偏差的結果。</span><span class="sxs-lookup"><span data-stu-id="ec716-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="ec716-116">按一下 [事件] 使用者產生： 所按下此文件中，我們 tooa 使用者選取搜尋查詢所傳回的特定搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="ec716-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="ec716-117">點選通常表示文件為特定搜尋查詢的相關結果。</span><span class="sxs-lookup"><span data-stu-id="ec716-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="ec716-118">藉由連結相互關聯識別碼的搜尋，然後按一下事件，很可能 tooanalyze hello 行為，您的應用程式上的使用者。</span><span class="sxs-lookup"><span data-stu-id="ec716-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="ec716-119">這些搜尋 insights 是不可能 tooobtain 與搜尋流量記錄。</span><span class="sxs-lookup"><span data-stu-id="ec716-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="ec716-120">Tooimplement 如何搜尋服務流量分析</span><span class="sxs-lookup"><span data-stu-id="ec716-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="ec716-121">hello 訊號述 hello 上述 hello 使用者互動時，必須從 hello 搜尋應用程式收集 > 一節。</span><span class="sxs-lookup"><span data-stu-id="ec716-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="ec716-122">Application Insights 是可延伸的監視解決方案，適用於多個平台，並具有彈性的檢測選項。</span><span class="sxs-lookup"><span data-stu-id="ec716-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="ec716-123">Application Insights 的使用方式，可讓您充分利用 hello Power BI 搜尋所建立的報表資料的 Azure 搜尋 toomake hello 分析更容易。</span><span class="sxs-lookup"><span data-stu-id="ec716-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="ec716-124">在 hello[入口網站](https://portal.azure.com)Azure 搜尋服務，hello 搜尋流量分析分頁的頁面包含對下列這個遙測模式小祕技。</span><span class="sxs-lookup"><span data-stu-id="ec716-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="ec716-125">您也可以選取或建立 Application Insights 資源，並請參閱 hello 必要資料，在一個地方。</span><span class="sxs-lookup"><span data-stu-id="ec716-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![搜尋流量分析指示][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="ec716-127">1.選取 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="ec716-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="ec716-128">您需要 tooselect Application Insights 資源 toouse，或者如果沒有已經建立一個。</span><span class="sxs-lookup"><span data-stu-id="ec716-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="ec716-129">您可以使用具有已在使用 toolog hello 需要自訂事件的資源。</span><span class="sxs-lookup"><span data-stu-id="ec716-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="ec716-130">在建立新的 Application Insights 資源時，所有應用程式類型都適用於這種情況。</span><span class="sxs-lookup"><span data-stu-id="ec716-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="ec716-131">選取 hello 其中一個最符合您所使用的 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="ec716-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="ec716-132">您建立 hello 遙測用戶端應用程式需要 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="ec716-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="ec716-133">收到 hello Application Insights 入口網站儀表板，或您可以從取得 hello 搜尋服務流量分析 頁面上，選取您想要 toouse hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec716-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="ec716-134">2.檢測應用程式</span><span class="sxs-lookup"><span data-stu-id="ec716-134">2. Instrument your application</span></span>

<span data-ttu-id="ec716-135">在此階段，其中您檢測您自己的搜尋應用程式，使用上述步驟您在建立的 hello hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="ec716-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="ec716-136">Toothis 程序有四個步驟：</span><span class="sxs-lookup"><span data-stu-id="ec716-136">There are four steps toothis process:</span></span>

<span data-ttu-id="ec716-137">**I.建立用戶端遙測**這是傳送事件 toohello Application Insights 資源的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="ec716-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="ec716-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="ec716-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="ec716-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="ec716-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="ec716-140">如需其他語言與平台，請參閱 hello 完成[清單](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)。</span><span class="sxs-lookup"><span data-stu-id="ec716-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="ec716-141">**II.要求相互關聯的搜尋識別碼**toocorrelate 搜尋要求按下，它是必要的 toohave 關聯這兩個相異事件的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec716-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="ec716-142">當您使用標頭進行要求時，Azure 搜尋服務會為您提供搜尋識別碼︰</span><span class="sxs-lookup"><span data-stu-id="ec716-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="ec716-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="ec716-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="ec716-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="ec716-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="ec716-145">**III.記錄搜尋事件**</span><span class="sxs-lookup"><span data-stu-id="ec716-145">**III. Log Search events**</span></span>

<span data-ttu-id="ec716-146">搜尋要求發給使用者時，每次您應該記錄，做為搜尋事件具有下列結構描述上的 Application Insights 自訂事件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec716-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="ec716-147">**ServiceName**: （字串） 搜尋服務名稱**SearchId**: hello 搜尋查詢 (guid) 唯一識別項 （傳入 hello 搜尋回應） **IndexName**: （字串） 搜尋服務的索引查詢 toobe **QueryTerms**: hello 使用者所輸入的 （字串） 的搜尋詞彙**ResultCount**: (int) 所傳回的文件的數目 （傳入 hello 搜尋回應） **ScoringProfile**: hello 計分設定檔，如果有任何名稱 （字串）</span><span class="sxs-lookup"><span data-stu-id="ec716-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="ec716-148">要求計數上產生的使用者查詢，藉由新增 $count = true tooyour 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="ec716-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="ec716-149">請在[這裡](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)參閱詳細資訊</span><span class="sxs-lookup"><span data-stu-id="ec716-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="ec716-150">請記住 tooonly 由使用者所產生的記錄搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="ec716-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="ec716-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="ec716-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="ec716-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="ec716-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="ec716-153">**IV.記錄點選事件**</span><span class="sxs-lookup"><span data-stu-id="ec716-153">**IV. Log Click events**</span></span>

<span data-ttu-id="ec716-154">每當使用者點選文件時，必須記錄這個訊號才可進行搜尋分析。</span><span class="sxs-lookup"><span data-stu-id="ec716-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="ec716-155">使用下列結構描述的 hello Application Insights 自訂事件 toolog 這些事件：</span><span class="sxs-lookup"><span data-stu-id="ec716-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="ec716-156">**ServiceName**: （字串） 搜尋服務名稱**SearchId**: hello 相關的搜尋查詢 (guid) 唯一識別項**DocId**: （字串） 的文件識別碼**位置**: hello 搜尋中的 hello 文件的排列次序，(int) 結果頁面</span><span class="sxs-lookup"><span data-stu-id="ec716-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="ec716-157">位置是指 toohello 基線應用程式中的順序。</span><span class="sxs-lookup"><span data-stu-id="ec716-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="ec716-158">您是免費 tooset 此數字，只要它一律已 hello 相同 tooallow 進行比較。</span><span class="sxs-lookup"><span data-stu-id="ec716-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="ec716-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="ec716-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="ec716-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="ec716-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="ec716-161">3.使用 Power BI Desktop 進行分析</span><span class="sxs-lookup"><span data-stu-id="ec716-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="ec716-162">在檢測您的應用程式並驗證您的應用程式已正確連接的 tooApplication Insights 之後，您可以使用預先定義的範本建立的 Power BI desktop 的 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="ec716-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="ec716-163">此範本包含圖表和資料表可協助您讓較明智的決策 tooimprove，您的搜尋效能及相關性。</span><span class="sxs-lookup"><span data-stu-id="ec716-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="ec716-164">tooinstantiate hello Power BI 桌面範本，您需要三組 Application Insights 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ec716-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="ec716-165">當您選取 hello 資源 toouse 時，可以在 hello 搜尋服務流量分析 頁面上，找到這項資料</span><span class="sxs-lookup"><span data-stu-id="ec716-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Application Insights 資料，在刀鋒視窗中搜尋服務流量分析 hello][2]

<span data-ttu-id="ec716-167">Hello Power BI 桌面範本中所包含的度量：</span><span class="sxs-lookup"><span data-stu-id="ec716-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="ec716-168">按一下 透過速率 (CTR): 使用者按一下總搜尋特定的文件 toohello 數的比率。</span><span class="sxs-lookup"><span data-stu-id="ec716-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="ec716-169">無點選搜尋︰註冊無點選的熱門查詢詞彙</span><span class="sxs-lookup"><span data-stu-id="ec716-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="ec716-170">最按一下文件： 過去 24 小時、 7 天和 30 天內最按下的文件依識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="ec716-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="ec716-171">常用的詞彙文件組： hello 按一下同一份文件，會導致的條款依點選。</span><span class="sxs-lookup"><span data-stu-id="ec716-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="ec716-172">時間 tooclick： 按一下會按照 hello 搜尋查詢之後的時間</span><span class="sxs-lookup"><span data-stu-id="ec716-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![從 Application Insights 讀取的 Power BI 範本][3]


## <a name="next-steps"></a><span data-ttu-id="ec716-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec716-174">Next Steps</span></span>
<span data-ttu-id="ec716-175">檢測您的搜尋應用程式 tooget 功能強大且深入資料有關您的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="ec716-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="ec716-176">您可以在[這裡](https://go.microsoft.com/fwlink/?linkid=842905)找到 Application Insights 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ec716-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="ec716-177">請瀏覽 Application Insights[定價頁面](https://azure.microsoft.com/pricing/details/application-insights/)toolearn 深入了解其不同服務層。</span><span class="sxs-lookup"><span data-stu-id="ec716-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="ec716-178">深入了解如何建立令人讚嘆的報告。</span><span class="sxs-lookup"><span data-stu-id="ec716-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="ec716-179">如需詳細資訊，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="ec716-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
