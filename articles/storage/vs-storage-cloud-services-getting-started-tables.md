---
title: "開始使用資料表儲存體和 Visual Studio 已連接服務 (雲端服務) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接到儲存體帳戶之後，如何在 Visual Studio 雲端服務專案中開始使用 Azure 資料表儲存體"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3208ddb1a1246a5ff25d272bfc7d8ba842348a36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="41b6d-103">開始使用 Azure 資料表儲存體和 Visual Studio 已連接服務 (雲端服務專案)</span><span class="sxs-lookup"><span data-stu-id="41b6d-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="41b6d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="41b6d-104">Overview</span></span>
<span data-ttu-id="41b6d-105">本文說明如何在您使用 Visual Studio 的 [新增連接的服務]  對話方塊建立或參考雲端服務專案中的 Azure 儲存體帳戶之後，開始在 Visual Studio 中使用 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="41b6d-106">[新增連接的服務]  作業會安裝適當的 NuGet 套件，以存取專案中的 Azure 儲存體，並將儲存體帳戶的連接字串新增至您的專案設定檔。</span><span class="sxs-lookup"><span data-stu-id="41b6d-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="41b6d-107">Azure 資料表儲存體服務可讓您儲存大量的結構化資料。</span><span class="sxs-lookup"><span data-stu-id="41b6d-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="41b6d-108">此服務是一個 NoSQL 資料存放區，接受來自 Azure 雲端內外經過驗證的呼叫。</span><span class="sxs-lookup"><span data-stu-id="41b6d-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="41b6d-109">Azure 資料表很適合儲存結構化、非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="41b6d-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="41b6d-110">若要開始，首先您必須在儲存體帳戶中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="41b6d-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="41b6d-111">我們將說明如何使用程式碼建立 Azure 資料表，以及如何執行基本的資料表和實體作業，例如新增、修改、讀取和讀取資料表實體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="41b6d-112">這些範例均以 C\# 程式碼撰寫，並使用 [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="41b6d-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="41b6d-113">**注意：** 有一些 API會以非同步方式對 Azure 儲存體執行呼叫。</span><span class="sxs-lookup"><span data-stu-id="41b6d-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="41b6d-114">如需詳細資訊，請參閱 [使用 Async 及 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="41b6d-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="41b6d-115">以下程式碼假設使用非同步程式設計方法。</span><span class="sxs-lookup"><span data-stu-id="41b6d-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="41b6d-116">如需以程式設計方式處理資料表的詳細資訊，請參閱 [以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md) 。</span><span class="sxs-lookup"><span data-stu-id="41b6d-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="41b6d-117">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="41b6d-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="41b6d-118">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。</span><span class="sxs-lookup"><span data-stu-id="41b6d-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="41b6d-119">若需要如何編寫 ASP.NET 應用程式的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。</span><span class="sxs-lookup"><span data-stu-id="41b6d-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="41b6d-120">在程式碼中存取資料表</span><span class="sxs-lookup"><span data-stu-id="41b6d-120">Access tables in code</span></span>
<span data-ttu-id="41b6d-121">若要存取雲端服務專案中的資料表，您需要將下列項目併入至存取 Azure 資料表儲存體的任何 C# 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="41b6d-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="41b6d-122">請確定 C# 檔案頂端的命名空間宣告包含這些 **using** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="41b6d-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="41b6d-123">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="41b6d-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="41b6d-124">使用下列程式碼，從 Azure 服務組態取得儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="41b6d-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="41b6d-125">請在下列範例中的程式碼前面使用上述所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="41b6d-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="41b6d-126">取得 **CloudTableClient** 物件，以參考您儲存體帳戶中的資料表物件。</span><span class="sxs-lookup"><span data-stu-id="41b6d-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="41b6d-127">取得 **CloudTable** 參考物件，以參考特定資料表與實體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="41b6d-128">在程式碼中建立資料表</span><span class="sxs-lookup"><span data-stu-id="41b6d-128">Create a table in code</span></span>
<span data-ttu-id="41b6d-129">若要建立 Azure 資料表，只要依照＜存取程式碼中的資料表＞一節所述，在取得 **CloudTable** 物件後加入 **CreateIfNotExistsAsync** 呼叫即可。</span><span class="sxs-lookup"><span data-stu-id="41b6d-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="41b6d-130">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="41b6d-130">Add an entity to a table</span></span>
<span data-ttu-id="41b6d-131">若要將實體新增至資料表，請建立一個類別來定義實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="41b6d-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="41b6d-132">下列程式碼會定義稱為 **CustomerEntity** 的實體類別，其使用客戶名字作為資料列索引鍵，並使用姓氏作為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="41b6d-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="41b6d-133">實體相關的資料表作業會使用您稍早在＜在程式碼中存取資料表＞中建立的 **CloudTable** 物件執行。</span><span class="sxs-lookup"><span data-stu-id="41b6d-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="41b6d-134">**TableOperation** 物件要執行的操作。</span><span class="sxs-lookup"><span data-stu-id="41b6d-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="41b6d-135">下列程式碼範例顯示如何建立 **CloudTable** 物件及 **CustomerEntity** 物件。</span><span class="sxs-lookup"><span data-stu-id="41b6d-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="41b6d-136">為了準備這項操作，其建立了 **TableOperation** ，以便在資料表中插入客戶實體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="41b6d-137">最後會呼叫 **CloudTable.ExecuteAsync**來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="41b6d-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="41b6d-138">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="41b6d-138">Insert a batch of entities</span></span>
<span data-ttu-id="41b6d-139">您可以在單一寫入操作中將多個項目插入至資料表。</span><span class="sxs-lookup"><span data-stu-id="41b6d-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="41b6d-140">下列程式碼範例會建立兩個實體物件 ("Jeff Smith" 和 "Ben Smith")，並使用 Insert 方法將這兩個物件加入 **TableBatchOperation** 物件中，然後再呼叫 **CloudTable.ExecuteBatchAsync** 啟動作業。</span><span class="sxs-lookup"><span data-stu-id="41b6d-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="41b6d-141">取得資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="41b6d-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="41b6d-142">若要向資料表查詢資料分割中的所有實體，請使用 **TableQuery** 物件。</span><span class="sxs-lookup"><span data-stu-id="41b6d-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="41b6d-143">下列程式碼範例會指定篩選器來篩選出資料分割索引鍵為 'Smith' 的實體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="41b6d-144">此範例會將查詢結果中每個實體的欄位列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="41b6d-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
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


## <a name="get-a-single-entity"></a><span data-ttu-id="41b6d-145">取得單一實體</span><span class="sxs-lookup"><span data-stu-id="41b6d-145">Get a single entity</span></span>
<span data-ttu-id="41b6d-146">您可以撰寫查詢來取得單一特定實體。</span><span class="sxs-lookup"><span data-stu-id="41b6d-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="41b6d-147">下列程式碼使用 **TableOperation** 物件來指定名為 'Ben Smith' 的客戶。</span><span class="sxs-lookup"><span data-stu-id="41b6d-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="41b6d-148">這個方法只會傳回一個實體而不是集合，而且所傳回的 **TableResult.Result** 值是 **CustomerEntity** 物件。</span><span class="sxs-lookup"><span data-stu-id="41b6d-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="41b6d-149">若要從「資料表」  服務中擷取單一實體，最快的方法是在查詢中同時指定資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="41b6d-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="41b6d-150">刪除實體</span><span class="sxs-lookup"><span data-stu-id="41b6d-150">Delete an entity</span></span>
<span data-ttu-id="41b6d-151">找到實體之後，您可以刪除它。</span><span class="sxs-lookup"><span data-stu-id="41b6d-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="41b6d-152">下列程式碼會尋找名為 "Ben Smith" 的客戶實體，如果找到，就會刪除它。</span><span class="sxs-lookup"><span data-stu-id="41b6d-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="41b6d-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41b6d-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

