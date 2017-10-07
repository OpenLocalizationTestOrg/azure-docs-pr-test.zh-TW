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
# <a name="how-toouse-table-storage-in-python"></a>如何 toouse Python 的表格儲存體

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

本指南也說明如何 tooperform 常見 Azure 資料表儲存體的案例中使用的 Python hello [Microsoft Azure 儲存體 SDK for Python](https://github.com/Azure/azure-storage-python)。 涵蓋的 hello 案例包括建立和刪除資料表，以及插入和查詢實體。

在本教學課程 hello 情況下工作，同時您可能希望 toorefer toohello [Azure 儲存體 SDK for Python 應用程式開發介面參考](https://azure-storage.readthedocs.io/en/latest/index.html)。

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>安裝 hello Azure 儲存體 SDK for Python

建立儲存體帳戶之後下, 一步為 tooinstall hello [Microsoft Azure 儲存體 SDK for Python](https://github.com/Azure/azure-storage-python)。 如需安裝的詳細資料 hello SDK，請參閱 toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst)檔案中儲存體 SDK hello Python 儲存機制的 GitHub 上。

## <a name="create-a-table"></a>建立資料表

toowork 以 hello Azure 表格服務有 Python，您必須匯入 hello [TableService] [ py_TableService]模組。 由於您會使用資料表實體，您也需要 hello[實體][ py_Entity]類別。 將這個 hello 頂端附近的程式碼加入您 Python 檔案 tooimport 這兩個：

```python
from azure.storage.table import TableService, Entity
```

建立 [TableService][py_TableService] 物件以傳遞您的儲存體帳戶名稱與帳戶金鑰。 取代`myaccount`和`mykey`與您的帳戶名稱和金鑰，並呼叫[create_table] [ py_create_table] toocreate hello 資料表在 Azure 儲存體。

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表

tooadd 實體，您先建立物件，表示您的實體，然後傳遞 hello 物件 toohello [TableService][py_TableService]。[insert_entity] [ py_insert_entity]方法。 hello 實體物件可以是字典或型別的物件[實體][py_Entity]，並定義實體的屬性名稱和值。 每個實體都必須包含所需的 hello [PartitionKey 和 RowKey](#partitionkey-and-rowkey)屬性，在加法 tooany 其他屬性您定義 hello 實體。

這個範例會建立一個字典物件表示實體，然後將其傳遞 toohello [insert_entity] [ py_insert_entity]方法 tooadd 它 toohello 資料表：

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

這個範例會建立[實體][ py_Entity]物件，然後將它傳遞至 toohello [insert_entity] [ py_insert_entity]方法 tooadd 它 toohello 資料表：

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey 和 RowKey

您必須為每個實體指定 **PartitionKey** 與 **RowKey** 屬性。 這些是 hello 唯一識別碼的實體，為在一起便形成 hello 主索引鍵的實體。 使用這些值查詢的速度遠快於使用任何其他實體屬性查詢，因為系統只會將這些屬性編製索引。

hello 資料表服務中使用**PartitionKey** toointelligently 將資料表實體分散到存放裝置節點。 具有實體 hello 相同**PartitionKey**儲存在 hello 上相同的節點。 **RowKey**是 hello 的 hello 實體所屬的 hello 磁碟分割內的唯一識別碼。

## <a name="update-an-entity"></a>更新實體

tooupdate 所有實體的屬性值，呼叫 hello [update_entity] [ py_update_entity]方法。 這個範例會示範如何 tooreplace 現有的實體，以更新的版本：

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

若要更新的 hello 實體不存在，hello 更新作業將會失敗。 如果您想 toostore 實體，是否存在與否，使用[insert_or_replace_entity][py_insert_or_replace_entity]。 在下列範例的 hello，hello 第一次呼叫將會取代 hello 現有實體。 hello 第二個呼叫會插入新實體，因為沒有實體以 hello 指定 PartitionKey 和 RowKey 存在 hello 資料表中。

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> hello [update_entity] [ py_update_entity]方法會取代所有屬性和值的現有實體，您也可以使用 tooremove 屬性，從現有的實體。 您可以使用 hello [merge_entity] [ py_merge_entity]方法 tooupdate 新建或修改過的屬性值，而不會完全取代 hello 實體與現有的實體。

## <a name="modify-multiple-entities"></a>修改多個實體

tooensure hello hello 表格服務的要求不可部分完成的處理，您可以提交批次中在一起的多個作業。 首先，使用 hello [TableBatch] [ py_TableBatch]類別 tooadd 多個作業 tooa 單一批次。 接下來，呼叫[TableService][py_TableService]。[commit_batch] [ py_commit_batch] toosubmit hello 作業不可部分完成的作業中。 修改批次中的所有實體 toobe hello 必須都是相同的資料分割。

此範例會在一個批次中同時新增兩個實體：

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

批次也可以搭配 hello 內容管理員語法：

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>查詢實體

在資料表中，實體 tooquery 傳遞其 PartitionKey 和 RowKey toohello [TableService][py_TableService]。[get_entity] [ py_get_entity]方法。

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>查詢實體集合

您可以藉由提供篩選條件字串 hello 與查詢的一組實體**篩選**參數。 此範例會對 PartitionKey 套用篩選條件，以尋找西雅圖中的所有工作：

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集

您也可以限制會為查詢中的每個實體傳回哪些屬性。 這項稱為「投射」的技術可減少頻寬並提高查詢效能 (尤其是對大型實體或結果集而言)。 使用 hello**選取**的您想要的 hello 屬性的參數，並傳入 hello 名稱傳回 toohello 用戶端。

hello，下列程式碼中的 hello 查詢會傳回只 hello 描述實體的 hello 資料表中。

> [!NOTE]
> 下列程式碼片段適用於只針對 hello Azure 儲存體的 hello。 它不支援 hello 儲存體模擬器。

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>刪除實體

刪除實體，藉由傳遞其 PartitionKey 和 RowKey toohello [delete_entity] [ py_delete_entity]方法。

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>刪除資料表

如果您不再需要的資料表，或任何 hello 實體內，呼叫 hello [delete_table] [ py_delete_table]方法 toopermanently 從 Azure 儲存體刪除 hello 資料表。

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>後續步驟

* [Azure Storage SDK for Python API 參考資料](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)
* [Python 開發人員中心](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)：一個免費、跨平台的應用程式，以視覺化方式在 Windows、macOS 和 Linux 上使用 Azure 儲存體資料。

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
