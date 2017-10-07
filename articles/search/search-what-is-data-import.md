---
title: "在 Azure 搜尋 aaaData 上載 |Microsoft 文件"
description: "了解 tooupload 資料 tooan Azure 搜尋中的索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a><span data-ttu-id="eaef5-103">上傳資料 tooAzure 搜尋</span><span class="sxs-lookup"><span data-stu-id="eaef5-103">Upload data tooAzure Search</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eaef5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="eaef5-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="eaef5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="eaef5-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="eaef5-106">REST</span><span class="sxs-lookup"><span data-stu-id="eaef5-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="eaef5-107">有兩種方式 toopopulate 具有您資料的索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-107">There are two ways toopopulate an index with your data.</span></span> <span data-ttu-id="eaef5-108">hello 第一個選項以手動方式將資料推送至 hello 索引使用 hello Azure 搜尋[REST API](search-import-data-rest-api.md)或[.NET SDK](search-import-data-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="eaef5-108">hello first option is manually pushing your data into hello index using hello Azure Search [REST API](search-import-data-rest-api.md) or [.NET SDK](search-import-data-dotnet.md).</span></span> <span data-ttu-id="eaef5-109">hello 第二個選項太[點支援的資料來源](search-indexer-overview.md)tooyour 編製索引，並讓 Azure 搜尋會自動納入 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="eaef5-109">hello second option is too[point a supported data source](search-indexer-overview.md) tooyour index and let Azure Search automatically pull in hello data.</span></span>

## <a name="push-data-tooan-index"></a><span data-ttu-id="eaef5-110">推播資料 tooan 索引</span><span class="sxs-lookup"><span data-stu-id="eaef5-110">Push data tooan index</span></span>
<span data-ttu-id="eaef5-111">這種方法是指傳送您資料 tooAzure 搜尋 toomake tooprogrammatically 可供搜尋它。</span><span class="sxs-lookup"><span data-stu-id="eaef5-111">This approach refers tooprogrammatically sending your data tooAzure Search toomake it available for searching.</span></span> <span data-ttu-id="eaef5-112">對於具有非常低的延遲需求 （例如，如果您需要搜尋與動態清查資料庫同步作業 toobe） 應用程式，hello 發送模型是您唯一的選項。</span><span class="sxs-lookup"><span data-stu-id="eaef5-112">For applications having very low latency requirements (for example, if you need search operations toobe in sync with dynamic inventory databases), hello push model is your only option.</span></span>

<span data-ttu-id="eaef5-113">您可以使用 hello [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)或[.NET SDK](search-import-data-dotnet.md) toopush 資料 tooan 索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-113">You can use hello [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) or [.NET SDK](search-import-data-dotnet.md) toopush data tooan index.</span></span> <span data-ttu-id="eaef5-114">正在透過 hello 入口網站將資料推送沒有工具支援。</span><span class="sxs-lookup"><span data-stu-id="eaef5-114">There is currently no tool support for pushing data via hello portal.</span></span>

<span data-ttu-id="eaef5-115">這種方法是比 hello 提取模型更有彈性，因為個別或批次中，您可以上傳文件 （too1000 每個批次或 16 MB，總何種限制者為優先）。</span><span class="sxs-lookup"><span data-stu-id="eaef5-115">This approach is more flexible than hello pull model because you can upload documents individually or in batches (up too1000 per batch or 16 MB, whichever limit comes first).</span></span> <span data-ttu-id="eaef5-116">hello 發送模型也可讓您 tooupload 文件 tooAzure 搜尋無論資料的位置。</span><span class="sxs-lookup"><span data-stu-id="eaef5-116">hello push model also allows you tooupload documents tooAzure Search regardless of where your data is.</span></span>

<span data-ttu-id="eaef5-117">了解 Azure 搜尋的 hello 資料格式是 JSON，且 hello 資料集中的所有文件必須具有對應 toofields 索引結構描述中定義的欄位。</span><span class="sxs-lookup"><span data-stu-id="eaef5-117">hello data format understood by Azure Search is JSON, and all documents in hello dataset must have fields that map toofields defined in your index schema.</span></span> 

## <a name="pull-data-into-an-index"></a><span data-ttu-id="eaef5-118">將資料提取到索引</span><span class="sxs-lookup"><span data-stu-id="eaef5-118">Pull data into an index</span></span>
<span data-ttu-id="eaef5-119">hello 提取模型搜耙支援的資料來源，並自動 hello 資料上傳至您的索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-119">hello pull model crawls a supported data source and automatically uploads hello data into your index.</span></span> <span data-ttu-id="eaef5-120">在 Azure 搜尋服務中，這項功能是透過索引子來實作，其目前可供 [Blob 儲存體](search-howto-indexing-azure-blob-storage.md)、[表格儲存體](search-howto-indexing-azure-tables.md)、[Azure Cosmos DB](http://aka.ms/documentdb-search-indexer)、[Azure SQL Database 和 Azure VM 上的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) 使用。</span><span class="sxs-lookup"><span data-stu-id="eaef5-120">In Azure Search, this capability is implemented through *indexers*, currently available for [Blob storage](search-howto-indexing-azure-blob-storage.md), [Table storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure SQL database, and SQL Server on Azure VMs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md).</span></span> 

<span data-ttu-id="eaef5-121">索引子連接索引 tooa 資料來源 （通常是資料表、 檢視或對等的結構），並將對應 hello 索引中的來源欄位 tooequivalent 欄位。</span><span class="sxs-lookup"><span data-stu-id="eaef5-121">Indexers connect an index tooa data source (usually a table, view, or equivalent structure), and map source fields tooequivalent fields in hello index.</span></span> <span data-ttu-id="eaef5-122">在執行期間，hello 資料列集是自動轉換的 tooJSON 並載入 hello 指定的索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-122">During execution, hello rowset is automatically transformed tooJSON and loaded into hello specified index.</span></span> <span data-ttu-id="eaef5-123">所有的索引器支援排程，好讓您可以指定 hello 資料是 toobe 重新整理的頻率。</span><span class="sxs-lookup"><span data-stu-id="eaef5-123">All indexers support scheduling so that you can specify how frequently hello data is toobe refreshed.</span></span> <span data-ttu-id="eaef5-124">大部分的索引子會提供變更追蹤如果 hello 資料來源支援它。</span><span class="sxs-lookup"><span data-stu-id="eaef5-124">Most indexers provide change tracking if hello data source supports it.</span></span> <span data-ttu-id="eaef5-125">所追蹤變更和刪除 tooexisting 文件除了 toorecognizing 新文件、 索引子移除 hello 需求 tooactively 管理您的索引中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="eaef5-125">By tracking changes and deletes tooexisting documents in addition toorecognizing new documents, indexers remove hello need tooactively manage hello data in your index.</span></span> 

<span data-ttu-id="eaef5-126">索引子功能會公開在 hello [Azure 入口網站](search-import-data-portal.md)，hello [REST API](/rest/api/searchservice/Indexer-operations)，和 hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations)。</span><span class="sxs-lookup"><span data-stu-id="eaef5-126">Indexer functionality is exposed in hello [Azure portal](search-import-data-portal.md), hello [REST API](/rest/api/searchservice/Indexer-operations), and hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations).</span></span> 

<span data-ttu-id="eaef5-127">利用 toousing hello 入口網站是，Azure 搜尋可以通常會產生預設的索引結構描述為您藉由讀取 hello hello 來源資料集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="eaef5-127">An advantage toousing hello portal is that Azure Search can usually generate a default index schema for you by reading hello metadata of hello source dataset.</span></span> <span data-ttu-id="eaef5-128">處理 hello 索引之後的 hello, 允許則不需要重新索引只有結構描述編輯之前，您可以修改 hello 產生的索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-128">You can modify hello generated index until hello index is processed, after which hello only schema edits allowed are those that do not require reindexing.</span></span> <span data-ttu-id="eaef5-129">如果您想要 toomake 影響的 hello 變更直接 hello 結構描述，您需要 toorebuild hello 索引。</span><span class="sxs-lookup"><span data-stu-id="eaef5-129">If hello changes you want toomake impact hello schema directly, you would need toorebuild hello index.</span></span> 

<span data-ttu-id="eaef5-130">填入 hello 索引之後，您可以使用**搜尋總管**當作驗證步驟的 hello 入口網站的命令列中。</span><span class="sxs-lookup"><span data-stu-id="eaef5-130">After hello index is populated, you can use **Search Explorer** in hello portal command bar as a verification step.</span></span>

## <a name="query-an-index-using-search-explorer"></a><span data-ttu-id="eaef5-131">使用搜尋總管查詢索引</span><span class="sxs-lookup"><span data-stu-id="eaef5-131">Query an index using Search Explorer</span></span>

<span data-ttu-id="eaef5-132">快速 tooperform hello 文件上傳的初步檢查是 toouse**搜尋總管**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="eaef5-132">A quick way tooperform a preliminary check on hello document upload is toouse **Search Explorer** in hello portal.</span></span> <span data-ttu-id="eaef5-133">hello 總管可讓您查詢的索引，而不需要 toowrite 任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="eaef5-133">hello explorer lets you query an index without having toowrite any code.</span></span> <span data-ttu-id="eaef5-134">hello 搜尋經驗為基礎預設設定，例如 hello[簡單的語法](/rest/api/searchservice/simple-query-syntax-in-azure-search)和預設[受 searchMode 查詢參數](/rest/api/searchservice/search-documents)。</span><span class="sxs-lookup"><span data-stu-id="eaef5-134">hello search experience is based on default settings, such as hello [simple syntax](/rest/api/searchservice/simple-query-syntax-in-azure-search) and default [searchMode query parameter](/rest/api/searchservice/search-documents).</span></span> <span data-ttu-id="eaef5-135">在 JSON 中會傳回結果，以便您可以檢查 hello 整份文件。</span><span class="sxs-lookup"><span data-stu-id="eaef5-135">Results are returned in JSON so that you can inspect hello entire document.</span></span>

> [!TIP]
> <span data-ttu-id="eaef5-136">許多[Azure 搜尋程式碼範例](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search)包含內嵌或隨時可用資料集，提供簡單的方式 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="eaef5-136">Numerous [Azure Search code samples](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) include embedded or readily available datasets, offering an easy way tooget started.</span></span> <span data-ttu-id="eaef5-137">hello 入口網站也提供範例索引子和小型不動產資料集 （名為 「 realestate-我們的範例 」） 所組成的資料來源。</span><span class="sxs-lookup"><span data-stu-id="eaef5-137">hello portal also provides a sample indexer and data source consisting of a small real estate dataset (named "realestate-us-sample").</span></span> <span data-ttu-id="eaef5-138">當您執行 hello 預先設定的索引子上 hello 範例資料來源時，索引建立，並使用文件，然後在 搜尋總管或由您撰寫的程式碼可查詢載入。</span><span class="sxs-lookup"><span data-stu-id="eaef5-138">When you run hello preconfigured indexer on hello sample data source, an index is created and loaded with documents that can then be queried in Search Explorer or by code that you write.</span></span>
