---
title: "如何將 Azure 表格儲存體搭配 Python 使用 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: c310a52182bbc3cf44ed4dc6a04e97aa59200a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="72fde-103">如何在 Python 中使用表格儲存體</span><span class="sxs-lookup"><span data-stu-id="72fde-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="72fde-104">本指南說明如何使用 [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python) 在 Python 中執行一般 Azure 表格儲存體案例。</span><span class="sxs-lookup"><span data-stu-id="72fde-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="72fde-105">所涵蓋的案例包括建立與刪除資料表，以及插入與查詢實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="72fde-106">在進行本教學課程中的案例時，您可以參閱 [Azure Storage SDK for Python API 參考資料 (英文)](https://azure-storage.readthedocs.io/en/latest/index.html)。</span><span class="sxs-lookup"><span data-stu-id="72fde-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="72fde-107">安裝 Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="72fde-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="72fde-108">儲存體帳戶已建立後，下一個步驟就是安裝 [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)。</span><span class="sxs-lookup"><span data-stu-id="72fde-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="72fde-109">如需安裝 SDK 的詳細資料，請參閱 GitHub 上 [Storage SDK for Python] 存放庫中的 [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) 檔案。</span><span class="sxs-lookup"><span data-stu-id="72fde-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="72fde-110">建立資料表</span><span class="sxs-lookup"><span data-stu-id="72fde-110">Create a table</span></span>

<span data-ttu-id="72fde-111">若要在 Python 中使用 Azure 表格服務，您必須匯入 [TableService][py_TableService] 模組。</span><span class="sxs-lookup"><span data-stu-id="72fde-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="72fde-112">由於您將使用表格實體，因此也需要 [Entity][py_Entity] 類別。</span><span class="sxs-lookup"><span data-stu-id="72fde-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="72fde-113">在靠近您 Python 檔案的頂端處新增此程式碼，以匯入這兩者：</span><span class="sxs-lookup"><span data-stu-id="72fde-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="72fde-114">建立 [TableService][py_TableService] 物件以傳遞您的儲存體帳戶名稱與帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="72fde-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="72fde-115">以您的帳戶名稱與索引鍵取代 `myaccount` 與 `mykey`，然後呼叫 [create_table][py_create_table] 以便在 Azure 儲存體中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="72fde-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="72fde-116">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="72fde-116">Add an entity to a table</span></span>

<span data-ttu-id="72fde-117">若要新增實體，您先建立一個代表您實體的物件，然後將物件傳遞至 [TableService][py_TableService].[insert_entity][py_insert_entity] 方法。</span><span class="sxs-lookup"><span data-stu-id="72fde-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="72fde-118">實體物件可以是字典或類型為 [Entity][py_Entity] 的物件，並定義您實體的屬性名稱與值。</span><span class="sxs-lookup"><span data-stu-id="72fde-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="72fde-119">除了您為實體定義的任何其他屬性外。每個實體必須包含必要的 [PartitionKey and RowKey](#partitionkey-and-rowkey) 屬性。</span><span class="sxs-lookup"><span data-stu-id="72fde-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="72fde-120">此範例會建立一個代表實體的字典物件，然後將該物件傳遞至 [insert_entity][py_insert_entity] 方法，以將它新增至資料表：</span><span class="sxs-lookup"><span data-stu-id="72fde-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="72fde-121">此範例會建立一個代表[實體][py_Entity]的物件，然後將該物件傳遞至 [insert_entity][py_insert_entity] 方法，以將它新增至資料表：</span><span class="sxs-lookup"><span data-stu-id="72fde-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="72fde-122">PartitionKey 和 RowKey</span><span class="sxs-lookup"><span data-stu-id="72fde-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="72fde-123">您必須為每個實體指定 **PartitionKey** 與 **RowKey** 屬性。</span><span class="sxs-lookup"><span data-stu-id="72fde-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="72fde-124">這些屬性是您實體的唯一識別碼，共同形成實體的主要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="72fde-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="72fde-125">使用這些值查詢的速度遠快於使用任何其他實體屬性查詢，因為系統只會將這些屬性編製索引。</span><span class="sxs-lookup"><span data-stu-id="72fde-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="72fde-126">表格服務會使用 **PartitionKey**，以智慧化方式在儲存體節點之間分散資料表實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="72fde-127">具有相同 **PartitionKey** 的實體會儲存在相同的節點上。</span><span class="sxs-lookup"><span data-stu-id="72fde-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="72fde-128">**RowKey** 是實體在其所屬資料分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="72fde-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="72fde-129">更新實體</span><span class="sxs-lookup"><span data-stu-id="72fde-129">Update an entity</span></span>

<span data-ttu-id="72fde-130">若要更新實體的所有屬性值，請呼叫 [update_entity][py_update_entity] 方法。</span><span class="sxs-lookup"><span data-stu-id="72fde-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="72fde-131">此範例說明如何以實體的更新版本取代現有的實體：</span><span class="sxs-lookup"><span data-stu-id="72fde-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="72fde-132">如果正在更新的實體已不存在，則更新操作便會失敗。</span><span class="sxs-lookup"><span data-stu-id="72fde-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="72fde-133">如果您想要儲存實體，無論其是否存在，請使用 [insert_or_replace_entity][py_insert_or_replace_entity]。</span><span class="sxs-lookup"><span data-stu-id="72fde-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="72fde-134">在下列範例中，第一個呼叫將取代現有實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="72fde-135">第二個呼叫將插入新實體，因為資料表中沒有具有指定 PartitionKey 和 RowKey 的實體存在。</span><span class="sxs-lookup"><span data-stu-id="72fde-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="72fde-136">[update_entity][py_update_entity] 方法會取代現有實體其所有的屬性與值，您也可以用於移除現有實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="72fde-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="72fde-137">您可以使用 [merge_entity][py_merge_entity] 方法以新或已修改的屬性值來更新現有的實體，而不完全取代該實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="72fde-138">修改多個實體</span><span class="sxs-lookup"><span data-stu-id="72fde-138">Modify multiple entities</span></span>

<span data-ttu-id="72fde-139">若要確保表格服務對要求的處理為不可部分完成，您可以在一個批次中一起提交多個作業。</span><span class="sxs-lookup"><span data-stu-id="72fde-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="72fde-140">首先，使用 [TableBatch][py_TableBatch] 類別將多個作業新增至單一批次。</span><span class="sxs-lookup"><span data-stu-id="72fde-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="72fde-141">接著，呼叫 [TableService][py_TableService].[commit_batch][py_commit_batch] 以不可部分完成的作業提交這些作業。</span><span class="sxs-lookup"><span data-stu-id="72fde-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="72fde-142">要以批次修改的所有文件必須在同一個分割中。</span><span class="sxs-lookup"><span data-stu-id="72fde-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="72fde-143">此範例會在一個批次中同時新增兩個實體：</span><span class="sxs-lookup"><span data-stu-id="72fde-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="72fde-144">批次也可以與內容管理員語法搭配使用：</span><span class="sxs-lookup"><span data-stu-id="72fde-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="72fde-145">查詢實體</span><span class="sxs-lookup"><span data-stu-id="72fde-145">Query for an entity</span></span>

<span data-ttu-id="72fde-146">若要查詢資料表中的實體，請將其 PartitionKey 與 RowKey 傳遞至 [TableService][py_TableService].[get_entity][py_get_entity] 方法。</span><span class="sxs-lookup"><span data-stu-id="72fde-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="72fde-147">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="72fde-147">Query a set of entities</span></span>

<span data-ttu-id="72fde-148">您可以提供一個含 **filter** 參數的篩選字串，來查詢一組實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="72fde-149">此範例會對 PartitionKey 套用篩選條件，以尋找西雅圖中的所有工作：</span><span class="sxs-lookup"><span data-stu-id="72fde-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="72fde-150">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="72fde-150">Query a subset of entity properties</span></span>

<span data-ttu-id="72fde-151">您也可以限制會為查詢中的每個實體傳回哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="72fde-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="72fde-152">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體或結果集而言)。</span><span class="sxs-lookup"><span data-stu-id="72fde-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="72fde-153">使用 **select** 參數並傳遞您要傳回到用戶端的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="72fde-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="72fde-154">下列程式碼中的查詢只會傳回資料表中各實體的說明。</span><span class="sxs-lookup"><span data-stu-id="72fde-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="72fde-155">下列程式碼片段只針對 Azure 儲存體運作。</span><span class="sxs-lookup"><span data-stu-id="72fde-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="72fde-156">儲存體模擬器並不支援此程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="72fde-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="72fde-157">刪除實體</span><span class="sxs-lookup"><span data-stu-id="72fde-157">Delete an entity</span></span>

<span data-ttu-id="72fde-158">透過將實體的 PartitionKey 與 RowKey 傳遞至 [delete_entity][py_delete_entity] 方法來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="72fde-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="72fde-159">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="72fde-159">Delete a table</span></span>

<span data-ttu-id="72fde-160">如果您不再需要資料表及其內的任何實體，請呼叫 [delete_table][py_delete_table] 方法將資料表永久地從 Azure 儲存體中刪除。</span><span class="sxs-lookup"><span data-stu-id="72fde-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="72fde-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72fde-161">Next steps</span></span>

* [<span data-ttu-id="72fde-162">Azure Storage SDK for Python API 參考資料</span><span class="sxs-lookup"><span data-stu-id="72fde-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="72fde-163">Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="72fde-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="72fde-164">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="72fde-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="72fde-165">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)：一個免費、跨平台的應用程式，以視覺化方式在 Windows、macOS 和 Linux 上使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="72fde-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
