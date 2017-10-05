---
title: "使用 Azure Cosmos DB 中的變更摘要支援 | Microsoft Docs"
description: "使用 Azure Cosmos DB 的變更摘要支援來追蹤文件中的變更，並執行以事件為基礎的處理 (例如觸發程序)，以及讓快取和分析系統保持最新狀態。"
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
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="836a6-104">使用 Azure Cosmos DB 中的變更摘要支援</span><span class="sxs-lookup"><span data-stu-id="836a6-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="836a6-105">[Azure Cosmos DB](../cosmos-db/introduction.md) 是一項快速且有彈性的全域複製資料庫服務，可用來儲存大量的交易式和操作資料，且具有可預測的讀取和寫入個位數毫秒延遲。</span><span class="sxs-lookup"><span data-stu-id="836a6-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="836a6-106">這使得它適合用於 IoT、遊戲、零售，以及操作記錄應用程式。</span><span class="sxs-lookup"><span data-stu-id="836a6-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="836a6-107">這些應用程式中的一個常見設計模式是，追蹤對 Azure Cosmos DB 資料所做的變更，並根據這些變更來更新具體化檢視、執行即時分析、將資料封存到冷儲存體，以及在特定事件上觸發通知。</span><span class="sxs-lookup"><span data-stu-id="836a6-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="836a6-108">Azure Cosmos DB 中的**變更摘要支援**允許您針對每一個模式建置有效率且可調整的解決方案。</span><span class="sxs-lookup"><span data-stu-id="836a6-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="836a6-109">透過變更摘要支援，Azure Cosmos DB 提供一份 Azure Cosmos DB 集合內的文件排序清單，並以文件的修改順序做出排序。</span><span class="sxs-lookup"><span data-stu-id="836a6-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="836a6-110">此摘要可用來接聽集合內的資料修改，並執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="836a6-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="836a6-111">於插入或修改文件時觸發 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="836a6-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="836a6-112">執行即時 (串流) 更新處理</span><span class="sxs-lookup"><span data-stu-id="836a6-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="836a6-113">與快取、搜尋引擎或資料倉儲進行資料同步處理</span><span class="sxs-lookup"><span data-stu-id="836a6-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="836a6-114">Azure Cosmos DB 中的變更會加以保存，且可進行非同步處理，並分散到一或多個取用者以進行平行處理。</span><span class="sxs-lookup"><span data-stu-id="836a6-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="836a6-115">讓我們看看適用於變更摘要的 API，以及您如何使用它們來建置可調整的即時應用程式。</span><span class="sxs-lookup"><span data-stu-id="836a6-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="836a6-116">本文示範如何使用 Azure Cosmos DB 變更摘要和 DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="836a6-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![使用 Azure Cosmos DB 變更摘要來提供即時分析和事件導向的計算案例](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="836a6-118">目前，我們只針對 DocumentDB API 提供變更摘要支援。圖形 API 和資料表 API 尚未獲得支援。</span><span class="sxs-lookup"><span data-stu-id="836a6-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="836a6-119">使用個案和案例</span><span class="sxs-lookup"><span data-stu-id="836a6-119">Use cases and scenarios</span></span>
<span data-ttu-id="836a6-120">變更摘要允許透過大量寫入來有效處理大型資料集，並提供查詢整個資料集以識別已變更之項目的替代方式。</span><span class="sxs-lookup"><span data-stu-id="836a6-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="836a6-121">例如，您可以有效率地執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="836a6-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="836a6-122">透過儲存在 Azure Cosmos DB 中的資料，來更新快取、搜尋索引或資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="836a6-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="836a6-123">實作應用程式層級的資料階層處理和封存，也就是在 Azure Cosmos DB 中儲存「熱資料」，並將「冷資料」淘汰到 [Azure Blob 儲存體](../storage/common/storage-introduction.md)或 [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="836a6-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="836a6-124">使用 [Apache Hadoop](run-hadoop-with-hdinsight.md) 在資料上實作批次分析。</span><span class="sxs-lookup"><span data-stu-id="836a6-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="836a6-125">透過 Azure Cosmos DB [在 Azure 上實作 Lambda 管線 (英文)](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="836a6-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="836a6-126">Azure Cosmos DB 提供一個可調整的資料庫解決方案，可以處理擷取和查詢，並實作具有低 TCO 的 Lambda 架構。</span><span class="sxs-lookup"><span data-stu-id="836a6-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="836a6-127">透過不同的分割配置，執行零停機時間移轉至另一個 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="836a6-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="836a6-128">**搭配 Azure Cosmos DB 使用 Lambda 管線進行擷取和查詢：**</span><span class="sxs-lookup"><span data-stu-id="836a6-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![適用於擷取和查詢的 Azure Cosmos DB 型 Lambda 管線](./media/change-feed/lambda.png)

<span data-ttu-id="836a6-130">您可以使用 Azure Cosmos DB 來接收與儲存來自裝置、感應器、基礎結構和應用程式的事件資料，並透過 [Azure 串流分析](../stream-analytics/stream-analytics-documentdb-output.md)、[Apache Storm](../hdinsight/hdinsight-storm-overview.md) 或 [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md) 即時處理這些事件。</span><span class="sxs-lookup"><span data-stu-id="836a6-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="836a6-131">在您的 [serverless](http://azure.com/serverless) Web 和行動應用程式內，您可以追蹤例如變更客戶設定檔、喜好設定或位置等的事件，以觸發像是使用 [Azure Functions](../azure-functions/functions-bindings-documentdb.md) 或[應用程式服務](https://azure.microsoft.com/services/app-service/)傳送推播通知到客戶裝置的特定動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="836a6-132">例如，如果您使用 Azure Cosmos DB 來建置遊戲，就可以根據完成遊戲的分數，使用變更摘要來實作即時排行榜。</span><span class="sxs-lookup"><span data-stu-id="836a6-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="836a6-133">變更摘要在 Azure Cosmos DB 中的運作方式</span><span class="sxs-lookup"><span data-stu-id="836a6-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="836a6-134">Azure Cosmos DB 提供以累加方式讀取對 Azure Cosmos DB 集合做出之更新的功能。</span><span class="sxs-lookup"><span data-stu-id="836a6-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="836a6-135">此變更摘要具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="836a6-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="836a6-136">變更會在 Azure Cosmos DB 中持續保存，並且可以非同步處理。</span><span class="sxs-lookup"><span data-stu-id="836a6-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="836a6-137">集合內的文件變更會立即在變更摘要中提供。</span><span class="sxs-lookup"><span data-stu-id="836a6-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="836a6-138">對文件所做的每項變更皆會在變更摘要中出現一次，且用戶端會管理其檢查點邏輯。</span><span class="sxs-lookup"><span data-stu-id="836a6-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="836a6-139">變更摘要的處理器程式庫提供自動檢查點和「至少一次」語意。</span><span class="sxs-lookup"><span data-stu-id="836a6-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="836a6-140">變更記錄檔中只會包含指定文件的最新變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="836a6-141">中繼變更可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="836a6-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="836a6-142">變更摘要會依照各個資料分割索引鍵值內的修改順序排序。</span><span class="sxs-lookup"><span data-stu-id="836a6-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="836a6-143">跨資料分割索引鍵值順序不會是固定的。</span><span class="sxs-lookup"><span data-stu-id="836a6-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="836a6-144">變更可以從任何時間點同步處理，也就是說，可用變更沒有固定的資料保留期限。</span><span class="sxs-lookup"><span data-stu-id="836a6-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="836a6-145">變更會以資料分割索引鍵區塊為單位提供。</span><span class="sxs-lookup"><span data-stu-id="836a6-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="836a6-146">這項功能可讓大型集合的變更由多個取用者/伺服器平行處理。</span><span class="sxs-lookup"><span data-stu-id="836a6-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="836a6-147">應用程式可以在同一個集合上同時要求多個變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="836a6-148">根據預設，所有帳戶都會啟用 Azure Cosmos DB 的變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="836a6-149">就像是 Azure Cosmos DB 的任何其他作業，您可以在寫入區域或任何[讀取區域](distribute-data-globally.md)中使用[佈建輸送量](request-units.md)來讀取變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="836a6-150">變更摘要包含對集合內文件進行的插入與更新作業。</span><span class="sxs-lookup"><span data-stu-id="836a6-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="836a6-151">您可以擷取刪除項目，方法是在您的文件內設定「虛刪除」旗標來取代刪除動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="836a6-152">或者，您可以透過 [TTL 功能](time-to-live.md)針對您的文件設定有限的逾期期限 (例如 24 小時)，並使用該屬性的值擷取刪除項目。</span><span class="sxs-lookup"><span data-stu-id="836a6-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="836a6-153">使用此解決方案，您必須在比 TTL 逾期期限更短的時間間隔內處理變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="836a6-154">文件集合內每個資料分割索引鍵範圍都可使用變更摘要，因此可以分散到一或多個取用者以進行平行處理。</span><span class="sxs-lookup"><span data-stu-id="836a6-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB 變更摘要的分散式處理](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="836a6-156">關於如何在用戶端程式碼中實作變更摘要，我們提供了幾個選項給您。</span><span class="sxs-lookup"><span data-stu-id="836a6-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="836a6-157">接下來的幾節會說明如何使用 Azure Cosmos DB REST API 和 DocumentDB SDK 來實作變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="836a6-158">不過，如果您使用 .NET 應用程式，則建議您使用新的[變更摘要處理器程式庫](#change-feed-processor)來處理變更摘要所傳來的事件，因為該程式庫可簡化分割區變更的讀取作業，並讓多個執行緒平行運作。</span><span class="sxs-lookup"><span data-stu-id="836a6-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="836a6-159"><a id="rest-apis"></a>使用 REST API 和 DocumentDB SDK</span><span class="sxs-lookup"><span data-stu-id="836a6-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="836a6-160">Azure Cosmos DB 提供彈性的儲存體及輸送量容器，稱為**集合**。</span><span class="sxs-lookup"><span data-stu-id="836a6-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="836a6-161">集合內的資料會針對延展性和效能，使用[資料分割索引鍵](partition-data.md)以邏輯方式分組。</span><span class="sxs-lookup"><span data-stu-id="836a6-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="836a6-162">Azure Cosmos DB 提供各種用來存取此資料的 API，包括依識別碼查閱 (Read/Get)、查詢及讀取摘要 (掃描)。</span><span class="sxs-lookup"><span data-stu-id="836a6-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="836a6-163">變更摘要可以透過將兩個新的要求標頭填入至 DocumentDB 的 `ReadDocumentFeed` API 來取得，並且可以跨分割區索引鍵的範圍來平行處理。</span><span class="sxs-lookup"><span data-stu-id="836a6-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="836a6-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="836a6-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="836a6-165">讓我們快速看一下 ReadDocumentFeed 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="836a6-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="836a6-166">Azure Cosmos DB 支援透過 `ReadDocumentFeed` API 讀取集合內文件的摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="836a6-167">例如，下列要求會傳回 `serverlogs` 集合內文件的頁面。</span><span class="sxs-lookup"><span data-stu-id="836a6-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="836a6-168">可以使用 `x-ms-max-item-count` 標頭限制結果，且可以透過重新提交要求 (包含先前回應中傳回的 `x-ms-continuation` 標頭) 繼續先前的讀取。</span><span class="sxs-lookup"><span data-stu-id="836a6-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="836a6-169">當從單一用戶端執行時，`ReadDocumentFeed` 會以序列方式逐一查看資料分割之間的結果。</span><span class="sxs-lookup"><span data-stu-id="836a6-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="836a6-170">**序列讀取文件摘要**</span><span class="sxs-lookup"><span data-stu-id="836a6-170">**Serial read document feed**</span></span>

<span data-ttu-id="836a6-171">您也可以使用其中一個支援的 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 來擷取文件摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="836a6-172">例如，下列程式碼片段會示範如何在 .NET 中使用 [ReadDocumentFeedAsync 方法](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="836a6-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="836a6-173">ReadDocumentFeed 的分散式執行</span><span class="sxs-lookup"><span data-stu-id="836a6-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="836a6-174">針對包含數 TB 以上資料或需內嵌大量更新的集合，序列執行單一用戶端電腦的讀取摘要可能不夠實際。</span><span class="sxs-lookup"><span data-stu-id="836a6-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="836a6-175">為了支援這些巨量資料案例，Azure Cosmos DB 提供在多個用戶端讀取者/取用者之間明確分散 `ReadDocumentFeed` 呼叫的 API。</span><span class="sxs-lookup"><span data-stu-id="836a6-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="836a6-176">**分散式讀取文件摘要**</span><span class="sxs-lookup"><span data-stu-id="836a6-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="836a6-177">若要提供可調整的累加式變更處理，Azure Cosmos DB 會根據分割區索引鍵的範圍，支援變更摘要 API 的向外延展模型。</span><span class="sxs-lookup"><span data-stu-id="836a6-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="836a6-178">您可以針對執行 `ReadPartitionKeyRanges` 呼叫的集合取得資料分割索引鍵範圍的清單。</span><span class="sxs-lookup"><span data-stu-id="836a6-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="836a6-179">針對每個資料分割索引鍵範圍，您可以執行 `ReadDocumentFeed` 來讀取該範圍內資料分割索引鍵的文件。</span><span class="sxs-lookup"><span data-stu-id="836a6-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="836a6-180">擷取集合的資料分割索引鍵範圍</span><span class="sxs-lookup"><span data-stu-id="836a6-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="836a6-181">您可以藉由要求集合內的 `pkranges` 資源來擷取資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="836a6-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="836a6-182">例如，下列要求會擷取 `serverlogs` 集合的資料分割索引鍵範圍清單：</span><span class="sxs-lookup"><span data-stu-id="836a6-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="836a6-183">此要求會傳回下列包含資料分割索引鍵範圍相關中繼資料的回應：</span><span class="sxs-lookup"><span data-stu-id="836a6-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

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


<span data-ttu-id="836a6-184">**資料分割索引鍵範圍屬性**：每個資料分割索引鍵範圍包含下表中的中繼資料屬性︰</span><span class="sxs-lookup"><span data-stu-id="836a6-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="836a6-185">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="836a6-185">Header name</span></span></th>
        <th><span data-ttu-id="836a6-186">說明</span><span class="sxs-lookup"><span data-stu-id="836a6-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-187">id</span><span class="sxs-lookup"><span data-stu-id="836a6-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="836a6-188">資料分割索引鍵範圍的識別碼。</span><span class="sxs-lookup"><span data-stu-id="836a6-188">The ID for the partition key range.</span></span> <span data-ttu-id="836a6-189">這是每個集合內穩定且唯的一識別碼。</span><span class="sxs-lookup"><span data-stu-id="836a6-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="836a6-190">必須在下列呼叫中使用，以依據資料分割索引鍵範圍讀取變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="836a6-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="836a6-192">資料分割索引鍵範圍的最大資料分割索引鍵雜湊值。</span><span class="sxs-lookup"><span data-stu-id="836a6-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="836a6-193">供內部使用。</span><span class="sxs-lookup"><span data-stu-id="836a6-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="836a6-194">minInclusive</span></span></td>
        <td><span data-ttu-id="836a6-195">資料分割索引鍵範圍的最小資料分割索引鍵雜湊值。</span><span class="sxs-lookup"><span data-stu-id="836a6-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="836a6-196">供內部使用。</span><span class="sxs-lookup"><span data-stu-id="836a6-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="836a6-197">您可以使用其中一個支援的 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="836a6-198">例如，下列程式碼片段示範如何在 .NET 中使用 [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) 方法來擷取分割區索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="836a6-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="836a6-199">Azure Cosmos DB 支援針對每個分割區索引鍵範圍進行文件擷取，方法是設定選擇性的 `x-ms-documentdb-partitionkeyrangeid` 標頭。</span><span class="sxs-lookup"><span data-stu-id="836a6-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="836a6-200">執行累加式 ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="836a6-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="836a6-201">ReadDocumentFeed 支援下列在 Azure Cosmos DB 集合中進行累加式變更處理的案例/工作：</span><span class="sxs-lookup"><span data-stu-id="836a6-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="836a6-202">從開始 (也就是集合建立開始) 讀取所有文件變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="836a6-203">從目前時間讀取包含未來更新的所有文件變更，或自從使用者指定時間以來的任何變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="836a6-204">從集合邏輯版本 (ETag) 讀取所有文件變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="836a6-205">您可以根據從累加式讀取摘要要求傳回的 ETag，將您的取用者設為檢查點。</span><span class="sxs-lookup"><span data-stu-id="836a6-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="836a6-206">變更包含對文件進行的插入和更新。</span><span class="sxs-lookup"><span data-stu-id="836a6-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="836a6-207">若要擷取刪除項目，您必須在您的文件內使用「虛刪除」屬性，或使用[內建 TTL 屬性](time-to-live.md)在變更摘要中指示暫止刪除。</span><span class="sxs-lookup"><span data-stu-id="836a6-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="836a6-208">下表列出 ReadDocumentFeed 作業的[要求](/rest/api/documentdb/common-documentdb-rest-request-headers.md)和[回應標頭](/rest/api/documentdb/common-documentdb-rest-response-headers.md)。</span><span class="sxs-lookup"><span data-stu-id="836a6-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="836a6-209">**累加式 ReadDocumentFeed 的要求標頭**：</span><span class="sxs-lookup"><span data-stu-id="836a6-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="836a6-210">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="836a6-210">Header name</span></span></th>
        <th><span data-ttu-id="836a6-211">說明</span><span class="sxs-lookup"><span data-stu-id="836a6-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="836a6-212">A-IM</span></span></td>
        <td><span data-ttu-id="836a6-213">必須設定為「累加式摘要」或省略</span><span class="sxs-lookup"><span data-stu-id="836a6-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="836a6-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="836a6-215">No header：傳回從一開始 (集合建立) 的所有變更</span><span class="sxs-lookup"><span data-stu-id="836a6-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="836a6-216">"*"：傳回集合內資料的所有新變更</span><span class="sxs-lookup"><span data-stu-id="836a6-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="836a6-217">&lt;etag&gt;：如果設定為集合 ETag，則傳回邏輯時間戳記之後所做的所有變更</span><span class="sxs-lookup"><span data-stu-id="836a6-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="836a6-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="836a6-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="836a6-219">RFC 1123 時間格式；如果已指定 If-None-Match，則忽略</span><span class="sxs-lookup"><span data-stu-id="836a6-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="836a6-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="836a6-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="836a6-221">用來讀取資料的資料分割索引鍵範圍識別碼。</span><span class="sxs-lookup"><span data-stu-id="836a6-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="836a6-222">**累加式 ReadDocumentFeed 的回應標頭**：</span><span class="sxs-lookup"><span data-stu-id="836a6-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="836a6-223">標頭名稱</span><span class="sxs-lookup"><span data-stu-id="836a6-223">Header name</span></span></th>
        <th><span data-ttu-id="836a6-224">說明</span><span class="sxs-lookup"><span data-stu-id="836a6-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-225">etag</span><span class="sxs-lookup"><span data-stu-id="836a6-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="836a6-226">回應中最後傳回文件的邏輯序號 (LSN)。</span><span class="sxs-lookup"><span data-stu-id="836a6-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="836a6-227">透過在 If-None-Match 中重新提交此值，可以繼續執行累加式 ReadDocumentFeed。</span><span class="sxs-lookup"><span data-stu-id="836a6-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="836a6-228">以下是從邏輯版本/ETag `28535`和資料分割索引鍵範圍 = `16` 傳回集合中所有累加變更的範例要求：</span><span class="sxs-lookup"><span data-stu-id="836a6-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="836a6-229">變更會依照資料分割索引鍵範圍內每個資料分割索引鍵值內的時間加以排序。</span><span class="sxs-lookup"><span data-stu-id="836a6-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="836a6-230">跨資料分割索引鍵值順序不會是固定的。</span><span class="sxs-lookup"><span data-stu-id="836a6-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="836a6-231">如果結果無法容納於單一頁面，您可以透過重新提交包含 `If-None-Match` 標頭的要求，以及和上一個回應中的 `etag` 相同的值，來讀取下一頁的結果。</span><span class="sxs-lookup"><span data-stu-id="836a6-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="836a6-232">如果多個文件已在預存程序或觸發程序內以交易式方式插入或更新，則文件會在相同的回應頁面中傳回。</span><span class="sxs-lookup"><span data-stu-id="836a6-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="836a6-233">使用變更摘要時，若在預存程序或觸發程序內插入或更新多份文件，您在頁面中取得的傳回項目可能會比 `x-ms-max-item-count` 中指定的項目更多。</span><span class="sxs-lookup"><span data-stu-id="836a6-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="836a6-234">使用 .NET SDK (1.17.0) 時，在 `ChangeFeedOptions` 中設定欄位 `StartTime`，以在呼叫 `CreateDocumentChangeFeedQuery` 時，直接傳回自 `StartTime` 以來的變更文件。</span><span class="sxs-lookup"><span data-stu-id="836a6-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="836a6-235">藉由使用 REST API 指定 `If-Modified-Since`，您的要求並不會傳回文件本身，而會傳回接續權杖或回應標頭中的 `etag`。</span><span class="sxs-lookup"><span data-stu-id="836a6-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="836a6-236">若要傳回修改指定時間的文件，接續權杖 `etag` 必須在下一個要求中與 `If-None-Match` 搭配使用，以傳回實際文件。</span><span class="sxs-lookup"><span data-stu-id="836a6-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="836a6-237">.NET SDK 提供 [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) 和 [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) 協助程式類別來存取對集合所做的變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="836a6-238">下列程式碼片段示範如何使用來自單一用戶端的 .NET SDK 來擷取從一開始的所有變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

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
<span data-ttu-id="836a6-239">下列程式碼片段示範如何使用變更摘要支援和先前的函式，透過 Azure Cosmos DB 即時處理變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="836a6-240">第一次呼叫會傳回集合中所有的文件，而第二次呼叫只會傳回於最後一個檢查點之後建立的兩個文件。</span><span class="sxs-lookup"><span data-stu-id="836a6-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="836a6-241">您也可以使用用戶端邏輯以選擇性地處理事件，來篩選變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="836a6-242">例如，以下是使用用戶端 LINQ 處理僅來自裝置感應器之溫度變更事件的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="836a6-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="836a6-243"><a id="change-feed-processor"></a>變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="836a6-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="836a6-244">另一個選項是使用 [Azure Cosmos DB 變更摘要處理器程式庫](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)，以協助您輕鬆地將來自變更摘要的事件處理分散到多個取用者。</span><span class="sxs-lookup"><span data-stu-id="836a6-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="836a6-245">程式庫很適合用來在 .NET 平台上建置變更摘要讀取程式。</span><span class="sxs-lookup"><span data-stu-id="836a6-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="836a6-246">透過其他 Cosmos DB SDK 所含方法來使用變更摘要處理器程式庫時，所能簡化的某些工作流程包括：</span><span class="sxs-lookup"><span data-stu-id="836a6-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="836a6-247">當資料儲存在多個分割區時，提取變更摘要的更新</span><span class="sxs-lookup"><span data-stu-id="836a6-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="836a6-248">將資料從某個集合移動或複寫到另一個集合</span><span class="sxs-lookup"><span data-stu-id="836a6-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="836a6-249">平行執行因資料和變更摘要有更新所觸發的動作</span><span class="sxs-lookup"><span data-stu-id="836a6-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="836a6-250">雖然在 Cosmos SDK 中使用 API 可讓您精確地存取每個分割區中的變更摘要更新，但使用變更摘要處理器程式庫卻能簡化分割區變更的讀取作業，並讓多個執行緒平行運作。</span><span class="sxs-lookup"><span data-stu-id="836a6-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="836a6-251">您不必手動讀取每個容器的變更並儲存每個分割區的接續權杖，變更摘要處理器會自動使用租用機制來為您管理分割區變更的讀取作業。</span><span class="sxs-lookup"><span data-stu-id="836a6-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="836a6-252">此程式庫是以 NuGet 套件的形式來提供：[Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)，並可從原始程式碼取得來作為 Github [範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)。</span><span class="sxs-lookup"><span data-stu-id="836a6-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="836a6-253">了解變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="836a6-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="836a6-254">用來實作變更摘要處理器的主要元件有四個：受監視的集合、租用集合、處理器主機和取用者。</span><span class="sxs-lookup"><span data-stu-id="836a6-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="836a6-255">**受監視的集合：**受監視的集合是將會產生變更摘要的資料。</span><span class="sxs-lookup"><span data-stu-id="836a6-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="836a6-256">對於受監視集合所進行的任何插入和變更都會反映在集合的變更摘要中。</span><span class="sxs-lookup"><span data-stu-id="836a6-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="836a6-257">**租用集合：**租用集合會協調如何處理多個背景工作角色的變更摘要。</span><span class="sxs-lookup"><span data-stu-id="836a6-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="836a6-258">另外會有一個集合用來儲存租用 (每個分割區一個租用)。</span><span class="sxs-lookup"><span data-stu-id="836a6-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="836a6-259">在不同帳戶儲存此租用集合，並讓其寫入區域更靠近變更摘要處理器的執行所在位置會有好處。</span><span class="sxs-lookup"><span data-stu-id="836a6-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="836a6-260">租用物件包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="836a6-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="836a6-261">擁有者：指定擁有租用的主機</span><span class="sxs-lookup"><span data-stu-id="836a6-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="836a6-262">接續：指定特定分割區在變更摘要中的位置 (接續權杖)</span><span class="sxs-lookup"><span data-stu-id="836a6-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="836a6-263">時間戳記：上次更新租用的時間；時間戳記可用來檢查是否將租用視為過期</span><span class="sxs-lookup"><span data-stu-id="836a6-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="836a6-264">**處理器主機：**每一部主機都會根據主機的其他執行個體中有多少個執行個體擁有作用中租用，來決定要處理的分割區數量。</span><span class="sxs-lookup"><span data-stu-id="836a6-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="836a6-265">主機在啟動時會取得租用，以平衡分配所有主機的工作負載。</span><span class="sxs-lookup"><span data-stu-id="836a6-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="836a6-266">主機會定期更新租用，以便讓租用保持作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="836a6-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="836a6-267">主機會對其每個讀取的租用設置最後一個接續權杖的檢查點。</span><span class="sxs-lookup"><span data-stu-id="836a6-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="836a6-268">為確保能夠安全地進行並行存取，主機會檢查每個租用更新的 ETag。</span><span class="sxs-lookup"><span data-stu-id="836a6-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="836a6-269">主機也支援其他檢查點策略。</span><span class="sxs-lookup"><span data-stu-id="836a6-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="836a6-270">關機後，主機會將所有租用釋出，但會保留接續資訊，以便之後能夠繼續讀取預存的檢查點。</span><span class="sxs-lookup"><span data-stu-id="836a6-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="836a6-271">目前，主機數目不能大於分割區 (租用) 數目。</span><span class="sxs-lookup"><span data-stu-id="836a6-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="836a6-272">**取用者：**取用者 (或背景工作角色) 是負責執行每個主機所起始之變更摘要處理活動的執行緒。</span><span class="sxs-lookup"><span data-stu-id="836a6-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="836a6-273">每個處理器主機都可以有多個取用者。</span><span class="sxs-lookup"><span data-stu-id="836a6-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="836a6-274">每個取用者會從其獲派到的分割區讀取變更摘要，並向其主機通知所發生的變更和已過期的租用。</span><span class="sxs-lookup"><span data-stu-id="836a6-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="836a6-275">為了進一步了解變更摘要處理器的這四個元素是如何一起運作的，我們來看一下下圖中的範例。</span><span class="sxs-lookup"><span data-stu-id="836a6-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="836a6-276">受監視的集合會儲存文件，並使用 "city" 來作為分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="836a6-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="836a6-277">我們可以看到，藍色的分割區包含 "city" 欄位為 "A 到 E" 的文件，依此類推。</span><span class="sxs-lookup"><span data-stu-id="836a6-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="836a6-278">主機有兩部，每一部都有兩個取用者從四個分割區進行平行讀取。</span><span class="sxs-lookup"><span data-stu-id="836a6-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="836a6-279">箭號顯示從變更摘要中的特定地點進行讀取的取用者。</span><span class="sxs-lookup"><span data-stu-id="836a6-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="836a6-280">在第一個分割區中，較深的藍色代表未讀取的變更，較淺的藍色則代表變更摘要上已讀取的變更。</span><span class="sxs-lookup"><span data-stu-id="836a6-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="836a6-281">主機會使用租用集合來儲存「接續」值，以追蹤每個取用者目前的讀取位置。</span><span class="sxs-lookup"><span data-stu-id="836a6-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![使用 Azure Cosmos DB 變更摘要處理器主機](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="836a6-283">使用變更摘要處理器程式庫</span><span class="sxs-lookup"><span data-stu-id="836a6-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="836a6-284">下節說明如何在將來源集合的變更複寫到目的地集合的情況下使用變更摘要處理器程式庫。</span><span class="sxs-lookup"><span data-stu-id="836a6-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="836a6-285">在這裡，來源集合是變更摘要處理器內的受監視集合。</span><span class="sxs-lookup"><span data-stu-id="836a6-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="836a6-286">**安裝和納入變更摘要處理器 NuGet 套件**</span><span class="sxs-lookup"><span data-stu-id="836a6-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="836a6-287">在安裝變更摘要處理器 NuGet 套件之前，請先安裝：</span><span class="sxs-lookup"><span data-stu-id="836a6-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="836a6-288">Microsoft.Azure.DocumentDB 1.13.1 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="836a6-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="836a6-289">Newtonsoft.Json 9.0.1 版或更新版本 安裝 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 並將它納入以作為參考。</span><span class="sxs-lookup"><span data-stu-id="836a6-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="836a6-290">**建立受監視的租用集合和目的地集合**</span><span class="sxs-lookup"><span data-stu-id="836a6-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="836a6-291">若要使用變更摘要處理器程式庫，您必須先建立租用集合再執行處理器主機。</span><span class="sxs-lookup"><span data-stu-id="836a6-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="836a6-292">我們再次地建議，請將租用集合儲存在不同帳戶，並讓其寫入區域更靠近變更摘要處理器的執行所在位置。</span><span class="sxs-lookup"><span data-stu-id="836a6-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="836a6-293">在這個資料移動範例中，我們需要先建立目的地集合再執行變更摘要處理器主機。</span><span class="sxs-lookup"><span data-stu-id="836a6-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="836a6-294">在程式碼範例中，我們會呼叫 Helper 方法來建立受監視的租用集合和目的地集合 (如果您還沒有這些集合)。</span><span class="sxs-lookup"><span data-stu-id="836a6-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="836a6-295">建立集合會牽涉到定價，因為您會將輸送量保留供應用程式與 Azure Cosmos DB 通訊使用。</span><span class="sxs-lookup"><span data-stu-id="836a6-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="836a6-296">如需詳細資訊，請瀏覽[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="836a6-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="836a6-297">建立處理器主機</span><span class="sxs-lookup"><span data-stu-id="836a6-297">*Creating a processor host*</span></span>

<span data-ttu-id="836a6-298">`ChangeFeedProcessorHost` 類別能為事件處理器實作提供安全執行緒、多處理序、安全的執行階段環境，進而提供檢查點和分割區租用管理。</span><span class="sxs-lookup"><span data-stu-id="836a6-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="836a6-299">若要使用 `ChangeFeedProcessorHost` 類別，您可以實作 `IChangeFeedObserver`。</span><span class="sxs-lookup"><span data-stu-id="836a6-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="836a6-300">這個介面包含三個方法：</span><span class="sxs-lookup"><span data-stu-id="836a6-300">This interface contains three methods:</span></span>

* <span data-ttu-id="836a6-301">`OpenAsync`：當變更摘要觀察者開啟時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="836a6-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="836a6-302">您可以修改這個函式，以在取用者/觀察者開啟時執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="836a6-303">`CloseAsync`：當變更摘要觀察者終止時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="836a6-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="836a6-304">您可以修改這個函式，以在取用者/觀察者關閉時執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="836a6-305">`ProcessChangesAsync`：當變更摘要有新的文件變更時，系統就會呼叫這個函式。</span><span class="sxs-lookup"><span data-stu-id="836a6-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="836a6-306">您可以修改這個函式，以對每個變更摘要更新執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="836a6-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="836a6-307">在我們的範例中，我們會透過 `DocumentFeedObserver` 類別實作 `IChangeFeedObserver` 介面。</span><span class="sxs-lookup"><span data-stu-id="836a6-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="836a6-308">在這裡，`ProcessChangesAsync` 函式會將文件從變更摘要中更新插入 (更新) 到目的地集合。</span><span class="sxs-lookup"><span data-stu-id="836a6-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="836a6-309">這個範例可用於將資料從某個集合移到另一個集合，以變更資料集的分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="836a6-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="836a6-310">執行處理器主機</span><span class="sxs-lookup"><span data-stu-id="836a6-310">*Running the Processor Host*</span></span>

<span data-ttu-id="836a6-311">在開始事件的處理之前，您可以自訂變更摘要選項和變更摘要主機選項。</span><span class="sxs-lookup"><span data-stu-id="836a6-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="836a6-312">下表摘要說明可自訂的特定欄位。</span><span class="sxs-lookup"><span data-stu-id="836a6-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="836a6-313">**變更摘要選項**：</span><span class="sxs-lookup"><span data-stu-id="836a6-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="836a6-314">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="836a6-314">Property Name</span></span></th>
        <th><span data-ttu-id="836a6-315">說明</span><span class="sxs-lookup"><span data-stu-id="836a6-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="836a6-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="836a6-317">取得或設定要在 Azure Cosmos DB 資料庫服務中的列舉作業傳回的項目數上限。</span><span class="sxs-lookup"><span data-stu-id="836a6-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="836a6-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="836a6-319">取得或設定 Azure Cosmos DB 資料庫服務中目前要求的分割區索引鍵範圍識別碼。</span><span class="sxs-lookup"><span data-stu-id="836a6-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="836a6-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="836a6-321">取得或設定 Azure Cosmos DB 資料庫服務中的要求接續權杖。</span><span class="sxs-lookup"><span data-stu-id="836a6-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="836a6-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="836a6-322">SessionToken</span></span></td>
        <td><span data-ttu-id="836a6-323">取得或設定要在 Azure Cosmos DB 資料庫服務中用於工作階段一致性的工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="836a6-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="836a6-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="836a6-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="836a6-325">取得或設定 Azure Cosmos DB 資料庫服務中的變更摘要應該從開頭 (true) 或目前位置 (false) 來開始。</span><span class="sxs-lookup"><span data-stu-id="836a6-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="836a6-326">根據預設，它會從目前位置 (false) 來開始。</span><span class="sxs-lookup"><span data-stu-id="836a6-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="836a6-327">**變更摘要主機選項**:</span><span class="sxs-lookup"><span data-stu-id="836a6-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="836a6-328">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="836a6-328">Property Name</span></span></th>
        <th><span data-ttu-id="836a6-329">類型</span><span class="sxs-lookup"><span data-stu-id="836a6-329">Type</span></span></th>
        <th><span data-ttu-id="836a6-330">說明</span><span class="sxs-lookup"><span data-stu-id="836a6-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="836a6-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="836a6-332">時間範圍</span><span class="sxs-lookup"><span data-stu-id="836a6-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="836a6-333">目前由 ChangeFeedEventHost 執行個體所持有之分割區的所有租用間隔。</span><span class="sxs-lookup"><span data-stu-id="836a6-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="836a6-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="836a6-335">時間範圍</span><span class="sxs-lookup"><span data-stu-id="836a6-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="836a6-336">工作的啟動間隔，這些工作可用來計算分割區是否有平均地分散到已知的主機執行個體。</span><span class="sxs-lookup"><span data-stu-id="836a6-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="836a6-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="836a6-338">時間範圍</span><span class="sxs-lookup"><span data-stu-id="836a6-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="836a6-339">租用花在代表分割區之租用的間隔。</span><span class="sxs-lookup"><span data-stu-id="836a6-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="836a6-340">未在此間隔內更新的租用將會過期，而且分割區的擁有權會移轉給另一個 ChangeFeedEventHost 執行個體。</span><span class="sxs-lookup"><span data-stu-id="836a6-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="836a6-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="836a6-342">時間範圍</span><span class="sxs-lookup"><span data-stu-id="836a6-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="836a6-343">在目前所有的變更都清空後，每次輪詢分割區以了解摘要上是否有新變更時所要延遲的時間。</span><span class="sxs-lookup"><span data-stu-id="836a6-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="836a6-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="836a6-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="836a6-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="836a6-346">要對租用設置檢查點的頻率。</span><span class="sxs-lookup"><span data-stu-id="836a6-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="836a6-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="836a6-348">int</span><span class="sxs-lookup"><span data-stu-id="836a6-348">Int</span></span></td>
        <td><span data-ttu-id="836a6-349">主機的分割區計數下限。</span><span class="sxs-lookup"><span data-stu-id="836a6-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="836a6-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="836a6-351">int</span><span class="sxs-lookup"><span data-stu-id="836a6-351">Int</span></span></td>
        <td><span data-ttu-id="836a6-352">主機可以提供的分割區數目上限。</span><span class="sxs-lookup"><span data-stu-id="836a6-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="836a6-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="836a6-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="836a6-354">Bool</span><span class="sxs-lookup"><span data-stu-id="836a6-354">Bool</span></span></td>
        <td><span data-ttu-id="836a6-355">在主機啟動時，是否應該刪除所有的現有租用，以及是否要讓主機從全新狀態來開始。</span><span class="sxs-lookup"><span data-stu-id="836a6-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="836a6-356">若要啟動事件處理，請具現化 `ChangeFeedProcessorHost`，並為 Azure Cosmos DB 集合提供適當的參數。</span><span class="sxs-lookup"><span data-stu-id="836a6-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="836a6-357">然後，呼叫 `RegisterObserverAsync` 以在執行階段註冊您的 `IChangeFeedObserver` (在此範例中為 DocumentFeedObserver) 實作。</span><span class="sxs-lookup"><span data-stu-id="836a6-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="836a6-358">此時，主機會嘗試使用「窮盡」演算法，來取得 Azure Cosmos DB 集合內每個分割區索引鍵範圍的租用。</span><span class="sxs-lookup"><span data-stu-id="836a6-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="836a6-359">這些租用會延續一段指定時間，然後必須更新。</span><span class="sxs-lookup"><span data-stu-id="836a6-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="836a6-360">新節點 (在本案例中為背景工作角色執行個體) 在上線時會保留租用，而且隨著時間的推移，負載會隨著每個主機嘗試取得更多租用而轉移到不同節點。</span><span class="sxs-lookup"><span data-stu-id="836a6-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="836a6-361">在程式碼範例中，我們使用 Factory 類別 (DocumentFeedObserverFactory.cs) 來建立觀察者，並使用 `RegistObserverFactoryAsync` 來註冊觀察者。</span><span class="sxs-lookup"><span data-stu-id="836a6-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="836a6-362">經過一段時間後，均衡的局面將會出現。</span><span class="sxs-lookup"><span data-stu-id="836a6-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="836a6-363">此動態功能可讓您將 CPU 架構自動調整套用至消費者，以便進行向上和向下調整。</span><span class="sxs-lookup"><span data-stu-id="836a6-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="836a6-364">如果 Azure Cosmos DB 中出現可用變更的速度超出取用者的處理能力，可以使用取用者上的 CPU 提升來引發背景工作執行個體計數的自動調整。</span><span class="sxs-lookup"><span data-stu-id="836a6-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="836a6-365">後續步驟</span><span class="sxs-lookup"><span data-stu-id="836a6-365">Next steps</span></span>
* <span data-ttu-id="836a6-366">嘗試 [GitHub 上的 Azure Cosmos DB 變更摘要程式碼範例 (英文)](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="836a6-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="836a6-367">使用 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 或 [REST API](/rest/api/documentdb/) 開始撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="836a6-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
