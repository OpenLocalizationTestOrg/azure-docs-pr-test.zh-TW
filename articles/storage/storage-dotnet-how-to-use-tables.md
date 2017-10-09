---
title: "開始使用適用於.NET 的 Azure 資料表儲存體 aaaGet |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 9635079d61d874ff7f4bc9e7d610e0ad54b4fd6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="fbac6-103">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="fbac6-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="fbac6-104">Azure 資料表儲存體是儲存結構化的 NoSQL 資料 hello 雲端中的提供索引鍵/屬性存放區搭配 schemaless 設計的服務。</span><span class="sxs-lookup"><span data-stu-id="fbac6-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="fbac6-105">因為資料表儲存體是 schemaless，很容易 tooadapt 資料做為 hello 需要的應用程式 evolve。</span><span class="sxs-lookup"><span data-stu-id="fbac6-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="fbac6-106">存取 tooTable 儲存體資料非常快速且符合成本效益的許多類型的應用程式，，和通常中較低成本比傳統的 SQL 資料磁碟區類似。</span><span class="sxs-lookup"><span data-stu-id="fbac6-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="fbac6-107">您可以使用資料表儲存體 toostore 彈性的資料集像是使用者資料的 web 應用程式、 通訊錄，裝置資訊或其他類型的服務需要的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fbac6-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="fbac6-108">您可以將任意數目的實體儲存在資料表中，而且儲存體帳戶包含任何數量的資料表，向上 toohello hello 儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="fbac6-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="fbac6-109">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="fbac6-109">About this tutorial</span></span>
<span data-ttu-id="fbac6-110">本教學課程示範如何 toouse hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)中一些常見的 Azure 資料表儲存體案例。</span><span class="sxs-lookup"><span data-stu-id="fbac6-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="fbac6-111">這些案例會使用 C# 作為範例，以建立和刪除資料表，並插入、更新、刪除及查詢資料表資料。</span><span class="sxs-lookup"><span data-stu-id="fbac6-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbac6-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="fbac6-112">Prerequisites</span></span>

<span data-ttu-id="fbac6-113">您需要 hello toocomplete 遵循本教學課程成功：</span><span class="sxs-lookup"><span data-stu-id="fbac6-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="fbac6-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbac6-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="fbac6-115">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="fbac6-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="fbac6-116">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="fbac6-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="fbac6-117">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fbac6-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="fbac6-118">更多範例</span><span class="sxs-lookup"><span data-stu-id="fbac6-118">More samples</span></span>
<span data-ttu-id="fbac6-119">如需使用表格儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="fbac6-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="fbac6-120">您可以下載 hello 範例應用程式並執行它，或瀏覽 hello GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fbac6-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="fbac6-121">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="fbac6-121">Add using directives</span></span>
<span data-ttu-id="fbac6-122">新增下列 hello**使用**指示詞 toohello 頂端 hello`Program.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="fbac6-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="fbac6-123">剖析 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="fbac6-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="fbac6-124">建立 hello 表格服務用戶端</span><span class="sxs-lookup"><span data-stu-id="fbac6-124">Create hello Table service client</span></span>
<span data-ttu-id="fbac6-125">hello [CloudTableClient] [ dotnet_CloudTableClient]類別可讓您 tooretrieve 資料表和資料表儲存體中儲存的實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="fbac6-126">以下是其中一種方式 toocreate hello 表格服務用戶端：</span><span class="sxs-lookup"><span data-stu-id="fbac6-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="fbac6-127">現在您已準備好 toowrite 讀取和寫入資料 tooTable 儲存的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fbac6-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="fbac6-128">建立資料表</span><span class="sxs-lookup"><span data-stu-id="fbac6-128">Create a table</span></span>
<span data-ttu-id="fbac6-129">這個範例會示範如何 toocreate 如果不存在的資料表：</span><span class="sxs-lookup"><span data-stu-id="fbac6-129">This example shows how toocreate a table if it does not already exist:</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="fbac6-130">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="fbac6-130">Add an entity tooa table</span></span>
<span data-ttu-id="fbac6-131">實體對應 tooC # 物件使用的自訂類別衍生自[TableEntity][dotnet_TableEntity]。</span><span class="sxs-lookup"><span data-stu-id="fbac6-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="fbac6-132">tooadd 實體 tooa 資料表，建立一個類別來定義實體的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="fbac6-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="fbac6-133">hello 下列程式碼會定義為 hello 資料列索引鍵和姓氏的 hello 客戶名字做 hello 資料分割索引鍵的實體類別。</span><span class="sxs-lookup"><span data-stu-id="fbac6-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="fbac6-134">在一起，實體的資料分割和資料列索引鍵內唯一識別此 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="fbac6-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="fbac6-135">以 hello 速度的不同實體可查詢相同的資料分割索引鍵的實體資料分割索引鍵，但使用不同的資料分割索引鍵可讓平行作業的更佳的延展性。</span><span class="sxs-lookup"><span data-stu-id="fbac6-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="fbac6-136">儲存在資料表中的實體 toobe 必須是支援的型別，例如衍生自 hello [TableEntity] [ dotnet_TableEntity]類別。</span><span class="sxs-lookup"><span data-stu-id="fbac6-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="fbac6-137">您想要 toostore 資料表中的實體屬性必須是 hello 型別的公用屬性，而且支援取得和設定的值。</span><span class="sxs-lookup"><span data-stu-id="fbac6-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="fbac6-138">此外，您的實體類型「必須」  公開無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="fbac6-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="fbac6-139">包含實體的資料表作業將會透過 hello [CloudTable] [ dotnet_CloudTable] hello 「 建立資料表 」 一節中稍早建立的物件。</span><span class="sxs-lookup"><span data-stu-id="fbac6-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="fbac6-140">hello 作業 toobe 執行由[TableOperation] [ dotnet_TableOperation]物件。</span><span class="sxs-lookup"><span data-stu-id="fbac6-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="fbac6-141">hello 下列程式碼範例顯示 hello 的建立 hello [CloudTable] [ dotnet_CloudTable]物件，然後**CustomerEntity**物件。</span><span class="sxs-lookup"><span data-stu-id="fbac6-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="fbac6-142">tooprepare hello 作業， [TableOperation] [ dotnet_TableOperation]物件建立到 hello 資料表 tooinsert hello customer 實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="fbac6-143">最後，藉由呼叫執行 hello 作業[CloudTable][dotnet_CloudTable]。[執行][dotnet_CloudTable_Execute]。</span><span class="sxs-lookup"><span data-stu-id="fbac6-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="fbac6-144">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="fbac6-144">Insert a batch of entities</span></span>
<span data-ttu-id="fbac6-145">您可以在單一寫入作業中，插入實體批次至資料表。</span><span class="sxs-lookup"><span data-stu-id="fbac6-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="fbac6-146">以下是批次作業的其他一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="fbac6-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="fbac6-147">您可以執行更新、 刪除及插入相同的 hello 在單一批次作業。</span><span class="sxs-lookup"><span data-stu-id="fbac6-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="fbac6-148">在單一批次作業可以包括安裝 too100 實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="fbac6-149">在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fbac6-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="fbac6-150">雖然可能 tooperform 查詢以批次作業，它必須是 hello hello 批次中唯一的作業。</span><span class="sxs-lookup"><span data-stu-id="fbac6-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="fbac6-151">hello 下列程式碼範例會建立兩個實體物件並加入每個太[TableBatchOperation] [ dotnet_TableBatchOperation]使用 hello[插入][ dotnet_TableBatchOperation_Insert]方法。</span><span class="sxs-lookup"><span data-stu-id="fbac6-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="fbac6-152">然後， [CloudTable][dotnet_CloudTable]。[ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch]稱為 tooexecute hello 作業。</span><span class="sxs-lookup"><span data-stu-id="fbac6-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="fbac6-153">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="fbac6-154">資料表的資料分割，使用中的所有實體 tooquery [TableQuery] [ dotnet_TableQuery]物件。</span><span class="sxs-lookup"><span data-stu-id="fbac6-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="fbac6-155">hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="fbac6-156">這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。</span><span class="sxs-lookup"><span data-stu-id="fbac6-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="fbac6-157">擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="fbac6-158">如果您不想 tooquery 資料分割中的所有實體，您可以藉由結合 hello 與資料列索引鍵的篩選資料分割索引鍵篩選指定範圍。</span><span class="sxs-lookup"><span data-stu-id="fbac6-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="fbac6-159">hello 下列程式碼範例會使用兩個篩選 tooget 所有實體分割區 'Smith' hello 資料列索引鍵 （第一個名稱） 開頭為字母 'E' 之前在 hello 字母，然後列印 hello 查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="fbac6-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="fbac6-160">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-160">Retrieve a single entity</span></span>
<span data-ttu-id="fbac6-161">您可以撰寫查詢 tooretrieve 單一的特定實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="fbac6-162">hello 下列程式碼使用[TableOperation] [ dotnet_TableOperation] toospecify hello 客戶 ' Ben Smith'。</span><span class="sxs-lookup"><span data-stu-id="fbac6-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="fbac6-163">這個方法會傳回單一實體，而不是集合，且 hello 傳回值中的[TableResult][dotnet_TableResult]。[結果][ dotnet_TableResult_Result]是**CustomerEntity**物件。</span><span class="sxs-lookup"><span data-stu-id="fbac6-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="fbac6-164">在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="fbac6-165">取代實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-165">Replace an entity</span></span>
<span data-ttu-id="fbac6-166">tooupdate 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="fbac6-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="fbac6-167">hello 下列程式碼變更現有的客戶電話號碼。</span><span class="sxs-lookup"><span data-stu-id="fbac6-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="fbac6-168">此程式碼不會呼叫 [Insert][dotnet_TableOperation_Insert]，而是使用 [Replace][dotnet_TableOperation_Replace]。</span><span class="sxs-lookup"><span data-stu-id="fbac6-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="fbac6-169">[取代][ dotnet_TableOperation_Replace]原因 hello 完全取代 hello 伺服器上的實體 toobe，除非變更 hello hello 伺服器上的實體自擷取後，在此情況下 hello 作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fbac6-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="fbac6-170">此失敗是的 tooprevent hello 擷取和更新您的應用程式的另一個元件之間，進行您的應用程式不慎覆寫變更。</span><span class="sxs-lookup"><span data-stu-id="fbac6-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="fbac6-171">hello 正確處理失敗的恢復 tooretrieve hello 實體，進行變更 （如果仍然有效），然後再執行另一個[取代][ dotnet_TableOperation_Replace]作業。</span><span class="sxs-lookup"><span data-stu-id="fbac6-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="fbac6-172">hello 下一節將示範如何 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="fbac6-172">hello next section will show you how toooverride this behavior.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="fbac6-173">插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="fbac6-174">[取代][ dotnet_TableOperation_Replace] hello 實體已變更，因為它從 hello 伺服器擷取作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="fbac6-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="fbac6-175">此外，您必須擷取從 hello 伺服器 hello 實體先讓 hello[取代][ dotnet_TableOperation_Replace]作業 toobe 成功。</span><span class="sxs-lookup"><span data-stu-id="fbac6-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="fbac6-176">有時候，不過，您不知道是否 hello 實體 hello 伺服器上存在和 hello 目前儲存在它的值無關。</span><span class="sxs-lookup"><span data-stu-id="fbac6-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="fbac6-177">您的更新應該將其全部覆寫。</span><span class="sxs-lookup"><span data-stu-id="fbac6-177">Your update should overwrite them all.</span></span> <span data-ttu-id="fbac6-178">tooaccomplish，您會使用[InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace]作業。</span><span class="sxs-lookup"><span data-stu-id="fbac6-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="fbac6-179">如果它不存在，或予以取代，若是如此，無論 hello 上次更新已進行時，這項作業會插入 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="fbac6-180">在下列程式碼範例的 hello，會建立 ' Fred Jones' [客戶] 實體，並將其插入 hello 'people' 資料表中。</span><span class="sxs-lookup"><span data-stu-id="fbac6-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="fbac6-181">接下來，我們使用 hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace]作業 toosave hello 與實體相同的資料分割索引鍵 (Jones) 和資料列金鑰 (Fred) toohello 伺服器，這一次使用不同的值 hello 電話號碼屬性。</span><span class="sxs-lookup"><span data-stu-id="fbac6-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="fbac6-182">因為我們使用 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace]，其所有的屬性值都會被取代。</span><span class="sxs-lookup"><span data-stu-id="fbac6-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="fbac6-183">不過，如果 ' Fred Jones' 實體以往已經存在於 hello 資料表中，它會插入。</span><span class="sxs-lookup"><span data-stu-id="fbac6-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="fbac6-184">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="fbac6-184">Query a subset of entity properties</span></span>
<span data-ttu-id="fbac6-185">資料表查詢可以擷取只需要幾個屬性，從實體而不是所有 hello 實體屬性。</span><span class="sxs-lookup"><span data-stu-id="fbac6-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="fbac6-186">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="fbac6-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="fbac6-187">hello，下列程式碼中的 hello 查詢會傳回只 hello 電子郵件地址的實體 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="fbac6-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="fbac6-188">這是使用 [DynamicTableEntity][dotnet_DynamicTableEntity] 以及 [EntityResolver][dotnet_EntityResolver] 的查詢所完成的。</span><span class="sxs-lookup"><span data-stu-id="fbac6-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="fbac6-189">您可以進一步了解在 hello[簡介 Upsert 和查詢投影部落格文章][blog_post_upsert]。</span><span class="sxs-lookup"><span data-stu-id="fbac6-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="fbac6-190">投射不是支援 hello 儲存體模擬器，因此在 hello 表格服務中使用的帳戶時，才執行此程式碼。</span><span class="sxs-lookup"><span data-stu-id="fbac6-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="fbac6-191">刪除實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-191">Delete an entity</span></span>
<span data-ttu-id="fbac6-192">您已在使用 hello 擷取之後，您可以輕鬆地刪除實體的更新實體顯示的相同模式。</span><span class="sxs-lookup"><span data-stu-id="fbac6-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="fbac6-193">下列程式碼的 hello 擷取，並刪除一個 customer 實體。</span><span class="sxs-lookup"><span data-stu-id="fbac6-193">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="fbac6-194">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="fbac6-194">Delete a table</span></span>
<span data-ttu-id="fbac6-195">最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="fbac6-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="fbac6-196">已刪除的資料表將無法使用 toobe 重新建立一段時間 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="fbac6-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="fbac6-197">以非同步方式擷取頁面中的實體</span><span class="sxs-lookup"><span data-stu-id="fbac6-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="fbac6-198">如果您正在閱讀大量實體，且想 tooprocess/顯示實體時擷取，而非等待它們所有 tooreturn，您可以擷取實體使用分割的查詢。</span><span class="sxs-lookup"><span data-stu-id="fbac6-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="fbac6-199">這個範例會示範如何 tooreturn 結果頁面使用 hello 非同步等候模式，讓您不會封鎖執行中的等待結果 tooreturn 的大型集合。</span><span class="sxs-lookup"><span data-stu-id="fbac6-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="fbac6-200">如需有關使用 hello.NET 中的非同步 Await 模式，請參閱 <<c0> [ 使用 Async 和 Await （C# 和 Visual Basic） 的非同步程式設計](https://msdn.microsoft.com/library/hh191443.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fbac6-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="fbac6-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fbac6-201">Next steps</span></span>
<span data-ttu-id="fbac6-202">現在，您學到的資料表儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="fbac6-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="fbac6-203">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="fbac6-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="fbac6-204">如需更多表格儲存體範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="fbac6-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="fbac6-205">如需可用的應用程式開發介面的完整詳細資料的資料表服務參考文件的檢視 hello:</span><span class="sxs-lookup"><span data-stu-id="fbac6-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="fbac6-206">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="fbac6-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="fbac6-207">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="fbac6-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="fbac6-208">了解您所撰寫 toosimplify hello 程式碼如何使用 hello 與 Azure 儲存體 toowork [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="fbac6-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="fbac6-209">檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。</span><span class="sxs-lookup"><span data-stu-id="fbac6-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="fbac6-210">[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage-dotnet-how-to-use-blobs.md)toostore 非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="fbac6-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="fbac6-211">[使用.NET (C#) 連線 tooSQL 資料庫](../sql-database/sql-database-develop-dotnet-simple.md)toostore 關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="fbac6-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
