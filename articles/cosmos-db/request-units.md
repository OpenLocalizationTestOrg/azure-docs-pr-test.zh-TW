---
title: "aaaRequest 單位 & 估計輸送量-Azure Cosmos DB |Microsoft 文件"
description: "深入了解 toounderstand，指定，並評估 Azure Cosmos DB 中的要求單位需求的方式。"
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
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="e8d81-103">Azure Cosmos DB 中的要求單位</span><span class="sxs-lookup"><span data-stu-id="e8d81-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="e8d81-104">現在可供使用︰Azure Cosmos DB [要求單位計算機 (英文)](https://www.documentdb.com/capacityplanner)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="e8d81-105">深入了解 [預估您的輸送量需求](request-units.md#estimating-throughput-needs)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![輸送量計算機][5]

## <a name="introduction"></a><span data-ttu-id="e8d81-107">簡介</span><span class="sxs-lookup"><span data-stu-id="e8d81-107">Introduction</span></span>
<span data-ttu-id="e8d81-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是 Microsoft 的全域分散式多模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8d81-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="e8d81-109">以 Azure Cosmos DB，您尚未 toorent 虛擬機器、 部署軟體，或監視資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8d81-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="e8d81-110">Azure Cosmos DB 是操作，並持續受到 Microsoft 頂端工程師 toodeliver 世界類別可用性、 效能及資料保護。</span><span class="sxs-lookup"><span data-stu-id="e8d81-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="e8d81-111">您可以使用選擇的 API 來存取資料，因為 [DocumentDB SQL](documentdb-sql-query.md) (文件)、MongoDB (文件)、[Azure 資料表儲存體](https://azure.microsoft.com/services/storage/tables/) (索引鍵值) 和 [Gremlin (英文)](https://tinkerpop.apache.org/gremlin.html) (圖表) 皆受到原 生支援。</span><span class="sxs-lookup"><span data-stu-id="e8d81-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="e8d81-112">hello 貨幣的 Azure Cosmos DB 為 hello 要求單位 (RU)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="e8d81-113">RUs，與您不需要 tooreserve 讀/寫容量或佈建 CPU、 記憶體和 IOPS。</span><span class="sxs-lookup"><span data-stu-id="e8d81-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="e8d81-114">Azure Cosmos DB 支援的 Api 以不同的作業，範圍從簡單的讀取和寫入 toocomplex graph 查詢。</span><span class="sxs-lookup"><span data-stu-id="e8d81-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="e8d81-115">由於並非所有要求都都相同，就都會指派正規化的數量**要求單位**根據計算需要的 tooserve hello 要求 hello 金額。</span><span class="sxs-lookup"><span data-stu-id="e8d81-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="e8d81-116">作業的要求單位的 hello 數目是具決定性，而且您可以追蹤 hello Azure Cosmos DB 中透過回應標頭的任何作業所使用的要求單位數目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="e8d81-117">tooprovide 可預測的效能，您需要 tooreserve 輸送量單位的 100 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="e8d81-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="e8d81-118">閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="e8d81-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="e8d81-119">什麼是要求單位和要求費用？</span><span class="sxs-lookup"><span data-stu-id="e8d81-119">What are request units and request charges?</span></span>
* <span data-ttu-id="e8d81-120">如何指定集合的要求單位容量？</span><span class="sxs-lookup"><span data-stu-id="e8d81-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="e8d81-121">如何估計應用程式的要求單位需求？</span><span class="sxs-lookup"><span data-stu-id="e8d81-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="e8d81-122">如果超過集合的要求單位容量，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="e8d81-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="e8d81-123">如同 Azure Cosmos DB 多模型資料庫，所以我們將會針對應用程式開發介面文件、 圖形/節點 graph API 的資料表/實體資料表應用程式開發介面參考 tooa 集合文件的重要 toonote。</span><span class="sxs-lookup"><span data-stu-id="e8d81-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="e8d81-124">輸送量這份文件，我們將一般化 toohello 概念容器/項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="e8d81-125">要求單位和要求費用</span><span class="sxs-lookup"><span data-stu-id="e8d81-125">Request units and request charges</span></span>
<span data-ttu-id="e8d81-126">Azure Cosmos DB 都會提供快速、 可預測的效能，由*保留*資源 toosatisfy 應用程式的輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="e8d81-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="e8d81-127">應用程式會載入並存取一段時間的模式變更，因為 Azure Cosmos DB 可讓您 tooeasily 增加，或減少 hello 保留的輸送量可用 tooyour 應用程式的數量。</span><span class="sxs-lookup"><span data-stu-id="e8d81-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="e8d81-128">有了 Azure Cosmos DB，保留的輸送量是根據每秒處理的要求單位來指定。</span><span class="sxs-lookup"><span data-stu-id="e8d81-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="e8d81-129">您可以視為要求單位的輸送量貨幣，讓您*保留*數量保證的要求單位可用 tooyour 每秒為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8d81-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="e8d81-130">Azure Cosmos DB 中的每個作業 (寫入文件、執行查詢、更新文件) 都會耗用 CPU、記憶體和 IOPS。</span><span class="sxs-lookup"><span data-stu-id="e8d81-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="e8d81-131">也就是說，每個作業都會產生「要求費用」，這是以「要求單位」來表示。</span><span class="sxs-lookup"><span data-stu-id="e8d81-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="e8d81-132">了解 hello 因素會影響要求單位的費用，您的應用程式輸送量需求，以及可讓您 toorun 成本儘可能有效的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8d81-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="e8d81-133">hello 查詢總管也是查詢的完美工具 tootest hello 核心。</span><span class="sxs-lookup"><span data-stu-id="e8d81-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="e8d81-134">我們建議您藉由監看下列影片，其中 Aravind Ramachandran 說明要求單位，以及可預測的效能與 Azure Cosmos DB hello 開始使用。</span><span class="sxs-lookup"><span data-stu-id="e8d81-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="e8d81-135">在 Azure Cosmos DB 中指定要求單位容量</span><span class="sxs-lookup"><span data-stu-id="e8d81-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="e8d81-136">當啟動新的集合、 資料表或圖表時，您會指定 hello 號碼的要求單位 (RU 每秒) 秒您想保留。</span><span class="sxs-lookup"><span data-stu-id="e8d81-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="e8d81-137">根據 hello 佈建輸送量，Azure Cosmos DB 配置實體分割區 toohost 您的集合，並分割/rebalances 資料在資料分割的成長。</span><span class="sxs-lookup"><span data-stu-id="e8d81-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="e8d81-138">Azure Cosmos DB 需要資料分割索引鍵的 toobe 指定集合已佈建以供 2,500 要求單位或更高版本時。</span><span class="sxs-lookup"><span data-stu-id="e8d81-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="e8d81-139">資料分割索引鍵也是必要的 tooscale 集合的輸送量超過 2,500 在 hello 未來的要求單位。</span><span class="sxs-lookup"><span data-stu-id="e8d81-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="e8d81-140">因此，強烈建議 tooconfigure[資料分割索引鍵](partition-data.md)時建立的容器，不論您初始的輸送量。</span><span class="sxs-lookup"><span data-stu-id="e8d81-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="e8d81-141">因為您的資料可能會有 toobe 分成多個資料分割，就會需要 toopick 具有高基數 (相異值的 100 toomillions)，讓您收集/資料表/圖形與要求可以縮放統一 Azure Cosmos db 的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e8d81-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="e8d81-142">資料分割索引鍵是一種邏輯界限，而不是實體界限。</span><span class="sxs-lookup"><span data-stu-id="e8d81-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="e8d81-143">因此，您不需要 toolimit hello 數目相異的資料分割索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="e8d81-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="e8d81-144">它實際上是較佳 toohave 比較明顯分割區較少的索引鍵值，因為 Azure Cosmos DB 具有多個負載平衡選項。</span><span class="sxs-lookup"><span data-stu-id="e8d81-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="e8d81-145">以下是用來建立集合與 3000 的程式碼片段要求每個第二個使用單位 hello.NET SDK:</span><span class="sxs-lookup"><span data-stu-id="e8d81-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="e8d81-146">Azure Cosmos DB 會在輸送量的保留模型上運作。</span><span class="sxs-lookup"><span data-stu-id="e8d81-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="e8d81-147">也就是，您需要付費 hello 段輸送量*保留*，不論有多少的輸送量主動*用*。</span><span class="sxs-lookup"><span data-stu-id="e8d81-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="e8d81-148">為您的應用程式負載、 資料和使用模式變更您可以輕鬆地向上和向下調整 hello 保留 RUs 透過 Sdk 的數量，或使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e8d81-149">對應每個集合/資料表/圖形 tooan `Offer` Azure Cosmos DB 已 hello 佈建輸送量的相關中繼資料中的資源。</span><span class="sxs-lookup"><span data-stu-id="e8d81-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="e8d81-150">您可以變更配置的 hello 輸送量查閱 hello 對應優惠資源容器，然後更新以 hello 新的處理量值。</span><span class="sxs-lookup"><span data-stu-id="e8d81-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="e8d81-151">以下是變更集合 too5 hello 輸送量的程式碼片段，每個第二個使用 000 要求單位 hello.NET SDK:</span><span class="sxs-lookup"><span data-stu-id="e8d81-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="e8d81-152">當您變更 hello 輸送量時沒有任何影響 toohello 可用性，您的容器。</span><span class="sxs-lookup"><span data-stu-id="e8d81-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="e8d81-153">通常 hello 新增保留的輸送量 hello 新產能的應用程式上的數秒內是有效。</span><span class="sxs-lookup"><span data-stu-id="e8d81-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="e8d81-154">要求單位的考量</span><span class="sxs-lookup"><span data-stu-id="e8d81-154">Request unit considerations</span></span>
<span data-ttu-id="e8d81-155">評估 hello Azure Cosmos DB 容器的要求單位 tooreserve 數目時，重要 tootake hello 考量下列變數：</span><span class="sxs-lookup"><span data-stu-id="e8d81-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="e8d81-156">**項目大小**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-156">**Item size**.</span></span> <span data-ttu-id="e8d81-157">大小會增加 hello 使用的單位 tooread 或寫入 hello 資料也會增加。</span><span class="sxs-lookup"><span data-stu-id="e8d81-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="e8d81-158">**項目屬性計數**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-158">**Item property count**.</span></span> <span data-ttu-id="e8d81-159">假設預設索引的所有屬性，hello 使用的單位 toowrite 文件/節點/ntity hello 屬性計數增加時，會增加。</span><span class="sxs-lookup"><span data-stu-id="e8d81-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="e8d81-160">**資料一致性**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-160">**Data consistency**.</span></span> <span data-ttu-id="e8d81-161">使用強式或繫結失效的資料一致性層級，額外的單位會取用的 tooread 項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="e8d81-162">**已編製索引的屬性**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-162">**Indexed properties**.</span></span> <span data-ttu-id="e8d81-163">每個容器上的索引原則會判定預設要編製哪些索引的屬性。</span><span class="sxs-lookup"><span data-stu-id="e8d81-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="e8d81-164">藉由限制 hello 索引的屬性數目，或藉由啟用延遲索引，您可以減少您的要求單位耗用量。</span><span class="sxs-lookup"><span data-stu-id="e8d81-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="e8d81-165">**編製文件索引**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-165">**Document indexing**.</span></span> <span data-ttu-id="e8d81-166">根據預設，每個項目會自動編製索引，您會耗用較少的要求單位，如果您選擇不 tooindex 部分的項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="e8d81-167">**查詢模式**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-167">**Query patterns**.</span></span> <span data-ttu-id="e8d81-168">查詢的 hello 複雜性會影響作業耗用多少要求單位。</span><span class="sxs-lookup"><span data-stu-id="e8d81-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="e8d81-169">述詞的 hello 數目、 性質 hello 述詞、 投射、 Udf、 數目和 hello 大小會影響所有的 hello 成本 hello 來源資料集的查詢作業。</span><span class="sxs-lookup"><span data-stu-id="e8d81-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="e8d81-170">**指令碼使用方式**。</span><span class="sxs-lookup"><span data-stu-id="e8d81-170">**Script usage**.</span></span>  <span data-ttu-id="e8d81-171">如同查詢、 預存程序和觸發程序會耗用根據 hello 複雜度 hello 作業正在執行的要求單位。</span><span class="sxs-lookup"><span data-stu-id="e8d81-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="e8d81-172">當您開發應用程式時，檢查 hello 要求電量標頭 toobetter 了解如何每一項作業會耗用要求單位容量。</span><span class="sxs-lookup"><span data-stu-id="e8d81-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="e8d81-173">估計輸送量需求</span><span class="sxs-lookup"><span data-stu-id="e8d81-173">Estimating throughput needs</span></span>
<span data-ttu-id="e8d81-174">要求單位是要求處理成本的標準化量值。</span><span class="sxs-lookup"><span data-stu-id="e8d81-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="e8d81-175">單一要求單位代表 hello 處理所需的容量 tooread （透過自我連結或識別碼） （不含系統屬性） 的 10 個唯一的屬性值的項目所組成的單一 1 KB。</span><span class="sxs-lookup"><span data-stu-id="e8d81-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="e8d81-176">要求 toocreate （插入），取代或刪除相同項目會耗用更多的處理從 hello 服務的 hello，藉此多個要求單位。</span><span class="sxs-lookup"><span data-stu-id="e8d81-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="e8d81-177">1 的要求單位的 hello 基準為 1 KB 項目對應 tooa 簡單取得自我連結或 hello 項目的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e8d81-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="e8d81-178">例如，以下是資料表，其中顯示多少要求單位 tooprovision 在三個不同的項目大小 （1 KB、 4 KB 和 64 KB） 和兩個不同的效能層級 （每秒 500 讀取 + 100 寫入/秒與 500 讀取/秒 + 500 寫入/秒）。</span><span class="sxs-lookup"><span data-stu-id="e8d81-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="e8d81-179">在工作階段，設定 hello 資料的一致性，且 tooNone hello 檢索原則設定。</span><span class="sxs-lookup"><span data-stu-id="e8d81-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-180"><strong>項目大小</strong></span><span class="sxs-lookup"><span data-stu-id="e8d81-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-181"><strong>讀取/秒</strong></span><span class="sxs-lookup"><span data-stu-id="e8d81-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-182"><strong>寫入/秒</strong></span><span class="sxs-lookup"><span data-stu-id="e8d81-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-183"><strong>要求單位</strong></span><span class="sxs-lookup"><span data-stu-id="e8d81-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-185">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-186">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-189">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-190">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-193">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-194">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-197">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-198">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-201">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-202">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e8d81-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="e8d81-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-205">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-206">500</span><span class="sxs-lookup"><span data-stu-id="e8d81-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e8d81-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="e8d81-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="e8d81-208">使用 [小算盤] 的要求單位 hello</span><span class="sxs-lookup"><span data-stu-id="e8d81-208">Use hello request unit calculator</span></span>
<span data-ttu-id="e8d81-209">正常 toohelp 客戶調整其處理能力數量的估計值，所以在 web 架構[要求單位計算機](https://www.documentdb.com/capacityplanner)toohelp 估計 hello 要求單位需求一般作業，包括：</span><span class="sxs-lookup"><span data-stu-id="e8d81-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="e8d81-210">項目建立 (寫入)</span><span class="sxs-lookup"><span data-stu-id="e8d81-210">Item creates (writes)</span></span>
* <span data-ttu-id="e8d81-211">項目讀取</span><span class="sxs-lookup"><span data-stu-id="e8d81-211">Item reads</span></span>
* <span data-ttu-id="e8d81-212">項目刪除</span><span class="sxs-lookup"><span data-stu-id="e8d81-212">Item deletes</span></span>
* <span data-ttu-id="e8d81-213">項目更新</span><span class="sxs-lookup"><span data-stu-id="e8d81-213">Item updates</span></span>

<span data-ttu-id="e8d81-214">hello 工具也包含支援估計 hello 您提供的範例項目為基礎的資料存放區需求。</span><span class="sxs-lookup"><span data-stu-id="e8d81-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="e8d81-215">使用 hello 工具很簡單：</span><span class="sxs-lookup"><span data-stu-id="e8d81-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="e8d81-216">上傳一或多個具代表性的項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-216">Upload one or more representative items.</span></span>
   
    ![上傳項目 toohello 要求單位計算機][2]
2. <span data-ttu-id="e8d81-218">tooestimate 資料儲存需求，請輸入 hello 總數的項目中，您預期 toostore。</span><span class="sxs-lookup"><span data-stu-id="e8d81-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="e8d81-219">輸入 hello 數目的項目建立、 讀取、 更新和刪除的作業，您需要 （每秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="e8d81-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="e8d81-220">tooestimate hello 要求單位費用的項目更新作業上, 傳一份 hello 從上方步驟 1 包含一般的欄位更新的範例項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="e8d81-221">例如，如果項目更新通常修改名為 lastLogin 和 userVisits，兩個屬性，則只需複製 hello 範例項目，更新這兩個屬性，以 hello 值，並上傳 hello 複製項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![在 hello 要求單位計算機輸入輸送量需求][3]
4. <span data-ttu-id="e8d81-223">按一下計算，並檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e8d81-223">Click calculate and examine hello results.</span></span>
   
    ![要求單位計算機結果][4]

> [!NOTE]
> <span data-ttu-id="e8d81-225">如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後上傳的每個範例*類型*典型的項目 toohello 的工具，然後再計算 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e8d81-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="e8d81-226">使用 hello Azure Cosmos DB 要求電量回應標頭</span><span class="sxs-lookup"><span data-stu-id="e8d81-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="e8d81-227">每個回應 hello Azure Cosmos DB 服務從包含自訂標頭 (`x-ms-request-charge`)，其中包含使用 hello 要求的 hello 要求單位。</span><span class="sxs-lookup"><span data-stu-id="e8d81-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="e8d81-228">也可透過 hello Azure Cosmos DB Sdk 存取此標頭。</span><span class="sxs-lookup"><span data-stu-id="e8d81-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="e8d81-229">在 hello.NET SDK，RequestCharge 是 hello ResourceResponse 物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="e8d81-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="e8d81-230">查詢，hello Azure 入口網站中的 hello Azure Cosmos DB 查詢總管會提供執行查詢的要求計量資訊。</span><span class="sxs-lookup"><span data-stu-id="e8d81-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![檢查在 hello 查詢總管 RU 費用][1]

<span data-ttu-id="e8d81-232">這一點，估計 hello 保留輸送量應用程式所需數量的方法之一是 toorecord hello 要求單位電量與執行一般作業，針對您的應用程式所使用的代表項目相關聯，然後您預期執行每秒估計 hello 作業數目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="e8d81-233">能確定 toomeasure，而且包含一般的查詢和 Azure Cosmos DB 指令碼使用。</span><span class="sxs-lookup"><span data-stu-id="e8d81-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d81-234">如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後記錄每個相關聯的 hello 適用的作業要求單位收費*類型*的典型的項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="e8d81-235">例如：</span><span class="sxs-lookup"><span data-stu-id="e8d81-235">For example:</span></span>

1. <span data-ttu-id="e8d81-236">記錄 hello 要求單位收費 （插入） 所建立的一般項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="e8d81-237">典型的項目中讀取的要求單位費用記錄 hello。</span><span class="sxs-lookup"><span data-stu-id="e8d81-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="e8d81-238">資料錄 hello 要求單位的更新的一般項目費用。</span><span class="sxs-lookup"><span data-stu-id="e8d81-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="e8d81-239">一般、 常見的項目查詢的要求單位費用記錄 hello。</span><span class="sxs-lookup"><span data-stu-id="e8d81-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="e8d81-240">記錄 hello 要求單位收費用的任何自訂指令碼 （預存程序、 觸發程序、 使用者定義函數） 透過 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e8d81-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="e8d81-241">計算 hello 需要給定作業的 hello 估計數的單位您預期 toorun 每秒的要求。</span><span class="sxs-lookup"><span data-stu-id="e8d81-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="e8d81-242"><a id="GetLastRequestStatistics"></a>使用 API for MongoDB 的 GetLastRequestStatistics 命令</span><span class="sxs-lookup"><span data-stu-id="e8d81-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="e8d81-243">MongoDB 的 API 支援自訂的命令， *getLastRequestStatistics*，擷取指定作業的 hello 要求需付費。</span><span class="sxs-lookup"><span data-stu-id="e8d81-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="e8d81-244">比方說，在 hello Mongo 殼層，執行您要 tooverify hello 要求不需要支付費用的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e8d81-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="e8d81-245">接下來，執行 hello 命令*getLastRequestStatistics*。</span><span class="sxs-lookup"><span data-stu-id="e8d81-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="e8d81-246">這一點，估計 hello 保留輸送量應用程式所需數量的方法之一是 toorecord hello 要求單位電量與執行一般作業，針對您的應用程式所使用的代表項目相關聯，然後您預期執行每秒估計 hello 作業數目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d81-247">如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後記錄每個相關聯的 hello 適用的作業要求單位收費*類型*的典型的項目。</span><span class="sxs-lookup"><span data-stu-id="e8d81-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="e8d81-248">使用 API for MongoDB 的入口網站計量</span><span class="sxs-lookup"><span data-stu-id="e8d81-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="e8d81-249">hello MongoDB 資料庫是 toouse hello 要求單位的良好的估計費用您 api 的最簡單方式 tooget [Azure 入口網站](https://portal.azure.com)度量。</span><span class="sxs-lookup"><span data-stu-id="e8d81-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="e8d81-250">以 hello*的要求數目*和*要求電量*圖表，您可以取得每個作業的要求單位數量的估計，耗用和要求單位的數量它們會耗用相對 tooone 另一個。</span><span class="sxs-lookup"><span data-stu-id="e8d81-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![API for MongoDB 入口網站計量][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="e8d81-252">要求單位估計範例</span><span class="sxs-lookup"><span data-stu-id="e8d81-252">A request unit estimation example</span></span>
<span data-ttu-id="e8d81-253">請考慮下列 ~ 1 KB 文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="e8d81-253">Consider hello following ~1KB document:</span></span>

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
> <span data-ttu-id="e8d81-254">文件會在 Azure Cosmos DB，縮短，因此 hello 系統計算上述 hello 文件的大小為略小於 1 KB。</span><span class="sxs-lookup"><span data-stu-id="e8d81-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="e8d81-255">hello 下表顯示大約要求此項目上的一般作業的單位收費 (hello 近似的要求單位收費假設 hello 帳戶一致性層級設定得 「 工作階段 」 和所有項目會自動編製索引):</span><span class="sxs-lookup"><span data-stu-id="e8d81-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="e8d81-256">作業</span><span class="sxs-lookup"><span data-stu-id="e8d81-256">Operation</span></span> | <span data-ttu-id="e8d81-257">要求單位費用</span><span class="sxs-lookup"><span data-stu-id="e8d81-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="e8d81-258">建立項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-258">Create item</span></span> |<span data-ttu-id="e8d81-259">~15 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-259">~15 RU</span></span> |
| <span data-ttu-id="e8d81-260">讀取項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-260">Read item</span></span> |<span data-ttu-id="e8d81-261">~1 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-261">~1 RU</span></span> |
| <span data-ttu-id="e8d81-262">依識別碼查詢項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-262">Query item by id</span></span> |<span data-ttu-id="e8d81-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-263">~2.5 RU</span></span> |

<span data-ttu-id="e8d81-264">此外下, 表顯示概略的要求單位費用 hello 應用程式中使用的典型查詢：</span><span class="sxs-lookup"><span data-stu-id="e8d81-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="e8d81-265">查詢</span><span class="sxs-lookup"><span data-stu-id="e8d81-265">Query</span></span> | <span data-ttu-id="e8d81-266">要求單位費用</span><span class="sxs-lookup"><span data-stu-id="e8d81-266">Request Unit Charge</span></span> | <span data-ttu-id="e8d81-267"># 個傳回的項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8d81-268">依識別碼選取食物</span><span class="sxs-lookup"><span data-stu-id="e8d81-268">Select food by id</span></span> |<span data-ttu-id="e8d81-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-269">~2.5 RU</span></span> |<span data-ttu-id="e8d81-270">1</span><span class="sxs-lookup"><span data-stu-id="e8d81-270">1</span></span> |
| <span data-ttu-id="e8d81-271">依製造商選取食物</span><span class="sxs-lookup"><span data-stu-id="e8d81-271">Select foods by manufacturer</span></span> |<span data-ttu-id="e8d81-272">~7 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-272">~7 RU</span></span> |<span data-ttu-id="e8d81-273">7</span><span class="sxs-lookup"><span data-stu-id="e8d81-273">7</span></span> |
| <span data-ttu-id="e8d81-274">依食物群組選取並依重量排序</span><span class="sxs-lookup"><span data-stu-id="e8d81-274">Select by food group and order by weight</span></span> |<span data-ttu-id="e8d81-275">~70 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-275">~70 RU</span></span> |<span data-ttu-id="e8d81-276">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-276">100</span></span> |
| <span data-ttu-id="e8d81-277">選取食物群組中的前 10 個食物</span><span class="sxs-lookup"><span data-stu-id="e8d81-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="e8d81-278">~10 RU</span><span class="sxs-lookup"><span data-stu-id="e8d81-278">~10 RU</span></span> |<span data-ttu-id="e8d81-279">10</span><span class="sxs-lookup"><span data-stu-id="e8d81-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="e8d81-280">RU 費用會根據 hello 傳回項目數目而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e8d81-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="e8d81-281">利用此資訊，我們可以估計 hello RU 需求的作業和我們預期每秒查詢這個應用程式指定 hello 號碼：</span><span class="sxs-lookup"><span data-stu-id="e8d81-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="e8d81-282">作業/查詢</span><span class="sxs-lookup"><span data-stu-id="e8d81-282">Operation/Query</span></span> | <span data-ttu-id="e8d81-283">每秒估計的數目</span><span class="sxs-lookup"><span data-stu-id="e8d81-283">Estimated number per second</span></span> | <span data-ttu-id="e8d81-284">必要的 RU 數</span><span class="sxs-lookup"><span data-stu-id="e8d81-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8d81-285">建立項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-285">Create item</span></span> |<span data-ttu-id="e8d81-286">10</span><span class="sxs-lookup"><span data-stu-id="e8d81-286">10</span></span> |<span data-ttu-id="e8d81-287">150</span><span class="sxs-lookup"><span data-stu-id="e8d81-287">150</span></span> |
| <span data-ttu-id="e8d81-288">讀取項目</span><span class="sxs-lookup"><span data-stu-id="e8d81-288">Read item</span></span> |<span data-ttu-id="e8d81-289">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-289">100</span></span> |<span data-ttu-id="e8d81-290">100</span><span class="sxs-lookup"><span data-stu-id="e8d81-290">100</span></span> |
| <span data-ttu-id="e8d81-291">依製造商選取食物</span><span class="sxs-lookup"><span data-stu-id="e8d81-291">Select foods by manufacturer</span></span> |<span data-ttu-id="e8d81-292">25</span><span class="sxs-lookup"><span data-stu-id="e8d81-292">25</span></span> |<span data-ttu-id="e8d81-293">175</span><span class="sxs-lookup"><span data-stu-id="e8d81-293">175</span></span> |
| <span data-ttu-id="e8d81-294">依食物群組選取</span><span class="sxs-lookup"><span data-stu-id="e8d81-294">Select by food group</span></span> |<span data-ttu-id="e8d81-295">10</span><span class="sxs-lookup"><span data-stu-id="e8d81-295">10</span></span> |<span data-ttu-id="e8d81-296">700</span><span class="sxs-lookup"><span data-stu-id="e8d81-296">700</span></span> |
| <span data-ttu-id="e8d81-297">選取前 10 個</span><span class="sxs-lookup"><span data-stu-id="e8d81-297">Select top 10</span></span> |<span data-ttu-id="e8d81-298">15</span><span class="sxs-lookup"><span data-stu-id="e8d81-298">15</span></span> |<span data-ttu-id="e8d81-299">總共 150 個</span><span class="sxs-lookup"><span data-stu-id="e8d81-299">150 Total</span></span> |

<span data-ttu-id="e8d81-300">在此情況下，我們預期平均輸送量需求為 1,275 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="e8d81-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="e8d81-301">四捨五入為最接近 100 toohello，我們會佈建 1300 RU/秒針對此應用程式的集合。</span><span class="sxs-lookup"><span data-stu-id="e8d81-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="e8d81-302"><a id="RequestRateTooLarge"></a> 超過 Azure Cosmos DB 中保留的輸送量限制</span><span class="sxs-lookup"><span data-stu-id="e8d81-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="e8d81-303">前文提過要求單位耗用量會評估為每秒的速率，是否是空的 hello 預算。</span><span class="sxs-lookup"><span data-stu-id="e8d81-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="e8d81-304">超過 hello 的應用程式的佈建的要求單位容器中，要求速率 toothat 集合將會受到節流，直到 hello 速率低於 hello 保留層級。</span><span class="sxs-lookup"><span data-stu-id="e8d81-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="e8d81-305">Hello RequestRateTooLargeException （HTTP 狀態碼 429） 要求，並傳回 hello x ms-重試-之後-ms 標頭指出 hello 一段時間，以毫秒為單位，hello 使用者之前，必須等候，節流發生時，會先結束 hello 伺服器本項 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="e8d81-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="e8d81-306">如果您打算 hello.NET 用戶端 SDK 和 LINQ 查詢，大部分的 hello 您永遠不會有 toodeal 與這個例外狀況，如 hello 目前版本的.NET 用戶端 SDK hello 隱含攔截這個回應的時間，方面 hello 伺服器指定 retry-after 標頭，並重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="e8d81-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="e8d81-307">除非正在多個用戶端同時存取您的帳戶，將會成功 hello 下次重試。</span><span class="sxs-lookup"><span data-stu-id="e8d81-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="e8d81-308">如果您有多個用戶端累積運作 hello 要求率超過 hello 預設重試行為可能不敷使用，並 hello 用戶端將會擲回狀態碼 429 toohello 應用程式與 DocumentClientException。</span><span class="sxs-lookup"><span data-stu-id="e8d81-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="e8d81-309">在這類情況下，您可以考慮處理重試行和您的應用程式錯誤處理常式，或增加 hello 保留的輸送量 hello 容器中的邏輯。</span><span class="sxs-lookup"><span data-stu-id="e8d81-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="e8d81-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> 超過 API for MongoDB 中保留的輸送量限制</span><span class="sxs-lookup"><span data-stu-id="e8d81-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="e8d81-311">超過集合的佈建的 hello 要求單位的應用程式將會受到節流，直到 hello 速率低於 hello 保留層級。</span><span class="sxs-lookup"><span data-stu-id="e8d81-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="e8d81-312">Hello 後端節流發生時，會先結束 hello 要求*16500*錯誤碼-*太多要求*。</span><span class="sxs-lookup"><span data-stu-id="e8d81-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="e8d81-313">根據預設，應用程式開發介面 for MongoDB。 將自動重試 too10 時間傳回前*太多要求*錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="e8d81-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="e8d81-314">如果您收到許多*太多要求*錯誤代碼，您可以考慮在您的應用程式錯誤處理常式中任一加入重試行或[提高 hello 集合hello保留的輸送量](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="e8d81-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8d81-315">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8d81-315">Next steps</span></span>
<span data-ttu-id="e8d81-316">深入了解 Azure Cosmos DB 資料庫使用保留輸送量 toolearn 瀏覽這些資源：</span><span class="sxs-lookup"><span data-stu-id="e8d81-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="e8d81-317">Azure Cosmos DB 定價</span><span class="sxs-lookup"><span data-stu-id="e8d81-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="e8d81-318">在 Azure Cosmos DB 中分割資料</span><span class="sxs-lookup"><span data-stu-id="e8d81-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="e8d81-319">toolearn 深入了解 Azure Cosmos DB，請參閱 hello Azure Cosmos DB[文件](https://azure.microsoft.com/documentation/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="e8d81-320">tooget 入門規模和效能測試以 Azure Cosmos DB，請參閱[效能與延展測試 Azure Cosmos db](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d81-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
