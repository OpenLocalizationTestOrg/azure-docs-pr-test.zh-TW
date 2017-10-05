---
title: "如何使用 PHP 中的資料表儲存體 | Microsoft Docs"
description: "了解如何使用 PHP 的資料表服務來建立和刪除資料表，以及插入、刪除和查詢資料表。"
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7a48446a11c5c6db0c9f4fdd8872b1e3c12e85c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="0dea8-103">如何使用 PHP 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="0dea8-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="0dea8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0dea8-104">Overview</span></span>
<span data-ttu-id="0dea8-105">本指南說明如何使用 Azure 資料表服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="0dea8-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="0dea8-106">這些範例均是以 PHP 撰寫，並使用 [Azure SDK for PHP][download]。</span><span class="sxs-lookup"><span data-stu-id="0dea8-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="0dea8-107">所涵蓋的案例包括「建立和刪除資料表」以及「在資料表中插入、刪除及查詢實體」 。</span><span class="sxs-lookup"><span data-stu-id="0dea8-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="0dea8-108">如需有關 Azure 資料表服務的詳細資訊，請參閱 [後續步驟](#next-steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="0dea8-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="0dea8-109">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="0dea8-109">Create a PHP application</span></span>
<span data-ttu-id="0dea8-110">若要建立一個存取 Azure 資料表服務的 PHP 應用程式，唯一的要求就是從您的程式碼內參考 Azure SDK for PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="0dea8-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="0dea8-111">您可以使用任何開發工具來建立應用程式 (包括 [記事本])。</span><span class="sxs-lookup"><span data-stu-id="0dea8-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="0dea8-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的資料表服務功能，或可從 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的資料表服務功能。</span><span class="sxs-lookup"><span data-stu-id="0dea8-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="0dea8-113">取得 Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="0dea8-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="0dea8-114">設定讓您的應用程式存取資料表服務</span><span class="sxs-lookup"><span data-stu-id="0dea8-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="0dea8-115">若要使用 Azure 資料表服務 API，您必須：</span><span class="sxs-lookup"><span data-stu-id="0dea8-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="0dea8-116">參考使用 [require_once][require_once] 陳述式的自動載入器檔案，以及</span><span class="sxs-lookup"><span data-stu-id="0dea8-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="0dea8-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="0dea8-117">Reference any classes you might use.</span></span>

<span data-ttu-id="0dea8-118">下列範例顯示如何納入自動載入器檔案及參考 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="0dea8-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="0dea8-119">本文中的範例假設您已透過 Composer 安裝 PHP Client Libraries for Azure。</span><span class="sxs-lookup"><span data-stu-id="0dea8-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="0dea8-120">如果您是以手動方式安裝程式庫，則必須參考 <code>WindowsAzure.php</code> 自動載入器檔案。</span><span class="sxs-lookup"><span data-stu-id="0dea8-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="0dea8-121">在下列各範例中，一律會顯示 `require_once` 陳述式，但只會參考要執行之範例所需的類別。</span><span class="sxs-lookup"><span data-stu-id="0dea8-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="0dea8-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="0dea8-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="0dea8-123">若要具現化 Azure 資料表服務用戶端，您必須先具備一個有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0dea8-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="0dea8-124">資料表服務的連接字串格式為：</span><span class="sxs-lookup"><span data-stu-id="0dea8-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="0dea8-125">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="0dea8-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="0dea8-126">用於存取模擬器儲存體：</span><span class="sxs-lookup"><span data-stu-id="0dea8-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="0dea8-127">若要建立任何 Azure 服務用戶端，您必須使用 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="0dea8-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="0dea8-128">您可以：</span><span class="sxs-lookup"><span data-stu-id="0dea8-128">You can:</span></span>

* <span data-ttu-id="0dea8-129">直接將連接字串傳遞給它，或</span><span class="sxs-lookup"><span data-stu-id="0dea8-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="0dea8-130">使用 **CloudConfigurationManager (CCM)** 到多種外部來源檢查連接字串：</span><span class="sxs-lookup"><span data-stu-id="0dea8-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="0dea8-131">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="0dea8-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="0dea8-132">您可以擴充 **ConnectionStringSource** 類別以加入新來源</span><span class="sxs-lookup"><span data-stu-id="0dea8-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="0dea8-133">在本文的各範例中，將會直接傳遞連接字串。</span><span class="sxs-lookup"><span data-stu-id="0dea8-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="0dea8-134">建立資料表</span><span class="sxs-lookup"><span data-stu-id="0dea8-134">Create a table</span></span>
<span data-ttu-id="0dea8-135">**TableRestProxy** 物件可讓您以 **createTable** 方法建立資料表。</span><span class="sxs-lookup"><span data-stu-id="0dea8-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="0dea8-136">建立資料表時，您可以設定資料表服務逾時值。</span><span class="sxs-lookup"><span data-stu-id="0dea8-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="0dea8-137">(如需有關表格服務逾時值的詳細資訊，請參閱[設定表格服務作業的逾時值][table-service-timeouts]。)</span><span class="sxs-lookup"><span data-stu-id="0dea8-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

<span data-ttu-id="0dea8-138">如需有關資料表名稱限制的資訊，請參閱[了解表格服務資料模型][table-data-model]。</span><span class="sxs-lookup"><span data-stu-id="0dea8-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="0dea8-139">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="0dea8-139">Add an entity to a table</span></span>
<span data-ttu-id="0dea8-140">若要將實體新增至資料表，請建立一個新的 **Entity** 物件，然後將它傳遞給 **TableRestProxy->insertEntity**。</span><span class="sxs-lookup"><span data-stu-id="0dea8-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="0dea8-141">請注意，建立實體時，您必須指定 `PartitionKey` 和 `RowKey`。</span><span class="sxs-lookup"><span data-stu-id="0dea8-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="0dea8-142">這些是實體的唯一識別碼，且其值的查詢速度比其他屬性快上許多。</span><span class="sxs-lookup"><span data-stu-id="0dea8-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="0dea8-143">系統使用 `PartitionKey` 自動將資料表的實體散發在許多儲存體節點上。</span><span class="sxs-lookup"><span data-stu-id="0dea8-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="0dea8-144">具有相同 `PartitionKey` 的實體會儲存在相同節點上。</span><span class="sxs-lookup"><span data-stu-id="0dea8-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="0dea8-145">(對儲存在同一節點上的多個實體執行作業，會比對儲存在不同節點上的實體執行作業有更佳的執行效果。)`RowKey` 是實體在分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0dea8-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="0dea8-146">如需有關資料表屬性和類型的資訊，請參閱[了解表格服務資料模型][table-data-model]。</span><span class="sxs-lookup"><span data-stu-id="0dea8-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="0dea8-147">**TableRestProxy** 類別提供兩種插入實體的替代方法：**insertOrMergeEntity** 和 **insertOrReplaceEntity**。</span><span class="sxs-lookup"><span data-stu-id="0dea8-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="0dea8-148">若要使用這些方法，請建立一個新的 **Entity** ，然後將它當做參數傳遞給其中一個方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="0dea8-149">只要實體不存在，每個方法都會插入實體。</span><span class="sxs-lookup"><span data-stu-id="0dea8-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="0dea8-150">如果實體已經存在，**insertOrMergeEntity** 會在屬性已經存在時更新屬性值，並在屬性不存在時新增屬性，而 **insertOrReplaceEntity** 則是會完全取代現有的實體。</span><span class="sxs-lookup"><span data-stu-id="0dea8-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="0dea8-151">下列範例示範如何使用 **insertOrMergeEntity**。</span><span class="sxs-lookup"><span data-stu-id="0dea8-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="0dea8-152">如果 `PartitionKey` 為「tasksSeattle」且 `RowKey` 為「1」的實體尚未存在，便會將之插入。</span><span class="sxs-lookup"><span data-stu-id="0dea8-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="0dea8-153">不過，如果先前已經插入 insertOrMergeEntity (如上述範例所示)，方法便會更新 `DueDate` 屬性並新增 `Status` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0dea8-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="0dea8-154">`Description` 和 `Location` 屬性也會更新，但是所使用的值實際上會讓它們保持不變。</span><span class="sxs-lookup"><span data-stu-id="0dea8-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="0dea8-155">如果如範例中所示並未新增後面兩個屬性，但這兩個屬性存在於目標實體上，它們現有的值就會保持不變。</span><span class="sxs-lookup"><span data-stu-id="0dea8-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="0dea8-156">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="0dea8-156">Retrieve a single entity</span></span>
<span data-ttu-id="0dea8-157">**TableRestProxy-&gt;getEntity`RowKey` 方法可讓您透過查詢其** 和 `PartitionKey` 來擷取單一實體。</span><span class="sxs-lookup"><span data-stu-id="0dea8-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="0dea8-158">在以下範例中，會將分割區索引鍵 `tasksSeattle` 和資料列索引鍵 `1` 傳遞給 **getEntity** 方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="0dea8-159">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="0dea8-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="0dea8-160">實體查詢使用篩選條件建構而成 (如需詳細資訊，請參閱[查詢資料表和實體][filters])。</span><span class="sxs-lookup"><span data-stu-id="0dea8-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="0dea8-161">若要擷取資料分割中的所有實體，請使用 "PartitionKey eq *partition_name*" 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="0dea8-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="0dea8-162">下列範例示範如何透過將篩選條件傳遞給 **queryEntities** 方法來擷取 `tasksSeattle` 分割中的所有實體。</span><span class="sxs-lookup"><span data-stu-id="0dea8-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="0dea8-163">擷取資料分割中實體的子集</span><span class="sxs-lookup"><span data-stu-id="0dea8-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="0dea8-164">前面範例中所使用的相同模式可用來擷取資料分割中的任何實體子集。</span><span class="sxs-lookup"><span data-stu-id="0dea8-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="0dea8-165">您所擷取的實體子集將取決於您使用的篩選條件 (如需詳細資訊，請參閱[查詢資料表和實體][filters])。下列範例示範如何使用篩選條件擷取位於特定 `Location` 且 `DueDate` 在指定日期之前的所有實體。</span><span class="sxs-lookup"><span data-stu-id="0dea8-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="0dea8-166">擷取實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="0dea8-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="0dea8-167">查詢可以擷取實體屬性的子集。</span><span class="sxs-lookup"><span data-stu-id="0dea8-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="0dea8-168">這項稱為「投射」 的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="0dea8-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="0dea8-169">若要指定要擷取的屬性，請將屬性的名稱傳遞給 **Query->addSelectField** 方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="0dea8-170">您可以呼叫此方法許多次以新增其他屬性。</span><span class="sxs-lookup"><span data-stu-id="0dea8-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="0dea8-171">執行 **TableRestProxy->queryEntities** 之後，傳回的實體將只具有選取的屬性。</span><span class="sxs-lookup"><span data-stu-id="0dea8-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="0dea8-172">(如果您想要傳回資料表實體的子集，請使用篩選條件，如上面的查詢所示。)</span><span class="sxs-lookup"><span data-stu-id="0dea8-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="0dea8-173">更新實體</span><span class="sxs-lookup"><span data-stu-id="0dea8-173">Update an entity</span></span>
<span data-ttu-id="0dea8-174">若要更新現有的實體，可以對實體使用 **Entity->setProperty** 和 **Entity->addProperty** 方法，然後呼叫 **TableRestProxy->updateEntity**。</span><span class="sxs-lookup"><span data-stu-id="0dea8-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="0dea8-175">下列範例會擷取一個實體、修改一個屬性、移除另一個屬性，以及新增一個屬性。</span><span class="sxs-lookup"><span data-stu-id="0dea8-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="0dea8-176">請注意，移除屬性的方式是將它的值設定成 **null**。</span><span class="sxs-lookup"><span data-stu-id="0dea8-176">Note that you can remove a property by setting its value to **null**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="0dea8-177">刪除實體</span><span class="sxs-lookup"><span data-stu-id="0dea8-177">Delete an entity</span></span>
<span data-ttu-id="0dea8-178">若要刪除實體，請將資料表名稱以及實體的 `PartitionKey` 和 `RowKey` 傳遞給 **TableRestProxy->deleteEntity** 方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0dea8-179">請注意，針對並行檢查，您可以使用 **DeleteEntityOptions->setEtag** 方法為要刪除的實體設定 Etag，並將 **DeleteEntityOptions** 物件傳遞給 **deleteEntity** 做為第四個參數。</span><span class="sxs-lookup"><span data-stu-id="0dea8-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="0dea8-180">批次資料表作業</span><span class="sxs-lookup"><span data-stu-id="0dea8-180">Batch table operations</span></span>
<span data-ttu-id="0dea8-181">**TableRestProxy->batch** 方法可讓您以單一要求執行多項作業。</span><span class="sxs-lookup"><span data-stu-id="0dea8-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="0dea8-182">這裡的模式涉及將作業新增至 **BatchRequest** 物件，然後將 **BatchRequest** 物件傳遞給 **TableRestProxy->batch** 方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="0dea8-183">若要將作業新增至 **BatchRequest** 物件，您可以呼叫下列任一方法許多次：</span><span class="sxs-lookup"><span data-stu-id="0dea8-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="0dea8-184">**addInsertEntity** (新增 insertEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="0dea8-185">**addUpdateEntity** (新增 updateEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="0dea8-186">**addMergeEntity** (新增 mergeEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="0dea8-187">**addInsertOrReplaceEntity** (新增 insertOrReplaceEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="0dea8-188">**addInsertOrMergeEntity** (新增 insertOrMergeEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="0dea8-189">**addDeleteEntity** (新增 deleteEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="0dea8-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="0dea8-190">下列範例示範如何以單一要求執行 **insertEntity** 和 **deleteEntity** 作業：</span><span class="sxs-lookup"><span data-stu-id="0dea8-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0dea8-191">如需有關批次處理資料表作業的詳細資訊，請參閱[執行實體群組交易][entity-group-transactions]。</span><span class="sxs-lookup"><span data-stu-id="0dea8-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="0dea8-192">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="0dea8-192">Delete a table</span></span>
<span data-ttu-id="0dea8-193">最後，若要刪除資料表，請將資料表名稱傳遞給 **TableRestProxy->deleteTable** 方法。</span><span class="sxs-lookup"><span data-stu-id="0dea8-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="0dea8-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dea8-194">Next steps</span></span>
<span data-ttu-id="0dea8-195">了解 Azure 資料表服務的基礎概念之後，請依循下列連結以深入了解更複雜的儲存體工作。</span><span class="sxs-lookup"><span data-stu-id="0dea8-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="0dea8-196">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="0dea8-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="0dea8-197">[PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="0dea8-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
