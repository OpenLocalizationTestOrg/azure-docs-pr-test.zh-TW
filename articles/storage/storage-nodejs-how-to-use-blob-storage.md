---
title: "aaaHow toouse Node.js 從 Blob 儲存體 |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>如何 toouse Node.js 從 Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>概觀
本文章將示範如何使用 Blob 儲存體 tooperform 常見案例。 透過 hello Node.js 應用程式開發介面撰寫 hello 範例。 涵蓋的 hello 案例包括 tooupload，列出、 下載及刪除 blob 的方式。

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式
如需有關指示 toocreate Node.js 應用程式，請參閱[Node.js web 應用程式建立 Azure App Service 中]，[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan] -使用 Windows PowerShell或[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]。

## <a name="configure-your-application-tooaccess-storage"></a>設定您的應用程式 tooaccess 儲存體
toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>使用節點封裝管理員 (NPM) tooobtain hello 套件
1. 使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Unix)，您用來建立您的範例 toonavigate toohello 資料夾應用程式。
2. 型別**npm 安裝 azure 儲存體**hello 命令視窗中。 Hello 命令的輸出會類似下列程式碼範例的 toohello。

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
3. 您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。 在該資料夾中，找出 hello **azure 儲存體**套件，其中包含需要 tooaccess 儲存體的 hello 程式庫。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用 [記事本] 或其他文字編輯器，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案，但您想 toouse 儲存體：

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello Azure 模組會讀取 hello 環境變數`AZURE_STORAGE_ACCOUNT`和`AZURE_STORAGE_ACCESS_KEY`，或`AZURE_STORAGE_CONNECTION_STRING`，資訊所需 tooconnect tooyour Azure 儲存體帳戶。 如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**createBlobService**。

如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure web 應用程式中，請參閱[Node.js web 應用程式使用 hello Azure 資料表服務]。

## <a name="create-a-container"></a>建立容器
hello **BlobService**物件可讓您使用容器和 blob。 hello 下列程式碼會建立**BlobService**物件。 新增 hello 頂端附近的 hello 下列**立即轉譯 server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> 您可以使用匿名存取 blob **createBlobServiceAnonymous**並提供 hello 主機位址。 例如，使用 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`。
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

使用新的容器，toocreate **createContainerIfNotExists**。 hello 下列程式碼範例會建立名為 'mycontainer' 的新容器：

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

如果剛新建 hello 容器，`result.created`為 true。 如果 hello 容器已經存在，`result.created`為 false。 `response`包含 hello 作業，包括 hello hello 容器的 ETag 資訊的相關資訊。

### <a name="container-security"></a>容器安全性
依預設，新的容器屬私人性質，無法以匿名方式存取。 toomake hello 容器公用，以供匿名存取，您可以設定 hello 容器的存取層級太**blob**或**容器**。

* **blob** -匿名讀取權限 tooblob 內容和中繼資料內這個容器中，但不 toocontainer 中繼資料，例如列出容器內的所有 blob
* **容器**-可讓匿名讀取權限 tooblob 內容和中繼資料，以及容器中繼資料

hello 下列程式碼範例示範設定 hello 存取層級太**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

或者，您可以修改容器的 hello 存取層級使用**setContainerAcl** toospecify hello 存取層級。 hello 下列程式碼範例變更 hello 存取層級 toocontainer:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

hello 結果包含 hello 作業資訊，包括 hello 目前**ETag** hello 容器。

### <a name="filters"></a>篩選器
您可以套用篩選作業選擇性使用 toooperations 執行**BlobService**。 篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：

```nodejs
function handle (requestOptions, next)
```

執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步，將回呼傳遞具有下列簽章的 hello:

```nodejs
function (returnObject, finalCallback, next)
```

Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback tooend hello 服務引動過程。

實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。 hello 下列範例會建立**BlobService**物件，使用 hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
有三種類型的 Blob：區塊 Blob、分頁 Blob 和附加 Blob。 區塊 blob 可讓您 toomore 有效率地將大型的資料上傳。 附加 Blob 已針對附加作業最佳化。 分頁 Blob 已針對讀/寫作業最佳化。 如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。

### <a name="block-blobs"></a>區塊 Blob
tooupload 資料 tooa 區塊 blob，使用下列的 hello:

* **createBlockBlobFromLocalFile** -建立新的區塊 blob 並上傳檔案的 hello 內容
* **createBlockBlobFromStream** -建立新的區塊 blob 並上傳的資料流的 hello 內容
* **createBlockBlobFromText** -建立新的區塊 blob 並上傳 hello 字串的內容
* **createWriteStreamToBlockBlob** -提供寫入資料流 tooa 區塊 blob

hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myblob**。

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

hello`result`這些方法所傳回包含有關 hello 作業，例如 hello **ETag**的 hello blob。

### <a name="append-blobs"></a>附加 Blob
tooupload 資料 tooa 新附加 blob，請使用下列 hello:

* **createAppendBlobFromLocalFile** -建立新的附加 blob 並上傳檔案的 hello 內容
* **createAppendBlobFromStream** -建立新的附加 blob 並上傳的資料流的 hello 內容
* **createAppendBlobFromText** -建立新的附加 blob 並上傳 hello 字串的內容
* **createWriteStreamToNewAppendBlob** -建立新的附加 blob，並提供資料流 toowrite tooit

hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myappendblob**。

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend 現有區塊 tooan 附加 blob，使用下列的 hello:

* **appendFromLocalFile** -附加 hello 內容的檔案 tooan 現有附加 blob
* **appendFromStream** -附加 hello 內容的資料流 tooan 現有附加 blob
* **appendFromText** -附加 hello 內容的字串 tooan 現有附加 blob
* **appendBlockFromStream** -附加 hello 內容的資料流 tooan 現有附加 blob
* **appendBlockFromText** -附加 hello 內容的字串 tooan 現有附加 blob

> [!NOTE]
> appendFromXXX Api 將會進行某些用戶端驗證 toofail 快速 tooavoid 不必要的伺服器呼叫。 appendBlockFromXXX 則否。
>
>

hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myappendblob**。

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>分頁 Blob
tooupload 資料 tooa 分頁 blob，使用下列的 hello:

* **createPageBlob** - 建立特定長度的新分頁 Blob
* **createPageBlobFromLocalFile** -建立新的分頁 blob 並上傳檔案的 hello 內容
* **createPageBlobFromStream** -建立新的分頁 blob 並上傳的資料流的 hello 內容
* **createWriteStreamToExistingPageBlob** -提供寫入資料流 tooan 現有的分頁 blob
* **createWriteStreamToNewPageBlob** -建立新的分頁 blob，並提供資料流 toowrite tooit

hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**mypageblob**。

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> 分頁 Blob 由 512 位元組的「分頁」組成。 如果上傳的資料大小不是 512 的倍數，則會接收到錯誤。
>
>

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的使用 hello **listBlobsSegmented**方法。 如果您想要以特定的前置詞 tooreturn blob，使用**listBlobsSegmentedWithPrefix**。

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

hello`result`包含`entries`集合，其描述每一個 blob 物件的陣列。 如果無法傳回的所有 blob，hello`result`也提供`continuationToken`，而您可以使用做為 hello 第二個參數 tooretrieve 其他項目。

## <a name="download-blobs"></a>下載 Blob
從 blob，toodownload 資料使用 hello 下列：

* **getBlobToLocalFile** -寫入 hello blob 內容 toofile
* **getBlobToStream** -寫入 hello blob 內容 tooa 資料流
* **getBlobToText** -hello blob 內容寫入 tooa 字串
* **createReadStream** -提供從 hello blob 資料流 tooread

hello 下列程式碼範例示範如何使用**getBlobToStream** hello toodownload hello 內容**myblob** blob，並將它儲存 toohello **output.txt**所使用的檔案資料流：

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

hello`result`包含 hello blob 的相關資訊包括**ETag**資訊。

## <a name="delete-a-blob"></a>刪除 Blob
最後，呼叫 toodelete blob， **deleteBlob**。 下列程式碼範例刪除 hello 名為 blob 的 hello **myblob**。

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>並行存取
您可以使用從多個用戶端或多個處理序執行個體的並行存取 tooa blob toosupport， **Etag**或**租用**。

* **Etag** -提供 hello blob 或容器的方式 toodetect 已被另一個處理序
* **租用**-提供方式 tooobtain 獨佔、 更新、 寫入或刪除的一段時間的存取 tooa blob

### <a name="etag"></a>ETag
如果您需要多個用戶端或執行個體 toowrite toohello 區塊 Blob 或分頁 Blob 同時 tooallow，使用 Etag。 hello ETag 可讓您 toodetermine 如果 hello 容器或 blob 已修改一開始讀取或建立，可讓您 tooavoid 覆寫其他用戶端或處理序認可的變更之後。

您可以使用選擇性的 hello 設定 ETag 條件`options.accessConditions`參數。 hello 下列程式碼範例只會將上傳 hello **test.txt**所包含的檔案，如果 hello blob 已經存在，而且具有 hello ETag 值`etagToMatch`。

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

當您使用的 Etag 時，hello 一般模式將會是：

1. 取得 hello ETag hello 的建立、 清單或取得作業的結果。
2. 執行動作，檢查該 hello ETag 值不修改。

如果已修改 hello 值，這表示另一個用戶端或執行個體修改 hello blob 或容器取得 hello ETag 值之後。

### <a name="lease"></a>租用
您可以取得新的租用，方式是使用 hello **acquireLease**方法，並指定 hello blob 或容器想 tooobtain 租用上。 例如，下列程式碼的 hello 上中取得的租用**myblob**。

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

在後續作業**myblob**必須提供 hello`options.leaseId`參數。 做為傳回識別碼 hello 租用`result.id`從**acquireLease**。

> [!NOTE]
> 根據預設，hello 租用持續時間為無限。 您可以指定非無限期持續時間 （介於 15 到 60 秒為單位） 藉由提供 hello`options.leaseDuration`參數。
>
>

tooremove 租用，使用**releaseLease**。 toobreak 租用，但防止其他 hello 原始期間過期之前，請取得新的租用，從使用**breakLease**。

## <a name="work-with-shared-access-signatures"></a>使用共用存取簽章
共用的存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tooblobs 和容器，但未提供您的儲存體帳戶名稱或索引鍵。 共用的存取簽章通常是使用的 tooprovide 有限存取 tooyour 資料，例如 tooaccess blob 允許行動裝置應用程式。

> [!NOTE]
> 雖然您也可以允許匿名存取 tooblobs，共用的存取簽章可讓您 tooprovide 較受控制的存取權，您必須產生 hello SAS。
>
>

信任的應用程式，例如雲端服務會產生共用的存取簽章使用 hello **generateSharedAccessSignature**的 hello **BlobService**，然後將其提供 tooan 不受信任或非完全信任應用程式，例如行動裝置應用程式。 共用的存取簽章使用產生的原則，其中描述 hello 開始和結束日期的 hello 期間共用的存取簽章不正確，以及 hello 存取層級授與的 toohello 共用的存取簽章持有者。

hello 下列程式碼範例會產生新的共用的存取原則，可讓 hello 共用存取簽章持有者 tooperform 的讀取作業 hello **myblob** blob，而且已過期之後建立的 hello 時 100 分鐘。

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

請注意 hello 主機資訊必須提供此外，視需要當 hello 共用的存取簽章持有者嘗試 tooaccess hello 容器。

hello 用戶端應用程式接著會使用共用的存取簽章**BlobServiceWithSAS** tooperform hello blob 的作業。 hello 下列取得資訊的相關**myblob**。

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

如果嘗試 toomodify hello blob hello 共用存取簽章產生具有唯讀存取權，因為將會傳回錯誤。

### <a name="access-control-lists"></a>存取控制清單
您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。 如果您想 tooallow 多個用戶端 tooaccess 容器，但每個用戶端提供不同的存取原則，這非常有用。

ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。 hello，下列程式碼範例會定義兩個原則，一個用於 'user1'，'user2' 其中一個：

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

下列程式碼範例會取得 hello hello 目前 ACL **mycontainer**，並將 hello 新原則使用**setBlobAcl**。 此方法允許：

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

一次 hello ACL 設定，然後您可以建立共用的存取簽章根據 hello 原則的識別碼。 hello，下列程式碼範例會建立新的共用的存取簽章 'user2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello。

* [Azure Storage SDK for Node API 參考][Azure Storage SDK for Node API Reference]
* [Azure 儲存體團隊部落格][Azure Storage Team Blog]
* GitHub 上的 [Azure Storage SDK for Node][Azure Storage SDK for Node] 儲存機制
* [Node.js 開發人員中心](https://azure.microsoft.com/develop/nodejs/)
* [使用 hello AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Node.js web 應用程式建立 Azure App Service 中]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web 應用程式使用 hello Azure 資料表服務]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
