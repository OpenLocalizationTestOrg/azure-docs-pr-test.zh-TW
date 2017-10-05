---
title: "如何在 Azure 搜尋服務中對搜尋結果分頁 | Microsoft Docs"
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
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="06dd5-103">如何在 Azure 搜尋服務中對搜尋結果分頁</span><span class="sxs-lookup"><span data-stu-id="06dd5-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="06dd5-104">本文提供指引，關於如何使用 Azure 搜尋服務 REST API 來實作搜尋結果頁面的標準項目，例如次數總計、擷取文件、排序次序和導覽。</span><span class="sxs-lookup"><span data-stu-id="06dd5-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="06dd5-105">在以下提到的每個案例中，發表資料或資訊到您的搜尋結果頁面的頁面相關選項，會由傳送到 Azure 搜尋服務的 [搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx) 要求所指定。</span><span class="sxs-lookup"><span data-stu-id="06dd5-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="06dd5-106">要求會包含 GET 命令、路徑和查詢參數，這些會對服務通知要求是什麼，以及如何制訂回應。</span><span class="sxs-lookup"><span data-stu-id="06dd5-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="06dd5-107">有效的要求包含一些項目，例如服務 URL 及路徑、HTTP 動詞命令、`api-version` 等。</span><span class="sxs-lookup"><span data-stu-id="06dd5-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="06dd5-108">為求簡單明瞭，我們縮減此範例，只突顯與分頁相關的語法。</span><span class="sxs-lookup"><span data-stu-id="06dd5-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="06dd5-109">如需要求語法的詳細資訊，請參閱 [Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) 文件。</span><span class="sxs-lookup"><span data-stu-id="06dd5-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="06dd5-110">總點擊數和頁面計數</span><span class="sxs-lookup"><span data-stu-id="06dd5-110">Total hits and Page Counts</span></span>
<span data-ttu-id="06dd5-111">顯示從查詢傳回的結果總數，然後以較小的區塊傳回這些結果，幾乎對所有搜尋頁面都相當基本。</span><span class="sxs-lookup"><span data-stu-id="06dd5-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="06dd5-112">在 Azure 搜尋服務中，您可以使用 `$count`、`$top` 和 `$skip` 參數來傳回這些值。</span><span class="sxs-lookup"><span data-stu-id="06dd5-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="06dd5-113">下列範例示範總點擊數做為 `@OData.count`傳回的範例要求：</span><span class="sxs-lookup"><span data-stu-id="06dd5-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="06dd5-114">開始在第一頁擷取文件，以 15 個為一組，同時顯示總點擊數：</span><span class="sxs-lookup"><span data-stu-id="06dd5-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="06dd5-115">分頁結果需要 `$top` 和 `$skip`，其中 `$top` 指定有多少項目要批次傳回，而 `$skip` 指定有多少項目要略過。</span><span class="sxs-lookup"><span data-stu-id="06dd5-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="06dd5-116">在下列範例中，每個頁面顯示下 15 個項目，表示在 `$skip` 參數中的遞增跳躍。</span><span class="sxs-lookup"><span data-stu-id="06dd5-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="06dd5-117">版面配置</span><span class="sxs-lookup"><span data-stu-id="06dd5-117">Layout</span></span>
<span data-ttu-id="06dd5-118">在搜尋結果頁面中，您可能會想要顯示縮圖、欄位子集以及完整產品頁面的連結。</span><span class="sxs-lookup"><span data-stu-id="06dd5-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="06dd5-119">在 Azure 搜尋服務中，您可使用 `$select` 和查閱命令來實作這種體驗。</span><span class="sxs-lookup"><span data-stu-id="06dd5-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="06dd5-120">若要傳回並排版面配置的欄位子集：</span><span class="sxs-lookup"><span data-stu-id="06dd5-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="06dd5-121">不能直接搜尋影像和媒體檔案，且應儲存在其他儲存體平台，例如 Azure Blob 儲存體，以降低成本。</span><span class="sxs-lookup"><span data-stu-id="06dd5-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="06dd5-122">在索引和文件中，請定義儲存外部內容 URL 位址的欄位。</span><span class="sxs-lookup"><span data-stu-id="06dd5-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="06dd5-123">然後您可以使用此欄位做為影像參考。</span><span class="sxs-lookup"><span data-stu-id="06dd5-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="06dd5-124">此影像的 URL 應位於此文件中。</span><span class="sxs-lookup"><span data-stu-id="06dd5-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="06dd5-125">若要擷取 **onClick** 事件的產品描述頁面，請使用 [查閱文件](http://msdn.microsoft.com/library/azure/dn798929.aspx) 來傳入此文件的金鑰以進行擷取。</span><span class="sxs-lookup"><span data-stu-id="06dd5-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="06dd5-126">此金鑰的資料類型為 `Edm.String`。</span><span class="sxs-lookup"><span data-stu-id="06dd5-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="06dd5-127">在此範例中為 *246810*。</span><span class="sxs-lookup"><span data-stu-id="06dd5-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="06dd5-128">根據相關性、評等或價格排序</span><span class="sxs-lookup"><span data-stu-id="06dd5-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="06dd5-129">排序次序通常預設為相關性，但也常見到立即可用的替代排序次序，好讓客戶可迅速重新將現有的結果排列為不同的排名次序。</span><span class="sxs-lookup"><span data-stu-id="06dd5-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="06dd5-130">在 Azure 搜尋服務中，對於所有索引編製為 `"Sortable": true.` 的欄位，會根據 `$orderby` 運算式來排序。</span><span class="sxs-lookup"><span data-stu-id="06dd5-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="06dd5-131">相關性和評分設定檔密切相關。</span><span class="sxs-lookup"><span data-stu-id="06dd5-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="06dd5-132">您可使用預設評分，這會依賴文字分析和統計資料來對所有結果排名次序，與搜尋詞彙有更多或更密切符合的文件會有更高的評分。</span><span class="sxs-lookup"><span data-stu-id="06dd5-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="06dd5-133">替代的排序次序通常和 **onClick** 事件有關，這會回呼建置此排序次序的方法。</span><span class="sxs-lookup"><span data-stu-id="06dd5-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="06dd5-134">例如指定頁面項目如下：</span><span class="sxs-lookup"><span data-stu-id="06dd5-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="06dd5-135">您可建立一個方法，它會接受所選取的排序選項做為輸入，然後對於和該選項相關的準則傳回已排序的清單。</span><span class="sxs-lookup"><span data-stu-id="06dd5-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="06dd5-136">雖然預設評分對大多數案例都已足夠，但我們建議改用自訂評分設定檔來建立相關性。</span><span class="sxs-lookup"><span data-stu-id="06dd5-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="06dd5-137">自訂評分設定檔給您提升項目的方式，這會對您的企業更有助益。</span><span class="sxs-lookup"><span data-stu-id="06dd5-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="06dd5-138">如需詳細資訊，請參閱 [新增評分設定檔](http://msdn.microsoft.com/library/azure/dn798928.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="06dd5-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="06dd5-139">多面向導覽</span><span class="sxs-lookup"><span data-stu-id="06dd5-139">Faceted navigation</span></span>
<span data-ttu-id="06dd5-140">搜尋導覽常見於結果頁面上，通常位於頁面的一側或頂端。</span><span class="sxs-lookup"><span data-stu-id="06dd5-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="06dd5-141">在 Azure 搜尋服務中，多面向導覽會根據預先定義的篩選器提供自我導向的搜尋。</span><span class="sxs-lookup"><span data-stu-id="06dd5-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="06dd5-142">如需詳細資訊，請參閱 [Azure 搜尋服務中的多面向導覽](search-faceted-navigation.md) 。</span><span class="sxs-lookup"><span data-stu-id="06dd5-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="06dd5-143">頁面層級的篩選器</span><span class="sxs-lookup"><span data-stu-id="06dd5-143">Filters at the page level</span></span>
<span data-ttu-id="06dd5-144">如果解決方案設計包含特定類型之內容的專用搜尋頁面 (例如，線上零售應用程式具有列於頁面頂端的部門)，則您可一起插入篩選運算式和 **onClick** 事件，在預先篩選的狀態下開啟頁面。</span><span class="sxs-lookup"><span data-stu-id="06dd5-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="06dd5-145">您可以傳送篩選器，但不一定要有搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="06dd5-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="06dd5-146">例如，下列要求會篩選品牌名稱，只傳回符合該名稱的文件。</span><span class="sxs-lookup"><span data-stu-id="06dd5-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="06dd5-147">如需 `$filter` 運算式的詳細資訊，請參閱[搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06dd5-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="06dd5-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="06dd5-148">See Also</span></span>
* [<span data-ttu-id="06dd5-149">Azure 搜尋服務 REST API</span><span class="sxs-lookup"><span data-stu-id="06dd5-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="06dd5-150">索引作業</span><span class="sxs-lookup"><span data-stu-id="06dd5-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="06dd5-151">文件作業</span><span class="sxs-lookup"><span data-stu-id="06dd5-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="06dd5-152">Azure 搜尋服務的影片和教學課程</span><span class="sxs-lookup"><span data-stu-id="06dd5-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="06dd5-153">Azure 搜尋服務中的多面向導覽</span><span class="sxs-lookup"><span data-stu-id="06dd5-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
