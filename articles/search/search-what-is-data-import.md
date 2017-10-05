---
title: "在 Azure 搜尋服務中上傳資料 | Microsoft Docs"
description: "了解如何將資料上傳至 Azure 搜尋服務中的索引"
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
ms.openlocfilehash: 5a601b75ec67824e72d8736bc3c45f8e1231ca86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upload-data-to-azure-search"></a><span data-ttu-id="53c2b-103">上傳資料至 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="53c2b-103">Upload data to Azure Search</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53c2b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="53c2b-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="53c2b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="53c2b-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="53c2b-106">REST</span><span class="sxs-lookup"><span data-stu-id="53c2b-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="53c2b-107">有兩種方法可以在索引中填入資料。</span><span class="sxs-lookup"><span data-stu-id="53c2b-107">There are two ways to populate an index with your data.</span></span> <span data-ttu-id="53c2b-108">第一種方法是使用 Azure 搜尋服務 [REST API](search-import-data-rest-api.md) 或 [.NET SDK](search-import-data-dotnet.md) 來以手動方式將資料推送到索引中。</span><span class="sxs-lookup"><span data-stu-id="53c2b-108">The first option is manually pushing your data into the index using the Azure Search [REST API](search-import-data-rest-api.md) or [.NET SDK](search-import-data-dotnet.md).</span></span> <span data-ttu-id="53c2b-109">第二種方法是[將支援的資料來源指向](search-indexer-overview.md)您的索引，並讓 Azure 搜尋服務自動提取資料。</span><span class="sxs-lookup"><span data-stu-id="53c2b-109">The second option is to [point a supported data source](search-indexer-overview.md) to your index and let Azure Search automatically pull in the data.</span></span>

## <a name="push-data-to-an-index"></a><span data-ttu-id="53c2b-110">將資料推送到索引</span><span class="sxs-lookup"><span data-stu-id="53c2b-110">Push data to an index</span></span>
<span data-ttu-id="53c2b-111">本方法涉及以程式設計方式將資料傳送至 Azure 搜尋服務以便可供搜尋。</span><span class="sxs-lookup"><span data-stu-id="53c2b-111">This approach refers to programmatically sending your data to Azure Search to make it available for searching.</span></span> <span data-ttu-id="53c2b-112">若應用程式需要極低的延遲 (例如，如果您需要讓搜尋作業與動態庫存資料庫保持同步)，推送模式是您的唯一選擇。</span><span class="sxs-lookup"><span data-stu-id="53c2b-112">For applications having very low latency requirements (for example, if you need search operations to be in sync with dynamic inventory databases), the push model is your only option.</span></span>

<span data-ttu-id="53c2b-113">您可以使用 [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) 或 [.NET SDK](search-import-data-dotnet.md) 將資料推送到索引。</span><span class="sxs-lookup"><span data-stu-id="53c2b-113">You can use the [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) or [.NET SDK](search-import-data-dotnet.md) to push data to an index.</span></span> <span data-ttu-id="53c2b-114">目前沒有工具可支援透過入口網站推送資料。</span><span class="sxs-lookup"><span data-stu-id="53c2b-114">There is currently no tool support for pushing data via the portal.</span></span>

<span data-ttu-id="53c2b-115">這種方法比提取模型更有彈性，因為您可以個別或批次上傳文件 (每個批次最多 1000 個或 16 MB，視何者先到達)。</span><span class="sxs-lookup"><span data-stu-id="53c2b-115">This approach is more flexible than the pull model because you can upload documents individually or in batches (up to 1000 per batch or 16 MB, whichever limit comes first).</span></span> <span data-ttu-id="53c2b-116">推送模型也可讓您將文件上傳至 Azure 搜尋服務，無論資料是存放在哪裡。</span><span class="sxs-lookup"><span data-stu-id="53c2b-116">The push model also allows you to upload documents to Azure Search regardless of where your data is.</span></span>

<span data-ttu-id="53c2b-117">Azure 搜尋服務認得的資料格式為 JSON，而資料集中的所有文件都必須具有對應至索引結構描述中所定義欄位的欄位。</span><span class="sxs-lookup"><span data-stu-id="53c2b-117">The data format understood by Azure Search is JSON, and all documents in the dataset must have fields that map to fields defined in your index schema.</span></span> 

## <a name="pull-data-into-an-index"></a><span data-ttu-id="53c2b-118">將資料提取到索引</span><span class="sxs-lookup"><span data-stu-id="53c2b-118">Pull data into an index</span></span>
<span data-ttu-id="53c2b-119">提取模型會將支援的資料來源編目，並自動將資料上傳到您的索引。</span><span class="sxs-lookup"><span data-stu-id="53c2b-119">The pull model crawls a supported data source and automatically uploads the data into your index.</span></span> <span data-ttu-id="53c2b-120">在 Azure 搜尋服務中，這項功能是透過索引子來實作，其目前可供 [Blob 儲存體](search-howto-indexing-azure-blob-storage.md)、[表格儲存體](search-howto-indexing-azure-tables.md)、[Azure Cosmos DB](http://aka.ms/documentdb-search-indexer)、[Azure SQL Database 和 Azure VM 上的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) 使用。</span><span class="sxs-lookup"><span data-stu-id="53c2b-120">In Azure Search, this capability is implemented through *indexers*, currently available for [Blob storage](search-howto-indexing-azure-blob-storage.md), [Table storage](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure SQL database, and SQL Server on Azure VMs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md).</span></span> 

<span data-ttu-id="53c2b-121">索引子可將索引連接到資料來源 (通常是資料表、檢視或對等結構)，並將來源欄位對應至索引中的對等欄位。</span><span class="sxs-lookup"><span data-stu-id="53c2b-121">Indexers connect an index to a data source (usually a table, view, or equivalent structure), and map source fields to equivalent fields in the index.</span></span> <span data-ttu-id="53c2b-122">在執行期間，資料列集會自動轉換為 JSON 並載入指定的索引。</span><span class="sxs-lookup"><span data-stu-id="53c2b-122">During execution, the rowset is automatically transformed to JSON and loaded into the specified index.</span></span> <span data-ttu-id="53c2b-123">所有索引子都支援排程，以便您指定資料重新整理的頻率。</span><span class="sxs-lookup"><span data-stu-id="53c2b-123">All indexers support scheduling so that you can specify how frequently the data is to be refreshed.</span></span> <span data-ttu-id="53c2b-124">如果資料來源支援索引子，則大部分的索引子都會提供變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="53c2b-124">Most indexers provide change tracking if the data source supports it.</span></span> <span data-ttu-id="53c2b-125">除了辨識新文件，索引子還會追蹤現有文件的變更和刪除，讓您不必主動管理索引中的資料。</span><span class="sxs-lookup"><span data-stu-id="53c2b-125">By tracking changes and deletes to existing documents in addition to recognizing new documents, indexers remove the need to actively manage the data in your index.</span></span> 

<span data-ttu-id="53c2b-126">索引子功能會在 [Azure 入口網站](search-import-data-portal.md)、[REST API](/rest/api/searchservice/Indexer-operations) 以及 [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations)中出現。</span><span class="sxs-lookup"><span data-stu-id="53c2b-126">Indexer functionality is exposed in the [Azure portal](search-import-data-portal.md), the [REST API](/rest/api/searchservice/Indexer-operations), and the [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations).</span></span> 

<span data-ttu-id="53c2b-127">使用入口網站的優點是 Azure 搜尋服務通常可藉由讀取來源資料集的中繼資料，為您產生預設的索引結構描述。</span><span class="sxs-lookup"><span data-stu-id="53c2b-127">An advantage to using the portal is that Azure Search can usually generate a default index schema for you by reading the metadata of the source dataset.</span></span> <span data-ttu-id="53c2b-128">直到處理索引後，您才可以修改產生的索引，而後只允許不需要重新編製索引的結構描述編輯。</span><span class="sxs-lookup"><span data-stu-id="53c2b-128">You can modify the generated index until the index is processed, after which the only schema edits allowed are those that do not require reindexing.</span></span> <span data-ttu-id="53c2b-129">如果您想要進行的變更會直接影響結構描述，您必須重建索引。</span><span class="sxs-lookup"><span data-stu-id="53c2b-129">If the changes you want to make impact the schema directly, you would need to rebuild the index.</span></span> 

<span data-ttu-id="53c2b-130">填入索引之後，您可以使用入口網站命令列中的 [搜尋總管] 作為驗證步驟。</span><span class="sxs-lookup"><span data-stu-id="53c2b-130">After the index is populated, you can use **Search Explorer** in the portal command bar as a verification step.</span></span>

## <a name="query-an-index-using-search-explorer"></a><span data-ttu-id="53c2b-131">使用搜尋總管查詢索引</span><span class="sxs-lookup"><span data-stu-id="53c2b-131">Query an index using Search Explorer</span></span>

<span data-ttu-id="53c2b-132">對文件上傳執行初步檢查的快速方法是使用入口網站中的 [搜尋總管]。</span><span class="sxs-lookup"><span data-stu-id="53c2b-132">A quick way to perform a preliminary check on the document upload is to use **Search Explorer** in the portal.</span></span> <span data-ttu-id="53c2b-133">此總管可讓您查詢索引，而不需撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="53c2b-133">The explorer lets you query an index without having to write any code.</span></span> <span data-ttu-id="53c2b-134">搜尋體驗是以預設設定為基礎，例如[簡單語法](/rest/api/searchservice/simple-query-syntax-in-azure-search)和預設 [searchMode 查詢參數](/rest/api/searchservice/search-documents)。</span><span class="sxs-lookup"><span data-stu-id="53c2b-134">The search experience is based on default settings, such as the [simple syntax](/rest/api/searchservice/simple-query-syntax-in-azure-search) and default [searchMode query parameter](/rest/api/searchservice/search-documents).</span></span> <span data-ttu-id="53c2b-135">結果會以 JSON 格式傳回，以便您檢查整份文件。</span><span class="sxs-lookup"><span data-stu-id="53c2b-135">Results are returned in JSON so that you can inspect the entire document.</span></span>

> [!TIP]
> <span data-ttu-id="53c2b-136">許多 [Azure 搜尋服務程式碼範例](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search)包含內嵌或隨手可得的資料集，並提供簡單的開始使用方式。</span><span class="sxs-lookup"><span data-stu-id="53c2b-136">Numerous [Azure Search code samples](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) include embedded or readily available datasets, offering an easy way to get started.</span></span> <span data-ttu-id="53c2b-137">入口網站也會提供範例索引子和資料來源 (由稱為 "realestate-us-sample" 的小型不動產資料集所組成)。</span><span class="sxs-lookup"><span data-stu-id="53c2b-137">The portal also provides a sample indexer and data source consisting of a small real estate dataset (named "realestate-us-sample").</span></span> <span data-ttu-id="53c2b-138">當您在範例資料來源上執行預先設定的索引子時，系統會建立索引並隨著文件載入，而後即可在 [搜尋總管] 中或由您撰寫的程式碼查詢索引。</span><span class="sxs-lookup"><span data-stu-id="53c2b-138">When you run the preconfigured indexer on the sample data source, an index is created and loaded with documents that can then be queried in Search Explorer or by code that you write.</span></span>