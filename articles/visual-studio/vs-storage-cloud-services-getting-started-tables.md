---
title: "開始使用資料表儲存體和 Visual Studio 已連線的服務 （雲端服務） 的 aaaGet |Microsoft 文件"
description: "Tooget 啟動連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務之後，在 Visual Studio 中的雲端服務專案中使用 Azure 資料表儲存體的方式"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>開始使用 Azure 資料表儲存體和 Visual Studio 已連接服務 (雲端服務專案)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>概觀
本文章說明 tooget 開始使用 Visual Studio 中的 Azure 資料表儲存體之後您建立或參考 Azure 儲存體帳戶的雲端服務專案中使用 Visual Studio hello,**加入已連接服務**對話方塊. hello**加入已連接服務**作業安裝在您的專案中的適當 NuGet 封裝 tooaccess hello Azure 儲存體，並新增 hello 連接字串，hello 儲存體帳戶 tooyour 專案組態檔。

hello Azure 資料表儲存體服務可讓您 toostore 大量結構化資料。 hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。 Azure 資料表很適合儲存結構化、非關聯式資料。

tooget 開始，您必須先 toocreate 資料表儲存體帳戶中。 我們將示範如何 toocreate Azure 資料表中的程式碼，以及如何 tooperform 基本資料表和實體作業，例如加入、 修改、 讀取以及讀取資料表實體。 hello 範例以 C 撰寫\#程式碼和使用 hello[適用於.NET 的 Microsoft Azure 儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/dn261237.aspx)。

**注意：** hello Api 執行呼叫 tooAzure 存放裝置，有些非同步。 如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。 下列程式碼 hello 假設正在使用非同步程式設計的方法。

* 如需以程式設計方式處理資料表的詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](../storage/storage-dotnet-how-to-use-tables.md) 。
* 如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。
* 如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。
* 若需要如何編寫 ASP.NET 應用程式的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。

## <a name="access-tables-in-code"></a>在程式碼中存取資料表
tooaccess 雲端服務專案中的資料表，您需要下列項目 tooany C# 來源檔案，存取 Azure 資料表儲存體 tooinclude hello。

1. 請確定在 hello hello C# 檔案最上方的 hello 命名空間宣告包括**使用**陳述式。
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 使用 hello hello Azure 服務組態中的下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊。
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > 您可以使用所有前面 hello 程式碼的程式碼上方的 hello hello 遵循範例中。
   > 
   > 
3. 取得**CloudTableClient** tooreference hello 資料表物件儲存體帳戶中的物件。
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. 取得**CloudTable**參考物件 tooreference 特定資料表和實體。
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>在程式碼中建立資料表
toocreate hello Azure 資料表，只要加入呼叫太**CreateIfNotExistsAsync** toohello 您之後**CloudTable** hello < 存取資料表中的程式碼 > 一節中所述的物件。

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
tooadd 實體 tooa 資料表，建立一個類別來定義實體的 hello 屬性。 hello 下列程式碼會定義實體類別，稱為**CustomerEntity**使用 hello 客戶的名字為 hello 資料列索引鍵和 hello hello 資料分割索引鍵的最後一個名稱。

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

關於實體的資料表作業完成後使用 hello **CloudTable**您先前在 < 程式碼中存取資料表 >。 建立的物件 hello **TableOperation**物件都代表 hello 作業 toobe 完成。 hello 下列程式碼範例顯示如何 toocreate **CloudTable**物件和**CustomerEntity**物件。 tooprepare hello 作業， **TableOperation** tooinsert hello customer 實體建立 hello 資料表。 最後，藉由呼叫執行 hello 作業**CloudTable.ExecuteAsync**。

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>插入實體批次
您可以在單一寫入操作中將多個項目插入至資料表。 hello 下列程式碼範例會建立兩個實體物件 （"Jeff Smith"和"Ben Smith"）、 將它們加入 tooa **TableBatchOperation**物件使用 hello 插入方法並開始然後藉由呼叫 hello 作業**CloudTable.ExecuteBatchAsync**。

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a>取得 hello 實體的所有資料分割中
資料表中的所有資料分割，使用中的 hello 實體 tooquery **TableQuery**物件。 hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。 這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

    return View();


## <a name="get-a-single-entity"></a>取得單一實體
您可以撰寫查詢 tooget 單一的特定實體。 hello 下列程式碼使用**TableOperation** toospecify 客戶，名為 ' Ben Smith' 的物件。 這個方法會傳回單一實體，而不是集合，而且 hello 傳回值中的**TableResult.Result**是**CustomerEntity**物件。 在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello hello 從單一實體**資料表**服務。

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>刪除實體
找到實體之後，您可以刪除它。 hello 下列程式碼會尋找名為"Ben Smith"customer 實體，如果找到，就會刪除它。

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a>後續步驟
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]
