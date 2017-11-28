---
title: "aaaPartitioning 在 Azure Cosmos DB 中和縮放 |Microsoft 文件"
description: "了解有關如何分割 Azure Cosmos DB 的運作方式、 如何 tooconfigure 資料分割和資料分割索引鍵，和如何 toopick hello 右資料分割索引鍵應用程式。"
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="87c3b-103">使用 DocumentDB API hello Azure Cosmos DB 中的資料分割</span><span class="sxs-lookup"><span data-stu-id="87c3b-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="87c3b-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md)是全域的分散式、 多模型資料庫服務，其設計 toohelp 您達成快速、 可預測的效能和擴充順暢地連同應用程式的成長。</span><span class="sxs-lookup"><span data-stu-id="87c3b-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="87c3b-105">本文章提供如何 Cosmos DB 容器使用的資料分割的 toowork hello DocumentDB API 的概觀。</span><span class="sxs-lookup"><span data-stu-id="87c3b-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="87c3b-106">如需使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀，請參閱[資料分割與水平調整](../cosmos-db/partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="87c3b-107">tooget 開始使用程式碼，請下載 hello 專案從[Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="87c3b-108">閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="87c3b-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="87c3b-109">Azure Cosmos DB 中資料分割的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="87c3b-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="87c3b-110">如何在 Azure Cosmos DB 中設定資料分割</span><span class="sxs-lookup"><span data-stu-id="87c3b-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="87c3b-111">什麼是資料分割索引鍵，以及如何針對我的應用程式挑選 hello 右邊的資料分割索引鍵？</span><span class="sxs-lookup"><span data-stu-id="87c3b-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="87c3b-112">tooget 開始使用程式碼，請下載 hello 專案從[Azure Cosmos DB 效能測試驅動程式範例](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="87c3b-113">資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="87c3b-113">Partition keys</span></span>

<span data-ttu-id="87c3b-114">在 hello DocumentDB API，您可以指定 hello 資料分割索引鍵定義中 hello 使用的 JSON 路徑格式。</span><span class="sxs-lookup"><span data-stu-id="87c3b-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="87c3b-115">hello 下表顯示資料分割索引鍵定義和對應 tooeach hello 值的範例。</span><span class="sxs-lookup"><span data-stu-id="87c3b-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="87c3b-116">例如： hello 資料分割索引鍵指定為路徑，`/department`代表 hello 屬性部門。</span><span class="sxs-lookup"><span data-stu-id="87c3b-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="87c3b-117"><strong>資料分割索引鍵</strong></span><span class="sxs-lookup"><span data-stu-id="87c3b-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="87c3b-118"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="87c3b-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="87c3b-119">/department</span><span class="sxs-lookup"><span data-stu-id="87c3b-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="87c3b-120">對應 toohello doc.department 文件所在 hello 項目值。</span><span class="sxs-lookup"><span data-stu-id="87c3b-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="87c3b-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="87c3b-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="87c3b-122">對應 toohello doc.properties.name 文件所在 hello 項目 （巢狀屬性） 值。</span><span class="sxs-lookup"><span data-stu-id="87c3b-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="87c3b-123">/id</span><span class="sxs-lookup"><span data-stu-id="87c3b-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="87c3b-124">對應 doc.id toohello 值 (識別碼和資料分割索引鍵是 hello 相同屬性)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="87c3b-125">/"department name"</span><span class="sxs-lookup"><span data-stu-id="87c3b-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="87c3b-126">對應 toohello 值的文件 [」 部門名稱"] 文件所在 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="87c3b-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="87c3b-127">資料分割索引鍵的 hello 語法是具有編製索引原則路徑 hello hello 路徑的主要差異對應 toohello 屬性，而不是 hello 值類似 toohello 路徑規格，也就是沒有萬用字元 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="87c3b-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="87c3b-128">例如，您可以指定 /department/?</span><span class="sxs-lookup"><span data-stu-id="87c3b-128">For example, you would specify /department/?</span></span> <span data-ttu-id="87c3b-129">tooindex hello 下部門值，但指定 /department hello 資料分割索引鍵定義。</span><span class="sxs-lookup"><span data-stu-id="87c3b-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="87c3b-130">hello 資料分割索引鍵以隱含方式編製索引，而且無法從索引使用索引的原則覆寫排除。</span><span class="sxs-lookup"><span data-stu-id="87c3b-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="87c3b-131">讓我們看看 hello 所選擇的資料分割索引鍵會 hello 應用程式效能的影響。</span><span class="sxs-lookup"><span data-stu-id="87c3b-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="87c3b-132">使用 hello Azure Cosmos DB Sdk</span><span class="sxs-lookup"><span data-stu-id="87c3b-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="87c3b-133">Azure Cosmos DB 已透過 [REST API 版本 2015-12-16](/rest/api/documentdb/) 新增對自動資料分割的支援。</span><span class="sxs-lookup"><span data-stu-id="87c3b-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="87c3b-134">在訂單 toocreate 分割容器中，您必須下載 SDK 版本 1.6.0 或更新版本中的 hello 其中一個支援 SDK 平台 （.NET、 Node.js、 Java、 Python、 MongoDB）。</span><span class="sxs-lookup"><span data-stu-id="87c3b-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="87c3b-135">建立容器</span><span class="sxs-lookup"><span data-stu-id="87c3b-135">Creating containers</span></span>
<span data-ttu-id="87c3b-136">hello 下列範例示範.NET 程式碼片段 toocreate 20000 的要求單位，每秒的輸送量容器 toostore 裝置遙測資料。</span><span class="sxs-lookup"><span data-stu-id="87c3b-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="87c3b-137">hello SDK 設定 hello OfferThroughput 值 (可接著設定 hello `x-ms-offer-throughput` hello REST API 中的要求標頭)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="87c3b-138">這裡我們設定 hello `/deviceId` hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="87c3b-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="87c3b-139">hello 所選擇的資料分割索引鍵是 hello 容器中繼資料，例如名稱和編製索引原則 hello 其餘部分一起儲存。</span><span class="sxs-lookup"><span data-stu-id="87c3b-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="87c3b-140">此範例中，我們挑選`deviceId`我們知道 （a） 因為有大量的裝置，因為寫入可以發佈在資料分割之間平均和讓我們 tooscale hello 資料庫 tooingest 大量資料磁碟區，而且 （b） 的許多 hello 要求像擷取 hello 最新的讀取裝置是已設定領域的 tooa 單一 deviceId，並且可以擷取單一資料分割。</span><span class="sxs-lookup"><span data-stu-id="87c3b-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="87c3b-141">這個方法會呼叫 tooCosmos DB REST API 和 hello 服務將會提供根據 hello 要求輸送量的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="87c3b-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="87c3b-142">當您的效能需求的發展，您可以變更容器的 hello 輸送量。</span><span class="sxs-lookup"><span data-stu-id="87c3b-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="87c3b-143">讀取和寫入項目</span><span class="sxs-lookup"><span data-stu-id="87c3b-143">Reading and writing items</span></span>
<span data-ttu-id="87c3b-144">現在，我們將資料插入 Cosmos DB 中。</span><span class="sxs-lookup"><span data-stu-id="87c3b-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="87c3b-145">以下是包含裝置讀取，且呼叫 tooCreateDocumentAsync tooinsert 讀取到容器的新裝置的範例類別。</span><span class="sxs-lookup"><span data-stu-id="87c3b-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="87c3b-146">這是利用 hello DocumentDB API 範例：</span><span class="sxs-lookup"><span data-stu-id="87c3b-146">This is an example leveraging hello DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="87c3b-147">讓我們來讀取 hello 其資料分割索引鍵和 id 的項目、 更新和最後一個步驟，然後將它刪除資料分割索引鍵和 id。請注意，hello 讀取包含 PartitionKey 值 (對應 toohello `x-ms-documentdb-partitionkey` hello REST API 中的要求標頭)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="87c3b-148">查詢資料分割的容器</span><span class="sxs-lookup"><span data-stu-id="87c3b-148">Querying partitioned containers</span></span>
<span data-ttu-id="87c3b-149">當您查詢資料分割的容器，Cosmos DB 中的資料會自動路由 hello 對應 toohello 資料分割索引鍵值 （如果有的話），hello 篩選中指定的查詢 toohello 分割區。</span><span class="sxs-lookup"><span data-stu-id="87c3b-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="87c3b-150">例如，此查詢是路由的 toojust hello 磁碟分割包含 hello 資料分割索引鍵"XMS 0001"。</span><span class="sxs-lookup"><span data-stu-id="87c3b-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="87c3b-151">hello 下列查詢 hello 資料分割索引鍵 (DeviceId) 上沒有篩選器，視窗成扇形散開 tooall 分割區執行針對 hello 分割區索引。</span><span class="sxs-lookup"><span data-stu-id="87c3b-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="87c3b-152">請注意，您必須 toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` hello REST API 中) toohave hello SDK tooexecute 橫跨資料分割的查詢。</span><span class="sxs-lookup"><span data-stu-id="87c3b-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="87c3b-153">Cosmos DB 使用 SQL (包含 SDK 1.12.0 和更新版本) 支援資料分割容器的[彙總函式](documentdb-sql-query.md#Aggregates) `COUNT`、`MIN`、`MAX`、`SUM` 和 `AVG`。</span><span class="sxs-lookup"><span data-stu-id="87c3b-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="87c3b-154">查詢必須包含單一的彙總運算子，而且必須包含 hello 投影中的單一值。</span><span class="sxs-lookup"><span data-stu-id="87c3b-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="87c3b-155">平行查詢執行</span><span class="sxs-lookup"><span data-stu-id="87c3b-155">Parallel query execution</span></span>
<span data-ttu-id="87c3b-156">hello Cosmos DB Sdk 1.9.0 和上方支援平行查詢執行選項，可讓您 tooperform 低度延遲查詢針對資料分割的集合，即使他們需要 tootouch 大量的資料分割。</span><span class="sxs-lookup"><span data-stu-id="87c3b-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="87c3b-157">比方說，下列查詢的 hello 是以平行方式設定的 toorun 橫跨資料分割。</span><span class="sxs-lookup"><span data-stu-id="87c3b-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="87c3b-158">您可以管理執行平行查詢微調 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="87c3b-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="87c3b-159">藉由設定`MaxDegreeOfParallelism`，您可以控制 hello 程度即 hello 同時網路連線 toohello 容器的資料分割數目上限。</span><span class="sxs-lookup"><span data-stu-id="87c3b-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="87c3b-160">如果您設定太-1，會將平行處理原則程度 hello 受 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="87c3b-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="87c3b-161">如果 hello`MaxDegreeOfParallelism`未指定或設定 too0，也就是 hello 預設值，會有單一網路連線 toohello 容器的資料分割。</span><span class="sxs-lookup"><span data-stu-id="87c3b-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="87c3b-162">您可藉由設定 `MaxBufferedItemCount`，來權衡取捨查詢延遲和用戶端記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="87c3b-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="87c3b-163">如果您省略這個參數，或將此設定太-1，由 hello SDK 管理 hello 平行查詢執行期間經過緩衝處理的項目數目。</span><span class="sxs-lookup"><span data-stu-id="87c3b-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="87c3b-164">指定 hello hello 集合的相同的州名，平行查詢會傳回結果中 hello 相同排序如同序列執行。</span><span class="sxs-lookup"><span data-stu-id="87c3b-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="87c3b-165">當執行包含排序 （ORDER BY 和/或頂端） 的跨資料分割查詢，hello Azure Cosmos DB SDK 問題會跨越磁碟分割及合併部分已排序的結果，在 hello 全域排序結果的用戶端端 tooproduce hello 平行查詢。</span><span class="sxs-lookup"><span data-stu-id="87c3b-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="87c3b-166">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="87c3b-166">Executing stored procedures</span></span>
<span data-ttu-id="87c3b-167">您也可以執行不可部分完成的交易，對文件以 hello 相同的裝置識別碼，例如您正在維護彙總或 hello 的單一項目中的裝置最新狀態。</span><span class="sxs-lookup"><span data-stu-id="87c3b-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="87c3b-168">Hello 下一節，我們會探討如何移動 toopartitioned 容器，以及在從單一資料分割的容器。</span><span class="sxs-lookup"><span data-stu-id="87c3b-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87c3b-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87c3b-169">Next steps</span></span>
<span data-ttu-id="87c3b-170">在本文中，我們會提供如何與 Azure Cosmos DB 容器的資料分割的 toowork hello DocumentDB API 的概觀。</span><span class="sxs-lookup"><span data-stu-id="87c3b-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="87c3b-171">如需使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀，另請參閱[資料分割與水平調整](../cosmos-db/partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="87c3b-172">使用 Azure Cosmos DB 執行規模和效能測試。</span><span class="sxs-lookup"><span data-stu-id="87c3b-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="87c3b-173">如需範例，請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="87c3b-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="87c3b-174">開始撰寫程式碼以 hello [Sdk](documentdb-sdk-dotnet.md)或 hello [REST API](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="87c3b-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="87c3b-175">了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="87c3b-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

