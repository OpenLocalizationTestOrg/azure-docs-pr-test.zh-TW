---
title: "Azure Cosmos DB 的資料分割與調整規模 | Microsoft Docs"
description: "了解資料分割在 Azure Cosmos DB 中的運作方式、如何設定資料分割和資料分割索引鍵，以及如何為您的應用程式挑選合適的資料分割索引鍵。"
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
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="ecf52-103">使用 DocumentDB API 在 Azure Cosmos DB 進行資料分割</span><span class="sxs-lookup"><span data-stu-id="ecf52-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="ecf52-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) 是全域分散式多模型資料庫服務，其設計可協助您達成快速且可預測的效能，並順暢地隨著應用程式的成長而調整規模。</span><span class="sxs-lookup"><span data-stu-id="ecf52-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="ecf52-105">本文提供如何透過 DocumentDB API 使用 Cosmos DB 容器資料分割的概觀。</span><span class="sxs-lookup"><span data-stu-id="ecf52-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ecf52-106">如需使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀，請參閱[資料分割與水平調整](../cosmos-db/partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="ecf52-107">若要開始使用程式碼，請從 [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark) 下載專案。</span><span class="sxs-lookup"><span data-stu-id="ecf52-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="ecf52-108">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="ecf52-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="ecf52-109">Azure Cosmos DB 中資料分割的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="ecf52-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="ecf52-110">如何在 Azure Cosmos DB 中設定資料分割</span><span class="sxs-lookup"><span data-stu-id="ecf52-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="ecf52-111">什麼是資料分割索引鍵，以及如何為我的應用程式選擇正確的資料分割索引鍵？</span><span class="sxs-lookup"><span data-stu-id="ecf52-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="ecf52-112">若要開始使用程式碼，請從 [Azure Cosmos DB 效能測試驅動程式範例](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)下載專案。</span><span class="sxs-lookup"><span data-stu-id="ecf52-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="ecf52-113">資料分割索引鍵</span><span class="sxs-lookup"><span data-stu-id="ecf52-113">Partition keys</span></span>

<span data-ttu-id="ecf52-114">在 DocumentDB API 中，您要以 JSON 路徑的形式來指定分割區索引鍵定義。</span><span class="sxs-lookup"><span data-stu-id="ecf52-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="ecf52-115">下表顯示資料分割索引鍵定義及各個對應值的範例。</span><span class="sxs-lookup"><span data-stu-id="ecf52-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="ecf52-116">資料分割索引鍵會以路徑的形式指定，例如 `/department` 代表 department 屬性。</span><span class="sxs-lookup"><span data-stu-id="ecf52-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="ecf52-117"><strong>資料分割索引鍵</strong></span><span class="sxs-lookup"><span data-stu-id="ecf52-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ecf52-118"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="ecf52-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ecf52-119">/department</span><span class="sxs-lookup"><span data-stu-id="ecf52-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ecf52-120">對應至 doc.department 的值，其中 doc 是指項目。</span><span class="sxs-lookup"><span data-stu-id="ecf52-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ecf52-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="ecf52-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ecf52-122">對應至 doc.properties.name 的值，其中 doc 是指項目 (巢狀屬性)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ecf52-123">/id</span><span class="sxs-lookup"><span data-stu-id="ecf52-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ecf52-124">對應至 doc.id 的值 (識別碼和資料分割索引鍵是相同屬性)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ecf52-125">/"department name"</span><span class="sxs-lookup"><span data-stu-id="ecf52-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ecf52-126">對應至 doc["department name"] 的值，其中 doc 是指項目。</span><span class="sxs-lookup"><span data-stu-id="ecf52-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="ecf52-127">資料分割索引鍵的語法類似於指定路徑以為原則路徑編製索引，但主要的差別在於路徑會對應至屬性而不是值，也就是結尾沒有萬用字元。</span><span class="sxs-lookup"><span data-stu-id="ecf52-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="ecf52-128">例如，您可以指定 /department/?</span><span class="sxs-lookup"><span data-stu-id="ecf52-128">For example, you would specify /department/?</span></span> <span data-ttu-id="ecf52-129">以為 department 下的值編製索引，但您會將 /department 指定為資料分割索引鍵定義。</span><span class="sxs-lookup"><span data-stu-id="ecf52-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="ecf52-130">資料分割索引鍵會以隱含方式編製索引，而且無法使用索引原則覆寫來排除編製索引。</span><span class="sxs-lookup"><span data-stu-id="ecf52-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="ecf52-131">讓我們看看資料分割索引鍵選擇對於應用程式效能的影響。</span><span class="sxs-lookup"><span data-stu-id="ecf52-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="ecf52-132">使用 Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="ecf52-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="ecf52-133">Azure Cosmos DB 已透過 [REST API 版本 2015-12-16](/rest/api/documentdb/) 新增對自動資料分割的支援。</span><span class="sxs-lookup"><span data-stu-id="ecf52-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="ecf52-134">若要建立資料分割的容器，必須下載其中一個支援的 SDK 平台 (.NET、Node.js、Java、Python、MongoDB) 中的 SDK 1.6.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ecf52-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="ecf52-135">建立容器</span><span class="sxs-lookup"><span data-stu-id="ecf52-135">Creating containers</span></span>
<span data-ttu-id="ecf52-136">下列範例顯示建立容器的 .NET 程式碼片段，可儲存輸送量每秒 20,000 個要求單位的裝置遙測資料。</span><span class="sxs-lookup"><span data-stu-id="ecf52-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="ecf52-137">SDK 會設定 OfferThroughput 值 (這會接著設定 REST API 中的 `x-ms-offer-throughput` 要求標頭)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="ecf52-138">此處我們將 `/deviceId` 設定為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ecf52-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="ecf52-139">選擇的資料分割索引鍵會與其餘的容器中繼資料 (例如名稱與編製索引原則) 一併儲存。</span><span class="sxs-lookup"><span data-stu-id="ecf52-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="ecf52-140">在此範例中，我們挑選了 `deviceId` ，因為我們知道 (a) 由於有大量的裝置，因此可以將寫入平均分散到所有資料分割，讓我們能夠調整資料庫規模以內嵌大量資料，以及 (b) 許多要求 (例如，提取裝置的最新讀取) 會限定在單一 deviceId，而可以從單一資料分割擷取。</span><span class="sxs-lookup"><span data-stu-id="ecf52-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="ecf52-141">此方法會對 Cosmos DB 進行 REST API 呼叫，且服務會根據要求的輸送量來佈建許多資料分割。</span><span class="sxs-lookup"><span data-stu-id="ecf52-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="ecf52-142">您可以隨著效能需求的發展變更容器的輸送量。</span><span class="sxs-lookup"><span data-stu-id="ecf52-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="ecf52-143">讀取和寫入項目</span><span class="sxs-lookup"><span data-stu-id="ecf52-143">Reading and writing items</span></span>
<span data-ttu-id="ecf52-144">現在，我們將資料插入 Cosmos DB 中。</span><span class="sxs-lookup"><span data-stu-id="ecf52-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="ecf52-145">以下是包含裝置讀取的範例類別，以及呼叫 CreateDocumentAsync 將新的裝置讀取插入容器中。</span><span class="sxs-lookup"><span data-stu-id="ecf52-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="ecf52-146">這是運用 DocumentDB API 的範例︰</span><span class="sxs-lookup"><span data-stu-id="ecf52-146">This is an example leveraging the DocumentDB API:</span></span>

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

<span data-ttu-id="ecf52-147">請依資料分割索引鍵和識別碼來讀取項目，並加以更新，然後最後一個步驟是依資料分割索引鍵和識別碼刪除項目。請注意，讀取包括 PartitionKey 值 (對應至 REST API 中的 `x-ms-documentdb-partitionkey` 要求標頭)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="ecf52-148">查詢資料分割的容器</span><span class="sxs-lookup"><span data-stu-id="ecf52-148">Querying partitioned containers</span></span>
<span data-ttu-id="ecf52-149">當您查詢資料分割容器中的資料時，Cosmos DB 會自動將查詢路由傳送到與篩選中所指定之資料分割索引鍵值 (如果有的話) 對應的資料分割。</span><span class="sxs-lookup"><span data-stu-id="ecf52-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="ecf52-150">例如，此查詢只會路由傳送至包含資料分割索引鍵 "XMS-0001" 的資料分割。</span><span class="sxs-lookup"><span data-stu-id="ecf52-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="ecf52-151">下列查詢沒有根據資料分割索引鍵 (DeviceId) 的篩選，且已展開至對資料分割索引執行它的所有資料分割。</span><span class="sxs-lookup"><span data-stu-id="ecf52-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="ecf52-152">請注意，您必須指定 EnableCrossPartitionQuery (REST API 中的`x-ms-documentdb-query-enablecrosspartition` )，才能讓 SDK 跨資料分割執行查詢。</span><span class="sxs-lookup"><span data-stu-id="ecf52-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="ecf52-153">Cosmos DB 使用 SQL (包含 SDK 1.12.0 和更新版本) 支援資料分割容器的[彙總函式](documentdb-sql-query.md#Aggregates) `COUNT`、`MIN`、`MAX`、`SUM` 和 `AVG`。</span><span class="sxs-lookup"><span data-stu-id="ecf52-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="ecf52-154">查詢必須包含單一彙總運算子，而且在投射中必須包含單一值。</span><span class="sxs-lookup"><span data-stu-id="ecf52-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="ecf52-155">平行查詢執行</span><span class="sxs-lookup"><span data-stu-id="ecf52-155">Parallel query execution</span></span>
<span data-ttu-id="ecf52-156">Cosmos DB SDK 1.9.0 和更新版本支援平行查詢執行選項，可讓您對資料分割集合執行低延遲查詢 (即使它們需要涉及大量的資料分割也一樣)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="ecf52-157">例如，下列查詢設定為跨資料分割平行執行。</span><span class="sxs-lookup"><span data-stu-id="ecf52-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="ecf52-158">若要管理平行執行查詢，您可以調整下列參數︰</span><span class="sxs-lookup"><span data-stu-id="ecf52-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="ecf52-159">藉由設定 `MaxDegreeOfParallelism`，您可以控制平行處理原則的程度，亦即同時連往容器資料分割的網路連線數上限。</span><span class="sxs-lookup"><span data-stu-id="ecf52-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="ecf52-160">如果您將此設定為 -1，平行處理原則的程度是由 SDK 管理。</span><span class="sxs-lookup"><span data-stu-id="ecf52-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="ecf52-161">如果 `MaxDegreeOfParallelism` 未指定或設為 0 (這是預設值)，將會有連往容器資料分割的單一網路連線。</span><span class="sxs-lookup"><span data-stu-id="ecf52-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="ecf52-162">您可藉由設定 `MaxBufferedItemCount`，來權衡取捨查詢延遲和用戶端記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="ecf52-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="ecf52-163">如果您省略這個參數或將此設定為 -1，平行查詢執行期間緩衝處理的項目數是由 SDK 管理。</span><span class="sxs-lookup"><span data-stu-id="ecf52-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="ecf52-164">在相同的集合狀態下，平行查詢會以和序列執行相同的順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="ecf52-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="ecf52-165">執行包含排序 (ORDER BY 和/或 TOP) 的跨資料分割查詢時，Azure Cosmos DB SDK 會跨資料分割發出平行查詢，並合併用戶端中已部分排序的結果來產生全域排序的結果。</span><span class="sxs-lookup"><span data-stu-id="ecf52-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="ecf52-166">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="ecf52-166">Executing stored procedures</span></span>
<span data-ttu-id="ecf52-167">您也可以對具有相同裝置識別碼的文件執行不可部分完成交易，例如，如果您正在維護彙總或處於單一項目中裝置的最新狀態。</span><span class="sxs-lookup"><span data-stu-id="ecf52-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="ecf52-168">在下一節中，我們會探討如何從單一資料分割容器改為資料分割的容器。</span><span class="sxs-lookup"><span data-stu-id="ecf52-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecf52-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecf52-169">Next steps</span></span>
<span data-ttu-id="ecf52-170">在本文中，我們提供如何透過 DocumentDB API 使用 Azure Cosmos DB 容器資料分割的概觀。</span><span class="sxs-lookup"><span data-stu-id="ecf52-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="ecf52-171">如需使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀，另請參閱[資料分割與水平調整](../cosmos-db/partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="ecf52-172">使用 Azure Cosmos DB 執行規模和效能測試。</span><span class="sxs-lookup"><span data-stu-id="ecf52-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ecf52-173">如需範例，請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf52-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ecf52-174">使用 [SDK](documentdb-sdk-dotnet.md) 或 [REST API](/rest/api/documentdb/) 開始撰寫程式碼</span><span class="sxs-lookup"><span data-stu-id="ecf52-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="ecf52-175">了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ecf52-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

