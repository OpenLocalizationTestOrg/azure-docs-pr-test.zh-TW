---
title: "使用資料表儲存體和 Visual Studio 啟動 aaaHow tooget 已連線的服務 (ASP.NET Core) |Microsoft 文件"
description: "如何 tooget 開始使用 Visual Studio 中 ASP.NET Core 專案中的 Azure 資料表儲存體之後連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 6a8fb6aa085d78a087fcd14adbc765a0d59e0308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="f5748-103">Tooget 如何開始使用 Azure 資料表儲存體和 Visual Studio 已連接服務</span><span class="sxs-lookup"><span data-stu-id="f5748-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="f5748-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f5748-104">Overview</span></span>
<span data-ttu-id="f5748-105">本文說明如何開始使用 Azure 資料表儲存體，在 Visual Studio 中建立或參考使用 ASP.NET Core 專案中的 Azure 儲存體帳戶後 hello Visual Studio**加入已連接服務**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f5748-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="f5748-106">hello Azure 資料表儲存體服務可讓您 toostore 大量結構化資料。</span><span class="sxs-lookup"><span data-stu-id="f5748-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="f5748-107">hello 服務是可接受來自內部和外部 hello Azure 雲端的已驗證的呼叫的 NoSQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f5748-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="f5748-108">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="f5748-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="f5748-109">hello**加入已連接服務**作業安裝在您的專案中的適當 NuGet 封裝 tooaccess hello Azure 儲存體，並新增 hello 連接字串，hello 儲存體帳戶 tooyour 專案組態檔。</span><span class="sxs-lookup"><span data-stu-id="f5748-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="f5748-110">如需其他有關使用 Azure 資料表儲存體的一般資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="f5748-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="f5748-111">tooget 開始，您必須先 toocreate 資料表儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f5748-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="f5748-112">我們將示範如何 toocreate Azure 資料表中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f5748-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="f5748-113">我們也會顯示您 tooperform 基本資料表和實體作業，例如加入、 修改、 讀取以及讀取資料表實體。</span><span class="sxs-lookup"><span data-stu-id="f5748-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="f5748-114">hello 範例以 C 撰寫\#程式碼和使用適用於.NET 的 hello Azure 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="f5748-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="f5748-115">**請注意**-某些 hello 應用程式開發介面中執行 ASP.NET Core tooAzure 存放裝置的呼叫是非同步。</span><span class="sxs-lookup"><span data-stu-id="f5748-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="f5748-116">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f5748-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="f5748-117">下列程式碼 hello 假設正在使用非同步程式設計的方法。</span><span class="sxs-lookup"><span data-stu-id="f5748-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="f5748-118">在程式碼中存取資料表</span><span class="sxs-lookup"><span data-stu-id="f5748-118">Access tables in code</span></span>
<span data-ttu-id="f5748-119">tooaccess ASP.NET Core 專案中的資料表，您需要下列項目 tooany C# 來源檔案，存取 Azure 資料表儲存體 tooinclude hello。</span><span class="sxs-lookup"><span data-stu-id="f5748-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="f5748-120">請確定在 hello hello C# 檔案最上方的 hello 命名空間宣告包括**使用**陳述式。</span><span class="sxs-lookup"><span data-stu-id="f5748-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="f5748-121">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="f5748-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f5748-122">下列程式碼 tooget 使用 hello hello 您的儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態。</span><span class="sxs-lookup"><span data-stu-id="f5748-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="f5748-123">**請注意**-hello 遵循範例中使用所有 hello hello 程式碼前面的程式碼上方。</span><span class="sxs-lookup"><span data-stu-id="f5748-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="f5748-124">取得**CloudTableClient** tooreference hello 資料表物件儲存體帳戶中的物件。</span><span class="sxs-lookup"><span data-stu-id="f5748-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="f5748-125">取得**CloudTable**參考物件 tooreference 特定資料表和實體。</span><span class="sxs-lookup"><span data-stu-id="f5748-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="f5748-126">在程式碼中建立資料表</span><span class="sxs-lookup"><span data-stu-id="f5748-126">Create a table in code</span></span>
<span data-ttu-id="f5748-127">toocreate hello Azure 資料表，只要加入呼叫太**CreateIfNotExistsAsync()**。</span><span class="sxs-lookup"><span data-stu-id="f5748-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="f5748-128">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="f5748-128">Add an entity tooa table</span></span>
<span data-ttu-id="f5748-129">tooadd 實體 tooa 表您建立的類別所定義之實體的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="f5748-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="f5748-130">hello 下列程式碼會定義實體類別，稱為**CustomerEntity**使用 hello hello 資料列索引鍵為客戶的名字和姓氏 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f5748-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="f5748-131">關於實體的資料表作業完成後使用 hello **CloudTable**物件建立稍早在 < 程式碼中存取資料表 >。</span><span class="sxs-lookup"><span data-stu-id="f5748-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="f5748-132">hello **TableOperation**物件都代表 hello 作業 toobe 完成。</span><span class="sxs-lookup"><span data-stu-id="f5748-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="f5748-133">hello 下列程式碼範例顯示如何 toocreate **CloudTable**物件和**CustomerEntity**物件。</span><span class="sxs-lookup"><span data-stu-id="f5748-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="f5748-134">tooprepare hello 作業， **TableOperation** tooinsert hello customer 實體建立 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="f5748-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="f5748-135">最後，藉由呼叫 CloudTable.ExecuteAsync 執行 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="f5748-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="f5748-136">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="f5748-136">Insert a batch of entities</span></span>
<span data-ttu-id="f5748-137">您可以在單一寫入操作中將多個項目插入至資料表。</span><span class="sxs-lookup"><span data-stu-id="f5748-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="f5748-138">hello 下列程式碼範例會建立兩個實體物件 （"Jeff Smith"和"Ben Smith"）、 將它們加入 tooa **TableBatchOperation**物件使用 hello**插入**方法，然後按一下 啟動 hello 作業呼叫 CloudTable.ExecuteBatchAsync。</span><span class="sxs-lookup"><span data-stu-id="f5748-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="f5748-139">取得 hello 實體的所有資料分割中</span><span class="sxs-lookup"><span data-stu-id="f5748-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="f5748-140">資料表中的所有資料分割，使用中的 hello 實體 tooquery **TableQuery**物件。</span><span class="sxs-lookup"><span data-stu-id="f5748-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="f5748-141">hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="f5748-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="f5748-142">這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。</span><span class="sxs-lookup"><span data-stu-id="f5748-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

## <a name="get-a-single-entity"></a><span data-ttu-id="f5748-143">取得單一實體</span><span class="sxs-lookup"><span data-stu-id="f5748-143">Get a single entity</span></span>
<span data-ttu-id="f5748-144">您可以撰寫查詢 tooget 單一的特定實體。</span><span class="sxs-lookup"><span data-stu-id="f5748-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="f5748-145">hello 下列程式碼使用**TableOperation** toospecify 客戶，名為 ' Ben Smith' 的物件。</span><span class="sxs-lookup"><span data-stu-id="f5748-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="f5748-146">這個方法會傳回單一實體，而不是集合，而且 hello 傳回值中的**TableResult.Result**是**CustomerEntity**物件。</span><span class="sxs-lookup"><span data-stu-id="f5748-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="f5748-147">在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello hello 從單一實體**資料表**服務。</span><span class="sxs-lookup"><span data-stu-id="f5748-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="f5748-148">刪除實體</span><span class="sxs-lookup"><span data-stu-id="f5748-148">Delete an entity</span></span>
<span data-ttu-id="f5748-149">找到實體之後，您可以刪除它。</span><span class="sxs-lookup"><span data-stu-id="f5748-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="f5748-150">hello 下列程式碼會尋找名為"Ben Smith"customer 實體，如果找到，就會刪除它。</span><span class="sxs-lookup"><span data-stu-id="f5748-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f5748-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5748-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

