---
title: "Azure Cosmos DB 中的資料分割和水平調整 | Microsoft Docs"
description: "了解資料分割在 Azure Cosmos DB 中的運作方式、如何設定資料分割和資料分割索引鍵，以及如何為您的應用程式挑選合適的資料分割索引鍵。"
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2d2847276e553d7511241ff323c3e00aad8e5c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a><span data-ttu-id="08c74-103">如何在 Azure Cosmos DB 中進行資料分割和調整</span><span class="sxs-lookup"><span data-stu-id="08c74-103">How to partition and scale in Azure Cosmos DB</span></span>

<span data-ttu-id="08c74-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是全域分散的多重模型資料庫服務，其設計可協助您達成快速且可預測的效能，並順暢地隨著應用程式的成長而調整規模。</span><span class="sxs-lookup"><span data-stu-id="08c74-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="08c74-105">本文概述 Azure Cosmos DB 中所有資料模型的資料分割運作方式的概觀，並描述可如何設定 Azure Cosmos DB 容器以有效地調整應用程式規模。</span><span class="sxs-lookup"><span data-stu-id="08c74-105">This article provides an overview of how partitioning works for all the data models in Azure Cosmos DB, and describes how you can configure Azure Cosmos DB containers to effectively scale your applications.</span></span>

<span data-ttu-id="08c74-106">Scott Hanselman 和 Azure Cosmos DB 工程總經理 Shireesh Thota 也會在這段 Azure Friday 影片中說明資料分割和資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-106">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and Azure Cosmos DB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a><span data-ttu-id="08c74-107">Azure Cosmos DB 中的資料分割</span><span class="sxs-lookup"><span data-stu-id="08c74-107">Partitioning in Azure Cosmos DB</span></span>
<span data-ttu-id="08c74-108">您在 Azure Cosmos DB 中可儲存及查詢無結構描述的資料，以及任何規模的毫秒順序回應時間。</span><span class="sxs-lookup"><span data-stu-id="08c74-108">In Azure Cosmos DB, you can store and query schema-less data with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="08c74-109">Cosmos DB 提供存放資料的容器，稱為**集合 (適用於文件)、圖形或資料表**。</span><span class="sxs-lookup"><span data-stu-id="08c74-109">Cosmos DB provides containers for storing data called **collections (for document), graphs, or tables**.</span></span> <span data-ttu-id="08c74-110">容器是邏輯資源，可以跨一或多個實體分割或伺服器。</span><span class="sxs-lookup"><span data-stu-id="08c74-110">Containers are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="08c74-111">資料分割數目取決於 Cosmos DB 的儲存體大小與佈建的容器輸送量。</span><span class="sxs-lookup"><span data-stu-id="08c74-111">The number of partitions is determined by Cosmos DB based on the storage size and the provisioned throughput of the container.</span></span> <span data-ttu-id="08c74-112">Cosmos DB 中的每個分割都有其相關聯的固定 SSD 支援儲存體數量，並且複寫以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="08c74-112">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="08c74-113">分割管理完全是由 Azure Cosmos DB 所管理，您不需要撰寫複雜程式碼或管理分割。</span><span class="sxs-lookup"><span data-stu-id="08c74-113">Partition management is fully managed by Azure Cosmos DB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="08c74-114">Cosmos DB 容器在儲存體和輸送量方面並無限制。</span><span class="sxs-lookup"><span data-stu-id="08c74-114">Cosmos DB containers are unlimited in terms of storage and throughput.</span></span> 

![水平](./media/introduction/azure-cosmos-db-partitioning.png) 

<span data-ttu-id="08c74-116">資料分割對應用程式而言是透明的作業。</span><span class="sxs-lookup"><span data-stu-id="08c74-116">Partitioning is transparent to your application.</span></span> <span data-ttu-id="08c74-117">Cosmos DB 支援快速的讀取與寫入、查詢、交易邏輯、一致性層級，以及透過方法/API 對單一容器資源進行更細微的存取控制。</span><span class="sxs-lookup"><span data-stu-id="08c74-117">Cosmos DB supports fast reads and writes, queries, transactional logic, consistency levels, and fine-grained access control via methods/APIs to a single container resource.</span></span> <span data-ttu-id="08c74-118">此服務會處理跨資料分割所分散的資料，以及將查詢要求路由傳送至正確的資料分割。</span><span class="sxs-lookup"><span data-stu-id="08c74-118">The service handles distributing data across partitions and routing query requests to the right partition.</span></span> 

<span data-ttu-id="08c74-119">資料分割如何運作？</span><span class="sxs-lookup"><span data-stu-id="08c74-119">How does partitioning work?</span></span> <span data-ttu-id="08c74-120">每個項目必須具備可唯一識別它的資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-120">Each item must have a partition key and a row key, which uniquely identify it.</span></span> <span data-ttu-id="08c74-121">您的資料分割索引鍵是存放資料的邏輯資料分割區，並為 Cosmos DB 提供將資料分散到分割區的自然界限。</span><span class="sxs-lookup"><span data-stu-id="08c74-121">Your partition key acts as a logical partition for your data, and provides Cosmos DB with a natural boundary for distributing data across partitions.</span></span> <span data-ttu-id="08c74-122">簡單地說，Azure Cosmos DB 中的資料分割運作方式如下︰</span><span class="sxs-lookup"><span data-stu-id="08c74-122">In brief, here is how partitioning works in Azure Cosmos DB:</span></span>

* <span data-ttu-id="08c74-123">您使用 `T` 要求/秒的輸送量佈建 Cosmos DB 容器</span><span class="sxs-lookup"><span data-stu-id="08c74-123">You provision a Cosmos DB container with `T` requests/s throughput</span></span>
* <span data-ttu-id="08c74-124">Cosmos DB 會在幕後佈建服務 `T` 要求/秒所需的分割區。</span><span class="sxs-lookup"><span data-stu-id="08c74-124">Behind the scenes, Cosmos DB provisions partitions needed to serve `T` requests/s.</span></span> <span data-ttu-id="08c74-125">如果 `T` 超過每一分割區的最大輸送量 `t`，Cosmos DB 會佈建 `N` = `T/t` 分割區</span><span class="sxs-lookup"><span data-stu-id="08c74-125">If `T` is higher than the maximum throughput per partition `t`, then Cosmos DB provisions `N` = `T/t` partitions</span></span>
* <span data-ttu-id="08c74-126">Cosmos DB 會在 `N` 分割區平均地配置資料分割索引鍵雜湊的索引鍵空間。</span><span class="sxs-lookup"><span data-stu-id="08c74-126">Cosmos DB allocates the key space of partition key hashes evenly across the `N` partitions.</span></span> <span data-ttu-id="08c74-127">因此，每個分割區 (實體分割區) 會裝載 1-N 個資料分割索引鍵值 (邏輯分割區)</span><span class="sxs-lookup"><span data-stu-id="08c74-127">So, each partition (physical partition) hosts 1-N partition key values (logical partitions)</span></span>
* <span data-ttu-id="08c74-128">當實體分割區 `p` 達到儲存體限制時，Cosmos DB 會以無縫方式將 `p` 分割成兩個新的分割區 `p1` 和 `p2`，並會分配相當於約索引鍵一半的值給每個分割區。</span><span class="sxs-lookup"><span data-stu-id="08c74-128">When a physical partition `p` reaches its storage limit, Cosmos DB seamlessly splits `p` into two new partitions `p1` and `p2` and distributes values corresponding to roughly half the keys to each of the partitions.</span></span> <span data-ttu-id="08c74-129">應用程式不會察覺此分割作業。</span><span class="sxs-lookup"><span data-stu-id="08c74-129">This split operation is invisible to your application.</span></span>
* <span data-ttu-id="08c74-130">同樣地，當您佈建超過 `t*N` 輸送量的輸送量時，Cosmos DB 會分割一或多個分割區以支援更高的輸送量</span><span class="sxs-lookup"><span data-stu-id="08c74-130">Similarly, when you provision throughput higher than `t*N` throughput, Cosmos DB splits one or more of your partitions to support the higher throughput</span></span>

<span data-ttu-id="08c74-131">資料分割索引鍵的語意會稍有不同，以符合各 API 的語意，如下表所示︰</span><span class="sxs-lookup"><span data-stu-id="08c74-131">The semantics for partition keys are slightly different to match the semantics of each API, as shown in the following table:</span></span>

| <span data-ttu-id="08c74-132">API</span><span class="sxs-lookup"><span data-stu-id="08c74-132">API</span></span> | <span data-ttu-id="08c74-133">資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="08c74-133">Partition Key</span></span> | <span data-ttu-id="08c74-134">列索引鍵</span><span class="sxs-lookup"><span data-stu-id="08c74-134">Row Key</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08c74-135">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="08c74-135">DocumentDB</span></span> | <span data-ttu-id="08c74-136">自訂資料分割索引鍵路徑</span><span class="sxs-lookup"><span data-stu-id="08c74-136">custom partition key path</span></span> | <span data-ttu-id="08c74-137">固定 `id`</span><span class="sxs-lookup"><span data-stu-id="08c74-137">fixed `id`</span></span> | 
| <span data-ttu-id="08c74-138">MongoDB</span><span class="sxs-lookup"><span data-stu-id="08c74-138">MongoDB</span></span> | <span data-ttu-id="08c74-139">自訂共用索引鍵</span><span class="sxs-lookup"><span data-stu-id="08c74-139">custom shard key</span></span>  | <span data-ttu-id="08c74-140">固定 `_id`</span><span class="sxs-lookup"><span data-stu-id="08c74-140">fixed `_id`</span></span> | 
| <span data-ttu-id="08c74-141">圖形</span><span class="sxs-lookup"><span data-stu-id="08c74-141">Graph</span></span> | <span data-ttu-id="08c74-142">自訂資料分割索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="08c74-142">custom partition key property</span></span> | <span data-ttu-id="08c74-143">固定 `id`</span><span class="sxs-lookup"><span data-stu-id="08c74-143">fixed `id`</span></span> | 
| <span data-ttu-id="08c74-144">資料表</span><span class="sxs-lookup"><span data-stu-id="08c74-144">Table</span></span> | <span data-ttu-id="08c74-145">固定 `PartitionKey`</span><span class="sxs-lookup"><span data-stu-id="08c74-145">fixed `PartitionKey`</span></span> | <span data-ttu-id="08c74-146">固定 `RowKey`</span><span class="sxs-lookup"><span data-stu-id="08c74-146">fixed `RowKey`</span></span> | 

<span data-ttu-id="08c74-147">Cosmos DB 使用雜湊型資料分割。</span><span class="sxs-lookup"><span data-stu-id="08c74-147">Cosmos DB uses hash-based partitioning.</span></span> <span data-ttu-id="08c74-148">當您寫入項目時，Cosmos DB 會將資料分割索引鍵值進行雜湊處理，然後使用雜湊的結果來判斷要在其中儲存項目的分割區。</span><span class="sxs-lookup"><span data-stu-id="08c74-148">When you write an item, Cosmos DB hashes the partition key value and use the hashed result to determine which partition to store the item in.</span></span> <span data-ttu-id="08c74-149">Cosmos DB 會將資料分割索引鍵相同的所有項目儲存在相同的實體分割區中。</span><span class="sxs-lookup"><span data-stu-id="08c74-149">Cosmos DB stores all items with the same partition key in the same physical partition.</span></span> <span data-ttu-id="08c74-150">選擇資料分割索引鍵是在設計階段必須進行的一項重要決策。</span><span class="sxs-lookup"><span data-stu-id="08c74-150">The choice of the partition key is an important decision that you have to make at design time.</span></span> <span data-ttu-id="08c74-151">您必須選擇具有各種不同的值並且有平均存取模式的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="08c74-151">You must pick a property name that has a wide range of values and has even access patterns.</span></span>

> [!NOTE]
> <span data-ttu-id="08c74-152">資料分割索引鍵最好有許多相異值 (至少數百至數千個)。</span><span class="sxs-lookup"><span data-stu-id="08c74-152">It is a best practice to have a partition key with many distinct values (100s-1000s at a minimum).</span></span>
>

<span data-ttu-id="08c74-153">Azure Cosmos DB 容器可視為「固定」或「無限制」。</span><span class="sxs-lookup"><span data-stu-id="08c74-153">Azure Cosmos DB containers can be created as "fixed" or "unlimited."</span></span> <span data-ttu-id="08c74-154">固定大小的容器具有上限為 10 GB 和 10,000 RU/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="08c74-154">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="08c74-155">某些 API 對於固定大小的容器可允許省略資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-155">Some APIs allow the partition key to be omitted for fixed-size containers.</span></span> <span data-ttu-id="08c74-156">若要建立無限制的容器，您必須指定最小輸送量 2500 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="08c74-156">To create a container as unlimited, you must specify a minimum throughput of 2500 RU/s.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="08c74-157">資料分割與佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="08c74-157">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="08c74-158">Cosmos DB 設計用來取得可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="08c74-158">Cosmos DB is designed for predictable performance.</span></span> <span data-ttu-id="08c74-159">當您建立容器時，可以根據每秒的[要求單位](request-units.md) (RU) 來為每分的 RU 預留輸送量。</span><span class="sxs-lookup"><span data-stu-id="08c74-159">When you create a container, you reserve throughput in terms of **[request units](request-units.md) (RU) per second with a potential add-on for RU per minute**.</span></span> <span data-ttu-id="08c74-160">每項要求都會指派有與系統資源 (例如作業所使用的 CPU、記憶體和 IO) 數量成正比的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="08c74-160">Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU, Memory, and IO consumed by the operation.</span></span> <span data-ttu-id="08c74-161">讀取 1 KB 具有工作階段一致性的文件，會使用 1 個要求單位。</span><span class="sxs-lookup"><span data-stu-id="08c74-161">A read of a 1-KB document with Session consistency consumes one request unit.</span></span> <span data-ttu-id="08c74-162">不論儲存的項目數或同時執行的並行要求數，讀取一次都是 1 個 RU。</span><span class="sxs-lookup"><span data-stu-id="08c74-162">A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time.</span></span> <span data-ttu-id="08c74-163">根據大小之不同，較大的項目需要較高的要求單位。</span><span class="sxs-lookup"><span data-stu-id="08c74-163">Larger items require higher request units depending on the size.</span></span> <span data-ttu-id="08c74-164">如果您知道實體大小以及支援您應用程式所需的讀取次數，則可以佈建應用程式讀取需求確實需要的輸送量。</span><span class="sxs-lookup"><span data-stu-id="08c74-164">If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs.</span></span> 

> [!NOTE]
> <span data-ttu-id="08c74-165">為達到容器的完整輸送量，您必須選擇資料分割索引鍵，讓您能將要求平均地分散到數個相異的資料分割索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="08c74-165">To achieve the full throughput of the container, you must choose a partition key that allows you to evenly distribute requests among some distinct partition key values.</span></span>
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a><span data-ttu-id="08c74-166">使用 Azure Cosmos DB API</span><span class="sxs-lookup"><span data-stu-id="08c74-166">Working with the Azure Cosmos DB APIs</span></span>
<span data-ttu-id="08c74-167">您可以使用 Azure 入口網站或 Azure CLI 建立容器，並在任何時間進行調整。</span><span class="sxs-lookup"><span data-stu-id="08c74-167">You can use the Azure portal or Azure CLI to create containers and scale them at any time.</span></span> <span data-ttu-id="08c74-168">本節說明如何建立容器，並在每個支援的 API 中指定輸送量和資料分割索引鍵定義。</span><span class="sxs-lookup"><span data-stu-id="08c74-168">This section shows how to create containers and specify the throughput and partition key definition in each of the supported APIs.</span></span>

### <a name="documentdb-api"></a><span data-ttu-id="08c74-169">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="08c74-169">DocumentDB API</span></span>
<span data-ttu-id="08c74-170">下列範例示範如何使用 DocumentDB API 建立容器 (集合)。</span><span class="sxs-lookup"><span data-stu-id="08c74-170">The following sample shows how to create a container (collection) using the DocumentDB API.</span></span> <span data-ttu-id="08c74-171">您可以在[使用 DocumentDB API 進行資料分割](partition-data.md)中找到更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="08c74-171">You can find more details in [Partitioning with DocumentDB API](partition-data.md).</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="08c74-172">您可以使用 REST API 中的 `GET` 方法或使用其中一個 SDK 中的 `ReadDocumentAsync` 來讀取項目 (文件)。</span><span class="sxs-lookup"><span data-stu-id="08c74-172">You can read an item (document) using the `GET` method in the REST API or using `ReadDocumentAsync` in one of the SDKs.</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a><span data-ttu-id="08c74-173">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="08c74-173">MongoDB API</span></span>
<span data-ttu-id="08c74-174">您可以使用 MongoDB API，透過您喜愛的工具、驅動程式或 SDK 建立分區化集合。</span><span class="sxs-lookup"><span data-stu-id="08c74-174">With the MongoDB API, you can create a sharded collection through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="08c74-175">在此範例中，我們使用 Mongo 殼層建立集合。</span><span class="sxs-lookup"><span data-stu-id="08c74-175">In this example, we use the Mongo Shell for the collection creation.</span></span>

<span data-ttu-id="08c74-176">在 Mongo 殼層中︰</span><span class="sxs-lookup"><span data-stu-id="08c74-176">In the Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="08c74-177">結果：</span><span class="sxs-lookup"><span data-stu-id="08c74-177">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a><span data-ttu-id="08c74-178">資料表 API</span><span class="sxs-lookup"><span data-stu-id="08c74-178">Table API</span></span>

<span data-ttu-id="08c74-179">使用資料表 API，可以在 appSettings 組態中為應用程式指定資料表的輸送量︰</span><span class="sxs-lookup"><span data-stu-id="08c74-179">With the Table API, you specify the throughput for tables in the appSettings configuration for your application:</span></span>

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

<span data-ttu-id="08c74-180">然後，您可以使用 Azure 資料表儲存體 SDK 建立資料表。</span><span class="sxs-lookup"><span data-stu-id="08c74-180">Then you create a table using the Azure Table storage SDK.</span></span> <span data-ttu-id="08c74-181">資料分割索引鍵會隱含地建立為 `PartitionKey` 值。</span><span class="sxs-lookup"><span data-stu-id="08c74-181">The partition key is implicitly created as the `PartitionKey` value.</span></span> 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

<span data-ttu-id="08c74-182">您可以使用下列程式碼片段來擷取單一實體：</span><span class="sxs-lookup"><span data-stu-id="08c74-182">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
<span data-ttu-id="08c74-183">如需詳細資訊，請參閱[使用資料表 API 進行開發](tutorial-develop-table-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="08c74-183">See [Developing with the Table API](tutorial-develop-table-dotnet.md) for more details.</span></span>

### <a name="graph-api"></a><span data-ttu-id="08c74-184">Graph API</span><span class="sxs-lookup"><span data-stu-id="08c74-184">Graph API</span></span>

<span data-ttu-id="08c74-185">使用 Graph API 時，必須使用 Azure 入口網站或 CLI 來建立容器。</span><span class="sxs-lookup"><span data-stu-id="08c74-185">With the Graph API, you must use the Azure portal or CLI to create containers.</span></span> <span data-ttu-id="08c74-186">此外，由於 Azure Cosmos DB 是多重模型，您可以使用其中一種其他模型來建立及調整您的圖形容器。</span><span class="sxs-lookup"><span data-stu-id="08c74-186">Alternatively, since Azure Cosmos DB is multi-model, you can use one of the other models to create and scale your graph container.</span></span>

<span data-ttu-id="08c74-187">您可以在 Gremlin 中使用資料分割索引鍵和識別碼來判讀任何頂點或邊緣。</span><span class="sxs-lookup"><span data-stu-id="08c74-187">You can read any vertex or edge using the partition key and id in Gremlin.</span></span> <span data-ttu-id="08c74-188">例如，對於使用區域 (美國) 做為資料分割索引鍵和使用「西雅圖」做為資料列索引鍵的圖形，您可以使用下列語法找到頂點︰</span><span class="sxs-lookup"><span data-stu-id="08c74-188">For example, for a graph with region ("USA") as the partition key, and "Seattle" as the row key, you can find a vertex using the following syntax:</span></span>

```
g.V(['USA', 'Seattle'])
```

<span data-ttu-id="08c74-189">如同許多邊緣，您可以使用資料分割索引鍵和資料列索引鍵來參考某個邊緣。</span><span class="sxs-lookup"><span data-stu-id="08c74-189">Same with edges, you can reference an edge using the partition key and row key.</span></span>

```
g.E(['USA', 'I5'])
```

<span data-ttu-id="08c74-190">如需詳細資訊，請參閱 [Cosmos DB 的 Gremlin 支援](gremlin-support.md)。</span><span class="sxs-lookup"><span data-stu-id="08c74-190">See [Gremlin support for Cosmos DB](gremlin-support.md) for more details.</span></span>


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="08c74-191">設計資料分割</span><span class="sxs-lookup"><span data-stu-id="08c74-191">Designing for partitioning</span></span>
<span data-ttu-id="08c74-192">若要使用 Azure Cosmos DB 進行有效調整，您必須在建立容器時挑選適當的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-192">To scale effectively with Azure Cosmos DB, you need to pick a good partition key when you create your container.</span></span> <span data-ttu-id="08c74-193">選擇資料分割索引鍵時有兩個重要考量︰</span><span class="sxs-lookup"><span data-stu-id="08c74-193">There are two key considerations for choosing a partition key:</span></span>

* <span data-ttu-id="08c74-194">**查詢和交易的界限**：您選擇的資料分割索引鍵應兼顧交易使用和將實體分散到多個資料分割索引鍵 (以確保可調整的解決方案) 的需求。</span><span class="sxs-lookup"><span data-stu-id="08c74-194">**Boundary for query and transactions**: Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution.</span></span> <span data-ttu-id="08c74-195">以一個極端的情況來說，您可以針對所有項目設定相同的資料分割索引鍵，但如此可能會限制解決方案的延展性。</span><span class="sxs-lookup"><span data-stu-id="08c74-195">At one extreme, you could set the same partition key for all your items, but this may limit the scalability of your solution.</span></span> <span data-ttu-id="08c74-196">以另一個極端而言，您可以為每個項目指派唯一的資料分割索引鍵以達到高調整性，但如此會透過預存程序和觸發程序，讓您無法使用跨文件交易。</span><span class="sxs-lookup"><span data-stu-id="08c74-196">At the other extreme, you could assign a unique partition key for each item, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="08c74-197">理想的分割區索引鍵可讓您使用有效率的查詢，而且具有足夠的基數，可確保您的解決方案能加以調整。</span><span class="sxs-lookup"><span data-stu-id="08c74-197">An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable.</span></span> 
* <span data-ttu-id="08c74-198">**沒有儲存體和效能瓶頸**︰請務必選取允許寫入分散到不同相異值的屬性。</span><span class="sxs-lookup"><span data-stu-id="08c74-198">**No storage and performance bottlenecks**: It is important to pick a property that allows writes to be distributed across various distinct values.</span></span> <span data-ttu-id="08c74-199">相同資料分割索引鍵的要求不能超過單一分割區的輸送量，因此會進行節流。</span><span class="sxs-lookup"><span data-stu-id="08c74-199">Requests to the same partition key cannot exceed the throughput of a single partition, and are throttled.</span></span> <span data-ttu-id="08c74-200">因此，請務必挑選不會在應用程式內導致「作用點」的分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-200">So it is important to pick a partition key that does not result in "hot spots" within your application.</span></span> <span data-ttu-id="08c74-201">因為單一分割索引鍵的所有資料皆必須儲存在資料分割中，也建議在遇到有大量相同值的資料時，避免分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-201">Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value.</span></span> 

<span data-ttu-id="08c74-202">來看看一些真實案例和每個案例良好的資料分割索引鍵︰</span><span class="sxs-lookup"><span data-stu-id="08c74-202">Let's look at a few real-world scenarios, and good partition keys for each:</span></span>
* <span data-ttu-id="08c74-203">如果您實作使用者設定檔後端，則使用者識別碼是不錯的資料分割索引鍵選擇。</span><span class="sxs-lookup"><span data-stu-id="08c74-203">If you’re implementing a user profile backend, then the user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="08c74-204">如果您在儲存 IoT 資料 (例如，裝置狀態)，則裝置識別碼是不錯的資料分割索引鍵選擇。</span><span class="sxs-lookup"><span data-stu-id="08c74-204">If you’re storing IoT data for example, device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="08c74-205">如果您使用 Azure Cosmos DB 來記錄時間序列資料，則主機名稱或處理序識別碼很適合作為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-205">If you’re using Azure Cosmos DB for logging time-series data, then the hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="08c74-206">如果您有多重租用戶架構，租用戶識別碼是不錯的資料分割索引鍵選擇。</span><span class="sxs-lookup"><span data-stu-id="08c74-206">If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="08c74-207">在一些使用案例 (例如 IoT 與使用者設定檔) 中，資料分割索引鍵可能與您的識別碼 (文件索引鍵) 相同。</span><span class="sxs-lookup"><span data-stu-id="08c74-207">In some use cases like IoT and user profiles, the partition key might be the same as your id (document key).</span></span> <span data-ttu-id="08c74-208">在其他使用案例 (例如時間序列資料) 中，您的資料分割索引鍵可能與識別碼不同。</span><span class="sxs-lookup"><span data-stu-id="08c74-208">In others like the time series data, you might have a partition key that’s different than the id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="08c74-209">資料分割和記錄/時間序列資料</span><span class="sxs-lookup"><span data-stu-id="08c74-209">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="08c74-210">Cosmos DB 常見的其中一個使用案例是用在記錄與遙測。</span><span class="sxs-lookup"><span data-stu-id="08c74-210">One of the common use cases of Cosmos DB is for logging and telemetry.</span></span> <span data-ttu-id="08c74-211">您可能需要讀取/寫入大量資料，因此請務必挑選適當的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08c74-211">It is important to pick a good partition key since you might need to read/write vast volumes of data.</span></span> <span data-ttu-id="08c74-212">要做什麼選擇取決於讀取和寫入速率以及您預期要執行的查詢類型。</span><span class="sxs-lookup"><span data-stu-id="08c74-212">The choice depends on your read and write rates and kinds of queries you expect to run.</span></span> <span data-ttu-id="08c74-213">如何選擇適當資料分割索引鍵的一些秘訣如下。</span><span class="sxs-lookup"><span data-stu-id="08c74-213">Here are some tips on how to choose a good partition key.</span></span>

* <span data-ttu-id="08c74-214">如果您的使用案例牽涉到以較小的速率寫入已累積很長一段時間的資料，而且必須依時間戳記範圍和其他篩選器進行查詢，則使用彙總的時間戳記 (例如日期) 做為資料分割索引鍵是不錯的方法。</span><span class="sxs-lookup"><span data-stu-id="08c74-214">If your use case involves a small rate of writes accumulating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp, for example,  date as a partition key is a good approach.</span></span> <span data-ttu-id="08c74-215">這可讓您查詢單一資料分割中某一天的所有資料。</span><span class="sxs-lookup"><span data-stu-id="08c74-215">This allows you to query over all the data for a date from a single partition.</span></span> 
* <span data-ttu-id="08c74-216">如果您的寫入工作負載繁重 (這是更常見的情形)，則不應該使用根據時間戳記的資料分割索引鍵，這樣一來，Cosmos DB 才可以將寫入工作平均分散到多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="08c74-216">If your workload is written heavy, which is more common, you should use a partition key that’s not based on timestamp so that Cosmos DB can distribute writes evenly across various partitions.</span></span> <span data-ttu-id="08c74-217">在這個案例中，主機名稱、處理序識別碼、活動識別碼或其他具有高基數的屬性是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="08c74-217">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="08c74-218">第三種方法是混合式方法，在此方法中您會擁有多個容器，每天/每月各有一個容器，而且資料分割索引鍵是細微的屬性，例如主機名稱。</span><span class="sxs-lookup"><span data-stu-id="08c74-218">A third approach is a hybrid one where you have multiple containers, one for each day/month and the partition key is a granular property like hostname.</span></span> <span data-ttu-id="08c74-219">這樣的好處是，您可以根據時間範圍設定不同的輸送量，例如當月的容器會佈建較高的輸送量，因為它要處理讀取和寫入，而先前月份則佈建較低的輸送量，因為它們只要處理讀取。</span><span class="sxs-lookup"><span data-stu-id="08c74-219">This has the benefit that you can set different throughput based on the time window, for example, the container for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="08c74-220">資料分割與多重租用</span><span class="sxs-lookup"><span data-stu-id="08c74-220">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="08c74-221">如果您使用 Cosmos DB 實作多重租用戶應用程式，有兩種常見的模式：一個租用戶一個資料分割索引鍵，和一個租用戶一個容器。</span><span class="sxs-lookup"><span data-stu-id="08c74-221">If you are implementing a multi-tenant application using Cosmos DB, there are two popular patterns – one partition key per tenant, and one container per tenant.</span></span> <span data-ttu-id="08c74-222">以下是每項方式的優缺點︰</span><span class="sxs-lookup"><span data-stu-id="08c74-222">Here are the pros and cons for each:</span></span>

* <span data-ttu-id="08c74-223">一個租用戶一個資料分割索引鍵：在此模型中，租用戶共置於單一容器內。</span><span class="sxs-lookup"><span data-stu-id="08c74-223">One Partition Key per tenant: In this model, tenants are collocated within a single container.</span></span> <span data-ttu-id="08c74-224">但是，針對單一資料分割，可以執行單一租用戶內項目的查詢與插入。</span><span class="sxs-lookup"><span data-stu-id="08c74-224">But queries and inserts for items within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="08c74-225">您也可以跨租用戶內的所有項目實作交易邏輯。</span><span class="sxs-lookup"><span data-stu-id="08c74-225">You can also implement transactional logic across all items within a tenant.</span></span> <span data-ttu-id="08c74-226">因為多重租用戶共用一個容器，所以您可以節省儲存體和輸送量成本，方法是在單一容器內輪詢租用戶的資源，而不是為每個租用戶佈建額外的空餘空間。</span><span class="sxs-lookup"><span data-stu-id="08c74-226">Since multiple tenants share a container, you can save storage and throughput costs by pooling resources for tenants within a single container rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="08c74-227">缺點是未隔離每個租用戶的效能。</span><span class="sxs-lookup"><span data-stu-id="08c74-227">The drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="08c74-228">整個容器的效能/輸送量增加與鎖定特定租用戶的增加。</span><span class="sxs-lookup"><span data-stu-id="08c74-228">Performance/throughput increases apply to the entire container vs targeted increases for tenants.</span></span>
* <span data-ttu-id="08c74-229">一個租用戶一個容器：每個租用戶都有其專屬容器。</span><span class="sxs-lookup"><span data-stu-id="08c74-229">One Container per tenant: Each tenant has its own container.</span></span> <span data-ttu-id="08c74-230">在此模型中，您可以保留每個租用戶的效能。</span><span class="sxs-lookup"><span data-stu-id="08c74-230">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="08c74-231">使用 Cosmos DB 全新的佈建計價模式，這種模式對於具有少數租用戶的多重租用戶應用程式最具成本效益。</span><span class="sxs-lookup"><span data-stu-id="08c74-231">With Cosmos DB's new provisioning pricing model, this model is more cost-effective for multi-tenant applications with a few tenants.</span></span>

<span data-ttu-id="08c74-232">您也可以使用組合/分層的方式，來共置少數租用戶，並將較大的租用戶移轉到其專屬容器。</span><span class="sxs-lookup"><span data-stu-id="08c74-232">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08c74-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08c74-233">Next steps</span></span>
<span data-ttu-id="08c74-234">在本文中，我們提供使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀。</span><span class="sxs-lookup"><span data-stu-id="08c74-234">In this article, we provided an overview for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="08c74-235">了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="08c74-235">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>
* <span data-ttu-id="08c74-236">了解 [Azure Cosmos DB 中的全域分散](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="08c74-236">Learn about [global distribution in Azure Cosmos DB](distribute-data-globally.md)</span></span>



