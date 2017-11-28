---
title: "如何在 Azure 搜尋服務中實作多面向導覽 | Microsoft Docs"
description: "將「多面向導覽」加入與 Azure 搜尋服務 (Microsoft Azure 上之託管的雲端搜尋服務) 整合的應用程式。"
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
ms.openlocfilehash: 413f498eeb0bbc9a971c7a65200ed2fd8caa9aaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-implement-faceted-navigation-in-azure-search"></a><span data-ttu-id="f3a6e-103">如何在 Azure 搜尋服務中實作多面向導覽</span><span class="sxs-lookup"><span data-stu-id="f3a6e-103">How to implement faceted navigation in Azure Search</span></span>
<span data-ttu-id="f3a6e-104">多面向導覽是一個篩選機制，它在搜尋應用程式中提供自動導向的向下鑽研導覽。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span></span> <span data-ttu-id="f3a6e-105">「多面向導覽」一詞可能讓您感到陌生，但您可能早已使用過它。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-105">The term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span></span> <span data-ttu-id="f3a6e-106">如下列範例所示，多面向導覽其實就是用來篩選結果的類別。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-106">As the following example shows, faceted navigation is nothing more than the categories used to filter results.</span></span>

 ![Azure 搜尋服務作業入口網站示範][1]

<span data-ttu-id="f3a6e-108">多面向導覽是替代的搜尋進入點。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-108">Faceted navigation is an alternative entry point to search.</span></span> <span data-ttu-id="f3a6e-109">它提供了方便的替代功能，讓您不必手動輸入複雜搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-109">It offers a convenient alternative to typing complex search expressions by hand.</span></span> <span data-ttu-id="f3a6e-110">多面向可協助您找到要找的項目，同時確保您不會得到沒有項目的結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span></span> <span data-ttu-id="f3a6e-111">身為開發人員，面向可讓您將最有用的搜尋準則公開，以導覽您的搜尋主體。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-111">As a developer, facets let you expose the most useful search criteria for navigating your search corpus.</span></span> <span data-ttu-id="f3a6e-112">在線上零售應用程式中，通常會根據品牌、部門 (童鞋)、尺寸、價格、熱門程度和評分來建置多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span></span> 

<span data-ttu-id="f3a6e-113">實作多面向導覽會因各搜尋技術而不同。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-113">Implementing faceted navigation differs across search technologies.</span></span> <span data-ttu-id="f3a6e-114">在 Azure 搜尋服務中，多面向導覽會在查詢時使用您先前歸屬在結構描述中的欄位來建置。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span></span>

-   <span data-ttu-id="f3a6e-115">在應用程式所建置的查詢中，查詢必須傳送「面向查詢參數」，以取得該文件結果集的可用面向篩選值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-115">In the queries that your application builds, a query must send *facet query parameters* to get the available facet filter values for that document result set.</span></span>

-   <span data-ttu-id="f3a6e-116">若要實際修剪文件結果集，應用程式還必須套用 `$filter` 運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-116">To actually trim the document result set, the application must also apply a `$filter` expression.</span></span>

<span data-ttu-id="f3a6e-117">在您的應用程式開發中，撰寫建構查詢的程式碼，而這些查詢構成整體工作的一大部分。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-117">In your application development, writing code that constructs queries constitutes the bulk of the work.</span></span> <span data-ttu-id="f3a6e-118">此服務提供大部分您希望從多面向導覽獲得的應用程式行為，包括定義範圍和取得面向結果計數的內建支援。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-118">Many of the application behaviors that you would expect from faceted navigation are provided by the service, including built-in support for defining ranges and getting counts for facet results.</span></span> <span data-ttu-id="f3a6e-119">服務也包含合理的預設值，能協助您避免難處理的導覽結構。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-119">The service also includes sensible defaults that help you avoid unwieldy navigation structures.</span></span> 

## <a name="sample-code-and-demo"></a><span data-ttu-id="f3a6e-120">程式碼範例和示範</span><span class="sxs-lookup"><span data-stu-id="f3a6e-120">Sample code and demo</span></span>
<span data-ttu-id="f3a6e-121">本文使用作業搜尋入口網站來作為範例。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-121">This article uses a job search portal as an example.</span></span> <span data-ttu-id="f3a6e-122">此範例會實作為 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-122">The example is implemented as an ASP.NET MVC application.</span></span>

-   <span data-ttu-id="f3a6e-123">請在 [Azure 搜尋服務作業入口網站示範](http://azjobsdemo.azurewebsites.net/)參閱運作示範並進行線上測試。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-123">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="f3a6e-124">從 [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)下載程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-124">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

## <a name="get-started"></a><span data-ttu-id="f3a6e-125">開始使用</span><span class="sxs-lookup"><span data-stu-id="f3a6e-125">Get started</span></span>
<span data-ttu-id="f3a6e-126">如果您不了解搜尋開發，最好的方法就是把多面向導覽想成它會顯示自動導向搜尋的可能選項。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-126">If you're new to search development, the best way to think of faceted navigation is that it shows the possibilities for self-directed search.</span></span> <span data-ttu-id="f3a6e-127">它是向下鑽研搜尋體驗的一種，基於預先定義的篩選條件，可以藉由「指向並按一下」的動作快速縮減搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span></span> 

### <a name="interaction-model"></a><span data-ttu-id="f3a6e-128">互動模型</span><span class="sxs-lookup"><span data-stu-id="f3a6e-128">Interaction model</span></span>

<span data-ttu-id="f3a6e-129">多面向導覽的搜尋體驗是反覆進行，因此，讓我們先將它理解成一連串回應使用者動作而展開的查詢。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-129">The search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response to user actions.</span></span>

<span data-ttu-id="f3a6e-130">起點是一個提供多面向導覽 (通常位在側邊) 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-130">The starting point is an application page that provides faceted navigation, typically placed on the periphery.</span></span> <span data-ttu-id="f3a6e-131">多面向導覽通常是樹狀結構，且每個值有核取方塊，或可點選的文字。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span></span> 

1. <span data-ttu-id="f3a6e-132">傳送到 Azure 搜尋服務會透過一或多個多面向查詢參數指定多面向導覽結構。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-132">A query sent to Azure Search specifies the faceted navigation structure via one or more facet query parameters.</span></span> <span data-ttu-id="f3a6e-133">例如，查詢可能包括 `facet=Rating`，可能還有 `:values` 或 `:sort` 選項，以進一步精簡展示。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-133">For instance, the query might include `facet=Rating`, perhaps with a `:values` or `:sort` option to further refine the presentation.</span></span>
2. <span data-ttu-id="f3a6e-134">展示層會使用要求上的面向來轉譯提供多面向導覽的頁面。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-134">The presentation layer renders a search page that provides faceted navigation, using the facets specified on the request.</span></span>
3. <span data-ttu-id="f3a6e-135">舉包含「評分」的多面向導覽結構為例，您按一下「4」表示只會顯示評分為 4 或更高的產品。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-135">Given a faceted navigation structure that includes Rating, you click "4" to indicate that only products with a rating of 4 or higher should be shown.</span></span> 
4. <span data-ttu-id="f3a6e-136">應用程式會傳送包含 `$filter=Rating ge 4`</span><span class="sxs-lookup"><span data-stu-id="f3a6e-136">In response, the application sends a query that includes `$filter=Rating ge 4`</span></span> 
5. <span data-ttu-id="f3a6e-137">展示層會更新頁面，並顯示精簡過的結果集，其中只包含滿足新準則 (此案例中是評分為 4 或更高) 的產品。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-137">The presentation layer updates the page, showing a reduced result set, containing just those items that satisfy the new criteria (in this case, products rated 4 and up).</span></span>

<span data-ttu-id="f3a6e-138">面向是查詢參數，但不要將它與查詢輸入混淆了。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-138">A facet is a query parameter, but do not confuse it with query input.</span></span> <span data-ttu-id="f3a6e-139">它在查詢中不是當作選取準則。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-139">It is never used as selection criteria in a query.</span></span> <span data-ttu-id="f3a6e-140">反之，將面向查詢參數想成是，返回的回應中所包含對導覽結構的輸入。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-140">Instead, think of facet query parameters as inputs to the navigation structure that comes back in the response.</span></span> <span data-ttu-id="f3a6e-141">對於提供的每個面向查詢參數，Azure 搜尋服務會評估每個面向值的部分結果中有多少文件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in the partial results for each facet value.</span></span>

<span data-ttu-id="f3a6e-142">請注意步驟 4 中的 `$filter` 。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-142">Notice the `$filter` in step 4.</span></span> <span data-ttu-id="f3a6e-143">此篩選是多面向導覽中的一個重要層面。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-143">The filter is an important aspect of faceted navigation.</span></span> <span data-ttu-id="f3a6e-144">雖然面向和篩選條件在 API 中是獨立的，但您會需要兩者來提供您想要的體驗。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-144">Although facets and filters are independent in the API, you need both to deliver the experience you intend.</span></span> 

### <a name="app-design-pattern"></a><span data-ttu-id="f3a6e-145">應用程式設計模式</span><span class="sxs-lookup"><span data-stu-id="f3a6e-145">App design pattern</span></span>

<span data-ttu-id="f3a6e-146">在應用程式程式碼中，模式為使用面向查詢參數來傳回多面向導覽結構和面向結果，並外加一個 $filter 運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-146">In application code, the pattern is to use facet query parameters to return the faceted navigation structure along with facet results, plus a $filter expression.</span></span>  <span data-ttu-id="f3a6e-147">篩選條件運算式會處理面向值的點擊事件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-147">The filter expression handles the click event on the facet value.</span></span> <span data-ttu-id="f3a6e-148">將 `$filter` 運算式想成修剪傳回展示層之結果的程式碼</span><span class="sxs-lookup"><span data-stu-id="f3a6e-148">Think of the `$filter` expression as the code behind the actual trimming of search results returned to the presentation layer.</span></span> <span data-ttu-id="f3a6e-149">舉「色彩」的面向為例，按一下 [紅色] 這個色彩是透過只選取有紅色這個色彩的項目之 `$filter` 運算式來實作。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-149">Given a Colors facet, clicking the color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span></span> 

### <a name="query-basics"></a><span data-ttu-id="f3a6e-150">查詢基本概念</span><span class="sxs-lookup"><span data-stu-id="f3a6e-150">Query basics</span></span>

<span data-ttu-id="f3a6e-151">在 Azure 搜尋服務中，要求是透過一或多個查詢參數 (如需個別的詳細描述，請參閱 [搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx) ) 指定。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span></span> <span data-ttu-id="f3a6e-152">沒有任何一個查詢參數是必要的，但您至少要有一個才能讓查詢有效。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-152">None of the query parameters are required, but you must have at least one in order for a query to be valid.</span></span>

<span data-ttu-id="f3a6e-153">精確度 (視為篩選並排除不相關項目的能力) 是透過下列運算式而達到：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-153">Precision, understood as the ability to filter out irrelevant hits, is achieved through one or both of these expressions:</span></span>

-   <span data-ttu-id="f3a6e-154">**搜尋=**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-154">**search=**</span></span>  
    <span data-ttu-id="f3a6e-155">此參數的值構成搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-155">The value of this parameter constitutes the search expression.</span></span> <span data-ttu-id="f3a6e-156">它可能為單一的文字，或包括多個名詞和運算子的複雜搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span></span> <span data-ttu-id="f3a6e-157">在伺服器上，搜尋運算式用於進行全文檢索搜尋、針對符合的單字查詢索引中可搜尋的欄位、按順位順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-157">On the server, a search expression is used for full-text search, querying searchable fields in the index for matching terms, returning results in rank order.</span></span> <span data-ttu-id="f3a6e-158">如果您將 `search` 設為 null，查詢會在整個索引執行 (也就是 `search=*`)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-158">If you set `search` to null, query execution is over the entire index (that is, `search=*`).</span></span> <span data-ttu-id="f3a6e-159">在此情況下，查詢的其他元素 (例如 `$filter` 或評分設定檔) 是影響所傳回文件 `($filter`，以及順序 (`scoringProfile` 或 `$orderby`) 的主要因素。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-159">In this case, other elements of the query, such as a `$filter` or scoring profile, are the primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span></span>

-   <span data-ttu-id="f3a6e-160">**$filter=**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-160">**$filter=**</span></span>  
    <span data-ttu-id="f3a6e-161">篩選器是一個強大的機制，可以根據指定的文件屬性限制搜尋結果的大小。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-161">A filter is a powerful mechanism for limiting the size of search results based on the values of specific document attributes.</span></span> <span data-ttu-id="f3a6e-162">`$filter` 會先被評估，接著是會產生每個值的可用值和對應計數的多面向邏輯。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-162">A `$filter` is evaluated first, followed by faceting logic that generates the available values and corresponding counts for each value</span></span>

<span data-ttu-id="f3a6e-163">複雜的搜尋運算式會降低查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-163">Complex search expressions decrease the performance of the query.</span></span> <span data-ttu-id="f3a6e-164">盡可能使用建構良好的篩選條件運算式，來提高精確度並改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-164">Where possible, use well-constructed filter expressions to increase precision and improve query performance.</span></span>

<span data-ttu-id="f3a6e-165">為了更明白篩選器如何提高精確度，請將一個複雜的搜尋運算式，與包含下列篩選運算式的搜尋預算式進行比較：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-165">To better understand how a filter adds more precision, compare a complex search expression to one that includes a filter expression:</span></span>

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

<span data-ttu-id="f3a6e-166">兩個查詢都有效，但如果您是尋找「位在西雅圖且有停車位的非汽車旅館」，後者會是較佳的查詢。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-166">Both queries are valid, but the second is superior if you’re looking for non-motels with parking in Seattle.</span></span>
-   <span data-ttu-id="f3a6e-167">第一個查詢依賴字串欄位 (例如「名稱」、「描述」及其他包含可搜尋資料的欄位) 是否提及指定的文字。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-167">The first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span></span>
-   <span data-ttu-id="f3a6e-168">第二個查詢是尋找精確符合的結構化資料，且可能較為正確。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-168">The second query looks for precise matches on structured data and is likely to be much more accurate.</span></span>

<span data-ttu-id="f3a6e-169">在包含多面向導覽的應用程式中，請確定每個透過多面向導覽結構進行的使用者動作都伴隨搜尋結果縮減。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span></span> <span data-ttu-id="f3a6e-170">若要縮減結果，請使用篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-170">To narrow results, use a filter expression.</span></span>

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a><span data-ttu-id="f3a6e-171">建置多面向導覽應用程式</span><span class="sxs-lookup"><span data-stu-id="f3a6e-171">Build a faceted navigation app</span></span>
<span data-ttu-id="f3a6e-172">您可以在建置搜尋要求的應用程式程式碼中，實作使用 Azure 搜尋服務的多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-172">You implement faceted navigation with Azure Search in your application code that builds the search request.</span></span> <span data-ttu-id="f3a6e-173">多面向導覽會依賴您先前在結構描述中定義的元素。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-173">The faceted navigation relies on elements in your schema that you defined previously.</span></span>

<span data-ttu-id="f3a6e-174">`Facetable [true|false]` 索引屬性預先定義在您的搜尋索引中，且設定在所選取的欄位，以便在多面向導覽結構中啟用或停用他們。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-174">Predefined in your search index is the `Facetable [true|false]` index attribute, set on selected fields to enable or disable their use in a faceted navigation structure.</span></span> <span data-ttu-id="f3a6e-175">若沒有 `"Facetable" = true`，該欄位就不能在多面向導覽中使用。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span></span>

<span data-ttu-id="f3a6e-176">您程式碼中的展示層提供使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-176">The presentation layer in your code provides the user experience.</span></span> <span data-ttu-id="f3a6e-177">它應該列示多面向導覽的組成部份，例如標籤、值、核取方塊和計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-177">It should list the constituent parts of the faceted navigation, such as the label, values, check boxes, and the count.</span></span> <span data-ttu-id="f3a6e-178">Azure 搜尋服務 REST API 不限於任何平台，因此您可以使用任何想要的語言和平台。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-178">The Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span></span> <span data-ttu-id="f3a6e-179">重要的是要包含支援累加式重新整理的 UI 元素，當選取額外的面向便會更新 UI 狀態。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-179">The important thing is to include UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span></span> 

<span data-ttu-id="f3a6e-180">查詢的時候，應用程式程式碼會建立包含 `facet=[string]`要求參數的要求，它會提供要進行面向篩選的欄位。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides the field to facet by.</span></span> <span data-ttu-id="f3a6e-181">一個查詢可以有多個面向，例如 `&facet=color&facet=category&facet=rating`，每個面向都以 & 符號分隔。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span></span>

<span data-ttu-id="f3a6e-182">應用程式程式碼也必須建構 `$filter` 運算式來處理多面向導覽中的點選事件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-182">Application code must also construct a `$filter` expression to handle the click events in faceted navigation.</span></span> <span data-ttu-id="f3a6e-183">`$filter` 會使用面向值當作篩選準則將搜尋結果縮減。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-183">A `$filter` reduces the search results, using the facet value as filter criteria.</span></span>

<span data-ttu-id="f3a6e-184">Azure 搜尋服務會根據您輸入的一或多個字詞，以及多面向導覽結構的更新，來傳回搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-184">Azure Search returns the search results, based on one or more terms that you enter, along with updates to the faceted navigation structure.</span></span> <span data-ttu-id="f3a6e-185">在 Azure 搜尋服務中，多面向導覽是單一層級的結構，其中包含面向值及其找到結果的計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span></span>

<span data-ttu-id="f3a6e-186">在接下來的章節中，我們將進一步了解如何建立各個部份。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-186">In the following sections, we take a closer look at how to build each part.</span></span>

<a name="buildindex"></a>

## <a name="build-the-index"></a><span data-ttu-id="f3a6e-187">建置索引</span><span class="sxs-lookup"><span data-stu-id="f3a6e-187">Build the index</span></span>
<span data-ttu-id="f3a6e-188">多面向的功能是透過索引中各欄位的 `"Facetable": true`索引屬性來啟用。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-188">Faceting is enabled on a field-by-field basis in the index, via this index attribute: `"Facetable": true`.</span></span>  
<span data-ttu-id="f3a6e-189">根據預設，所有可能用於多面向導覽的欄位類型為 `Facetable` 。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span></span> <span data-ttu-id="f3a6e-190">這類欄位類型包括 `Edm.String`、`Edm.DateTimeOffset`，以及所有數值欄位類型 (基本上所有欄位類型都可用於多面向導覽，除了 `Edm.GeographyPoint`)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all the numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span></span> 

<span data-ttu-id="f3a6e-191">在建置索引時，多面向導覽的最佳作法是關閉不應做為面向之欄位的多面向功能。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-191">When building an index, a best practice for faceted navigation is to explicitly turn faceting off for fields that should never be used as a facet.</span></span>  <span data-ttu-id="f3a6e-192">尤其是單一值的字串欄位 (例如識別碼或產品名稱)，應該將它們設為 `"Facetable": false` 以防止意外被用於多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-192">In particular, string fields for singleton values, such as an ID or product name, should be set to `"Facetable": false` to prevent their accidental (and ineffective) use in faceted navigation.</span></span> <span data-ttu-id="f3a6e-193">關閉不需要的多面向功能可讓索引的大小比較小，而且通常會增進效能。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-193">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

<span data-ttu-id="f3a6e-194">以下是「作業入口網站示範」應用程式範例之結構描述的一部分 (已修剪一些屬性來減少大小)：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-194">Following is part of the schema for the Job Portal Demo sample app, trimmed of some attributes to reduce the size:</span></span>

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

<span data-ttu-id="f3a6e-195">如您在結構描述範例中所見，我們已針對不應作為面向的字串欄位 (例如識別碼值) 關閉 `Facetable`。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-195">As you can see in the sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span></span> <span data-ttu-id="f3a6e-196">關閉不需要的多面向功能可讓索引的大小比較小，而且通常會增進效能。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-196">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

> [!TIP]
> <span data-ttu-id="f3a6e-197">根據最佳作法，建議每個欄位都包含整組完整的索引屬性。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-197">As a best practice, include the full set of index attributes for each field.</span></span> <span data-ttu-id="f3a6e-198">雖然幾乎所有欄位的 `Facetable` 預設都為開啟，但刻意設定每個屬性，可協助您仔細思考每個結構描述的決定。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through the implications of each schema decision.</span></span> 

<a name="checkdata"></a>

## <a name="check-the-data"></a><span data-ttu-id="f3a6e-199">檢查資料</span><span class="sxs-lookup"><span data-stu-id="f3a6e-199">Check the data</span></span>
<span data-ttu-id="f3a6e-200">資料品質會直接影響所具體化的多面向導覽結構是否符合您的預期。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-200">The quality of your data has a direct effect on whether the faceted navigation structure materializes as you expect it to.</span></span> <span data-ttu-id="f3a6e-201">它也會影響建構篩選器來減少結果集的作業容易與否。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-201">It also affects the ease of constructing filters to reduce the result set.</span></span>

<span data-ttu-id="f3a6e-202">若您想要根據「品牌」或「價格」進行多面向導覽，每個文件就應包含 BrandName 和 ProductPrice 值，它們要像篩選選項般有效且一致，並能提昇效率。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-202">If you want to facet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span></span>

<span data-ttu-id="f3a6e-203">以下是一些需要注意的提醒事項：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-203">Here are a few reminders of what to scrub for:</span></span>

* <span data-ttu-id="f3a6e-204">思考每個要用於多面向導覽的欄位，是否包含適合在自動導向搜尋中，當作篩選條件的值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-204">For every field that you want to facet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span></span> <span data-ttu-id="f3a6e-205">該值應簡短、具描述性，且能在對照的選項之間，提供可有效分辨的明確選擇。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-205">The values should be short, descriptive, and sufficiently distinctive to offer a clear choice between competing options.</span></span>
* <span data-ttu-id="f3a6e-206">拼字錯誤或近似符合的值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-206">Misspellings or nearly matching values.</span></span> <span data-ttu-id="f3a6e-207">如果您根據「色彩」進行多面向導覽，且欄位值包含 Orange 和 Ornage (拼字錯誤)，根據「色彩」欄位的面向應該兩者都採用。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on the Color field would pick up both.</span></span>
* <span data-ttu-id="f3a6e-208">混合大小寫的文字對多面向導覽也會遭成嚴重影響 (orange 和 Orange 為兩個不同的值)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span></span> 
* <span data-ttu-id="f3a6e-209">同一個植的單數和附數版本會導致個別的面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-209">Single and plural versions of the same value can result in a separate facet for each.</span></span>

<span data-ttu-id="f3a6e-210">正如您所想，準備資料的評鑑部份，是建置有效的多面向導覽之必要層面。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-210">As you can imagine, diligence in preparing the data is an essential aspect of effective faceted navigation.</span></span>

<a name="presentationlayer"></a>

## <a name="build-the-ui"></a><span data-ttu-id="f3a6e-211">建置 UI</span><span class="sxs-lookup"><span data-stu-id="f3a6e-211">Build the UI</span></span>
<span data-ttu-id="f3a6e-212">從展示層反向做起可協助您發現從另一方向可能忽略的需求，並了解搜尋體驗的必要功能有哪些。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-212">Working back from the presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential to the search experience.</span></span>

<span data-ttu-id="f3a6e-213">以多面向導覽而言，您的網頁或應用程式頁面會顯示多面向導覽結構，偵測頁面上的使用者輸入，並插入變更的元素。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-213">In terms of faceted navigation, your web or application page displays the faceted navigation structure, detects user input on the page, and inserts the changed elements.</span></span> 

<span data-ttu-id="f3a6e-214">對於 Web 應用程式，展示層通常是使用 AJAX，因為它可讓您重新整理累加的變更。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-214">For web applications, AJAX is commonly used in the presentation layer because it allows you to refresh incremental changes.</span></span> <span data-ttu-id="f3a6e-215">您也可以使用 ASP.NET MVC，或任何其他可透過 HTTP 連線到 Azure 搜尋服務的虛擬平台。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-215">You could also use ASP.NET MVC or any other visualization platform that can connect to an Azure Search service over HTTP.</span></span> <span data-ttu-id="f3a6e-216">這整篇文章所參考的範例應用程式 (**Azure 搜尋服務作業入口網站示範**)，恰好是一個 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-216">The sample application referenced throughout this article -- the **Azure Search Job Portal Demo** – happens to be an ASP.NET MVC application.</span></span>

<span data-ttu-id="f3a6e-217">在範例中，多面向導覽會內建在搜尋結果頁面。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-217">In the sample, faceted navigation is built into the search results page.</span></span> <span data-ttu-id="f3a6e-218">下列範例取自應用程式範例的 `index.cshtml` 檔案，它會顯示可在搜尋結果頁面顯示多面向導覽的靜態 HTML 結構。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-218">The following example, taken from the `index.cshtml` file of the sample application, shows the static HTML structure for displaying faceted navigation on the search results page.</span></span> <span data-ttu-id="f3a6e-219">當您提交搜尋詞彙或是選取或清除面向時，系統便會動態建置或重建面向清單。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-219">The list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span></span>

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

<span data-ttu-id="f3a6e-220">下列來自 `index.cshtml` 頁面的程式碼片段會動態建置 HTML，以顯示第一個面向 (職稱)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-220">The following code snippet from the `index.cshtml` page dynamically builds the HTML to display the first facet, Business Title.</span></span> <span data-ttu-id="f3a6e-221">類似的函式會動態建置其他面向的 HTML。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-221">Similar functions dynamically build the HTML for the other facets.</span></span> <span data-ttu-id="f3a6e-222">每個面向都有標籤和計數，以顯示針對該面向結果所找到的項目數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-222">Each facet has a label and a count, which displays the number of items found for that facet result.</span></span>

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
> <span data-ttu-id="f3a6e-223">在設計搜尋結果頁面時，請記得加入清除面向的機制。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-223">When you design the search results page, remember to add a mechanism for clearing facets.</span></span> <span data-ttu-id="f3a6e-224">如果您新增核取方塊，即可輕鬆地了解如何清除篩選條件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-224">If you add check boxes, you can easily see how to clear the filters.</span></span> <span data-ttu-id="f3a6e-225">針對其他配置，您可能需要階層模式或其他具創意的方法。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span></span> <span data-ttu-id="f3a6e-226">例如，在「作業搜尋入口網站」應用程式範例中，您可以按一下所選面向後的 `[X]` 以清除該面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-226">For example, in the Job Search Portal sample application, you can click the `[X]` after a selected facet to clear the facet.</span></span>

<a name="buildquery"></a>

## <a name="build-the-query"></a><span data-ttu-id="f3a6e-227">建置查詢</span><span class="sxs-lookup"><span data-stu-id="f3a6e-227">Build the query</span></span>
<span data-ttu-id="f3a6e-228">您所撰寫用於建置查詢的程式碼，應指定有效查詢的所有部份，包括搜尋運算式、面向、篩選條件、評分設定檔 (制訂要求使用的任何項目)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-228">The code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used to formulate a request.</span></span> <span data-ttu-id="f3a6e-229">在本節中，我們會探索面向在查詢中的位置，及篩選條件如何配合面向使用以提供縮減的結果集。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-229">In this section, we explore where facets fit into a query, and how filters are used with facets to deliver a reduced result set.</span></span>

<span data-ttu-id="f3a6e-230">請注意，面向在此範例應用程式中是必要的。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-230">Notice that facets are integral in this sample application.</span></span> <span data-ttu-id="f3a6e-231">「作業入口網站示範」中的搜尋體驗是根據多面向導覽和篩選條件而設計。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-231">The search experience in the Job Portal Demo is designed around faceted navigation and filters.</span></span> <span data-ttu-id="f3a6e-232">從多面向導覽是放置在頁面上的顯著位置這一點，可以看出其重要性。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-232">The prominent placement of faceted navigation on the page demonstrates its importance.</span></span> 

<span data-ttu-id="f3a6e-233">從範例著手是不錯的開始。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-233">An example is often a good place to begin.</span></span> <span data-ttu-id="f3a6e-234">下列範例取自 `JobsSearch.cs` 檔案，它所建置的要求會根據「職稱」、「位置」、「過賬類型」和「最低工資」建立多面向導覽。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-234">The following example, taken from the `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span></span> 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

<span data-ttu-id="f3a6e-235">面向查詢參數已設定至欄位，且根據資料類型能夠由包含 `count:<integer>`、`sort:<>`、`interval:<integer>` 與 `values:<list>` 的逗號分隔清單進一步參數化。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-235">A facet query parameter is set to a field and depending on the data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span></span> <span data-ttu-id="f3a6e-236">當設定範圍時，針對數值資料支援值清單。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-236">A values list is supported for numeric data when setting up ranges.</span></span> <span data-ttu-id="f3a6e-237">如需用量詳細資訊，請參閱 [搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span></span>

<span data-ttu-id="f3a6e-238">由您的應用程式制訂的要求也應該與面向一起建置篩選條件，以根據選取的面向值縮小候選文件集的範圍。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-238">Along with facets, the request formulated by your application should also build filters to narrow down the set of candidate documents based on a facet value selection.</span></span> <span data-ttu-id="f3a6e-239">就單車店而言，多面向導覽可提供「有哪些顏色、製造商和單車類型可供販售？」等問題的線索。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-239">For a bike store, faceted navigation provides clues to questions like *What colors, manufacturers, and types of bikes are available?*.</span></span> <span data-ttu-id="f3a6e-240">篩選功能可解答「哪些單車確實是位於此價格帶內的紅色登山車？」之類的問題。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span></span> <span data-ttu-id="f3a6e-241">當您按一下 [紅色] 來表示僅顯示紅色的商品，應用程式傳送的下一個查詢會包含 `$filter=Color eq ‘Red’`。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-241">When you click "Red" to indicate that only Red products should be shown, the next query the application sends includes `$filter=Color eq ‘Red’`.</span></span>

<span data-ttu-id="f3a6e-242">下列來自 `JobsSearch.cs` 頁面的程式碼片段會在您選取「職稱」面向的值時，在篩選中新增所選的職稱。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-242">The following code snippet from the `JobsSearch.cs` page adds the selected Business Title to the filter if you select a value from the Business Title facet.</span></span>

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a><span data-ttu-id="f3a6e-243">秘訣和最佳作法</span><span class="sxs-lookup"><span data-stu-id="f3a6e-243">Tips and best practices</span></span>

### <a name="indexing-tips"></a><span data-ttu-id="f3a6e-244">編製索引的秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a6e-244">Indexing tips</span></span>
<span data-ttu-id="f3a6e-245">**在不使用搜尋方塊的情況下改善索引效率**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-245">**Improve index efficiency if you don't use a Search box**</span></span>

<span data-ttu-id="f3a6e-246">如果您的應用程式單獨使用多面向導覽 (也就是沒有搜尋方塊)，您可以將欄位標記為 `searchable=false`、`facetable=true` 以產生更多壓縮索引。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark the field as `searchable=false`, `facetable=true` to produce a more compact index.</span></span> <span data-ttu-id="f3a6e-247">此外，僅會在完整的面向值 (沒有文字分行或多重文字值元件部分的索引) 上編製索引。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of the component parts of a multi-word value.</span></span>

<span data-ttu-id="f3a6e-248">**指定可做為面向的欄位**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-248">**Specify which fields can be used as facets**</span></span>

<span data-ttu-id="f3a6e-249">請記得索引結構描述會定義哪一個欄位可做為面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-249">Recall that the schema of the index determines which fields are available to use as a facet.</span></span> <span data-ttu-id="f3a6e-250">假設欄位可面向化，查詢會指定要執行面向化的欄位。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-250">Assuming a field is facetable, the query specifies which fields to facet by.</span></span> <span data-ttu-id="f3a6e-251">您執行面向化的欄位會提供顯示於標籤下方的值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-251">The field by which you are faceting provides the values that appear below the label.</span></span> 

<span data-ttu-id="f3a6e-252">顯示於各標籤下方的值會從索引擷取。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-252">The values that appear under each label are retrieved from the index.</span></span> <span data-ttu-id="f3a6e-253">例如，如果面向欄位是 [色彩]，其他篩選條件可用的值會是適用於該欄位的值 (紅色、黑色，依此類推)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-253">For example, if the facet field is *Color*, the values available for additional filtering are the values for that field - Red, Black, and so forth.</span></span>

<span data-ttu-id="f3a6e-254">僅針對數值與日期時間值，您可以明確地在面向欄位上設定值 (例如， `facet=Rating,values:1|2|3|4|5`)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-254">For Numeric and DateTime values only, you can explicitly set values on the facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span></span> <span data-ttu-id="f3a6e-255">這些欄位類型允許值清單，以簡化將面向結果分離至連續範圍 (根據數值或時間間隔其中之一的範圍) 的動作。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-255">A values list is allowed for these field types to simplify the separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span></span> 

<span data-ttu-id="f3a6e-256">**依預設您只能擁有一個多面向導覽層級**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-256">**By default you can only have one level of faceted navigation**</span></span> 

<span data-ttu-id="f3a6e-257">如附註所說明，階層中沒有直接支援巢狀面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-257">As noted, there is no direct support for nesting facets in a hierarchy.</span></span> <span data-ttu-id="f3a6e-258">根據預設，Azure 搜尋服務中的多面向導覽僅支援單層篩選。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-258">By default, faceted navigation in Azure Search only supports one level of filters.</span></span> <span data-ttu-id="f3a6e-259">不過有因應措施。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-259">However, workarounds do exist.</span></span> <span data-ttu-id="f3a6e-260">您可以在 `Collection(Edm.String)` 中利用各階層各一個進入點來編碼階層面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span></span> <span data-ttu-id="f3a6e-261">此因應措施的實作不是本文的討論範圍。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-261">Implementing this workaround is beyond the scope of this article.</span></span> 

### <a name="querying-tips"></a><span data-ttu-id="f3a6e-262">查詢秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a6e-262">Querying tips</span></span>
<span data-ttu-id="f3a6e-263">**驗證欄位**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-263">**Validate fields**</span></span>

<span data-ttu-id="f3a6e-264">如果您根據未受信任的使用者輸入動態建置面向清單，請驗證多面向欄位的名稱是否有效。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-264">If you build the list of facets dynamically based on untrusted user input, validate that the names of the faceted fields are valid.</span></span> <span data-ttu-id="f3a6e-265">或者，請在建置 URL 時，使用 .NET 中的 `Uri.EscapeDataString()` 或所選平台的同等功能來逸出這些名稱。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-265">Or, escape the names when building URLs by using either `Uri.EscapeDataString()` in .NET, or the equivalent in your platform of choice.</span></span>

### <a name="filtering-tips"></a><span data-ttu-id="f3a6e-266">篩選秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a6e-266">Filtering tips</span></span>
<span data-ttu-id="f3a6e-267">**使用篩選條件提高搜尋精準度**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-267">**Increase search precision with filters**</span></span>

<span data-ttu-id="f3a6e-268">使用篩選條件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-268">Use filters.</span></span> <span data-ttu-id="f3a6e-269">如果您只仰賴搜尋運算式，詞幹分析可能會造成傳回的文件中的任何欄位都沒有精確面向值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-269">If you rely on just search expressions alone, stemming could cause a document to be returned that doesn’t have the precise facet value in any of its fields.</span></span>

<span data-ttu-id="f3a6e-270">**使用篩選條件提高搜尋效能**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-270">**Increase search performance with filters**</span></span>

<span data-ttu-id="f3a6e-271">篩選條件能縮小候選文件集的範圍，以從排名中搜尋與排除它們。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-271">Filters narrow down the set of candidate documents for search and exclude them from ranking.</span></span> <span data-ttu-id="f3a6e-272">如果您有大型文件集，使用經過挑選的面向向下切入通常能讓您的效能提升。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span></span>
  
<span data-ttu-id="f3a6e-273">**僅篩選多面向欄位**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-273">**Filter only the faceted fields**</span></span>

<span data-ttu-id="f3a6e-274">在多面向向下切入中，您通常希望僅包含在特定欄位中，而非在所有可搜尋欄位的任一處具有面向值的文件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-274">In faceted drill-down, you typically want to only include documents that have the facet value in a specific (faceted) field, not anywhere across all searchable fields.</span></span> <span data-ttu-id="f3a6e-275">新增篩選條件能透過指示服務僅在多面向欄位中搜尋相符值，加強目標欄位。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-275">Adding a filter reinforces the target field by directing the service to search only in the faceted field for a matching value.</span></span>

<span data-ttu-id="f3a6e-276">**使用更多篩選條件修剪面向結果**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-276">**Trim facet results with more filters**</span></span>

<span data-ttu-id="f3a6e-277">面向結果是在符合面向字詞的搜尋結果中找到的文件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-277">Facet results are documents found in the search results that match a facet term.</span></span> <span data-ttu-id="f3a6e-278">在下列範例中，「雲端運算」的搜尋結果中有 254 個項目也具有做為內容類型的「內部規格」。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-278">In the following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span></span> <span data-ttu-id="f3a6e-279">項目毋須互斥。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-279">Items are not necessarily mutually exclusive.</span></span> <span data-ttu-id="f3a6e-280">如果項目同時符合兩個篩選條件的條件，則會個別計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-280">If an item meets the criteria of both filters, it is counted in each one.</span></span> <span data-ttu-id="f3a6e-281">在 `Collection(Edm.String)` 欄位 (通常用來實作文件標記) 上進行面向化時可能發生此重複情形。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used to implement document tagging.</span></span>

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

<span data-ttu-id="f3a6e-282">一般來說，如果您發現面向結果一直過大，建議您新增更多篩選條件，以便讓使用者有更多選項可縮小搜尋範圍。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters to give users more options for narrowing the search.</span></span>

### <a name="tips-about-result-count"></a><span data-ttu-id="f3a6e-283">關於結果計數的秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a6e-283">Tips about result count</span></span>

<span data-ttu-id="f3a6e-284">**限制多面向導覽中的項目數**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-284">**Limit the number of items in the facet navigation**</span></span>

<span data-ttu-id="f3a6e-285">針對瀏覽樹狀目錄中的每個多面向欄位，預設限制為 10 個值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-285">For each faceted field in the navigation tree, there is a default limit of 10 values.</span></span> <span data-ttu-id="f3a6e-286">對於導覽結構來說，此項預設值相當合理，因為它維持值清單在一個可管理的大小。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-286">This default makes sense for navigation structures because it keeps the values list to a manageable size.</span></span> <span data-ttu-id="f3a6e-287">您可以透過指派計數值來覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-287">You can override the default by assigning a value to count.</span></span>

* <span data-ttu-id="f3a6e-288">`&facet=city,count:5` 指定只有最高排序結果中的前 5 個城市會傳回為面向結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-288">`&facet=city,count:5` specifies that only the first five cities found in the top ranked results are returned as a facet result.</span></span> <span data-ttu-id="f3a6e-289">請設想具有搜尋字詞「機場」和 32 個符合項的查詢範例。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-289">Consider a sample query with a search term of “airport” and 32 matches.</span></span> <span data-ttu-id="f3a6e-290">若查詢指定 `&facet=city,count:5`，則只有搜尋結果中包含最多文件的前五個特定城市會包含在面向結果中。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-290">If the query specifies `&facet=city,count:5`, only the first five unique cities with the most documents in the search results are included in the facet results.</span></span>

<span data-ttu-id="f3a6e-291">請注意面向結果與搜尋結果之間的區別。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-291">Notice the distinction between facet results and search results.</span></span> <span data-ttu-id="f3a6e-292">搜尋結果是符合查詢的所有文件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-292">Search results are all the documents that match the query.</span></span> <span data-ttu-id="f3a6e-293">面向結果是各面向值的符合項。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-293">Facet results are the matches for each facet value.</span></span> <span data-ttu-id="f3a6e-294">在此範例中，搜尋結果會包含不在面向分類清單中的「城市」名稱 (範例中為 5 個)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-294">In the example, search results include City names that are not in the facet classification list (5 in our example).</span></span> <span data-ttu-id="f3a6e-295">當您清除面向或選擇「城市」以外的其他面向時，系統會顯示透過多面向導覽篩選出的結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span></span> 

> [!NOTE]
> <span data-ttu-id="f3a6e-296">當有一種類型以上時討論 `count` 可能會讓人混淆。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-296">Discussing `count` when there is more than one type can be confusing.</span></span> <span data-ttu-id="f3a6e-297">下列表格提供了如何於 Azure Search API、範例程式碼與文件中使用字詞的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-297">The following table offers a brief summary of how the term is used in Azure Search API, sample code, and documentation.</span></span> 

* `@colorFacet.count`<br/>
  <span data-ttu-id="f3a6e-298">在簡報程式碼中，您應該會在面向上面看見用來顯示面向結果數目的計數參數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-298">In presentation code, you should see a count parameter on the facet, used to display the number of facet results.</span></span> <span data-ttu-id="f3a6e-299">在面向結果中，計數表示符合面向字詞或範圍的文件數目。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-299">In facet results, count indicates the number of documents that match on the facet term or range.</span></span>
* `&facet=City,count:12`<br/>
  <span data-ttu-id="f3a6e-300">在面向查詢中，您可以設定值的計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-300">In a facet query, you can set count to a value.</span></span>  <span data-ttu-id="f3a6e-301">預設值為 10，但您可以將它設為更高或更低的值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-301">The default is 10, but you can set it higher or lower.</span></span> <span data-ttu-id="f3a6e-302">設定 `count:12` 會取得面向結果中依照文件計數排序的前 12 個相符項。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-302">Setting `count:12` gets the top 12 matches in facet results by document count.</span></span>
* <span data-ttu-id="f3a6e-303">"`@odata.count`"</span><span class="sxs-lookup"><span data-stu-id="f3a6e-303">"`@odata.count`"</span></span><br/>
  <span data-ttu-id="f3a6e-304">在查詢回應中，此值表示搜尋結果中相符項目的數目。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-304">In the query response, this value indicates the number of matching items in the search results.</span></span> <span data-ttu-id="f3a6e-305">平均起來，該值大於所有面向結果結合的加總 (因為符合搜尋字詞的項目存在)，但沒有符合的面向值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-305">On average, it’s larger than the sum of all facet results combined, due to the presence of items that match the search term, but have no facet value matches.</span></span>

<span data-ttu-id="f3a6e-306">**取得面向結果中的計數**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-306">**Get counts in facet results**</span></span>

<span data-ttu-id="f3a6e-307">新增篩選條件至多面向查詢時，您可能希望保留面向陳述式 (例如，`facet=Rating&$filter=Rating ge 4`)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-307">When you add a filter to a faceted query, you might want to retain the facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span></span> <span data-ttu-id="f3a6e-308">以技術層面來看，不需要 facet=Rating，但保留它會傳回分級 4 與更高層級的面向值計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-308">Technically, facet=Rating isn’t needed, but keeping it returns the counts of facet values for ratings 4 and higher.</span></span> <span data-ttu-id="f3a6e-309">例如，如果您按一下 "4" 且查詢包含大於或等於 "4" 的篩選條件，則會針對等於或大於 4 的各分級傳回計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-309">For example, if you click "4" and the query includes a filter for greater or equal to "4", counts are returned for each rating that is 4 and higher.</span></span>  

<span data-ttu-id="f3a6e-310">**確實取得精確的面向計數**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-310">**Make sure you get accurate facet counts**</span></span>

<span data-ttu-id="f3a6e-311">在特定情況下，您可能會發現面向計數不符合結果集 (請參閱 [Azure Search 中的多面向導覽 (論壇文章)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch))。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-311">Under certain circumstances, you might find that facet counts do not match the result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span></span>

<span data-ttu-id="f3a6e-312">面向計數可能會因為分區結構而不正確。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-312">Facet counts can be inaccurate due to the sharding architecture.</span></span> <span data-ttu-id="f3a6e-313">每個搜尋索引都有多個分區，且每個分區都會依照文件計數報告前 N 個面向，然後結合為單一結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-313">Every search index has multiple shards, and each shard reports the top N facets by document count, which is then combined into a single result.</span></span> <span data-ttu-id="f3a6e-314">如果一些分區有許多相符值，而一些有較少相符值，您可能發現結果中有一些面向值遺失或短少。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in the results.</span></span>

<span data-ttu-id="f3a6e-315">雖然此行為可以隨時變更，但如果您今天碰到這個行為，您可以透過人工將計數:<number> 擴張到很大的數目，以加強來自各分區的完整報告來暫時解決問題。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating the count:<number> to a large number to enforce full reporting from each shard.</span></span> <span data-ttu-id="f3a6e-316">如果計數: 的值大於或等於欄位中唯一值的數目，您就能保證結果正確。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-316">If the value of count: is greater than or equal to the number of unique values in the field, you are guaranteed accurate results.</span></span> <span data-ttu-id="f3a6e-317">不過，當文件計數很高的時候，則會有效能的負面影響，因此請謹慎使用此選項。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span></span>

### <a name="user-interface-tips"></a><span data-ttu-id="f3a6e-318">使用者介面秘訣</span><span class="sxs-lookup"><span data-stu-id="f3a6e-318">User interface tips</span></span>
<span data-ttu-id="f3a6e-319">**針對多面向導覽中的各欄位新增標籤**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-319">**Add labels for each field in facet navigation**</span></span>

<span data-ttu-id="f3a6e-320">標籤通常以 HTML 或表單定義 (應用程式範例中為 `index.cshtml`)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-320">Labels are typically defined in the HTML or form (`index.cshtml` in the sample application).</span></span> <span data-ttu-id="f3a6e-321">Azure 搜尋服務中沒有適用於多面向導覽標籤或任何其他中繼資料的 API。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span></span>

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a><span data-ttu-id="f3a6e-322">根據範圍進行篩選</span><span class="sxs-lookup"><span data-stu-id="f3a6e-322">Filter based on a range</span></span>
<span data-ttu-id="f3a6e-323">透過值範圍進行面向化是常見的搜尋應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-323">Faceting over ranges of values is a common search application requirement.</span></span> <span data-ttu-id="f3a6e-324">範圍支援數值資料與日期時間值。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-324">Ranges are supported for numeric data and DateTime values.</span></span> <span data-ttu-id="f3a6e-325">您可以在 [搜尋文件 (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)中閱讀各方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span></span>

<span data-ttu-id="f3a6e-326">Azure Search 透過提供兩種方法進行範圍運算，來簡化範圍建構。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span></span> <span data-ttu-id="f3a6e-327">針對這兩種方法，Azure Search 會依照您提供的輸入建立適當的範圍。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-327">For both approaches, Azure Search creates the appropriate ranges given the inputs you’ve provided.</span></span> <span data-ttu-id="f3a6e-328">例如，如果您指定 10|20|30 的值範圍，它會自動建立 0-10、10-20、20-30 的範圍。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span></span> <span data-ttu-id="f3a6e-329">您的應用程式可以選擇性地移除任何空白間隔。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-329">Your application can optionally remove any intervals that are empty.</span></span> 

<span data-ttu-id="f3a6e-330">**方法 1︰使用間隔參數**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-330">**Approach 1: Use the interval parameter**</span></span>  
<span data-ttu-id="f3a6e-331">若要設定 10 美元增量的價格面向，您會指定︰`&facet=price,interval:10`</span><span class="sxs-lookup"><span data-stu-id="f3a6e-331">To set price facets in $10 increments, you would specify: `&facet=price,interval:10`</span></span>

<span data-ttu-id="f3a6e-332">**方法 2︰使用值清單**</span><span class="sxs-lookup"><span data-stu-id="f3a6e-332">**Approach 2: Use a values list**</span></span>  
<span data-ttu-id="f3a6e-333">針對數值資料，您可以使用值清單。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-333">For numeric data, you can use a values list.</span></span>  <span data-ttu-id="f3a6e-334">請設想 `listPrice` 欄位的面向範圍，其呈現如下：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-334">Consider the facet range for a `listPrice` field, rendered as follows:</span></span>

  ![範例值清單][5]

<span data-ttu-id="f3a6e-336">若要指定如先前的螢幕擷取畫面所示的面向範圍，請使用值清單︰</span><span class="sxs-lookup"><span data-stu-id="f3a6e-336">To specify a facet range like the one in the preceding screen shot, use a values list:</span></span>

    facet=listPrice,values:10|25|100|500|1000|2500

<span data-ttu-id="f3a6e-337">已使用 0 做為起始點，清單中的值做為結束點建置各範圍，並且修剪之前的範圍來建立離散間隔。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-337">Each range is built using 0 as a starting point, a value from the list as an endpoint, and then trimmed of the previous range to create discrete intervals.</span></span> <span data-ttu-id="f3a6e-338">Azure 搜尋服務會將這些動作做為多面向導覽的一部分來執行。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-338">Azure Search does these things as part of faceted navigation.</span></span> <span data-ttu-id="f3a6e-339">您不需要撰寫程式碼來建構各個間隔。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-339">You do not have to write code for structuring each interval.</span></span>

### <a name="build-a-filter-for-a-range"></a><span data-ttu-id="f3a6e-340">針對範圍建置篩選條件</span><span class="sxs-lookup"><span data-stu-id="f3a6e-340">Build a filter for a range</span></span>
<span data-ttu-id="f3a6e-341">若要根據您選取的範圍篩選文件，您可以在定義範圍端點的兩段式運算式中使用 `"ge"` 與 `"lt"` 篩選運算子。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-341">To filter documents based on a range you select, you can use the `"ge"` and `"lt"` filter operators in a two-part expression that defines the endpoints of the range.</span></span> <span data-ttu-id="f3a6e-342">例如，如果您選擇 10-25 作為 `listPrice` 欄位的範圍，篩選條件會是 `$filter=listPrice ge 10 and listPrice lt 25`。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-342">For example, if you choose the range 10-25 for a `listPrice` field, the filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span></span> <span data-ttu-id="f3a6e-343">在程式碼範例中，篩選條件運算式使用 **priceFrom** 與 **priceTo** 參數來設定端點。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-343">In the sample code, the filter expression uses **priceFrom** and **priceTo** parameters to set the endpoints.</span></span> 

  ![查詢某範圍的值][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a><span data-ttu-id="f3a6e-345">根據距離進行篩選</span><span class="sxs-lookup"><span data-stu-id="f3a6e-345">Filter based on distance</span></span>
<span data-ttu-id="f3a6e-346">根據篩選條件與您目前位置的鄰近性，協助您選擇店家、餐廳或目的地等很常見。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-346">It’s common to see filters that help you choose a store, restaurant, or destination based on its proximity to your current location.</span></span> <span data-ttu-id="f3a6e-347">這類型的篩選條件看起來像是多面向導覽，但實際上只是篩選條件。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-347">While this type of filter might look like faceted navigation, it’s just a filter.</span></span> <span data-ttu-id="f3a6e-348">對於那些特別要尋找特定設計問題之實作建議的使用者，我們會在此處說明。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span></span>

<span data-ttu-id="f3a6e-349">搜尋服務中有兩種地理空間函式，**geo.distance** 與 **geo.intersects**。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span></span>

* <span data-ttu-id="f3a6e-350">**geo.distance** 函式會傳回兩點之間的距離 (以公里為單位)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-350">The **geo.distance** function returns the distance in kilometers between two points.</span></span> <span data-ttu-id="f3a6e-351">一個點是欄位，另一個點則是傳遞作為篩選條件一部分的常數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-351">One point is a field and other is a constant passed as part of the filter.</span></span> 
* <span data-ttu-id="f3a6e-352">如果給定的點位於給定的多邊形內，**geo.distance** 函式會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-352">The **geo.intersects** function returns true if a given point is within a given polygon.</span></span> <span data-ttu-id="f3a6e-353">該點為欄位，而多邊形則會指定作為座標的常數清單，並傳遞作為篩選條件的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-353">The point is a field and the polygon is specified as a constant list of coordinates passed as part of the filter.</span></span>

<span data-ttu-id="f3a6e-354">您可以在 [OData 運算式語法 (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx)中找到篩選條件範例。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span></span>

<a name="tryitout"></a>

## <a name="try-the-demo"></a><span data-ttu-id="f3a6e-355">試用示範</span><span class="sxs-lookup"><span data-stu-id="f3a6e-355">Try the demo</span></span>
<span data-ttu-id="f3a6e-356">Azure 搜尋服務作業入口網站示範包含了本文所參考的範例。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-356">The Azure Search Job Portal Demo contains the examples referenced in this article.</span></span>

-   <span data-ttu-id="f3a6e-357">請在 [Azure 搜尋服務作業入口網站示範](http://azjobsdemo.azurewebsites.net/)參閱運作示範並進行線上測試。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-357">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="f3a6e-358">從 [GitHub 上的 Azure 範例儲存機制](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)下載程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-358">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

<span data-ttu-id="f3a6e-359">當您使用搜尋結果的同時，請造訪該 URL 查看查詢建構中的變更。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-359">As you work with search results, watch the URL for changes in query construction.</span></span> <span data-ttu-id="f3a6e-360">當您選取各個結果時，此應用程式會將面向附加到 URI。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-360">This application happens to append facets to the URI as you select each one.</span></span>

1. <span data-ttu-id="f3a6e-361">若要使用示範應用程式的對應功能，請從 [Bing 地圖服務開發人員中心](https://www.bingmapsportal.com/)取得 Bing 地圖服務的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-361">To use the mapping functionality of the demo app, get a Bing Maps key from the [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="f3a6e-362">將它貼在 `index.cshtml` 頁面中的現有金鑰上。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-362">Paste it over the existing key in the `index.cshtml` page.</span></span> <span data-ttu-id="f3a6e-363">系統不會使用 `Web.config` 檔案中的 `BingApiKey` 設定。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-363">The `BingApiKey` setting in the `Web.config` file is not used.</span></span> 

2. <span data-ttu-id="f3a6e-364">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-364">Run the application.</span></span> <span data-ttu-id="f3a6e-365">接受選擇性的導覽，或關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-365">Take the optional tour, or dismiss the dialog box.</span></span>
   
3. <span data-ttu-id="f3a6e-366">輸入搜尋詞彙，例如「分析師」，然後按一下 [搜尋] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-366">Enter a search term, such as "analyst", and click the Search icon.</span></span> <span data-ttu-id="f3a6e-367">查詢會快速執行。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-367">The query executes quickly.</span></span>
   
   <span data-ttu-id="f3a6e-368">多面向導覽結構會隨搜尋結果一併傳回。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-368">A faceted navigation structure is also returned with the search results.</span></span> <span data-ttu-id="f3a6e-369">在搜尋結果頁面中，多面向導覽結構會包含各面向結果計數。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-369">In the search result page, the faceted navigation structure includes counts for each facet result.</span></span> <span data-ttu-id="f3a6e-370">我們並未選取任何面向，因此會傳回所有符合的結果。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-370">No facets are selected, so all matching results are returned.</span></span>
   
   ![選取面向之前的搜尋結果][11]

4. <span data-ttu-id="f3a6e-372">按一下 [職稱]、[位置] 或 [最低工資]。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-372">Click a Business Title, Location, or Minimum Salary.</span></span> <span data-ttu-id="f3a6e-373">初始搜尋時面向會是 Null，但是隨著它們取得值，搜尋結果會修剪不再符合的項目。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-373">Facets were null on the initial search, but as they take on values, the search results are trimmed of items that no longer match.</span></span>
   
   ![選取面向之後的搜尋結果][12]

5. <span data-ttu-id="f3a6e-375">若要清除多面向查詢，以便能夠嘗試不同的查詢行為，請按一下所選面向後面的 `[X]` 以清除面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-375">To clear the faceted query so that you can try different query behaviors, click the `[X]` after the selected facets to clear the facets.</span></span>
   
<a name="nextstep"></a>

## <a name="learn-more"></a><span data-ttu-id="f3a6e-376">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f3a6e-376">Learn more</span></span>
<span data-ttu-id="f3a6e-377">觀賞[深入了解 Azure 搜尋服務](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span></span> <span data-ttu-id="f3a6e-378">在 45:25 時有示範如何實作多面向。</span><span class="sxs-lookup"><span data-stu-id="f3a6e-378">At 45:25, there is a demo on how to implement facets.</span></span>

<span data-ttu-id="f3a6e-379">如需多面向導覽設計原則的深入見解，推薦您下列連結：</span><span class="sxs-lookup"><span data-stu-id="f3a6e-379">For more insights on design principles for faceted navigation, we recommend the following links:</span></span>

* [<span data-ttu-id="f3a6e-380">多面向搜尋的設計</span><span class="sxs-lookup"><span data-stu-id="f3a6e-380">Designing for Faceted Search</span></span>](http://www.uie.com/articles/faceted_search/)
* [<span data-ttu-id="f3a6e-381">設計模式：多面向導覽</span><span class="sxs-lookup"><span data-stu-id="f3a6e-381">Design Patterns: Faceted Navigation</span></span>](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How to build it]: #howtobuildit
[Build the presentation layer]: #presentationlayer
[Build the index]: #buildindex
[Check for data quality]: #checkdata
[Build the query]: #buildquery
[Tips on how to control faceted navigation]: #tips
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

