---
title: "hello 變更 aaaWorking 摘要支援在 Azure Cosmos DB |Microsoft 文件"
description: "使用 Azure Cosmos DB 變更摘要的支援 tootrack 變更文件中，與執行以事件為基礎的處理，例如觸發程序及保持最新狀態的快取和分析系統。"
keywords: "變更摘要"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="3b9d8-104">使用在 Azure Cosmos DB hello 變更摘要支援</span><span class="sxs-lookup"><span data-stu-id="3b9d8-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="3b9d8-105">[Azure Cosmos DB](../cosmos-db/introduction.md) 是一項快速且有彈性的全域複製資料庫服務，可用來儲存大量的交易式和操作資料，且具有可預測的讀取和寫入個位數毫秒延遲。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="3b9d8-106">這使得它適合用於 IoT、遊戲、零售，以及操作記錄應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="3b9d8-107">這些應用程式中的一般設計模式是 tootrack 變更進行 tooAzure Cosmos DB 的資料，並更新具體化的檢視，根據這些變更的特定事件上執行即時分析、 封存資料 toocold 存放裝置及觸發通知。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="3b9d8-108">hello**變更摘要支援**Azure Cosmos DB 可讓您在 toobuild 有效率且可擴充的解決方案為每個這些模式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="3b9d8-109">變更摘要的支援，Azure Cosmos DB 會提供 Azure Cosmos DB 中的集合已修改它們的 hello 順序中的文件的已排序的清單。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="3b9d8-110">此摘要可以修改 toodata hello 集合內的使用的 toolisten 和執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="3b9d8-111">插入或修改文件時，觸發程序呼叫 tooan 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="3b9d8-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="3b9d8-112">執行即時 (串流) 更新處理</span><span class="sxs-lookup"><span data-stu-id="3b9d8-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="3b9d8-113">與快取、搜尋引擎或資料倉儲進行資料同步處理</span><span class="sxs-lookup"><span data-stu-id="3b9d8-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="3b9d8-114">Azure Cosmos DB 中的變更會加以保存，且可進行非同步處理，並分散到一或多個取用者以進行平行處理。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="3b9d8-115">讓我們看看 hello 應用程式開發介面的變更摘要，並且您可以如何使用這些 toobuild 可擴充的即時應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="3b9d8-116">本文示範如何搭配 Azure Cosmos DB toowork 變更摘要 」 和 「 hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![使用 Azure Cosmos DB 變更摘要 toopower 即時分析和事件導向運算的案例](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="3b9d8-118">變更摘要支援僅提供 hello DocumentDB API 在這個階段中。hello Graph API 和資料表 API 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="3b9d8-119">使用個案和案例</span><span class="sxs-lookup"><span data-stu-id="3b9d8-119">Use cases and scenarios</span></span>
<span data-ttu-id="3b9d8-120">變更摘要可有效處理大型資料集有大量的寫入時，可讓，並提供替代 tooquerying 整個資料集 tooidentify 有什麼變更。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="3b9d8-121">比方說，您可以執行下列工作有效率地 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="3b9d8-122">透過儲存在 Azure Cosmos DB 中的資料，來更新快取、搜尋索引或資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="3b9d8-123">實作階層處理和封存的應用程式層級資料，也就是儲存在 Azure Cosmos DB 中，「 熱資料 」，並且太到期 「 冷資料 」[Azure Blob 儲存體](../storage/common/storage-introduction.md)或[Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="3b9d8-124">使用 [Apache Hadoop](run-hadoop-with-hdinsight.md) 在資料上實作批次分析。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="3b9d8-125">透過 Azure Cosmos DB [在 Azure 上實作 Lambda 管線 (英文)](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="3b9d8-126">Azure Cosmos DB 提供一個可調整的資料庫解決方案，可以處理擷取和查詢，並實作具有低 TCO 的 Lambda 架構。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="3b9d8-127">執行零停機時間移轉 tooanother Azure Cosmos DB 帳戶不同的資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="3b9d8-128">**搭配 Azure Cosmos DB 使用 Lambda 管線進行擷取和查詢：**</span><span class="sxs-lookup"><span data-stu-id="3b9d8-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![適用於擷取和查詢的 Azure Cosmos DB 型 Lambda 管線](./media/change-feed/lambda.png)

<span data-ttu-id="3b9d8-130">您可以使用 Azure Cosmos DB tooreceive 和儲存事件資料，從裝置、 感應器、 基礎結構和應用程式，並處理這些事件與即時[Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md)， [Apache Storm](../hdinsight/hdinsight-storm-overview.md)，或[Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="3b9d8-131">在您[無伺服器](http://azure.com/serverless)web 和行動裝置應用程式，您可以追蹤事件，例如變更 tooyour 客戶的設定檔、 喜好設定或位置 tootrigger 特定動作，如傳送推播通知 tootheir 裝置使用[Azure 函數](../azure-functions/functions-bindings-documentdb.md)或[應用程式服務](https://azure.microsoft.com/services/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="3b9d8-132">如果您使用 Azure Cosmos DB toobuild 遊戲，比方說，您可以使用變更摘要的 tooimplement 即時排行榜根據從已完成的遊戲的分數。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="3b9d8-133">變更摘要在 Azure Cosmos DB 中的運作方式</span><span class="sxs-lookup"><span data-stu-id="3b9d8-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="3b9d8-134">Azure 的 Cosmos DB 會提供 hello 能力 tooincrementally 讀取所做的更新 tooan Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="3b9d8-135">此變更摘要具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="3b9d8-136">變更會在 Azure Cosmos DB 中持續保存，並且可以非同步處理。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="3b9d8-137">在集合中的變更 toodocuments 可立即用於 hello 變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="3b9d8-138">每個變更 tooa 文件會出現一次在 hello 變更的摘要，以及用戶端管理其檢查點的邏輯。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="3b9d8-139">hello 變更摘要的處理器程式庫會提供自動檢查點和 「 至少一次 」 語意。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="3b9d8-140">唯一 hello 最新變更給定文件包含在 hello 變更記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="3b9d8-141">中繼變更可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="3b9d8-142">hello 變更摘要 （依照修改內每個資料分割索引鍵值的順序） 排序。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="3b9d8-143">跨資料分割索引鍵值順序不會是固定的。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="3b9d8-144">變更可以從任何時間點同步處理，也就是說，可用變更沒有固定的資料保留期限。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="3b9d8-145">變更會以資料分割索引鍵區塊為單位提供。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="3b9d8-146">這項功能可讓大型集合 toobe 平行處理多個取用者/伺服器的變更。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="3b9d8-147">應用程式可以要求多個變更的摘要同時 hello 相同的集合。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="3b9d8-148">根據預設，所有帳戶都會啟用 Azure Cosmos DB 的變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="3b9d8-149">您可以使用您[佈建的輸送量](request-units.md)中寫入區域或任何[讀取區域](distribute-data-globally.md)tooread hello 從變更的摘要，就像任何其他作業，從 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="3b9d8-150">hello 變更摘要會包含插入和更新作業進行 toodocuments hello 集合內。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="3b9d8-151">您可以擷取刪除項目，方法是在您的文件內設定「虛刪除」旗標來取代刪除動作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="3b9d8-152">或者，您可以設定您的文件，透過 hello 有限的逾期期限[TTL 功能](time-to-live.md)，例如，24 小時和使用 hello 值 toocapture 刪除該屬性。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="3b9d8-153">此解決方案中，您可以 tooprocess 變更比 hello TTL 到期期限內存留較短的時間間隔內。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="3b9d8-154">hello 變更摘要供在 hello 文件集合中，每個資料分割索引鍵範圍，因此可以分散安裝在平行處理的一或多個取用者。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB 變更摘要的分散式處理](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="3b9d8-156">關於如何在用戶端程式碼中實作變更摘要，我們提供了幾個選項給您。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="3b9d8-157">hello 區段，請立即遵循說明 tooimplement hello 使用 hello Azure Cosmos DB REST API 的變更摘要的方式，和 hello DocumentDB Sdk。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="3b9d8-158">不過，.NET 應用程式，我們建議您使用 hello 新[變更摘要處理器庫](#change-feed-processor)簡化資料分割的讀取變更，並可讓多個執行緒使用，處理事件從 hello 變更摘要平行。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="3b9d8-159"><a id="rest-apis"></a>使用 REST API 和 DocumentDB Sdk hello</span><span class="sxs-lookup"><span data-stu-id="3b9d8-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="3b9d8-160">Azure Cosmos DB 提供彈性的儲存體及輸送量容器，稱為**集合**。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="3b9d8-161">集合內的資料會針對延展性和效能，使用[資料分割索引鍵](partition-data.md)以邏輯方式分組。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="3b9d8-162">Azure Cosmos DB 提供各種用來存取此資料的 API，包括依識別碼查閱 (Read/Get)、查詢及讀取摘要 (掃描)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="3b9d8-163">hello 變更摘要，可取得擴展兩個新的要求標頭 toohello DocumentDB`ReadDocumentFeed`應用程式開發介面，而且跨越的資料分割索引鍵範圍以平行方式處理。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="3b9d8-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="3b9d8-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="3b9d8-165">讓我們快速看一下 ReadDocumentFeed 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="3b9d8-166">Azure Cosmos DB 支援讀取透過 hello 集合內的文件的摘要`ReadDocumentFeed`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="3b9d8-167">例如，hello 下列要求會傳回文件內部 hello 頁面`serverlogs`集合。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="3b9d8-168">結果會受到使用 hello`x-ms-max-item-count`由重新送出 hello 要求，則可以繼續標頭，並且讀取`x-ms-continuation`hello 前一個回應中傳回的標頭。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="3b9d8-169">當從單一用戶端執行時，`ReadDocumentFeed` 會以序列方式逐一查看資料分割之間的結果。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="3b9d8-170">**序列讀取文件摘要**</span><span class="sxs-lookup"><span data-stu-id="3b9d8-170">**Serial read document feed**</span></span>

<span data-ttu-id="3b9d8-171">您也可以擷取的文件使用其中一種支援的 hello hello 摘要[Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="3b9d8-172">例如，下列程式碼片段說明如何 hello toouse hello [ReadDocumentFeedAsync 方法](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet).NET 中。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="3b9d8-173">ReadDocumentFeed 的分散式執行</span><span class="sxs-lookup"><span data-stu-id="3b9d8-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="3b9d8-174">針對包含數 TB 以上資料或需內嵌大量更新的集合，序列執行單一用戶端電腦的讀取摘要可能不夠實際。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="3b9d8-175">在訂單 toosupport 這些巨量資料案例中，Azure Cosmos DB 也提供 Api toodistribute`ReadDocumentFeed`無障礙地跨多個用戶端讀取器/取用者呼叫。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="3b9d8-176">**分散式讀取文件摘要**</span><span class="sxs-lookup"><span data-stu-id="3b9d8-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="3b9d8-177">累加變更，Azure Cosmos DB tooprovide 可擴充處理 hello 變更摘要的資料分割索引鍵範圍為基礎的應用程式開發介面支援向外延展模型。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="3b9d8-178">您可以針對執行 `ReadPartitionKeyRanges` 呼叫的集合取得資料分割索引鍵範圍的清單。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="3b9d8-179">對於每個資料分割索引鍵範圍，您可以執行`ReadDocumentFeed`tooread 該範圍內的資料分割索引鍵的文件。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="3b9d8-180">擷取集合的資料分割索引鍵範圍</span><span class="sxs-lookup"><span data-stu-id="3b9d8-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="3b9d8-181">您可以擷取要求的 hello hello 資料分割索引鍵範圍`pkranges`集合中的資源。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="3b9d8-182">例如 hello 下列要求會擷取 hello 份資料分割索引鍵範圍 hello`serverlogs`集合：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="3b9d8-183">此要求會傳回下列回應包含 hello 資料分割索引鍵範圍的相關中繼資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="3b9d8-184">**資料分割索引鍵範圍屬性**： 每個資料分割索引鍵範圍 hello 中繼資料中包含下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="3b9d8-185">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="3b9d8-185">Header name</span></span></th>
        <th><span data-ttu-id="3b9d8-186">說明</span><span class="sxs-lookup"><span data-stu-id="3b9d8-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-187">id</span><span class="sxs-lookup"><span data-stu-id="3b9d8-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="3b9d8-188">hello 識別碼 hello 資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="3b9d8-189">這是每個集合內穩定且唯的一識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="3b9d8-190">必須使用下列呼叫 tooread 變更 hello 中資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="3b9d8-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="3b9d8-192">hello 最大的磁碟分割 hello 資料分割索引鍵範圍的索引鍵的雜湊值。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="3b9d8-193">供內部使用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="3b9d8-194">minInclusive</span></span></td>
        <td><span data-ttu-id="3b9d8-195">hello 最小分割區 hello 資料分割索引鍵範圍的索引鍵的雜湊值。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="3b9d8-196">供內部使用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="3b9d8-197">您可以使用其中一種支援的 hello [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="3b9d8-198">比方說，hello 下列程式碼片段示範如何 tooretrieve 資料分割索引鍵範圍在.NET 中使用 hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet)方法。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="3b9d8-199">Azure Cosmos DB 支援擷取的每個資料分割索引鍵範圍的文件的選擇性設定 hello`x-ms-documentdb-partitionkeyrangeid`標頭。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="3b9d8-200">執行累加式 ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="3b9d8-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="3b9d8-201">ReadDocumentFeed 支援下列案例/工作的 Azure Cosmos DB 集合中的變更累加處理 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="3b9d8-202">讀取所有變更 toodocuments 從 hello 開頭，也就是從集合建立。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="3b9d8-203">讀取所有變更 toofuture 更新 toodocuments 從目前的時間或任何變更，因為使用者指定的時間。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="3b9d8-204">讀取所有變更 toodocuments hello 集合 (ETag) 的邏輯版本。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="3b9d8-205">您可以根據 hello 累加讀取摘要要求所傳回的 ETag 的取用者的檢查點。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="3b9d8-206">hello 變更包括 toodocuments 插入和更新。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="3b9d8-207">toocapture 刪除，您必須使用在文件中的 「 虛刪除 」 的屬性，或使用 hello[內建的 TTL 屬性](time-to-live.md)toosignal hello 暫止刪除動作變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="3b9d8-208">下列表格列出 hello hello[要求](/rest/api/documentdb/common-documentdb-rest-request-headers.md)和[回應標頭](/rest/api/documentdb/common-documentdb-rest-response-headers.md)ReadDocumentFeed 作業。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="3b9d8-209">**累加式 ReadDocumentFeed 的要求標頭**：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="3b9d8-210">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="3b9d8-210">Header name</span></span></th>
        <th><span data-ttu-id="3b9d8-211">說明</span><span class="sxs-lookup"><span data-stu-id="3b9d8-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="3b9d8-212">A-IM</span></span></td>
        <td><span data-ttu-id="3b9d8-213">必須設定太"Incremental 摘要 」，或省略</span><span class="sxs-lookup"><span data-stu-id="3b9d8-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="3b9d8-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="3b9d8-215">沒有標頭： 從 hello 開頭 （建立集合） 會傳回所有變更</span><span class="sxs-lookup"><span data-stu-id="3b9d8-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="3b9d8-216">"*": 傳回 hello 集合內的所有新變更 toodata</span><span class="sxs-lookup"><span data-stu-id="3b9d8-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="3b9d8-217">&lt;etag&gt;： 如果設定 tooa 集合 ETag，會傳回所有的邏輯時間戳記之後所做的變更</span><span class="sxs-lookup"><span data-stu-id="3b9d8-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="3b9d8-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="3b9d8-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="3b9d8-219">RFC 1123 時間格式；如果已指定 If-None-Match，則忽略</span><span class="sxs-lookup"><span data-stu-id="3b9d8-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="3b9d8-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="3b9d8-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="3b9d8-221">讀取資料的資料分割索引鍵範圍識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="3b9d8-222">**累加式 ReadDocumentFeed 的回應標頭**：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="3b9d8-223">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="3b9d8-223">Header name</span></span></th>
        <th><span data-ttu-id="3b9d8-224">說明</span><span class="sxs-lookup"><span data-stu-id="3b9d8-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-225">etag</span><span class="sxs-lookup"><span data-stu-id="3b9d8-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="3b9d8-226">hello 邏輯序號 (LSN) 的最後一個 hello 回應中傳回的文件。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="3b9d8-227">透過在 If-None-Match 中重新提交此值，可以繼續執行累加式 ReadDocumentFeed。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="3b9d8-228">以下是範例要求 tooreturn hello 邏輯版本/ETag 從集合中的所有增量變更`28535`和資料分割索引鍵範圍 = `16`:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="3b9d8-229">變更會依據排序內每個資料分割索引鍵值 hello 資料分割索引鍵範圍內的時間。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="3b9d8-230">跨資料分割索引鍵值順序不會是固定的。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="3b9d8-231">如果有超過可在單一頁面中容納更多結果，您可以重新提交具有以 hello hello 要求讀取下一頁結果 hello`If-None-Match`標頭的值等於 toohello`etag`從 hello 前一個回應。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="3b9d8-232">如果多個文件插入或更新預存程序或觸發程序內的交易，它們將全部傳回 hello 內相同的回應頁面。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="3b9d8-233">使用變更的摘要，您可能會收到多個項目中所指定，在頁面中傳回`x-ms-max-item-count`在 hello 案例中的多個文件中插入或更新預存程序或觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="3b9d8-234">Hello.NET SDK (1.17.0) 時，設定 hello 欄位`StartTime`中`ChangeFeedOptions`toodirectly 傳回變更後的文件`StartTime`呼叫時`CreateDocumentChangeFeedQuery`。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="3b9d8-235">藉由指定`If-Modified-Since`使用 hello REST API，您的要求會傳回不 hello 文件，本身，但而 hello 接續 token 或`etag`hello 回應標頭中。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="3b9d8-236">修改過的 hello 指定 hello 接續 token 的時間之 tooreturn hello 文件`etag`然後必須使用與 hello 下一次要求`If-None-Match`tooreturn hello 實際文件。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="3b9d8-237">hello.NET SDK 提供 hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet)和[ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper 類別 tooaccess 變更 tooa 集合。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="3b9d8-238">hello 下列程式碼片段示範如何 tooretrieve 所有變更從 hello 開頭使用從單一用戶端 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="3b9d8-239">Hello 下列程式碼片段示範如何 tooprocess 變更即時和搭配使用 hello 變更 Azure Cosmos DB 摘要支援和 hello 前面函式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="3b9d8-240">hello 第一次呼叫 hello 集合中傳回所有 hello 文件，hello 第二個只會都傳回 hello 兩份文件建立 hello 最後一個檢查點之後所建立。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="3b9d8-241">您也可以篩選 hello 使用用戶端邏輯 tooselectively 程序事件的變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="3b9d8-242">例如，以下是使用用戶端端 LINQ tooprocess 僅溫度變更事件，從裝置感應器的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="3b9d8-243"><a id="change-feed-processor"></a>變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="3b9d8-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="3b9d8-244">另一個選項是 toouse hello [Azure Cosmos DB 變更摘要處理器文件庫](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)，這可以幫助您輕鬆地分散處理從摘要跨多個取用者的變更的事件。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="3b9d8-245">hello 程式庫適合用來建置摘要讀取器 hello.NET 平台上的變更。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="3b9d8-246">透過使用包含在 hello hello 方法 hello 變更摘要處理器文件庫會簡化某些工作流程其他 Cosmos DB Sdk 包括：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="3b9d8-247">當資料儲存在多個分割區時，提取變更摘要的更新</span><span class="sxs-lookup"><span data-stu-id="3b9d8-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="3b9d8-248">移動，或從一個集合 tooanother 複寫資料</span><span class="sxs-lookup"><span data-stu-id="3b9d8-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="3b9d8-249">平行執行的更新 toodata 所觸發的動作和摘要的變更</span><span class="sxs-lookup"><span data-stu-id="3b9d8-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="3b9d8-250">雖然使用 hello Cosmos Sdk 中的 hello Api 提供精確的存取 toochange 摘要更新每個資料分割中，使用 hello 變更摘要處理器文件庫簡化讀取變更資料分割和多個平行運作的執行緒。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="3b9d8-251">而不是以手動方式讀取每個容器中的變更並儲存每個資料分割的接續 token，hello 變更摘要處理器會自動管理讀取變更資料分割使用租用機制。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="3b9d8-252">hello 程式庫是以 NuGet 套件形式提供： [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)來源為 Github 的程式碼往來[範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="3b9d8-253">了解變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="3b9d8-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="3b9d8-254">有四個主要元件實作 hello 變更摘要的處理器： hello 監視集合、 hello 租用集合、 hello 處理器主機和 hello 取用者。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="3b9d8-255">**受監視的集合：** hello 監視集合已 hello 資料產生哪些 hello 變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="3b9d8-256">任何插入和變更 toohello 監視集合會反映在 hello 集合的 hello 變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="3b9d8-257">**租用集合：** hello 租用集合座標處理 hello 變更摘要跨多個背景工作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="3b9d8-258">個別集合是一個租用，每個資料分割使用的 toostore hello 租用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="3b9d8-259">在不同的帳戶以 hello 這個租用集合寫入區域變更摘要的處理器執行接近 toowhere hello 有利 toostore 它。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="3b9d8-260">租用物件包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="3b9d8-261">擁有者： 指定擁有 hello 租用 hello 主機</span><span class="sxs-lookup"><span data-stu-id="3b9d8-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="3b9d8-262">接續： 指定在 hello 變更特定資料分割摘要 hello 位置 (接續 token)</span><span class="sxs-lookup"><span data-stu-id="3b9d8-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="3b9d8-263">時間戳記： 上次更新租用。hello 時間戳記會使用的 toocheck 無論 hello 租用會視為已過期</span><span class="sxs-lookup"><span data-stu-id="3b9d8-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="3b9d8-264">**處理器的主機：**多少資料分割 tooprocess 根據多少的主控件的執行個體有作用中租用時，決定每一部主機。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="3b9d8-265">主應用程式啟動時，它會取得所有主機之間的租用 toobalance hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="3b9d8-266">主機會定期更新租用，以便讓租用保持作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="3b9d8-267">主機的檢查點 hello 最後一個接續權杖 tooits 租用每個讀取。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="3b9d8-268">tooensure 並行安全，主機就會檢查每個租用更新 hello ETag。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="3b9d8-269">主機也支援其他檢查點策略。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="3b9d8-270">在關機，主機會釋出所有租用，但保留 hello 接續資訊，因此它可以繼續讀取 hello 預存的檢查點之後。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="3b9d8-271">在此階段 hello 主機數目不能大於 hello 資料分割 （租用） 的數目。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="3b9d8-272">**取用者：**取用者或背景工作，是指執行 hello 變更摘要處理每個主機所起始的執行緒。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="3b9d8-273">每個處理器主機都可以有多個取用者。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="3b9d8-274">每一個取用者讀取 hello 變更摘要 hello 從磁碟分割指派 tooand 通知其主機的變更和過期租用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="3b9d8-275">toofurther 了解這些四個元素的變更摘要處理器如何一起運作，讓我們看看下列圖表中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="3b9d8-276">hello 監視集合存放區文件，而且使用 hello"city"hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="3b9d8-277">我們看到藍色 hello 分割區包含從"A E"hello"city"欄位的文件，依此類推。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="3b9d8-278">有兩部主機，每個都有兩個取用者從 hello 四個資料分割，以平行方式讀取。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="3b9d8-279">hello 箭號顯示 hello 取用者讀取 hello 中的特定點變更摘要。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="3b9d8-280">Hello 第一個資料分割中 hello 深藍色代表未讀取的變更而 hello 淺藍色代表 hello 已經讀取 hello 變更摘要的變更。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="3b9d8-281">hello 主機使用 hello 租用集合 toostore 「 接續 」 值 tookeep 追蹤記錄的 hello 目前讀取每一個取用者的位置。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![使用 hello Azure Cosmos DB 變更摘要處理器主機](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="3b9d8-283">使用變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="3b9d8-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="3b9d8-284">hello 下列章節說明如何 toouse hello 變更複寫來源集合 tooa 目的地集合中的 hello 內容中的變更摘要處理器文件庫。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="3b9d8-285">此處 hello 來源集合是 hello 監視集合中變更摘要的處理器。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="3b9d8-286">**安裝並包含 hello 變更摘要處理器 NuGet 封裝**</span><span class="sxs-lookup"><span data-stu-id="3b9d8-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="3b9d8-287">在安裝變更摘要處理器 NuGet 套件之前，請先安裝：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="3b9d8-288">Microsoft.Azure.DocumentDB 1.13.1 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="3b9d8-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="3b9d8-289">Newtonsoft.Json 9.0.1 版或更新版本 安裝 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 並將它納入以作為參考。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="3b9d8-290">**建立受監視的租用集合和目的地集合**</span><span class="sxs-lookup"><span data-stu-id="3b9d8-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="3b9d8-291">Hello 租用集合順序 toouse hello 變更摘要處理器文件庫，必須 toobe 建立之前執行 hello 處理器的主機。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="3b9d8-292">同樣地，我們建議將租用集合儲存在不同的帳戶以寫入區域更接近 toowhere hello 變更摘要處理器正在執行。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="3b9d8-293">資料移動在本例中，我們需要 toocreate hello 目的集合，然後再執行 hello 變更摘要處理器的主機。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="3b9d8-294">在 hello 範例程式碼中，我們稱監視，協助程式方法 toocreate hello 租用，和如果它們尚不存在的目的集合。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="3b9d8-295">建立集合的定價顧慮，為您保留 Azure Cosmos db hello 應用程式 toocommunicate 的輸送量。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="3b9d8-296">如需詳細資訊，請瀏覽 hello[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="3b9d8-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="3b9d8-297">建立處理器主機</span><span class="sxs-lookup"><span data-stu-id="3b9d8-297">*Creating a processor host*</span></span>

<span data-ttu-id="3b9d8-298">hello`ChangeFeedProcessorHost`類別會提供安全執行緒、 多處理序、 安全的執行階段環境來實作事件處理器，也提供檢查點檢查與資料分割租用管理。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="3b9d8-299">toouse hello`ChangeFeedProcessorHost`類別時，您可以實作`IChangeFeedObserver`。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="3b9d8-300">這個介面包含三個方法：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-300">This interface contains three methods:</span></span>

* <span data-ttu-id="3b9d8-301">`OpenAsync`：當變更摘要觀察者開啟時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="3b9d8-302">取用者/觀察者開啟時，它可以是修改的 tooperform 特定動作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="3b9d8-303">`CloseAsync`：當變更摘要觀察者終止時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="3b9d8-304">取用者/觀察者關閉時，它可以是修改的 tooperform 特定動作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="3b9d8-305">`ProcessChangesAsync`：當變更摘要有新的文件變更時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="3b9d8-306">它可以是修改的 tooperform 每個摘要的變更更新時的特定動作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="3b9d8-307">在本例中，我們會實作 hello 介面`IChangeFeedObserver`透過 hello`DocumentFeedObserver`類別。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="3b9d8-308">在這裡，hello`ProcessChangesAsync`函式從變更的文件送入 hello 目的地集合 upserts （更新）。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="3b9d8-309">這個範例可用於將資料從一個集合 tooanother 中順序 toochange hello 資料分割索引鍵的資料集。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="3b9d8-310">*執行 hello 處理器主機*</span><span class="sxs-lookup"><span data-stu-id="3b9d8-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="3b9d8-311">在開始事件的處理之前，您可以自訂變更摘要選項和變更摘要主機選項。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="3b9d8-312">在 hello 下表摘要說明 hello 可自訂的特定欄位。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="3b9d8-313">**變更摘要選項**：</span><span class="sxs-lookup"><span data-stu-id="3b9d8-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="3b9d8-314">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="3b9d8-314">Property Name</span></span></th>
        <th><span data-ttu-id="3b9d8-315">說明</span><span class="sxs-lookup"><span data-stu-id="3b9d8-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="3b9d8-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="3b9d8-317">取得或設定 hello hello Azure Cosmos DB 資料庫服務中的 hello 列舉作業傳回的項目 toobe 數目上限。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="3b9d8-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="3b9d8-319">取得或設定在 hello Azure Cosmos DB 資料庫服務的 hello hello 目前要求的資料分割索引鍵範圍識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="3b9d8-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="3b9d8-321">取得或設定在 hello Azure Cosmos DB 資料庫服務的 hello 要求接續 token。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="3b9d8-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="3b9d8-322">SessionToken</span></span></td>
        <td><span data-ttu-id="3b9d8-323">取得或設定與 hello Azure Cosmos DB 資料庫服務的工作階段一致性 hello 工作階段語彙基元供使用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="3b9d8-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="3b9d8-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="3b9d8-325">取得或設定是否從 hello 開頭 (true) 或目前 (false)，應該啟動摘要 hello Azure Cosmos DB 資料庫服務中的變更。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="3b9d8-326">根據預設，它會從目前位置 (false) 來開始。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="3b9d8-327">**變更摘要主機選項**:</span><span class="sxs-lookup"><span data-stu-id="3b9d8-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="3b9d8-328">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="3b9d8-328">Property Name</span></span></th>
        <th><span data-ttu-id="3b9d8-329">類型</span><span class="sxs-lookup"><span data-stu-id="3b9d8-329">Type</span></span></th>
        <th><span data-ttu-id="3b9d8-330">說明</span><span class="sxs-lookup"><span data-stu-id="3b9d8-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="3b9d8-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="3b9d8-332">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b9d8-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="3b9d8-333">hello 的間隔時間的所有租用目前 hello ChangeFeedEventHost 執行個體所持有的資料分割。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="3b9d8-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="3b9d8-335">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b9d8-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="3b9d8-336">資料分割，平均分散在已知的主控件執行個體是否 hello 間隔 tookick 工作 toocompute 關閉。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="3b9d8-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="3b9d8-338">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b9d8-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="3b9d8-339">代表資料分割在租用期租用會執行哪些 hello 的 hello 間隔。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="3b9d8-340">在此時間間隔內未更新 hello 租用後，如果它已過期，而且 hello 分割區的擁有權移 tooanother ChangeFeedEventHost 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="3b9d8-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="3b9d8-342">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b9d8-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="3b9d8-343">之後即會清空所有目前的變更摘要 hello 輪詢 hello 上的新變更的資料分割之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="3b9d8-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="3b9d8-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="3b9d8-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="3b9d8-346">hello 頻率 toocheckpoint 租用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="3b9d8-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="3b9d8-348">int</span><span class="sxs-lookup"><span data-stu-id="3b9d8-348">Int</span></span></td>
        <td><span data-ttu-id="3b9d8-349">hello hello 主機的最小分割區計數。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="3b9d8-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="3b9d8-351">int</span><span class="sxs-lookup"><span data-stu-id="3b9d8-351">Int</span></span></td>
        <td><span data-ttu-id="3b9d8-352">可以做 hello 分割 hello 主機的數目上限。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3b9d8-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="3b9d8-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="3b9d8-354">Bool</span><span class="sxs-lookup"><span data-stu-id="3b9d8-354">Bool</span></span></td>
        <td><span data-ttu-id="3b9d8-355">應該刪除是否 hello 上啟動 hello 主機的所有現有的租用和 hello 主機應該從頭開始。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="3b9d8-356">toostart 事件處理，具現化`ChangeFeedProcessorHost`，提供 Azure Cosmos DB 集合中的 hello 適當的參數。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="3b9d8-357">然後，呼叫`RegisterObserverAsync`tooregister 您`IChangeFeedObserver`hello 執行階段 (在此範例中 DocumentFeedObserver) 實作。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="3b9d8-358">此時，hello 主機嘗試 tooacquire 使用 「 窮盡 」 演算法 hello Azure Cosmos DB 集合中每個資料分割索引鍵範圍上的租用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="3b9d8-359">這些租用會延續一段指定時間，然後必須更新。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="3b9d8-360">為新的節點，背景工作執行個體，在此情況下，上線，它們會預訂租約，並且經過一段時間 hello 負載會轉移節點之間為每一部主機嘗試次數 tooacquire 更多租用。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="3b9d8-361">在 hello 範例程式碼，我們使用處理站類別 (DocumentFeedObserverFactory.cs) toocreate 觀察者和 hello `RegistObserverFactoryAsync` tooregister hello 觀察者。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="3b9d8-362">經過一段時間後，均衡的局面將會出現。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="3b9d8-363">此動態功能可讓 CPU 型自動調整套用 toobe tooconsumers 向上延展和向下調整。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="3b9d8-364">變更有更快的速度比處理取用者可以提供 Azure Cosmos DB，取用者上的 hello CPU 增加可以使用的 toocause 自動調整規模上背景工作執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b9d8-365">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b9d8-365">Next steps</span></span>
* <span data-ttu-id="3b9d8-366">再試一次 hello [Azure Cosmos 資料庫變更摘要 GitHub 上的程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="3b9d8-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="3b9d8-367">開始撰寫程式碼以 hello [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)或 hello [REST API](/rest/api/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="3b9d8-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
