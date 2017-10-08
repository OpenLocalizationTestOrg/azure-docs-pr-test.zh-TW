---
title: "aaaHow toouse 從 Node.js 的 Azure 資料表儲存體 |Microsoft 文件"
description: "使用 Azure 資料表儲存體，NoSQL 資料存放區的 hello 雲端中儲存結構化的資料。"
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>如何 toouse 從 Node.js 的 Azure 資料表儲存體
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>概觀
本主題說明如何 tooperform 常見的案例，使用 hello Azure 表格服務在 Node.js 應用程式。

本主題中的 hello 程式碼範例假設您已經有 Node.js 應用程式。 如需有關資訊 toocreate Node.js 應用程式在 Azure 中，請參閱這些主題：

* [在 Azure App Service 中建立 Node.js Web 應用程式](../app-service-web/app-service-web-get-started-nodejs.md)
* [建置和部署使用 WebMatrix Node.js web 應用程式 tooAzure](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) （使用 Windows PowerShell）

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>設定您的應用程式 tooaccess Azure 儲存體
toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>使用節點封裝管理員 (NPM) tooinstall hello 套件
1. 使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Unix)，並瀏覽 toohello 資料夾建立您的應用程式的位置。
2. 型別**npm 安裝 azure 儲存體**hello 命令視窗中。 Hello 命令的輸出會類似下列範例的 toohello。

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
3. 您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。 在該資料夾中，您會發現 hello **azure 儲存體**套件，其中包含需要 tooaccess 儲存體的 hello 程式庫。

### <a name="import-hello-package"></a>匯入 hello 封裝
新增下列程式碼 toohello 頂端 hello hello**立即轉譯 server.js**應用程式中的檔案：

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello azure 模組會讀取 hello 環境變數 AZURE\_儲存體\_帳戶和 AZURE\_儲存體\_存取\_索引鍵或 AZURE\_儲存體\_連線\_所需的資訊 tooconnect tooyour Azure 儲存體帳戶的字串。 如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**TableService**。

如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure 網站，請參閱[Node.js web 應用程式使用 hello Azure 資料表服務](../app-service-web/storage-nodejs-use-table-storage-web-site.md)。

## <a name="create-a-table"></a>建立資料表
hello 下列程式碼會建立**TableService**物件，並使用它 toocreate 新的資料表。 新增 hello 頂端附近的 hello 下列**立即轉譯 server.js**。

```nodejs
var tableSvc = azure.createTableService();
```

太 hello 呼叫**createTableIfNotExists**將使用 hello 指定的名稱建立新的資料表，如果不存在。 hello 下列範例會建立新的資料表，名為 'mytable'，如果不存在：

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

hello`result.created`將`true`如果建立新的資料表，和`false`如果 hello 資料表已經存在。 hello`response`包含 hello 要求的相關資訊。

### <a name="filters"></a>篩選器
選擇性的篩選作業可能會使用執行套用的 toooperations **TableService**。 篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：

```nodejs
function handle (requestOptions, next)
```

執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步，將回呼傳遞具有下列簽章的 hello:

```nodejs
function (returnObject, finalCallback, next)
```

Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback 否則 tooend hello叫用服務。

實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。 hello 下列範例會建立**TableService**物件，使用 hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
tooadd 實體，會先建立定義實體屬性的物件。 所有實體必須都包含**PartitionKey**和**RowKey**，這是 hello 實體的唯一識別碼。

* **PartitionKey** -決定 hello 資料分割中所儲存的 hello 實體
* **RowKey** -唯一識別 hello hello 磁碟分割內的實體

**PartitionKey** 和 **RowKey** 都必須是字串值。 如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。

hello 下列是定義實體的範例。 請注意，**dueDate** 定義為 **Edm.DateTime** 類型。 指定 hello 類型為選擇性，而且型別會被推斷如果未指定。

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> 每筆記錄還有 [時間戳記] 欄位，插入或更新實體時，Azure 會設定此欄位。
>
>

您也可以使用 hello **entityGenerator** toocreate 實體。 hello 下列範例會建立 hello 相同工作的實體，使用 hello **entityGenerator**。

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd 實體 tooyour 表，傳遞 hello 實體物件 toohello **insertEntity**方法。

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

如果 hello 作業成功，`result`將包含 hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag)的 hello 插入記錄和`response`將包含 hello 作業的相關資訊。

範例回應：

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> 根據預設， **insertEntity**不會傳回插入的 hello 實體一部分 hello`response`資訊。 如果您計劃在這個實體上執行其他作業，或想 toocache hello 資訊時，它可以是它的 hello 一部分傳回的有用 toohave `result`。 您可以啟用 **echoContent** 來達成目的，如下所示：
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>更新實體
有多個方法可用 tooupdate 現有的實體：

* **replaceEntity** - 藉由取代來更新現有實體
* **mergeEntity** -將新的屬性值合併為 hello 現有實體，以更新現有的實體
* **insertOrReplaceEntity** - 藉由取代來更新現有實體。 如果實體不存在，將會插入新的實體。
* **insertOrMergeEntity** -更新現有的實體合併到現有的 hello 的新屬性值。 如果實體不存在，將會插入新的實體。

hello 下列範例示範如何更新實體使用**replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> 根據預設，更新實體不會檢查 toosee 如果 hello 資料正在更新先前已修改另一個處理序。 toosupport 並行更新：
>
> 1. 收到 hello hello 物件正在更新的 ETag。 這傳回的 hello`response`的任何實體相關的作業，而且可以透過擷取`response['.metadata'].etag`。
> 2. 當執行實體上的更新作業，會加入先前擷取 hello ETag 資訊 toohello 新實體。 例如：
>
>       entity2['.metadata'].etag = currentEtag;
> 3. 執行 hello 更新作業。 如果您擷取 hello ETag 值，例如應用程式的另一個執行個體之後，已被修改 hello 實體`error`將會傳回指出 hello 要求中指定的 hello 更新條件不符合。
>
>

與**replaceEntity**和**mergeEntity**，如果正在更新的 hello 實體不存在，hello 更新作業將會失敗。 如果您想 toostore 不論是否已經存在的實體，因此使用**insertOrReplaceEntity**或**insertOrMergeEntity**。

hello`result`成功的更新作業將會包含 hello **Etag** hello 更新實體。

## <a name="work-with-groups-of-entities"></a>使用實體群組
有時它可讓意義 toosubmit 多個作業一起批次 tooensure 中不可部分完成 hello 伺服器所處理。 可使用 hello tooaccomplish **TableBatch**類別 toocreate 批次中，然後使用 hello **executeBatch**方法**TableService** tooperform hello 批次作業。

 下列範例中的 hello 示範提交批次中的兩個實體：

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
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

成功的批次作業`result`會包含 hello 批次中每個作業的資訊。

### <a name="work-with-batched-operations"></a>處理批次作業
新增作業可以由檢視 hello 檢查 tooa 批次`operations`屬性。 您也可以使用下列方法 toowork 與作業的 hello:

* **clear** - 清除批次中的所有操作
* **getOperations** -取得作業從 hello 批次
* **hasOperations** -如果 hello 批次包含作業會傳回 true
* **removeOperations** - 移除操作
* **大小**-傳回 hello hello 批次中的作業數目

## <a name="retrieve-an-entity-by-key"></a>依索引鍵擷取實體
特定實體根據 hello tooreturn **PartitionKey**和**RowKey**，使用 hello **retrieveEntity**方法。

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

這項作業完成之後，`result`將包含 hello 實體。

## <a name="query-a-set-of-entities"></a>查詢實體集合
tooquery 資料表時，使用 hello **TableQuery**物件 toobuild 向上查詢運算式，使用下列子句 hello:

* **選取**-hello 欄位 toobe 查詢所傳回的 hello
* **其中**-hello 其中子句

  * **and** - `and` where 條件
  * **or** - `or` where 條件
* **top** -hello toofetch 項目數目

hello 下列範例建立一個查詢會傳回前五個項目與 PartitionKey 的 'hometasks' hello。

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

因為沒有使用 **select** ，所以會傳回所有欄位。 針對每個資料表，使用 tooperform hello 查詢**queryEntities**。 hello 下列範例會使用 'mytable' 來自這個查詢 tooreturn 實體。

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

如果成功的話，`result.entries`會包含符合 hello 查詢的實體的陣列。 如果無法 tooreturn hello 查詢所有實體，`result.continuationToken`將非*null* ，可以用來當做 hello 第三個參數**queryEntities** tooretrieve 取得更多結果。 Hello 初始查詢中，使用*null* hello 第三個參數。

### <a name="query-a-subset-of-entity-properties"></a>查詢實體屬性的子集
查詢 tooa 資料表可以從實體擷取幾個欄位。
這可以減少頻寬並提高查詢效能 (尤其是對大型實體而言)。 使用 hello**選取**hello 欄位 toobe 子句和傳遞 hello 名稱傳回。 例如，hello 下列查詢會傳回只 hello**描述**和**dueDate**欄位。

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>刪除實體
您可以使用實體的資料分割和資料列索引鍵來刪除實體。 在此範例中，hello **task1**物件包含 hello **RowKey**和**PartitionKey** hello 實體 toobe 刪除的值。 然後 hello 物件會傳遞 toohello **deleteEntity**方法。

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
> 請考慮刪除項目，項目 hello 的 tooensure 尚未由其他處理序修改時使用的 Etag。 請參閱 [更新實體](#update-an-entity) ，以取得使用 ETag 的相關資訊。
>
>

## <a name="delete-a-table"></a>刪除資料表
下列程式碼的 hello 從儲存體帳戶刪除資料表。

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

如果您不確定 hello 資料表是否存在，請使用**deleteTableIfExists**。

## <a name="use-continuation-tokens"></a>使用接續 Token
當您查詢大量結果的資料表時，請尋找接續 Token。 可能有大量的資料可供您可能不知道是否您不要建置 toorecognize 接續 token 存在時的查詢。

hello 結果物件期間查詢的實體集傳回`continuationToken`語彙基元時存在的屬性。 您可以再使用此跨 hello 資料分割和資料表實體執行查詢 toocontinue toomove 時。

在查詢時，可能會 hello 查詢物件執行個體與 hello 回呼函式之間提供 continuationToken 參數：

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

如果您檢查 hello`continuationToken`物件，您會發現屬性例如`nextPartitionKey`，`nextRowKey`和`targetLocation`，可能會使用的 tooiterate 透過 hello 的所有結果。

另外還有 hello GitHub 上的 Azure 儲存體 Node.js 儲存機制內的接續範例。 尋找 `examples/samples/continuationsample.js`。

## <a name="work-with-shared-access-signatures"></a>使用共用存取簽章
共用的存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tootables，但未提供您的儲存體帳戶名稱或索引鍵。 SAS 通常是使用的 tooprovide 有限存取 tooyour 資料，例如 tooquery 記錄允許行動裝置應用程式。

信任的應用程式，例如雲端服務會產生 SAS 使用 hello **generateSharedAccessSignature**的 hello **TableService**，然後將其提供 tooan 不受信任或非完全信任的應用程式例如，行動應用程式。 hello SAS 會產生使用原則描述 hello 開始和結束日期的 hello 期間 SAS 有效，以及 hello 存取層級授與的 toohello SAS 持有者。

hello 下列範例會產生新的共用的存取原則，可讓 SAS 持有者 ('r') tooquery hello 資料表 hello 與到期之後建立的 hello 時 100 分鐘。

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

請注意 hello 主機資訊必須提供此外，視需要當 hello SAS 持有者嘗試 tooaccess hello 資料表。

hello 用戶端應用程式，然後使用 hello 與 SAS **TableServiceWithSAS** tooperform hello 資料表作業。 下列範例中的 hello 連接 toohello 資料表，並執行查詢。

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Hello SAS 產生後有只查詢存取，嘗試進行 tooinsert 更新或刪除實體，則會傳回錯誤。

### <a name="access-control-lists"></a>存取控制清單
您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。 如果您想 tooallow 多個用戶端 tooaccess hello 資料表，但每個用戶端提供不同的存取原則，這非常有用。

ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。 hello 下列範例會定義兩個原則，一個用於 'user1'，'user2' 其中一個：

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

下列範例取得 hello hello hello 的目前 ACL **hometasks**資料表，並將 hello 新原則使用**setTableAcl**。 此方法允許：

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

一次 hello 已設定 ACL，然後您可以建立根據 hello 識別碼原則 SAS。 hello 下列範例會建立新的 SAS 'user2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello。

* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 儲存機制。
* [Node.js 開發人員中心](/develop/nodejs/)
* [建立及部署 Node.js 應用程式 tooan Azure 網站](../app-service-web/app-service-web-get-started-nodejs.md)
