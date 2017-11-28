---
title: "以 .NET 開始使用 Azure 表格儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
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
ms.openlocfilehash: 16a9dad1b01fdbef5ec8949bf9ff25497f33d994
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="75c13-103">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="75c13-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="75c13-104">Azure 表格儲存體是可將結構化的 NoSQL 資料儲存在雲端中的服務，並提供具有無結構描述設計的索引鍵/屬性存放區。</span><span class="sxs-lookup"><span data-stu-id="75c13-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="75c13-105">由於表格儲存體並無結構描述，因此可輕易隨著應用程式發展需求改寫資料。</span><span class="sxs-lookup"><span data-stu-id="75c13-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="75c13-106">相較於類似資料量的傳統 SQL，對許多類型的應用程式而言，表格儲存體資料可快速存取且符合成本效益，通常可降低成本。</span><span class="sxs-lookup"><span data-stu-id="75c13-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="75c13-107">您可以使用表格儲存體來儲存具彈性的資料集，例如 Web 應用程式的使用者資料、通訊錄、裝置資訊，以及服務所需的其他中繼資料類型。</span><span class="sxs-lookup"><span data-stu-id="75c13-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="75c13-108">您可以在資料表中儲存任意數目的實體，且儲存體帳戶可包含任意數目的資料表，最高可達儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="75c13-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="75c13-109">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="75c13-109">About this tutorial</span></span>
<span data-ttu-id="75c13-110">本教學課程示範如何在一些常見的 Azure 表格儲存體案例中使用 [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)。</span><span class="sxs-lookup"><span data-stu-id="75c13-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="75c13-111">這些案例會使用 C# 作為範例，以建立和刪除資料表，並插入、更新、刪除及查詢資料表資料。</span><span class="sxs-lookup"><span data-stu-id="75c13-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75c13-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="75c13-112">Prerequisites</span></span>

<span data-ttu-id="75c13-113">您需要下列項目才能成功完成此教學課程︰</span><span class="sxs-lookup"><span data-stu-id="75c13-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="75c13-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="75c13-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="75c13-115">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="75c13-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="75c13-116">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="75c13-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="75c13-117">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="75c13-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="75c13-118">更多範例</span><span class="sxs-lookup"><span data-stu-id="75c13-118">More samples</span></span>
<span data-ttu-id="75c13-119">如需使用表格儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="75c13-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="75c13-120">您可以下載範例應用程式並加以執行，或瀏覽 GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="75c13-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="75c13-121">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="75c13-121">Add using directives</span></span>
<span data-ttu-id="75c13-122">將下列 using 指示詞新增至 `Program.cs` 檔案的開頭處：</span><span class="sxs-lookup"><span data-stu-id="75c13-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="75c13-123">解析連接字串</span><span class="sxs-lookup"><span data-stu-id="75c13-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="75c13-124">建立表格服務用戶端</span><span class="sxs-lookup"><span data-stu-id="75c13-124">Create the Table service client</span></span>
<span data-ttu-id="75c13-125">[CloudTableClient][dotnet_CloudTableClient] 類別可讓您擷取表格儲存體中儲存的資料表。</span><span class="sxs-lookup"><span data-stu-id="75c13-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="75c13-126">以下是建立表格服務用戶端的其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="75c13-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="75c13-127">您現在可以開始撰寫程式碼，以讀取表格儲存體的資料並將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="75c13-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="75c13-128">建立資料表</span><span class="sxs-lookup"><span data-stu-id="75c13-128">Create a table</span></span>
<span data-ttu-id="75c13-129">此範例說明如何建立尚不存在的資料表：</span><span class="sxs-lookup"><span data-stu-id="75c13-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="75c13-130">將實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="75c13-130">Add an entity to a table</span></span>
<span data-ttu-id="75c13-131">使用衍生自 [TableEntity][dotnet_TableEntity] 的自訂類別，將實體對應至 C# 物件。</span><span class="sxs-lookup"><span data-stu-id="75c13-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="75c13-132">若要將實體新增至資料表，請建立一個類別來定義實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="75c13-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="75c13-133">下列程式碼會定義一個使用客戶名字作為資料列索引鍵、並使用姓氏作為資料分割索引鍵的實體類別。</span><span class="sxs-lookup"><span data-stu-id="75c13-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="75c13-134">系統會在資料表中以實體的資料分割和資料列索引鍵共同針對實體進行唯一識別。</span><span class="sxs-lookup"><span data-stu-id="75c13-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="75c13-135">查詢具有相同分割區索引鍵的實體，其速度快於查詢具有不同分割區索引鍵的實體，但使用不同的資料分割索引鍵可提供更佳的延展性或平行作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="75c13-136">要儲存在資料表中的實體都必須屬於支援的類型，例如衍生自 [TableEntity][dotnet_TableEntity] 類別。</span><span class="sxs-lookup"><span data-stu-id="75c13-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="75c13-137">您想要儲存在資料表中的實體屬性必須是該類型的公用屬性，而且同時支援值的取得和設定。</span><span class="sxs-lookup"><span data-stu-id="75c13-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="75c13-138">此外，您的實體類型「必須」  公開無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="75c13-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="75c13-139">包含實體的資料表作業會透過您先前在＜建立資料表＞一節建立的 [CloudTable][dotnet_CloudTable] 物件執行。</span><span class="sxs-lookup"><span data-stu-id="75c13-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="75c13-140">要執行的作業是以 [TableOperation][dotnet_TableOperation] 物件代表。</span><span class="sxs-lookup"><span data-stu-id="75c13-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="75c13-141">下列程式碼範例示範如何依序建立 [CloudTable][dotnet_CloudTable] 物件及 **CustomerEntity** 物件。</span><span class="sxs-lookup"><span data-stu-id="75c13-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="75c13-142">為了準備作業，已建立 [TableOperation][dotnet_TableOperation] 物件以將客戶實體插入資料表。</span><span class="sxs-lookup"><span data-stu-id="75c13-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="75c13-143">最後，其呼叫了 [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute] 來執行作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="75c13-144">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="75c13-144">Insert a batch of entities</span></span>
<span data-ttu-id="75c13-145">您可以在單一寫入作業中，插入實體批次至資料表。</span><span class="sxs-lookup"><span data-stu-id="75c13-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="75c13-146">以下是批次作業的其他一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="75c13-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="75c13-147">您可以在同一批次作業中執行更新、刪除和插入。</span><span class="sxs-lookup"><span data-stu-id="75c13-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="75c13-148">單一批次作業最多可包含 100 個實體。</span><span class="sxs-lookup"><span data-stu-id="75c13-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="75c13-149">單一批次作業中的所有實體必須具有相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="75c13-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="75c13-150">雖然可以單一批次作業的形式來執行查詢，但該查詢必須是批次中的唯一作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="75c13-151">下列程式碼範例會建立兩個實體物件，並使用 [Insert][dotnet_TableBatchOperation_Insert] 方法將每個物件新增至 [TableBatchOperation][dotnet_TableBatchOperation]。</span><span class="sxs-lookup"><span data-stu-id="75c13-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="75c13-152">然後會呼叫 [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] 以執行作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="75c13-153">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="75c13-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="75c13-154">若要向資料表查詢資料分割中的所有實體，請使用 [TableQuery][dotnet_TableQuery] 物件。</span><span class="sxs-lookup"><span data-stu-id="75c13-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="75c13-155">下列程式碼範例會指定篩選器來篩選出資料分割索引鍵為 'Smith' 的實體。</span><span class="sxs-lookup"><span data-stu-id="75c13-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="75c13-156">此範例會將查詢結果中每個實體的欄位列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="75c13-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="75c13-157">擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="75c13-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="75c13-158">如果您不想要查詢資料分割中的所有實體，可結合資料分割索引鍵篩選器與資料列索引鍵篩選器來指定範圍。</span><span class="sxs-lookup"><span data-stu-id="75c13-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="75c13-159">下列程式碼範例會使用兩個篩選器來取得資料分割 'Smith' 中，資料列索引鍵 (名字) 是以字母 'E' 前之字母為開頭的所有實體，然後會列印查詢結果。</span><span class="sxs-lookup"><span data-stu-id="75c13-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="75c13-160">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="75c13-160">Retrieve a single entity</span></span>
<span data-ttu-id="75c13-161">您可以撰寫查詢來擷取單一特定實體。</span><span class="sxs-lookup"><span data-stu-id="75c13-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="75c13-162">下列程式碼會使用 [TableOperation][dotnet_TableOperation] 來指定客戶 'Ben Smith'。</span><span class="sxs-lookup"><span data-stu-id="75c13-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="75c13-163">這個方法只會傳回一個實體而不是集合，而且所傳回的 [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] 值是 **CustomerEntity** 物件。</span><span class="sxs-lookup"><span data-stu-id="75c13-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="75c13-164">若要從資料表服務中擷取單一實體，最快的方法是在查詢中同時指定資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="75c13-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="75c13-165">取代實體</span><span class="sxs-lookup"><span data-stu-id="75c13-165">Replace an entity</span></span>
<span data-ttu-id="75c13-166">若要更新實體，從資料表服務擷取實體、修改實體物件，然後將變更儲存回資料表服務。</span><span class="sxs-lookup"><span data-stu-id="75c13-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="75c13-167">下列程式碼會變更現有客戶的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="75c13-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="75c13-168">此程式碼不會呼叫 [Insert][dotnet_TableOperation_Insert]，而是使用 [Replace][dotnet_TableOperation_Replace]。</span><span class="sxs-lookup"><span data-stu-id="75c13-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="75c13-169">[Replace][dotnet_TableOperation_Replace] 會完全取代伺服器上的實體，但如果伺服器上的實體自擷取後產生變化，作業就會失敗。</span><span class="sxs-lookup"><span data-stu-id="75c13-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="75c13-170">如此會造成失敗，是為了防止應用程式意外覆寫該應用程式的其他元件在擷取後到更新前的這段期間所做的變更。</span><span class="sxs-lookup"><span data-stu-id="75c13-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="75c13-171">正確處理此失敗的方式為重新擷取實體、進行變更 (如果仍然有效)，然後再執行一次 [Replace][dotnet_TableOperation_Replace] 作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="75c13-172">下一節將示範如何覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="75c13-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="75c13-173">插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="75c13-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="75c13-174">如果從伺服器擷取的實體自擷取後發生變化，[Replace][dotnet_TableOperation_Replace] 作業將失敗。</span><span class="sxs-lookup"><span data-stu-id="75c13-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="75c13-175">此外，您必須先從伺服器擷取實體，[Replace][dotnet_TableOperation_Replace] 作業才會成功。</span><span class="sxs-lookup"><span data-stu-id="75c13-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="75c13-176">不過有時候，您不知道實體是否存在於伺服器上且其中所儲存的值是否無關。</span><span class="sxs-lookup"><span data-stu-id="75c13-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="75c13-177">您的更新應該將其全部覆寫。</span><span class="sxs-lookup"><span data-stu-id="75c13-177">Your update should overwrite them all.</span></span> <span data-ttu-id="75c13-178">若要達到此目標，您可以使用 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] 作業。</span><span class="sxs-lookup"><span data-stu-id="75c13-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="75c13-179">此作業會插入實體 (如果其目前並不存在) 或取代實體 (如果其已存在)，不論上次是何時更新。</span><span class="sxs-lookup"><span data-stu-id="75c13-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="75c13-180">在下列程式碼範例中，'Fred Jones' 的客戶實體會建立並插入 'people' 資料表中。</span><span class="sxs-lookup"><span data-stu-id="75c13-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="75c13-181">接下來，我們使用 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] 作業，將具有相同資料分割索引鍵 (Jones) 和資料列索引鍵 (Fred) 的實體儲存到伺服器，但這次使用不同的 PhoneNumber 屬性值。</span><span class="sxs-lookup"><span data-stu-id="75c13-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="75c13-182">因為我們使用 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace]，其所有的屬性值都會被取代。</span><span class="sxs-lookup"><span data-stu-id="75c13-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="75c13-183">不過，如果 'Fred Jones' 實體尚未存在於資料表中，則會予以插入。</span><span class="sxs-lookup"><span data-stu-id="75c13-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="75c13-184">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="75c13-184">Query a subset of entity properties</span></span>
<span data-ttu-id="75c13-185">一項資料表查詢可以只擷取實體的少數屬性而非所有屬性。</span><span class="sxs-lookup"><span data-stu-id="75c13-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="75c13-186">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="75c13-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="75c13-187">下列程式碼中的查詢只會傳回資料表中各實體的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="75c13-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="75c13-188">這是使用 [DynamicTableEntity][dotnet_DynamicTableEntity] 以及 [EntityResolver][dotnet_EntityResolver] 的查詢所完成的。</span><span class="sxs-lookup"><span data-stu-id="75c13-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="75c13-189">您可以在[更新插入和查詢投影簡介的部落格文章][blog_post_upsert]中進一步了解投影。</span><span class="sxs-lookup"><span data-stu-id="75c13-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="75c13-190">儲存體模擬器並不支援投影，因此此程式碼只有在資料表服務中使用帳戶時才會執行。</span><span class="sxs-lookup"><span data-stu-id="75c13-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="75c13-191">刪除實體</span><span class="sxs-lookup"><span data-stu-id="75c13-191">Delete an entity</span></span>
<span data-ttu-id="75c13-192">使用更新實體時所展示的相同方法，輕鬆地在擷取實體後將其刪除。</span><span class="sxs-lookup"><span data-stu-id="75c13-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="75c13-193">下列程式碼會擷取並刪除客戶實體。</span><span class="sxs-lookup"><span data-stu-id="75c13-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="75c13-194">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="75c13-194">Delete a table</span></span>
<span data-ttu-id="75c13-195">最後，下列程式碼範例會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="75c13-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="75c13-196">已刪除的資料表在刪除後一段時間內，將無法重新建立。</span><span class="sxs-lookup"><span data-stu-id="75c13-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="75c13-197">以非同步方式擷取頁面中的實體</span><span class="sxs-lookup"><span data-stu-id="75c13-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="75c13-198">如果您要讀取大量實體，且您想要在擷取實體時處理/顯示實體，但不想等待它們全部傳回，您可以使用分割查詢來擷取實體。</span><span class="sxs-lookup"><span data-stu-id="75c13-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="75c13-199">這個範例示範如何使用 Async-Await 模式，在您等候大量的結果集傳回時亦不會妨礙執行作業，以便在頁面中傳回結果。</span><span class="sxs-lookup"><span data-stu-id="75c13-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="75c13-200">如需在 .NET 中使用 Async-Awaitt 模式的詳細資訊，請參閱 [Async 和 Await (C# 和 Visual Basic) 的非同步程式設計](https://msdn.microsoft.com/library/hh191443.aspx)。</span><span class="sxs-lookup"><span data-stu-id="75c13-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="75c13-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75c13-201">Next steps</span></span>
<span data-ttu-id="75c13-202">現在您已經了解表格儲存體的基本概念，請參考下列連結以了解更複雜的儲存體工作：</span><span class="sxs-lookup"><span data-stu-id="75c13-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="75c13-203">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="75c13-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="75c13-204">如需更多表格儲存體範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="75c13-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="75c13-205">如需可用 API 的完整詳細資訊，請檢視資料表服務參考文件：</span><span class="sxs-lookup"><span data-stu-id="75c13-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="75c13-206">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="75c13-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="75c13-207">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="75c13-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="75c13-208">了解如何使用 [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="75c13-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="75c13-209">如需了解 Azure 中的其他資料儲存選項，請檢視更多功能指南。</span><span class="sxs-lookup"><span data-stu-id="75c13-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="75c13-210">[以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md) 以儲存非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="75c13-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="75c13-211">[使用 .NET (C#) 連接到 SQL Database ](../sql-database/sql-database-develop-dotnet-simple.md) 以儲存關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="75c13-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
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
