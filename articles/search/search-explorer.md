---
title: "aaa\"查詢索引 （入口網站的 Azure 搜尋） |Microsoft 文件 」"
description: "發出 hello Azure 入口網站的搜尋總管 中搜尋查詢。"
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
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="da3b4-103">查詢 Azure 搜尋索引使用 hello Azure 入口網站中的搜尋總管</span><span class="sxs-lookup"><span data-stu-id="da3b4-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da3b4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="da3b4-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="da3b4-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="da3b4-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="da3b4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="da3b4-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="da3b4-107">REST</span><span class="sxs-lookup"><span data-stu-id="da3b4-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="da3b4-108">本文將告訴您如何 tooquery Azure 搜尋索引使用**搜尋總管**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="da3b4-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="da3b4-109">在您的服務，您可以使用搜尋總管 toosubmit 簡單或完整 Lucene 查詢字串 tooany 現有的索引。</span><span class="sxs-lookup"><span data-stu-id="da3b4-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="da3b4-110">開啟 hello 服務儀表板</span><span class="sxs-lookup"><span data-stu-id="da3b4-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="da3b4-111">按一下**所有資源**hello 跳躍列上的 hello 左方的 hello [Azure 入口網站](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)。</span><span class="sxs-lookup"><span data-stu-id="da3b4-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="da3b4-112">選取您的 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="da3b4-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="da3b4-113">選取索引</span><span class="sxs-lookup"><span data-stu-id="da3b4-113">Select an index</span></span>

<span data-ttu-id="da3b4-114">您想要從 hello toosearch 選取 hello 索引**索引**磚。</span><span class="sxs-lookup"><span data-stu-id="da3b4-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="da3b4-115">開啟搜尋總管</span><span class="sxs-lookup"><span data-stu-id="da3b4-115">Open Search Explorer</span></span>

<span data-ttu-id="da3b4-116">按一下 hello 搜尋總管磚 tooslide 開啟 hello 搜尋列上的和 [結果] 窗格。</span><span class="sxs-lookup"><span data-stu-id="da3b4-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="da3b4-117">開始搜尋</span><span class="sxs-lookup"><span data-stu-id="da3b4-117">Start searching</span></span>

<span data-ttu-id="da3b4-118">當使用 hello 搜尋總管，您可以指定[查詢參數](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)tooformulate hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="da3b4-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="da3b4-119">在 [查詢字串] 中輸入查詢，然後按 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="da3b4-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="da3b4-120">hello 查詢字串會自動剖析成 hello 適當要求 URL toosubmit hello Azure 搜尋 REST API 針對 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="da3b4-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="da3b4-121">您可以使用任何有效簡單或完整 Lucene 查詢語法 toocreate hello 的要求。</span><span class="sxs-lookup"><span data-stu-id="da3b4-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="da3b4-122">hello`*`字元是不依特定順序傳回所有文件的對等 tooan 空白或未指定搜尋。</span><span class="sxs-lookup"><span data-stu-id="da3b4-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="da3b4-123">在**結果**，查詢結果會出現在未經處理的 JSON，以傳回相同 toohello 裝載時以程式設計方式發出要求的 HTTP 回應主體。</span><span class="sxs-lookup"><span data-stu-id="da3b4-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="da3b4-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da3b4-124">Next steps</span></span>

<span data-ttu-id="da3b4-125">hello 下列資源提供其他的查詢語法資訊和範例。</span><span class="sxs-lookup"><span data-stu-id="da3b4-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="da3b4-126">簡單查詢語法</span><span class="sxs-lookup"><span data-stu-id="da3b4-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="da3b4-127">Lucene 查詢語法</span><span class="sxs-lookup"><span data-stu-id="da3b4-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="da3b4-128">Lucene 查詢語法範例</span><span class="sxs-lookup"><span data-stu-id="da3b4-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="da3b4-129">OData 篩選條件運算式語法</span><span class="sxs-lookup"><span data-stu-id="da3b4-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 