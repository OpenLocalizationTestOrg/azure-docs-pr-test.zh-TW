---
title: "aaaHow toouse 從 Ruby 的 Azure 資料表儲存體 |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
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
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="6bc47-103">如何 toouse 從 Ruby 的 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="6bc47-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="6bc47-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6bc47-104">Overview</span></span>
<span data-ttu-id="6bc47-105">本指南也說明如何使用 tooperform 常見案例 hello Azure 表格服務。</span><span class="sxs-lookup"><span data-stu-id="6bc47-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="6bc47-106">使用 hello Ruby 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="6bc47-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="6bc47-107">hello 涵蓋案例包括**建立和刪除資料表、 插入和查詢資料表中的實體**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="6bc47-108">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="6bc47-108">Create a Ruby application</span></span>
<span data-ttu-id="6bc47-109">如需相關指示如何 toocreate 拼音的應用程式，請參閱[拼音滑軌 Web 應用程式在 Azure VM 上](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6bc47-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="6bc47-110">設定您的應用程式 tooaccess 儲存體</span><span class="sxs-lookup"><span data-stu-id="6bc47-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="6bc47-111">toouse Azure 儲存體，您需要 toodownload 和使用 hello Ruby 的 azure 封裝包括一組方便程式庫與 hello 儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="6bc47-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="6bc47-112">使用 RubyGems tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="6bc47-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="6bc47-113">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="6bc47-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="6bc47-114">型別**健身安裝 azure** hello 命令視窗 tooinstall hello 健身和相依性。</span><span class="sxs-lookup"><span data-stu-id="6bc47-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="6bc47-115">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="6bc47-115">Import hello package</span></span>
<span data-ttu-id="6bc47-116">使用您慣用的文字編輯器，請新增下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bc47-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="6bc47-117">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="6bc47-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="6bc47-118">hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_存取\_金鑰**資訊所需 tooconnect tooyour Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bc47-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="6bc47-119">如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::TableService**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bc47-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="6bc47-120">tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：</span><span class="sxs-lookup"><span data-stu-id="6bc47-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="6bc47-121">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6bc47-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6bc47-122">瀏覽您想 toouse toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bc47-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="6bc47-123">在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="6bc47-124">在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6bc47-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="6bc47-125">您可以使用其中一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6bc47-125">You can use either of these.</span></span>
5. <span data-ttu-id="6bc47-126">按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="6bc47-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="6bc47-127">tooobtain hello 傳統 Azure 入口網站中的這些值從傳統儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="6bc47-127">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="6bc47-128">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="6bc47-128">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6bc47-129">瀏覽您想 toouse toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bc47-129">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="6bc47-130">按一下**管理存取金鑰**在 hello hello 瀏覽窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="6bc47-130">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="6bc47-131">在 hello 快顯對話方塊中，您會看到 hello 儲存體帳戶名稱、 主要存取金鑰和次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6bc47-131">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="6bc47-132">針對存取金鑰，您可以使用 hello 主要或次要的一個 hello。</span><span class="sxs-lookup"><span data-stu-id="6bc47-132">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="6bc47-133">按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="6bc47-133">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="6bc47-134">建立資料表</span><span class="sxs-lookup"><span data-stu-id="6bc47-134">Create a table</span></span>
<span data-ttu-id="6bc47-135">hello **Azure::TableService**物件可讓您使用資料表和實體。</span><span class="sxs-lookup"><span data-stu-id="6bc47-135">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="6bc47-136">toocreate 資料表時，使用 hello**建立\_table()**方法。</span><span class="sxs-lookup"><span data-stu-id="6bc47-136">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="6bc47-137">hello 下列範例會建立資料表，或列印 hello 錯誤，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="6bc47-137">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="6bc47-138">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="6bc47-138">Add an entity tooa table</span></span>
<span data-ttu-id="6bc47-139">tooadd 實體，會先建立可定義實體屬性的雜湊物件。</span><span class="sxs-lookup"><span data-stu-id="6bc47-139">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="6bc47-140">請注意，對每個實體都必須指定 **PartitionKey** 及 **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="6bc47-141">這些是 hello 的實體，唯一識別碼，而且可以進行查詢速度，比其他程式屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6bc47-141">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="6bc47-142">Azure 儲存體使用**PartitionKey** tooautomatically 散發 hello 資料表實體，在許多儲存節點。</span><span class="sxs-lookup"><span data-stu-id="6bc47-142">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="6bc47-143">實體與 hello 相同**PartitionKey**儲存在 hello 上相同的節點。</span><span class="sxs-lookup"><span data-stu-id="6bc47-143">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="6bc47-144">hello **RowKey**是 hello 的 hello 實體所屬的 hello 磁碟分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="6bc47-144">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="6bc47-145">更新實體</span><span class="sxs-lookup"><span data-stu-id="6bc47-145">Update an entity</span></span>
<span data-ttu-id="6bc47-146">有多個方法可用 tooupdate 現有的實體：</span><span class="sxs-lookup"><span data-stu-id="6bc47-146">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="6bc47-147">**update\_entity()：**透過取代現有實體來進行更新。</span><span class="sxs-lookup"><span data-stu-id="6bc47-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="6bc47-148">**合併\_entity():**將新的屬性值合併為 hello 現有實體，以更新現有的實體。</span><span class="sxs-lookup"><span data-stu-id="6bc47-148">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="6bc47-149">**insert\_or\_merge\_entity()：**藉由取代來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="6bc47-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="6bc47-150">如果實體不存在，將會插入新的實體：</span><span class="sxs-lookup"><span data-stu-id="6bc47-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="6bc47-151">**插入\_或\_取代\_entity():**將新的屬性值合併為 hello 現有實體，以更新現有的實體。</span><span class="sxs-lookup"><span data-stu-id="6bc47-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="6bc47-152">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="6bc47-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="6bc47-153">hello 下列範例示範如何更新實體使用**更新\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="6bc47-153">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="6bc47-154">與**更新\_entity()**和**合併\_entity()**，如果您要更新的 hello 實體不存在 hello 更新作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6bc47-154">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="6bc47-155">因此如果您想 toostore 不論是否已經存在的實體，您應該改用**插入\_或\_取代\_entity()**或**插入\_或\_合併\_entity()**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-155">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="6bc47-156">使用實體群組</span><span class="sxs-lookup"><span data-stu-id="6bc47-156">Work with groups of entities</span></span>
<span data-ttu-id="6bc47-157">有時它可讓意義 toosubmit 多個作業一起批次 tooensure 中不可部分完成 hello 伺服器所處理。</span><span class="sxs-lookup"><span data-stu-id="6bc47-157">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="6bc47-158">tooaccomplish，您必須先建立**批次**物件，然後使用 hello**執行\_batch()**方法**TableService**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-158">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="6bc47-159">hello 下列範例示範送出兩個實體 RowKey 2 和 3 批次中。</span><span class="sxs-lookup"><span data-stu-id="6bc47-159">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="6bc47-160">請注意，它，僅適用於實體與 hello 相同的 PartitionKey。</span><span class="sxs-lookup"><span data-stu-id="6bc47-160">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="6bc47-161">查詢實體</span><span class="sxs-lookup"><span data-stu-id="6bc47-161">Query for an entity</span></span>
<span data-ttu-id="6bc47-162">在資料表中，使用 hello 實體 tooquery**取得\_entity()**方法，藉由傳遞 hello 資料表名稱， **PartitionKey**和**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="6bc47-162">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="6bc47-163">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="6bc47-163">Query a set of entities</span></span>
<span data-ttu-id="6bc47-164">tooquery 的一組實體，在資料表中，建立查詢雜湊物件，並使用 hello**查詢\_entities()**方法。</span><span class="sxs-lookup"><span data-stu-id="6bc47-164">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="6bc47-165">hello 下列範例示範如何取得所有 hello 實體以 hello 相同**PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="6bc47-165">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="6bc47-166">如果 hello 結果集是單一查詢 tooreturn 而言太大，接續 token 將會傳回您可以使用 tooretrieve 後續頁面。</span><span class="sxs-lookup"><span data-stu-id="6bc47-166">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="6bc47-167">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="6bc47-167">Query a subset of entity properties</span></span>
<span data-ttu-id="6bc47-168">查詢 tooa 資料表可從實體擷取少數的屬性。</span><span class="sxs-lookup"><span data-stu-id="6bc47-168">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="6bc47-169">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="6bc47-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="6bc47-170">使用 hello select 子句，以及傳遞 hello 名稱 hello 您想要 toobring toohello 用戶端上的屬性。</span><span class="sxs-lookup"><span data-stu-id="6bc47-170">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="6bc47-171">刪除實體</span><span class="sxs-lookup"><span data-stu-id="6bc47-171">Delete an entity</span></span>
<span data-ttu-id="6bc47-172">toodelete 實體，使用 hello**刪除\_entity()**方法。</span><span class="sxs-lookup"><span data-stu-id="6bc47-172">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="6bc47-173">您需要 toopass hello hello 資料表，其中包含 hello 實體、 hello PartitionKey 和 RowKey hello 實體的名稱。</span><span class="sxs-lookup"><span data-stu-id="6bc47-173">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="6bc47-174">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="6bc47-174">Delete a table</span></span>
<span data-ttu-id="6bc47-175">toodelete 資料表時，使用 hello**刪除\_table()**方法並傳入的 hello 名稱 hello 想 toodelete 資料表。</span><span class="sxs-lookup"><span data-stu-id="6bc47-175">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="6bc47-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bc47-176">Next steps</span></span>

* <span data-ttu-id="6bc47-177">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="6bc47-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="6bc47-178">GitHub 上的 [Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制</span><span class="sxs-lookup"><span data-stu-id="6bc47-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

