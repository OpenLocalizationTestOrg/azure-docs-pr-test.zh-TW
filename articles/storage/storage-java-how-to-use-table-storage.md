---
title: "如何使用 Java 的表格儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
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
ms.openlocfilehash: a4d6f144cc6940ffe2b2c6f27553cd7aa3bcb381
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="9cf63-103">如何使用 Java 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="9cf63-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="9cf63-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9cf63-104">Overview</span></span>
<span data-ttu-id="9cf63-105">本指南將示範如何使用 Azure 資料表儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="9cf63-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="9cf63-106">相關範例是以 Java 撰寫並使用 [Azure Storage SDK for Java][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="9cf63-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="9cf63-107">所涵蓋的案例包括「建立」、「列出」和「刪除」資料表，以及在資料表中「插入」、「查詢」、「修改」和「刪除」實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="9cf63-108">如需資料表的詳細資訊，請參閱 [後續步驟](#Next-Steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="9cf63-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="9cf63-109">注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="9cf63-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="9cf63-110">如需詳細資訊，請參閱 [Azure Storage SDK for Android][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="9cf63-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="9cf63-111">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cf63-111">Create a Java application</span></span>
<span data-ttu-id="9cf63-112">在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。</span><span class="sxs-lookup"><span data-stu-id="9cf63-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="9cf63-113">若要這樣做，您需要安裝 Java Development Kit (JDK)，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cf63-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="9cf63-114">完成此動作之後，您需要驗證開發系統符合 GitHub 上的 [Azure Storage SDK for Java][Azure Storage SDK for Java] 儲存機制中所列出的最低需求和相依性。</span><span class="sxs-lookup"><span data-stu-id="9cf63-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="9cf63-115">如果系統符合這些需求，則您可以依照指示，從該儲存機制中下載 Azure Storage Libraries for Java 並安裝在系統上。</span><span class="sxs-lookup"><span data-stu-id="9cf63-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="9cf63-116">完成這些工作之後，您就能夠利用本文中的範例來建立 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf63-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="9cf63-117">設定您的應用程式來存取資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="9cf63-117">Configure your application to access table storage</span></span>
<span data-ttu-id="9cf63-118">在您要使用 Microsoft Azure 儲存體 API 來存取資料表的 Java 檔案頂端，新增下列 import 陳述式：</span><span class="sxs-lookup"><span data-stu-id="9cf63-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="9cf63-119">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="9cf63-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="9cf63-120">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="9cf63-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9cf63-121">在用戶端應用程式中執行時，您必須以下列格式提供儲存體連接字串 (其中的 AccountName 和 AccountKey 值要使用您儲存體帳戶的名稱，以及在 [Azure 入口網站](https://portal.azure.com)中針對該儲存體帳戶而列出的主要存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="9cf63-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9cf63-122">本範例將示範如何宣告靜態欄位來存放連接字串：</span><span class="sxs-lookup"><span data-stu-id="9cf63-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="9cf63-123">在 Microsoft Azure 的角色內執行的應用程式中，此字串可以儲存在服務組態檔 *ServiceConfiguration.cscfg* 裡，且可以藉由呼叫 **RoleEnvironment.getConfigurationSettings** 方法來存取。</span><span class="sxs-lookup"><span data-stu-id="9cf63-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="9cf63-124">以下是從服務組態檔中名為 **StorageConnectionString** 的 *Setting* 元素取得連接字串的範例：</span><span class="sxs-lookup"><span data-stu-id="9cf63-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="9cf63-125">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="9cf63-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="9cf63-126">作法：建立資料表</span><span class="sxs-lookup"><span data-stu-id="9cf63-126">How to: Create a table</span></span>
<span data-ttu-id="9cf63-127">**CloudTableClient** 物件可讓您取得資料表和實體的參照物件。</span><span class="sxs-lookup"><span data-stu-id="9cf63-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="9cf63-128">下列程式碼會建立 **CloudTableClient** 物件，並使用此物件建立新的 **CloudTable** 物件，此新物件代表一個名為 "people" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="9cf63-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="9cf63-129">(注意：還有其他方式可建立 **CloudStorageAccount** 物件。如需詳細資訊，請參閱 [Azure 儲存體用戶端 SDK 參考]中的 **CloudStorageAccount**。)</span><span class="sxs-lookup"><span data-stu-id="9cf63-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="9cf63-130">作法：列出資料表</span><span class="sxs-lookup"><span data-stu-id="9cf63-130">How to: List the tables</span></span>
<span data-ttu-id="9cf63-131">若要取得資料表清單，請呼叫 **CloudTableClient.listTables()** 方法來擷取可逐一查看的資料表名稱清單。</span><span class="sxs-lookup"><span data-stu-id="9cf63-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="9cf63-132">作法：將實體新增至資料表</span><span class="sxs-lookup"><span data-stu-id="9cf63-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="9cf63-133">將實體對應至 Java 物件，是透過一個實作 **TableEntity**的自訂類別進行。</span><span class="sxs-lookup"><span data-stu-id="9cf63-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="9cf63-134">為了方便起見，**TableServiceEntity** 類別會實作 **TableEntity**，並使用反映將屬性對應至為屬性指定的 Getter 和 Setter 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf63-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="9cf63-135">若要將實體新增至資料表，請先建立一個類別來定義實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="9cf63-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="9cf63-136">下列程式碼會定義一個使用客戶名字作為資料列索引鍵、並使用姓氏作為資料分割索引鍵的實體類別。</span><span class="sxs-lookup"><span data-stu-id="9cf63-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="9cf63-137">實體的資料分割索引鍵和資料列索引鍵共同唯一識別資料表中的實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="9cf63-138">相較於查詢具有不同資料分割索引鍵的實體，查詢具有相同資料分割索引鍵的實體速度會較快。</span><span class="sxs-lookup"><span data-stu-id="9cf63-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="9cf63-139">涉及實體的資料表操作需要 **TableOperation** 物件。</span><span class="sxs-lookup"><span data-stu-id="9cf63-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="9cf63-140">此物件定義了要在實體上執行的操作，而該操作可由 **CloudTable** 物件執行。</span><span class="sxs-lookup"><span data-stu-id="9cf63-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="9cf63-141">下列程式碼會建立 **CustomerEntity** 類別的新執行個體，其中含有一些要儲存的客戶資料。</span><span class="sxs-lookup"><span data-stu-id="9cf63-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="9cf63-142">程式碼接著會呼叫 **TableOperation.insertOrReplace** 來建立將實體插入資料表中的 **TableOperation** 物件，然後將新的 **CustomerEntity** 與該物件建立關聯。</span><span class="sxs-lookup"><span data-stu-id="9cf63-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="9cf63-143">最後，程式碼會呼叫 **CloudTable** 物件上的 **execute** 方法，其中指定 "people" 資料表和新的 **TableOperation**，而後者就會傳送要求給儲存體服務，以將新的客戶實體插入 "people" 資料表中。</span><span class="sxs-lookup"><span data-stu-id="9cf63-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="9cf63-144">作法：插入實體批次</span><span class="sxs-lookup"><span data-stu-id="9cf63-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="9cf63-145">您可以在單一寫入操作中，插入實體批次至資料表服務。</span><span class="sxs-lookup"><span data-stu-id="9cf63-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="9cf63-146">下列程式碼會建立一個 **TableBatchOperation** 物件，然後在其中新增三個插入操作。</span><span class="sxs-lookup"><span data-stu-id="9cf63-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="9cf63-147">新增插入作業的方式都是建立新的實體物件、設定其值，然後呼叫 **TableBatchOperation** 物件上的 **insert** 方法以將實體與新的插入操作建立關聯。</span><span class="sxs-lookup"><span data-stu-id="9cf63-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="9cf63-148">然後，程式碼會呼叫 **CloudTable** 物件上的 **execute**，其中指定 "people" 資料表和 **TableBatchOperation** 物件，而後者就會以單一要求將整批資料表操作傳送給儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="9cf63-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="9cf63-149">以下是批次操作的一些注意事項：</span><span class="sxs-lookup"><span data-stu-id="9cf63-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="9cf63-150">您可以在單一批次中最多執行 100 個插入、刪除、合併、取代、插入或合併，以及插入或取代操作的任意組合。</span><span class="sxs-lookup"><span data-stu-id="9cf63-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="9cf63-151">當擷取操作是批次中的唯一操作時，批次操作可以包含擷取操作。</span><span class="sxs-lookup"><span data-stu-id="9cf63-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="9cf63-152">單一批次操作中的所有實體必須具有相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9cf63-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="9cf63-153">一個批次操作的資料裝載限制為 4MB。</span><span class="sxs-lookup"><span data-stu-id="9cf63-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="9cf63-154">作法：擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="9cf63-155">若要查詢資料表以取得某個資料分割中的實體，可以使用 **TableQuery**。</span><span class="sxs-lookup"><span data-stu-id="9cf63-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="9cf63-156">呼叫 **TableQuery.from** 可在特定資料表上建立傳回指定結果類型的查詢。</span><span class="sxs-lookup"><span data-stu-id="9cf63-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="9cf63-157">下列程式碼會指定篩選器來篩選出資料分割索引鍵為 'Smith' 的實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="9cf63-158">**TableQuery.generateFilterCondition** 是一個用來建立查詢篩選器的 Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf63-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="9cf63-159">在 **TableQuery.from** 方法傳回的參考上呼叫 **where**，可將篩選器套用至查詢。</span><span class="sxs-lookup"><span data-stu-id="9cf63-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="9cf63-160">當呼叫 **CloudTable** 物件上的 **execute** 來執行查詢時，會傳回一個指定了 **CustomerEntity** 結果類型的 **Iterator**。</span><span class="sxs-lookup"><span data-stu-id="9cf63-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="9cf63-161">然後，您便可以將傳回的 **Iterator** 用於 for each 迴圈中以取用結果。</span><span class="sxs-lookup"><span data-stu-id="9cf63-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="9cf63-162">此程式碼會將查詢結果中每個實體的欄位列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="9cf63-162">This code prints the fields of each entity in the query results to the console.</span></span>

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

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="9cf63-163">作法：擷取資料分割中某個範圍的實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="9cf63-164">如果您不想要查詢資料分割中的所有實體，可以在篩選器中使用比較運算子來指定範圍。</span><span class="sxs-lookup"><span data-stu-id="9cf63-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="9cf63-165">下列程式碼會結合兩個篩選器，以取得 "Smith" 資料分割中資料列索引鍵 (名字) 開頭為字母 A 到 E 的所有實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="9cf63-166">然後列印查詢結果。</span><span class="sxs-lookup"><span data-stu-id="9cf63-166">Then it prints the query results.</span></span> <span data-ttu-id="9cf63-167">如果您使用在本指南批次插入小節中新增至資料表的實體，則這時只會傳回兩個實例 (Ben Smith 及 Denise Smith)；Jeff Smith 不在其中。</span><span class="sxs-lookup"><span data-stu-id="9cf63-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="9cf63-168">作法：擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="9cf63-169">您可以撰寫查詢來擷取單一特定實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="9cf63-170">下列程式碼會呼叫含資料分割索引鍵和資料列索引鍵參數 (以指定客戶 "Jeff Smith") 的 **TableOperation.retrieve**，而不是建立 **TableQuery** 再使用篩選器來達到同樣的目的。</span><span class="sxs-lookup"><span data-stu-id="9cf63-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="9cf63-171">執行時，擷取操作只會傳回一個實體，而不是傳回一個集合。</span><span class="sxs-lookup"><span data-stu-id="9cf63-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="9cf63-172">**getResultAsType** 方法會將結果轉換成指派目標 (**CustomerEntity** 物件) 的類型。</span><span class="sxs-lookup"><span data-stu-id="9cf63-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="9cf63-173">如果此類型與指定給查詢的類型不相容，將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9cf63-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="9cf63-174">如果沒有實體具有完全相符的資料分割和資料列索引鍵，則會傳回 Null 值。</span><span class="sxs-lookup"><span data-stu-id="9cf63-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="9cf63-175">若要從資料表服務中擷取單一實體，最快的方法是在查詢中同時指定資料分割索引鍵和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9cf63-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
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
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="9cf63-176">作法：修改實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-176">How to: Modify an entity</span></span>
<span data-ttu-id="9cf63-177">若要修改實體，請從資料表服務擷取它，對實體物件進行變更，然後以取代或合併操作將變更儲存回資料表服務。</span><span class="sxs-lookup"><span data-stu-id="9cf63-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="9cf63-178">下列程式碼會變更現有客戶的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="9cf63-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="9cf63-179">不像我們之前為了執行插入而呼叫 **TableOperation.insert**，這個程式碼會呼叫 **TableOperation.replace**。</span><span class="sxs-lookup"><span data-stu-id="9cf63-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="9cf63-180">**CloudTable.execute** 方法會呼叫資料表服務，然後實體就會被取代，除非有另一個應用程式在此應用程式擷取它後的這段時間變更了這個實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="9cf63-181">發生此情況時，系統會擲回例外狀況，且必須重新擷取、修改及儲存實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="9cf63-182">這種開放式並行存取重試模式在分散式儲存體系統中相當常見。</span><span class="sxs-lookup"><span data-stu-id="9cf63-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="9cf63-183">作法：查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="9cf63-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="9cf63-184">一項資料表查詢可以只擷取實體的少數屬性。</span><span class="sxs-lookup"><span data-stu-id="9cf63-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="9cf63-185">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="9cf63-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="9cf63-186">下列程式碼中的查詢會使用 **select** 方法，只傳回資料表中之實體的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9cf63-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="9cf63-187">結果會在 **EntityResolver** (負責對從伺服器傳回的實體執行類型轉換) 的幫助下投影至 **String** 的集合中。</span><span class="sxs-lookup"><span data-stu-id="9cf63-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="9cf63-188">您可以在 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解投影。</span><span class="sxs-lookup"><span data-stu-id="9cf63-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="9cf63-189">請注意，投射並不支援在本機儲存體模擬器上進行，因此此程式碼唯有在使用資料表服務上的帳戶時才會執行。</span><span class="sxs-lookup"><span data-stu-id="9cf63-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="9cf63-190">作法：插入或取代實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="9cf63-191">您經常會想要新增實體至資料表，但不知道它是否已在資料表中。</span><span class="sxs-lookup"><span data-stu-id="9cf63-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="9cf63-192">插入或取代實體允許您透過單一要求，如果實體不存在便插入它，若是存在則取代現有實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="9cf63-193">以先前的範例為基礎，下列程式碼會插入或取代 "Walter Harp" 的實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="9cf63-194">建立新實體之後，此程式碼會呼叫 **TableOperation.insertOrReplace** 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf63-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="9cf63-195">此程式碼接著會以資料表以及插入或取代資料表操作當作參數，在 **CloudTable** 物件上呼叫 **execute**。</span><span class="sxs-lookup"><span data-stu-id="9cf63-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="9cf63-196">若只要更新實體的某一部分，可以改用 **TableOperation.insertOrMerge** 方法。</span><span class="sxs-lookup"><span data-stu-id="9cf63-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="9cf63-197">請注意，插入或取代並不支援在本機儲存體模擬器上進行，因此此程式碼唯有在使用資料表服務上的帳戶時才會執行。</span><span class="sxs-lookup"><span data-stu-id="9cf63-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="9cf63-198">您可以在這個 [Azure 資料表：插入和查詢投影簡介][Azure Tables: Introducing Upsert and Query Projection]中進一步了解插入或取代和插入或合併。</span><span class="sxs-lookup"><span data-stu-id="9cf63-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="9cf63-199">作法：刪除實體</span><span class="sxs-lookup"><span data-stu-id="9cf63-199">How to: Delete an entity</span></span>
<span data-ttu-id="9cf63-200">擷取實體之後，可以輕鬆地將它刪除。</span><span class="sxs-lookup"><span data-stu-id="9cf63-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="9cf63-201">擷取實體之後，請以要刪除的實體呼叫 **TableOperation.delete** 。</span><span class="sxs-lookup"><span data-stu-id="9cf63-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="9cf63-202">然後在 **CloudTable** 物件上呼叫 **execute**。</span><span class="sxs-lookup"><span data-stu-id="9cf63-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="9cf63-203">下列程式碼會擷取並刪除客戶實體。</span><span class="sxs-lookup"><span data-stu-id="9cf63-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="9cf63-204">作法：刪除資料表</span><span class="sxs-lookup"><span data-stu-id="9cf63-204">How to: Delete a table</span></span>
<span data-ttu-id="9cf63-205">最後，下列程式碼會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="9cf63-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="9cf63-206">刪除資料表後，將有一段時間無法重新建立該資料表，通常是 40 秒內。</span><span class="sxs-lookup"><span data-stu-id="9cf63-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="9cf63-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cf63-207">Next steps</span></span>

* <span data-ttu-id="9cf63-208">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="9cf63-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="9cf63-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="9cf63-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="9cf63-210">[Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]</span><span class="sxs-lookup"><span data-stu-id="9cf63-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="9cf63-211">[Azure 儲存體 REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="9cf63-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="9cf63-212">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="9cf63-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="9cf63-213">如需詳細資訊，也請參閱 [Java 開發人員中心](/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="9cf63-213">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="9cf63-214">[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="9cf63-214">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
