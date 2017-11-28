---
title: "如何使用資料表儲存體 (C++) | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: d68843153921c72f6e808f62e82d3686c7e2f160
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="71cdb-103">如何使用 C++ 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="71cdb-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="71cdb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="71cdb-104">Overview</span></span>
<span data-ttu-id="71cdb-105">本指南將示範如何使用 Azure 資料表儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="71cdb-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="71cdb-106">這些範例均以 C++ 撰寫，並使用 [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="71cdb-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="71cdb-107">所涵蓋的案例包括**建立和刪除資料表**，以及**使用資料表實體**。</span><span class="sxs-lookup"><span data-stu-id="71cdb-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="71cdb-108">本指南以 Azure Storage Client Library for C++ 1.0.0 版和更新版本為對象。</span><span class="sxs-lookup"><span data-stu-id="71cdb-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="71cdb-109">建議的版本是 Storage Client Library 2.2.0，可透過 [NuGet](http://www.nuget.org/packages/wastorage) 或 [GitHub](https://github.com/Azure/azure-storage-cpp/) 取得。</span><span class="sxs-lookup"><span data-stu-id="71cdb-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="71cdb-110">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="71cdb-110">Create a C++ application</span></span>
<span data-ttu-id="71cdb-111">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="71cdb-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="71cdb-112">若要這樣做，您需要安裝 Azure Storage Client Library for C++，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="71cdb-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="71cdb-113">若要安裝 Azure Storage Client Library for C++，您可以使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="71cdb-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="71cdb-114">**Linux：** 遵循 [Azure Storage Client Library for C++ 讀我檔案](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 頁面中提供的指示進行。</span><span class="sxs-lookup"><span data-stu-id="71cdb-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="71cdb-115">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="71cdb-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="71cdb-116">在 [NuGet 套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 中輸入下列命令，然後按下 Enter。</span><span class="sxs-lookup"><span data-stu-id="71cdb-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="71cdb-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="71cdb-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="71cdb-118">設定您的應用程式來存取資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="71cdb-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="71cdb-119">在您要使用 Azure 儲存體 API 來存取資料表的 C++ 檔案頂端，加入下列 include 陳述式：</span><span class="sxs-lookup"><span data-stu-id="71cdb-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="71cdb-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="71cdb-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="71cdb-121">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="71cdb-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="71cdb-122">執行用戶端應用程式時，您必須提供下列格式的儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="71cdb-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="71cdb-123">使用您的儲存體帳戶名稱和儲存體存取金鑰，來輸入 [Azure 入口網站](https://portal.azure.com)中所列的儲存體帳戶的 AccountName 和 AccountKey 值。</span><span class="sxs-lookup"><span data-stu-id="71cdb-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="71cdb-124">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="71cdb-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="71cdb-125">本範例將示範如何宣告靜態欄位來存放連接字串：</span><span class="sxs-lookup"><span data-stu-id="71cdb-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="71cdb-126">若要在本機 Windows 電腦中測試您的應用程式，可以使用隨 [Azure SDK](https://azure.microsoft.com/downloads/) 一起安裝的 Azure [儲存體模擬器](storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="71cdb-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="71cdb-127">儲存體模擬器是一個公用程式，可模擬本機開發電腦上的 Azure Blob、佇列和表格服務。</span><span class="sxs-lookup"><span data-stu-id="71cdb-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="71cdb-128">下列範例示範如何宣告靜態欄位以便將連接字串存放到本機儲存體模擬器中：</span><span class="sxs-lookup"><span data-stu-id="71cdb-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="71cdb-129">若要啟動 Azure 儲存體模擬器，請按一下 [開始] 按鈕或按下 [Windows] 鍵。</span><span class="sxs-lookup"><span data-stu-id="71cdb-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="71cdb-130">開始輸入 **Azure 儲存體模擬器**，然後從應用程式清單選取 [Microsoft Azure 儲存體模擬器]。</span><span class="sxs-lookup"><span data-stu-id="71cdb-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="71cdb-131">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="71cdb-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="71cdb-132">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="71cdb-132">Retrieve your connection string</span></span>
<span data-ttu-id="71cdb-133">您可以使用 **cloud_storage_account** 類別來代表儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="71cdb-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="71cdb-134">若要從儲存體連接字串擷取儲存體帳戶資訊，您可以使用 parse 方法。</span><span class="sxs-lookup"><span data-stu-id="71cdb-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="71cdb-135">接著，取得 **cloud_table_client** 類別的參考，因為這可讓您取得資料表儲存體服務內儲存的資料表和實體的參考物件。</span><span class="sxs-lookup"><span data-stu-id="71cdb-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="71cdb-136">下列程式碼會使用我們在前面擷取的儲存體帳戶物件建立 **cloud_table_client** 物件：</span><span class="sxs-lookup"><span data-stu-id="71cdb-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="71cdb-137">建立資料表</span><span class="sxs-lookup"><span data-stu-id="71cdb-137">Create a table</span></span>
<span data-ttu-id="71cdb-138">**cloud_table_client** 物件可讓您取得資料表和實體的參考物件。</span><span class="sxs-lookup"><span data-stu-id="71cdb-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="71cdb-139">下列程式碼會建立 **cloud_table_client** 物件，並使用該物件建立新資料表。</span><span class="sxs-lookup"><span data-stu-id="71cdb-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="71cdb-140">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="71cdb-140">Add an entity to a table</span></span>
<span data-ttu-id="71cdb-141">若要將實體新增至資料表，請建立一個新的 **table_entity** 物件，然後將該物件傳遞至 **table_operation::insert_entity**。</span><span class="sxs-lookup"><span data-stu-id="71cdb-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="71cdb-142">下列程式碼會使用客戶名字做為資料列索引鍵，並使用姓氏做為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="71cdb-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="71cdb-143">實體的資料分割索引鍵和資料列索引鍵共同唯一識別資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="71cdb-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="71cdb-144">相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快，但使用不同的資料分割索引鍵可獲得更大的平行操作延展性。</span><span class="sxs-lookup"><span data-stu-id="71cdb-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="71cdb-145">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="71cdb-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="71cdb-146">下列程式碼會建立 **table_entity** 的新執行個體，其中含有一些要儲存的客戶資料。</span><span class="sxs-lookup"><span data-stu-id="71cdb-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="71cdb-147">程式碼接著會呼叫 **table_operation::insert_entity** 來建立 **table_operation** 物件，以便將實體插入資料表中，並將新的資料表與該物件建立關聯。</span><span class="sxs-lookup"><span data-stu-id="71cdb-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="71cdb-148">最後，程式碼會針對 **cloud_table** 物件呼叫 execute 方法。</span><span class="sxs-lookup"><span data-stu-id="71cdb-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="71cdb-149">此外，新的 **table_operation** 會傳送一個要求到資料表服務，以便將新的客戶實體插入到 "people" 資料表。</span><span class="sxs-lookup"><span data-stu-id="71cdb-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="71cdb-150">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="71cdb-150">Insert a batch of entities</span></span>
<span data-ttu-id="71cdb-151">您可以在單一寫入操作中，插入實體批次至資料表服務。</span><span class="sxs-lookup"><span data-stu-id="71cdb-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="71cdb-152">下列程式碼會建立一個 **table_batch_operation** 物件，然後在其中新增三個插入操作。</span><span class="sxs-lookup"><span data-stu-id="71cdb-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="71cdb-153">加入每個插入操作的方式都是建立新的實體物件、設定其值，然後針對 **table_batch_operation** 物件呼叫 insert 方法，以便將實體與新的插入操作建立關聯。</span><span class="sxs-lookup"><span data-stu-id="71cdb-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="71cdb-154">接著會呼叫 **cloud_table.execute** 來執行操作。</span><span class="sxs-lookup"><span data-stu-id="71cdb-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="71cdb-155">以下是批次操作的一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="71cdb-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="71cdb-156">您可以在單一批次中最多執行 100 個插入、刪除、合併、取代、插入或合併，以及插入或取代操作的任意組合。</span><span class="sxs-lookup"><span data-stu-id="71cdb-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="71cdb-157">當擷取操作是批次中的唯一操作時，批次操作可以包含擷取操作。</span><span class="sxs-lookup"><span data-stu-id="71cdb-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="71cdb-158">單一批次操作中的所有實體必須具有相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="71cdb-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="71cdb-159">一個批次操作的資料裝載限制為 4MB。</span><span class="sxs-lookup"><span data-stu-id="71cdb-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="71cdb-160">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="71cdb-161">若要向資料表查詢資料分割中的所有實體，請使用 **table_query** 物件。</span><span class="sxs-lookup"><span data-stu-id="71cdb-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="71cdb-162">下列程式碼範例會指定篩選器來篩選出資料分割索引鍵為 'Smith' 的實體。</span><span class="sxs-lookup"><span data-stu-id="71cdb-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="71cdb-163">此範例會將查詢結果中每個實體的欄位列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="71cdb-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="71cdb-164">此範例中的查詢會顯示符合篩選準則的所有實體。</span><span class="sxs-lookup"><span data-stu-id="71cdb-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="71cdb-165">如果您有大型資料表，而必需要經常下載資料表實體，建議您將資料改為儲存在 Azure 儲存體 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="71cdb-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="71cdb-166">擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="71cdb-167">如果您不想要查詢資料分割中的所有實體，可結合資料分割索引鍵篩選器與資料列索引鍵篩選器來指定範圍。</span><span class="sxs-lookup"><span data-stu-id="71cdb-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="71cdb-168">下列程式碼範例會使用兩個篩選器來取得資料分割 'Smith' 中，資料列索引鍵 (名字) 是以字母 'E' 前之字母為開頭的所有實體，然後會列印查詢結果。</span><span class="sxs-lookup"><span data-stu-id="71cdb-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="71cdb-169">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-169">Retrieve a single entity</span></span>
<span data-ttu-id="71cdb-170">您可以撰寫查詢來擷取單一特定實體。</span><span class="sxs-lookup"><span data-stu-id="71cdb-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="71cdb-171">下列程式碼使用 **table_operation::retrive_entity** 指定客戶 'Jeff Smith'。</span><span class="sxs-lookup"><span data-stu-id="71cdb-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="71cdb-172">此方法只會傳回一個實體而非一個集合，且傳回的值位於 **table_result** 中。</span><span class="sxs-lookup"><span data-stu-id="71cdb-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="71cdb-173">若要從資料表服務中擷取單一實體，最快的方法是在查詢中同時指定資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="71cdb-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="71cdb-174">取代實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-174">Replace an entity</span></span>
<span data-ttu-id="71cdb-175">若要更新實體，請從資料表服務擷取該實體、修改實體物件，然後將變更儲存回資料表服務。</span><span class="sxs-lookup"><span data-stu-id="71cdb-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="71cdb-176">下列程式碼會變更現有客戶的電話號碼和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="71cdb-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="71cdb-177">此程式碼會使用 **table_operation:: replace_entity**，而不是呼叫 **table_operation:: insert_entity**。</span><span class="sxs-lookup"><span data-stu-id="71cdb-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="71cdb-178">如此會完全取代伺服器上的實體，但如果伺服器上的實體自擷取後產生變化，操作就會失敗。</span><span class="sxs-lookup"><span data-stu-id="71cdb-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="71cdb-179">如此會造成失敗，是為了防止應用程式意外覆寫該應用程式的其他元件在擷取後到更新前的這段期間所做的變更。</span><span class="sxs-lookup"><span data-stu-id="71cdb-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="71cdb-180">正確處理此失敗的方式為重新擷取實體、進行變更 (如果仍然有效)，然後再執行一次 **table_operation::replace_entity** 操作。</span><span class="sxs-lookup"><span data-stu-id="71cdb-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="71cdb-181">下一節將示範如何覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="71cdb-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="71cdb-182">插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="71cdb-183">如果從伺服器擷取的實體自擷取後發生變化，**table_operation::replace_entity** 操作將失敗。</span><span class="sxs-lookup"><span data-stu-id="71cdb-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="71cdb-184">此外，您必須先從伺服器擷取實體，**table_operation::replace_entity** 才會成功。</span><span class="sxs-lookup"><span data-stu-id="71cdb-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="71cdb-185">但有時候，您可能不知道實體是否存在伺服器上，而實體中目前儲存的值並不重要，此時您的更新就應該加以完全覆寫。</span><span class="sxs-lookup"><span data-stu-id="71cdb-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="71cdb-186">若要達成此目的，您要使用 **table_operation::insert_or_replace_entity** 操作。</span><span class="sxs-lookup"><span data-stu-id="71cdb-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="71cdb-187">此操作會插入實體 (如果其目前並不存在) 或取代實體 (如果其已存在)，不論上次是何時更新。</span><span class="sxs-lookup"><span data-stu-id="71cdb-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="71cdb-188">在下列程式碼範例中，仍會擷取 Jeff Smith 的客戶實體，但接著會透過 **table_operation::insert_or_replace_entity** 將它儲存回伺服器。</span><span class="sxs-lookup"><span data-stu-id="71cdb-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="71cdb-189">在擷取後到更新前的這段期間對實體所做的任何更新，都會遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="71cdb-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="71cdb-190">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="71cdb-190">Query a subset of entity properties</span></span>
<span data-ttu-id="71cdb-191">一項資料表查詢可以只擷取實體的少數屬性。</span><span class="sxs-lookup"><span data-stu-id="71cdb-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="71cdb-192">下列程式碼中的查詢會使用 **table_query::set_select_columns** 方法，只傳回資料表中實體的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="71cdb-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="71cdb-193">從實體查詢一些屬性比擷取所有屬性更有效率。</span><span class="sxs-lookup"><span data-stu-id="71cdb-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="71cdb-194">刪除實體</span><span class="sxs-lookup"><span data-stu-id="71cdb-194">Delete an entity</span></span>
<span data-ttu-id="71cdb-195">擷取實體之後，可以輕鬆地將它刪除。</span><span class="sxs-lookup"><span data-stu-id="71cdb-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="71cdb-196">擷取實體之後，請以要刪除的實體呼叫 **table_operation::delete_entity**。</span><span class="sxs-lookup"><span data-stu-id="71cdb-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="71cdb-197">接著，呼叫 **cloud_table.execute** 方法。</span><span class="sxs-lookup"><span data-stu-id="71cdb-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="71cdb-198">下列程式碼會擷取並刪除資料分割索引鍵為 "Smith" 且資料列索引鍵為 "Jeff" 的實體。</span><span class="sxs-lookup"><span data-stu-id="71cdb-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="71cdb-199">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="71cdb-199">Delete a table</span></span>
<span data-ttu-id="71cdb-200">最後，下列程式碼範例會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="71cdb-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="71cdb-201">已刪除的資料表在刪除後一段時間內，將無法重新建立。</span><span class="sxs-lookup"><span data-stu-id="71cdb-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="71cdb-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71cdb-202">Next steps</span></span>
<span data-ttu-id="71cdb-203">了解資料表儲存體的基礎概念之後，請依照下列連結深入了解 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="71cdb-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="71cdb-204">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="71cdb-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="71cdb-205">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="71cdb-205">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="71cdb-206">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="71cdb-206">How to use Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="71cdb-207">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="71cdb-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="71cdb-208">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="71cdb-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="71cdb-209">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="71cdb-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
