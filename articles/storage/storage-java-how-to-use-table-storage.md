---
title: "aaaHow toouse 資料表儲存體從 Java |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>如何從 Java 資料表儲存體 toouse
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>概觀
本指南將說明如何使用 tooperform 常見案例 hello Azure 資料表儲存體服務。 hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。 hello 涵蓋案例包括**建立**，**列出**，和**刪除**資料表，以及**插入**， **查詢**，**修改**，和**刪除**資料表中的實體。 如需有關資料表的詳細資訊，請參閱 hello[後續步驟](#Next-Steps)> 一節。

注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。 如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>建立 Java 應用程式
在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。

toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。 一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。 如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。 當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。

## <a name="configure-your-application-tooaccess-table-storage"></a>設定您的應用程式 tooaccess 資料表儲存體
新增下列匯入陳述式 toohello 想 toouse Microsoft Azure 儲存體 Api tooaccess 資料表 hello Java 檔案頂端的 hello:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 此範例顯示如何宣告靜態欄位 toohold hello 連接字串：

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。 以下是取得 hello 連接字串的範例**設定**名*StorageConnectionString* hello 服務組態檔中：

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。

## <a name="how-to-create-a-table"></a>作法：建立資料表
**CloudTableClient** 物件可讓您取得資料表和實體的參照物件。 hello 下列程式碼會建立**CloudTableClient**物件，並使用該新 toocreate **CloudTable**物件表示資料表名為 「 人員 」。 (注意： 有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考].)

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a>如何： 列出 hello 資料表
一份資料表，呼叫 hello tooget **CloudTableClient.listTables()**方法 tooretrieve 可反覆執行的資料表名稱清單。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a>如何： 將實體 tooa 資料表
實體對應 tooJava 物件正在使用自訂類別，實作**TableEntity**。 為了方便起見，hello **TableServiceEntity**類別會實作**TableEntity**和名為 toogetter 和 setter 方法會使用反映 toomap 屬性 hello 屬性。 tooadd 實體 tooa 表，先建立一個類別來定義實體的 hello 屬性。 hello 下列程式碼會定義使用 hello 資料列索引鍵，以及姓氏的 hello 客戶名字為 hello 資料分割索引鍵的實體類別。 在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。 Hello 速度比不同資料分割索引鍵的可查詢相同的資料分割索引鍵的實體。

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

涉及實體的資料表操作需要 **TableOperation** 物件。 此物件會定義可以使用執行的實體上執行的 hello 作業 toobe **CloudTable**物件。 hello 下列程式碼建立的新執行個體 hello **CustomerEntity**儲存某些客戶資料 toobe 類別。 hello 程式碼的下一個呼叫**TableOperation.insertOrReplace** toocreate **TableOperation**物件 tooinsert 實體插入資料表中，並將新 hello **CustomerEntity**與它。 最後，hello 程式碼會呼叫 hello**執行**方法上 hello **CloudTable**物件，指定 hello 「 的人 」 資料表和新的 hello **TableOperation**，哪些然後傳送要求 toohello 儲存體服務 tooinsert hello 新客戶的實體插入 hello 「 的人 」 資料表，或取代 hello 實體，如果已經存在。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a>作法：插入實體批次
您可以插入實體 toohello 表格服務的批次中一個寫入作業。 hello 下列程式碼會建立**TableBatchOperation**物件，然後將三個 insert 作業 tooit。 每項插入作業由建立新的實體物件、 設定其值，然後再呼叫 hello 新增**插入**方法上 hello **TableBatchOperation** tooassociate hello 實體與新的物件插入作業。 然後 hello 程式碼會呼叫**執行**上 hello **CloudTable**物件，指定 hello 「 的人 」 資料表和 hello **TableBatchOperation**物件，它會傳送 hello 批次的資料表作業 toohello 單一要求中的儲存體服務。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

批次作業上一些事情 toonote:

* 您可以執行向上 too100 insert、 delete、 merge、 取代、 insert 或 merge 和插入或取代作業的單一批次中的任何組合。
* 批次作業可以有擷取作業，如果它是 hello hello 批次中的唯一作業。
* 在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。
* 批次作業是有限的 tooa 4 MB 的資料內容。

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>作法：擷取資料分割中的所有實體
tooquery 實體資料分割中的資料表，您可以使用**TableQuery**。 呼叫**TableQuery.from** toocreate 傳回指定之結果型別特定資料表上的查詢。 hello 下列程式碼指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。 **TableQuery.generateFilterCondition** toocreate 查詢篩選器是 helper 方法。 呼叫**其中**hello 所傳回的 hello 參考上**TableQuery.from**方法 tooapply hello 篩選 toohello 查詢。 Hello 查詢執行時呼叫太**執行**上 hello **CloudTable**物件，它會傳回**迭代器**以 hello **CustomerEntity**結果所指定的類型。 然後，您可以使用 hello**迭代器**中傳回的每個迴圈 tooconsume hello 結果。 此程式碼會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>作法：擷取資料分割中某個範圍的實體
如果您不想 tooquery 所有 hello 實體資料分割中的，您可以指定一個範圍篩選器中使用比較運算子。 hello 下列兩個篩選 tooget"Smith"的磁碟分割中的所有實體 hello 資料列索引鍵 （第一個名稱） 以向上 too'E 字母的開始位置的程式碼會結合 ' hello 字母順序中。 然後它會顯示 hello 查詢結果。 如果您使用 hello 批次中的 hello 實體加入的 toohello 資料表插入本指南的區段，會傳回此時間 （Ben 和韓旻 Smith）; 只有兩個實體Jeff Smith 就不會包含。

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a>作法：擷取單一實體
您可以撰寫查詢 tooretrieve 單一的特定實體。 hello 下列程式碼呼叫**TableOperation.retrieve**與資料分割索引鍵和資料列索引鍵參數 toospecify hello 客戶"Jeff Smith"，而不是建立**TableQuery**和使用篩選器 toodo hello相同的動作。 在執行時，hello 擷取作業傳回單一實體，而不是集合。 hello **getResultAsType**方法將 hello 結果 toohello hello 分派目標類型， **CustomerEntity**物件。 如果此類型不相容於 hello hello 查詢指定的型別，就會擲回例外狀況。 如果沒有實體具有完全相符的資料分割和資料列索引鍵，則會傳回 Null 值。 在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a>作法：修改實體
toomodify 實體，擷取與 hello 表格服務、 變更 toohello 實體物件，變更並儲存 hello 後 toohello 表格服務與取代或合併作業。 hello 下列程式碼變更現有的客戶電話號碼。 而不是呼叫**TableOperation.insert**像我們 tooinsert，此程式碼會呼叫**TableOperation.replace**。 hello **CloudTable.execute**方法會呼叫 hello 表格服務，而且要更換 hello 實體，除非另一個應用程式變更它的 hello 時間因為此應用程式擷取它。 當發生這種情況時，會擲回例外狀況，並 hello 實體必須擷取、 修改和儲存一次。 這種開放式並行存取重試模式在分散式儲存體系統中相當常見。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a>作法：查詢實體屬性的子集
查詢 tooa 資料表可從實體擷取少數的屬性。 這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。 hello hello 下列程式碼中的查詢會使用 hello**選取**方法 tooreturn 只有 hello 電子郵件地址 hello 資料表中的實體。 hello 結果會投影成集合**字串**hello 協助**EntityResolver**，其中沒有 hello hello hello 伺服器傳回的實體上的型別轉換。 您可以在 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解投影。 請注意，投影上不支援 hello 本機儲存體模擬器，以便在 hello 表格服務上使用的帳戶時，才執行此程式碼。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a>作法：插入或取代實體
通常您會希望 tooadd 實體 tooa 表而不需要知道如果 hello 資料表中已經存在。 插入或取代作業可讓您 toomake 單一要求將會插入 hello 實體，如果它不存在，或取代現有一，如果是這樣的 hello。 在先前的範例上建置，hello 下列程式碼插入或取代"Walter 絃樂豎琴"hello 實體。 之後建立新的實體，此程式碼呼叫 hello **TableOperation.insertOrReplace**方法。 此程式碼接著呼叫**執行**上 hello **CloudTable**物件 hello 資料表和 hello 插入或取代做為 hello 參數的資料表作業。 只有部分的實體，tooupdate hello **TableOperation.insertOrMerge**改為使用方法。 請注意讓 hello 表格服務上使用的帳戶時，才執行此程式碼，hello 本機儲存體模擬器，在不支援該插入-或-取代。 您可以在這個 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解插入或取代和插入或合併。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a>作法：刪除實體
擷取實體之後，可以輕鬆地將它刪除。 Hello 實體擷取之後，呼叫**TableOperation.delete**與 hello 實體 toodelete。 然後呼叫**執行**上 hello **CloudTable**物件。 下列程式碼的 hello 擷取，並刪除一個 customer 實體。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a>作法：刪除資料表
最後，hello 下列程式碼會刪除資料表從儲存體帳戶。 已刪除的資料表將無法使用 toobe 一段時間通常少於 40 秒 hello 刪除重新建立。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a>後續步驟

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* [Azure Storage SDK for Java][Azure Storage SDK for Java]
* [Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]
* [Azure 儲存體 REST API][Azure Storage REST API]
* [Azure 儲存體團隊部落格][Azure Storage Team Blog]

如需詳細資訊，請參閱 hello [Java 開發人員中心](/develop/java/)。

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
