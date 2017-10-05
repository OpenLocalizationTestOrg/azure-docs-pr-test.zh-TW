---
title: "適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢計量 | Microsoft Docs"
description: "了解如何檢測和偵錯 Azure Cosmos DB 要求的 SQL 查詢效能。"
keywords: "sql 語法, sql 查詢, sql 查詢, json 查詢語言, 資料庫概念和 sql 查詢, 彙總函式"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: d928113e809e5ad43901e79dc256a8a39c210181
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a><span data-ttu-id="0e0e0-104">使用 Azure Cosmos DB 調整查詢效能</span><span class="sxs-lookup"><span data-stu-id="0e0e0-104">Tuning query performance with Azure Cosmos DB</span></span>
<span data-ttu-id="0e0e0-105">Azure Cosmos DB 提供一個[適用於查詢資料的 SQL API](documentdb-sql-query.md)，而不需結構描述或次要索引。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-105">Azure Cosmos DB provides a [SQL API for querying data](documentdb-sql-query.md), without requiring schema or secondary indexes.</span></span> <span data-ttu-id="0e0e0-106">本文可為開發人員提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-106">This article provides the following information for developers:</span></span>

* <span data-ttu-id="0e0e0-107">關於 Azure Cosmos DB 之 SQL 查詢執行如何運作的高階詳細資料</span><span class="sxs-lookup"><span data-stu-id="0e0e0-107">High-level details on how Azure Cosmos DB's SQL query execution works</span></span>
* <span data-ttu-id="0e0e0-108">關於查詢要求和回應標頭以及用戶端 SDK 選項的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="0e0e0-108">Details on query request and response headers, and client SDK options</span></span>
* <span data-ttu-id="0e0e0-109">查詢效能的秘訣和最佳作法</span><span class="sxs-lookup"><span data-stu-id="0e0e0-109">Tips and best practices for query performance</span></span>
* <span data-ttu-id="0e0e0-110">如何運用 SQL 執行統計資料來偵錯查詢效能的範例</span><span class="sxs-lookup"><span data-stu-id="0e0e0-110">Examples of how to utilize SQL execution statistics to debug query performance</span></span>

## <a name="about-sql-query-execution"></a><span data-ttu-id="0e0e0-111">關於 SQL 查詢執行</span><span class="sxs-lookup"><span data-stu-id="0e0e0-111">About SQL query execution</span></span>

<span data-ttu-id="0e0e0-112">在 Azure Cosmos DB 中，您會將資料儲存於容器中，其可擴張到任何的[儲存體大小或要求輸送量](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-112">In Azure Cosmos DB, you store data in containers, which can grow to any [storage size or request throughput](partition-data.md).</span></span> <span data-ttu-id="0e0e0-113">Azure Cosmos DB 會在涵蓋範圍內，於實體分割區之間順暢地調整資料，以處理資料成長或提高佈建的輸送量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-113">Azure Cosmos DB seamlessly scales data across physical partitions under the covers to handle data growth or increase in provisioned throughput.</span></span> <span data-ttu-id="0e0e0-114">您可以使用 REST API 或其中一個支援的 [DocumentDB SDK](documentdb-sdk-dotnet.md)，向任何容器發出 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-114">You can issue SQL queries to any container using the REST API or one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span>

<span data-ttu-id="0e0e0-115">分割的簡短概觀：您定義分割區索引鍵 (例如 "city")，以決定在實體分割區之間分割資料的方式。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-115">A brief overview of partitioning: you define a partition key like "city", which determines how data is split across physical partitions.</span></span> <span data-ttu-id="0e0e0-116">屬於單一分割區索引鍵的資料 (例如，"city" == "Seattle") 會儲存於一個實體分割區內，但通常單一實體分割區會具有多個分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-116">Data belonging to a single partition key (for example, "city" == "Seattle") is stored within a physical partition, but typically a single physical partition has multiple partition keys.</span></span> <span data-ttu-id="0e0e0-117">當分割區達到其儲存體大小時，服務會順暢地將該分割區分割為兩個新的分割區，並在這些分割區之間將分割區索引鍵平均分割。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-117">When a partition reaches its storage size, the service seamlessly splits the partition into two new partitions, and divides the partition key evenly across these partitions.</span></span> <span data-ttu-id="0e0e0-118">由於分割區是暫時性的，因此，API 會使用「分割區索引鍵範圍」的抽象概念，來代表分割區索引鍵雜湊的範圍。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-118">Since partitions are transient, the APIs use an abstraction of a "partition key range", which denotes the ranges of partition key hashes.</span></span> 

<span data-ttu-id="0e0e0-119">當您向 Azure Cosmos DB 發出查詢時，SDK 會執行下列邏輯步驟：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-119">When you issue a query to Azure Cosmos DB, the SDK performs these logical steps:</span></span>

* <span data-ttu-id="0e0e0-120">剖析 SQL 查詢以決定查詢執行計畫。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-120">Parse the SQL query to determine the query execution plan.</span></span> 
* <span data-ttu-id="0e0e0-121">如果查詢所包含的篩選係以分割區索引鍵為依據 (例如 `SELECT * FROM c WHERE c.city = "Seattle"`)，即會將該查詢路由傳送至單一分割區。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-121">If the query includes a filter against the partition key, like `SELECT * FROM c WHERE c.city = "Seattle"`, it is routed to a single partition.</span></span> <span data-ttu-id="0e0e0-122">如果查詢中沒有與分割區索引鍵相關的篩選，則會在所有分割區中執行該查詢，且結果會合併用戶端。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-122">If the query does not have a filter on partition key, then it is executed in all partitions, and results are merged client side.</span></span>
* <span data-ttu-id="0e0e0-123">根據用戶端設定而定，查詢會依序或平行地在每個分割區內執行。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-123">The query is executed within each partition in series or parallel, based on client configuration.</span></span> <span data-ttu-id="0e0e0-124">在每個分割區內，根據查詢複雜度、設定的頁面大小，以及集合的佈建輸送量而定，查詢可能會進行一或多次來回行程。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-124">Within each partition, the query might make one or more round trips depending on the query complexity, configured page size, and provisioned throughput of the collection.</span></span> <span data-ttu-id="0e0e0-125">每次執行都會傳回查詢執行所取用的[要求單位](request-units.md)數目，以及 (選擇性地) 查詢執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-125">Each execution returns the number of [request units](request-units.md) consumed by query execution, and optionally, query execution statistics.</span></span> 
* <span data-ttu-id="0e0e0-126">SDK 會跨分割區執行查詢結果的摘要。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-126">The SDK performs a summarization of the query results across partitions.</span></span> <span data-ttu-id="0e0e0-127">例如，如果查詢跨分割區包含 ORDER BY，則來自個別分割區的結果就會依序合併，以全域排序順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-127">For example, if the query involves an ORDER BY across partitions, then results from individual partitions are merge-sorted to return results in globally sorted order.</span></span> <span data-ttu-id="0e0e0-128">如果查詢是 `COUNT` 之類的彙總，即會將來自個別分割區的計數加總以產生整體計數。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-128">If the query is an aggregation like `COUNT`, the counts from individual partitions are summed to produce the overall count.</span></span>

<span data-ttu-id="0e0e0-129">SDK 提供適用於查詢執行的各種選項。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-129">The SDKs provide various options for query execution.</span></span> <span data-ttu-id="0e0e0-130">例如，在 .NET 中，下列選項適用於 `FeedOptions` 類別。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-130">For example, in .NET these options are available in the `FeedOptions` class.</span></span> <span data-ttu-id="0e0e0-131">下表描述這些選項，以及它們如何影響查詢執行時間。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-131">The following table describes these options and how they impact query execution time.</span></span> 

| <span data-ttu-id="0e0e0-132">選項</span><span class="sxs-lookup"><span data-stu-id="0e0e0-132">Option</span></span> | <span data-ttu-id="0e0e0-133">說明</span><span class="sxs-lookup"><span data-stu-id="0e0e0-133">Description</span></span> |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | <span data-ttu-id="0e0e0-134">必須針對任何需要跨多個分割區執行的查詢設定為 true。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-134">Must be set to true for any query that requires to be executed across more than one partition.</span></span> <span data-ttu-id="0e0e0-135">這是一個明確的旗標，讓您能夠在開發期間進行明智的效能取捨。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-135">This is an explicit flag to enable you to make conscious performance tradeoffs during development time.</span></span> |
| `EnableScanInQuery` | <span data-ttu-id="0e0e0-136">如果您已選擇不編製索引，但仍想透過掃描繼續執行查詢，就必須設定為 true。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-136">Must be set to true if you have opted out of indexing, but want to run the query via a scan anyway.</span></span> <span data-ttu-id="0e0e0-137">只有在已停用針對所要求篩選路徑編製索引的功能時才適用。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-137">Only applicable if indexing for the requested filter path is disabled.</span></span> | 
| `MaxItemCount` | <span data-ttu-id="0e0e0-138">在每次到伺服器的來回行程中要傳回的項目數上限。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-138">The maximum number of items to return per round trip to the server.</span></span> <span data-ttu-id="0e0e0-139">設定為 -1，您就能讓伺服器管理項目數。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-139">By setting to -1, you can let the server manage the number of items.</span></span> <span data-ttu-id="0e0e0-140">或者，您可以降低此值，以便在每次來回行程中只擷取少數項目。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-140">Or, you can lower this value to retrieve only a small number of items per round trip.</span></span> 
| `MaxBufferedItemCount` | <span data-ttu-id="0e0e0-141">這是用戶端選項，可在執行跨分割區 ORDER BY 時，用來限制記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-141">This is a client-side option, and used to limit the memory consumption when performing cross-partition ORDER BY.</span></span> <span data-ttu-id="0e0e0-142">較高的值有助於降低跨分割區排序的延遲。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-142">A higher value helps reduce the latency of cross-partition sorting.</span></span> |
| `MaxDegreeOfParallelism` | <span data-ttu-id="0e0e0-143">取得或設定在 Azure DocumentDB 資料庫服務中平行查詢執行期間，在用戶端執行的並行操作次數。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-143">Gets or sets the number of concurrent operations run client side during parallel query execution in the Azure DocumentDB database service.</span></span> <span data-ttu-id="0e0e0-144">正值的屬性值會將並行操作次數限制為設定的值。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-144">A positive property value limits the number of concurrent operations to the set value.</span></span> <span data-ttu-id="0e0e0-145">如果將它設為小於 0，系統就會自動決定要執行的並行操作次數。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-145">If it is set to less than 0, the system automatically decides the number of concurrent operations to run.</span></span> |
| `PopulateQueryMetrics` | <span data-ttu-id="0e0e0-146">啟用在查詢執行的各種階段 (例如，編譯時間、索引迴圈時間及文件載入時間) 所花費時間的統計資料詳細記錄。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-146">Enables detailed logging of statistics of time spent in various phases of query execution like compilation time, index loop time, and document load time.</span></span> <span data-ttu-id="0e0e0-147">您可以與 Azure 支援人員分享來自查詢統計資料的輸出，以診斷查詢效能問題。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-147">You can share output from query statistics with Azure Support to diagnose query performance issues.</span></span> |
| `RequestContinuation` | <span data-ttu-id="0e0e0-148">您可以藉由傳入任何查詢所傳回的不透明接續 Token，繼續進行查詢執行。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-148">You can resume query execution by passing in the opaque continuation token returned by any query.</span></span> <span data-ttu-id="0e0e0-149">接續 Token 會封裝查詢執行所需的所有狀態。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-149">The continuation token encapsulates all state required for query execution.</span></span> |
| `ResponseContinuationTokenLimitInKb` | <span data-ttu-id="0e0e0-150">您可以限制伺服器所傳回之接續 Token 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-150">You can limit the maximum size of the continuation token returned by the server.</span></span> <span data-ttu-id="0e0e0-151">如果您的應用程式主機有回應標頭大小的限制，則您可能需要設定此項。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-151">You might need to set this if your application host has limits on response header size.</span></span> <span data-ttu-id="0e0e0-152">設定此項，可能會增加整體持續時間以及針對查詢所取用的 RU。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-152">Setting this may increase the overall duration and RUs consumed for the query.</span></span>  |

<span data-ttu-id="0e0e0-153">例如，假設我們的範例查詢會將集合上透過 `/city` 要求的分割區索引鍵當作分割區索引鍵，並使用 100,000 RU/秒的輸送量進行佈建。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-153">For example, let's take an example query on partition key requested on a collection with `/city` as the partition key and provisioned with 100,000 RU/s of throughput.</span></span> <span data-ttu-id="0e0e0-154">您可以在 .NET 中使用 `CreateDocumentQuery<T>` 要求此查詢，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-154">You request this query using `CreateDocumentQuery<T>` in .NET like the following:</span></span>

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

<span data-ttu-id="0e0e0-155">如上所示的 SDK 程式碼片段會對應至下列 REST API 要求：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-155">The SDK snippet shown above, corresponds to the following REST API request:</span></span>

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

<span data-ttu-id="0e0e0-156">每個查詢執行頁面都會對應至含有 `Accept: application/query+json` 標頭的 REST API `POST`，以及主體中的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-156">Each query execution page corresponds to a REST API `POST` with the `Accept: application/query+json` header, and the SQL query in the body.</span></span> <span data-ttu-id="0e0e0-157">每個查詢都會利用在用戶端與伺服器之間傳遞的 `x-ms-continuation` Token，來進行到伺服器的一或多次來回行程，以便繼續執行。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-157">Each query makes one or more round trips to the server with the `x-ms-continuation` token echoed between the client and server to resume execution.</span></span> <span data-ttu-id="0e0e0-158">FeedOptions 中的設定選項均會以要求標頭的形式傳遞到伺服器。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-158">The configuration options in FeedOptions are passed to the server in the form of request headers.</span></span> <span data-ttu-id="0e0e0-159">例如，`MaxItemCount` 會對應到 `x-ms-max-item-count`。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-159">For example, `MaxItemCount` corresponds to `x-ms-max-item-count`.</span></span> 

<span data-ttu-id="0e0e0-160">要求會傳回下列 (已截斷以提高可讀性) 的回應：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-160">The request returns the following (truncated for readability) response:</span></span>

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

<span data-ttu-id="0e0e0-161">從查詢傳回的索引鍵回應標頭包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-161">The key response headers returned from the query include the following:</span></span>

| <span data-ttu-id="0e0e0-162">選項</span><span class="sxs-lookup"><span data-stu-id="0e0e0-162">Option</span></span> | <span data-ttu-id="0e0e0-163">說明</span><span class="sxs-lookup"><span data-stu-id="0e0e0-163">Description</span></span> |
| ------ | ----------- |
| `x-ms-item-count` | <span data-ttu-id="0e0e0-164">在回應中傳回的項目數。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-164">The number of items returned in the response.</span></span> <span data-ttu-id="0e0e0-165">這相依於所提供的 `x-ms-max-item-count`、最大回應承載大小內可容納的項目數、佈建的輸送量，以及查詢執行時間。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-165">This is dependent on the supplied `x-ms-max-item-count`, the number of items that can be fit within the maximum response payload size, the provisioned throughput, and query execution time.</span></span> |  
| `x-ms-continuation:` | <span data-ttu-id="0e0e0-166">要繼續執行查詢的接續 Token (如果有其他結果可供使用)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-166">The continuation token to resume execution of the query, if additional results are available.</span></span> | 
| `x-ms-documentdb-query-metrics` | <span data-ttu-id="0e0e0-167">執行的查詢統計資料。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-167">The query statistics for the execution.</span></span> <span data-ttu-id="0e0e0-168">這是一個分隔的字串，包含在查詢執行的各個不同階段所花費時間的統計資料。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-168">This is a delimited string containing statistics of time spent in the various phases of query execution.</span></span> <span data-ttu-id="0e0e0-169">如果將 `x-ms-documentdb-populatequerymetrics` 設為 `True`，即會傳回。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-169">Returned if `x-ms-documentdb-populatequerymetrics` is set to `True`.</span></span> | 
| `x-ms-request-charge` | <span data-ttu-id="0e0e0-170">查詢取用的[要求單位](request-units.md)數目。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-170">The number of [request units](request-units.md) consumed by the query.</span></span> | 

<span data-ttu-id="0e0e0-171">如需 REST API 要求標頭和選項的詳細資訊，請參閱[使用 DocumentDB REST API 查詢資源](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-171">For details on the REST API request headers and options, see [Querying resources using the DocumentDB REST API](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).</span></span>

## <a name="best-practices-for-query-performance"></a><span data-ttu-id="0e0e0-172">查詢效能的最佳作法</span><span class="sxs-lookup"><span data-stu-id="0e0e0-172">Best practices for query performance</span></span>
<span data-ttu-id="0e0e0-173">以下是影響 Azure Cosmos DB 查詢效能的最常見因素。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-173">The following are the most common factors that impact Azure Cosmos DB query performance.</span></span> <span data-ttu-id="0e0e0-174">我們將在本文中更深入探討下列每個主題。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-174">We dig deeper into each of these topics in this article.</span></span>

| <span data-ttu-id="0e0e0-175">因素</span><span class="sxs-lookup"><span data-stu-id="0e0e0-175">Factor</span></span> | <span data-ttu-id="0e0e0-176">秘訣</span><span class="sxs-lookup"><span data-stu-id="0e0e0-176">Tip</span></span> | 
| ------ | -----| 
| <span data-ttu-id="0e0e0-177">佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-177">Provisioned throughput</span></span> | <span data-ttu-id="0e0e0-178">測量每個查詢的 RU，並確認您擁有查詢所需的佈建輸送量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-178">Measure RU per query, and ensure that you have the required provisioned throughput for your queries.</span></span> | 
| <span data-ttu-id="0e0e0-179">分割區和分割區索引鍵</span><span class="sxs-lookup"><span data-stu-id="0e0e0-179">Partitioning and partition keys</span></span> | <span data-ttu-id="0e0e0-180">在篩選子句中偏好使用具有分割區索引鍵的查詢以降低延遲。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-180">Favor queries with the partition key value in the filter clause for low latency.</span></span> |
| <span data-ttu-id="0e0e0-181">SDK 與查詢選項</span><span class="sxs-lookup"><span data-stu-id="0e0e0-181">SDK and query options</span></span> | <span data-ttu-id="0e0e0-182">遵循 SDK 最佳作法 (例如直接連線)，並調整用戶端查詢執行選項。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-182">Follow SDK best practices like direct connectivity, and tune client-side query execution options.</span></span> |
| <span data-ttu-id="0e0e0-183">網路延遲</span><span class="sxs-lookup"><span data-stu-id="0e0e0-183">Network latency</span></span> | <span data-ttu-id="0e0e0-184">在進行測量時需考量網路的額外負荷，並使用多路連接的 API 從最接近的區域進行讀取。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-184">Account for network overhead in measurement, and use multi-homing APIs to read from the nearest region.</span></span> |
| <span data-ttu-id="0e0e0-185">索引原則</span><span class="sxs-lookup"><span data-stu-id="0e0e0-185">Indexing Policy</span></span> | <span data-ttu-id="0e0e0-186">確定您具有查詢所需的編製索引路徑/原則。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-186">Ensure that you have the required indexing paths/policy for the query.</span></span> |
| <span data-ttu-id="0e0e0-187">查詢執行計量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-187">Query execution metrics</span></span> | <span data-ttu-id="0e0e0-188">分析查詢執行計量，以識別可能發生重新寫入的查詢與資料圖形。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-188">Analyze the query execution metrics to identify potential rewrites of query and data shapes.</span></span>  |

### <a name="provisioned-throughput"></a><span data-ttu-id="0e0e0-189">佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-189">Provisioned throughput</span></span>
<span data-ttu-id="0e0e0-190">在 Cosmos DB 中，您會建立資料的容器，每一個容器都具有以每秒要求單位 (RU) 表示的保留輸送量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-190">In Cosmos DB, you create containers of data, each with reserved throughput expressed in request units (RU) per-second.</span></span> <span data-ttu-id="0e0e0-191">讀取 1 KB 文件就是 1 RU，而每個操作 (包括查詢) 都會根據它的複雜度正規化為固定數目的 RU。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-191">A read of a 1-KB document is 1 RU, and every operation (including queries) is normalized to a fixed number of RUs based on its complexity.</span></span> <span data-ttu-id="0e0e0-192">例如，如果您已針對容器佈建了 1000 RU/秒，且具有類似 `SELECT * FROM c WHERE c.city = 'Seattle'` 的查詢 (其取用 5 RU)，則您每秒可執行 (1000 RU/秒) / (5 RU/查詢) = 200 個查詢/秒之類的查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-192">For example, if you have 1000 RU/s provisioned for your container, and you have a query like `SELECT * FROM c WHERE c.city = 'Seattle'` that consumes 5 RUs, then you can perform (1000 RU/s) / (5 RU/query) = 200 query/s such queries per second.</span></span> 

<span data-ttu-id="0e0e0-193">如果您每秒提交 200 個以上的查詢，則服務會在每秒的傳入要求超過 200 個時啟動速率限制。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-193">If you submit more than 200 queries/sec, the service starts rate-limiting incoming requests above 200/s.</span></span> <span data-ttu-id="0e0e0-194">SDK 會藉由執行輪詢/重試來自動處理這種情況，因此您可能會注意到這些查詢具有較高的延遲。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-194">The SDKs automatically handle this case by performing a backoff/retry, therefore you might notice a higher latency for these queries.</span></span> <span data-ttu-id="0e0e0-195">將佈建的輸送量提高為要求的值，即可改善您的查詢延遲和輸送量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-195">Increasing the provisioned throughput to the required value improves your query latency and throughput.</span></span> 

<span data-ttu-id="0e0e0-196">若要深入了解要求單位，請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-196">To learn more about request units, see [Request units](request-units.md).</span></span>

### <a name="partitioning-and-partition-keys"></a><span data-ttu-id="0e0e0-197">分割區和分割區索引鍵</span><span class="sxs-lookup"><span data-stu-id="0e0e0-197">Partitioning and partition keys</span></span>
<span data-ttu-id="0e0e0-198">在 Azure Cosmos DB 中，查詢通常會以下列順序，從最快/最有效率到較慢/較無效率的方式執行。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-198">With Azure Cosmos DB, typically queries perform in the following order from fastest/most efficient to slower/less efficient.</span></span> 

* <span data-ttu-id="0e0e0-199">單一分割區索引鍵和項目索引鍵上的 GET</span><span class="sxs-lookup"><span data-stu-id="0e0e0-199">GET on a single partition key and item key</span></span>
* <span data-ttu-id="0e0e0-200">單一分割區索引鍵上具有篩選子句的查詢</span><span class="sxs-lookup"><span data-stu-id="0e0e0-200">Query with a filter clause on a single partition key</span></span>
* <span data-ttu-id="0e0e0-201">任何屬性上不具等號比較或範圍篩選子句的查詢</span><span class="sxs-lookup"><span data-stu-id="0e0e0-201">Query without an equality or range filter clause on any property</span></span>
* <span data-ttu-id="0e0e0-202">不含篩選的查詢</span><span class="sxs-lookup"><span data-stu-id="0e0e0-202">Query without filters</span></span>

<span data-ttu-id="0e0e0-203">需要查閱所有分割區的查詢需要較高的延遲，而且可以取用較高的 RU。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-203">Queries that need to consult all partitions need higher latency, and can consume higher RUs.</span></span> <span data-ttu-id="0e0e0-204">由於每個分割區都會針對所有屬性自動編製索引，因此，在此情況下，就能有效率地從索引中提供查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-204">Since each partition has automatic indexing against all properties, the query can be served efficiently from the index in this case.</span></span> <span data-ttu-id="0e0e0-205">您可以使用平行處理原則選項，更快速地進行跨越分割區的查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-205">You can make queries that span partitions faster by using the parallelism options.</span></span>

<span data-ttu-id="0e0e0-206">若要深入了解分割區和分割區索引鍵，請參閱[在 Azure Cosmos DB 中進行資料分割](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-206">To learn more about partitioning and partition keys, see [Partitioning in Azure Cosmos DB](partition-data.md).</span></span>

### <a name="sdk-and-query-options"></a><span data-ttu-id="0e0e0-207">SDK 與查詢選項</span><span class="sxs-lookup"><span data-stu-id="0e0e0-207">SDK and query options</span></span>
<span data-ttu-id="0e0e0-208">若要了解如何從 Azure Cosmos DB 取得最佳用戶端效能，請參閱[效能祕訣](performance-tips.md)和[效能測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-208">See [Performance Tips](performance-tips.md) and [Performance testing](performance-testing.md) for how to get the best client-side performance from Azure Cosmos DB.</span></span> <span data-ttu-id="0e0e0-209">這包括使用最新的 SDK、設定平台專屬設定 (例如預設的連線數目)、記憶體回收的頻率，以及使用輕量級連線選項 (例如直接/TCP)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-209">This includes using the latest SDKs, configuring platform-specific configurations like default number of connections, frequency of garbage collection, and using lightweight connectivity options like Direct/TCP.</span></span> 


#### <a name="max-item-count"></a><span data-ttu-id="0e0e0-210">最大項目計數</span><span class="sxs-lookup"><span data-stu-id="0e0e0-210">Max Item Count</span></span>
<span data-ttu-id="0e0e0-211">對於查詢，`MaxItemCount` 的值可能會對端對端查詢時間有重大影響。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-211">For queries, the value of `MaxItemCount` can have a significant impact on end-to-end query time.</span></span> <span data-ttu-id="0e0e0-212">伺服器每次往返將會傳回不超過 `MaxItemCount` 中的項目數 (預設值是 100 個項目)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-212">Each round trip to the server will return no more than the number of items in `MaxItemCount` (Default of 100 items).</span></span> <span data-ttu-id="0e0e0-213">將此設為較高的值 (-1 是最大值，建議使用)，會限制伺服器和用戶端之間的往返次數，尤其是具有大量結果集的查詢，以改善整體查詢持續時間。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-213">Setting this to a higher value (-1 is maximum, and recommended) will improve your query duration overall by limiting the number of round trips between server and client, especially for queries with large result sets.</span></span>

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a><span data-ttu-id="0e0e0-214">平行處理原則的最大程度</span><span class="sxs-lookup"><span data-stu-id="0e0e0-214">Max Degree of Parallelism</span></span>
<span data-ttu-id="0e0e0-215">針對查詢，請調整 `MaxDegreeOfParallelism` 來識別應用程式的最佳設定，特別是當您執行跨分割區查詢時 (不含分割區索引鍵值上的篩選)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-215">For queries, tune the `MaxDegreeOfParallelism` to identify the best configurations for your application, especially if you perform cross-partition queries (without a filter on the partition-key value).</span></span> <span data-ttu-id="0e0e0-216">`MaxDegreeOfParallelism` 可控制平行工作的最大數目，例如，要平行造訪的最大分割區數目。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-216">`MaxDegreeOfParallelism`  controls the maximum number of parallel tasks, i.e., the maximum of partitions to be visited in parallel.</span></span> 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

<span data-ttu-id="0e0e0-217">假設</span><span class="sxs-lookup"><span data-stu-id="0e0e0-217">Let’s assume that</span></span>
* <span data-ttu-id="0e0e0-218">D = 平行工作的預設最大數目 (= 用戶端機器中的處理器數目總計)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-218">D = Default Maximum number of parallel tasks (= total number of processor in the client machine)</span></span>
* <span data-ttu-id="0e0e0-219">P = 使用者指定的平行工作最大數目</span><span class="sxs-lookup"><span data-stu-id="0e0e0-219">P = User-specified maximum number of parallel tasks</span></span>
* <span data-ttu-id="0e0e0-220">N = 針對回答查詢需要造訪的分割區數目</span><span class="sxs-lookup"><span data-stu-id="0e0e0-220">N = Number of partitions that needs  to be visited for answering a query</span></span>

<span data-ttu-id="0e0e0-221">以下是平行查詢對於不同 P 值之行為的影響。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-221">Following are implications of how the parallel queries would behave for different values of P.</span></span>
* <span data-ttu-id="0e0e0-222">(P == 0) => 序列模式</span><span class="sxs-lookup"><span data-stu-id="0e0e0-222">(P == 0) => Serial Mode</span></span>
* <span data-ttu-id="0e0e0-223">(P == 1) => 一項工作的最大值</span><span class="sxs-lookup"><span data-stu-id="0e0e0-223">(P == 1) => Maximum of one task</span></span>
* <span data-ttu-id="0e0e0-224">(P > 1) => 平行工作的最小值 (P, N)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-224">(P > 1) => Min (P, N) parallel tasks</span></span> 
* <span data-ttu-id="0e0e0-225">(P < 1) => 平行工作的最小值 (N, D)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-225">(P < 1) => Min (N, D) parallel tasks</span></span>

<span data-ttu-id="0e0e0-226">如需 SDK 版本資訊，以及所實作類別和方法的詳細資訊，請參閱 [DocumentDB SDK](documentdb-sdk-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-226">For SDK release notes, and details on implemented classes and methods see [DocumentDB SDKs](documentdb-sdk-dotnet.md)</span></span>

### <a name="network-latency"></a><span data-ttu-id="0e0e0-227">網路延遲</span><span class="sxs-lookup"><span data-stu-id="0e0e0-227">Network latency</span></span>
<span data-ttu-id="0e0e0-228">若要了解如何設定全域散發，並連線到最接近的區域，請參閱 [Azure Cosmos DB 全域散發](tutorial-global-distribution-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-228">See [Azure Cosmos DB global distribution](tutorial-global-distribution-documentdb.md) for how to set up global distribution, and connect to the closest region.</span></span> <span data-ttu-id="0e0e0-229">當您需要進行多次來回行程或從查詢擷取大型結果集時，網路延遲會對查詢效能產生顯著影響。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-229">Network latency has a significant impact on query performance when you need to make multiple round-trips or retrieve a large result set from the query.</span></span> 

<span data-ttu-id="0e0e0-230">查詢執行計量上的區段說明如何擷取查詢的伺服器執行時間 ( `totalExecutionTimeInMs`)，以便您可以區分查詢執行所花費的時間以及網路傳輸所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-230">The section on query execution metrics explains how to retrieve the server execution time of queries ( `totalExecutionTimeInMs`), so that you can differentiate between time spent in query execution and time spent in network transit.</span></span>

### <a name="indexing-policy"></a><span data-ttu-id="0e0e0-231">編製索引原則</span><span class="sxs-lookup"><span data-stu-id="0e0e0-231">Indexing policy</span></span>
<span data-ttu-id="0e0e0-232">若要了解編製索引路徑、種類和模式，以及它們如何影響執行查詢，請參閱[設定編製索引原則](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-232">See [Configuring indexing policy](indexing-policies.md) for indexing paths, kinds, and modes, and how they impact query execution.</span></span> <span data-ttu-id="0e0e0-233">根據預設，編製索引原則會針對字串使用雜湊索引編製，這對於等號比較查詢很有效率，但不適用於範圍查詢/排序依據查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-233">By default, the indexing policy uses Hash indexing for strings, which is effective for equality queries, but not for range queries/order by queries.</span></span> <span data-ttu-id="0e0e0-234">如果您需要針對字串進行範圍查詢，我們建議針對所有字串指定範圍索引類型。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-234">If you need range queries for strings, we recommend specifying the Range index type for all strings.</span></span> 

## <a name="query-execution-metrics"></a><span data-ttu-id="0e0e0-235">查詢執行計量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-235">Query execution metrics</span></span>
<span data-ttu-id="0e0e0-236">您可以藉由傳入選擇性的 `x-ms-documentdb-populatequerymetrics` 標頭 (.NET SDK 中的 `FeedOptions.PopulateQueryMetrics`)，來取得查詢執行的詳細計量。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-236">You can obtain detailed metrics on query execution by passing in the optional `x-ms-documentdb-populatequerymetrics` header (`FeedOptions.PopulateQueryMetrics` in the .NET SDK).</span></span> <span data-ttu-id="0e0e0-237">`x-ms-documentdb-query-metrics` 中傳回的值含有下列索引鍵/值組，適用於對查詢執行進行進階疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-237">The value returned in `x-ms-documentdb-query-metrics` has the following key-value pairs meant for advanced troubleshooting of query execution.</span></span> 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| <span data-ttu-id="0e0e0-238">度量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-238">Metric</span></span> | <span data-ttu-id="0e0e0-239">單位</span><span class="sxs-lookup"><span data-stu-id="0e0e0-239">Unit</span></span> | <span data-ttu-id="0e0e0-240">說明</span><span class="sxs-lookup"><span data-stu-id="0e0e0-240">Description</span></span> | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | <span data-ttu-id="0e0e0-241">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-241">milliseconds</span></span> | <span data-ttu-id="0e0e0-242">查詢執行時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-242">Query execution time</span></span> | 
| `queryCompileTimeInMs` | <span data-ttu-id="0e0e0-243">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-243">milliseconds</span></span> | <span data-ttu-id="0e0e0-244">查詢編譯時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-244">Query compile time</span></span>  | 
| `queryLogicalPlanBuildTimeInMs` | <span data-ttu-id="0e0e0-245">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-245">milliseconds</span></span> | <span data-ttu-id="0e0e0-246">建置邏輯查詢計劃的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-246">Time to build logical query plan</span></span> | 
| `queryPhysicalPlanBuildTimeInMs` | <span data-ttu-id="0e0e0-247">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-247">milliseconds</span></span> | <span data-ttu-id="0e0e0-248">建置實體查詢計劃的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-248">Time to build physical query plan</span></span> | 
| `queryOptimizationTimeInMs` | <span data-ttu-id="0e0e0-249">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-249">milliseconds</span></span> | <span data-ttu-id="0e0e0-250">最佳化查詢所花費的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-250">Time spent in optimizing query</span></span> | 
| `VMExecutionTimeInMs` | <span data-ttu-id="0e0e0-251">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-251">milliseconds</span></span> | <span data-ttu-id="0e0e0-252">查詢執行階段所花費的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-252">Time spent in query runtime</span></span> | 
| `indexLookupTimeInMs` | <span data-ttu-id="0e0e0-253">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-253">milliseconds</span></span> | <span data-ttu-id="0e0e0-254">實體索引層內所花費的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-254">Time spent in physical index layer</span></span> | 
| `documentLoadTimeInMs` | <span data-ttu-id="0e0e0-255">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-255">milliseconds</span></span> | <span data-ttu-id="0e0e0-256">載入文件所花費的時間</span><span class="sxs-lookup"><span data-stu-id="0e0e0-256">Time spent in loading documents</span></span>  | 
| `systemFunctionExecuteTimeInMs` | <span data-ttu-id="0e0e0-257">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-257">milliseconds</span></span> | <span data-ttu-id="0e0e0-258">執行系統 (內建) 函式所花費的總時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="0e0e0-258">Total time spent executing system (built-in) functions in milliseconds</span></span>  | 
| `userFunctionExecuteTimeInMs` | <span data-ttu-id="0e0e0-259">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-259">milliseconds</span></span> | <span data-ttu-id="0e0e0-260">執行使用者定義函式所花費的總時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="0e0e0-260">Total time spent executing user-defined functions in milliseconds</span></span> | 
| `retrievedDocumentCount` | <span data-ttu-id="0e0e0-261">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-261">milliseconds</span></span> | <span data-ttu-id="0e0e0-262">擷取的文件總數</span><span class="sxs-lookup"><span data-stu-id="0e0e0-262">Total number of retrieved documents</span></span>  | 
| `retrievedDocumentSize` | <span data-ttu-id="0e0e0-263">位元組</span><span class="sxs-lookup"><span data-stu-id="0e0e0-263">bytes</span></span> | <span data-ttu-id="0e0e0-264">擷取的文件大小總計，以位元組為單位</span><span class="sxs-lookup"><span data-stu-id="0e0e0-264">Total size of retrieved documents in bytes</span></span>  | 
| `outputDocumentCount` | <span data-ttu-id="0e0e0-265">計數</span><span class="sxs-lookup"><span data-stu-id="0e0e0-265">count</span></span> | <span data-ttu-id="0e0e0-266">輸出文件數目</span><span class="sxs-lookup"><span data-stu-id="0e0e0-266">Number of output documents</span></span> | 
| `writeOutputTimeInMs` | <span data-ttu-id="0e0e0-267">毫秒</span><span class="sxs-lookup"><span data-stu-id="0e0e0-267">milliseconds</span></span> | <span data-ttu-id="0e0e0-268">查詢執行時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="0e0e0-268">Query execution time in milliseconds</span></span> | 
| `indexUtilizationRatio` | <span data-ttu-id="0e0e0-269">比率 (<=1)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-269">ratio (<=1)</span></span> | <span data-ttu-id="0e0e0-270">符合篩選的文件數目與所載入文件數目的比率</span><span class="sxs-lookup"><span data-stu-id="0e0e0-270">Ratio of number of documents matched by the filter to the number of documents loaded</span></span>  | 

<span data-ttu-id="0e0e0-271">用戶端 SDK 可能會在內部進行多個查詢操作，以在每個分割區內提供查詢。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-271">The client SDKs may internally make multiple query operations to serve the query within each partition.</span></span> <span data-ttu-id="0e0e0-272">如果結果總數超過 `x-ms-max-item-count`、如果查詢超出分割區的佈建輸送量、如果查詢承載達到每個頁面的大小上限，或者如果查詢達到系統已配置的逾時限制，用戶端就會針對每個分割區進行多個呼叫。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-272">The client makes more than one call per-partition if the total results exceed `x-ms-max-item-count`, if the query exceeds the provisioned throughput for the partition, or if the query payload reaches the maximum size per page, or if the query reaches the system allocated timeout limit.</span></span> <span data-ttu-id="0e0e0-273">每個部分查詢執行都會傳回該頁面的 `x-ms-documentdb-query-metrics`。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-273">Each partial query execution returns a `x-ms-documentdb-query-metrics` for that page.</span></span> 

<span data-ttu-id="0e0e0-274">以下是一些範例查詢，以及如何解譯從查詢執行傳回的部分計量資訊：</span><span class="sxs-lookup"><span data-stu-id="0e0e0-274">Here are some sample queries, and how to interpret some of the metrics returned from query execution:</span></span> 

| <span data-ttu-id="0e0e0-275">查詢</span><span class="sxs-lookup"><span data-stu-id="0e0e0-275">Query</span></span> | <span data-ttu-id="0e0e0-276">範例計量</span><span class="sxs-lookup"><span data-stu-id="0e0e0-276">Sample Metric</span></span> | <span data-ttu-id="0e0e0-277">說明</span><span class="sxs-lookup"><span data-stu-id="0e0e0-277">Description</span></span> | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | <span data-ttu-id="0e0e0-278">擷取的文件數目為 100 + 1，可符合 TOP 子句。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-278">The number of documents retrieved is 100+1 to match the TOP clause.</span></span> <span data-ttu-id="0e0e0-279">查詢時間大部分花費在 `WriteOutputTime` 和 `DocumentLoadTime`，因為它是一次掃描。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-279">Query time is mostly spent in `WriteOutputTime` and `DocumentLoadTime` since it is a scan.</span></span> | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | <span data-ttu-id="0e0e0-280">RetrievedDocumentCount 現在較高 (500+1 以符合 TOP 子句)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-280">RetrievedDocumentCount is now higher (500+1 to match the TOP clause).</span></span> | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | <span data-ttu-id="0e0e0-281">在 IndexLookupTime 中大約花費了 0.9 毫秒進行索引鍵查閱，因為它會透過 `/N/?` 進行索引查閱。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-281">About 0.9 ms is spent in IndexLookupTime for a key lookup, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="0e0e0-282">在範圍索引中，於 IndexLookupTime 中所花費的時間稍微多一點 (1.7 毫秒)，因為它會根據 `/N/?` 進行索引查閱。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-282">Slightly more time (1.7 ms) spent in IndexLookupTime over a range scan, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="0e0e0-283">在 `DocumentLoadTime` 上所花費的時間與上一個查詢相同，但 `WriteOutputTime` 較低，因為我們只要投影一個屬性。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-283">Same time spent on `DocumentLoadTime` as previous queries, but lower `WriteOutputTime` because we're projecting only one property.</span></span> | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | <span data-ttu-id="0e0e0-284">在 `UserDefinedFunctionExecutionTime` 中大約花費了 213 毫秒，以針對 `c.N` 的每個值執行 UDF。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-284">About 213 ms is spent in `UserDefinedFunctionExecutionTime` executing the UDF on each value of `c.N`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | <span data-ttu-id="0e0e0-285">在 `IndexLookupTime` 中針對 `/Name/?` 大約花費了 0.6 毫秒。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-285">About 0.6 ms is spent in `IndexLookupTime` on `/Name/?`.</span></span> <span data-ttu-id="0e0e0-286">`SystemFunctionExecutionTime` 中，大部分的查詢執行時間 (~7 毫秒)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-286">Most of the query execution time (~7 ms) in `SystemFunctionExecutionTime`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | <span data-ttu-id="0e0e0-287">查詢會當作掃描來執行，因為它使用 `LOWER`，而且會傳回 2491 份擷取文件中的 500 份。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-287">Query is performed as a scan because it uses `LOWER`, and 500 out of 2491 retrieved documents are returned.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0e0e0-288">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e0e0-288">Next steps</span></span>
* <span data-ttu-id="0e0e0-289">若要了解支援的 SQL 查詢運算子和關鍵字，請參閱 [SQL 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-289">To learn about the supported SQL query operators and keywords, see [SQL query](documentdb-sql-query.md).</span></span> 
* <span data-ttu-id="0e0e0-290">若要了解要求單位，請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="0e0e0-290">To learn about request units, see [request units](request-units.md).</span></span>
* <span data-ttu-id="0e0e0-291">若要了解編製索引原則，請參閱[編製索引原則](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="0e0e0-291">To learn about indexing policy, see [indexing policy](indexing-policies.md)</span></span> 


