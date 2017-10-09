---
title: "在 Azure 搜尋 aaaHow tooimplement 多面向導覽 |Microsoft 文件"
description: "加入多面向導覽 tooapplications 與 Azure 搜尋中，在 Microsoft Azure 上裝載的雲端搜尋服務整合。"
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a><span data-ttu-id="ac164-103">如何在 Azure 搜尋 tooimplement 多面向導覽</span><span class="sxs-lookup"><span data-stu-id="ac164-103">How tooimplement faceted navigation in Azure Search</span></span>
<span data-ttu-id="ac164-104">多面向導覽是一個篩選機制，它在搜尋應用程式中提供自動導向的向下鑽研導覽。</span><span class="sxs-lookup"><span data-stu-id="ac164-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span></span> <span data-ttu-id="ac164-105">hello 詞彙 '多面向導覽' 可能不熟悉，但您可能使用它之前。</span><span class="sxs-lookup"><span data-stu-id="ac164-105">hello term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span></span> <span data-ttu-id="ac164-106">下列範例會顯示 hello，多面向導覽是而已 hello 類別使用 toofilter 結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-106">As hello following example shows, faceted navigation is nothing more than hello categories used toofilter results.</span></span>

 ![Azure 搜尋服務作業入口網站示範][1]

<span data-ttu-id="ac164-108">多面向導覽是替代項目點 toosearch。</span><span class="sxs-lookup"><span data-stu-id="ac164-108">Faceted navigation is an alternative entry point toosearch.</span></span> <span data-ttu-id="ac164-109">它會提供方便的替代 tootyping 複雜搜尋運算式以手動方式。</span><span class="sxs-lookup"><span data-stu-id="ac164-109">It offers a convenient alternative tootyping complex search expressions by hand.</span></span> <span data-ttu-id="ac164-110">多面向可協助您找到要找的項目，同時確保您不會得到沒有項目的結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span></span> <span data-ttu-id="ac164-111">身為開發人員，facet 可讓您公開 hello 最為實用的搜尋準則瀏覽搜尋主體。</span><span class="sxs-lookup"><span data-stu-id="ac164-111">As a developer, facets let you expose hello most useful search criteria for navigating your search corpus.</span></span> <span data-ttu-id="ac164-112">在線上零售應用程式中，通常會根據品牌、部門 (童鞋)、尺寸、價格、熱門程度和評分來建置多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="ac164-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span></span> 

<span data-ttu-id="ac164-113">實作多面向導覽會因各搜尋技術而不同。</span><span class="sxs-lookup"><span data-stu-id="ac164-113">Implementing faceted navigation differs across search technologies.</span></span> <span data-ttu-id="ac164-114">在 Azure 搜尋服務中，多面向導覽會在查詢時使用您先前歸屬在結構描述中的欄位來建置。</span><span class="sxs-lookup"><span data-stu-id="ac164-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span></span>

-   <span data-ttu-id="ac164-115">在建置您的應用程式，必須先傳送查詢的 hello 查詢*facet 查詢參數*tooget hello 可用 facet 該文件的篩選值的結果集。</span><span class="sxs-lookup"><span data-stu-id="ac164-115">In hello queries that your application builds, a query must send *facet query parameters* tooget hello available facet filter values for that document result set.</span></span>

-   <span data-ttu-id="ac164-116">tooactually 修剪 hello 文件的結果集、 hello 應用程式還必須套用`$filter`運算式。</span><span class="sxs-lookup"><span data-stu-id="ac164-116">tooactually trim hello document result set, hello application must also apply a `$filter` expression.</span></span>

<span data-ttu-id="ac164-117">在您的應用程式開發，撰寫程式碼會建構查詢，即構成 hello 大量 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="ac164-117">In your application development, writing code that constructs queries constitutes hello bulk of hello work.</span></span> <span data-ttu-id="ac164-118">許多 hello 應用程式的行為如預期般從多面向導覽會提供 hello 服務，包括內建支援來定義範圍和取得 facet 結果中的計數。</span><span class="sxs-lookup"><span data-stu-id="ac164-118">Many of hello application behaviors that you would expect from faceted navigation are provided by hello service, including built-in support for defining ranges and getting counts for facet results.</span></span> <span data-ttu-id="ac164-119">hello 服務也包含實用的預設值，可協助您避免變得不便瀏覽結構。</span><span class="sxs-lookup"><span data-stu-id="ac164-119">hello service also includes sensible defaults that help you avoid unwieldy navigation structures.</span></span> 

## <a name="sample-code-and-demo"></a><span data-ttu-id="ac164-120">程式碼範例和示範</span><span class="sxs-lookup"><span data-stu-id="ac164-120">Sample code and demo</span></span>
<span data-ttu-id="ac164-121">本文使用作業搜尋入口網站來作為範例。</span><span class="sxs-lookup"><span data-stu-id="ac164-121">This article uses a job search portal as an example.</span></span> <span data-ttu-id="ac164-122">hello 範例會實作為 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac164-122">hello example is implemented as an ASP.NET MVC application.</span></span>

-   <span data-ttu-id="ac164-123">請參閱和測試 hello 工作示範線上在[Azure 搜尋作業入口網站示範](http://azjobsdemo.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="ac164-123">See and test hello working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="ac164-124">下載 hello 程式碼從 hello [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)。</span><span class="sxs-lookup"><span data-stu-id="ac164-124">Download hello code from hello [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

## <a name="get-started"></a><span data-ttu-id="ac164-125">開始使用</span><span class="sxs-lookup"><span data-stu-id="ac164-125">Get started</span></span>
<span data-ttu-id="ac164-126">如果您是新 toosearch 開發，hello 最佳方式 toothink 的多面向導覽是，它會顯示 hello 自我引導搜尋的可能性。</span><span class="sxs-lookup"><span data-stu-id="ac164-126">If you're new toosearch development, hello best way toothink of faceted navigation is that it shows hello possibilities for self-directed search.</span></span> <span data-ttu-id="ac164-127">它是向下鑽研搜尋體驗的一種，基於預先定義的篩選條件，可以藉由「指向並按一下」的動作快速縮減搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span></span> 

### <a name="interaction-model"></a><span data-ttu-id="ac164-128">互動模型</span><span class="sxs-lookup"><span data-stu-id="ac164-128">Interaction model</span></span>

<span data-ttu-id="ac164-129">hello 搜尋經驗，針對多面向導覽是反覆執行，讓我們開始了解以回應 toouser 動作在展開的查詢的序列。</span><span class="sxs-lookup"><span data-stu-id="ac164-129">hello search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response toouser actions.</span></span>

<span data-ttu-id="ac164-130">hello 開始點就是提供多面向導覽，通常會放在 hello 位於周邊視覺範圍上的應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="ac164-130">hello starting point is an application page that provides faceted navigation, typically placed on hello periphery.</span></span> <span data-ttu-id="ac164-131">多面向導覽通常是樹狀結構，且每個值有核取方塊，或可點選的文字。</span><span class="sxs-lookup"><span data-stu-id="ac164-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span></span> 

1. <span data-ttu-id="ac164-132">傳送 tooAzure 搜尋查詢會指定透過一或多個 facet 查詢參數的 hello 多面向導覽結構。</span><span class="sxs-lookup"><span data-stu-id="ac164-132">A query sent tooAzure Search specifies hello faceted navigation structure via one or more facet query parameters.</span></span> <span data-ttu-id="ac164-133">Hello 查詢可能會包含執行個體， `facet=Rating`，可能與`:values`或`:sort`選項 toofurther 精簡 hello 簡報。</span><span class="sxs-lookup"><span data-stu-id="ac164-133">For instance, hello query might include `facet=Rating`, perhaps with a `:values` or `:sort` option toofurther refine hello presentation.</span></span>
2. <span data-ttu-id="ac164-134">hello 展示層會轉譯提供多面向導覽中，使用 hello facet hello 要求上指定的搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="ac164-134">hello presentation layer renders a search page that provides faceted navigation, using hello facets specified on hello request.</span></span>
3. <span data-ttu-id="ac164-135">您指定多面向導覽結構，其中包含評等，按一下"4"tooindicate 應顯示只為等級 4 或更新版本的產品。</span><span class="sxs-lookup"><span data-stu-id="ac164-135">Given a faceted navigation structure that includes Rating, you click "4" tooindicate that only products with a rating of 4 or higher should be shown.</span></span> 
4. <span data-ttu-id="ac164-136">傳送，回應 hello 應用程式包含的查詢`$filter=Rating ge 4`</span><span class="sxs-lookup"><span data-stu-id="ac164-136">In response, hello application sends a query that includes `$filter=Rating ge 4`</span></span> 
5. <span data-ttu-id="ac164-137">hello 展示層更新 hello 頁面顯示減少的結果集，其中包含只符合 hello 新的篩選條件的項目 (在此情況下，產品評等為 4 與更新版本)。</span><span class="sxs-lookup"><span data-stu-id="ac164-137">hello presentation layer updates hello page, showing a reduced result set, containing just those items that satisfy hello new criteria (in this case, products rated 4 and up).</span></span>

<span data-ttu-id="ac164-138">面向是查詢參數，但不要將它與查詢輸入混淆了。</span><span class="sxs-lookup"><span data-stu-id="ac164-138">A facet is a query parameter, but do not confuse it with query input.</span></span> <span data-ttu-id="ac164-139">它在查詢中不是當作選取準則。</span><span class="sxs-lookup"><span data-stu-id="ac164-139">It is never used as selection criteria in a query.</span></span> <span data-ttu-id="ac164-140">相反地，將 facet 查詢參數視為恢復 hello 回應中的輸入 toohello 導覽結構。</span><span class="sxs-lookup"><span data-stu-id="ac164-140">Instead, think of facet query parameters as inputs toohello navigation structure that comes back in hello response.</span></span> <span data-ttu-id="ac164-141">您提供每一個 facet 查詢參數，Azure 搜尋會評估多少文件位於 hello 部分結果的每個 facet 的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in hello partial results for each facet value.</span></span>

<span data-ttu-id="ac164-142">請注意 hello`$filter`在步驟 4 中。</span><span class="sxs-lookup"><span data-stu-id="ac164-142">Notice hello `$filter` in step 4.</span></span> <span data-ttu-id="ac164-143">hello 篩選器是多面向導覽的重要層面。</span><span class="sxs-lookup"><span data-stu-id="ac164-143">hello filter is an important aspect of faceted navigation.</span></span> <span data-ttu-id="ac164-144">雖然 facet 和篩選無關 hello 應用程式開發介面中，您會需要您想要這兩個 toodeliver hello 經驗。</span><span class="sxs-lookup"><span data-stu-id="ac164-144">Although facets and filters are independent in hello API, you need both toodeliver hello experience you intend.</span></span> 

### <a name="app-design-pattern"></a><span data-ttu-id="ac164-145">應用程式設計模式</span><span class="sxs-lookup"><span data-stu-id="ac164-145">App design pattern</span></span>

<span data-ttu-id="ac164-146">在應用程式程式碼 hello 模式是 toouse facet 查詢參數 tooreturn hello 多面向導覽結構以及 facet 結果加上 $filter 運算式。</span><span class="sxs-lookup"><span data-stu-id="ac164-146">In application code, hello pattern is toouse facet query parameters tooreturn hello faceted navigation structure along with facet results, plus a $filter expression.</span></span>  <span data-ttu-id="ac164-147">hello 篩選運算式的控制代碼 hello 按一下 hello facet 的值上的事件。</span><span class="sxs-lookup"><span data-stu-id="ac164-147">hello filter expression handles hello click event on hello facet value.</span></span> <span data-ttu-id="ac164-148">考慮的 hello `$filter` hello hello 實際修剪背後的程式碼搜尋結果的運算式傳回 toohello 展示層。</span><span class="sxs-lookup"><span data-stu-id="ac164-148">Think of hello `$filter` expression as hello code behind hello actual trimming of search results returned toohello presentation layer.</span></span> <span data-ttu-id="ac164-149">按一下紅色 hello 色彩透過實作提供色彩 facet，`$filter`運算式會選取有紅色的色彩的項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-149">Given a Colors facet, clicking hello color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span></span> 

### <a name="query-basics"></a><span data-ttu-id="ac164-150">查詢基本概念</span><span class="sxs-lookup"><span data-stu-id="ac164-150">Query basics</span></span>

<span data-ttu-id="ac164-151">在 Azure 搜尋服務中，要求是透過一或多個查詢參數 (如需個別的詳細描述，請參閱 [搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx) ) 指定。</span><span class="sxs-lookup"><span data-stu-id="ac164-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span></span> <span data-ttu-id="ac164-152">無 hello 查詢參數是必要的但您必須至少有一個有效查詢 toobe 的順序。</span><span class="sxs-lookup"><span data-stu-id="ac164-152">None of hello query parameters are required, but you must have at least one in order for a query toobe valid.</span></span>

<span data-ttu-id="ac164-153">有效位數，辨識 hello 能力 toofilter 出不相關的叫用，可以透過完成一或多個這些運算式：</span><span class="sxs-lookup"><span data-stu-id="ac164-153">Precision, understood as hello ability toofilter out irrelevant hits, is achieved through one or both of these expressions:</span></span>

-   <span data-ttu-id="ac164-154">**搜尋=**</span><span class="sxs-lookup"><span data-stu-id="ac164-154">**search=**</span></span>  
    <span data-ttu-id="ac164-155">此參數 hello 值構成 hello 搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="ac164-155">hello value of this parameter constitutes hello search expression.</span></span> <span data-ttu-id="ac164-156">它可能為單一的文字，或包括多個名詞和運算子的複雜搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="ac164-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span></span> <span data-ttu-id="ac164-157">Hello 在伺服器上，搜尋運算式用於全文檢索搜尋，查詢可搜尋符合的詞彙中，次序順序傳回結果的 hello 索引中的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac164-157">On hello server, a search expression is used for full-text search, querying searchable fields in hello index for matching terms, returning results in rank order.</span></span> <span data-ttu-id="ac164-158">如果您設定`search`toonull，是透過 hello 整個索引的查詢執行 (也就是`search=*`)。</span><span class="sxs-lookup"><span data-stu-id="ac164-158">If you set `search` toonull, query execution is over hello entire index (that is, `search=*`).</span></span> <span data-ttu-id="ac164-159">In this case，hello 的其他項目查詢，例如`$filter`或計分設定檔，會影響傳回的文件的主要因素 hello `($filter`) 以及依照何種 (`scoringProfile`或`$orderby`)。</span><span class="sxs-lookup"><span data-stu-id="ac164-159">In this case, other elements of hello query, such as a `$filter` or scoring profile, are hello primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span></span>

-   <span data-ttu-id="ac164-160">**$filter=**</span><span class="sxs-lookup"><span data-stu-id="ac164-160">**$filter=**</span></span>  
    <span data-ttu-id="ac164-161">篩選是強大的機制，來限制根據特定文件屬性的 hello 值的搜尋結果的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="ac164-161">A filter is a powerful mechanism for limiting hello size of search results based on hello values of specific document attributes.</span></span> <span data-ttu-id="ac164-162">A`$filter`會先評估，後面接著 faceting 邏輯，以產生 hello 可用的值及針對每個值對應的計數</span><span class="sxs-lookup"><span data-stu-id="ac164-162">A `$filter` is evaluated first, followed by faceting logic that generates hello available values and corresponding counts for each value</span></span>

<span data-ttu-id="ac164-163">複雜的搜尋運算式降低 hello hello 查詢效能。</span><span class="sxs-lookup"><span data-stu-id="ac164-163">Complex search expressions decrease hello performance of hello query.</span></span> <span data-ttu-id="ac164-164">可能的話，請使用格式建構的篩選運算式 tooincrease 有效位數，而且改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="ac164-164">Where possible, use well-constructed filter expressions tooincrease precision and improve query performance.</span></span>

<span data-ttu-id="ac164-165">toobetter 了解如何篩選器加入更多有效位數，請比較複雜的搜尋運算式 tooone 包含篩選條件運算式：</span><span class="sxs-lookup"><span data-stu-id="ac164-165">toobetter understand how a filter adds more precision, compare a complex search expression tooone that includes a filter expression:</span></span>

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

<span data-ttu-id="ac164-166">這兩個查詢有效，但 hello 第二種是如果您想要尋求非屋與位於西雅圖的暫止。</span><span class="sxs-lookup"><span data-stu-id="ac164-166">Both queries are valid, but hello second is superior if you’re looking for non-motels with parking in Seattle.</span></span>
-   <span data-ttu-id="ac164-167">hello 第一個查詢依賴特定文字被提及或字串欄位名稱、 描述和包含可搜尋資料的任何其他欄位中未提及。</span><span class="sxs-lookup"><span data-stu-id="ac164-167">hello first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span></span>
-   <span data-ttu-id="ac164-168">hello 第二個查詢會尋找精確比對結構化資料，且可能 toobe 更為精確。</span><span class="sxs-lookup"><span data-stu-id="ac164-168">hello second query looks for precise matches on structured data and is likely toobe much more accurate.</span></span>

<span data-ttu-id="ac164-169">在包含多面向導覽的應用程式中，請確定每個透過多面向導覽結構進行的使用者動作都伴隨搜尋結果縮減。</span><span class="sxs-lookup"><span data-stu-id="ac164-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span></span> <span data-ttu-id="ac164-170">toonarrow 結果，請使用篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="ac164-170">toonarrow results, use a filter expression.</span></span>

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a><span data-ttu-id="ac164-171">建置多面向導覽應用程式</span><span class="sxs-lookup"><span data-stu-id="ac164-171">Build a faceted navigation app</span></span>
<span data-ttu-id="ac164-172">您可以實作多面向導覽使用 Azure 搜尋在應用程式程式碼會建置 hello 搜尋要求。</span><span class="sxs-lookup"><span data-stu-id="ac164-172">You implement faceted navigation with Azure Search in your application code that builds hello search request.</span></span> <span data-ttu-id="ac164-173">hello 多面向導覽依賴您先前定義的結構描述中的項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-173">hello faceted navigation relies on elements in your schema that you defined previously.</span></span>

<span data-ttu-id="ac164-174">在搜尋索引中預先定義為 hello`Facetable [true|false]`屬性編製索引，在選取的欄位 tooenable 上設定或停用在多面向導覽結構中的使用。</span><span class="sxs-lookup"><span data-stu-id="ac164-174">Predefined in your search index is hello `Facetable [true|false]` index attribute, set on selected fields tooenable or disable their use in a faceted navigation structure.</span></span> <span data-ttu-id="ac164-175">若沒有 `"Facetable" = true`，該欄位就不能在多面向導覽中使用。</span><span class="sxs-lookup"><span data-stu-id="ac164-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span></span>

<span data-ttu-id="ac164-176">在程式碼中的 hello 展示層提供 hello 使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="ac164-176">hello presentation layer in your code provides hello user experience.</span></span> <span data-ttu-id="ac164-177">它應該會列出 hello 的 hello 多面向導覽，例如 hello 標籤、 值、 核取方塊及 hello 計數的構成部分。</span><span class="sxs-lookup"><span data-stu-id="ac164-177">It should list hello constituent parts of hello faceted navigation, such as hello label, values, check boxes, and hello count.</span></span> <span data-ttu-id="ac164-178">hello Azure 搜尋 REST API 是無從驗證平台，因此，使用任何語言和您想要的平台。</span><span class="sxs-lookup"><span data-stu-id="ac164-178">hello Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span></span> <span data-ttu-id="ac164-179">hello 重點是 tooinclude UI 項目支援累加式的重新整理，更新的 UI 狀態與選取每一個額外的 facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-179">hello important thing is tooinclude UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span></span> 

<span data-ttu-id="ac164-180">在查詢時，應用程式程式碼會建立要求，其中包含`facet=[string]`，提供由 hello 欄位 toofacet 要求參數。</span><span class="sxs-lookup"><span data-stu-id="ac164-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides hello field toofacet by.</span></span> <span data-ttu-id="ac164-181">一個查詢可以有多個面向，例如 `&facet=color&facet=category&facet=rating`，每個面向都以 & 符號分隔。</span><span class="sxs-lookup"><span data-stu-id="ac164-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span></span>

<span data-ttu-id="ac164-182">應用程式程式碼也必須建構`$filter`運算式 toohandle hello 按一下多面向導覽中的事件。</span><span class="sxs-lookup"><span data-stu-id="ac164-182">Application code must also construct a `$filter` expression toohandle hello click events in faceted navigation.</span></span> <span data-ttu-id="ac164-183">A`$filter`減少 hello 搜尋結果中，使用 hello facet 的值做為篩選準則。</span><span class="sxs-lookup"><span data-stu-id="ac164-183">A `$filter` reduces hello search results, using hello facet value as filter criteria.</span></span>

<span data-ttu-id="ac164-184">Azure 搜尋傳回 hello 搜尋結果中，根據一個或多個輸入，以及更新 toohello 多面向導覽結構的詞彙。</span><span class="sxs-lookup"><span data-stu-id="ac164-184">Azure Search returns hello search results, based on one or more terms that you enter, along with updates toohello faceted navigation structure.</span></span> <span data-ttu-id="ac164-185">在 Azure 搜尋服務中，多面向導覽是單一層級的結構，其中包含面向值及其找到結果的計數。</span><span class="sxs-lookup"><span data-stu-id="ac164-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span></span>

<span data-ttu-id="ac164-186">我們在 hello 下列各節，深入了解 toobuild 每個部分。</span><span class="sxs-lookup"><span data-stu-id="ac164-186">In hello following sections, we take a closer look at how toobuild each part.</span></span>

<a name="buildindex"></a>

## <a name="build-hello-index"></a><span data-ttu-id="ac164-187">建立 hello 索引</span><span class="sxs-lookup"><span data-stu-id="ac164-187">Build hello index</span></span>
<span data-ttu-id="ac164-188">啟用 faceting hello 在索引中，透過此索引屬性-欄位為基礎： `"Facetable": true`。</span><span class="sxs-lookup"><span data-stu-id="ac164-188">Faceting is enabled on a field-by-field basis in hello index, via this index attribute: `"Facetable": true`.</span></span>  
<span data-ttu-id="ac164-189">根據預設，所有可能用於多面向導覽的欄位類型為 `Facetable` 。</span><span class="sxs-lookup"><span data-stu-id="ac164-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span></span> <span data-ttu-id="ac164-190">這類的欄位類型包括`Edm.String`， `Edm.DateTimeOffset`，和所有 hello 數值的欄位型別 (基本上，所有的欄位類型都是可進行 facet 處理除了`Edm.GeographyPoint`，這不能用於在多面向導覽)。</span><span class="sxs-lookup"><span data-stu-id="ac164-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all hello numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span></span> 

<span data-ttu-id="ac164-191">當建立索引時，多面向導覽的最佳作法超出 tooexplicitly 開啟 faceting 永遠不應該當做 facet 使用的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac164-191">When building an index, a best practice for faceted navigation is tooexplicitly turn faceting off for fields that should never be used as a facet.</span></span>  <span data-ttu-id="ac164-192">特別是，單一值、 識別碼或產品名稱，例如字串欄位應該設定太`"Facetable": false`tooprevent 其意外 （並沒有作用） 使用的多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="ac164-192">In particular, string fields for singleton values, such as an ID or product name, should be set too`"Facetable": false` tooprevent their accidental (and ineffective) use in faceted navigation.</span></span> <span data-ttu-id="ac164-193">開啟關閉您不需要在其中 faceting 可協助確保 hello 索引的 hello 大小很小，以及將通常會改善效能。</span><span class="sxs-lookup"><span data-stu-id="ac164-193">Turning faceting off where you don’t need it helps keep hello size of hello index small, and typically improves performance.</span></span>

<span data-ttu-id="ac164-194">以下是 hello 作業入口網站示範範例應用程式的某些屬性 tooreduce hello 大小修剪 hello 結構描述的一部分：</span><span class="sxs-lookup"><span data-stu-id="ac164-194">Following is part of hello schema for hello Job Portal Demo sample app, trimmed of some attributes tooreduce hello size:</span></span>

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

<span data-ttu-id="ac164-195">如您所見 hello 範例結構描述中`Facetable`功能是關閉的字串欄位不應該做為 facet，例如識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ac164-195">As you can see in hello sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span></span> <span data-ttu-id="ac164-196">開啟關閉您不需要在其中 faceting 可協助確保 hello 索引的 hello 大小很小，以及將通常會改善效能。</span><span class="sxs-lookup"><span data-stu-id="ac164-196">Turning faceting off where you don’t need it helps keep hello size of hello index small, and typically improves performance.</span></span>

> [!TIP]
> <span data-ttu-id="ac164-197">最佳做法，包括 hello 完整的每個欄位的索引屬性集。</span><span class="sxs-lookup"><span data-stu-id="ac164-197">As a best practice, include hello full set of index attributes for each field.</span></span> <span data-ttu-id="ac164-198">雖然`Facetable`預設為開啟的幾乎所有的欄位，刻意設定每個屬性可協助您仔細思考每個結構描述決策 hello 含意。</span><span class="sxs-lookup"><span data-stu-id="ac164-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through hello implications of each schema decision.</span></span> 

<a name="checkdata"></a>

## <a name="check-hello-data"></a><span data-ttu-id="ac164-199">檢查 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ac164-199">Check hello data</span></span>
<span data-ttu-id="ac164-200">hello 資料的品質有直接影響 hello 多面向導覽結構是否會具體化您所預期的。</span><span class="sxs-lookup"><span data-stu-id="ac164-200">hello quality of your data has a direct effect on whether hello faceted navigation structure materializes as you expect it to.</span></span> <span data-ttu-id="ac164-201">它也會影響 hello 輕鬆建構篩選 tooreduce hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="ac164-201">It also affects hello ease of constructing filters tooreduce hello result set.</span></span>

<span data-ttu-id="ac164-202">如果您想 toofacet 品牌或價格，每份文件應包含的值*BrandName*和*ProductPrice*屬於有效、 一致且有效率當做篩選選項。</span><span class="sxs-lookup"><span data-stu-id="ac164-202">If you want toofacet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span></span>

<span data-ttu-id="ac164-203">以下是針對哪些 tooscrub 的幾個提醒：</span><span class="sxs-lookup"><span data-stu-id="ac164-203">Here are a few reminders of what tooscrub for:</span></span>

* <span data-ttu-id="ac164-204">為您想要依 toofacet 每個欄位，請詢問自己是否包含在搜尋中自我引導適合做為篩選的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-204">For every field that you want toofacet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span></span> <span data-ttu-id="ac164-205">hello 值應該是簡短、 描述性，和足以特殊 toooffer 競爭選項之間的明確選項。</span><span class="sxs-lookup"><span data-stu-id="ac164-205">hello values should be short, descriptive, and sufficiently distinctive toooffer a clear choice between competing options.</span></span>
* <span data-ttu-id="ac164-206">拼字錯誤或近似符合的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-206">Misspellings or nearly matching values.</span></span> <span data-ttu-id="ac164-207">如果 facet 上色彩，以及欄位的值包括橙色和 Ornage （拼字錯誤）、 根據 hello 色彩欄位 facet 將會收取兩者。</span><span class="sxs-lookup"><span data-stu-id="ac164-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on hello Color field would pick up both.</span></span>
* <span data-ttu-id="ac164-208">混合大小寫的文字對多面向導覽也會遭成嚴重影響 (orange 和 Orange 為兩個不同的值)。</span><span class="sxs-lookup"><span data-stu-id="ac164-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span></span> 
* <span data-ttu-id="ac164-209">單一的單複數形態 hello 相同的值可以針對每個會導致不同的 facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-209">Single and plural versions of hello same value can result in a separate facet for each.</span></span>

<span data-ttu-id="ac164-210">您可以想像，勤加注意準備 hello 資料是有效的多面向導覽的重要層面。</span><span class="sxs-lookup"><span data-stu-id="ac164-210">As you can imagine, diligence in preparing hello data is an essential aspect of effective faceted navigation.</span></span>

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a><span data-ttu-id="ac164-211">建置 hello UI</span><span class="sxs-lookup"><span data-stu-id="ac164-211">Build hello UI</span></span>
<span data-ttu-id="ac164-212">使用從 hello 展示層可以說明您在發現需求，否則可能會遺漏，並且了解哪些功能基本 toohello 搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="ac164-212">Working back from hello presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential toohello search experience.</span></span>

<span data-ttu-id="ac164-213">多面向導覽，以您的 web 或應用程式頁面會顯示 hello 多面向導覽結構、 偵測到在 hello 頁面上，使用者輸入和插入 hello 變更項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-213">In terms of faceted navigation, your web or application page displays hello faceted navigation structure, detects user input on hello page, and inserts hello changed elements.</span></span> 

<span data-ttu-id="ac164-214">Web 應用程式，AJAX 常用於 hello 展示層因為它可讓您 toorefresh 累加變更。</span><span class="sxs-lookup"><span data-stu-id="ac164-214">For web applications, AJAX is commonly used in hello presentation layer because it allows you toorefresh incremental changes.</span></span> <span data-ttu-id="ac164-215">您也可以使用 ASP.NET MVC 或任何其他視覺效果平台都可以透過 HTTP 連線 tooan Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="ac164-215">You could also use ASP.NET MVC or any other visualization platform that can connect tooan Azure Search service over HTTP.</span></span> <span data-ttu-id="ac164-216">hello 範例應用程式參考整篇文章-hello **Azure 搜尋作業入口網站示範**– 發生 toobe ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac164-216">hello sample application referenced throughout this article -- hello **Azure Search Job Portal Demo** – happens toobe an ASP.NET MVC application.</span></span>

<span data-ttu-id="ac164-217">在 hello 範例中，多面向導覽是內建 hello 搜尋結果頁面。</span><span class="sxs-lookup"><span data-stu-id="ac164-217">In hello sample, faceted navigation is built into hello search results page.</span></span> <span data-ttu-id="ac164-218">下列範例取自 hello hello`index.cshtml`檔案 hello 範例應用程式，顯示 hello 靜態 HTML 結構 hello 搜尋上顯示多面向導覽的結果頁面。</span><span class="sxs-lookup"><span data-stu-id="ac164-218">hello following example, taken from hello `index.cshtml` file of hello sample application, shows hello static HTML structure for displaying faceted navigation on hello search results page.</span></span> <span data-ttu-id="ac164-219">建立或送出搜尋文字，或選取或清除 facet 時以動態方式重建 hello 別的 facet 清單。</span><span class="sxs-lookup"><span data-stu-id="ac164-219">hello list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span></span>

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

<span data-ttu-id="ac164-220">下列程式碼片段從 hello hello`index.cshtml`頁面會動態建立 hello HTML toodisplay hello 第一個 facet，商務標題。</span><span class="sxs-lookup"><span data-stu-id="ac164-220">hello following code snippet from hello `index.cshtml` page dynamically builds hello HTML toodisplay hello first facet, Business Title.</span></span> <span data-ttu-id="ac164-221">類似的函式動態建立 hello HTML hello 其他方面。</span><span class="sxs-lookup"><span data-stu-id="ac164-221">Similar functions dynamically build hello HTML for hello other facets.</span></span> <span data-ttu-id="ac164-222">每一個 facet 都有標籤及顯示 hello 數目來傳回 facet 所找到的項目計數。</span><span class="sxs-lookup"><span data-stu-id="ac164-222">Each facet has a label and a count, which displays hello number of items found for that facet result.</span></span>

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> <span data-ttu-id="ac164-223">當您設計 hello 搜尋結果頁面時，請記住 tooadd 清除 facet 的機制。</span><span class="sxs-lookup"><span data-stu-id="ac164-223">When you design hello search results page, remember tooadd a mechanism for clearing facets.</span></span> <span data-ttu-id="ac164-224">如果您加入核取方塊，您可以輕鬆地查看 tooclear hello 的篩選器。</span><span class="sxs-lookup"><span data-stu-id="ac164-224">If you add check boxes, you can easily see how tooclear hello filters.</span></span> <span data-ttu-id="ac164-225">針對其他配置，您可能需要階層模式或其他具創意的方法。</span><span class="sxs-lookup"><span data-stu-id="ac164-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span></span> <span data-ttu-id="ac164-226">例如，在 hello 作業搜尋入口網站範例應用程式，您可以按一下 hello`[X]`之後所選的 facet tooclear hello facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-226">For example, in hello Job Search Portal sample application, you can click hello `[X]` after a selected facet tooclear hello facet.</span></span>

<a name="buildquery"></a>

## <a name="build-hello-query"></a><span data-ttu-id="ac164-227">建立 hello 查詢</span><span class="sxs-lookup"><span data-stu-id="ac164-227">Build hello query</span></span>
<span data-ttu-id="ac164-228">hello 來建立查詢所撰寫的程式碼應指定有效的查詢，包括搜尋運算式、 facet、 篩選、 計分設定檔 – 任何項目中的所有部分都使用 tooformulate 要求。</span><span class="sxs-lookup"><span data-stu-id="ac164-228">hello code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used tooformulate a request.</span></span> <span data-ttu-id="ac164-229">在本節中，我們探討其中 facet 放入查詢時，以及如何使用篩選條件的 facet toodeliver 以減少結果集。</span><span class="sxs-lookup"><span data-stu-id="ac164-229">In this section, we explore where facets fit into a query, and how filters are used with facets toodeliver a reduced result set.</span></span>

<span data-ttu-id="ac164-230">請注意，面向在此範例應用程式中是必要的。</span><span class="sxs-lookup"><span data-stu-id="ac164-230">Notice that facets are integral in this sample application.</span></span> <span data-ttu-id="ac164-231">hello hello 作業入口網站的示範中的搜尋經驗是針對設計多面向導覽和篩選。</span><span class="sxs-lookup"><span data-stu-id="ac164-231">hello search experience in hello Job Portal Demo is designed around faceted navigation and filters.</span></span> <span data-ttu-id="ac164-232">hello 顯著放置在 hello 頁面上的多面向導覽示範其重要性。</span><span class="sxs-lookup"><span data-stu-id="ac164-232">hello prominent placement of faceted navigation on hello page demonstrates its importance.</span></span> 

<span data-ttu-id="ac164-233">範例通常是很好的起點 toobegin。</span><span class="sxs-lookup"><span data-stu-id="ac164-233">An example is often a good place toobegin.</span></span> <span data-ttu-id="ac164-234">下列範例取自 hello hello`JobsSearch.cs`檔案，建立 facet 瀏覽的要求會根據商務標題、 位置、 張貼型別和最低薪資的組建。</span><span class="sxs-lookup"><span data-stu-id="ac164-234">hello following example, taken from hello `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span></span> 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

<span data-ttu-id="ac164-235">設定 tooa 欄位 facet 查詢參數，而且根據 hello 資料類型，可以進一步由進行參數化，其中包含以逗號分隔清單`count:<integer>`， `sort:<>`， `interval:<integer>`，和`values:<list>`。</span><span class="sxs-lookup"><span data-stu-id="ac164-235">A facet query parameter is set tooa field and depending on hello data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span></span> <span data-ttu-id="ac164-236">當設定範圍時，針對數值資料支援值清單。</span><span class="sxs-lookup"><span data-stu-id="ac164-236">A values list is supported for numeric data when setting up ranges.</span></span> <span data-ttu-id="ac164-237">如需用量詳細資訊，請參閱 [搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ac164-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span></span>

<span data-ttu-id="ac164-238">Facet，以及應用程式所構成的 hello 要求也應建置篩選 toonarrow 向 hello 組 facet 值選取項目所根據的候選文件。</span><span class="sxs-lookup"><span data-stu-id="ac164-238">Along with facets, hello request formulated by your application should also build filters toonarrow down hello set of candidate documents based on a facet value selection.</span></span> <span data-ttu-id="ac164-239">對於 bike 存放區中，多面向導覽提供線索 tooquestions 喜歡*何種色彩、 製造商和類型的自行車可用？*。</span><span class="sxs-lookup"><span data-stu-id="ac164-239">For a bike store, faceted navigation provides clues tooquestions like *What colors, manufacturers, and types of bikes are available?*.</span></span> <span data-ttu-id="ac164-240">篩選功能可解答「哪些單車確實是位於此價格帶內的紅色登山車？」之類的問題。</span><span class="sxs-lookup"><span data-stu-id="ac164-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span></span> <span data-ttu-id="ac164-241">當您按一下應顯示紅色的產品，"Red"tooindicate hello 下一個查詢 hello 應用程式會傳送包含`$filter=Color eq ‘Red’`。</span><span class="sxs-lookup"><span data-stu-id="ac164-241">When you click "Red" tooindicate that only Red products should be shown, hello next query hello application sends includes `$filter=Color eq ‘Red’`.</span></span>

<span data-ttu-id="ac164-242">下列程式碼片段從 hello hello`JobsSearch.cs`頁面新增選取的 hello 商務標題 toohello 篩選器，如果您選取從 hello 商務標題 facet 的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-242">hello following code snippet from hello `JobsSearch.cs` page adds hello selected Business Title toohello filter if you select a value from hello Business Title facet.</span></span>

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a><span data-ttu-id="ac164-243">秘訣和最佳作法</span><span class="sxs-lookup"><span data-stu-id="ac164-243">Tips and best practices</span></span>

### <a name="indexing-tips"></a><span data-ttu-id="ac164-244">編製索引的秘訣</span><span class="sxs-lookup"><span data-stu-id="ac164-244">Indexing tips</span></span>
<span data-ttu-id="ac164-245">**在不使用搜尋方塊的情況下改善索引效率**</span><span class="sxs-lookup"><span data-stu-id="ac164-245">**Improve index efficiency if you don't use a Search box**</span></span>

<span data-ttu-id="ac164-246">如果您的應用程式只會使用多面向導覽 （也就是沒有搜尋方塊中），您可以將標記為 hello 欄位`searchable=false`， `facetable=true` tooproduce 更精簡的索引。</span><span class="sxs-lookup"><span data-stu-id="ac164-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark hello field as `searchable=false`, `facetable=true` tooproduce a more compact index.</span></span> <span data-ttu-id="ac164-247">此外，索引只會整個 facet 的值，與沒有文字分隔或 hello 元件部分的多字值的索引。</span><span class="sxs-lookup"><span data-stu-id="ac164-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of hello component parts of a multi-word value.</span></span>

<span data-ttu-id="ac164-248">**指定可做為面向的欄位**</span><span class="sxs-lookup"><span data-stu-id="ac164-248">**Specify which fields can be used as facets**</span></span>

<span data-ttu-id="ac164-249">前文提過該 hello hello 索引的結構描述決定哪些欄位可用 toouse 做為 facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-249">Recall that hello schema of hello index determines which fields are available toouse as a facet.</span></span> <span data-ttu-id="ac164-250">Hello 查詢假設欄位可進行 facet 處理，指定由哪個欄位 toofacet。</span><span class="sxs-lookup"><span data-stu-id="ac164-250">Assuming a field is facetable, hello query specifies which fields toofacet by.</span></span> <span data-ttu-id="ac164-251">您已經 faceting hello 欄位提供 hello 標籤底下顯示 hello 值。</span><span class="sxs-lookup"><span data-stu-id="ac164-251">hello field by which you are faceting provides hello values that appear below hello label.</span></span> 

<span data-ttu-id="ac164-252">顯示每個標籤底下的 hello 值是從 hello 索引擷取。</span><span class="sxs-lookup"><span data-stu-id="ac164-252">hello values that appear under each label are retrieved from hello index.</span></span> <span data-ttu-id="ac164-253">例如，如果 hello facet 欄位是*色彩*，可用於其他篩選的 hello 值為 hello 該欄位值為紅色、 黑色，以及其他等等。</span><span class="sxs-lookup"><span data-stu-id="ac164-253">For example, if hello facet field is *Color*, hello values available for additional filtering are hello values for that field - Red, Black, and so forth.</span></span>

<span data-ttu-id="ac164-254">數值和日期時間只對值，您可以明確設定值 hello facet 欄位 (例如， `facet=Rating,values:1|2|3|4|5`)。</span><span class="sxs-lookup"><span data-stu-id="ac164-254">For Numeric and DateTime values only, you can explicitly set values on hello facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span></span> <span data-ttu-id="ac164-255">這些欄位類型 toosimplify hello 分離 facet 結果的連續範圍 （可能是數值或時間週期為基礎的範圍） 到允許的值清單。</span><span class="sxs-lookup"><span data-stu-id="ac164-255">A values list is allowed for these field types toosimplify hello separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span></span> 

<span data-ttu-id="ac164-256">**依預設您只能擁有一個多面向導覽層級**</span><span class="sxs-lookup"><span data-stu-id="ac164-256">**By default you can only have one level of faceted navigation**</span></span> 

<span data-ttu-id="ac164-257">如附註所說明，階層中沒有直接支援巢狀面向。</span><span class="sxs-lookup"><span data-stu-id="ac164-257">As noted, there is no direct support for nesting facets in a hierarchy.</span></span> <span data-ttu-id="ac164-258">根據預設，Azure 搜尋服務中的多面向導覽僅支援單層篩選。</span><span class="sxs-lookup"><span data-stu-id="ac164-258">By default, faceted navigation in Azure Search only supports one level of filters.</span></span> <span data-ttu-id="ac164-259">不過有因應措施。</span><span class="sxs-lookup"><span data-stu-id="ac164-259">However, workarounds do exist.</span></span> <span data-ttu-id="ac164-260">您可以在 `Collection(Edm.String)` 中利用各階層各一個進入點來編碼階層面向。</span><span class="sxs-lookup"><span data-stu-id="ac164-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span></span> <span data-ttu-id="ac164-261">實作這個因應措施已超出本文的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="ac164-261">Implementing this workaround is beyond hello scope of this article.</span></span> 

### <a name="querying-tips"></a><span data-ttu-id="ac164-262">查詢秘訣</span><span class="sxs-lookup"><span data-stu-id="ac164-262">Querying tips</span></span>
<span data-ttu-id="ac164-263">**驗證欄位**</span><span class="sxs-lookup"><span data-stu-id="ac164-263">**Validate fields**</span></span>

<span data-ttu-id="ac164-264">如果您建立的 facet 以動態方式根據不受信任的使用者輸入的 hello 清單時，驗證確定 hello hello 多面向的欄位名稱是否有效。</span><span class="sxs-lookup"><span data-stu-id="ac164-264">If you build hello list of facets dynamically based on untrusted user input, validate that hello names of hello faceted fields are valid.</span></span> <span data-ttu-id="ac164-265">或者，當建置使用 Url 逸出 hello 名稱`Uri.EscapeDataString()`在.NET 中或在您的平台選擇的對等的 hello。</span><span class="sxs-lookup"><span data-stu-id="ac164-265">Or, escape hello names when building URLs by using either `Uri.EscapeDataString()` in .NET, or hello equivalent in your platform of choice.</span></span>

### <a name="filtering-tips"></a><span data-ttu-id="ac164-266">篩選秘訣</span><span class="sxs-lookup"><span data-stu-id="ac164-266">Filtering tips</span></span>
<span data-ttu-id="ac164-267">**使用篩選條件提高搜尋精準度**</span><span class="sxs-lookup"><span data-stu-id="ac164-267">**Increase search precision with filters**</span></span>

<span data-ttu-id="ac164-268">使用篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ac164-268">Use filters.</span></span> <span data-ttu-id="ac164-269">如果您依賴單獨詞幹分析可能會導致文件 toobe 只搜尋運算式會傳回任何欄位中不具有 hello 精確 facet 的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-269">If you rely on just search expressions alone, stemming could cause a document toobe returned that doesn’t have hello precise facet value in any of its fields.</span></span>

<span data-ttu-id="ac164-270">**使用篩選條件提高搜尋效能**</span><span class="sxs-lookup"><span data-stu-id="ac164-270">**Increase search performance with filters**</span></span>

<span data-ttu-id="ac164-271">篩選器縮小 hello 組搜尋候選文件，並排除排名。</span><span class="sxs-lookup"><span data-stu-id="ac164-271">Filters narrow down hello set of candidate documents for search and exclude them from ranking.</span></span> <span data-ttu-id="ac164-272">如果您有大型文件集，使用經過挑選的面向向下切入通常能讓您的效能提升。</span><span class="sxs-lookup"><span data-stu-id="ac164-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span></span>
  
<span data-ttu-id="ac164-273">**篩選 hello 多面向欄位**</span><span class="sxs-lookup"><span data-stu-id="ac164-273">**Filter only hello faceted fields**</span></span>

<span data-ttu-id="ac164-274">在多面向向下鑽研，您通常想 tooonly 包含文件有任何位置不在跨所有可搜尋的欄位在特定的 （多面向） 欄位中，hello facet 的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-274">In faceted drill-down, you typically want tooonly include documents that have hello facet value in a specific (faceted) field, not anywhere across all searchable fields.</span></span> <span data-ttu-id="ac164-275">加入篩選，以控制程式只在 hello 多面向的欄位相符的值為 hello 服務 toosearch 強調 hello 目標欄位。</span><span class="sxs-lookup"><span data-stu-id="ac164-275">Adding a filter reinforces hello target field by directing hello service toosearch only in hello faceted field for a matching value.</span></span>

<span data-ttu-id="ac164-276">**使用更多篩選條件修剪面向結果**</span><span class="sxs-lookup"><span data-stu-id="ac164-276">**Trim facet results with more filters**</span></span>

<span data-ttu-id="ac164-277">Facet 結果是找到符合 facet 字詞的 hello 搜尋結果中的文件。</span><span class="sxs-lookup"><span data-stu-id="ac164-277">Facet results are documents found in hello search results that match a facet term.</span></span> <span data-ttu-id="ac164-278">在下列範例中的，在搜尋結果中的 hello*雲端運算*，254 項目也具有*內部規格*做為內容的類型。</span><span class="sxs-lookup"><span data-stu-id="ac164-278">In hello following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span></span> <span data-ttu-id="ac164-279">項目毋須互斥。</span><span class="sxs-lookup"><span data-stu-id="ac164-279">Items are not necessarily mutually exclusive.</span></span> <span data-ttu-id="ac164-280">如果項目符合 hello 這兩個篩選準則，計算每個。</span><span class="sxs-lookup"><span data-stu-id="ac164-280">If an item meets hello criteria of both filters, it is counted in each one.</span></span> <span data-ttu-id="ac164-281">這種重複狀況時，可能在 faceting`Collection(Edm.String)`欄位，而這通常是用 tooimplement 文件標記。</span><span class="sxs-lookup"><span data-stu-id="ac164-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used tooimplement document tagging.</span></span>

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

<span data-ttu-id="ac164-282">一般情況下，如果您發現 facet 結果會一致地太大，我們建議您加入其他篩選 toogive 使用者縮小 hello 搜尋更多的選項。</span><span class="sxs-lookup"><span data-stu-id="ac164-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters toogive users more options for narrowing hello search.</span></span>

### <a name="tips-about-result-count"></a><span data-ttu-id="ac164-283">關於結果計數的秘訣</span><span class="sxs-lookup"><span data-stu-id="ac164-283">Tips about result count</span></span>

<span data-ttu-id="ac164-284">**限制 hello hello facet 導覽中的項目數目**</span><span class="sxs-lookup"><span data-stu-id="ac164-284">**Limit hello number of items in hello facet navigation**</span></span>

<span data-ttu-id="ac164-285">Hello 導覽樹狀目錄中每個 facet 欄位，沒有預設的 10 個值的限制。</span><span class="sxs-lookup"><span data-stu-id="ac164-285">For each faceted field in hello navigation tree, there is a default limit of 10 values.</span></span> <span data-ttu-id="ac164-286">這個預設值就導覽結構的有意義，因為它會將 hello 值清單 tooa 大小容易管理。</span><span class="sxs-lookup"><span data-stu-id="ac164-286">This default makes sense for navigation structures because it keeps hello values list tooa manageable size.</span></span> <span data-ttu-id="ac164-287">您可以藉由指派值 toocount 覆寫 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="ac164-287">You can override hello default by assigning a value toocount.</span></span>

* <span data-ttu-id="ac164-288">`&facet=city,count:5`指定只有 hello 前五個城市位於 hello 上方的等級結果會傳回做為 facet 結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-288">`&facet=city,count:5` specifies that only hello first five cities found in hello top ranked results are returned as a facet result.</span></span> <span data-ttu-id="ac164-289">請設想具有搜尋字詞「機場」和 32 個符合項的查詢範例。</span><span class="sxs-lookup"><span data-stu-id="ac164-289">Consider a sample query with a search term of “airport” and 32 matches.</span></span> <span data-ttu-id="ac164-290">如果 hello 查詢指定`&facet=city,count:5`，只有 hello 前五個唯一的城市與 hello 搜尋結果中的大部分文件中包含的 hello hello facet 結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-290">If hello query specifies `&facet=city,count:5`, only hello first five unique cities with hello most documents in hello search results are included in hello facet results.</span></span>

<span data-ttu-id="ac164-291">請注意 hello 區分 facet 結果和搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-291">Notice hello distinction between facet results and search results.</span></span> <span data-ttu-id="ac164-292">搜尋結果的所有符合 hello 查詢 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="ac164-292">Search results are all hello documents that match hello query.</span></span> <span data-ttu-id="ac164-293">Facet 結果的 hello 比對每個 facet 的值。</span><span class="sxs-lookup"><span data-stu-id="ac164-293">Facet results are hello matches for each facet value.</span></span> <span data-ttu-id="ac164-294">在 hello 範例中，搜尋結果會包含不在 hello facet 分類清單 (在本例中為 5) 的城市名稱。</span><span class="sxs-lookup"><span data-stu-id="ac164-294">In hello example, search results include City names that are not in hello facet classification list (5 in our example).</span></span> <span data-ttu-id="ac164-295">當您清除面向或選擇「城市」以外的其他面向時，系統會顯示透過多面向導覽篩選出的結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span></span> 

> [!NOTE]
> <span data-ttu-id="ac164-296">當有一種類型以上時討論 `count` 可能會讓人混淆。</span><span class="sxs-lookup"><span data-stu-id="ac164-296">Discussing `count` when there is more than one type can be confusing.</span></span> <span data-ttu-id="ac164-297">hello 下表提供如何使用 Azure 搜尋 API、 程式碼範例和文件中的 hello 詞彙的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="ac164-297">hello following table offers a brief summary of how hello term is used in Azure Search API, sample code, and documentation.</span></span> 

* `@colorFacet.count`<br/>
  <span data-ttu-id="ac164-298">呈現程式碼中，您應該看到 hello facet，facet 結果使用的 toodisplay hello 數目的計數參數。</span><span class="sxs-lookup"><span data-stu-id="ac164-298">In presentation code, you should see a count parameter on hello facet, used toodisplay hello number of facet results.</span></span> <span data-ttu-id="ac164-299">在 facet 結果中，計數會指出 hello 符合 hello facet 一詞或範圍的文件的數目。</span><span class="sxs-lookup"><span data-stu-id="ac164-299">In facet results, count indicates hello number of documents that match on hello facet term or range.</span></span>
* `&facet=City,count:12`<br/>
  <span data-ttu-id="ac164-300">在 facet 查詢中，您可以設定計數 tooa 值。</span><span class="sxs-lookup"><span data-stu-id="ac164-300">In a facet query, you can set count tooa value.</span></span>  <span data-ttu-id="ac164-301">hello 預設值為 10，但您可以將其高或較低。</span><span class="sxs-lookup"><span data-stu-id="ac164-301">hello default is 10, but you can set it higher or lower.</span></span> <span data-ttu-id="ac164-302">設定`count:12`取得文件計數的 hello facet 結果中的前 12 相符項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-302">Setting `count:12` gets hello top 12 matches in facet results by document count.</span></span>
* <span data-ttu-id="ac164-303">"`@odata.count`"</span><span class="sxs-lookup"><span data-stu-id="ac164-303">"`@odata.count`"</span></span><br/>
  <span data-ttu-id="ac164-304">Hello 查詢回應，這個值會表示 hello hello 搜尋結果中的相符項目數目。</span><span class="sxs-lookup"><span data-stu-id="ac164-304">In hello query response, this value indicates hello number of matching items in hello search results.</span></span> <span data-ttu-id="ac164-305">平均而言，大於 hello 總和的組合，因為 toohello 符合 hello 的搜尋詞彙的項目存在的所有 facet 結果，但有 facet 值相符的項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-305">On average, it’s larger than hello sum of all facet results combined, due toohello presence of items that match hello search term, but have no facet value matches.</span></span>

<span data-ttu-id="ac164-306">**取得面向結果中的計數**</span><span class="sxs-lookup"><span data-stu-id="ac164-306">**Get counts in facet results**</span></span>

<span data-ttu-id="ac164-307">當您新增篩選條件 tooa 多面向查詢時，您可能想 tooretain hello facet 陳述式 (例如， `facet=Rating&$filter=Rating ge 4`)。</span><span class="sxs-lookup"><span data-stu-id="ac164-307">When you add a filter tooa faceted query, you might want tooretain hello facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span></span> <span data-ttu-id="ac164-308">技術上來說，facet = 評等不需要但 4 及更新版本，讓它維持在傳回 hello 的評等的 facet 值的計數。</span><span class="sxs-lookup"><span data-stu-id="ac164-308">Technically, facet=Rating isn’t needed, but keeping it returns hello counts of facet values for ratings 4 and higher.</span></span> <span data-ttu-id="ac164-309">例如，如果您按一下"4"，並且在 hello 查詢包含一個篩選大於或等於的太"4"，計數會傳回每個評等為 4 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="ac164-309">For example, if you click "4" and hello query includes a filter for greater or equal too"4", counts are returned for each rating that is 4 and higher.</span></span>  

<span data-ttu-id="ac164-310">**確實取得精確的面向計數**</span><span class="sxs-lookup"><span data-stu-id="ac164-310">**Make sure you get accurate facet counts**</span></span>

<span data-ttu-id="ac164-311">在某些情況下，您可能會發現 facet 計數不符 hello 結果集 (請參閱[Azure 搜尋 （論壇貼文） 中的多面向導覽](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch))。</span><span class="sxs-lookup"><span data-stu-id="ac164-311">Under certain circumstances, you might find that facet counts do not match hello result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span></span>

<span data-ttu-id="ac164-312">Facet 計數可能會因為 toohello 分區化架構不正確。</span><span class="sxs-lookup"><span data-stu-id="ac164-312">Facet counts can be inaccurate due toohello sharding architecture.</span></span> <span data-ttu-id="ac164-313">每個搜尋索引有多個分區，以及每個分區的文件計數，也就結合成單一結果，以報告 hello 前 n 個 facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-313">Every search index has multiple shards, and each shard reports hello top N facets by document count, which is then combined into a single result.</span></span> <span data-ttu-id="ac164-314">如果某些分區有許多相符的值，而有些則擁有較少，您可能會發現某些 facet 值遺漏或下計數 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="ac164-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in hello results.</span></span>

<span data-ttu-id="ac164-315">雖然這種行為無法變更在任何時間，如果您今天出現這種行為，您可以解決它以人為方式因而誇大 hello 計數：<number> tooa 大型數字 tooenforce 完整報告每個分區。</span><span class="sxs-lookup"><span data-stu-id="ac164-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating hello count:<number> tooa large number tooenforce full reporting from each shard.</span></span> <span data-ttu-id="ac164-316">如果 hello 計數值： 是大於或等於 toohello 數字的 hello 欄位中的唯一值，保證精確的結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-316">If hello value of count: is greater than or equal toohello number of unique values in hello field, you are guaranteed accurate results.</span></span> <span data-ttu-id="ac164-317">不過，當文件計數很高的時候，則會有效能的負面影響，因此請謹慎使用此選項。</span><span class="sxs-lookup"><span data-stu-id="ac164-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span></span>

### <a name="user-interface-tips"></a><span data-ttu-id="ac164-318">使用者介面秘訣</span><span class="sxs-lookup"><span data-stu-id="ac164-318">User interface tips</span></span>
<span data-ttu-id="ac164-319">**針對多面向導覽中的各欄位新增標籤**</span><span class="sxs-lookup"><span data-stu-id="ac164-319">**Add labels for each field in facet navigation**</span></span>

<span data-ttu-id="ac164-320">Hello HTML 或表單中通常會定義標籤 (`index.cshtml` hello 範例應用程式中)。</span><span class="sxs-lookup"><span data-stu-id="ac164-320">Labels are typically defined in hello HTML or form (`index.cshtml` in hello sample application).</span></span> <span data-ttu-id="ac164-321">Azure 搜尋服務中沒有適用於多面向導覽標籤或任何其他中繼資料的 API。</span><span class="sxs-lookup"><span data-stu-id="ac164-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span></span>

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a><span data-ttu-id="ac164-322">根據範圍進行篩選</span><span class="sxs-lookup"><span data-stu-id="ac164-322">Filter based on a range</span></span>
<span data-ttu-id="ac164-323">透過值範圍進行面向化是常見的搜尋應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="ac164-323">Faceting over ranges of values is a common search application requirement.</span></span> <span data-ttu-id="ac164-324">範圍支援數值資料與日期時間值。</span><span class="sxs-lookup"><span data-stu-id="ac164-324">Ranges are supported for numeric data and DateTime values.</span></span> <span data-ttu-id="ac164-325">您可以在 [搜尋文件 (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)中閱讀各方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ac164-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span></span>

<span data-ttu-id="ac164-326">Azure Search 透過提供兩種方法進行範圍運算，來簡化範圍建構。</span><span class="sxs-lookup"><span data-stu-id="ac164-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span></span> <span data-ttu-id="ac164-327">對於這兩種方法，Azure 搜尋會建立適當的範圍，提供您所提供的 hello 輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="ac164-327">For both approaches, Azure Search creates hello appropriate ranges given hello inputs you’ve provided.</span></span> <span data-ttu-id="ac164-328">例如，如果您指定 10|20|30 的值範圍，它會自動建立 0-10、10-20、20-30 的範圍。</span><span class="sxs-lookup"><span data-stu-id="ac164-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span></span> <span data-ttu-id="ac164-329">您的應用程式可以選擇性地移除任何空白間隔。</span><span class="sxs-lookup"><span data-stu-id="ac164-329">Your application can optionally remove any intervals that are empty.</span></span> 

<span data-ttu-id="ac164-330">**方法 1： 使用 hello 間隔參數**</span><span class="sxs-lookup"><span data-stu-id="ac164-330">**Approach 1: Use hello interval parameter**</span></span>  
<span data-ttu-id="ac164-331">$10 增量 tooset 價格 facet，您會指定：`&facet=price,interval:10`</span><span class="sxs-lookup"><span data-stu-id="ac164-331">tooset price facets in $10 increments, you would specify: `&facet=price,interval:10`</span></span>

<span data-ttu-id="ac164-332">**方法 2︰使用值清單**</span><span class="sxs-lookup"><span data-stu-id="ac164-332">**Approach 2: Use a values list**</span></span>  
<span data-ttu-id="ac164-333">針對數值資料，您可以使用值清單。</span><span class="sxs-lookup"><span data-stu-id="ac164-333">For numeric data, you can use a values list.</span></span>  <span data-ttu-id="ac164-334">請考慮 hello facet 範圍`listPrice` 欄位中，呈現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac164-334">Consider hello facet range for a `listPrice` field, rendered as follows:</span></span>

  ![範例值清單][5]

<span data-ttu-id="ac164-336">toospecify facet 範圍喜歡 hello 中 hello 前面螢幕擷取畫面，請使用值清單：</span><span class="sxs-lookup"><span data-stu-id="ac164-336">toospecify a facet range like hello one in hello preceding screen shot, use a values list:</span></span>

    facet=listPrice,values:10|25|100|500|1000|2500

<span data-ttu-id="ac164-337">使用 0 做為起點，作為端點，hello 清單中的值，然後再加以剪裁 hello 前一個範圍 toocreate 離散間隔的內建的每個範圍。</span><span class="sxs-lookup"><span data-stu-id="ac164-337">Each range is built using 0 as a starting point, a value from hello list as an endpoint, and then trimmed of hello previous range toocreate discrete intervals.</span></span> <span data-ttu-id="ac164-338">Azure 搜尋服務會將這些動作做為多面向導覽的一部分來執行。</span><span class="sxs-lookup"><span data-stu-id="ac164-338">Azure Search does these things as part of faceted navigation.</span></span> <span data-ttu-id="ac164-339">您沒有 toowrite 建構每個間隔的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ac164-339">You do not have toowrite code for structuring each interval.</span></span>

### <a name="build-a-filter-for-a-range"></a><span data-ttu-id="ac164-340">針對範圍建置篩選條件</span><span class="sxs-lookup"><span data-stu-id="ac164-340">Build a filter for a range</span></span>
<span data-ttu-id="ac164-341">根據您選取的範圍 toofilter 文件，您可以使用 hello`"ge"`和`"lt"`篩選定義 hello 端點 hello 範圍的兩段式運算式中的運算子。</span><span class="sxs-lookup"><span data-stu-id="ac164-341">toofilter documents based on a range you select, you can use hello `"ge"` and `"lt"` filter operators in a two-part expression that defines hello endpoints of hello range.</span></span> <span data-ttu-id="ac164-342">例如，如果您選擇 hello 範圍 10 到 25 的`listPrice`的欄位，就是 hello 篩選`$filter=listPrice ge 10 and listPrice lt 25`。</span><span class="sxs-lookup"><span data-stu-id="ac164-342">For example, if you choose hello range 10-25 for a `listPrice` field, hello filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span></span> <span data-ttu-id="ac164-343">Hello 範例程式碼，在 hello 篩選條件運算式會使用**priceFrom**和**priceTo**參數 tooset hello 端點。</span><span class="sxs-lookup"><span data-stu-id="ac164-343">In hello sample code, hello filter expression uses **priceFrom** and **priceTo** parameters tooset hello endpoints.</span></span> 

  ![查詢某範圍的值][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a><span data-ttu-id="ac164-345">根據距離進行篩選</span><span class="sxs-lookup"><span data-stu-id="ac164-345">Filter based on distance</span></span>
<span data-ttu-id="ac164-346">它的通用 toosee 篩選可協助您選擇商店、 餐廳或目的地的鄰近 tooyour 目前位置。</span><span class="sxs-lookup"><span data-stu-id="ac164-346">It’s common toosee filters that help you choose a store, restaurant, or destination based on its proximity tooyour current location.</span></span> <span data-ttu-id="ac164-347">這類型的篩選條件看起來像是多面向導覽，但實際上只是篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ac164-347">While this type of filter might look like faceted navigation, it’s just a filter.</span></span> <span data-ttu-id="ac164-348">對於那些特別要尋找特定設計問題之實作建議的使用者，我們會在此處說明。</span><span class="sxs-lookup"><span data-stu-id="ac164-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span></span>

<span data-ttu-id="ac164-349">搜尋服務中有兩種地理空間函式，**geo.distance** 與 **geo.intersects**。</span><span class="sxs-lookup"><span data-stu-id="ac164-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span></span>

* <span data-ttu-id="ac164-350">hello **geo.distance**函式以公里為單位傳回 hello 距離兩個點之間。</span><span class="sxs-lookup"><span data-stu-id="ac164-350">hello **geo.distance** function returns hello distance in kilometers between two points.</span></span> <span data-ttu-id="ac164-351">一個點是一個欄位，而另一個則 hello 篩選條件一部分傳遞的常數。</span><span class="sxs-lookup"><span data-stu-id="ac164-351">One point is a field and other is a constant passed as part of hello filter.</span></span> 
* <span data-ttu-id="ac164-352">hello **geo.intersects**函數會傳回 true，如果在給定的多邊形內，則指定的點。</span><span class="sxs-lookup"><span data-stu-id="ac164-352">hello **geo.intersects** function returns true if a given point is within a given polygon.</span></span> <span data-ttu-id="ac164-353">hello 點是欄位，hello 多邊形會指定為座標做為 hello 篩選條件一部分傳遞的常數清單。</span><span class="sxs-lookup"><span data-stu-id="ac164-353">hello point is a field and hello polygon is specified as a constant list of coordinates passed as part of hello filter.</span></span>

<span data-ttu-id="ac164-354">您可以在 [OData 運算式語法 (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx)中找到篩選條件範例。</span><span class="sxs-lookup"><span data-stu-id="ac164-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span></span>

<a name="tryitout"></a>

## <a name="try-hello-demo"></a><span data-ttu-id="ac164-355">請嘗試 hello 示範</span><span class="sxs-lookup"><span data-stu-id="ac164-355">Try hello demo</span></span>
<span data-ttu-id="ac164-356">hello Azure 搜尋作業入口網站示範包含參考本文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="ac164-356">hello Azure Search Job Portal Demo contains hello examples referenced in this article.</span></span>

-   <span data-ttu-id="ac164-357">請參閱和測試 hello 工作示範線上在[Azure 搜尋作業入口網站示範](http://azjobsdemo.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="ac164-357">See and test hello working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="ac164-358">下載 hello 程式碼從 hello [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)。</span><span class="sxs-lookup"><span data-stu-id="ac164-358">Download hello code from hello [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

<span data-ttu-id="ac164-359">當您使用的搜尋結果時，觀賞 hello URL 查詢建構中的變更。</span><span class="sxs-lookup"><span data-stu-id="ac164-359">As you work with search results, watch hello URL for changes in query construction.</span></span> <span data-ttu-id="ac164-360">當您選取每個此應用程式就會發生 tooappend facet toohello URI。</span><span class="sxs-lookup"><span data-stu-id="ac164-360">This application happens tooappend facets toohello URI as you select each one.</span></span>

1. <span data-ttu-id="ac164-361">toouse hello 對應功能的 hello 示範應用程式取得 Bing 地圖服務金鑰從 hello [Bing 地圖服務開發人員中心](https://www.bingmapsportal.com/)。</span><span class="sxs-lookup"><span data-stu-id="ac164-361">toouse hello mapping functionality of hello demo app, get a Bing Maps key from hello [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="ac164-362">將它貼入 hello hello 中的現有金鑰`index.cshtml`頁面。</span><span class="sxs-lookup"><span data-stu-id="ac164-362">Paste it over hello existing key in hello `index.cshtml` page.</span></span> <span data-ttu-id="ac164-363">hello `BingApiKey` hello 中設定`Web.config`不是檔案。</span><span class="sxs-lookup"><span data-stu-id="ac164-363">hello `BingApiKey` setting in hello `Web.config` file is not used.</span></span> 

2. <span data-ttu-id="ac164-364">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac164-364">Run hello application.</span></span> <span data-ttu-id="ac164-365">導覽 hello 選擇性，或關閉 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ac164-365">Take hello optional tour, or dismiss hello dialog box.</span></span>
   
3. <span data-ttu-id="ac164-366">輸入搜尋詞彙，例如 「 分析師 」，然後按一下 hello 搜尋圖示。</span><span class="sxs-lookup"><span data-stu-id="ac164-366">Enter a search term, such as "analyst", and click hello Search icon.</span></span> <span data-ttu-id="ac164-367">hello 查詢執行速度快速。</span><span class="sxs-lookup"><span data-stu-id="ac164-367">hello query executes quickly.</span></span>
   
   <span data-ttu-id="ac164-368">多面向導覽結構也會傳回與 hello 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-368">A faceted navigation structure is also returned with hello search results.</span></span> <span data-ttu-id="ac164-369">Hello 搜尋結果 頁面上，在 hello 多面向導覽結構會包含每個 facet 結果的計數。</span><span class="sxs-lookup"><span data-stu-id="ac164-369">In hello search result page, hello faceted navigation structure includes counts for each facet result.</span></span> <span data-ttu-id="ac164-370">我們並未選取任何面向，因此會傳回所有符合的結果。</span><span class="sxs-lookup"><span data-stu-id="ac164-370">No facets are selected, so all matching results are returned.</span></span>
   
   ![選取面向之前的搜尋結果][11]

4. <span data-ttu-id="ac164-372">按一下 [職稱]、[位置] 或 [最低工資]。</span><span class="sxs-lookup"><span data-stu-id="ac164-372">Click a Business Title, Location, or Minimum Salary.</span></span> <span data-ttu-id="ac164-373">Facet null hello 初始搜尋，但因為他們接受的值，則會修剪 hello 搜尋結果不再符合的項目。</span><span class="sxs-lookup"><span data-stu-id="ac164-373">Facets were null on hello initial search, but as they take on values, hello search results are trimmed of items that no longer match.</span></span>
   
   ![選取面向之後的搜尋結果][12]

5. <span data-ttu-id="ac164-375">tooclear hello 多面向查詢，以便您可以嘗試不同的查詢行為，請按一下 hello `[X]` hello 選取 facet tooclear hello facet 之後。</span><span class="sxs-lookup"><span data-stu-id="ac164-375">tooclear hello faceted query so that you can try different query behaviors, click hello `[X]` after hello selected facets tooclear hello facets.</span></span>
   
<a name="nextstep"></a>

## <a name="learn-more"></a><span data-ttu-id="ac164-376">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="ac164-376">Learn more</span></span>
<span data-ttu-id="ac164-377">觀賞[深入了解 Azure 搜尋服務](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)。</span><span class="sxs-lookup"><span data-stu-id="ac164-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span></span> <span data-ttu-id="ac164-378">在 45:25，沒有示範如何 tooimplement facet。</span><span class="sxs-lookup"><span data-stu-id="ac164-378">At 45:25, there is a demo on how tooimplement facets.</span></span>

<span data-ttu-id="ac164-379">更多深入多面向導覽的設計原則的詳細資訊，我們建議下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="ac164-379">For more insights on design principles for faceted navigation, we recommend hello following links:</span></span>

* [<span data-ttu-id="ac164-380">多面向搜尋的設計</span><span class="sxs-lookup"><span data-stu-id="ac164-380">Designing for Faceted Search</span></span>](http://www.uie.com/articles/faceted_search/)
* [<span data-ttu-id="ac164-381">設計模式：多面向導覽</span><span class="sxs-lookup"><span data-stu-id="ac164-381">Design Patterns: Faceted Navigation</span></span>](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

