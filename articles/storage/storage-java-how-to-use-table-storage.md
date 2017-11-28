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
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="66813-103">如何從 Java 資料表儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="66813-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="66813-104">概觀</span><span class="sxs-lookup"><span data-stu-id="66813-104">Overview</span></span>
<span data-ttu-id="66813-105">本指南將說明如何使用 tooperform 常見案例 hello Azure 資料表儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="66813-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="66813-106">hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="66813-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="66813-107">hello 涵蓋案例包括**建立**，**列出**，和**刪除**資料表，以及**插入**， **查詢**，**修改**，和**刪除**資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="66813-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="66813-108">如需有關資料表的詳細資訊，請參閱 hello[後續步驟](#Next-Steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="66813-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="66813-109">注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="66813-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="66813-110">如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="66813-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="66813-111">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="66813-111">Create a Java application</span></span>
<span data-ttu-id="66813-112">在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。</span><span class="sxs-lookup"><span data-stu-id="66813-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="66813-113">toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="66813-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="66813-114">一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="66813-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="66813-115">如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="66813-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="66813-116">當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66813-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="66813-117">設定您的應用程式 tooaccess 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="66813-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="66813-118">新增下列匯入陳述式 toohello 想 toouse Microsoft Azure 儲存體 Api tooaccess 資料表 hello Java 檔案頂端的 hello:</span><span class="sxs-lookup"><span data-stu-id="66813-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="66813-119">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="66813-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="66813-120">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="66813-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="66813-121">用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="66813-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="66813-122">此範例顯示如何宣告靜態欄位 toohold hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="66813-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="66813-123">在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。</span><span class="sxs-lookup"><span data-stu-id="66813-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="66813-124">以下是取得 hello 連接字串的範例**設定**名*StorageConnectionString* hello 服務組態檔中：</span><span class="sxs-lookup"><span data-stu-id="66813-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="66813-125">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="66813-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="66813-126">作法：建立資料表</span><span class="sxs-lookup"><span data-stu-id="66813-126">How to: Create a table</span></span>
<span data-ttu-id="66813-127">**CloudTableClient** 物件可讓您取得資料表和實體的參照物件。</span><span class="sxs-lookup"><span data-stu-id="66813-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="66813-128">hello 下列程式碼會建立**CloudTableClient**物件，並使用該新 toocreate **CloudTable**物件表示資料表名為 「 人員 」。</span><span class="sxs-lookup"><span data-stu-id="66813-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="66813-129">(注意： 有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考].)</span><span class="sxs-lookup"><span data-stu-id="66813-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

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

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="66813-130">如何： 列出 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="66813-130">How to: List hello tables</span></span>
<span data-ttu-id="66813-131">一份資料表，呼叫 hello tooget **CloudTableClient.listTables()**方法 tooretrieve 可反覆執行的資料表名稱清單。</span><span class="sxs-lookup"><span data-stu-id="66813-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

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

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="66813-132">如何： 將實體 tooa 資料表</span><span class="sxs-lookup"><span data-stu-id="66813-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="66813-133">實體對應 tooJava 物件正在使用自訂類別，實作**TableEntity**。</span><span class="sxs-lookup"><span data-stu-id="66813-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="66813-134">為了方便起見，hello **TableServiceEntity**類別會實作**TableEntity**和名為 toogetter 和 setter 方法會使用反映 toomap 屬性 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="66813-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="66813-135">tooadd 實體 tooa 表，先建立一個類別來定義實體的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="66813-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="66813-136">hello 下列程式碼會定義使用 hello 資料列索引鍵，以及姓氏的 hello 客戶名字為 hello 資料分割索引鍵的實體類別。</span><span class="sxs-lookup"><span data-stu-id="66813-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="66813-137">在一起，實體的資料分割和資料列索引鍵可唯一識別 hello 資料表中的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="66813-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="66813-138">Hello 速度比不同資料分割索引鍵的可查詢相同的資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="66813-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="66813-139">涉及實體的資料表操作需要 **TableOperation** 物件。</span><span class="sxs-lookup"><span data-stu-id="66813-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="66813-140">此物件會定義可以使用執行的實體上執行的 hello 作業 toobe **CloudTable**物件。</span><span class="sxs-lookup"><span data-stu-id="66813-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="66813-141">hello 下列程式碼建立的新執行個體 hello **CustomerEntity**儲存某些客戶資料 toobe 類別。</span><span class="sxs-lookup"><span data-stu-id="66813-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="66813-142">hello 程式碼的下一個呼叫**TableOperation.insertOrReplace** toocreate **TableOperation**物件 tooinsert 實體插入資料表中，並將新 hello **CustomerEntity**與它。</span><span class="sxs-lookup"><span data-stu-id="66813-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="66813-143">最後，hello 程式碼會呼叫 hello**執行**方法上 hello **CloudTable**物件，指定 hello 「 的人 」 資料表和新的 hello **TableOperation**，哪些然後傳送要求 toohello 儲存體服務 tooinsert hello 新客戶的實體插入 hello 「 的人 」 資料表，或取代 hello 實體，如果已經存在。</span><span class="sxs-lookup"><span data-stu-id="66813-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

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

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="66813-144">作法：插入實體批次</span><span class="sxs-lookup"><span data-stu-id="66813-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="66813-145">您可以插入實體 toohello 表格服務的批次中一個寫入作業。</span><span class="sxs-lookup"><span data-stu-id="66813-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="66813-146">hello 下列程式碼會建立**TableBatchOperation**物件，然後將三個 insert 作業 tooit。</span><span class="sxs-lookup"><span data-stu-id="66813-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="66813-147">每項插入作業由建立新的實體物件、 設定其值，然後再呼叫 hello 新增**插入**方法上 hello **TableBatchOperation** tooassociate hello 實體與新的物件插入作業。</span><span class="sxs-lookup"><span data-stu-id="66813-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="66813-148">然後 hello 程式碼會呼叫**執行**上 hello **CloudTable**物件，指定 hello 「 的人 」 資料表和 hello **TableBatchOperation**物件，它會傳送 hello 批次的資料表作業 toohello 單一要求中的儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="66813-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

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

<span data-ttu-id="66813-149">批次作業上一些事情 toonote:</span><span class="sxs-lookup"><span data-stu-id="66813-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="66813-150">您可以執行向上 too100 insert、 delete、 merge、 取代、 insert 或 merge 和插入或取代作業的單一批次中的任何組合。</span><span class="sxs-lookup"><span data-stu-id="66813-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="66813-151">批次作業可以有擷取作業，如果它是 hello hello 批次中的唯一作業。</span><span class="sxs-lookup"><span data-stu-id="66813-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="66813-152">在單一批次作業中的所有實體必須都有 hello 相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="66813-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="66813-153">批次作業是有限的 tooa 4 MB 的資料內容。</span><span class="sxs-lookup"><span data-stu-id="66813-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="66813-154">作法：擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="66813-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="66813-155">tooquery 實體資料分割中的資料表，您可以使用**TableQuery**。</span><span class="sxs-lookup"><span data-stu-id="66813-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="66813-156">呼叫**TableQuery.from** toocreate 傳回指定之結果型別特定資料表上的查詢。</span><span class="sxs-lookup"><span data-stu-id="66813-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="66813-157">hello 下列程式碼指定篩選，其中 'smith ' 距離是 hello 資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="66813-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="66813-158">**TableQuery.generateFilterCondition** toocreate 查詢篩選器是 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="66813-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="66813-159">呼叫**其中**hello 所傳回的 hello 參考上**TableQuery.from**方法 tooapply hello 篩選 toohello 查詢。</span><span class="sxs-lookup"><span data-stu-id="66813-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="66813-160">Hello 查詢執行時呼叫太**執行**上 hello **CloudTable**物件，它會傳回**迭代器**以 hello **CustomerEntity**結果所指定的類型。</span><span class="sxs-lookup"><span data-stu-id="66813-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="66813-161">然後，您可以使用 hello**迭代器**中傳回的每個迴圈 tooconsume hello 結果。</span><span class="sxs-lookup"><span data-stu-id="66813-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="66813-162">此程式碼會列印 hello hello 查詢結果 toohello 主控台中的每個實體的欄位。</span><span class="sxs-lookup"><span data-stu-id="66813-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="66813-163">作法：擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="66813-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="66813-164">如果您不想 tooquery 所有 hello 實體資料分割中的，您可以指定一個範圍篩選器中使用比較運算子。</span><span class="sxs-lookup"><span data-stu-id="66813-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="66813-165">hello 下列兩個篩選 tooget"Smith"的磁碟分割中的所有實體 hello 資料列索引鍵 （第一個名稱） 以向上 too'E 字母的開始位置的程式碼會結合 ' hello 字母順序中。</span><span class="sxs-lookup"><span data-stu-id="66813-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="66813-166">然後它會顯示 hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="66813-166">Then it prints hello query results.</span></span> <span data-ttu-id="66813-167">如果您使用 hello 批次中的 hello 實體加入的 toohello 資料表插入本指南的區段，會傳回此時間 （Ben 和韓旻 Smith）; 只有兩個實體Jeff Smith 就不會包含。</span><span class="sxs-lookup"><span data-stu-id="66813-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="66813-168">作法：擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="66813-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="66813-169">您可以撰寫查詢 tooretrieve 單一的特定實體。</span><span class="sxs-lookup"><span data-stu-id="66813-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="66813-170">hello 下列程式碼呼叫**TableOperation.retrieve**與資料分割索引鍵和資料列索引鍵參數 toospecify hello 客戶"Jeff Smith"，而不是建立**TableQuery**和使用篩選器 toodo hello相同的動作。</span><span class="sxs-lookup"><span data-stu-id="66813-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="66813-171">在執行時，hello 擷取作業傳回單一實體，而不是集合。</span><span class="sxs-lookup"><span data-stu-id="66813-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="66813-172">hello **getResultAsType**方法將 hello 結果 toohello hello 分派目標類型， **CustomerEntity**物件。</span><span class="sxs-lookup"><span data-stu-id="66813-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="66813-173">如果此類型不相容於 hello hello 查詢指定的型別，就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="66813-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="66813-174">如果沒有實體具有完全相符的資料分割和資料列索引鍵，則會傳回 Null 值。</span><span class="sxs-lookup"><span data-stu-id="66813-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="66813-175">在查詢中指定資料分割和資料列索引鍵是最快方式 tooretrieve hello 與 hello 表格服務的單一實體。</span><span class="sxs-lookup"><span data-stu-id="66813-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="66813-176">作法：修改實體</span><span class="sxs-lookup"><span data-stu-id="66813-176">How to: Modify an entity</span></span>
<span data-ttu-id="66813-177">toomodify 實體，擷取與 hello 表格服務、 變更 toohello 實體物件，變更並儲存 hello 後 toohello 表格服務與取代或合併作業。</span><span class="sxs-lookup"><span data-stu-id="66813-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="66813-178">hello 下列程式碼變更現有的客戶電話號碼。</span><span class="sxs-lookup"><span data-stu-id="66813-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="66813-179">而不是呼叫**TableOperation.insert**像我們 tooinsert，此程式碼會呼叫**TableOperation.replace**。</span><span class="sxs-lookup"><span data-stu-id="66813-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="66813-180">hello **CloudTable.execute**方法會呼叫 hello 表格服務，而且要更換 hello 實體，除非另一個應用程式變更它的 hello 時間因為此應用程式擷取它。</span><span class="sxs-lookup"><span data-stu-id="66813-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="66813-181">當發生這種情況時，會擲回例外狀況，並 hello 實體必須擷取、 修改和儲存一次。</span><span class="sxs-lookup"><span data-stu-id="66813-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="66813-182">這種開放式並行存取重試模式在分散式儲存體系統中相當常見。</span><span class="sxs-lookup"><span data-stu-id="66813-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

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

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="66813-183">作法：查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="66813-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="66813-184">查詢 tooa 資料表可從實體擷取少數的屬性。</span><span class="sxs-lookup"><span data-stu-id="66813-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="66813-185">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="66813-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="66813-186">hello hello 下列程式碼中的查詢會使用 hello**選取**方法 tooreturn 只有 hello 電子郵件地址 hello 資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="66813-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="66813-187">hello 結果會投影成集合**字串**hello 協助**EntityResolver**，其中沒有 hello hello hello 伺服器傳回的實體上的型別轉換。</span><span class="sxs-lookup"><span data-stu-id="66813-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="66813-188">您可以在 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解投影。</span><span class="sxs-lookup"><span data-stu-id="66813-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="66813-189">請注意，投影上不支援 hello 本機儲存體模擬器，以便在 hello 表格服務上使用的帳戶時，才執行此程式碼。</span><span class="sxs-lookup"><span data-stu-id="66813-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

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

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="66813-190">作法：插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="66813-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="66813-191">通常您會希望 tooadd 實體 tooa 表而不需要知道如果 hello 資料表中已經存在。</span><span class="sxs-lookup"><span data-stu-id="66813-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="66813-192">插入或取代作業可讓您 toomake 單一要求將會插入 hello 實體，如果它不存在，或取代現有一，如果是這樣的 hello。</span><span class="sxs-lookup"><span data-stu-id="66813-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="66813-193">在先前的範例上建置，hello 下列程式碼插入或取代"Walter 絃樂豎琴"hello 實體。</span><span class="sxs-lookup"><span data-stu-id="66813-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="66813-194">之後建立新的實體，此程式碼呼叫 hello **TableOperation.insertOrReplace**方法。</span><span class="sxs-lookup"><span data-stu-id="66813-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="66813-195">此程式碼接著呼叫**執行**上 hello **CloudTable**物件 hello 資料表和 hello 插入或取代做為 hello 參數的資料表作業。</span><span class="sxs-lookup"><span data-stu-id="66813-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="66813-196">只有部分的實體，tooupdate hello **TableOperation.insertOrMerge**改為使用方法。</span><span class="sxs-lookup"><span data-stu-id="66813-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="66813-197">請注意讓 hello 表格服務上使用的帳戶時，才執行此程式碼，hello 本機儲存體模擬器，在不支援該插入-或-取代。</span><span class="sxs-lookup"><span data-stu-id="66813-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="66813-198">您可以在這個 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解插入或取代和插入或合併。</span><span class="sxs-lookup"><span data-stu-id="66813-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

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

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="66813-199">作法：刪除實體</span><span class="sxs-lookup"><span data-stu-id="66813-199">How to: Delete an entity</span></span>
<span data-ttu-id="66813-200">擷取實體之後，可以輕鬆地將它刪除。</span><span class="sxs-lookup"><span data-stu-id="66813-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="66813-201">Hello 實體擷取之後，呼叫**TableOperation.delete**與 hello 實體 toodelete。</span><span class="sxs-lookup"><span data-stu-id="66813-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="66813-202">然後呼叫**執行**上 hello **CloudTable**物件。</span><span class="sxs-lookup"><span data-stu-id="66813-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="66813-203">下列程式碼的 hello 擷取，並刪除一個 customer 實體。</span><span class="sxs-lookup"><span data-stu-id="66813-203">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="how-to-delete-a-table"></a><span data-ttu-id="66813-204">作法：刪除資料表</span><span class="sxs-lookup"><span data-stu-id="66813-204">How to: Delete a table</span></span>
<span data-ttu-id="66813-205">最後，hello 下列程式碼會刪除資料表從儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="66813-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="66813-206">已刪除的資料表將無法使用 toobe 一段時間通常少於 40 秒 hello 刪除重新建立。</span><span class="sxs-lookup"><span data-stu-id="66813-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="66813-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66813-207">Next steps</span></span>

* <span data-ttu-id="66813-208">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="66813-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="66813-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="66813-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="66813-210">[Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]</span><span class="sxs-lookup"><span data-stu-id="66813-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="66813-211">[Azure 儲存體 REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="66813-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="66813-212">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="66813-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="66813-213">如需詳細資訊，請參閱 hello [Java 開發人員中心](/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="66813-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
