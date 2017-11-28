---
title: "aaaPartitioning 和 Azure Cosmos DB 中的水平延展 |Microsoft 文件"
description: "了解有關如何分割 Azure Cosmos DB 的運作方式、 如何 tooconfigure 資料分割和資料分割索引鍵，和如何 toopick hello 右資料分割索引鍵應用程式。"
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
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a><span data-ttu-id="b4cf6-103">如何 toopartition 和 Azure Cosmos DB 中的小數位數</span><span class="sxs-lookup"><span data-stu-id="b4cf6-103">How toopartition and scale in Azure Cosmos DB</span></span>

<span data-ttu-id="b4cf6-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)是全域的分散式、 多模型資料庫服務，其設計 toohelp 您達成快速、 可預測的效能和擴充順暢地連同應用程式的成長。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="b4cf6-105">本文章提供如何分割適用於所有 hello 資料模型在 Azure Cosmos DB 中，並說明如何設定 Azure Cosmos DB 容器 tooeffectively 延展您的應用程式的概觀。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-105">This article provides an overview of how partitioning works for all hello data models in Azure Cosmos DB, and describes how you can configure Azure Cosmos DB containers tooeffectively scale your applications.</span></span>

<span data-ttu-id="b4cf6-106">Scott Hanselman 和 Azure Cosmos DB 工程總經理 Shireesh Thota 也會在這段 Azure Friday 影片中說明資料分割和資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-106">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and Azure Cosmos DB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a><span data-ttu-id="b4cf6-107">Azure Cosmos DB 中的資料分割</span><span class="sxs-lookup"><span data-stu-id="b4cf6-107">Partitioning in Azure Cosmos DB</span></span>
<span data-ttu-id="b4cf6-108">您在 Azure Cosmos DB 中可儲存及查詢無結構描述的資料，以及任何規模的毫秒順序回應時間。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-108">In Azure Cosmos DB, you can store and query schema-less data with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="b4cf6-109">Cosmos DB 提供存放資料的容器，稱為**集合 (適用於文件)、圖形或資料表**。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-109">Cosmos DB provides containers for storing data called **collections (for document), graphs, or tables**.</span></span> <span data-ttu-id="b4cf6-110">容器是邏輯資源，可以跨一或多個實體分割或伺服器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-110">Containers are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="b4cf6-111">資料分割的 hello 數目取決於 Cosmos DB hello 儲存體大小和 hello 佈建的輸送量 hello 容器的基礎。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-111">hello number of partitions is determined by Cosmos DB based on hello storage size and hello provisioned throughput of hello container.</span></span> <span data-ttu-id="b4cf6-112">Cosmos DB 中的每個分割都有其相關聯的固定 SSD 支援儲存體數量，並且複寫以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-112">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="b4cf6-113">資料分割管理完全受 Azure Cosmos DB，且您沒有 toowrite 複雜的程式碼或管理您的資料分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-113">Partition management is fully managed by Azure Cosmos DB, and you do not have toowrite complex code or manage your partitions.</span></span> <span data-ttu-id="b4cf6-114">Cosmos DB 容器在儲存體和輸送量方面並無限制。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-114">Cosmos DB containers are unlimited in terms of storage and throughput.</span></span> 

![水平](./media/introduction/azure-cosmos-db-partitioning.png) 

<span data-ttu-id="b4cf6-116">資料分割是透明的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-116">Partitioning is transparent tooyour application.</span></span> <span data-ttu-id="b4cf6-117">Cosmos DB 支援快速讀取和寫入、 查詢、 交易式的邏輯、 一致性層級，以及透過方法/Api tooa 單一容器資源的更細緻的存取控制。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-117">Cosmos DB supports fast reads and writes, queries, transactional logic, consistency levels, and fine-grained access control via methods/APIs tooa single container resource.</span></span> <span data-ttu-id="b4cf6-118">將資料分散到資料分割和路由查詢要求 toohello 正確的資料分割，hello 服務控制代碼。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-118">hello service handles distributing data across partitions and routing query requests toohello right partition.</span></span> 

<span data-ttu-id="b4cf6-119">資料分割如何運作？</span><span class="sxs-lookup"><span data-stu-id="b4cf6-119">How does partitioning work?</span></span> <span data-ttu-id="b4cf6-120">每個項目必須具備可唯一識別它的資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-120">Each item must have a partition key and a row key, which uniquely identify it.</span></span> <span data-ttu-id="b4cf6-121">您的資料分割索引鍵是存放資料的邏輯資料分割區，並為 Cosmos DB 提供將資料分散到分割區的自然界限。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-121">Your partition key acts as a logical partition for your data, and provides Cosmos DB with a natural boundary for distributing data across partitions.</span></span> <span data-ttu-id="b4cf6-122">簡單地說，Azure Cosmos DB 中的資料分割運作方式如下︰</span><span class="sxs-lookup"><span data-stu-id="b4cf6-122">In brief, here is how partitioning works in Azure Cosmos DB:</span></span>

* <span data-ttu-id="b4cf6-123">您使用 `T` 要求/秒的輸送量佈建 Cosmos DB 容器</span><span class="sxs-lookup"><span data-stu-id="b4cf6-123">You provision a Cosmos DB container with `T` requests/s throughput</span></span>
* <span data-ttu-id="b4cf6-124">Hello 幕後 Cosmos DB 佈建資料分割需要 tooserve`T`要求/秒。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-124">Behind hello scenes, Cosmos DB provisions partitions needed tooserve `T` requests/s.</span></span> <span data-ttu-id="b4cf6-125">如果`T`高於 hello 每個分割區的最大輸送量`t`，然後佈建 Cosmos DB `N`  =  `T/t`資料分割</span><span class="sxs-lookup"><span data-stu-id="b4cf6-125">If `T` is higher than hello maximum throughput per partition `t`, then Cosmos DB provisions `N` = `T/t` partitions</span></span>
* <span data-ttu-id="b4cf6-126">Cosmos DB 配置 hello 金鑰空間的資料分割索引鍵的雜湊平均跨 hello`N`資料分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-126">Cosmos DB allocates hello key space of partition key hashes evenly across hello `N` partitions.</span></span> <span data-ttu-id="b4cf6-127">因此，每個分割區 (實體分割區) 會裝載 1-N 個資料分割索引鍵值 (邏輯分割區)</span><span class="sxs-lookup"><span data-stu-id="b4cf6-127">So, each partition (physical partition) hosts 1-N partition key values (logical partitions)</span></span>
* <span data-ttu-id="b4cf6-128">當實體資料分割`p`達到其儲存體限制，Cosmos DB 順暢地分割`p`分成兩個新的分割`p1`和`p2`及散發 tooroughly 半 hello 金鑰 tooeach 的 hello 的對應值資料分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-128">When a physical partition `p` reaches its storage limit, Cosmos DB seamlessly splits `p` into two new partitions `p1` and `p2` and distributes values corresponding tooroughly half hello keys tooeach of hello partitions.</span></span> <span data-ttu-id="b4cf6-129">這個分割作業是不可見的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-129">This split operation is invisible tooyour application.</span></span>
* <span data-ttu-id="b4cf6-130">同樣地，當您佈建輸送量高於時`t*N`一或多個程式磁碟分割 toosupport hello 較高的輸送量，輸送量，Cosmos DB 分割</span><span class="sxs-lookup"><span data-stu-id="b4cf6-130">Similarly, when you provision throughput higher than `t*N` throughput, Cosmos DB splits one or more of your partitions toosupport hello higher throughput</span></span>

<span data-ttu-id="b4cf6-131">資料分割索引鍵的 hello 語意會稍有不同的 toomatch hello 語意的每個 API，hello 下表中所示：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-131">hello semantics for partition keys are slightly different toomatch hello semantics of each API, as shown in hello following table:</span></span>

| <span data-ttu-id="b4cf6-132">API</span><span class="sxs-lookup"><span data-stu-id="b4cf6-132">API</span></span> | <span data-ttu-id="b4cf6-133">資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="b4cf6-133">Partition Key</span></span> | <span data-ttu-id="b4cf6-134">列索引鍵</span><span class="sxs-lookup"><span data-stu-id="b4cf6-134">Row Key</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4cf6-135">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b4cf6-135">DocumentDB</span></span> | <span data-ttu-id="b4cf6-136">自訂資料分割索引鍵路徑</span><span class="sxs-lookup"><span data-stu-id="b4cf6-136">custom partition key path</span></span> | <span data-ttu-id="b4cf6-137">固定 `id`</span><span class="sxs-lookup"><span data-stu-id="b4cf6-137">fixed `id`</span></span> | 
| <span data-ttu-id="b4cf6-138">MongoDB</span><span class="sxs-lookup"><span data-stu-id="b4cf6-138">MongoDB</span></span> | <span data-ttu-id="b4cf6-139">自訂共用索引鍵</span><span class="sxs-lookup"><span data-stu-id="b4cf6-139">custom shard key</span></span>  | <span data-ttu-id="b4cf6-140">固定 `_id`</span><span class="sxs-lookup"><span data-stu-id="b4cf6-140">fixed `_id`</span></span> | 
| <span data-ttu-id="b4cf6-141">圖形</span><span class="sxs-lookup"><span data-stu-id="b4cf6-141">Graph</span></span> | <span data-ttu-id="b4cf6-142">自訂資料分割索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="b4cf6-142">custom partition key property</span></span> | <span data-ttu-id="b4cf6-143">固定 `id`</span><span class="sxs-lookup"><span data-stu-id="b4cf6-143">fixed `id`</span></span> | 
| <span data-ttu-id="b4cf6-144">資料表</span><span class="sxs-lookup"><span data-stu-id="b4cf6-144">Table</span></span> | <span data-ttu-id="b4cf6-145">固定 `PartitionKey`</span><span class="sxs-lookup"><span data-stu-id="b4cf6-145">fixed `PartitionKey`</span></span> | <span data-ttu-id="b4cf6-146">固定 `RowKey`</span><span class="sxs-lookup"><span data-stu-id="b4cf6-146">fixed `RowKey`</span></span> | 

<span data-ttu-id="b4cf6-147">Cosmos DB 使用雜湊型資料分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-147">Cosmos DB uses hash-based partitioning.</span></span> <span data-ttu-id="b4cf6-148">當您撰寫一個項目時，Cosmos DB 雜湊 hello 資料分割索引鍵值，並使用 hello 雜湊結果 toodetermine 中的哪一個資料分割 toostore hello 項目。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-148">When you write an item, Cosmos DB hashes hello partition key value and use hello hashed result toodetermine which partition toostore hello item in.</span></span> <span data-ttu-id="b4cf6-149">所有的項目與 hello 中相同的資料分割索引鍵的 cosmos DB 存放區 hello 相同實體磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-149">Cosmos DB stores all items with hello same partition key in hello same physical partition.</span></span> <span data-ttu-id="b4cf6-150">hello 選擇 hello 資料分割索引鍵是您在設計階段有 toomake 的重要決策。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-150">hello choice of hello partition key is an important decision that you have toomake at design time.</span></span> <span data-ttu-id="b4cf6-151">您必須選擇具有各種不同的值並且有平均存取模式的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-151">You must pick a property name that has a wide range of values and has even access patterns.</span></span>

> [!NOTE]
> <span data-ttu-id="b4cf6-152">它是最佳的作法 toohave 具有許多相異值 (100年-最少的 1000) 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-152">It is a best practice toohave a partition key with many distinct values (100s-1000s at a minimum).</span></span>
>

<span data-ttu-id="b4cf6-153">Azure Cosmos DB 容器可視為「固定」或「無限制」。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-153">Azure Cosmos DB containers can be created as "fixed" or "unlimited."</span></span> <span data-ttu-id="b4cf6-154">固定大小的容器具有上限為 10 GB 和 10,000 RU/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-154">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="b4cf6-155">某些應用程式開發介面可讓 hello 資料分割索引鍵 toobe 省略的固定大小的容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-155">Some APIs allow hello partition key toobe omitted for fixed-size containers.</span></span> <span data-ttu-id="b4cf6-156">toocreate 為無限制的容器，您必須指定最小 2500 RU/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-156">toocreate a container as unlimited, you must specify a minimum throughput of 2500 RU/s.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="b4cf6-157">資料分割與佈建的輸送量</span><span class="sxs-lookup"><span data-stu-id="b4cf6-157">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="b4cf6-158">Cosmos DB 設計用來取得可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-158">Cosmos DB is designed for predictable performance.</span></span> <span data-ttu-id="b4cf6-159">當您建立容器時，可以根據每秒的[要求單位](request-units.md) (RU) 來為每分的 RU 預留輸送量。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-159">When you create a container, you reserve throughput in terms of **[request units](request-units.md) (RU) per second with a potential add-on for RU per minute**.</span></span> <span data-ttu-id="b4cf6-160">每個要求會指派是均衡 toohello 系統資源，例如 CPU、 記憶體和 IO hello 作業所耗用的數量的要求單位費用。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-160">Each request is assigned a request unit charge that is proportionate toohello amount of system resources like CPU, Memory, and IO consumed by hello operation.</span></span> <span data-ttu-id="b4cf6-161">讀取 1 KB 具有工作階段一致性的文件，會使用 1 個要求單位。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-161">A read of a 1-KB document with Session consistency consumes one request unit.</span></span> <span data-ttu-id="b4cf6-162">讀取為 1 RU 無論 hello 數目的項目儲存或 hello hello 在執行的並行要求數目相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-162">A read is 1 RU regardless of hello number of items stored or hello number of concurrent requests running at hello same time.</span></span> <span data-ttu-id="b4cf6-163">較大的項目需要較高的要求單位 hello 大小而定。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-163">Larger items require higher request units depending on hello size.</span></span> <span data-ttu-id="b4cf6-164">如果您知道 hello 大小的實體，並且在 hello 的讀取數 toosupport 需要您的應用程式，您可以佈建 hello 確實所需的應用程式的需要讀取所需的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-164">If you know hello size of your entities and hello number of reads you need toosupport for your application, you can provision hello exact amount of throughput required for your application's read needs.</span></span> 

> [!NOTE]
> <span data-ttu-id="b4cf6-165">tooachieve hello 的輸送量，hello 容器，您必須選擇資料分割索引鍵，可讓您 tooevenly 之間分散要求一些不同的資料分割索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-165">tooachieve hello full throughput of hello container, you must choose a partition key that allows you tooevenly distribute requests among some distinct partition key values.</span></span>
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a><span data-ttu-id="b4cf6-166">使用 hello Azure Cosmos DB Api</span><span class="sxs-lookup"><span data-stu-id="b4cf6-166">Working with hello Azure Cosmos DB APIs</span></span>
<span data-ttu-id="b4cf6-167">您可以使用 hello Azure 入口網站或 Azure CLI toocreate 容器，並調整其大小在任何時間。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-167">You can use hello Azure portal or Azure CLI toocreate containers and scale them at any time.</span></span> <span data-ttu-id="b4cf6-168">此區段會顯示如何 toocreate 容器並指定 hello 輸送量和資料分割索引鍵定義中的 hello 的每個支援的 Api。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-168">This section shows how toocreate containers and specify hello throughput and partition key definition in each of hello supported APIs.</span></span>

### <a name="documentdb-api"></a><span data-ttu-id="b4cf6-169">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="b4cf6-169">DocumentDB API</span></span>
<span data-ttu-id="b4cf6-170">hello 下列範例顯示如何 toocreate 容器 （集合），使用 hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-170">hello following sample shows how toocreate a container (collection) using hello DocumentDB API.</span></span> <span data-ttu-id="b4cf6-171">您可以在[使用 DocumentDB API 進行資料分割](partition-data.md)中找到更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-171">You can find more details in [Partitioning with DocumentDB API](partition-data.md).</span></span>

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

<span data-ttu-id="b4cf6-172">您可以讀取項目 （文件） 使用 hello `GET` hello REST API 或使用中的方法`ReadDocumentAsync`其中一種 hello Sdk。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-172">You can read an item (document) using hello `GET` method in hello REST API or using `ReadDocumentAsync` in one of hello SDKs.</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a><span data-ttu-id="b4cf6-173">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="b4cf6-173">MongoDB API</span></span>
<span data-ttu-id="b4cf6-174">以 hello MongoDB API，您可以建立分區化的集合，透過您最愛的工具、 驅動程式或 SDK。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-174">With hello MongoDB API, you can create a sharded collection through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="b4cf6-175">在此範例中，我們會使用 hello Mongo 殼層 hello 集合建立的。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-175">In this example, we use hello Mongo Shell for hello collection creation.</span></span>

<span data-ttu-id="b4cf6-176">在 [hello Mongo 殼層：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-176">In hello Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="b4cf6-177">結果：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-177">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a><span data-ttu-id="b4cf6-178">資料表 API</span><span class="sxs-lookup"><span data-stu-id="b4cf6-178">Table API</span></span>

<span data-ttu-id="b4cf6-179">以 hello 表格 API，您指定資料表的 hello 輸送量 hello appSettings 組態中應用程式：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-179">With hello Table API, you specify hello throughput for tables in hello appSettings configuration for your application:</span></span>

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

<span data-ttu-id="b4cf6-180">然後您會建立資料表，使用 hello Azure 資料表儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-180">Then you create a table using hello Azure Table storage SDK.</span></span> <span data-ttu-id="b4cf6-181">hello 資料分割索引鍵會隱含建立為 hello`PartitionKey`值。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-181">hello partition key is implicitly created as hello `PartitionKey` value.</span></span> 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

<span data-ttu-id="b4cf6-182">您可以擷取單一實體，使用下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="b4cf6-182">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
<span data-ttu-id="b4cf6-183">請參閱[開發以 hello 表格 API](tutorial-develop-table-dotnet.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-183">See [Developing with hello Table API](tutorial-develop-table-dotnet.md) for more details.</span></span>

### <a name="graph-api"></a><span data-ttu-id="b4cf6-184">圖形 API</span><span class="sxs-lookup"><span data-stu-id="b4cf6-184">Graph API</span></span>

<span data-ttu-id="b4cf6-185">以 hello Graph API，您必須使用 hello Azure 入口網站或 CLI toocreate 容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-185">With hello Graph API, you must use hello Azure portal or CLI toocreate containers.</span></span> <span data-ttu-id="b4cf6-186">或者，由於 Azure Cosmos DB 多模型，您可以使用其中一種 hello 其他模型 toocreate 並調整您的圖形容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-186">Alternatively, since Azure Cosmos DB is multi-model, you can use one of hello other models toocreate and scale your graph container.</span></span>

<span data-ttu-id="b4cf6-187">您可以閱讀任何頂點或使用中 Gremlin hello 資料分割索引鍵和 id 的邊緣。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-187">You can read any vertex or edge using hello partition key and id in Gremlin.</span></span> <span data-ttu-id="b4cf6-188">比方說，圖形與 hello 資料分割索引鍵，以及 「 西雅圖 」 做為 hello 資料列索引鍵的地區 （「 美國 」），您可以找到頂點使用 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-188">For example, for a graph with region ("USA") as hello partition key, and "Seattle" as hello row key, you can find a vertex using hello following syntax:</span></span>

```
g.V(['USA', 'Seattle'])
```

<span data-ttu-id="b4cf6-189">相同邊緣，您可以參考使用 hello 資料分割索引鍵和資料列索引鍵的邊緣。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-189">Same with edges, you can reference an edge using hello partition key and row key.</span></span>

```
g.E(['USA', 'I5'])
```

<span data-ttu-id="b4cf6-190">如需詳細資訊，請參閱 [Cosmos DB 的 Gremlin 支援](gremlin-support.md)。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-190">See [Gremlin support for Cosmos DB](gremlin-support.md) for more details.</span></span>


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="b4cf6-191">設計資料分割</span><span class="sxs-lookup"><span data-stu-id="b4cf6-191">Designing for partitioning</span></span>
<span data-ttu-id="b4cf6-192">有效地以 Azure Cosmos DB tooscale，您需要 toopick 良好的資料分割索引鍵，當您建立您的容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-192">tooscale effectively with Azure Cosmos DB, you need toopick a good partition key when you create your container.</span></span> <span data-ttu-id="b4cf6-193">選擇資料分割索引鍵時有兩個重要考量︰</span><span class="sxs-lookup"><span data-stu-id="b4cf6-193">There are two key considerations for choosing a partition key:</span></span>

* <span data-ttu-id="b4cf6-194">**查詢和交易界限**： 您所選擇的資料分割索引鍵應該平衡 hello 需要 tooenable hello 使用的交易，針對 hello 需求 toodistribute 實體之間的多個資料分割索引鍵 tooensure 靈活的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-194">**Boundary for query and transactions**: Your choice of partition key should balance hello need tooenable hello use of transactions against hello requirement toodistribute your entities across multiple partition keys tooensure a scalable solution.</span></span> <span data-ttu-id="b4cf6-195">其中一種方式，您可以設定 hello 相同的資料分割索引鍵的所有項目，但這可能會限制您的方案 hello 延展性。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-195">At one extreme, you could set hello same partition key for all your items, but this may limit hello scalability of your solution.</span></span> <span data-ttu-id="b4cf6-196">在 [hello 其他極端的做法是，您可能會指派唯一的資料分割索引鍵，每個項目，這會具有高擴充性，但會防止使用跨文件交易透過預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-196">At hello other extreme, you could assign a unique partition key for each item, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="b4cf6-197">在理想的資料分割索引鍵是其中一個，可讓您 toouse 有效率的查詢，且具有足夠的基數 tooensure 可擴充是您的方案。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-197">An ideal partition key is one that enables you toouse efficient queries and that has sufficient cardinality tooensure your solution is scalable.</span></span> 
* <span data-ttu-id="b4cf6-198">**任何儲存和效能的瓶頸**： 請務必 toopick 屬性，可讓寫入 toobe 分散到不同的相異值。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-198">**No storage and performance bottlenecks**: It is important toopick a property that allows writes toobe distributed across various distinct values.</span></span> <span data-ttu-id="b4cf6-199">要求 toohello 相同的資料分割索引鍵不能超過 hello 輸送量的單一資料分割，而且實行節流措施。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-199">Requests toohello same partition key cannot exceed hello throughput of a single partition, and are throttled.</span></span> <span data-ttu-id="b4cf6-200">因此，重要 toopick 並不會導致應用程式中的 「 作用點 」 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-200">So it is important toopick a partition key that does not result in "hot spots" within your application.</span></span> <span data-ttu-id="b4cf6-201">自 hello 的所有資料的單一資料分割索引鍵必須儲存在資料分割，也建議具有大量資料的 hello tooavoid 資料分割索引鍵相同的值。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-201">Since all hello data for a single partition key must be stored within a partition, it is also recommended tooavoid partition keys that have high volumes of data for hello same value.</span></span> 

<span data-ttu-id="b4cf6-202">來看看一些真實案例和每個案例良好的資料分割索引鍵︰</span><span class="sxs-lookup"><span data-stu-id="b4cf6-202">Let's look at a few real-world scenarios, and good partition keys for each:</span></span>
* <span data-ttu-id="b4cf6-203">如果您正在實作使用者設定檔後端，hello 使用者識別碼會是資料分割索引鍵的理想選擇。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-203">If you’re implementing a user profile backend, then hello user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="b4cf6-204">如果您在儲存 IoT 資料 (例如，裝置狀態)，則裝置識別碼是不錯的資料分割索引鍵選擇。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-204">If you’re storing IoT data for example, device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="b4cf6-205">如果您使用 Azure Cosmos DB 記錄時間序列資料，然後 hello 主機名稱或處理序識別碼是不錯的選擇的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-205">If you’re using Azure Cosmos DB for logging time-series data, then hello hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="b4cf6-206">如果您有多租用戶架構，hello 租用戶識別碼會是資料分割索引鍵的理想選擇。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-206">If you have a multi-tenant architecture, hello tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="b4cf6-207">在類似 IoT 和使用者設定檔、 hello 資料分割索引鍵的情況下可能是一些使用 hello 做為 （文件索引鍵） 的識別碼相同。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-207">In some use cases like IoT and user profiles, hello partition key might be hello same as your id (document key).</span></span> <span data-ttu-id="b4cf6-208">在其他類似 hello 時間序列資料，您可能必須與 hello 識別碼不同資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-208">In others like hello time series data, you might have a partition key that’s different than hello id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="b4cf6-209">資料分割和記錄/時間序列資料</span><span class="sxs-lookup"><span data-stu-id="b4cf6-209">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="b4cf6-210">Cosmos DB 的 hello 常見使用案例是針對記錄與遙測。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-210">One of hello common use cases of Cosmos DB is for logging and telemetry.</span></span> <span data-ttu-id="b4cf6-211">它是重要 toopick 良好的資料分割索引鍵，因為您可能需要大量的磁碟區 tooread/寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-211">It is important toopick a good partition key since you might need tooread/write vast volumes of data.</span></span> <span data-ttu-id="b4cf6-212">hello 選擇取決於您的讀取和寫入速率和種類的預期 toorun 的查詢。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-212">hello choice depends on your read and write rates and kinds of queries you expect toorun.</span></span> <span data-ttu-id="b4cf6-213">以下是一些秘訣 toochoose 良好的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-213">Here are some tips on how toochoose a good partition key.</span></span>

* <span data-ttu-id="b4cf6-214">如果您使用案例牽涉到較小的率寫入 [累積一段很長一段時間，以及需要 tooquery 由時間戳記和其他篩選的範圍，則使用彙總套件 hello 時間戳記，例如，日期為資料分割索引鍵是很好的方法。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-214">If your use case involves a small rate of writes accumulating over a long period of time, and need tooquery by ranges of timestamps and other filters, then using a rollup of hello timestamp, for example,  date as a partition key is a good approach.</span></span> <span data-ttu-id="b4cf6-215">這可讓您 tooquery 透過 hello 的所有資料針對單一資料分割的日期。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-215">This allows you tooquery over all hello data for a date from a single partition.</span></span> 
* <span data-ttu-id="b4cf6-216">如果您的寫入工作負載繁重 (這是更常見的情形)，則不應該使用根據時間戳記的資料分割索引鍵，這樣一來，Cosmos DB 才可以將寫入工作平均分散到多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-216">If your workload is written heavy, which is more common, you should use a partition key that’s not based on timestamp so that Cosmos DB can distribute writes evenly across various partitions.</span></span> <span data-ttu-id="b4cf6-217">在這個案例中，主機名稱、處理序識別碼、活動識別碼或其他具有高基數的屬性是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-217">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="b4cf6-218">第三種方法是一種混合體一個其中有多個容器，一個用於每日/月 hello 資料分割索引鍵是細微的屬性，例如主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-218">A third approach is a hybrid one where you have multiple containers, one for each day/month and hello partition key is a granular property like hostname.</span></span> <span data-ttu-id="b4cf6-219">此功能還有您可以設定不同的輸送量 hello 時間間隔為基礎的 hello 優點，例如 hello 當月的 hello 容器佈建較高的輸送量因為它是讀取和寫入，而與前的幾個月降低輸送量，因為它們只可讀取。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-219">This has hello benefit that you can set different throughput based on hello time window, for example, hello container for hello current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="b4cf6-220">資料分割與多重租用</span><span class="sxs-lookup"><span data-stu-id="b4cf6-220">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="b4cf6-221">如果您使用 Cosmos DB 實作多重租用戶應用程式，有兩種常見的模式：一個租用戶一個資料分割索引鍵，和一個租用戶一個容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-221">If you are implementing a multi-tenant application using Cosmos DB, there are two popular patterns – one partition key per tenant, and one container per tenant.</span></span> <span data-ttu-id="b4cf6-222">以下是 hello 專業人員以及每個缺點：</span><span class="sxs-lookup"><span data-stu-id="b4cf6-222">Here are hello pros and cons for each:</span></span>

* <span data-ttu-id="b4cf6-223">一個租用戶一個資料分割索引鍵：在此模型中，租用戶共置於單一容器內。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-223">One Partition Key per tenant: In this model, tenants are collocated within a single container.</span></span> <span data-ttu-id="b4cf6-224">但是，針對單一資料分割，可以執行單一租用戶內項目的查詢與插入。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-224">But queries and inserts for items within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="b4cf6-225">您也可以跨租用戶內的所有項目實作交易邏輯。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-225">You can also implement transactional logic across all items within a tenant.</span></span> <span data-ttu-id="b4cf6-226">因為多重租用戶共用一個容器，所以您可以節省儲存體和輸送量成本，方法是在單一容器內輪詢租用戶的資源，而不是為每個租用戶佈建額外的空餘空間。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-226">Since multiple tenants share a container, you can save storage and throughput costs by pooling resources for tenants within a single container rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="b4cf6-227">hello 缺點是，您不需要每個租用戶的效能隔離。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-227">hello drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="b4cf6-228">效能/輸送量增加套用 toohello 整個容器 vs 目標增加租用戶。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-228">Performance/throughput increases apply toohello entire container vs targeted increases for tenants.</span></span>
* <span data-ttu-id="b4cf6-229">一個租用戶一個容器：每個租用戶都有其專屬容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-229">One Container per tenant: Each tenant has its own container.</span></span> <span data-ttu-id="b4cf6-230">在此模型中，您可以保留每個租用戶的效能。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-230">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="b4cf6-231">使用 Cosmos DB 全新的佈建計價模式，這種模式對於具有少數租用戶的多重租用戶應用程式最具成本效益。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-231">With Cosmos DB's new provisioning pricing model, this model is more cost-effective for multi-tenant applications with a few tenants.</span></span>

<span data-ttu-id="b4cf6-232">您也可以使用組合/分層方法可 collocates 小型的租用戶，並移轉較大的租用戶 tootheir 自己的容器。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-232">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants tootheir own container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4cf6-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4cf6-233">Next steps</span></span>
<span data-ttu-id="b4cf6-234">在本文中，我們提供使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀。</span><span class="sxs-lookup"><span data-stu-id="b4cf6-234">In this article, we provided an overview for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="b4cf6-235">了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="b4cf6-235">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>
* <span data-ttu-id="b4cf6-236">了解 [Azure Cosmos DB 中的全域分散](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="b4cf6-236">Learn about [global distribution in Azure Cosmos DB](distribute-data-globally.md)</span></span>



