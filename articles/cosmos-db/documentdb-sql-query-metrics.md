---
title: "Azure Cosmos DB DocumentDB api aaaSQL 查詢度量資訊 |Microsoft 文件"
description: "深入了解 tooinstrument 和偵錯 hello Azure Cosmos 資料庫要求的 SQL 查詢效能。"
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
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a><span data-ttu-id="bb110-104">使用 Azure Cosmos DB 調整查詢效能</span><span class="sxs-lookup"><span data-stu-id="bb110-104">Tuning query performance with Azure Cosmos DB</span></span>
<span data-ttu-id="bb110-105">Azure Cosmos DB 提供一個[適用於查詢資料的 SQL API](documentdb-sql-query.md)，而不需結構描述或次要索引。</span><span class="sxs-lookup"><span data-stu-id="bb110-105">Azure Cosmos DB provides a [SQL API for querying data](documentdb-sql-query.md), without requiring schema or secondary indexes.</span></span> <span data-ttu-id="bb110-106">本文提供下列資訊適用於開發人員的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb110-106">This article provides hello following information for developers:</span></span>

* <span data-ttu-id="bb110-107">關於 Azure Cosmos DB 之 SQL 查詢執行如何運作的高階詳細資料</span><span class="sxs-lookup"><span data-stu-id="bb110-107">High-level details on how Azure Cosmos DB's SQL query execution works</span></span>
* <span data-ttu-id="bb110-108">關於查詢要求和回應標頭以及用戶端 SDK 選項的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="bb110-108">Details on query request and response headers, and client SDK options</span></span>
* <span data-ttu-id="bb110-109">查詢效能的秘訣和最佳作法</span><span class="sxs-lookup"><span data-stu-id="bb110-109">Tips and best practices for query performance</span></span>
* <span data-ttu-id="bb110-110">Tooutilize SQL 執行統計資料 toodebug 如何查詢效能的範例</span><span class="sxs-lookup"><span data-stu-id="bb110-110">Examples of how tooutilize SQL execution statistics toodebug query performance</span></span>

## <a name="about-sql-query-execution"></a><span data-ttu-id="bb110-111">關於 SQL 查詢執行</span><span class="sxs-lookup"><span data-stu-id="bb110-111">About SQL query execution</span></span>

<span data-ttu-id="bb110-112">在 Azure Cosmos DB 中，您將資料儲存在 tooany 所能成長的容器[儲存體大小或要求輸送量](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-112">In Azure Cosmos DB, you store data in containers, which can grow tooany [storage size or request throughput](partition-data.md).</span></span> <span data-ttu-id="bb110-113">Azure Cosmos DB 順暢地調整資料在 hello 涵蓋 toohandle 資料成長或佈建輸送量增加下的實體資料分割。</span><span class="sxs-lookup"><span data-stu-id="bb110-113">Azure Cosmos DB seamlessly scales data across physical partitions under hello covers toohandle data growth or increase in provisioned throughput.</span></span> <span data-ttu-id="bb110-114">您可以發出 SQL 查詢 tooany 容器使用 hello REST API 或其中一個支援的 hello [DocumentDB Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-114">You can issue SQL queries tooany container using hello REST API or one of hello supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span>

<span data-ttu-id="bb110-115">分割的簡短概觀：您定義分割區索引鍵 (例如 "city")，以決定在實體分割區之間分割資料的方式。</span><span class="sxs-lookup"><span data-stu-id="bb110-115">A brief overview of partitioning: you define a partition key like "city", which determines how data is split across physical partitions.</span></span> <span data-ttu-id="bb110-116">資料隸屬 tooa 單一資料分割索引鍵 (，例如"city"= = 「 西雅圖 」) 儲存在實體資料分割，但通常單一的實體資料分割有多個資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bb110-116">Data belonging tooa single partition key (for example, "city" == "Seattle") is stored within a physical partition, but typically a single physical partition has multiple partition keys.</span></span> <span data-ttu-id="bb110-117">當資料分割達到其儲存體大小時，hello 服務順暢地 hello 資料分割分成兩個新的資料分割，並在這些資料分割之間平均除以 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bb110-117">When a partition reaches its storage size, hello service seamlessly splits hello partition into two new partitions, and divides hello partition key evenly across these partitions.</span></span> <span data-ttu-id="bb110-118">由於資料分割是暫時性的 hello 應用程式開發介面使用 「 資料分割索引鍵範圍 」，代表 hello 範圍的資料分割索引鍵的雜湊的摘要。</span><span class="sxs-lookup"><span data-stu-id="bb110-118">Since partitions are transient, hello APIs use an abstraction of a "partition key range", which denotes hello ranges of partition key hashes.</span></span> 

<span data-ttu-id="bb110-119">當您發出查詢 tooAzure Cosmos DB 時，hello SDK 就會執行下列邏輯步驟：</span><span class="sxs-lookup"><span data-stu-id="bb110-119">When you issue a query tooAzure Cosmos DB, hello SDK performs these logical steps:</span></span>

* <span data-ttu-id="bb110-120">剖析 hello SQL 查詢 toodetermine hello 查詢執行計畫。</span><span class="sxs-lookup"><span data-stu-id="bb110-120">Parse hello SQL query toodetermine hello query execution plan.</span></span> 
* <span data-ttu-id="bb110-121">如果 hello 查詢包含篩選與 hello 資料分割索引鍵，如`SELECT * FROM c WHERE c.city = "Seattle"`，它是路由的 tooa 單一資料分割。</span><span class="sxs-lookup"><span data-stu-id="bb110-121">If hello query includes a filter against hello partition key, like `SELECT * FROM c WHERE c.city = "Seattle"`, it is routed tooa single partition.</span></span> <span data-ttu-id="bb110-122">如果 hello 查詢並沒有篩選的資料分割索引鍵，則執行的所有資料分割，而且結果會合併用戶端。</span><span class="sxs-lookup"><span data-stu-id="bb110-122">If hello query does not have a filter on partition key, then it is executed in all partitions, and results are merged client side.</span></span>
* <span data-ttu-id="bb110-123">hello 查詢是在數列中每個資料分割內執行，或平行，根據用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="bb110-123">hello query is executed within each partition in series or parallel, based on client configuration.</span></span> <span data-ttu-id="bb110-124">內每個資料分割，hello 查詢可能會讓其中一個或多個往返根據 hello 查詢複雜度，設定頁面大小和佈建輸送量 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="bb110-124">Within each partition, hello query might make one or more round trips depending on hello query complexity, configured page size, and provisioned throughput of hello collection.</span></span> <span data-ttu-id="bb110-125">每次執行會傳回 hello 數目[要求單位](request-units.md)耗用執行查詢，並選擇性地查詢執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="bb110-125">Each execution returns hello number of [request units](request-units.md) consumed by query execution, and optionally, query execution statistics.</span></span> 
* <span data-ttu-id="bb110-126">hello SDK 會在資料分割之間執行 hello 查詢結果的摘要。</span><span class="sxs-lookup"><span data-stu-id="bb110-126">hello SDK performs a summarization of hello query results across partitions.</span></span> <span data-ttu-id="bb110-127">比方說，如果 hello 查詢牽涉到橫跨資料分割的 ORDER BY，然後從個別資料分割的結果是合併排序 tooreturn 結果全域依排序順序。</span><span class="sxs-lookup"><span data-stu-id="bb110-127">For example, if hello query involves an ORDER BY across partitions, then results from individual partitions are merge-sorted tooreturn results in globally sorted order.</span></span> <span data-ttu-id="bb110-128">如果 hello 查詢之類的彙總`COUNT`，個別的資料分割中的 hello 計數會加總的 tooproduce hello 總數。</span><span class="sxs-lookup"><span data-stu-id="bb110-128">If hello query is an aggregation like `COUNT`, hello counts from individual partitions are summed tooproduce hello overall count.</span></span>

<span data-ttu-id="bb110-129">hello Sdk 提供查詢執行的各種選項。</span><span class="sxs-lookup"><span data-stu-id="bb110-129">hello SDKs provide various options for query execution.</span></span> <span data-ttu-id="bb110-130">例如，在.NET 中就使用這些選項在 hello`FeedOptions`類別。</span><span class="sxs-lookup"><span data-stu-id="bb110-130">For example, in .NET these options are available in hello `FeedOptions` class.</span></span> <span data-ttu-id="bb110-131">hello 下表描述這些選項，以及它們如何影響查詢執行時間。</span><span class="sxs-lookup"><span data-stu-id="bb110-131">hello following table describes these options and how they impact query execution time.</span></span> 

| <span data-ttu-id="bb110-132">選項</span><span class="sxs-lookup"><span data-stu-id="bb110-132">Option</span></span> | <span data-ttu-id="bb110-133">說明</span><span class="sxs-lookup"><span data-stu-id="bb110-133">Description</span></span> |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | <span data-ttu-id="bb110-134">必須設定 tootrue 需要 toobe 跨多個分割區執行任何查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-134">Must be set tootrue for any query that requires toobe executed across more than one partition.</span></span> <span data-ttu-id="bb110-135">這是明確的旗標 tooenable 您開發期間的 toomake 做出明智的效能取捨。</span><span class="sxs-lookup"><span data-stu-id="bb110-135">This is an explicit flag tooenable you toomake conscious performance tradeoffs during development time.</span></span> |
| `EnableScanInQuery` | <span data-ttu-id="bb110-136">必須設定 tootrue 如果您已選擇不建立索引，但仍想透過掃描 toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-136">Must be set tootrue if you have opted out of indexing, but want toorun hello query via a scan anyway.</span></span> <span data-ttu-id="bb110-137">只適用於索引 hello 要求已停用篩選路徑。</span><span class="sxs-lookup"><span data-stu-id="bb110-137">Only applicable if indexing for hello requested filter path is disabled.</span></span> | 
| `MaxItemCount` | <span data-ttu-id="bb110-138">hello 的每個往返 toohello 伺服器的項目 tooreturn 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb110-138">hello maximum number of items tooreturn per round trip toohello server.</span></span> <span data-ttu-id="bb110-139">藉由設定太-1，您可以讓 hello 伺服器管理 hello 項目數目。</span><span class="sxs-lookup"><span data-stu-id="bb110-139">By setting too-1, you can let hello server manage hello number of items.</span></span> <span data-ttu-id="bb110-140">或者，您可以降低此值 tooretrieve 只有少數往返每項目。</span><span class="sxs-lookup"><span data-stu-id="bb110-140">Or, you can lower this value tooretrieve only a small number of items per round trip.</span></span> 
| `MaxBufferedItemCount` | <span data-ttu-id="bb110-141">這是用戶端的選項，而且執行跨資料分割 ORDER BY 時，使用 toolimit hello 記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="bb110-141">This is a client-side option, and used toolimit hello memory consumption when performing cross-partition ORDER BY.</span></span> <span data-ttu-id="bb110-142">較高值有助於減少 hello 延遲的排序方式跨資料分割。</span><span class="sxs-lookup"><span data-stu-id="bb110-142">A higher value helps reduce hello latency of cross-partition sorting.</span></span> |
| `MaxDegreeOfParallelism` | <span data-ttu-id="bb110-143">取得或設定執行用戶端 hello Azure DocumentDB 資料庫服務中的平行查詢執行期間的並行作業的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="bb110-143">Gets or sets hello number of concurrent operations run client side during parallel query execution in hello Azure DocumentDB database service.</span></span> <span data-ttu-id="bb110-144">正值的屬性值會限制並行作業 toohello 設定值的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="bb110-144">A positive property value limits hello number of concurrent operations toohello set value.</span></span> <span data-ttu-id="bb110-145">如果它設定為大於 0 的 tooless，hello 系統會自動決定 hello toorun 並行作業數。</span><span class="sxs-lookup"><span data-stu-id="bb110-145">If it is set tooless than 0, hello system automatically decides hello number of concurrent operations toorun.</span></span> |
| `PopulateQueryMetrics` | <span data-ttu-id="bb110-146">啟用在查詢執行的各種階段 (例如，編譯時間、索引迴圈時間及文件載入時間) 所花費時間的統計資料詳細記錄。</span><span class="sxs-lookup"><span data-stu-id="bb110-146">Enables detailed logging of statistics of time spent in various phases of query execution like compilation time, index loop time, and document load time.</span></span> <span data-ttu-id="bb110-147">Azure 支援 toodiagnose 查詢效能問題，您可以共用從 查詢統計資料的輸出。</span><span class="sxs-lookup"><span data-stu-id="bb110-147">You can share output from query statistics with Azure Support toodiagnose query performance issues.</span></span> |
| `RequestContinuation` | <span data-ttu-id="bb110-148">您可以藉由任何查詢所傳回的 hello 不透明的接續 token，傳遞繼續執行查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-148">You can resume query execution by passing in hello opaque continuation token returned by any query.</span></span> <span data-ttu-id="bb110-149">hello 接續 token 封裝所需的查詢執行的所有狀態。</span><span class="sxs-lookup"><span data-stu-id="bb110-149">hello continuation token encapsulates all state required for query execution.</span></span> |
| `ResponseContinuationTokenLimitInKb` | <span data-ttu-id="bb110-150">您可以限制 hello hello 伺服器所傳回的 hello 接續 token 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="bb110-150">You can limit hello maximum size of hello continuation token returned by hello server.</span></span> <span data-ttu-id="bb110-151">您可能需要 tooset 這如果應用程式主機都有回應標頭大小限制。</span><span class="sxs-lookup"><span data-stu-id="bb110-151">You might need tooset this if your application host has limits on response header size.</span></span> <span data-ttu-id="bb110-152">將此設定可能會增加 hello 整體持續期間和 RUs 所耗用的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-152">Setting this may increase hello overall duration and RUs consumed for hello query.</span></span>  |

<span data-ttu-id="bb110-153">比方說，我們的範例查詢要求與集合上的資料分割索引鍵上`/city`為 hello 資料分割索引鍵且佈建 100,000 RU/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="bb110-153">For example, let's take an example query on partition key requested on a collection with `/city` as hello partition key and provisioned with 100,000 RU/s of throughput.</span></span> <span data-ttu-id="bb110-154">您要求此查詢使用`CreateDocumentQuery<T>`.net hello 如下：</span><span class="sxs-lookup"><span data-stu-id="bb110-154">You request this query using `CreateDocumentQuery<T>` in .NET like hello following:</span></span>

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

<span data-ttu-id="bb110-155">hello SDK 程式碼片段，如上所示對應 toohello 下列 REST API 要求：</span><span class="sxs-lookup"><span data-stu-id="bb110-155">hello SDK snippet shown above, corresponds toohello following REST API request:</span></span>

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

<span data-ttu-id="bb110-156">每個查詢執行頁面對應 tooa REST API`POST`以 hello`Accept: application/query+json`標頭，並且在 hello 主體中的 hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-156">Each query execution page corresponds tooa REST API `POST` with hello `Accept: application/query+json` header, and hello SQL query in hello body.</span></span> <span data-ttu-id="bb110-157">每個查詢可讓一或多個四捨五入往返 toohello 伺服器以 hello`x-ms-continuation`回應 hello tooresume 執行用戶端和伺服器之間的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="bb110-157">Each query makes one or more round trips toohello server with hello `x-ms-continuation` token echoed between hello client and server tooresume execution.</span></span> <span data-ttu-id="bb110-158">在 FeedOptions hello 組態選項會傳遞 toohello hello 表單的要求標頭中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb110-158">hello configuration options in FeedOptions are passed toohello server in hello form of request headers.</span></span> <span data-ttu-id="bb110-159">例如，`MaxItemCount`太對應`x-ms-max-item-count`。</span><span class="sxs-lookup"><span data-stu-id="bb110-159">For example, `MaxItemCount` corresponds too`x-ms-max-item-count`.</span></span> 

<span data-ttu-id="bb110-160">hello 要求會傳回 （截斷來提高可讀性） hello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="bb110-160">hello request returns hello following (truncated for readability) response:</span></span>

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

<span data-ttu-id="bb110-161">hello 索引鍵的回應標頭 hello 查詢所傳回的 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="bb110-161">hello key response headers returned from hello query include hello following:</span></span>

| <span data-ttu-id="bb110-162">選項</span><span class="sxs-lookup"><span data-stu-id="bb110-162">Option</span></span> | <span data-ttu-id="bb110-163">說明</span><span class="sxs-lookup"><span data-stu-id="bb110-163">Description</span></span> |
| ------ | ----------- |
| `x-ms-item-count` | <span data-ttu-id="bb110-164">hello hello 回應中傳回的項目數目。</span><span class="sxs-lookup"><span data-stu-id="bb110-164">hello number of items returned in hello response.</span></span> <span data-ttu-id="bb110-165">這是取決於提供的 hello `x-ms-max-item-count`，hello hello 回應承載大小上限、 hello 佈建的輸送量和查詢執行時間內可容納的項目數目。</span><span class="sxs-lookup"><span data-stu-id="bb110-165">This is dependent on hello supplied `x-ms-max-item-count`, hello number of items that can be fit within hello maximum response payload size, hello provisioned throughput, and query execution time.</span></span> |  
| `x-ms-continuation:` | <span data-ttu-id="bb110-166">hello 接續權杖 tooresume 執行 hello 查詢，如果其他結果可供使用。</span><span class="sxs-lookup"><span data-stu-id="bb110-166">hello continuation token tooresume execution of hello query, if additional results are available.</span></span> | 
| `x-ms-documentdb-query-metrics` | <span data-ttu-id="bb110-167">hello hello 執行的查詢統計資料。</span><span class="sxs-lookup"><span data-stu-id="bb110-167">hello query statistics for hello execution.</span></span> <span data-ttu-id="bb110-168">這是時間的分隔的字串，包含花費在 hello 各階段的查詢執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="bb110-168">This is a delimited string containing statistics of time spent in hello various phases of query execution.</span></span> <span data-ttu-id="bb110-169">時所傳回`x-ms-documentdb-populatequerymetrics`設定得`True`。</span><span class="sxs-lookup"><span data-stu-id="bb110-169">Returned if `x-ms-documentdb-populatequerymetrics` is set too`True`.</span></span> | 
| `x-ms-request-charge` | <span data-ttu-id="bb110-170">hello 數目[要求單位](request-units.md)hello 查詢所取用。</span><span class="sxs-lookup"><span data-stu-id="bb110-170">hello number of [request units](request-units.md) consumed by hello query.</span></span> | 

<span data-ttu-id="bb110-171">如需 hello REST API 的要求標頭和選項的詳細資訊，請參閱[查詢使用 hello DocumentDB REST API 資源](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="bb110-171">For details on hello REST API request headers and options, see [Querying resources using hello DocumentDB REST API](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).</span></span>

## <a name="best-practices-for-query-performance"></a><span data-ttu-id="bb110-172">查詢效能的最佳作法</span><span class="sxs-lookup"><span data-stu-id="bb110-172">Best practices for query performance</span></span>
<span data-ttu-id="bb110-173">hello 如下 hello 最常見因素會影響 Azure Cosmos DB 查詢效能。</span><span class="sxs-lookup"><span data-stu-id="bb110-173">hello following are hello most common factors that impact Azure Cosmos DB query performance.</span></span> <span data-ttu-id="bb110-174">我們將在本文中更深入探討下列每個主題。</span><span class="sxs-lookup"><span data-stu-id="bb110-174">We dig deeper into each of these topics in this article.</span></span>

| <span data-ttu-id="bb110-175">因素</span><span class="sxs-lookup"><span data-stu-id="bb110-175">Factor</span></span> | <span data-ttu-id="bb110-176">秘訣</span><span class="sxs-lookup"><span data-stu-id="bb110-176">Tip</span></span> | 
| ------ | -----| 
| <span data-ttu-id="bb110-177">佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="bb110-177">Provisioned throughput</span></span> | <span data-ttu-id="bb110-178">測量 RU 每個查詢，並確認您擁有 hello 需要佈建的輸送量您的查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-178">Measure RU per query, and ensure that you have hello required provisioned throughput for your queries.</span></span> | 
| <span data-ttu-id="bb110-179">分割區和分割區索引鍵</span><span class="sxs-lookup"><span data-stu-id="bb110-179">Partitioning and partition keys</span></span> | <span data-ttu-id="bb110-180">查詢，而非 hello 資料分割索引鍵值的低延遲的 hello 篩選子句中。</span><span class="sxs-lookup"><span data-stu-id="bb110-180">Favor queries with hello partition key value in hello filter clause for low latency.</span></span> |
| <span data-ttu-id="bb110-181">SDK 與查詢選項</span><span class="sxs-lookup"><span data-stu-id="bb110-181">SDK and query options</span></span> | <span data-ttu-id="bb110-182">遵循 SDK 最佳作法 (例如直接連線)，並調整用戶端查詢執行選項。</span><span class="sxs-lookup"><span data-stu-id="bb110-182">Follow SDK best practices like direct connectivity, and tune client-side query execution options.</span></span> |
| <span data-ttu-id="bb110-183">網路延遲</span><span class="sxs-lookup"><span data-stu-id="bb110-183">Network latency</span></span> | <span data-ttu-id="bb110-184">負責網路額外負荷中測量，並使用多路連接的應用程式開發介面 tooread hello 從最接近的區域。</span><span class="sxs-lookup"><span data-stu-id="bb110-184">Account for network overhead in measurement, and use multi-homing APIs tooread from hello nearest region.</span></span> |
| <span data-ttu-id="bb110-185">索引原則</span><span class="sxs-lookup"><span data-stu-id="bb110-185">Indexing Policy</span></span> | <span data-ttu-id="bb110-186">確定您擁有 hello 需要編製索引的路徑/原則 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-186">Ensure that you have hello required indexing paths/policy for hello query.</span></span> |
| <span data-ttu-id="bb110-187">查詢執行計量</span><span class="sxs-lookup"><span data-stu-id="bb110-187">Query execution metrics</span></span> | <span data-ttu-id="bb110-188">分析 hello 查詢執行度量 tooidentify 潛在撰寫查詢與資料的圖形。</span><span class="sxs-lookup"><span data-stu-id="bb110-188">Analyze hello query execution metrics tooidentify potential rewrites of query and data shapes.</span></span>  |

### <a name="provisioned-throughput"></a><span data-ttu-id="bb110-189">佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="bb110-189">Provisioned throughput</span></span>
<span data-ttu-id="bb110-190">在 Cosmos DB 中，您會建立資料的容器，每一個容器都具有以每秒要求單位 (RU) 表示的保留輸送量。</span><span class="sxs-lookup"><span data-stu-id="bb110-190">In Cosmos DB, you create containers of data, each with reserved throughput expressed in request units (RU) per-second.</span></span> <span data-ttu-id="bb110-191">讀取 1 KB 文件為 1 RU 和每一項作業 （包括查詢） 是正規化的 tooa 固定數目 RUs 根據它的複雜度。</span><span class="sxs-lookup"><span data-stu-id="bb110-191">A read of a 1-KB document is 1 RU, and every operation (including queries) is normalized tooa fixed number of RUs based on its complexity.</span></span> <span data-ttu-id="bb110-192">例如，如果您已針對容器佈建了 1000 RU/秒，且具有類似 `SELECT * FROM c WHERE c.city = 'Seattle'` 的查詢 (其取用 5 RU)，則您每秒可執行 (1000 RU/秒) / (5 RU/查詢) = 200 個查詢/秒之類的查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-192">For example, if you have 1000 RU/s provisioned for your container, and you have a query like `SELECT * FROM c WHERE c.city = 'Seattle'` that consumes 5 RUs, then you can perform (1000 RU/s) / (5 RU/query) = 200 query/s such queries per second.</span></span> 

<span data-ttu-id="bb110-193">如果您提交 200 個以上的查詢/sec，超過 200/s 的速率限制連入要求會啟動 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="bb110-193">If you submit more than 200 queries/sec, hello service starts rate-limiting incoming requests above 200/s.</span></span> <span data-ttu-id="bb110-194">hello Sdk 自動處理這種情況，藉由執行輪詢/重試，因此您可能會注意到這些查詢較高的延遲。</span><span class="sxs-lookup"><span data-stu-id="bb110-194">hello SDKs automatically handle this case by performing a backoff/retry, therefore you might notice a higher latency for these queries.</span></span> <span data-ttu-id="bb110-195">增加 hello 佈建輸送量 toohello 需要值可改善您的查詢延遲和輸送量。</span><span class="sxs-lookup"><span data-stu-id="bb110-195">Increasing hello provisioned throughput toohello required value improves your query latency and throughput.</span></span> 

<span data-ttu-id="bb110-196">toolearn 有關要求單位的詳細資訊請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-196">toolearn more about request units, see [Request units](request-units.md).</span></span>

### <a name="partitioning-and-partition-keys"></a><span data-ttu-id="bb110-197">分割區和分割區索引鍵</span><span class="sxs-lookup"><span data-stu-id="bb110-197">Partitioning and partition keys</span></span>
<span data-ttu-id="bb110-198">以 Azure Cosmos DB，通常是查詢中的執行順序，從最快的/最有效率 tooslower/較有效率的 hello。</span><span class="sxs-lookup"><span data-stu-id="bb110-198">With Azure Cosmos DB, typically queries perform in hello following order from fastest/most efficient tooslower/less efficient.</span></span> 

* <span data-ttu-id="bb110-199">單一分割區索引鍵和項目索引鍵上的 GET</span><span class="sxs-lookup"><span data-stu-id="bb110-199">GET on a single partition key and item key</span></span>
* <span data-ttu-id="bb110-200">單一分割區索引鍵上具有篩選子句的查詢</span><span class="sxs-lookup"><span data-stu-id="bb110-200">Query with a filter clause on a single partition key</span></span>
* <span data-ttu-id="bb110-201">任何屬性上不具等號比較或範圍篩選子句的查詢</span><span class="sxs-lookup"><span data-stu-id="bb110-201">Query without an equality or range filter clause on any property</span></span>
* <span data-ttu-id="bb110-202">不含篩選的查詢</span><span class="sxs-lookup"><span data-stu-id="bb110-202">Query without filters</span></span>

<span data-ttu-id="bb110-203">查詢該需要 tooconsult 所有資料分割需要較高的延遲，並可使用更高版本的俄文。</span><span class="sxs-lookup"><span data-stu-id="bb110-203">Queries that need tooconsult all partitions need higher latency, and can consume higher RUs.</span></span> <span data-ttu-id="bb110-204">因為每個資料分割具有自動檢索，針對所有屬性，所以 hello 查詢可以有效地從處理 hello 索引在此情況下。</span><span class="sxs-lookup"><span data-stu-id="bb110-204">Since each partition has automatic indexing against all properties, hello query can be served efficiently from hello index in this case.</span></span> <span data-ttu-id="bb110-205">您可以讓查詢更快的磁碟分割跨越透過 hello 平行處理原則的選項。</span><span class="sxs-lookup"><span data-stu-id="bb110-205">You can make queries that span partitions faster by using hello parallelism options.</span></span>

<span data-ttu-id="bb110-206">toolearn 深入了解資料分割和資料分割索引鍵，請參閱[分割在 Azure Cosmos DB](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-206">toolearn more about partitioning and partition keys, see [Partitioning in Azure Cosmos DB](partition-data.md).</span></span>

### <a name="sdk-and-query-options"></a><span data-ttu-id="bb110-207">SDK 與查詢選項</span><span class="sxs-lookup"><span data-stu-id="bb110-207">SDK and query options</span></span>
<span data-ttu-id="bb110-208">請參閱[效能祕訣](performance-tips.md)和[效能測試](performance-testing.md)如 tooget hello Azure Cosmos DB 從用戶端效能最佳的方式。</span><span class="sxs-lookup"><span data-stu-id="bb110-208">See [Performance Tips](performance-tips.md) and [Performance testing](performance-testing.md) for how tooget hello best client-side performance from Azure Cosmos DB.</span></span> <span data-ttu-id="bb110-209">這包括使用 hello 最新的 Sdk，設定平台專屬組態，例如 預設的連接數目，記憶體回收的頻率，並使用輕量級的連線選項，例如直接/TCP。</span><span class="sxs-lookup"><span data-stu-id="bb110-209">This includes using hello latest SDKs, configuring platform-specific configurations like default number of connections, frequency of garbage collection, and using lightweight connectivity options like Direct/TCP.</span></span> 


#### <a name="max-item-count"></a><span data-ttu-id="bb110-210">最大項目計數</span><span class="sxs-lookup"><span data-stu-id="bb110-210">Max Item Count</span></span>
<span data-ttu-id="bb110-211">查詢，hello 值`MaxItemCount`可以端對端查詢時間有重大影響。</span><span class="sxs-lookup"><span data-stu-id="bb110-211">For queries, hello value of `MaxItemCount` can have a significant impact on end-to-end query time.</span></span> <span data-ttu-id="bb110-212">每個往返 toohello 伺服器將會傳回多項目中的 hello 數目`MaxItemCount`（預設值是 100 個項目）。</span><span class="sxs-lookup"><span data-stu-id="bb110-212">Each round trip toohello server will return no more than hello number of items in `MaxItemCount` (Default of 100 items).</span></span> <span data-ttu-id="bb110-213">設定此 tooa 較高的值 （-1 是最大和建議使用） 會由限制 hello 的往返次數伺服器和用戶端之間，特別是針對大型結果集的查詢來改善整體查詢持續時間。</span><span class="sxs-lookup"><span data-stu-id="bb110-213">Setting this tooa higher value (-1 is maximum, and recommended) will improve your query duration overall by limiting hello number of round trips between server and client, especially for queries with large result sets.</span></span>

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a><span data-ttu-id="bb110-214">平行處理原則的最大程度</span><span class="sxs-lookup"><span data-stu-id="bb110-214">Max Degree of Parallelism</span></span>
<span data-ttu-id="bb110-215">查詢微調 hello `MaxDegreeOfParallelism` tooidentify hello 的最佳組態應用程式，特別是當您執行跨資料分割查詢 （不含篩選的 hello 資料分割索引鍵的值）。</span><span class="sxs-lookup"><span data-stu-id="bb110-215">For queries, tune hello `MaxDegreeOfParallelism` tooidentify hello best configurations for your application, especially if you perform cross-partition queries (without a filter on hello partition-key value).</span></span> <span data-ttu-id="bb110-216">`MaxDegreeOfParallelism`控制 hello 最大的平行工作數，亦即，hello 最多個資料分割 toobe 以平行方式瀏覽。</span><span class="sxs-lookup"><span data-stu-id="bb110-216">`MaxDegreeOfParallelism`  controls hello maximum number of parallel tasks, i.e., hello maximum of partitions toobe visited in parallel.</span></span> 

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

<span data-ttu-id="bb110-217">假設</span><span class="sxs-lookup"><span data-stu-id="bb110-217">Let’s assume that</span></span>
* <span data-ttu-id="bb110-218">D = 預設最大數目 （= hello 用戶端機器中的處理器總數） 的平行工作</span><span class="sxs-lookup"><span data-stu-id="bb110-218">D = Default Maximum number of parallel tasks (= total number of processor in hello client machine)</span></span>
* <span data-ttu-id="bb110-219">P = 使用者指定的平行工作最大數目</span><span class="sxs-lookup"><span data-stu-id="bb110-219">P = User-specified maximum number of parallel tasks</span></span>
* <span data-ttu-id="bb110-220">N = 需要瀏覽 toobe 回應查詢的資料分割數目</span><span class="sxs-lookup"><span data-stu-id="bb110-220">N = Number of partitions that needs  toobe visited for answering a query</span></span>

<span data-ttu-id="bb110-221">以下是 p 的各種值 hello 平行查詢會有的行為的影響</span><span class="sxs-lookup"><span data-stu-id="bb110-221">Following are implications of how hello parallel queries would behave for different values of P.</span></span>
* <span data-ttu-id="bb110-222">(P == 0) => 序列模式</span><span class="sxs-lookup"><span data-stu-id="bb110-222">(P == 0) => Serial Mode</span></span>
* <span data-ttu-id="bb110-223">(P == 1) => 一項工作的最大值</span><span class="sxs-lookup"><span data-stu-id="bb110-223">(P == 1) => Maximum of one task</span></span>
* <span data-ttu-id="bb110-224">(P > 1) => 平行工作的最小值 (P, N)</span><span class="sxs-lookup"><span data-stu-id="bb110-224">(P > 1) => Min (P, N) parallel tasks</span></span> 
* <span data-ttu-id="bb110-225">(P < 1) => 平行工作的最小值 (N, D)</span><span class="sxs-lookup"><span data-stu-id="bb110-225">(P < 1) => Min (N, D) parallel tasks</span></span>

<span data-ttu-id="bb110-226">如需 SDK 版本資訊，以及所實作類別和方法的詳細資訊，請參閱 [DocumentDB SDK](documentdb-sdk-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="bb110-226">For SDK release notes, and details on implemented classes and methods see [DocumentDB SDKs](documentdb-sdk-dotnet.md)</span></span>

### <a name="network-latency"></a><span data-ttu-id="bb110-227">網路延遲</span><span class="sxs-lookup"><span data-stu-id="bb110-227">Network latency</span></span>
<span data-ttu-id="bb110-228">請參閱[Azure Cosmos DB 全域發佈](tutorial-global-distribution-documentdb.md)tooset 如何向上全域發佈，和連接 toohello 最接近的區域。</span><span class="sxs-lookup"><span data-stu-id="bb110-228">See [Azure Cosmos DB global distribution](tutorial-global-distribution-documentdb.md) for how tooset up global distribution, and connect toohello closest region.</span></span> <span data-ttu-id="bb110-229">當您需要多個往返 toomake 或擷取大型結果集從 hello 查詢時，網路延遲會具有重要的影響查詢效能。</span><span class="sxs-lookup"><span data-stu-id="bb110-229">Network latency has a significant impact on query performance when you need toomake multiple round-trips or retrieve a large result set from hello query.</span></span> 

<span data-ttu-id="bb110-230">hello 的查詢執行計量一節說明如何 tooretrieve hello 查詢伺服器執行時間 ( `totalExecutionTimeInMs`)，如此您就可以區分查詢執行所花費的時間以及花在網路傳輸過程中時間之間。</span><span class="sxs-lookup"><span data-stu-id="bb110-230">hello section on query execution metrics explains how tooretrieve hello server execution time of queries ( `totalExecutionTimeInMs`), so that you can differentiate between time spent in query execution and time spent in network transit.</span></span>

### <a name="indexing-policy"></a><span data-ttu-id="bb110-231">編製索引原則</span><span class="sxs-lookup"><span data-stu-id="bb110-231">Indexing policy</span></span>
<span data-ttu-id="bb110-232">若要了解編製索引路徑、種類和模式，以及它們如何影響執行查詢，請參閱[設定編製索引原則](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-232">See [Configuring indexing policy](indexing-policies.md) for indexing paths, kinds, and modes, and how they impact query execution.</span></span> <span data-ttu-id="bb110-233">根據預設，hello 編製索引原則使用雜湊索引的字串，也就是有效的等號查詢，但不適用於範圍查詢/訂單的查詢。</span><span class="sxs-lookup"><span data-stu-id="bb110-233">By default, hello indexing policy uses Hash indexing for strings, which is effective for equality queries, but not for range queries/order by queries.</span></span> <span data-ttu-id="bb110-234">如果您需要範圍查詢字串時，我們建議您指定 hello 範圍索引類型的所有字串。</span><span class="sxs-lookup"><span data-stu-id="bb110-234">If you need range queries for strings, we recommend specifying hello Range index type for all strings.</span></span> 

## <a name="query-execution-metrics"></a><span data-ttu-id="bb110-235">查詢執行計量</span><span class="sxs-lookup"><span data-stu-id="bb110-235">Query execution metrics</span></span>
<span data-ttu-id="bb110-236">您可以取得詳細的度量，於查詢執行傳入 hello 選擇性`x-ms-documentdb-populatequerymetrics`標頭 (`FeedOptions.PopulateQueryMetrics` hello.NET SDK 中)。</span><span class="sxs-lookup"><span data-stu-id="bb110-236">You can obtain detailed metrics on query execution by passing in hello optional `x-ms-documentdb-populatequerymetrics` header (`FeedOptions.PopulateQueryMetrics` in hello .NET SDK).</span></span> <span data-ttu-id="bb110-237">hello 中傳回值`x-ms-documentdb-query-metrics`具有下列索引鍵 / 值組是對進階疑難排解的查詢執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="bb110-237">hello value returned in `x-ms-documentdb-query-metrics` has hello following key-value pairs meant for advanced troubleshooting of query execution.</span></span> 

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

| <span data-ttu-id="bb110-238">計量</span><span class="sxs-lookup"><span data-stu-id="bb110-238">Metric</span></span> | <span data-ttu-id="bb110-239">單位</span><span class="sxs-lookup"><span data-stu-id="bb110-239">Unit</span></span> | <span data-ttu-id="bb110-240">說明</span><span class="sxs-lookup"><span data-stu-id="bb110-240">Description</span></span> | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | <span data-ttu-id="bb110-241">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-241">milliseconds</span></span> | <span data-ttu-id="bb110-242">查詢執行時間</span><span class="sxs-lookup"><span data-stu-id="bb110-242">Query execution time</span></span> | 
| `queryCompileTimeInMs` | <span data-ttu-id="bb110-243">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-243">milliseconds</span></span> | <span data-ttu-id="bb110-244">查詢編譯時間</span><span class="sxs-lookup"><span data-stu-id="bb110-244">Query compile time</span></span>  | 
| `queryLogicalPlanBuildTimeInMs` | <span data-ttu-id="bb110-245">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-245">milliseconds</span></span> | <span data-ttu-id="bb110-246">時間 toobuild 邏輯的查詢計劃</span><span class="sxs-lookup"><span data-stu-id="bb110-246">Time toobuild logical query plan</span></span> | 
| `queryPhysicalPlanBuildTimeInMs` | <span data-ttu-id="bb110-247">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-247">milliseconds</span></span> | <span data-ttu-id="bb110-248">時間 toobuild 實體的查詢計劃</span><span class="sxs-lookup"><span data-stu-id="bb110-248">Time toobuild physical query plan</span></span> | 
| `queryOptimizationTimeInMs` | <span data-ttu-id="bb110-249">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-249">milliseconds</span></span> | <span data-ttu-id="bb110-250">最佳化查詢所花費的時間</span><span class="sxs-lookup"><span data-stu-id="bb110-250">Time spent in optimizing query</span></span> | 
| `VMExecutionTimeInMs` | <span data-ttu-id="bb110-251">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-251">milliseconds</span></span> | <span data-ttu-id="bb110-252">查詢執行階段所花費的時間</span><span class="sxs-lookup"><span data-stu-id="bb110-252">Time spent in query runtime</span></span> | 
| `indexLookupTimeInMs` | <span data-ttu-id="bb110-253">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-253">milliseconds</span></span> | <span data-ttu-id="bb110-254">實體索引層內所花費的時間</span><span class="sxs-lookup"><span data-stu-id="bb110-254">Time spent in physical index layer</span></span> | 
| `documentLoadTimeInMs` | <span data-ttu-id="bb110-255">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-255">milliseconds</span></span> | <span data-ttu-id="bb110-256">載入文件所花費的時間</span><span class="sxs-lookup"><span data-stu-id="bb110-256">Time spent in loading documents</span></span>  | 
| `systemFunctionExecuteTimeInMs` | <span data-ttu-id="bb110-257">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-257">milliseconds</span></span> | <span data-ttu-id="bb110-258">執行系統 (內建) 函式所花費的總時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="bb110-258">Total time spent executing system (built-in) functions in milliseconds</span></span>  | 
| `userFunctionExecuteTimeInMs` | <span data-ttu-id="bb110-259">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-259">milliseconds</span></span> | <span data-ttu-id="bb110-260">執行使用者定義函式所花費的總時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="bb110-260">Total time spent executing user-defined functions in milliseconds</span></span> | 
| `retrievedDocumentCount` | <span data-ttu-id="bb110-261">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-261">milliseconds</span></span> | <span data-ttu-id="bb110-262">擷取的文件總數</span><span class="sxs-lookup"><span data-stu-id="bb110-262">Total number of retrieved documents</span></span>  | 
| `retrievedDocumentSize` | <span data-ttu-id="bb110-263">位元組</span><span class="sxs-lookup"><span data-stu-id="bb110-263">bytes</span></span> | <span data-ttu-id="bb110-264">擷取的文件大小總計，以位元組為單位</span><span class="sxs-lookup"><span data-stu-id="bb110-264">Total size of retrieved documents in bytes</span></span>  | 
| `outputDocumentCount` | <span data-ttu-id="bb110-265">計數</span><span class="sxs-lookup"><span data-stu-id="bb110-265">count</span></span> | <span data-ttu-id="bb110-266">輸出文件數目</span><span class="sxs-lookup"><span data-stu-id="bb110-266">Number of output documents</span></span> | 
| `writeOutputTimeInMs` | <span data-ttu-id="bb110-267">毫秒</span><span class="sxs-lookup"><span data-stu-id="bb110-267">milliseconds</span></span> | <span data-ttu-id="bb110-268">查詢執行時間，以毫秒為單位</span><span class="sxs-lookup"><span data-stu-id="bb110-268">Query execution time in milliseconds</span></span> | 
| `indexUtilizationRatio` | <span data-ttu-id="bb110-269">比率 (<=1)</span><span class="sxs-lookup"><span data-stu-id="bb110-269">ratio (<=1)</span></span> | <span data-ttu-id="bb110-270">Hello 篩選 toohello 編號的文件載入所比對文件數目的比率</span><span class="sxs-lookup"><span data-stu-id="bb110-270">Ratio of number of documents matched by hello filter toohello number of documents loaded</span></span>  | 

<span data-ttu-id="bb110-271">hello 用戶端 Sdk 可能在內部進行多個查詢作業 tooserve hello 查詢內每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="bb110-271">hello client SDKs may internally make multiple query operations tooserve hello query within each partition.</span></span> <span data-ttu-id="bb110-272">hello 用戶端進行多個呼叫每個資料分割如果 hello 總結果超過`x-ms-max-item-count`，如果 hello 查詢超過 hello 佈建的輸送量為 hello 磁碟分割，或如果 hello 查詢裝載達到 hello 的大小上限每一頁，或如果 hello 查詢達到 hello系統配置的逾時限制。</span><span class="sxs-lookup"><span data-stu-id="bb110-272">hello client makes more than one call per-partition if hello total results exceed `x-ms-max-item-count`, if hello query exceeds hello provisioned throughput for hello partition, or if hello query payload reaches hello maximum size per page, or if hello query reaches hello system allocated timeout limit.</span></span> <span data-ttu-id="bb110-273">每個部分查詢執行都會傳回該頁面的 `x-ms-documentdb-query-metrics`。</span><span class="sxs-lookup"><span data-stu-id="bb110-273">Each partial query execution returns a `x-ms-documentdb-query-metrics` for that page.</span></span> 

<span data-ttu-id="bb110-274">以下是一些範例查詢，以及如何 toointerpret hello 度量的某些傳回執行查詢：</span><span class="sxs-lookup"><span data-stu-id="bb110-274">Here are some sample queries, and how toointerpret some of hello metrics returned from query execution:</span></span> 

| <span data-ttu-id="bb110-275">查詢</span><span class="sxs-lookup"><span data-stu-id="bb110-275">Query</span></span> | <span data-ttu-id="bb110-276">範例計量</span><span class="sxs-lookup"><span data-stu-id="bb110-276">Sample Metric</span></span> | <span data-ttu-id="bb110-277">說明</span><span class="sxs-lookup"><span data-stu-id="bb110-277">Description</span></span> | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | <span data-ttu-id="bb110-278">hello 擷取的文件數目是 100 + 1 toomatch hello TOP 子句。</span><span class="sxs-lookup"><span data-stu-id="bb110-278">hello number of documents retrieved is 100+1 toomatch hello TOP clause.</span></span> <span data-ttu-id="bb110-279">查詢時間大部分花費在 `WriteOutputTime` 和 `DocumentLoadTime`，因為它是一次掃描。</span><span class="sxs-lookup"><span data-stu-id="bb110-279">Query time is mostly spent in `WriteOutputTime` and `DocumentLoadTime` since it is a scan.</span></span> | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | <span data-ttu-id="bb110-280">RetrievedDocumentCount 現在是更高版本 （500 + 1 toomatch hello TOP 子句）。</span><span class="sxs-lookup"><span data-stu-id="bb110-280">RetrievedDocumentCount is now higher (500+1 toomatch hello TOP clause).</span></span> | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | <span data-ttu-id="bb110-281">在 IndexLookupTime 中大約花費了 0.9 毫秒進行索引鍵查閱，因為它會透過 `/N/?` 進行索引查閱。</span><span class="sxs-lookup"><span data-stu-id="bb110-281">About 0.9 ms is spent in IndexLookupTime for a key lookup, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="bb110-282">在範圍索引中，於 IndexLookupTime 中所花費的時間稍微多一點 (1.7 毫秒)，因為它會根據 `/N/?` 進行索引查閱。</span><span class="sxs-lookup"><span data-stu-id="bb110-282">Slightly more time (1.7 ms) spent in IndexLookupTime over a range scan, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="bb110-283">在 `DocumentLoadTime` 上所花費的時間與上一個查詢相同，但 `WriteOutputTime` 較低，因為我們只要投影一個屬性。</span><span class="sxs-lookup"><span data-stu-id="bb110-283">Same time spent on `DocumentLoadTime` as previous queries, but lower `WriteOutputTime` because we're projecting only one property.</span></span> | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | <span data-ttu-id="bb110-284">關於 213 ms 花費在`UserDefinedFunctionExecutionTime`執行上的每個值 hello UDF `c.N`。</span><span class="sxs-lookup"><span data-stu-id="bb110-284">About 213 ms is spent in `UserDefinedFunctionExecutionTime` executing hello UDF on each value of `c.N`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | <span data-ttu-id="bb110-285">在 `IndexLookupTime` 中針對 `/Name/?` 大約花費了 0.6 毫秒。</span><span class="sxs-lookup"><span data-stu-id="bb110-285">About 0.6 ms is spent in `IndexLookupTime` on `/Name/?`.</span></span> <span data-ttu-id="bb110-286">大部分的 hello 查詢中的執行時間 （~ 7 毫秒） `SystemFunctionExecutionTime`。</span><span class="sxs-lookup"><span data-stu-id="bb110-286">Most of hello query execution time (~7 ms) in `SystemFunctionExecutionTime`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | <span data-ttu-id="bb110-287">查詢會當作掃描來執行，因為它使用 `LOWER`，而且會傳回 2491 份擷取文件中的 500 份。</span><span class="sxs-lookup"><span data-stu-id="bb110-287">Query is performed as a scan because it uses `LOWER`, and 500 out of 2491 retrieved documents are returned.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="bb110-288">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb110-288">Next steps</span></span>
* <span data-ttu-id="bb110-289">toolearn 有關 hello 支援 SQL 查詢運算子和關鍵字，請參閱[SQL 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-289">toolearn about hello supported SQL query operators and keywords, see [SQL query](documentdb-sql-query.md).</span></span> 
* <span data-ttu-id="bb110-290">toolearn 需要求單位，請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="bb110-290">toolearn about request units, see [request units](request-units.md).</span></span>
* <span data-ttu-id="bb110-291">toolearn 有關編製索引原則，請參閱[編製索引原則](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="bb110-291">toolearn about indexing policy, see [indexing policy](indexing-policies.md)</span></span> 


