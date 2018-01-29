---
title: "如何搭配 C++ 使用 Azure 資料表儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/03/2017
ms.author: mimig
ms.openlocfilehash: a71098583af8722f2e191e0e665ac87ebd30f355
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="how-to-use-azure-table-storage-with-c"></a>如何搭配 C++ 使用 Azure 資料表儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>概觀
本指南將示範如何使用 Azure 資料表儲存體服務執行一般案例。 這些範例均以 C++ 撰寫，並使用 [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)。 所涵蓋的案例包括**建立和刪除資料表**，以及**使用資料表實體**。

> [!NOTE]
> 本指南以 Azure Storage Client Library for C++ 1.0.0 版和更新版本為對象。 建議的版本是 Storage Client Library 2.2.0，可透過 [NuGet](http://www.nuget.org/packages/wastorage) 或 [GitHub](https://github.com/Azure/azure-storage-cpp/) 取得。
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>建立 C++ 應用程式
在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。 若要這樣做，您需要安裝 Azure Storage Client Library for C++，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。  

若要安裝 Azure Storage Client Library for C++，您可以使用下列方法：

* **Linux：** 遵循 [Azure Storage Client Library for C++ 讀我檔案](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 頁面中提供的指示進行。  
* **Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。 在 [NuGet 套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 中輸入下列命令，然後按下 Enter。  
  
     Install-Package wastorage

## <a name="configure-your-application-to-access-table-storage"></a>設定您的應用程式來存取資料表儲存體
在您要使用 Azure 儲存體 API 來存取資料表的 C++ 檔案頂端，加入下列 include 陳述式：  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。 執行用戶端應用程式時，您必須提供下列格式的儲存體連接字串。 使用您的儲存體帳戶名稱和儲存體存取金鑰，來輸入 [Azure 入口網站](https://portal.azure.com)中所列的儲存體帳戶的 AccountName 和 AccountKey 值。 如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 本範例將示範如何宣告靜態欄位來存放連接字串：  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

若要在本機 Windows 電腦中測試您的應用程式，可以使用隨 [Azure SDK](https://azure.microsoft.com/downloads/) 一起安裝的 Azure [儲存體模擬器](../storage/common/storage-use-emulator.md)。 儲存體模擬器是一個公用程式，可模擬本機開發電腦上的 Azure Blob、佇列和表格服務。 下列範例示範如何宣告靜態欄位以便將連接字串存放到本機儲存體模擬器中：  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

若要啟動 Azure 儲存體模擬器，請按一下 [開始] 按鈕或按下 [Windows] 鍵。 開始輸入 **Azure 儲存體模擬器**，然後從應用程式清單選取 [Microsoft Azure 儲存體模擬器]。  

下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。  

## <a name="retrieve-your-connection-string"></a>擷取連接字串
您可以使用 **cloud_storage_account** 類別來代表儲存體帳戶資訊。 若要從儲存體連接字串擷取儲存體帳戶資訊，您可以使用 parse 方法。

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

接著，取得 **cloud_table_client** 類別的參考，因為這可讓您取得資料表儲存體服務內儲存的資料表和實體的參考物件。 下列程式碼會使用我們在前面擷取的儲存體帳戶物件建立 **cloud_table_client** 物件：  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>建立資料表
**cloud_table_client** 物件可讓您取得資料表和實體的參考物件。 下列程式碼會建立 **cloud_table_client** 物件，並使用該物件建立新資料表。

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

## <a name="add-an-entity-to-a-table"></a>將實體新增至資料表
若要將實體新增至資料表，請建立一個新的 **table_entity** 物件，然後將該物件傳遞至 **table_operation::insert_entity**。 下列程式碼會使用客戶名字做為資料列索引鍵，並使用姓氏做為資料分割索引鍵。 實體的資料分割索引鍵和資料列索引鍵共同唯一識別資料表中的實體。 相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快，但使用不同的資料分割索引鍵可獲得更大的平行操作延展性。 如需詳細資訊，請參閱 [Microsoft Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。

下列程式碼會建立 **table_entity** 的新執行個體，其中含有一些要儲存的客戶資料。 程式碼接著會呼叫 **table_operation::insert_entity** 來建立 **table_operation** 物件，以便將實體插入資料表中，並將新的資料表與該物件建立關聯。 最後，程式碼會針對 **cloud_table** 物件呼叫 execute 方法。 此外，新的 **table_operation** 會傳送一個要求到資料表服務，以便將新的客戶實體插入到 "people" 資料表。  

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

## <a name="insert-a-batch-of-entities"></a>插入實體批次
您可以在單一寫入操作中，插入實體批次至資料表服務。 下列程式碼會建立一個 **table_batch_operation** 物件，然後在其中新增三個插入操作。 加入每個插入操作的方式都是建立新的實體物件、設定其值，然後針對 **table_batch_operation** 物件呼叫 insert 方法，以便將實體與新的插入操作建立關聯。 接著會呼叫 **cloud_table.execute** 來執行操作。  

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

以下是批次操作的一些注意事項：  

* 您可以在單一批次中最多執行 100 個插入、刪除、合併、取代、插入或合併，以及插入或取代操作的任意組合。  
* 當擷取操作是批次中的唯一操作時，批次操作可以包含擷取操作。  
* 單一批次作業中的所有實體必須具有相同的資料分割索引鍵。  
* 一個批次操作的資料裝載限制為 4MB。  

## <a name="retrieve-all-entities-in-a-partition"></a>擷取資料分割中的所有實體
若要向資料表查詢資料分割中的所有實體，請使用 **table_query** 物件。 下列程式碼範例會指定篩選器來篩選出資料分割索引鍵為 'Smith' 的實體。 此範例會將查詢結果中每個實體的欄位列印至主控台。  

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

此範例中的查詢會顯示符合篩選準則的所有實體。 如果您有大型資料表，而必需要經常下載資料表實體，建議您將資料改為儲存在 Azure 儲存體 Blob 中。

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>擷取資料分割中某個範圍的實體
如果您不想要查詢資料分割中的所有實體，可結合資料分割索引鍵篩選器與資料列索引鍵篩選器來指定範圍。 下列程式碼範例會使用兩個篩選器來取得資料分割 'Smith' 中，資料列索引鍵 (名字) 是以字母 'E' 前之字母為開頭的所有實體，然後會列印查詢結果。  

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

## <a name="retrieve-a-single-entity"></a>擷取單一實體
您可以撰寫查詢來擷取單一特定實體。 下列程式碼使用 **table_operation::retrive_entity** 指定客戶 'Jeff Smith'。 此方法只會傳回一個實體而非一個集合，且傳回的值位於 **table_result** 中。 若要從資料表服務中擷取單一實體，最快的方法是在查詢中同時指定資料分割索引鍵和資料列索引鍵。  

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

## <a name="replace-an-entity"></a>取代實體
若要更新實體，請從資料表服務擷取該實體、修改實體物件，然後將變更儲存回資料表服務。 下列程式碼會變更現有客戶的電話號碼和電子郵件地址。 此程式碼會使用 **table_operation:: replace_entity**，而不是呼叫 **table_operation:: insert_entity**。 如此會完全取代伺服器上的實體，但如果伺服器上的實體自擷取後產生變化，操作就會失敗。 如此會造成失敗，是為了防止應用程式意外覆寫該應用程式的其他元件在擷取後到更新前的這段期間所做的變更。 正確處理此失敗的方式為重新擷取實體、進行變更 (如果仍然有效)，然後再執行一次 **table_operation::replace_entity** 操作。 下一節將示範如何覆寫此行為。  

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

## <a name="insert-or-replace-an-entity"></a>插入或取代實體
如果從伺服器擷取的實體自擷取後發生變化，**table_operation::replace_entity** 操作將失敗。 此外，您必須先從伺服器擷取實體，**table_operation::replace_entity** 才會成功。 但有時候，您可能不知道實體是否存在伺服器上，而實體中目前儲存的值並不重要，此時您的更新就應該加以完全覆寫。 若要達成此目的，您要使用 **table_operation::insert_or_replace_entity** 操作。 此作業會插入實體 (如果其目前並不存在) 或取代實體 (如果其已存在)，不論上次是何時更新。 在下列程式碼範例中，仍會擷取 Jeff Smith 的客戶實體，但接著會透過 **table_operation::insert_or_replace_entity** 將它儲存回伺服器。 在擷取後到更新前的這段期間對實體所做的任何更新，都會遭到覆寫。  

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

## <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
一項資料表查詢可以只擷取實體的少數屬性。 下列程式碼中的查詢會使用 **table_query::set_select_columns** 方法，只傳回資料表中實體的電子郵件地址。  

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
> 從實體查詢一些屬性比擷取所有屬性更有效率。
> 
> 

## <a name="delete-an-entity"></a>刪除實體
擷取實體之後，可以輕鬆地將它刪除。 擷取實體之後，請以要刪除的實體呼叫 **table_operation::delete_entity**。 接著，呼叫 **cloud_table.execute** 方法。 下列程式碼會擷取並刪除資料分割索引鍵為 "Smith" 且資料列索引鍵為 "Jeff" 的實體。  

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

## <a name="delete-a-table"></a>刪除資料表
最後，下列程式碼範例會從儲存體帳戶刪除資料表。 已刪除的資料表在刪除後一段時間內，將無法重新建立。  

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

## <a name="next-steps"></a>後續步驟
了解資料表儲存體的基礎概念之後，請依照下列連結深入了解 Azure 儲存體：  

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。
* [如何使用 C++ 的 Blob 儲存體](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [如何使用 C++ 的佇列儲存體](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [以 C++ 列出 Azure 儲存體資源](../storage/common/storage-c-plus-plus-enumeration.md)
* [Storage Client Library for C++ 參考資料](http://azure.github.io/azure-storage-cpp)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)
