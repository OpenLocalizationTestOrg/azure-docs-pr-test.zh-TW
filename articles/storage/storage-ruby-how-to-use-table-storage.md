---
title: "如何使用 Ruby 的 Azure 資料表儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 03f466cb08ed2ccbd2985471d0956af9e66d97f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="13859-103">如何使用 Ruby 的 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="13859-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="13859-104">概觀</span><span class="sxs-lookup"><span data-stu-id="13859-104">Overview</span></span>
<span data-ttu-id="13859-105">本指南說明如何使用 Azure 資料表服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="13859-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="13859-106">這些範例使用 Ruby API 撰寫。</span><span class="sxs-lookup"><span data-stu-id="13859-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="13859-107">所涵蓋的案例包括「建立和刪除資料表」、「在資料表中插入及查詢實體」。</span><span class="sxs-lookup"><span data-stu-id="13859-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="13859-108">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="13859-108">Create a Ruby application</span></span>
<span data-ttu-id="13859-109">如需如何建立 Ruby 應用程式的指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="13859-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="13859-110">設定您的應用程式以存取儲存體</span><span class="sxs-lookup"><span data-stu-id="13859-110">Configure your application to access Storage</span></span>
<span data-ttu-id="13859-111">若要使用 Azure 儲存體，您必須下載並使用 Ruby Azure 套件，其中包含一組便利程式庫，能與儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="13859-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="13859-112">使用 RubyGems 來取得套件</span><span class="sxs-lookup"><span data-stu-id="13859-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="13859-113">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="13859-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="13859-114">在命令視窗中鍵入 **gem install azure** 以安裝 Gem 和相依性。</span><span class="sxs-lookup"><span data-stu-id="13859-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="13859-115">匯入套件</span><span class="sxs-lookup"><span data-stu-id="13859-115">Import the package</span></span>
<span data-ttu-id="13859-116">使用您偏好的文字編輯器，將以下內容新增至您打算使用儲存體的 Ruby 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="13859-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="13859-117">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="13859-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="13859-118">azure 模組會讀取環境變數 **AZURE\_STORAGE\_ACCOUNT** 及**AZURE\_STORAGE\_ACCESS\_KEY**，以取得連接 Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="13859-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="13859-119">如果尚未設定這些環境變數，您必須使用下列程式碼，在使用 **Azure::TableService** 之前指定帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="13859-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="13859-120">若要從 Azure 入口網站中的傳統或 Resource Manager 儲存體帳戶取得這些值：</span><span class="sxs-lookup"><span data-stu-id="13859-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="13859-121">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="13859-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="13859-122">瀏覽到您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="13859-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="13859-123">在右邊的 [設定] 刀鋒視窗中，按一下 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="13859-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="13859-124">[存取金鑰] 刀鋒視窗隨即顯示，您會看到存取金鑰 1 和存取金鑰 2。</span><span class="sxs-lookup"><span data-stu-id="13859-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="13859-125">您可以使用其中一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="13859-125">You can use either of these.</span></span>
5. <span data-ttu-id="13859-126">按一下複製圖示以將金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="13859-126">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="13859-127">若要從 Azure 入口網站的傳統儲存體帳戶取得這些值：</span><span class="sxs-lookup"><span data-stu-id="13859-127">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="13859-128">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="13859-128">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="13859-129">瀏覽到您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="13859-129">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="13859-130">按一下導覽窗格底部的 [管理存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="13859-130">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="13859-131">在快顯對話方塊中，您將會看到儲存體帳戶名稱、主要存取金鑰和次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="13859-131">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="13859-132">如需存取金鑰，您可以使用主要存取金鑰或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="13859-132">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="13859-133">按一下複製圖示以將金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="13859-133">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="13859-134">建立資料表</span><span class="sxs-lookup"><span data-stu-id="13859-134">Create a table</span></span>
<span data-ttu-id="13859-135">**Azure::TableService** 物件可讓您操作資料表及實體。</span><span class="sxs-lookup"><span data-stu-id="13859-135">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="13859-136">若要建立資料表，請使用 **create\_table()** 方法。</span><span class="sxs-lookup"><span data-stu-id="13859-136">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="13859-137">下列範例將建立資料表或列印錯誤訊息 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="13859-137">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="13859-138">將實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="13859-138">Add an entity to a table</span></span>
<span data-ttu-id="13859-139">若要新增實體，請先建立定義實體屬性的雜湊物件。</span><span class="sxs-lookup"><span data-stu-id="13859-139">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="13859-140">請注意，對每個實體都必須指定 **PartitionKey** 及 **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="13859-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="13859-141">這些是實體的唯一識別碼，且其值的查詢速度比其他屬性快上許多。</span><span class="sxs-lookup"><span data-stu-id="13859-141">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="13859-142">Azure 儲存體會使用 **PartitionKey** ，自動將資料表的實體分散在許多儲存體節點上。</span><span class="sxs-lookup"><span data-stu-id="13859-142">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="13859-143">具有相同 **PartitionKey** 的實體會儲存在相同節點上。</span><span class="sxs-lookup"><span data-stu-id="13859-143">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="13859-144">**RowKey** 是實體在其所屬資料分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="13859-144">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="13859-145">更新實體</span><span class="sxs-lookup"><span data-stu-id="13859-145">Update an entity</span></span>
<span data-ttu-id="13859-146">有多種方法可以用來更新現有的實體：</span><span class="sxs-lookup"><span data-stu-id="13859-146">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="13859-147">**update\_entity()：**透過取代現有實體來進行更新。</span><span class="sxs-lookup"><span data-stu-id="13859-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="13859-148">**merge\_entity()：**藉由將新的屬性值合併到現有實體來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="13859-148">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="13859-149">**insert\_or\_merge\_entity()：**藉由取代來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="13859-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="13859-150">如果實體不存在，將會插入新的實體：</span><span class="sxs-lookup"><span data-stu-id="13859-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="13859-151">**insert\_or\_replace\_entity()：**藉由將新的屬性值合併到現有實體來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="13859-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="13859-152">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="13859-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="13859-153">下列範例示範使用 **update\_entity()** 來更新實體：</span><span class="sxs-lookup"><span data-stu-id="13859-153">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="13859-154">使用 **update\_entity()** 及 **merge\_entity()** 時，如果要更新的實體不存在，則更新作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="13859-154">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="13859-155">因此，如果您要儲存一個實體，而不管它是否已存在，您應該改用 **insert\_or\_replace\_entity()** 或 **insert\_or\_merge\_entity()**。</span><span class="sxs-lookup"><span data-stu-id="13859-155">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="13859-156">使用實體群組</span><span class="sxs-lookup"><span data-stu-id="13859-156">Work with groups of entities</span></span>
<span data-ttu-id="13859-157">有時候批次提交多個操作是有意義的，可以確保伺服器會進行不可部分完成的處理。</span><span class="sxs-lookup"><span data-stu-id="13859-157">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="13859-158">若要達到此目的，您首先必須建立 **Batch** 物件，然後在 **TableService** 上使用 **execute\_batch()** 方法。</span><span class="sxs-lookup"><span data-stu-id="13859-158">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="13859-159">下列範例示範在一個批次中，提交具備 RowKey 2 和 3 的兩個實體。</span><span class="sxs-lookup"><span data-stu-id="13859-159">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="13859-160">請注意，它僅適用於具備相同 PartitionKey 的實體。</span><span class="sxs-lookup"><span data-stu-id="13859-160">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="13859-161">查詢實體</span><span class="sxs-lookup"><span data-stu-id="13859-161">Query for an entity</span></span>
<span data-ttu-id="13859-162">若要查詢資料表中的實體，請使用 **get\_entity()** 方法，傳遞資料表名稱、**PartitionKey** 和 **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="13859-162">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="13859-163">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="13859-163">Query a set of entities</span></span>
<span data-ttu-id="13859-164">若要查詢資料表中的實體集合，請建立查詢雜湊物件並使用 **query\_entities()** 方法。</span><span class="sxs-lookup"><span data-stu-id="13859-164">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="13859-165">下列範例示範取得具備相同 **PartitionKey**的所有實體：</span><span class="sxs-lookup"><span data-stu-id="13859-165">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="13859-166">如果單一查詢的結果集太大，以致於無法傳回，則會傳回接續權杖，供您用以擷取後續頁面。</span><span class="sxs-lookup"><span data-stu-id="13859-166">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="13859-167">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="13859-167">Query a subset of entity properties</span></span>
<span data-ttu-id="13859-168">一項資料表查詢可以只擷取實體的少數屬性。</span><span class="sxs-lookup"><span data-stu-id="13859-168">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="13859-169">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="13859-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="13859-170">使用 select 子句並傳遞您要帶到用戶端的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="13859-170">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="13859-171">刪除實體</span><span class="sxs-lookup"><span data-stu-id="13859-171">Delete an entity</span></span>
<span data-ttu-id="13859-172">若要刪除實體，請使用 **delete\_entity()** 方法。</span><span class="sxs-lookup"><span data-stu-id="13859-172">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="13859-173">您必須傳入資料表名稱，其中包含實體、實體的 PartitionKey 和 RowKey。</span><span class="sxs-lookup"><span data-stu-id="13859-173">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="13859-174">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="13859-174">Delete a table</span></span>
<span data-ttu-id="13859-175">若要刪除資料表，請使用 **delete\_table()** 方法並傳入要刪除的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="13859-175">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="13859-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13859-176">Next steps</span></span>

* <span data-ttu-id="13859-177">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="13859-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="13859-178">GitHub 上的 [Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制</span><span class="sxs-lookup"><span data-stu-id="13859-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

