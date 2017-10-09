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
# <a name="how-toouse-table-storage-from-c"></a>如何 toouse 從 c + + 的資料表儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>概觀
本指南將說明如何使用 tooperform 常見案例 hello Azure 資料表儲存體服務。 hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)。 hello 涵蓋案例包括**建立和刪除資料表**和**處理資料表實體**。

> [!NOTE]
> 此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。 hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp/)。
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>建立 C++ 應用程式
在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。 toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。  

tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:

* **Linux:**按照上 hello hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。  
* **Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。 型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按下 Enter。  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>設定您的應用程式 tooaccess 資料表儲存體
加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess 資料表 hello c + + 檔案的陳述式 toohello 頂端：  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 當執行用戶端應用程式，您必須提供 hello 遵循格式中的 hello 儲存體連接字串。 使用的儲存體帳戶和 hello 儲存體存取金鑰 hello 儲存體帳戶的 hello 名稱列在 hello [Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 此範例顯示如何宣告靜態欄位 toohold hello 連接字串：  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 您的應用程式在本機 Windows 型電腦，您可以使用 hello Azure[儲存體模擬器](../storage/common/storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。 hello 儲存體模擬器是模擬 hello Azure Blob、 佇列和表格服務在本機開發電腦上可用的公用程式。 hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 儲存體模擬器，請按一下 hello**啟動**按鈕或按 hello Windows 鍵。 開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。  

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。  

## <a name="retrieve-your-connection-string"></a>擷取連接字串
您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 您儲存體帳戶資訊。 tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello parse 方法。

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

接下來，取得參考 tooa **cloud_table_client**類別，它可讓您取得的物件參考的資料表，並儲存在 hello 資料表儲存體服務的實體。 hello 下列程式碼會建立**cloud_table_client**使用 hello 我們擷取上述的儲存體帳戶物件的物件：  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>建立資料表
**cloud_table_client** 物件可讓您取得資料表和實體的參考物件。 hello 下列程式碼會建立**cloud_table_client**物件，並使用它 toocreate 新的資料表。

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

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
tooadd 實體 tooa 資料表，建立新**table_entity**物件，並將它傳遞到太**table_operation:: insert_entity**。 hello 下列程式碼會使用 hello 客戶名字當做 hello 資料列索引鍵和最後一個名稱當做 hello 資料分割索引鍵。 在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。 以 hello 可速度比不同的查詢相同的資料分割索引鍵的實體資料分割索引鍵，但使用不同的資料分割索引鍵可讓平行作業更佳的延展性。 如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。

hello 下列程式碼建立的新執行個體**table_entity**與儲存某些客戶資料 toobe。 hello 程式碼的下一個呼叫**table_operation:: insert_entity** toocreate **table_operation**物件 tooinsert 實體插入資料表中，並將相關聯 hello 與它的新資料表實體。 最後，hello 程式碼會呼叫 hello hello 上執行方法**cloud_table**物件。 與新的 hello **table_operation**會要求 toohello 資料表服務 tooinsert hello 新客戶的實體將傳送至 hello 「 的人 」 資料表。  

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

## <a name="insert-a-batch-of-entities"></a>插入實體批次
您可以插入實體 toohello 表格服務的批次中一個寫入作業。 hello 下列程式碼會建立**table_batch_operation**物件，並將三個 insert 作業 tooit。 每項插入作業會加入藉由建立新的實體物件，設定其值，而且呼叫 hello 插入上 hello 方法**table_batch_operation**物件 tooassociate hello 實體與新插入作業。 然後， **cloud_table.execute**稱為 tooexecute hello 作業。  

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

批次作業上一些事情 toonote:  

* 您可以執行向上 too100 插入、 刪除、 合併、 取代、 插入-或-「 合併 」 和插入或取代作業的單一批次中的任何組合。  
* 批次作業可以有擷取作業，如果它是 hello hello 批次中的唯一作業。  
* 在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。  
* 批次作業是有限的 tooa 4 MB 的資料承載。  

## <a name="retrieve-all-entities-in-a-partition"></a>擷取資料分割中的所有實體
資料表的資料分割，使用中的所有實體 tooquery **table_query**物件。 hello 下列程式碼範例指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。 這個範例會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。  

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

此範例中的 hello 查詢會符合 hello 篩選準則的所有 hello 實體。 如果您有大型資料表，而且通常需要 toodownload hello 資料表實體，我們建議，您將資料儲存在 Azure 儲存體 blob 中改用。

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>擷取資料分割中某個範圍的實體
如果您不想 tooquery 所有 hello 實體資料分割中的，您可以藉由結合 hello 與資料列索引鍵的篩選資料分割索引鍵篩選指定範圍。 hello 下列程式碼範例會使用兩個篩選 tooget 所有實體分割區 'Smith' hello 資料列索引鍵 （第一個名稱） 早於 'E' hello 字母中開頭為字母，然後列印 hello 查詢結果中。  

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

## <a name="retrieve-a-single-entity"></a>擷取單一實體
您可以撰寫查詢 tooretrieve 單一的特定實體。 hello 下列程式碼使用**table_operation:: retrieve_entity** toospecify hello 客戶 ' Jeff Smith'。 這個方法會傳回單一實體，而不是集合，且 hello 傳回的值位於**table_result**。 在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。  

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

## <a name="replace-an-entity"></a>取代實體
tooreplace 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。 hello 下列程式碼變更現有的客戶電話號碼和電子郵件地址。 此程式碼會使用 **table_operation:: replace_entity**，而不是呼叫 **table_operation:: insert_entity**。 這會導致 hello 實體 toobe 完全取代 hello 在伺服器上，除非變更 hello hello 伺服器上的實體自擷取後，在此情況下 hello 作業將會失敗。 此失敗是的 tooprevent hello 擷取和更新您的應用程式的另一個元件之間，進行您的應用程式不慎覆寫變更。 hello 正確處理失敗的恢復 tooretrieve hello 實體，進行變更 （如果仍然有效），然後再執行另一個**table_operation:: replace_entity**作業。 hello 下一節將示範如何 toooverride 這種行為。  

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

## <a name="insert-or-replace-an-entity"></a>插入或取代實體
**table_operation:: replace_entity** hello 實體已變更，因為它從 hello 伺服器擷取作業會失敗。 此外，您必須從第一次在順序中的 hello 伺服器擷取 hello 實體**table_operation:: replace_entity** toobe 成功。 有時候，不過，您不知道是否 hello 實體 hello 伺服器上存在和 hello 目前儲存在它的值無關-您的更新應該覆寫它們全部。 tooaccomplish，您會使用**table_operation:: insert_or_replace_entity**作業。 如果它不存在，或予以取代，若是如此，無論 hello 上次更新已進行時，這項作業會插入 hello 實體。 在下列程式碼範例的 hello，仍會擷取 Jeff Smith 的 hello customer 實體，但它再儲存後 toohello 伺服器透過**table_operation:: insert_or_replace_entity**。 將覆寫進行 toohello 實體 hello 擷取和更新作業之間的任何更新。  

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

## <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
查詢 tooa 資料表可從實體擷取少數的屬性。 hello hello 下列程式碼中的查詢會使用 hello **table_query:: set_select_columns**方法 tooreturn 只有 hello 電子郵件地址 hello 資料表中的實體。  

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
> 從實體查詢一些屬性比擷取所有屬性更有效率。
> 
> 

## <a name="delete-an-entity"></a>刪除實體
擷取實體之後，可以輕鬆地將它刪除。 Hello 實體擷取之後，呼叫**table_operation:: delete_entity**與 hello 實體 toodelete。 然後呼叫 hello **cloud_table.execute**方法。 hello 下列程式碼會擷取和刪除資料分割索引鍵為"Smith"與"Jeff"的資料列索引鍵的實體。  

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

## <a name="delete-a-table"></a>刪除資料表
最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。 已刪除的資料表將無法使用 toobe 重新建立一段時間 hello 刪除。  

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

## <a name="next-steps"></a>後續步驟
現在，您學到的資料表儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體：  

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* [如何 toouse 從 c + + 的 Blob 儲存體](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [如何 toouse 佇列儲存體從 c + +](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [以 C++ 列出 Azure 儲存體資源](../storage/common/storage-c-plus-plus-enumeration.md)
* [Storage Client Library for C++ 參考資料](http://azure.github.io/azure-storage-cpp)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)
