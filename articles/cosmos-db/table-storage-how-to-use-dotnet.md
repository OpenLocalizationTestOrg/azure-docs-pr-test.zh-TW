---
title: "開始使用適用於.NET 的 Azure 資料表儲存體 aaaGet |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>以 .NET 開始使用 Azure 表格儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Azure 資料表儲存體是儲存結構化的 NoSQL 資料 hello 雲端中的提供索引鍵/屬性存放區搭配 schemaless 設計的服務。 因為資料表儲存體是 schemaless，很容易 tooadapt 資料做為 hello 需要的應用程式 evolve。 存取 tooTable 儲存體資料非常快速且符合成本效益的許多類型的應用程式，，和通常中較低成本比傳統的 SQL 資料磁碟區類似。

您可以使用資料表儲存體 toostore 彈性的資料集像是使用者資料的 web 應用程式、 通訊錄，裝置資訊或其他類型的服務需要的中繼資料。 您可以將任意數目的實體儲存在資料表中，而且儲存體帳戶包含任何數量的資料表，向上 toohello hello 儲存體帳戶的容量限制。

### <a name="about-this-tutorial"></a>關於本教學課程
本教學課程示範如何 toouse hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)中一些常見的 Azure 資料表儲存體案例。 這些案例會使用 C# 作為範例，以建立和刪除資料表，並插入、更新、刪除及查詢資料表資料。

## <a name="prerequisites"></a>必要條件

您需要 hello toocomplete 遵循本教學課程成功：

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [適用於.NET 的 Azure 設定管理員](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>更多範例
如需使用表格儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)。 您可以下載 hello 範例應用程式並執行它，或瀏覽 hello GitHub 上的程式碼。

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>新增 using 指示詞
新增下列 hello**使用**指示詞 toohello 頂端 hello`Program.cs`檔案：

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>剖析 hello 連接字串
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>建立 hello 表格服務用戶端
hello [CloudTableClient] [ dotnet_CloudTableClient]類別可讓您 tooretrieve 資料表和資料表儲存體中儲存的實體。 以下是其中一種方式 toocreate hello 表格服務用戶端：

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

現在您已準備好 toowrite 讀取和寫入資料 tooTable 儲存的程式碼。

## <a name="create-a-table"></a>建立資料表
這個範例會示範如何 toocreate 如果不存在的資料表：

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

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
實體對應 tooC # 物件使用的自訂類別衍生自[TableEntity][dotnet_TableEntity]。 tooadd 實體 tooa 資料表，建立一個類別來定義實體的 hello 屬性。 hello 下列程式碼會定義為 hello 資料列索引鍵和姓氏的 hello 客戶名字做 hello 資料分割索引鍵的實體類別。 在一起，實體的資料分割和資料列索引鍵內唯一識別此 hello 資料表。 以 hello 速度的不同實體可查詢相同的資料分割索引鍵的實體資料分割索引鍵，但使用不同的資料分割索引鍵可讓平行作業的更佳的延展性。 儲存在資料表中的實體 toobe 必須是支援的型別，例如衍生自 hello [TableEntity] [ dotnet_TableEntity]類別。 您想要 toostore 資料表中的實體屬性必須是 hello 型別的公用屬性，而且支援取得和設定的值。 此外，您的實體類型「必須」  公開無參數建構函式。

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

包含實體的資料表作業將會透過 hello [CloudTable] [ dotnet_CloudTable] hello 「 建立資料表 」 一節中稍早建立的物件。 hello 作業 toobe 執行由[TableOperation] [ dotnet_TableOperation]物件。 hello 下列程式碼範例顯示 hello 的建立 hello [CloudTable] [ dotnet_CloudTable]物件，然後**CustomerEntity**物件。 tooprepare hello 作業， [TableOperation] [ dotnet_TableOperation]物件建立到 hello 資料表 tooinsert hello customer 實體。 最後，藉由呼叫執行 hello 作業[CloudTable][dotnet_CloudTable]。[執行][dotnet_CloudTable_Execute]。

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

## <a name="insert-a-batch-of-entities"></a>插入實體批次
您可以在單一寫入作業中，插入實體批次至資料表。 以下是批次作業的其他一些注意事項：

* 您可以執行更新、 刪除及插入相同的 hello 在單一批次作業。
* 在單一批次作業可以包括安裝 too100 實體。
* 在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。
* 雖然可能 tooperform 查詢以批次作業，它必須是 hello hello 批次中唯一的作業。

hello 下列程式碼範例會建立兩個實體物件並加入每個太[TableBatchOperation] [ dotnet_TableBatchOperation]使用 hello[插入][ dotnet_TableBatchOperation_Insert]方法。 然後， [CloudTable][dotnet_CloudTable]。[ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch]稱為 tooexecute hello 作業。

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

## <a name="retrieve-all-entities-in-a-partition"></a>擷取資料分割中的所有實體
資料表的資料分割，使用中的所有實體 tooquery [TableQuery] [ dotnet_TableQuery]物件。 hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。 這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>擷取資料分割中某個範圍的實體
如果您不想 tooquery 資料分割中的所有實體，您可以藉由結合 hello 與資料列索引鍵的篩選資料分割索引鍵篩選指定範圍。 hello 下列程式碼範例會使用兩個篩選 tooget 所有實體分割區 'Smith' hello 資料列索引鍵 （第一個名稱） 開頭為字母 'E' 之前在 hello 字母，然後列印 hello 查詢結果中。

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

## <a name="retrieve-a-single-entity"></a>擷取單一實體
您可以撰寫查詢 tooretrieve 單一的特定實體。 hello 下列程式碼使用[TableOperation] [ dotnet_TableOperation] toospecify hello 客戶 ' Ben Smith'。 這個方法會傳回單一實體，而不是集合，且 hello 傳回值中的[TableResult][dotnet_TableResult]。[結果][ dotnet_TableResult_Result]是**CustomerEntity**物件。 在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。

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

## <a name="replace-an-entity"></a>取代實體
tooupdate 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。 hello 下列程式碼變更現有的客戶電話號碼。 此程式碼不會呼叫 [Insert][dotnet_TableOperation_Insert]，而是使用 [Replace][dotnet_TableOperation_Replace]。 [取代][ dotnet_TableOperation_Replace]原因 hello 完全取代 hello 伺服器上的實體 toobe，除非變更 hello hello 伺服器上的實體自擷取後，在此情況下 hello 作業將會失敗。 此失敗是的 tooprevent hello 擷取和更新您的應用程式的另一個元件之間，進行您的應用程式不慎覆寫變更。 hello 正確處理失敗的恢復 tooretrieve hello 實體，進行變更 （如果仍然有效），然後再執行另一個[取代][ dotnet_TableOperation_Replace]作業。 hello 下一節將示範如何 toooverride 這種行為。

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

## <a name="insert-or-replace-an-entity"></a>插入或取代實體
[取代][ dotnet_TableOperation_Replace] hello 實體已變更，因為它從 hello 伺服器擷取作業會失敗。 此外，您必須擷取從 hello 伺服器 hello 實體先讓 hello[取代][ dotnet_TableOperation_Replace]作業 toobe 成功。 有時候，不過，您不知道是否 hello 實體 hello 伺服器上存在和 hello 目前儲存在它的值無關。 您的更新應該將其全部覆寫。 tooaccomplish，您會使用[InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace]作業。 如果它不存在，或予以取代，若是如此，無論 hello 上次更新已進行時，這項作業會插入 hello 實體。

在下列程式碼範例的 hello，會建立 ' Fred Jones' [客戶] 實體，並將其插入 hello 'people' 資料表中。 接下來，我們使用 hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace]作業 toosave hello 與實體相同的資料分割索引鍵 (Jones) 和資料列金鑰 (Fred) toohello 伺服器，這一次使用不同的值 hello 電話號碼屬性。 因為我們使用 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace]，其所有的屬性值都會被取代。 不過，如果 ' Fred Jones' 實體以往已經存在於 hello 資料表中，它會插入。

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

## <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
資料表查詢可以擷取只需要幾個屬性，從實體而不是所有 hello 實體屬性。 這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。 hello，下列程式碼中的 hello 查詢會傳回只 hello 電子郵件地址的實體 hello 資料表中。 這是使用 [DynamicTableEntity][dotnet_DynamicTableEntity] 以及 [EntityResolver][dotnet_EntityResolver] 的查詢所完成的。 您可以進一步了解在 hello[簡介 Upsert 和查詢投影部落格文章][blog_post_upsert]。 投射不是支援 hello 儲存體模擬器，因此在 hello 表格服務中使用的帳戶時，才執行此程式碼。

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

## <a name="delete-an-entity"></a>刪除實體
您已在使用 hello 擷取之後，您可以輕鬆地刪除實體的更新實體顯示的相同模式。 下列程式碼的 hello 擷取，並刪除一個 customer 實體。

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

## <a name="delete-a-table"></a>刪除資料表
最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。 已刪除的資料表將無法使用 toobe 重新建立一段時間 hello 刪除。

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

## <a name="retrieve-entities-in-pages-asynchronously"></a>以非同步方式擷取頁面中的實體
如果您正在閱讀大量實體，且想 tooprocess/顯示實體時擷取，而非等待它們所有 tooreturn，您可以擷取實體使用分割的查詢。 這個範例會示範如何 tooreturn 結果頁面使用 hello 非同步等候模式，讓您不會封鎖執行中的等待結果 tooreturn 的大型集合。 如需有關使用 hello.NET 中的非同步 Await 模式，請參閱 <<c0> [ 使用 Async 和 Await （C# 和 Visual Basic） 的非同步程式設計](https://msdn.microsoft.com/library/hh191443.aspx)。

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

## <a name="next-steps"></a>後續步驟
現在，您學到的資料表儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn:

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* 如需更多表格儲存體範例，請參閱 [在 .NET 中開始使用 Azure 表格儲存體](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* 如需可用的應用程式開發介面的完整詳細資料的資料表服務參考文件的檢視 hello:
* [Storage Client Library for .NET 參考資料](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [REST API 參考資料](http://msdn.microsoft.com/library/azure/dd179355)
* 了解您所撰寫 toosimplify hello 程式碼如何使用 hello 與 Azure 儲存體 toowork [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* 檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。
* [開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)toostore 非結構化的資料。
* [使用.NET (C#) 連線 tooSQL 資料庫](../sql-database/sql-database-develop-dotnet-simple.md)toostore 關聯式資料。

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
