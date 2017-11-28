---
title: "來自 PHP 的 aaaHow toouse 資料表儲存體 |Microsoft 文件"
description: "了解如何 toouse hello PHP toocreate 從表格服務及刪除資料表，並插入、 刪除和查詢 hello 資料表。"
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="4357f-103">如何 toouse 資料表來自 PHP 的儲存體</span><span class="sxs-lookup"><span data-stu-id="4357f-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="4357f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4357f-104">Overview</span></span>
<span data-ttu-id="4357f-105">本指南也說明如何使用 tooperform 常見案例 hello Azure 表格服務。</span><span class="sxs-lookup"><span data-stu-id="4357f-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="4357f-106">hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP][download]。</span><span class="sxs-lookup"><span data-stu-id="4357f-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="4357f-107">hello 涵蓋案例包括**建立和刪除資料表，並插入、 刪除和查詢資料表中的實體**。</span><span class="sxs-lookup"><span data-stu-id="4357f-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="4357f-108">如需有關 hello Azure 表格服務的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4357f-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="4357f-109">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="4357f-109">Create a PHP application</span></span>
<span data-ttu-id="4357f-110">只有建立 PHP 應用程式存取 hello Azure 表格服務的需求為 hello hello 參考 hello Azure SDK 中的類別從 PHP 的程式碼內。</span><span class="sxs-lookup"><span data-stu-id="4357f-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="4357f-111">您可以使用任何開發工具 toocreate 您的應用程式，包括 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="4357f-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="4357f-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的資料表服務功能，或可從 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的資料表服務功能。</span><span class="sxs-lookup"><span data-stu-id="4357f-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="4357f-113">取得 hello Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="4357f-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="4357f-114">設定您的應用程式 tooaccess hello 的資料表服務</span><span class="sxs-lookup"><span data-stu-id="4357f-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="4357f-115">您需要 toouse hello Azure 表格服務 Api:</span><span class="sxs-lookup"><span data-stu-id="4357f-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="4357f-116">參考 hello 自動換片器檔案使用 hello [require_once] [ require_once]陳述式，並</span><span class="sxs-lookup"><span data-stu-id="4357f-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="4357f-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="4357f-117">Reference any classes you might use.</span></span>

<span data-ttu-id="4357f-118">hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="4357f-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="4357f-119">本文中的 hello 範例假設您已安裝 hello Azure 透過編輯器的 PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4357f-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="4357f-120">如果您手動安裝 hello 程式庫，您需要 tooreference hello<code>WindowsAzure.php</code>自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="4357f-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="4357f-121">在以下範例 hello，hello`require_once`陳述式一定會顯示，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。</span><span class="sxs-lookup"><span data-stu-id="4357f-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="4357f-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="4357f-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="4357f-123">tooinstantiate Azure 表格服務用戶端，您必須先取得有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4357f-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="4357f-124">hello hello 資料表服務的連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="4357f-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="4357f-125">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="4357f-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="4357f-126">存取 hello 模擬器儲存體：</span><span class="sxs-lookup"><span data-stu-id="4357f-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="4357f-127">toocreate 任何 Azure 服務用戶端，您需要 toouse hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="4357f-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="4357f-128">您可以：</span><span class="sxs-lookup"><span data-stu-id="4357f-128">You can:</span></span>

* <span data-ttu-id="4357f-129">傳送嗨連接字串直接 tooit 或</span><span class="sxs-lookup"><span data-stu-id="4357f-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="4357f-130">使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：</span><span class="sxs-lookup"><span data-stu-id="4357f-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="4357f-131">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="4357f-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="4357f-132">您可以新增新的來源延伸 hello **ConnectionStringSource**類別</span><span class="sxs-lookup"><span data-stu-id="4357f-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="4357f-133">如需此處所述的 hello 範例，將直接傳遞 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="4357f-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="4357f-134">建立資料表</span><span class="sxs-lookup"><span data-stu-id="4357f-134">Create a table</span></span>
<span data-ttu-id="4357f-135">A **TableRestProxy**物件可讓您建立資料表以 hello **createTable**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="4357f-136">在建立資料表時，您可以設定 hello 資料表服務逾時。</span><span class="sxs-lookup"><span data-stu-id="4357f-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="4357f-137">(如需 hello 資料表服務逾時的詳細資訊，請參閱[設定表格服務作業的逾時值][table-service-timeouts]。)</span><span class="sxs-lookup"><span data-stu-id="4357f-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="4357f-138">資料表名稱的限制相關資訊，請參閱[了解 hello 表格服務資料模型][table-data-model]。</span><span class="sxs-lookup"><span data-stu-id="4357f-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="4357f-139">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="4357f-139">Add an entity tooa table</span></span>
<span data-ttu-id="4357f-140">tooadd 實體 tooa 資料表，建立新**實體**物件，並將它傳遞到太**TableRestProxy]-> [insertEntity**。</span><span class="sxs-lookup"><span data-stu-id="4357f-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="4357f-141">請注意，建立實體時，您必須指定 `PartitionKey` 和 `RowKey`。</span><span class="sxs-lookup"><span data-stu-id="4357f-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="4357f-142">這些是 hello 實體的唯一識別碼，而且可以進行查詢速度，比其他實體屬性的值。</span><span class="sxs-lookup"><span data-stu-id="4357f-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="4357f-143">hello 系統會使用`PartitionKey`tooautomatically 散發 hello 資料表實體，在許多儲存節點。</span><span class="sxs-lookup"><span data-stu-id="4357f-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="4357f-144">實體與 hello 相同`PartitionKey`儲存在 hello 上相同的節點。</span><span class="sxs-lookup"><span data-stu-id="4357f-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="4357f-145">(儲存在 hello 執行相同的節點上的多個實體上的作業優於實體儲存在不同節點上。)hello`RowKey`是 hello 的實體資料分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="4357f-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out hello trash.");
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

<span data-ttu-id="4357f-146">如需表格內容和型別資訊，請參閱[了解 hello 表格服務資料模型][table-data-model]。</span><span class="sxs-lookup"><span data-stu-id="4357f-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="4357f-147">hello **TableRestProxy**類別提供了兩個替代方法，來插入的實體： **insertOrMergeEntity**和**insertOrReplaceEntity**。</span><span class="sxs-lookup"><span data-stu-id="4357f-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="4357f-148">這些方法，建立新 toouse**實體**並將它傳遞為參數 tooeither 方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="4357f-149">每個方法會插入 hello 實體，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="4357f-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="4357f-150">如果 hello 實體已經存在， **insertOrMergeEntity** hello 屬性存在時，更新屬性值，並將新屬性加入如果它們尚不存在，而**insertOrReplaceEntity**完全取代現有的實體。</span><span class="sxs-lookup"><span data-stu-id="4357f-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="4357f-151">下列範例會示範如何 hello toouse **insertOrMergeEntity**。</span><span class="sxs-lookup"><span data-stu-id="4357f-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="4357f-152">如果 hello 與實體`PartitionKey`"tasksSeattle 」 和`RowKey`"1"不存在，將會插入。</span><span class="sxs-lookup"><span data-stu-id="4357f-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="4357f-153">不過，如果它先前已插入 （如上述的 hello 範例所示），hello`DueDate`屬性將會更新，而且 hello`Status`加入的屬性。</span><span class="sxs-lookup"><span data-stu-id="4357f-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="4357f-154">hello`Description`和`Location`屬性也會更新，但具有值，有效地讓它們保持不變。</span><span class="sxs-lookup"><span data-stu-id="4357f-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="4357f-155">如果這後者的兩個屬性不是加入 hello 範例所示，但存在於 hello 目標實體上，其現有的值會維持不變。</span><span class="sxs-lookup"><span data-stu-id="4357f-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="4357f-156">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="4357f-156">Retrieve a single entity</span></span>
<span data-ttu-id="4357f-157">hello **TableRestProxy]-> [getEntity**方法可讓您 tooretrieve 查詢取得的單一實體及其`PartitionKey`和`RowKey`。</span><span class="sxs-lookup"><span data-stu-id="4357f-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="4357f-158">Hello hello 以下範例中的 資料分割索引鍵`tasksSeattle`和資料列索引鍵`1`傳遞 toohello **getEntity**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="4357f-159">擷取資料分割中的所有實體</span><span class="sxs-lookup"><span data-stu-id="4357f-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="4357f-160">實體查詢使用篩選條件建構而成 (如需詳細資訊，請參閱[查詢資料表和實體][filters])。</span><span class="sxs-lookup"><span data-stu-id="4357f-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="4357f-161">tooretrieve 磁碟分割中的所有實體都使用 hello 篩選 」 PartitionKey eq *partition_name*"。</span><span class="sxs-lookup"><span data-stu-id="4357f-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="4357f-162">下列範例會示範如何 hello tooretrieve hello 中的所有實體`tasksSeattle`分割區藉由傳遞篩選 toohello **queryEntities**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="4357f-163">擷取資料分割中實體的子集</span><span class="sxs-lookup"><span data-stu-id="4357f-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="4357f-164">hello hello 前一個範例中所使用的相同模式可以是使用的 tooretrieve 資料分割中實體的任何子集。</span><span class="sxs-lookup"><span data-stu-id="4357f-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="4357f-165">您擷取的實體的 hello 子集取決於您使用的 hello 篩選器 (如需詳細資訊，請參閱[查詢資料表和實體][filters]).hello 下列範例會示範如何篩選 tooretrieve toouse所有與特定實體`Location`和`DueDate`小於指定的日期。</span><span class="sxs-lookup"><span data-stu-id="4357f-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="4357f-166">擷取實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="4357f-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="4357f-167">查詢可以擷取實體屬性的子集。</span><span class="sxs-lookup"><span data-stu-id="4357f-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="4357f-168">這項稱為「投射」 的技術可減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="4357f-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="4357f-169">toospecify 屬性 toobe 擷取，傳遞 hello 屬性 toohello hello 名稱**查詢]-> [addSelectField**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="4357f-170">您可以呼叫這個方法多次 tooadd 更多屬性。</span><span class="sxs-lookup"><span data-stu-id="4357f-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="4357f-171">在執行之後**TableRestProxy]-> [queryEntities**，hello 傳回實體只會有 hello 選取屬性。</span><span class="sxs-lookup"><span data-stu-id="4357f-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="4357f-172">（如果您想 tooreturn 資料表實體的子集，請使用篩選器 hello 上述查詢中所示）。</span><span class="sxs-lookup"><span data-stu-id="4357f-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="4357f-173">更新實體</span><span class="sxs-lookup"><span data-stu-id="4357f-173">Update an entity</span></span>
<span data-ttu-id="4357f-174">使用 hello 也可以更新現有的實體**實體]-> [setProperty**和**實體]-> [addProperty**上 hello 實體，然後呼叫的方法**TableRestProxy]-> [updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="4357f-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="4357f-175">hello 下列範例擷取實體、 修改一個屬性、 移除另一個屬性，並將新的屬性。</span><span class="sxs-lookup"><span data-stu-id="4357f-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="4357f-176">請注意，您可以移除屬性將其值設定為太**null**。</span><span class="sxs-lookup"><span data-stu-id="4357f-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="4357f-177">刪除實體</span><span class="sxs-lookup"><span data-stu-id="4357f-177">Delete an entity</span></span>
<span data-ttu-id="4357f-178">toodelete 實體，傳送 hello 資料表名稱，以及 hello 實體`PartitionKey`和`RowKey`toohello **TableRestProxy]-> [deleteEntity**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="4357f-179">請注意對於並行存取檢查，您可以設定為使用 hello 刪除實體 toobe hello Etag **DeleteEntityOptions]-> [setEtag**方法並傳遞 hello **DeleteEntityOptions**物件太**deleteEntity**做為第四個參數。</span><span class="sxs-lookup"><span data-stu-id="4357f-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="4357f-180">批次資料表作業</span><span class="sxs-lookup"><span data-stu-id="4357f-180">Batch table operations</span></span>
<span data-ttu-id="4357f-181">hello **TableRestProxy]-> [批次**方法可讓您 tooexecute 單一要求中的多個作業。</span><span class="sxs-lookup"><span data-stu-id="4357f-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="4357f-182">hello 模式，必須將加入作業太**BatchRequest**物件，然後再將傳遞 hello **BatchRequest**物件 toohello **TableRestProxy]-> [批次**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="4357f-183">tooadd 作業 tooa **BatchRequest**物件，您可以呼叫任何 hello 多次下列方法：</span><span class="sxs-lookup"><span data-stu-id="4357f-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="4357f-184">**addInsertEntity** (新增 insertEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="4357f-185">**addUpdateEntity** (新增 updateEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="4357f-186">**addMergeEntity** (新增 mergeEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="4357f-187">**addInsertOrReplaceEntity** (新增 insertOrReplaceEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="4357f-188">**addInsertOrMergeEntity** (新增 insertOrMergeEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="4357f-189">**addDeleteEntity** (新增 deleteEntity 作業)</span><span class="sxs-lookup"><span data-stu-id="4357f-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="4357f-190">下列範例會示範如何 hello tooexecute **insertEntity**和**deleteEntity**單一要求中的作業：</span><span class="sxs-lookup"><span data-stu-id="4357f-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
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

<span data-ttu-id="4357f-191">如需有關批次處理資料表作業的詳細資訊，請參閱[執行實體群組交易][entity-group-transactions]。</span><span class="sxs-lookup"><span data-stu-id="4357f-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="4357f-192">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="4357f-192">Delete a table</span></span>
<span data-ttu-id="4357f-193">最後，toodelete 資料表時，傳遞 hello 資料表名稱 toohello **TableRestProxy]-> [deleteTable**方法。</span><span class="sxs-lookup"><span data-stu-id="4357f-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4357f-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4357f-194">Next steps</span></span>
<span data-ttu-id="4357f-195">既然您已經學會 hello 的 hello Azure 表格服務的基本概念，請遵循這些連結 toolearn，更複雜的存放工作相關。</span><span class="sxs-lookup"><span data-stu-id="4357f-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="4357f-196">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="4357f-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="4357f-197">[PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="4357f-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
