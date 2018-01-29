---
title: "如何使用 Node.js 中的 Azure 資料表儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/03/2017
ms.author: mimig
ms.openlocfilehash: 0b412be8b93e1f871c09b7a4452141ac334d53ae
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a>如何使用 Node.js 的 Azure 資料表儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>概觀
本主題示範如何使用 Node.js 應用程式中的 Azure 表格服務執行一般案例。

本主題中的程式碼範例假設您已經有 Node.js 應用程式。 如需如何在 Azure 中建立 Node.js 應用程式的資訊，請參閱下列主題：

* [在 Azure App Service 中建立 Node.js Web 應用程式](../app-service/app-service-web-get-started-nodejs.md)
* [建置 Node.js 應用程式並部署到 Azure 雲端服務](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (使用 Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a>設定您的應用程式以存取 Azure 儲存體
若要使用 Azure 儲存體，您需要 Azure Storage SDK for Node.js，這包含一組便利程式庫，能與儲存體 REST 服務通訊。

### <a name="use-node-package-manager-npm-to-install-the-package"></a>使用 Node Package Manager (NPM) 安裝封裝
1. 使用命令列介面，例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Unix)，瀏覽至儲存所建立應用程式的資料夾。
2. 在命令視窗中輸入 **npm install azure-storage** 。 此命令的輸出類似下列範例。

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. 您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。 該資料夾中有 **azure-storage** 封裝，當中包含存取儲存體所需的程式庫。

### <a name="import-the-package"></a>匯入封裝
將下列程式碼加在應用程式中的 **server.js** 檔案之上：

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
azure 模組會讀取環境變數 AZURE\_STORAGE\_ACCOUNT 和 AZURE\_STORAGE\_ACCESS\_KEY，或 AZURE\_STORAGE\_CONNECTION\_STRING，以取得連接 Azure 儲存體帳戶所需的資訊。 如果未設定這些環境變數，則呼叫 **TableService**時必須指定帳戶資訊。

## <a name="create-a-table"></a>建立資料表
下列程式碼會建立 **TableService** 物件，並使用該物件建立新資料表。 將下列內容新增至接近 **server.js**的頂端。

```nodejs
var tableSvc = azure.createTableService();
```

呼叫 **createTableIfNotExists** 會以指定的名稱建立新的資料表 (若尚未建立)。 如果名為 'mytable' 的資料表尚不存在，下列範例便會建立這個新資料表：

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

如果建立新資料表，`result.created` 將是 `true`，如果資料表已存在，則為 `false`。 `response` 會包含要求的相關資訊。

### <a name="filters"></a>篩選器
可以將選用性的篩選操作套用到使用 **TableService** 執行的操作。 篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：

```nodejs
function handle (requestOptions, next)
```

在對要求選項進行前處理之後，方法需要呼叫 "next" 並傳遞具有下列簽章的回呼：

```nodejs
function (returnObject, finalCallback, next)
```

在此回呼中，以及處理 returnObject (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是就改為叫用 finalCallback 結束服務叫用。

Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。 以下會建立使用 **ExponentialRetryPolicyFilter** 的 **TableService** 物件：

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a>將實體加入至資料表
若要新增實體，請先建立一個定義實體屬性的物件。 所有實體必須包含 **PartitionKey** 和 **RowKey**，這些是實體的唯一識別碼。

* **PartitionKey** - 決定儲存實體的資料分割。
* **RowKey** - 在資料分割內唯一地識別實體

**PartitionKey** 和 **RowKey** 都必須是字串值。 如需詳細資訊，請參閱 [了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。

以下是定義實體的範例。 請注意，**dueDate** 定義為 **Edm.DateTime** 類型。 可選擇是否指定型別，若未指定，則會推斷型別。

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> 每筆記錄還有 [時間戳記] 欄位，插入或更新實體時，Azure 會設定此欄位。
>
>

您也可以使用 **entityGenerator** 來建立實體。 下列範例使用 **entityGenerator**建立相同的工作實體。

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

若要將實體新增至資料表，請將實體物件傳給 **insertEntity** 方法。

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

若作業成功，`result` 會包含已插入記錄的 [ETag](http://en.wikipedia.org/wiki/HTTP_ETag)，`response` 則會包含作業的相關資訊。

範例回應：

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> 根據預設，**insertEntity** 不會將已插入的實體包含在 `response` 資訊中傳回。 若您打算對此實體執行其他作業，或想要快取資訊，將此實體包含在 `result`中傳回會是個不錯的方式。 您可以啟用 **echoContent** 來達成目的，如下所示：
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>更新實體
有多種方法可以用來更新現有的實體：

* **replaceEntity** - 藉由取代來更新現有實體
* **mergeEntity** - 藉由將新的屬性值合併到現有實體來更新現有實體
* **insertOrReplaceEntity** - 藉由取代來更新現有實體。 如果實體不存在，將會插入新的實體。
* **insertOrMergeEntity** - 藉由將新的屬性值合併到現有實體來更新現有實體。 如果實體不存在，將會插入新的實體。

下列範例示範使用 **replaceEntity**來更新實體：

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> 依預設，更新實體並不會檢查正在更新的資料先前是否被另一個程序修改過。 若要支援並行更新：
>
> 1. 取得正在更新之物件的 ETag。 系統會針對實體相關的作業將 ETag 包含在 `response` 中傳回，且可透過 `response['.metadata'].etag` 擷取 ETag。
> 2. 對實體執行更新操作時，請將先前擷取的 ETag 資訊新增至新的實體。 例如︰
>
>       entity2['.metadata'].etag = currentEtag;
> 3. 執行更新操作。 如果擷取 ETag 值之後，實體 (例如您應用程式的其他執行個體) 進行了修改，系統會傳回 `error` ，表示不符合要求中指定的更新條件。
>
>

使用 **replaceEntity** 和 **mergeEntity** 時，如果正在更新的實體不存在，則更新作業會失敗。 因此，如果您要儲存一個實體，而不管它是否已存在，您應該改用 **insertOrReplaceEntity** 或 **insertOrMergeEntity**。

更新作業成功的 `result` 將包含已更新實體的 **Etag** 。

## <a name="work-with-groups-of-entities"></a>使用實體群組
有時候批次提交多個操作是有意義的，可以確保伺服器會進行不可部分完成的處理。 若要達到此目的，請使用 **TableBatch** 類別建立批次，然後使用 **TableService** 的 **executeBatch** 方法執行批次作業。

 下列範例示範在批次中提交兩個實體：

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

成功的批次作業的 `result` 將包含批次中每個作業的相關資訊。

### <a name="work-with-batched-operations"></a>處理批次作業
若要檢查新增至批次的操作，您可以檢視 `operations` 屬性。 您也可以使用下列方法來處理操作：

* **clear** - 清除批次中的所有操作
* **getOperations** - 從批次取得操作
* **hasOperations** - 若批次包含操作，則傳回 true
* **removeOperations** - 移除操作
* **size** - 傳回批次中的操作數目

## <a name="retrieve-an-entity-by-key"></a>依索引鍵擷取實體
若要根據 **PartitionKey** 和 **RowKey** 傳回特定的實體，請使用 **retrieveEntity** 方法。

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

此作業完成時， `result` 將包含實體。

## <a name="query-a-set-of-entities"></a>查詢實體集合
若要查詢資料表，請透過 **TableQuery** 物件使用下列子句建置查詢運算式：

* **select** - 要從查詢傳回的欄位
* **where** - where 子句

  * **and** - `and` where 條件
  * **or** - `or` where 條件
* **top** - 要提取的項目數

下列範例建立的查詢會傳回 PartitionKey 為 'hometasks' 的前 5 個項目。

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

因為沒有使用 **select** ，所以會傳回所有欄位。 若要對資料表執行查詢，請使用 **queryEntities**。 下列範例使用此查詢從 'mytable' 傳回實體。

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

如果作業成功， `result.entries` 將包含符合查詢的實體陣列。 若查詢無法傳回所有實體，則 `result.continuationToken` 將為非*Null* ，並且可作為 **queryEntities** 的第三個參數來擷取更多結果。 在初始查詢中，第三個參數請使用 *null* 。

### <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
一項資料表查詢可以只擷取實體的少數欄位。
這可以減少頻寬並提高查詢效能 (尤其是對大型實體而言)。 請使用 **select** 子句並傳遞要傳回的欄位名稱。 例如，下列查詢只會傳回 **description** 和 **dueDate** 欄位。

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>刪除實體
您可以使用實體的資料分割和資料列索引鍵來刪除實體。 在本例中，**task1** 物件包含待刪除實體的 **RowKey** 及 **PartitionKey** 值。 然後物件會傳給 **deleteEntity** 方法。

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> 刪除項目時應該考慮使用 ETag，以確保項目未被另一個程序修改過。 請參閱 [更新實體](#update-an-entity) ，以取得使用 ETag 的相關資訊。
>
>

## <a name="delete-a-table"></a>刪除資料表
下列程式碼會從儲存體帳戶刪除資料表。

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

若不確定資料表是否存在，請使用 **deleteTableIfExists**。

## <a name="use-continuation-tokens"></a>使用接續 Token
當您查詢大量結果的資料表時，請尋找接續 Token。 因為您的查詢可能會產生大量可用的資料，如果該查詢並非可識別接續權杖存在的查詢，可能會無法得知。

當此類權杖存在時，在查詢實體設定 `continuationToken` 屬性期間，系統便會傳回結果物件。 您可以在執行查詢使用此方法以繼續在分割和資料表實體之間移動。

查詢時，系統可能會將 continuationToken 參數放在查詢物件執行個體和回呼函數之間：

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

如果您檢查 `continuationToken` 物件，您會找到像是 `nextPartitionKey`、`nextRowKey` 和 `targetLocation` 的屬性，這些屬性可以用來逐一查看所有結果。

GitHub 上的 Azure 儲存體 Node.js 儲存機制中也有接續範例。 尋找 `examples/samples/continuationsample.js`。

## <a name="work-with-shared-access-signatures"></a>使用共用存取簽章
共用存取簽章 (SAS) 可安全地提供對資料表的精確存取，而不必提供您的儲存體帳戶名稱或金鑰。 SAS 通常用來提供對資料的有限存取，例如允許行動應用程式查詢記錄。

信任的應用程式 (例如雲端型服務) 會使用 **TableService** 的 **generateSharedAccessSignature** 來產生 SAS，並提供它給不信任或不完全信任的應用程式 (例如行動應用程式)。 SAS 是使用原則來產生，該原則描述 SAS 有效期間的開始和結束日期，以及授與 SAS 持有者的存取等級。

下列範例會產生新的共用存取原則，讓 SAS 持有者查詢 ('r') 資料表，並於建立它之後的 100 分鐘過期。

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

請注意，也必須提供主機資訊，因為 SAS 持有者嘗試存取資料表時需要此資訊。

用戶端應用程式接著以 **TableServiceWithSAS** 來使用 SAS，對資料表執行操作。 下列範例會連線到資料表並執行查詢。

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

因為產生的 SAS 只有查詢權限，若嘗試插入、更新或刪除實體，則會傳回錯誤。

### <a name="access-control-lists"></a>存取控制清單
您也可以使用存取控制清單 (ACL) 來設定 SAS 的存取原則。 若您要允許用戶端存取資料表，但對每個用戶端提供不同的存取原則，則這會很有用。

ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。 下列範例定義兩個原則，其中一個用於 'user1'，另一個用於 'user2'：

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

下列範例會取得 **hometasks**資料表的目前 ACL，然後使用 **setTableAcl** 來加入新的原則。 此方法允許：

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

設定 ACL 之後，您可以根據原則的識別碼來建立 SAS。 下列範例會建立 'user2' 的新 SAS：

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源。

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。
* [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 儲存機制。
* [Node.js 開發人員中心](/develop/nodejs/)
* [建立 Node.js 應用程式並部署到 Azure 網站](../app-service/app-service-web-get-started-nodejs.md)