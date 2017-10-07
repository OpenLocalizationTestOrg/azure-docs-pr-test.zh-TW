---
title: "aaaHow toouse 使用 Python Azure 資料表儲存體 |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="985ba-103">如何 toouse Python 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="985ba-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="985ba-104">本指南也說明如何 tooperform 常見 Azure 資料表儲存體的案例中使用的 Python hello [Microsoft Azure 儲存體 SDK for Python](https://github.com/Azure/azure-storage-python)。</span><span class="sxs-lookup"><span data-stu-id="985ba-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="985ba-105">涵蓋的 hello 案例包括建立和刪除資料表，以及插入和查詢實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="985ba-106">在本教學課程 hello 情況下工作，同時您可能希望 toorefer toohello [Azure 儲存體 SDK for Python 應用程式開發介面參考](https://azure-storage.readthedocs.io/en/latest/index.html)。</span><span class="sxs-lookup"><span data-stu-id="985ba-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="985ba-107">安裝 hello Azure 儲存體 SDK for Python</span><span class="sxs-lookup"><span data-stu-id="985ba-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="985ba-108">建立儲存體帳戶之後下, 一步為 tooinstall hello [Microsoft Azure 儲存體 SDK for Python](https://github.com/Azure/azure-storage-python)。</span><span class="sxs-lookup"><span data-stu-id="985ba-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="985ba-109">如需安裝的詳細資料 hello SDK，請參閱 toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst)檔案中儲存體 SDK hello Python 儲存機制的 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="985ba-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="985ba-110">建立資料表</span><span class="sxs-lookup"><span data-stu-id="985ba-110">Create a table</span></span>

<span data-ttu-id="985ba-111">toowork 以 hello Azure 表格服務有 Python，您必須匯入 hello [TableService] [ py_TableService]模組。</span><span class="sxs-lookup"><span data-stu-id="985ba-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="985ba-112">由於您會使用資料表實體，您也需要 hello[實體][ py_Entity]類別。</span><span class="sxs-lookup"><span data-stu-id="985ba-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="985ba-113">將這個 hello 頂端附近的程式碼加入您 Python 檔案 tooimport 這兩個：</span><span class="sxs-lookup"><span data-stu-id="985ba-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="985ba-114">建立 [TableService][py_TableService] 物件以傳遞您的儲存體帳戶名稱與帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="985ba-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="985ba-115">取代`myaccount`和`mykey`與您的帳戶名稱和金鑰，並呼叫[create_table] [ py_create_table] toocreate hello 資料表在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="985ba-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="985ba-116">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="985ba-116">Add an entity tooa table</span></span>

<span data-ttu-id="985ba-117">tooadd 實體，您先建立物件，表示您的實體，然後傳遞 hello 物件 toohello [TableService][py_TableService]。[insert_entity] [ py_insert_entity]方法。</span><span class="sxs-lookup"><span data-stu-id="985ba-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="985ba-118">hello 實體物件可以是字典或型別的物件[實體][py_Entity]，並定義實體的屬性名稱和值。</span><span class="sxs-lookup"><span data-stu-id="985ba-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="985ba-119">每個實體都必須包含所需的 hello [PartitionKey 和 RowKey](#partitionkey-and-rowkey)屬性，在加法 tooany 其他屬性您定義 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="985ba-120">這個範例會建立一個字典物件表示實體，然後將其傳遞 toohello [insert_entity] [ py_insert_entity]方法 tooadd 它 toohello 資料表：</span><span class="sxs-lookup"><span data-stu-id="985ba-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="985ba-121">這個範例會建立[實體][ py_Entity]物件，然後將它傳遞至 toohello [insert_entity] [ py_insert_entity]方法 tooadd 它 toohello 資料表：</span><span class="sxs-lookup"><span data-stu-id="985ba-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="985ba-122">PartitionKey 和 RowKey</span><span class="sxs-lookup"><span data-stu-id="985ba-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="985ba-123">您必須為每個實體指定 **PartitionKey** 與 **RowKey** 屬性。</span><span class="sxs-lookup"><span data-stu-id="985ba-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="985ba-124">這些是 hello 唯一識別碼的實體，為在一起便形成 hello 主索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="985ba-125">使用這些值查詢的速度遠快於使用任何其他實體屬性查詢，因為系統只會將這些屬性編製索引。</span><span class="sxs-lookup"><span data-stu-id="985ba-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="985ba-126">hello 資料表服務中使用**PartitionKey** toointelligently 將資料表實體分散到存放裝置節點。</span><span class="sxs-lookup"><span data-stu-id="985ba-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="985ba-127">具有實體 hello 相同**PartitionKey**儲存在 hello 上相同的節點。</span><span class="sxs-lookup"><span data-stu-id="985ba-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="985ba-128">**RowKey**是 hello 的 hello 實體所屬的 hello 磁碟分割內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="985ba-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="985ba-129">更新實體</span><span class="sxs-lookup"><span data-stu-id="985ba-129">Update an entity</span></span>

<span data-ttu-id="985ba-130">tooupdate 所有實體的屬性值，呼叫 hello [update_entity] [ py_update_entity]方法。</span><span class="sxs-lookup"><span data-stu-id="985ba-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="985ba-131">這個範例會示範如何 tooreplace 現有的實體，以更新的版本：</span><span class="sxs-lookup"><span data-stu-id="985ba-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="985ba-132">若要更新的 hello 實體不存在，hello 更新作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="985ba-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="985ba-133">如果您想 toostore 實體，是否存在與否，使用[insert_or_replace_entity][py_insert_or_replace_entity]。</span><span class="sxs-lookup"><span data-stu-id="985ba-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="985ba-134">在下列範例的 hello，hello 第一次呼叫將會取代 hello 現有實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="985ba-135">hello 第二個呼叫會插入新實體，因為沒有實體以 hello 指定 PartitionKey 和 RowKey 存在 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="985ba-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="985ba-136">hello [update_entity] [ py_update_entity]方法會取代所有屬性和值的現有實體，您也可以使用 tooremove 屬性，從現有的實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="985ba-137">您可以使用 hello [merge_entity] [ py_merge_entity]方法 tooupdate 新建或修改過的屬性值，而不會完全取代 hello 實體與現有的實體。</span><span class="sxs-lookup"><span data-stu-id="985ba-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="985ba-138">修改多個實體</span><span class="sxs-lookup"><span data-stu-id="985ba-138">Modify multiple entities</span></span>

<span data-ttu-id="985ba-139">tooensure hello hello 表格服務的要求不可部分完成的處理，您可以提交批次中在一起的多個作業。</span><span class="sxs-lookup"><span data-stu-id="985ba-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="985ba-140">首先，使用 hello [TableBatch] [ py_TableBatch]類別 tooadd 多個作業 tooa 單一批次。</span><span class="sxs-lookup"><span data-stu-id="985ba-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="985ba-141">接下來，呼叫[TableService][py_TableService]。[commit_batch] [ py_commit_batch] toosubmit hello 作業不可部分完成的作業中。</span><span class="sxs-lookup"><span data-stu-id="985ba-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="985ba-142">修改批次中的所有實體 toobe hello 必須都是相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="985ba-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="985ba-143">此範例會在一個批次中同時新增兩個實體：</span><span class="sxs-lookup"><span data-stu-id="985ba-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="985ba-144">批次也可以搭配 hello 內容管理員語法：</span><span class="sxs-lookup"><span data-stu-id="985ba-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="985ba-145">查詢實體</span><span class="sxs-lookup"><span data-stu-id="985ba-145">Query for an entity</span></span>

<span data-ttu-id="985ba-146">在資料表中，實體 tooquery 傳遞其 PartitionKey 和 RowKey toohello [TableService][py_TableService]。[get_entity] [ py_get_entity]方法。</span><span class="sxs-lookup"><span data-stu-id="985ba-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="985ba-147">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="985ba-147">Query a set of entities</span></span>

<span data-ttu-id="985ba-148">您可以藉由提供篩選條件字串 hello 與查詢的一組實體**篩選**參數。</span><span class="sxs-lookup"><span data-stu-id="985ba-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="985ba-149">此範例會對 PartitionKey 套用篩選條件，以尋找西雅圖中的所有工作：</span><span class="sxs-lookup"><span data-stu-id="985ba-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="985ba-150">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="985ba-150">Query a subset of entity properties</span></span>

<span data-ttu-id="985ba-151">您也可以限制會為查詢中的每個實體傳回哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="985ba-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="985ba-152">這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體或結果集而言)。</span><span class="sxs-lookup"><span data-stu-id="985ba-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="985ba-153">使用 hello**選取**的您想要的 hello 屬性的參數，並傳入 hello 名稱傳回 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="985ba-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="985ba-154">hello，下列程式碼中的 hello 查詢會傳回只 hello 描述實體的 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="985ba-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="985ba-155">下列程式碼片段適用於只針對 hello Azure 儲存體的 hello。</span><span class="sxs-lookup"><span data-stu-id="985ba-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="985ba-156">它不支援 hello 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="985ba-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="985ba-157">刪除實體</span><span class="sxs-lookup"><span data-stu-id="985ba-157">Delete an entity</span></span>

<span data-ttu-id="985ba-158">刪除實體，藉由傳遞其 PartitionKey 和 RowKey toohello [delete_entity] [ py_delete_entity]方法。</span><span class="sxs-lookup"><span data-stu-id="985ba-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="985ba-159">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="985ba-159">Delete a table</span></span>

<span data-ttu-id="985ba-160">如果您不再需要的資料表，或任何 hello 實體內，呼叫 hello [delete_table] [ py_delete_table]方法 toopermanently 從 Azure 儲存體刪除 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="985ba-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="985ba-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="985ba-161">Next steps</span></span>

* [<span data-ttu-id="985ba-162">Azure Storage SDK for Python API 參考資料</span><span class="sxs-lookup"><span data-stu-id="985ba-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="985ba-163">Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="985ba-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="985ba-164">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="985ba-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="985ba-165">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)：一個免費、跨平台的應用程式，以視覺化方式在 Windows、macOS 和 Linux 上使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="985ba-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
