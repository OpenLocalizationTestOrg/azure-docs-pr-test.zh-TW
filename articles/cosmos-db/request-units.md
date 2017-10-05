---
title: "要求單位和預估輸送量 - Azure Cosmos DB | Microsoft Docs"
description: "了解如何在 Azure Cosmos DB 中了解、指定及預估要求單位需求。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="72749-103">Azure Cosmos DB 中的要求單位</span><span class="sxs-lookup"><span data-stu-id="72749-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="72749-104">現在可供使用︰Azure Cosmos DB [要求單位計算機 (英文)](https://www.documentdb.com/capacityplanner)。</span><span class="sxs-lookup"><span data-stu-id="72749-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="72749-105">深入了解 [預估您的輸送量需求](request-units.md#estimating-throughput-needs)。</span><span class="sxs-lookup"><span data-stu-id="72749-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![輸送量計算機][5]

## <a name="introduction"></a><span data-ttu-id="72749-107">簡介</span><span class="sxs-lookup"><span data-stu-id="72749-107">Introduction</span></span>
<span data-ttu-id="72749-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是 Microsoft 的全域分散式多模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="72749-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="72749-109">有了 Azure Cosmos DB，您就不需要租用虛擬機器、部署軟體或監視資料庫。</span><span class="sxs-lookup"><span data-stu-id="72749-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="72749-110">Microsoft 頂尖工程師會負責操作並持續監視 Azure Cosmos DB，提供世界級的可用性、效能和資料保護能力。</span><span class="sxs-lookup"><span data-stu-id="72749-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="72749-111">您可以使用選擇的 API 來存取資料，因為 [DocumentDB SQL](documentdb-sql-query.md) (文件)、MongoDB (文件)、[Azure 資料表儲存體](https://azure.microsoft.com/services/storage/tables/) (索引鍵值) 和 [Gremlin (英文)](https://tinkerpop.apache.org/gremlin.html) (圖表) 皆受到原 生支援。</span><span class="sxs-lookup"><span data-stu-id="72749-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="72749-112">Azure Cosmos DB 的貨幣是要求單位 (RU)。</span><span class="sxs-lookup"><span data-stu-id="72749-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="72749-113">使用 RU，您就不需要保留讀取、寫入容量或佈建 CPU、記憶體和 IOPS。</span><span class="sxs-lookup"><span data-stu-id="72749-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="72749-114">Azure Cosmos DB 支援數種 API 以執行各種不同的作業，從簡單地讀取及寫入，到複雜的圖表查詢等等。</span><span class="sxs-lookup"><span data-stu-id="72749-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="72749-115">因為並非所有的要求都相等，所以系統會根據處理要求所需的計算量，指派標準化的**要求單位**數量。</span><span class="sxs-lookup"><span data-stu-id="72749-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="72749-116">作業的要求單位數具決定性，您可以在 Azure Cosmos DB 中透過回應標頭追蹤任何作業所取用的要求單位數。</span><span class="sxs-lookup"><span data-stu-id="72749-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="72749-117">若要提供可預測的效能，您需要保留每秒 100 RU 的輸送量單位。</span><span class="sxs-lookup"><span data-stu-id="72749-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="72749-118">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="72749-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="72749-119">什麼是要求單位和要求費用？</span><span class="sxs-lookup"><span data-stu-id="72749-119">What are request units and request charges?</span></span>
* <span data-ttu-id="72749-120">如何指定集合的要求單位容量？</span><span class="sxs-lookup"><span data-stu-id="72749-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="72749-121">如何估計應用程式的要求單位需求？</span><span class="sxs-lookup"><span data-stu-id="72749-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="72749-122">如果超過集合的要求單位容量，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="72749-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="72749-123">由於 Azure Cosmos DB 是多模型資料庫，請務必注意我們將參考文件 API 的集合/文件、圖形 API 的圖形/節點，以及資料表 API 的資料表/實體。</span><span class="sxs-lookup"><span data-stu-id="72749-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="72749-124">我們將在本文中概述容器/項目的概念。</span><span class="sxs-lookup"><span data-stu-id="72749-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="72749-125">要求單位和要求費用</span><span class="sxs-lookup"><span data-stu-id="72749-125">Request units and request charges</span></span>
<span data-ttu-id="72749-126">Azure Cosmos DB 藉由「保留」資源以滿足應用程式的輸送量需求，來提供快速且可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="72749-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="72749-127">因為應用程式會隨著時間載入和存取模式變化，所以 Azure Cosmos DB 可讓您輕鬆地增加或減少應用程式可用的保留輸送量。</span><span class="sxs-lookup"><span data-stu-id="72749-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="72749-128">有了 Azure Cosmos DB，保留的輸送量是根據每秒處理的要求單位來指定。</span><span class="sxs-lookup"><span data-stu-id="72749-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="72749-129">您可以將要求單位想像為輸送量貨幣，因此您每秒可「保留」  保證可供應用程式使用的要求單位數量。</span><span class="sxs-lookup"><span data-stu-id="72749-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="72749-130">Azure Cosmos DB 中的每個作業 (寫入文件、執行查詢、更新文件) 都會耗用 CPU、記憶體和 IOPS。</span><span class="sxs-lookup"><span data-stu-id="72749-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="72749-131">也就是說，每個作業都會產生「要求費用」，這是以「要求單位」來表示。</span><span class="sxs-lookup"><span data-stu-id="72749-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="72749-132">了解影響要求單位費用的因素，以及您應用程式的輸送量需求，讓您能夠以最經濟實惠的方式來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="72749-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="72749-133">[查詢總管] 也是測試查詢核心的絕佳工具。</span><span class="sxs-lookup"><span data-stu-id="72749-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="72749-134">我們建議從觀看 Aravind Ramachandran 說明使用 Azure Cosmos DB 的要求單位和可預測效能的下列影片來開始。</span><span class="sxs-lookup"><span data-stu-id="72749-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="72749-135">在 Azure Cosmos DB 中指定要求單位容量</span><span class="sxs-lookup"><span data-stu-id="72749-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="72749-136">開始新的集合、資料表或圖表時，您可以指定想要保留給每秒要求單位數 (每秒 RU)。</span><span class="sxs-lookup"><span data-stu-id="72749-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="72749-137">Azure Cosmos DB 會根據佈建的輸送量，配置實體資料分割來裝載您的集合，並隨著資料成長分割/再平衡所有資料分割的資料。</span><span class="sxs-lookup"><span data-stu-id="72749-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="72749-138">在集合中佈建了 2,500 個或更多要求單位時，Azure Cosmos DB 會要求指定資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="72749-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="72749-139">此外，也需要資料分割索引鍵，才能調整未來超過 2,500 個要求單位的集合輸送量。</span><span class="sxs-lookup"><span data-stu-id="72749-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="72749-140">因此，強烈建議在建立容器時設定[資料分割索引鍵](partition-data.md) (不論初始輸送量是多少)。</span><span class="sxs-lookup"><span data-stu-id="72749-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="72749-141">因為您的資料可能必須分散於多個資料分割，所以必須挑選具有高基數 (數百個到數百萬個相異值) 的資料分割索引鍵，以便 Azure Cosmos DB 一致調整您的集合/資料表/圖表和要求。</span><span class="sxs-lookup"><span data-stu-id="72749-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="72749-142">資料分割索引鍵是一種邏輯界限，而不是實體界限。</span><span class="sxs-lookup"><span data-stu-id="72749-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="72749-143">因此，您不需要限制不同資料分割索引鍵值的數目。</span><span class="sxs-lookup"><span data-stu-id="72749-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="72749-144">事實上，最好能擁有較多不同的資料分割索引鍵值，Azure Cosmos DB 才有更多的負載平衡選項。</span><span class="sxs-lookup"><span data-stu-id="72749-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="72749-145">以下的程式碼片段使用 .NET SDK 建立包含每秒 3,000 個要求單位的集合：</span><span class="sxs-lookup"><span data-stu-id="72749-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="72749-146">Azure Cosmos DB 會在輸送量的保留模型上運作。</span><span class="sxs-lookup"><span data-stu-id="72749-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="72749-147">也就是說，您需要針對所「保留」的輸送量支付費用，而不論該輸送量中有多少數量是主動「使用」的。</span><span class="sxs-lookup"><span data-stu-id="72749-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="72749-148">當您應用程式的負載、資料及使用方式模式變更時，您可以透過 SDK 或使用 [Azure 入口網站](https://portal.azure.com)，輕鬆地相應增加和減少保留 RU 的數量。</span><span class="sxs-lookup"><span data-stu-id="72749-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="72749-149">每個集合/資料表/圖表會對應至 Azure Cosmos DB 中的 `Offer` 資源，其具有佈建輸送量的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="72749-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="72749-150">藉由查閱容器的對應 offer 資源，然後使用新的輸送量值加以更新，即可變更已配置的輸送量。</span><span class="sxs-lookup"><span data-stu-id="72749-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="72749-151">以下的程式碼片段使用 .NET SDK 將集合的輸送量變更為每秒 5,000 個要求單位：</span><span class="sxs-lookup"><span data-stu-id="72749-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="72749-152">當您變更輸送量時，不會影響容器的可用性。</span><span class="sxs-lookup"><span data-stu-id="72749-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="72749-153">新保留的輸送量通常會在套用新輸送量的數秒內於生效。</span><span class="sxs-lookup"><span data-stu-id="72749-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="72749-154">要求單位的考量</span><span class="sxs-lookup"><span data-stu-id="72749-154">Request unit considerations</span></span>
<span data-ttu-id="72749-155">在估計要保留給 Azure Cosmos DB 容器的要求單位數量時，請務必考量下列變數：</span><span class="sxs-lookup"><span data-stu-id="72749-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="72749-156">**項目大小**。</span><span class="sxs-lookup"><span data-stu-id="72749-156">**Item size**.</span></span> <span data-ttu-id="72749-157">大小增加時，也會增加讀取或寫入資料所耗用的單位。</span><span class="sxs-lookup"><span data-stu-id="72749-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="72749-158">**項目屬性計數**。</span><span class="sxs-lookup"><span data-stu-id="72749-158">**Item property count**.</span></span> <span data-ttu-id="72749-159">假設預設會編製所有屬性的索引，撰寫文件/節點/實體所耗用的單位將會隨著屬性計數增加而增加。</span><span class="sxs-lookup"><span data-stu-id="72749-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="72749-160">**資料一致性**。</span><span class="sxs-lookup"><span data-stu-id="72749-160">**Data consistency**.</span></span> <span data-ttu-id="72749-161">當使用強式或限定過期的資料一致性層級時，將會耗用額外單位來讀取項目。</span><span class="sxs-lookup"><span data-stu-id="72749-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="72749-162">**已編製索引的屬性**。</span><span class="sxs-lookup"><span data-stu-id="72749-162">**Indexed properties**.</span></span> <span data-ttu-id="72749-163">每個容器上的索引原則會判定預設要編製哪些索引的屬性。</span><span class="sxs-lookup"><span data-stu-id="72749-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="72749-164">您可以限制已編製索引的屬性數目或讓索引延遲編製，以減少要求單位的耗用量。</span><span class="sxs-lookup"><span data-stu-id="72749-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="72749-165">**編製文件索引**。</span><span class="sxs-lookup"><span data-stu-id="72749-165">**Document indexing**.</span></span> <span data-ttu-id="72749-166">依預設會自動編製每份項目的索引，如果您選擇不要編製一些項目的索引，則會耗用較少的要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="72749-167">**查詢模式**。</span><span class="sxs-lookup"><span data-stu-id="72749-167">**Query patterns**.</span></span> <span data-ttu-id="72749-168">查詢的複雜性會影響針對作業所耗用的要求單位數量。</span><span class="sxs-lookup"><span data-stu-id="72749-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="72749-169">述詞數目、述詞性質、預測、UDF 數目，以及來源資料集的大小，全都會影響查詢作業的成本。</span><span class="sxs-lookup"><span data-stu-id="72749-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="72749-170">**指令碼使用方式**。</span><span class="sxs-lookup"><span data-stu-id="72749-170">**Script usage**.</span></span>  <span data-ttu-id="72749-171">查詢、預存程序和觸發程序會根據所執行作業的複雜度來耗用要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="72749-172">開發應用程式時，請檢查要求費用標頭，進一步了解每項作業如何耗用要求單位容量。</span><span class="sxs-lookup"><span data-stu-id="72749-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="72749-173">估計輸送量需求</span><span class="sxs-lookup"><span data-stu-id="72749-173">Estimating throughput needs</span></span>
<span data-ttu-id="72749-174">要求單位是要求處理成本的標準化量值。</span><span class="sxs-lookup"><span data-stu-id="72749-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="72749-175">單一要求單位代表讀取 (透過自我連結或識別碼) 由 10 個唯一屬性值 (不包括系統屬性) 所組成的單一 1KB 項目所需的處理容量。</span><span class="sxs-lookup"><span data-stu-id="72749-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="72749-176">建立 (插入)、取代或刪除相同項目的要求將會耗用服務的更多處理，因此會耗用更多的要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="72749-177">1KB 項目 1 個要求單位的基準，會對應至項目自我連結或識別碼的簡單 GET。</span><span class="sxs-lookup"><span data-stu-id="72749-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="72749-178">例如，下表顯示要在三個不同的項目大小 (1KB、4KB 和 64KB)，以及兩個不同效能等級 (500 讀取/秒 + 100 寫入/秒和 500 讀取/秒 + 500 寫入/秒) 中佈建多少要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="72749-179">在工作階段中設定資料一致性，且索引編製原則已設定為 [無]。</span><span class="sxs-lookup"><span data-stu-id="72749-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-180"><strong>項目大小</strong></span><span class="sxs-lookup"><span data-stu-id="72749-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-181"><strong>讀取/秒</strong></span><span class="sxs-lookup"><span data-stu-id="72749-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-182"><strong>寫入/秒</strong></span><span class="sxs-lookup"><span data-stu-id="72749-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-183"><strong>要求單位</strong></span><span class="sxs-lookup"><span data-stu-id="72749-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="72749-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-185">500</span><span class="sxs-lookup"><span data-stu-id="72749-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-186">100</span><span class="sxs-lookup"><span data-stu-id="72749-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="72749-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-189">500</span><span class="sxs-lookup"><span data-stu-id="72749-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-190">500</span><span class="sxs-lookup"><span data-stu-id="72749-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="72749-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-193">500</span><span class="sxs-lookup"><span data-stu-id="72749-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-194">100</span><span class="sxs-lookup"><span data-stu-id="72749-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="72749-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-197">500</span><span class="sxs-lookup"><span data-stu-id="72749-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-198">500</span><span class="sxs-lookup"><span data-stu-id="72749-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="72749-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-201">500</span><span class="sxs-lookup"><span data-stu-id="72749-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-202">100</span><span class="sxs-lookup"><span data-stu-id="72749-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="72749-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="72749-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-205">500</span><span class="sxs-lookup"><span data-stu-id="72749-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-206">500</span><span class="sxs-lookup"><span data-stu-id="72749-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="72749-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="72749-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="72749-208">使用要求單位計算機</span><span class="sxs-lookup"><span data-stu-id="72749-208">Use the request unit calculator</span></span>
<span data-ttu-id="72749-209">若要協助客戶微調其輸送量預估，有 Web 架構 [要求單位計算機](https://www.documentdb.com/capacityplanner) 可以協助預估一般作業的要求單位需求，包括︰</span><span class="sxs-lookup"><span data-stu-id="72749-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="72749-210">項目建立 (寫入)</span><span class="sxs-lookup"><span data-stu-id="72749-210">Item creates (writes)</span></span>
* <span data-ttu-id="72749-211">項目讀取</span><span class="sxs-lookup"><span data-stu-id="72749-211">Item reads</span></span>
* <span data-ttu-id="72749-212">項目刪除</span><span class="sxs-lookup"><span data-stu-id="72749-212">Item deletes</span></span>
* <span data-ttu-id="72749-213">項目更新</span><span class="sxs-lookup"><span data-stu-id="72749-213">Item updates</span></span>

<span data-ttu-id="72749-214">此工具也支援根據您提供的範例項目預估資料儲存需求。</span><span class="sxs-lookup"><span data-stu-id="72749-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="72749-215">使用此工具很簡單︰</span><span class="sxs-lookup"><span data-stu-id="72749-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="72749-216">上傳一或多個具代表性的項目。</span><span class="sxs-lookup"><span data-stu-id="72749-216">Upload one or more representative items.</span></span>
   
    ![將項目上傳至要求單位計算機][2]
2. <span data-ttu-id="72749-218">若要預估資料儲存需求，請輸入您預期要儲存的項目總數。</span><span class="sxs-lookup"><span data-stu-id="72749-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="72749-219">輸入您需要之建立、讀取、更新和刪除作業的項目數 (以每秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="72749-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="72749-220">若要預估項目更新作業的要求單位費用，請上傳一份上述步驟 1 中包含一般欄位更新的範例項目。</span><span class="sxs-lookup"><span data-stu-id="72749-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="72749-221">例如，如果項目更新通常會修改名為 lastLogin 和 userVisits 的兩個屬性，則只要複製範例項目、更新這兩個屬性的值，並上傳複製的項目。</span><span class="sxs-lookup"><span data-stu-id="72749-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![在要求單位計算機中輸入輸送量需求][3]
4. <span data-ttu-id="72749-223">按一下計算，並檢查結果。</span><span class="sxs-lookup"><span data-stu-id="72749-223">Click calculate and examine the results.</span></span>
   
    ![要求單位計算機結果][4]

> [!NOTE]
> <span data-ttu-id="72749-225">如果您的項目類型與已編製索引之屬性的大小與數目截然不同，則請將每個一般項目「類型」的範例上傳至工具，然後計算結果。</span><span class="sxs-lookup"><span data-stu-id="72749-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="72749-226">使用 Azure Cosmos DB 要求費用回應標頭</span><span class="sxs-lookup"><span data-stu-id="72749-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="72749-227">Azure Cosmos DB 服務的每個回應都會包括自訂標頭 (`x-ms-request-charge`)，其中包含要求所耗用的要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="72749-228">此標頭也可以透過 Azure Cosmos DB SDK 進行存取。</span><span class="sxs-lookup"><span data-stu-id="72749-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="72749-229">在 .NET SDK 中，RequestCharge 是 ResourceResponse 物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="72749-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="72749-230">針對查詢，Azure 入口網站中的 Azure Cosmos DB 查詢總管會提供已執行查詢的要求費用資訊。</span><span class="sxs-lookup"><span data-stu-id="72749-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![在查詢總管中檢查 RU 費用][1]

<span data-ttu-id="72749-232">將此銘記於心，有一個估計應用程式所需之保留輸送量的方法是，記錄與根據應用程式所使用之代表性項目執行一般作業相關聯的要求單位費用，然後估計您預期每秒執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="72749-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="72749-233">此外，請務必測量並包含一般查詢和 Azure Cosmos DB 指令碼使用方式。</span><span class="sxs-lookup"><span data-stu-id="72749-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="72749-234">如果您的項目類型與已編製索引之屬性的大小與數目截然不同，則請記錄與每個一般項目「類型」相關聯的適用作業要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="72749-235">例如：</span><span class="sxs-lookup"><span data-stu-id="72749-235">For example:</span></span>

1. <span data-ttu-id="72749-236">記錄建立 (插入) 一般項目的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="72749-237">記錄讀取一般項目的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="72749-238">記錄更新一般項目的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="72749-239">記錄一般且常見項目查詢的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="72749-240">記錄應用程式所使用的任何自訂指令碼 (預存程序、觸發程序、使用者定義的函式) 的要求單位費用</span><span class="sxs-lookup"><span data-stu-id="72749-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="72749-241">根據您預期每秒執行的作業估計數目，來計算必要的要求單位數。</span><span class="sxs-lookup"><span data-stu-id="72749-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="72749-242"><a id="GetLastRequestStatistics"></a>使用 API for MongoDB 的 GetLastRequestStatistics 命令</span><span class="sxs-lookup"><span data-stu-id="72749-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="72749-243">API for Mongodb 支援自訂命令 *getLastRequestStatistics*，可擷取指定之作業的要求費用。</span><span class="sxs-lookup"><span data-stu-id="72749-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="72749-244">例如，在 Mongo 殼層中，執行您想要驗證要求費用的作業。</span><span class="sxs-lookup"><span data-stu-id="72749-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="72749-245">接著，執行命令 *getLastRequestStatistics*。</span><span class="sxs-lookup"><span data-stu-id="72749-245">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="72749-246">將此銘記於心，有一個估計應用程式所需之保留輸送量的方法是，記錄與根據應用程式所使用之代表性項目執行一般作業相關聯的要求單位費用，然後估計您預期每秒執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="72749-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="72749-247">如果您的項目類型與已編製索引之屬性的大小與數目截然不同，則請記錄與每個一般項目「類型」相關聯的適用作業要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="72749-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="72749-248">使用 API for MongoDB 的入口網站計量</span><span class="sxs-lookup"><span data-stu-id="72749-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="72749-249">若要準確估計 API for MongoDB 資料庫的要求單位費用，最簡單的方法就是使用 [Azure 入口網站](https://portal.azure.com)計量。</span><span class="sxs-lookup"><span data-stu-id="72749-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="72749-250">利用 [要求數目] 和 [要求費用] 圖表，您可以估計每個作業耗用多少要求單位，以及它們彼此之間相對耗用多少要求單位。</span><span class="sxs-lookup"><span data-stu-id="72749-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![API for MongoDB 入口網站計量][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="72749-252">要求單位估計範例</span><span class="sxs-lookup"><span data-stu-id="72749-252">A request unit estimation example</span></span>
<span data-ttu-id="72749-253">請考量下列 ~1KB 文件：</span><span class="sxs-lookup"><span data-stu-id="72749-253">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="72749-254">文件在 Azure Cosmos DB 中會變小，因此系統針對上述文件計算出的大小會稍微少於 1KB。</span><span class="sxs-lookup"><span data-stu-id="72749-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="72749-255">下表顯示本項目中一般操作的概略要求單位費用 (概略的要求單位費用假設帳戶一致性層級會設定為「工作階段」且所有項目都已自動編製索引)：</span><span class="sxs-lookup"><span data-stu-id="72749-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="72749-256">作業</span><span class="sxs-lookup"><span data-stu-id="72749-256">Operation</span></span> | <span data-ttu-id="72749-257">要求單位費用</span><span class="sxs-lookup"><span data-stu-id="72749-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="72749-258">建立項目</span><span class="sxs-lookup"><span data-stu-id="72749-258">Create item</span></span> |<span data-ttu-id="72749-259">~15 RU</span><span class="sxs-lookup"><span data-stu-id="72749-259">~15 RU</span></span> |
| <span data-ttu-id="72749-260">讀取項目</span><span class="sxs-lookup"><span data-stu-id="72749-260">Read item</span></span> |<span data-ttu-id="72749-261">~1 RU</span><span class="sxs-lookup"><span data-stu-id="72749-261">~1 RU</span></span> |
| <span data-ttu-id="72749-262">依識別碼查詢項目</span><span class="sxs-lookup"><span data-stu-id="72749-262">Query item by id</span></span> |<span data-ttu-id="72749-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="72749-263">~2.5 RU</span></span> |

<span data-ttu-id="72749-264">此外，下表顯示應用程式中所使用之標準查詢的概略要求單位費用︰</span><span class="sxs-lookup"><span data-stu-id="72749-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="72749-265">查詢</span><span class="sxs-lookup"><span data-stu-id="72749-265">Query</span></span> | <span data-ttu-id="72749-266">要求單位費用</span><span class="sxs-lookup"><span data-stu-id="72749-266">Request Unit Charge</span></span> | <span data-ttu-id="72749-267"># 個傳回的項目</span><span class="sxs-lookup"><span data-stu-id="72749-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72749-268">依識別碼選取食物</span><span class="sxs-lookup"><span data-stu-id="72749-268">Select food by id</span></span> |<span data-ttu-id="72749-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="72749-269">~2.5 RU</span></span> |<span data-ttu-id="72749-270">1</span><span class="sxs-lookup"><span data-stu-id="72749-270">1</span></span> |
| <span data-ttu-id="72749-271">依製造商選取食物</span><span class="sxs-lookup"><span data-stu-id="72749-271">Select foods by manufacturer</span></span> |<span data-ttu-id="72749-272">~7 RU</span><span class="sxs-lookup"><span data-stu-id="72749-272">~7 RU</span></span> |<span data-ttu-id="72749-273">7</span><span class="sxs-lookup"><span data-stu-id="72749-273">7</span></span> |
| <span data-ttu-id="72749-274">依食物群組選取並依重量排序</span><span class="sxs-lookup"><span data-stu-id="72749-274">Select by food group and order by weight</span></span> |<span data-ttu-id="72749-275">~70 RU</span><span class="sxs-lookup"><span data-stu-id="72749-275">~70 RU</span></span> |<span data-ttu-id="72749-276">100</span><span class="sxs-lookup"><span data-stu-id="72749-276">100</span></span> |
| <span data-ttu-id="72749-277">選取食物群組中的前 10 個食物</span><span class="sxs-lookup"><span data-stu-id="72749-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="72749-278">~10 RU</span><span class="sxs-lookup"><span data-stu-id="72749-278">~10 RU</span></span> |<span data-ttu-id="72749-279">10</span><span class="sxs-lookup"><span data-stu-id="72749-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="72749-280">RU 費用會根據傳回的項目數目而有所不同。</span><span class="sxs-lookup"><span data-stu-id="72749-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="72749-281">利用此資訊，我們可以根據預期每秒的作業和查詢數目，來估計此應用程式的 RU 需求︰</span><span class="sxs-lookup"><span data-stu-id="72749-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="72749-282">作業/查詢</span><span class="sxs-lookup"><span data-stu-id="72749-282">Operation/Query</span></span> | <span data-ttu-id="72749-283">每秒估計的數目</span><span class="sxs-lookup"><span data-stu-id="72749-283">Estimated number per second</span></span> | <span data-ttu-id="72749-284">必要的 RU 數</span><span class="sxs-lookup"><span data-stu-id="72749-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72749-285">建立項目</span><span class="sxs-lookup"><span data-stu-id="72749-285">Create item</span></span> |<span data-ttu-id="72749-286">10</span><span class="sxs-lookup"><span data-stu-id="72749-286">10</span></span> |<span data-ttu-id="72749-287">150</span><span class="sxs-lookup"><span data-stu-id="72749-287">150</span></span> |
| <span data-ttu-id="72749-288">讀取項目</span><span class="sxs-lookup"><span data-stu-id="72749-288">Read item</span></span> |<span data-ttu-id="72749-289">100</span><span class="sxs-lookup"><span data-stu-id="72749-289">100</span></span> |<span data-ttu-id="72749-290">100</span><span class="sxs-lookup"><span data-stu-id="72749-290">100</span></span> |
| <span data-ttu-id="72749-291">依製造商選取食物</span><span class="sxs-lookup"><span data-stu-id="72749-291">Select foods by manufacturer</span></span> |<span data-ttu-id="72749-292">25</span><span class="sxs-lookup"><span data-stu-id="72749-292">25</span></span> |<span data-ttu-id="72749-293">175</span><span class="sxs-lookup"><span data-stu-id="72749-293">175</span></span> |
| <span data-ttu-id="72749-294">依食物群組選取</span><span class="sxs-lookup"><span data-stu-id="72749-294">Select by food group</span></span> |<span data-ttu-id="72749-295">10</span><span class="sxs-lookup"><span data-stu-id="72749-295">10</span></span> |<span data-ttu-id="72749-296">700</span><span class="sxs-lookup"><span data-stu-id="72749-296">700</span></span> |
| <span data-ttu-id="72749-297">選取前 10 個</span><span class="sxs-lookup"><span data-stu-id="72749-297">Select top 10</span></span> |<span data-ttu-id="72749-298">15</span><span class="sxs-lookup"><span data-stu-id="72749-298">15</span></span> |<span data-ttu-id="72749-299">總共 150 個</span><span class="sxs-lookup"><span data-stu-id="72749-299">150 Total</span></span> |

<span data-ttu-id="72749-300">在此情況下，我們預期平均輸送量需求為 1,275 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="72749-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="72749-301">四捨五入至最接近 100 的數目，我們會針對此應用程式的集合佈建 1,300 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="72749-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="72749-302"><a id="RequestRateTooLarge"></a> 超過 Azure Cosmos DB 中保留的輸送量限制</span><span class="sxs-lookup"><span data-stu-id="72749-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="72749-303">您應該記得，如果預算是空的，要求單位耗用量是以每秒的速率來評估。</span><span class="sxs-lookup"><span data-stu-id="72749-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="72749-304">應用程式若超過容器已佈建的要求單位速率，該集合的要求會受到節流控制，直到該速率降到預留層級以下。</span><span class="sxs-lookup"><span data-stu-id="72749-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="72749-305">當節流發生時，伺服器將預先使用 RequestRateTooLargeException (HTTP 狀態碼 429) 來結束要求，並傳回 x-ms-retry-after-ms 標頭，以指出使用者重試要求之前必須等候的時間量 (毫秒)。</span><span class="sxs-lookup"><span data-stu-id="72749-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="72749-306">如果您使用 .NET 用戶端 SDK 和 LINQ 查詢，則大部分時間您都不再需要處理這個例外狀況，因為目前版本的 .NET 用戶端 SDK 會隱含地攔截這個回應、遵守伺服器指定的 retry-after 標頭，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="72749-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="72749-307">除非有多個用戶端同時存取您的帳戶，否則下次重試將會成功。</span><span class="sxs-lookup"><span data-stu-id="72749-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="72749-308">如果您有多個用戶端會以高於要求速率的方式累積運作，則預設的重試行為可能會不敷使用，而用戶端將擲回 DocumentClientException (狀態碼 429) 到應用程式。</span><span class="sxs-lookup"><span data-stu-id="72749-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="72749-309">在這類情況下，您可以考慮處理應用程式錯誤處理常式中的重試行為和邏輯，或為容器提高保留的輸送量。</span><span class="sxs-lookup"><span data-stu-id="72749-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="72749-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> 超過 API for MongoDB 中保留的輸送量限制</span><span class="sxs-lookup"><span data-stu-id="72749-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="72749-311">如果應用程式超過集合已佈建的要求單位，則會受到節流控制，直到速率降到保留的等級以下。</span><span class="sxs-lookup"><span data-stu-id="72749-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="72749-312">節流發生時，後端會提前結束要求，並傳回 16500 錯誤碼 -「太多要求」。</span><span class="sxs-lookup"><span data-stu-id="72749-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="72749-313">根據預設，在傳回「太多要求」錯誤碼之前，API for MongoDB 會自動重試最多 10 次。</span><span class="sxs-lookup"><span data-stu-id="72749-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="72749-314">如果您收到很多「太多要求」錯誤碼，您可以考慮在應用程式的錯誤處理常式中新增重試行為，或[提高集合的保留輸送量](set-throughput.md)。</span><span class="sxs-lookup"><span data-stu-id="72749-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72749-315">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72749-315">Next steps</span></span>
<span data-ttu-id="72749-316">若要深入了解透過 Azure Cosmos DB 資料庫保留輸送量的方式，請探索下列資源：</span><span class="sxs-lookup"><span data-stu-id="72749-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="72749-317">Azure Cosmos DB 定價</span><span class="sxs-lookup"><span data-stu-id="72749-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="72749-318">在 Azure Cosmos DB 中分割資料</span><span class="sxs-lookup"><span data-stu-id="72749-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="72749-319">若要深入了解 Azure Cosmos DB，請參閱 Azure Cosmos DB [文件](https://azure.microsoft.com/documentation/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="72749-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="72749-320">若要開始使用 Azure Cosmos DB 的相關規模和效能測試，請參閱 [Azure Cosmos DB 的相關效能和規模測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="72749-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
