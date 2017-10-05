---
title: "查詢索引 (入口網站 - Azure 搜尋服務) | Microsoft Docs"
description: "在 Azure 入口網站的搜尋總管中發出搜尋查詢。"
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a><span data-ttu-id="9c21e-103">在 Azure 入口網站中使用搜尋總管查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="9c21e-103">Query an Azure Search index using Search Explorer in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c21e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9c21e-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9c21e-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="9c21e-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9c21e-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9c21e-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9c21e-107">REST</span><span class="sxs-lookup"><span data-stu-id="9c21e-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="9c21e-108">本文說明如何在 Azure 入口網站中使用**搜尋總管**查詢 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="9c21e-108">This article shows you how to query an Azure Search index using **Search Explorer** in the Azure portal.</span></span> <span data-ttu-id="9c21e-109">您可以使用搜尋總管，在您的服務中對於任何現有的索引送出簡單或完整的 Lucene 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="9c21e-109">You can use Search Explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="9c21e-110">開啟服務儀表板</span><span class="sxs-lookup"><span data-stu-id="9c21e-110">Open the service dashboard</span></span>
1. <span data-ttu-id="9c21e-111">按一下 [Azure 入口網站](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)左側導向列中的 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="9c21e-111">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="9c21e-112">選取您的 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="9c21e-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="9c21e-113">選取索引</span><span class="sxs-lookup"><span data-stu-id="9c21e-113">Select an index</span></span>

<span data-ttu-id="9c21e-114">選取您想要從 [索引] 圖格搜尋的索引。</span><span class="sxs-lookup"><span data-stu-id="9c21e-114">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="9c21e-115">開啟搜尋總管</span><span class="sxs-lookup"><span data-stu-id="9c21e-115">Open Search Explorer</span></span>

<span data-ttu-id="9c21e-116">按一下 [搜尋總管] 圖格以滑動開啟搜尋列和結果窗格。</span><span class="sxs-lookup"><span data-stu-id="9c21e-116">Click on the Search Explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="9c21e-117">開始搜尋</span><span class="sxs-lookup"><span data-stu-id="9c21e-117">Start searching</span></span>

<span data-ttu-id="9c21e-118">使用 [搜尋總管] 時可以指定任何 [查詢參數](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)以編寫查詢。</span><span class="sxs-lookup"><span data-stu-id="9c21e-118">When using the Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="9c21e-119">在 [查詢字串] 中輸入查詢，然後按 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="9c21e-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="9c21e-120">查詢字串會自動剖析為適當的要求 URL，以便對 Azure 搜尋服務 REST API 提交 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="9c21e-120">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="9c21e-121">您可以使用任何有效的簡單或完整 Lucene 查詢語法來建立要求。</span><span class="sxs-lookup"><span data-stu-id="9c21e-121">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="9c21e-122">`*` 字元就相當於不依特定順序傳回所有文件的空白或未指定搜尋。</span><span class="sxs-lookup"><span data-stu-id="9c21e-122">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="9c21e-123">在 [結果] 中，查詢結果會以未經處理的 JSON 呈現，與在以程式設計方式發出要求時，傳回 HTTP 回應主體的承載相同。</span><span class="sxs-lookup"><span data-stu-id="9c21e-123">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="9c21e-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c21e-124">Next steps</span></span>

<span data-ttu-id="9c21e-125">下列資源提供其他的查詢語法資訊和範例。</span><span class="sxs-lookup"><span data-stu-id="9c21e-125">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="9c21e-126">簡單查詢語法</span><span class="sxs-lookup"><span data-stu-id="9c21e-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="9c21e-127">Lucene 查詢語法</span><span class="sxs-lookup"><span data-stu-id="9c21e-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="9c21e-128">Lucene 查詢語法範例</span><span class="sxs-lookup"><span data-stu-id="9c21e-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="9c21e-129">OData 篩選條件運算式語法</span><span class="sxs-lookup"><span data-stu-id="9c21e-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 