---
title: "在 Azure 搜尋的 aaaHow toopage 搜尋結果 |Microsoft 文件"
description: "Azure 搜尋服務 (Microsoft Azure 上之託管的雲端搜尋服務) 中的分頁方式。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="a31ec-103">在 Azure 搜尋 toopage 搜尋結果的方式</span><span class="sxs-lookup"><span data-stu-id="a31ec-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="a31ec-104">這篇文章會提供有關如何 toouse hello Azure 搜尋服務 REST API tooimplement 標準的項目搜尋結果頁面上，例如的總次數、 文件擷取、 排序次序和瀏覽的指引。</span><span class="sxs-lookup"><span data-stu-id="a31ec-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="a31ec-105">在每個案例中，如下所述，提供資料或資訊 tooyour 搜尋結果頁面的頁面的相關選項透過 hello 指定[搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx)傳送要求 tooyour Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="a31ec-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="a31ec-106">要求包含 GET 命令、 路徑和 hello 服務要求功能，就會通知的查詢參數和 tooformulate hello 回應的方式。</span><span class="sxs-lookup"><span data-stu-id="a31ec-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="a31ec-107">有效的要求包含一些項目，例如服務 URL 及路徑、HTTP 動詞命令、`api-version` 等。</span><span class="sxs-lookup"><span data-stu-id="a31ec-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="a31ec-108">為求簡單明瞭，我們會修剪 hello 範例 toohighlight 只 hello 語法相關 toopagination。</span><span class="sxs-lookup"><span data-stu-id="a31ec-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="a31ec-109">請參閱 hello [Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)要求語法的詳細文件。</span><span class="sxs-lookup"><span data-stu-id="a31ec-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="a31ec-110">總點擊數和頁面計數</span><span class="sxs-lookup"><span data-stu-id="a31ec-110">Total hits and Page Counts</span></span>
<span data-ttu-id="a31ec-111">顯示 hello 總查詢，傳回的結果數目，然後傳回結果較小的區塊，是基本 toovirtually 所有搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="a31ec-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="a31ec-112">在 Azure 搜尋中，您可以使用 hello `$count`， `$top`，和`$skip`參數 tooreturn 這些值。</span><span class="sxs-lookup"><span data-stu-id="a31ec-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="a31ec-113">hello 下列範例顯示的範例要求的總叫用，以傳回`@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="a31ec-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="a31ec-114">擷取 15，群組中的文件，也會顯示 hello 的點擊總數，開始 hello 第一頁：</span><span class="sxs-lookup"><span data-stu-id="a31ec-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="a31ec-115">分頁結果同時需要`$top`和`$skip`，其中`$top`批次中指定數目的項目 tooreturn 和`$skip`指定數目的項目 tooskip。</span><span class="sxs-lookup"><span data-stu-id="a31ec-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="a31ec-116">在 hello 遵循範例中，每一頁會顯示 hello 接下來 15 的項目，以表示 hello 累加式跳躍點在 hello`$skip`參數。</span><span class="sxs-lookup"><span data-stu-id="a31ec-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="a31ec-117">版面配置</span><span class="sxs-lookup"><span data-stu-id="a31ec-117">Layout</span></span>
<span data-ttu-id="a31ec-118">在搜尋結果 頁面中，您可能想 tooshow 縮圖影像、 欄位、 的子集，以及連結 tooa 完整產品頁面。</span><span class="sxs-lookup"><span data-stu-id="a31ec-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="a31ec-119">在 Azure 搜尋中，您會使用`$select`和查閱命令 tooimplement 這項體驗。</span><span class="sxs-lookup"><span data-stu-id="a31ec-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="a31ec-120">tooreturn 子集並排顯示版面配置的欄位：</span><span class="sxs-lookup"><span data-stu-id="a31ec-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="a31ec-121">映像和媒體檔案不是直接搜尋，並應該儲存在另一個存放裝置平台，例如 Azure Blob 儲存體，tooreduce 成本。</span><span class="sxs-lookup"><span data-stu-id="a31ec-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="a31ec-122">在 hello 索引和文件中，定義會儲存 hello hello 外部內容的 URL 地址的欄位。</span><span class="sxs-lookup"><span data-stu-id="a31ec-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="a31ec-123">您接著可以使用 hello 欄位做為映像的參照。</span><span class="sxs-lookup"><span data-stu-id="a31ec-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="a31ec-124">hello URL toohello 映像應該 hello 文件中。</span><span class="sxs-lookup"><span data-stu-id="a31ec-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="a31ec-125">產品說明頁面的 tooretrieve **onClick**事件時，使用[查閱文件](http://msdn.microsoft.com/library/azure/dn798929.aspx)toopass hello 文件 tooretrieve hello 索引鍵中的。</span><span class="sxs-lookup"><span data-stu-id="a31ec-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="a31ec-126">hello hello 索引鍵資料類型是`Edm.String`。</span><span class="sxs-lookup"><span data-stu-id="a31ec-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="a31ec-127">在此範例中為 *246810*。</span><span class="sxs-lookup"><span data-stu-id="a31ec-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="a31ec-128">根據相關性、評等或價格排序</span><span class="sxs-lookup"><span data-stu-id="a31ec-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="a31ec-129">排序通常順序預設 toorelevance，但它是一般 toomake 替代排序次序便於使用，讓客戶可以快速地為不同的次序順序 reshuffle 現有的結果。</span><span class="sxs-lookup"><span data-stu-id="a31ec-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="a31ec-130">在 Azure 搜尋中，會根據排序 hello`$orderby`運算式，會與編製索引的所有欄位`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="a31ec-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="a31ec-131">相關性和評分設定檔密切相關。</span><span class="sxs-lookup"><span data-stu-id="a31ec-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="a31ec-132">您可以使用預設計分 hello，它會依賴文字分析和統計資料 toorank 順序所有結果，使用較高 toodocuments 的更多或更強的相符項目進行的搜尋詞彙的分數。</span><span class="sxs-lookup"><span data-stu-id="a31ec-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="a31ec-133">替代的排序順序通常與相關聯**onClick**回 tooa 方法會呼叫的事件建立 hello 排序順序。</span><span class="sxs-lookup"><span data-stu-id="a31ec-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="a31ec-134">例如指定頁面項目如下：</span><span class="sxs-lookup"><span data-stu-id="a31ec-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="a31ec-135">您會建立接受 hello 選取排序選項做為輸入，並傳回該選項相關聯的 hello 準則的已排序的清單的方法。</span><span class="sxs-lookup"><span data-stu-id="a31ec-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="a31ec-136">雖然 hello 預設計分足以適用許多情況，我們建議您改為基礎的自訂計分設定檔的相關性。</span><span class="sxs-lookup"><span data-stu-id="a31ec-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="a31ec-137">自訂的計分設定檔可讓您更有幫助 tooyour 商務方式 tooboost 項目。</span><span class="sxs-lookup"><span data-stu-id="a31ec-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="a31ec-138">如需詳細資訊，請參閱 [新增評分設定檔](http://msdn.microsoft.com/library/azure/dn798928.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="a31ec-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="a31ec-139">多面向導覽</span><span class="sxs-lookup"><span data-stu-id="a31ec-139">Faceted navigation</span></span>
<span data-ttu-id="a31ec-140">在 [結果] 頁面中，通常位於 hello 側邊或上方頁面上搜尋巡覽常會。</span><span class="sxs-lookup"><span data-stu-id="a31ec-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="a31ec-141">在 Azure 搜尋服務中，多面向導覽會根據預先定義的篩選器提供自我導向的搜尋。</span><span class="sxs-lookup"><span data-stu-id="a31ec-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="a31ec-142">如需詳細資訊，請參閱 [Azure 搜尋服務中的多面向導覽](search-faceted-navigation.md) 。</span><span class="sxs-lookup"><span data-stu-id="a31ec-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="a31ec-143">Hello 頁面層級篩選</span><span class="sxs-lookup"><span data-stu-id="a31ec-143">Filters at hello page level</span></span>
<span data-ttu-id="a31ec-144">如果您解決方案設計包含特定類型的內容 （例如，線上零售應用程式已列在 hello hello 頁面頂端的部門） 的專用的搜尋頁面中，您可以插入旁邊的篩選條件運算式**onClick**事件 tooopen 預先狀態中的頁面。</span><span class="sxs-lookup"><span data-stu-id="a31ec-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="a31ec-145">您可以傳送篩選器，但不一定要有搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="a31ec-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="a31ec-146">例如，hello 下列要求會篩選品牌名稱，傳回符合這些文件。</span><span class="sxs-lookup"><span data-stu-id="a31ec-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="a31ec-147">如需 `$filter` 運算式的詳細資訊，請參閱[搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a31ec-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="a31ec-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a31ec-148">See Also</span></span>
* [<span data-ttu-id="a31ec-149">Azure 搜尋服務 REST API</span><span class="sxs-lookup"><span data-stu-id="a31ec-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="a31ec-150">索引作業</span><span class="sxs-lookup"><span data-stu-id="a31ec-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="a31ec-151">文件作業</span><span class="sxs-lookup"><span data-stu-id="a31ec-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="a31ec-152">Azure 搜尋服務的影片和教學課程</span><span class="sxs-lookup"><span data-stu-id="a31ec-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="a31ec-153">Azure 搜尋服務中的多面向導覽</span><span class="sxs-lookup"><span data-stu-id="a31ec-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
