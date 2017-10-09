---
title: "aaaHow toouse 資料表儲存體 （c + +） |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="ac014-103">如何 toouse 從 c + + 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="ac014-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="ac014-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ac014-104">Overview</span></span>
<span data-ttu-id="ac014-105">本指南將說明如何使用 tooperform 常見案例 hello Azure 資料表儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="ac014-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="ac014-106">hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="ac014-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="ac014-107">hello 涵蓋案例包括**建立和刪除資料表**和**處理資料表實體**。</span><span class="sxs-lookup"><span data-stu-id="ac014-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="ac014-108">此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ac014-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="ac014-109">hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp/)。</span><span class="sxs-lookup"><span data-stu-id="ac014-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="ac014-110">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac014-110">Create a C++ application</span></span>
<span data-ttu-id="ac014-111">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="ac014-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="ac014-112">toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac014-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="ac014-113">tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="ac014-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="ac014-114">**Linux:**按照上 hello hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="ac014-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="ac014-115">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="ac014-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="ac014-116">型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按下 Enter。</span><span class="sxs-lookup"><span data-stu-id="ac014-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="ac014-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="ac014-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="ac014-118">設定您的應用程式 tooaccess 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="ac014-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="ac014-119">加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess 資料表 hello c + + 檔案的陳述式 toohello 頂端：</span><span class="sxs-lookup"><span data-stu-id="ac014-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="ac014-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="ac014-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="ac014-121">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="ac014-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="ac014-122">當執行用戶端應用程式，您必須提供 hello 遵循格式中的 hello 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac014-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="ac014-123">使用的儲存體帳戶和 hello 儲存體存取金鑰 hello 儲存體帳戶的 hello 名稱列在 hello [Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="ac014-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="ac014-124">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ac014-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="ac014-125">此範例顯示如何宣告靜態欄位 toohold hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="ac014-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="ac014-126">tootest 您的應用程式在本機 Windows 型電腦，您可以使用 hello Azure[儲存體模擬器](../storage/common/storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="ac014-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ac014-127">hello 儲存體模擬器是模擬 hello Azure Blob、 佇列和表格服務在本機開發電腦上可用的公用程式。</span><span class="sxs-lookup"><span data-stu-id="ac014-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="ac014-128">hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：</span><span class="sxs-lookup"><span data-stu-id="ac014-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="ac014-129">toostart hello Azure 儲存體模擬器，請按一下 hello**啟動**按鈕或按 hello Windows 鍵。</span><span class="sxs-lookup"><span data-stu-id="ac014-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="ac014-130">開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac014-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="ac014-131">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="ac014-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="ac014-132">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="ac014-132">Retrieve your connection string</span></span>
<span data-ttu-id="ac014-133">您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 您儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="ac014-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="ac014-134">tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello parse 方法。</span><span class="sxs-lookup"><span data-stu-id="ac014-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="ac014-135">接下來，取得參考 tooa **cloud_table_client**類別，它可讓您取得的物件參考的資料表，並儲存在 hello 資料表儲存體服務的實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="ac014-136">hello 下列程式碼會建立**cloud_table_client**使用 hello 我們擷取上述的儲存體帳戶物件的物件：</span><span class="sxs-lookup"><span data-stu-id="ac014-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="ac014-137">建立資料表</span><span class="sxs-lookup"><span data-stu-id="ac014-137">Create a table</span></span>
<span data-ttu-id="ac014-138">**cloud_table_client** 物件可讓您取得資料表和實體的參考物件。</span><span class="sxs-lookup"><span data-stu-id="ac014-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="ac014-139">hello 下列程式碼會建立**cloud_table_client**物件，並使用它 toocreate 新的資料表。</span><span class="sxs-lookup"><span data-stu-id="ac014-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="ac014-140">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="ac014-140">Add an entity tooa table</span></span>
<span data-ttu-id="ac014-141">tooadd 實體 tooa 資料表，建立新**table_entity**物件，並將它傳遞到太**table_operation:: insert_entity**。</span><span class="sxs-lookup"><span data-stu-id="ac014-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="ac014-142">hello 下列程式碼會使用 hello 客戶名字當做 hello 資料列索引鍵和最後一個名稱當做 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ac014-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="ac014-143">在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="ac014-144">以 hello 可速度比不同的查詢相同的資料分割索引鍵的實體資料分割索引鍵，但使用不同的資料分割索引鍵可讓平行作業更佳的延展性。</span><span class="sxs-lookup"><span data-stu-id="ac014-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="ac014-145">如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="ac014-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="ac014-146">hello 下列程式碼建立的新執行個體**table_entity**與儲存某些客戶資料 toobe。</span><span class="sxs-lookup"><span data-stu-id="ac014-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="ac014-147">hello 程式碼的下一個呼叫**table_operation:: insert_entity** toocreate **table_operation**物件 tooinsert 實體插入資料表中，並將相關聯 hello 與它的新資料表實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="ac014-148">最後，hello 程式碼會呼叫 hello hello 上執行方法**cloud_table**物件。</span><span class="sxs-lookup"><span data-stu-id="ac014-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="ac014-149">與新的 hello **table_operation**會要求 toohello 資料表服務 tooinsert hello 新客戶的實體將傳送至 hello 「 的人 」 資料表。</span><span class="sxs-lookup"><span data-stu-id="ac014-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="ac014-150">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="ac014-150">Insert a batch of entities</span></span>
<span data-ttu-id="ac014-151">您可以插入實體 toohello 表格服務的批次中一個寫入作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="ac014-152">hello 下列程式碼會建立**table_batch_operation**物件，並將三個 insert 作業 tooit。</span><span class="sxs-lookup"><span data-stu-id="ac014-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="ac014-153">每項插入作業會加入藉由建立新的實體物件，設定其值，而且呼叫 hello 插入上 hello 方法**table_batch_operation**物件 tooassociate hello 實體與新插入作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="ac014-154">然後， **cloud_table.execute**稱為 tooexecute hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="ac014-155">批次作業上一些事情 toonote:</span><span class="sxs-lookup"><span data-stu-id="ac014-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="ac014-156">您可以執行向上 too100 插入、 刪除、 合併、 取代、 插入-或-「 合併 」 和插入或取代作業的單一批次中的任何組合。</span><span class="sxs-lookup"><span data-stu-id="ac014-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="ac014-157">批次作業可以有擷取作業，如果它是 hello hello 批次中的唯一作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="ac014-158">在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ac014-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="ac014-159">批次作業是有限的 tooa 4 MB 的資料承載。</span><span class="sxs-lookup"><span data-stu-id="ac014-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="ac014-160">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="ac014-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="ac014-161">資料表的資料分割，使用中的所有實體 tooquery **table_query**物件。</span><span class="sxs-lookup"><span data-stu-id="ac014-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="ac014-162">hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="ac014-163">這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac014-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="ac014-164">此範例中的 hello 查詢會符合 hello 篩選準則的所有 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="ac014-165">如果您有大型資料表，而且通常需要 toodownload hello 資料表實體，我們建議，您將資料儲存在 Azure 儲存體 blob 中改用。</span><span class="sxs-lookup"><span data-stu-id="ac014-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="ac014-166">擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="ac014-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="ac014-167">如果您不想 tooquery 所有 hello 實體資料分割中的，您可以藉由結合 hello 與資料列索引鍵的篩選資料分割索引鍵篩選指定範圍。</span><span class="sxs-lookup"><span data-stu-id="ac014-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="ac014-168">hello 下列程式碼範例會使用兩個篩選 tooget 所有實體分割區 'Smith' hello 資料列索引鍵 （第一個名稱） 早於 'E' hello 字母中開頭為字母，然後列印 hello 查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="ac014-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="ac014-169">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="ac014-169">Retrieve a single entity</span></span>
<span data-ttu-id="ac014-170">您可以撰寫查詢 tooretrieve 單一的特定實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="ac014-171">hello 下列程式碼使用**table_operation:: retrieve_entity** toospecify hello 客戶 ' Jeff Smith'。</span><span class="sxs-lookup"><span data-stu-id="ac014-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="ac014-172">這個方法會傳回單一實體，而不是集合，且 hello 傳回的值位於**table_result**。</span><span class="sxs-lookup"><span data-stu-id="ac014-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="ac014-173">在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="ac014-174">取代實體</span><span class="sxs-lookup"><span data-stu-id="ac014-174">Replace an entity</span></span>
<span data-ttu-id="ac014-175">tooreplace 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="ac014-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="ac014-176">hello 下列程式碼變更現有的客戶電話號碼和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ac014-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="ac014-177">此程式碼會使用 **table_operation:: replace_entity**，而不是呼叫 **table_operation:: insert_entity**。</span><span class="sxs-lookup"><span data-stu-id="ac014-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="ac014-178">這會導致 hello 實體 toobe 完全取代 hello 在伺服器上，除非變更 hello hello 伺服器上的實體自擷取後，在此情況下 hello 作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ac014-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="ac014-179">此失敗是的 tooprevent hello 擷取和更新您的應用程式的另一個元件之間，進行您的應用程式不慎覆寫變更。</span><span class="sxs-lookup"><span data-stu-id="ac014-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="ac014-180">hello 正確處理失敗的恢復 tooretrieve hello 實體，進行變更 （如果仍然有效），然後再執行另一個**table_operation:: replace_entity**作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="ac014-181">hello 下一節將示範如何 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="ac014-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="ac014-182">插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="ac014-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="ac014-183">**table_operation:: replace_entity** hello 實體已變更，因為它從 hello 伺服器擷取作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="ac014-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="ac014-184">此外，您必須從第一次在順序中的 hello 伺服器擷取 hello 實體**table_operation:: replace_entity** toobe 成功。</span><span class="sxs-lookup"><span data-stu-id="ac014-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="ac014-185">有時候，不過，您不知道是否 hello 實體 hello 伺服器上存在和 hello 目前儲存在它的值無關-您的更新應該覆寫它們全部。</span><span class="sxs-lookup"><span data-stu-id="ac014-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="ac014-186">tooaccomplish，您會使用**table_operation:: insert_or_replace_entity**作業。</span><span class="sxs-lookup"><span data-stu-id="ac014-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="ac014-187">如果它不存在，或予以取代，若是如此，無論 hello 上次更新已進行時，這項作業會插入 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="ac014-188">在下列程式碼範例的 hello，仍會擷取 Jeff Smith 的 hello customer 實體，但它再儲存後 toohello 伺服器透過**table_operation:: insert_or_replace_entity**。</span><span class="sxs-lookup"><span data-stu-id="ac014-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="ac014-189">將覆寫進行 toohello 實體 hello 擷取和更新作業之間的任何更新。</span><span class="sxs-lookup"><span data-stu-id="ac014-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="ac014-190">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="ac014-190">Query a subset of entity properties</span></span>
<span data-ttu-id="ac014-191">查詢 tooa 資料表可從實體擷取少數的屬性。</span><span class="sxs-lookup"><span data-stu-id="ac014-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="ac014-192">hello hello 下列程式碼中的查詢會使用 hello **table_query:: set_select_columns**方法 tooreturn 只有 hello 電子郵件地址 hello 資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> <span data-ttu-id="ac014-193">從實體查詢一些屬性比擷取所有屬性更有效率。</span><span class="sxs-lookup"><span data-stu-id="ac014-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="ac014-194">刪除實體</span><span class="sxs-lookup"><span data-stu-id="ac014-194">Delete an entity</span></span>
<span data-ttu-id="ac014-195">擷取實體之後，可以輕鬆地將它刪除。</span><span class="sxs-lookup"><span data-stu-id="ac014-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="ac014-196">Hello 實體擷取之後，呼叫**table_operation:: delete_entity**與 hello 實體 toodelete。</span><span class="sxs-lookup"><span data-stu-id="ac014-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="ac014-197">然後呼叫 hello **cloud_table.execute**方法。</span><span class="sxs-lookup"><span data-stu-id="ac014-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="ac014-198">hello 下列程式碼會擷取和刪除資料分割索引鍵為"Smith"與"Jeff"的資料列索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="ac014-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="ac014-199">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="ac014-199">Delete a table</span></span>
<span data-ttu-id="ac014-200">最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="ac014-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="ac014-201">已刪除的資料表將無法使用 toobe 重新建立一段時間 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="ac014-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="ac014-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac014-202">Next steps</span></span>
<span data-ttu-id="ac014-203">現在，您學到的資料表儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="ac014-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="ac014-204">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="ac014-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="ac014-205">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ac014-205">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="ac014-206">如何 toouse 佇列儲存體從 c + +</span><span class="sxs-lookup"><span data-stu-id="ac014-206">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="ac014-207">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="ac014-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="ac014-208">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="ac014-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="ac014-209">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="ac014-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
