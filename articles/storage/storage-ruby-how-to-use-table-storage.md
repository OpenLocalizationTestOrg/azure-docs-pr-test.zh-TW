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
# <a name="how-toouse-azure-table-storage-from-ruby"></a>如何 toouse 從 Ruby 的 Azure 資料表儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>概觀
本指南也說明如何使用 tooperform 常見案例 hello Azure 表格服務。 使用 hello Ruby 應用程式開發介面撰寫 hello 範例。 hello 涵蓋案例包括**建立和刪除資料表、 插入和查詢資料表中的實體**。

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>建立 Ruby 應用程式
如需相關指示如何 toocreate 拼音的應用程式，請參閱[拼音滑軌 Web 應用程式在 Azure VM 上](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。

## <a name="configure-your-application-tooaccess-storage"></a>設定您的應用程式 tooaccess 儲存體
toouse Azure 儲存體，您需要 toodownload 和使用 hello Ruby 的 azure 封裝包括一組方便程式庫與 hello 儲存體 REST 服務通訊。

### <a name="use-rubygems-tooobtain-hello-package"></a>使用 RubyGems tooobtain hello 套件
1. 使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。
2. 型別**健身安裝 azure** hello 命令視窗 tooinstall hello 健身和相依性。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用您慣用的文字編輯器，請新增下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_存取\_金鑰**資訊所需 tooconnect tooyour Azure 儲存體帳戶。 如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::TableService**以下列程式碼的 hello:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽您想 toouse toohello 儲存體帳戶。
3. 在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。
4. 在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。 您可以使用其中一個存取金鑰。
5. 按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。

tooobtain hello 傳統 Azure 入口網站中的這些值從傳統儲存體帳戶：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 瀏覽您想 toouse toohello 儲存體帳戶。
3. 按一下**管理存取金鑰**在 hello hello 瀏覽窗格的底部。
4. 在 hello 快顯對話方塊中，您會看到 hello 儲存體帳戶名稱、 主要存取金鑰和次要存取金鑰。 針對存取金鑰，您可以使用 hello 主要或次要的一個 hello。
5. 按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。

## <a name="create-a-table"></a>建立資料表
hello **Azure::TableService**物件可讓您使用資料表和實體。 toocreate 資料表時，使用 hello**建立\_table()**方法。 hello 下列範例會建立資料表，或列印 hello 錯誤，如果有的話。

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
tooadd 實體，會先建立可定義實體屬性的雜湊物件。 請注意，對每個實體都必須指定 **PartitionKey** 及 **RowKey**。 這些是 hello 的實體，唯一識別碼，而且可以進行查詢速度，比其他程式屬性的值。 Azure 儲存體使用**PartitionKey** tooautomatically 散發 hello 資料表實體，在許多儲存節點。 實體與 hello 相同**PartitionKey**儲存在 hello 上相同的節點。 hello **RowKey**是 hello 的 hello 實體所屬的 hello 磁碟分割內的唯一識別碼。

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>更新實體
有多個方法可用 tooupdate 現有的實體：

* **update\_entity()：**透過取代現有實體來進行更新。
* **合併\_entity():**將新的屬性值合併為 hello 現有實體，以更新現有的實體。
* **insert\_or\_merge\_entity()：**藉由取代來更新現有實體。 如果實體不存在，將會插入新的實體：
* **插入\_或\_取代\_entity():**將新的屬性值合併為 hello 現有實體，以更新現有的實體。 如果實體不存在，將會插入新的實體。

hello 下列範例示範如何更新實體使用**更新\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

與**更新\_entity()**和**合併\_entity()**，如果您要更新的 hello 實體不存在 hello 更新作業將會失敗。 因此如果您想 toostore 不論是否已經存在的實體，您應該改用**插入\_或\_取代\_entity()**或**插入\_或\_合併\_entity()**。

## <a name="work-with-groups-of-entities"></a>使用實體群組
有時它可讓意義 toosubmit 多個作業一起批次 tooensure 中不可部分完成 hello 伺服器所處理。 tooaccomplish，您必須先建立**批次**物件，然後使用 hello**執行\_batch()**方法**TableService**。 hello 下列範例示範送出兩個實體 RowKey 2 和 3 批次中。 請注意，它，僅適用於實體與 hello 相同的 PartitionKey。

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>查詢實體
在資料表中，使用 hello 實體 tooquery**取得\_entity()**方法，藉由傳遞 hello 資料表名稱， **PartitionKey**和**RowKey**。

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>查詢實體集合
tooquery 的一組實體，在資料表中，建立查詢雜湊物件，並使用 hello**查詢\_entities()**方法。 hello 下列範例示範如何取得所有 hello 實體以 hello 相同**PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> 如果 hello 結果集是單一查詢 tooreturn 而言太大，接續 token 將會傳回您可以使用 tooretrieve 後續頁面。
>
>

## <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
查詢 tooa 資料表可從實體擷取少數的屬性。 這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。 使用 hello select 子句，以及傳遞 hello 名稱 hello 您想要 toobring toohello 用戶端上的屬性。

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>刪除實體
toodelete 實體，使用 hello**刪除\_entity()**方法。 您需要 toopass hello hello 資料表，其中包含 hello 實體、 hello PartitionKey 和 RowKey hello 實體的名稱。

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>刪除資料表
toodelete 資料表時，使用 hello**刪除\_table()**方法並傳入的 hello 名稱 hello 想 toodelete 資料表。

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>後續步驟

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* GitHub 上的 [Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制

