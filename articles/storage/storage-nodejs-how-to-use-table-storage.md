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
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="a6e21-103">如何 toouse 從 Node.js 的 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="a6e21-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="a6e21-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a6e21-104">Overview</span></span>
<span data-ttu-id="a6e21-105">本主題說明如何 tooperform 常見的案例，使用 hello Azure 表格服務在 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6e21-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="a6e21-106">本主題中的 hello 程式碼範例假設您已經有 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6e21-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="a6e21-107">如需有關資訊 toocreate Node.js 應用程式在 Azure 中，請參閱這些主題：</span><span class="sxs-lookup"><span data-stu-id="a6e21-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="a6e21-108">在 Azure App Service 中建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a6e21-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="a6e21-109">建置和部署使用 WebMatrix Node.js web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a6e21-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="a6e21-110">[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) （使用 Windows PowerShell）</span><span class="sxs-lookup"><span data-stu-id="a6e21-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="a6e21-111">設定您的應用程式 tooaccess Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a6e21-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="a6e21-112">toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="a6e21-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="a6e21-113">使用節點封裝管理員 (NPM) tooinstall hello 套件</span><span class="sxs-lookup"><span data-stu-id="a6e21-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="a6e21-114">使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Unix)，並瀏覽 toohello 資料夾建立您的應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="a6e21-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="a6e21-115">型別**npm 安裝 azure 儲存體**hello 命令視窗中。</span><span class="sxs-lookup"><span data-stu-id="a6e21-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="a6e21-116">Hello 命令的輸出會類似下列範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="a6e21-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="a6e21-117">您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="a6e21-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a6e21-118">在該資料夾中，您會發現 hello **azure 儲存體**套件，其中包含需要 tooaccess 儲存體的 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a6e21-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="a6e21-119">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="a6e21-119">Import hello package</span></span>
<span data-ttu-id="a6e21-120">新增下列程式碼 toohello 頂端 hello hello**立即轉譯 server.js**應用程式中的檔案：</span><span class="sxs-lookup"><span data-stu-id="a6e21-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="a6e21-121">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="a6e21-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="a6e21-122">hello azure 模組會讀取 hello 環境變數 AZURE\_儲存體\_帳戶和 AZURE\_儲存體\_存取\_索引鍵或 AZURE\_儲存體\_連線\_所需的資訊 tooconnect tooyour Azure 儲存體帳戶的字串。</span><span class="sxs-lookup"><span data-stu-id="a6e21-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="a6e21-123">如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**TableService**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="a6e21-124">如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure 網站，請參閱[Node.js web 應用程式使用 hello Azure 資料表服務](../app-service-web/storage-nodejs-use-table-storage-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e21-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a6e21-125">建立資料表</span><span class="sxs-lookup"><span data-stu-id="a6e21-125">Create a table</span></span>
<span data-ttu-id="a6e21-126">hello 下列程式碼會建立**TableService**物件，並使用它 toocreate 新的資料表。</span><span class="sxs-lookup"><span data-stu-id="a6e21-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="a6e21-127">新增 hello 頂端附近的 hello 下列**立即轉譯 server.js**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="a6e21-128">太 hello 呼叫**createTableIfNotExists**將使用 hello 指定的名稱建立新的資料表，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="a6e21-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="a6e21-129">hello 下列範例會建立新的資料表，名為 'mytable'，如果不存在：</span><span class="sxs-lookup"><span data-stu-id="a6e21-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="a6e21-130">hello`result.created`將`true`如果建立新的資料表，和`false`如果 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="a6e21-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="a6e21-131">hello`response`包含 hello 要求的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e21-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="a6e21-132">篩選器</span><span class="sxs-lookup"><span data-stu-id="a6e21-132">Filters</span></span>
<span data-ttu-id="a6e21-133">選擇性的篩選作業可能會使用執行套用的 toooperations **TableService**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="a6e21-134">篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：</span><span class="sxs-lookup"><span data-stu-id="a6e21-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="a6e21-135">執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步，將回呼傳遞具有下列簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6e21-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a6e21-136">Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback 否則 tooend hello叫用服務。</span><span class="sxs-lookup"><span data-stu-id="a6e21-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="a6e21-137">實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a6e21-138">hello 下列範例會建立**TableService**物件，使用 hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="a6e21-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="a6e21-139">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="a6e21-139">Add an entity tooa table</span></span>
<span data-ttu-id="a6e21-140">tooadd 實體，會先建立定義實體屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="a6e21-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="a6e21-141">所有實體必須都包含**PartitionKey**和**RowKey**，這是 hello 實體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a6e21-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="a6e21-142">**PartitionKey** -決定 hello 資料分割中所儲存的 hello 實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="a6e21-143">**RowKey** -唯一識別 hello hello 磁碟分割內的實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="a6e21-144">**PartitionKey** 和 **RowKey** 都必須是字串值。</span><span class="sxs-lookup"><span data-stu-id="a6e21-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="a6e21-145">如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a6e21-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="a6e21-146">hello 下列是定義實體的範例。</span><span class="sxs-lookup"><span data-stu-id="a6e21-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="a6e21-147">請注意，**dueDate** 定義為 **Edm.DateTime** 類型。</span><span class="sxs-lookup"><span data-stu-id="a6e21-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="a6e21-148">指定 hello 類型為選擇性，而且型別會被推斷如果未指定。</span><span class="sxs-lookup"><span data-stu-id="a6e21-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="a6e21-149">每筆記錄還有 [時間戳記] 欄位，插入或更新實體時，Azure 會設定此欄位。</span><span class="sxs-lookup"><span data-stu-id="a6e21-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="a6e21-150">您也可以使用 hello **entityGenerator** toocreate 實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="a6e21-151">hello 下列範例會建立 hello 相同工作的實體，使用 hello **entityGenerator**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="a6e21-152">tooadd 實體 tooyour 表，傳遞 hello 實體物件 toohello **insertEntity**方法。</span><span class="sxs-lookup"><span data-stu-id="a6e21-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="a6e21-153">如果 hello 作業成功，`result`將包含 hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag)的 hello 插入記錄和`response`將包含 hello 作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e21-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="a6e21-154">範例回應：</span><span class="sxs-lookup"><span data-stu-id="a6e21-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="a6e21-155">根據預設， **insertEntity**不會傳回插入的 hello 實體一部分 hello`response`資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e21-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="a6e21-156">如果您計劃在這個實體上執行其他作業，或想 toocache hello 資訊時，它可以是它的 hello 一部分傳回的有用 toohave `result`。</span><span class="sxs-lookup"><span data-stu-id="a6e21-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="a6e21-157">您可以啟用 **echoContent** 來達成目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6e21-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="a6e21-158">更新實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-158">Update an entity</span></span>
<span data-ttu-id="a6e21-159">有多個方法可用 tooupdate 現有的實體：</span><span class="sxs-lookup"><span data-stu-id="a6e21-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="a6e21-160">**replaceEntity** - 藉由取代來更新現有實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="a6e21-161">**mergeEntity** -將新的屬性值合併為 hello 現有實體，以更新現有的實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="a6e21-162">**insertOrReplaceEntity** - 藉由取代來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="a6e21-163">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="a6e21-164">**insertOrMergeEntity** -更新現有的實體合併到現有的 hello 的新屬性值。</span><span class="sxs-lookup"><span data-stu-id="a6e21-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="a6e21-165">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="a6e21-166">hello 下列範例示範如何更新實體使用**replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="a6e21-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="a6e21-167">根據預設，更新實體不會檢查 toosee 如果 hello 資料正在更新先前已修改另一個處理序。</span><span class="sxs-lookup"><span data-stu-id="a6e21-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="a6e21-168">toosupport 並行更新：</span><span class="sxs-lookup"><span data-stu-id="a6e21-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="a6e21-169">收到 hello hello 物件正在更新的 ETag。</span><span class="sxs-lookup"><span data-stu-id="a6e21-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="a6e21-170">這傳回的 hello`response`的任何實體相關的作業，而且可以透過擷取`response['.metadata'].etag`。</span><span class="sxs-lookup"><span data-stu-id="a6e21-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="a6e21-171">當執行實體上的更新作業，會加入先前擷取 hello ETag 資訊 toohello 新實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="a6e21-172">例如：</span><span class="sxs-lookup"><span data-stu-id="a6e21-172">For example:</span></span>
>
>       <span data-ttu-id="a6e21-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="a6e21-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="a6e21-174">執行 hello 更新作業。</span><span class="sxs-lookup"><span data-stu-id="a6e21-174">Perform hello update operation.</span></span> <span data-ttu-id="a6e21-175">如果您擷取 hello ETag 值，例如應用程式的另一個執行個體之後，已被修改 hello 實體`error`將會傳回指出 hello 要求中指定的 hello 更新條件不符合。</span><span class="sxs-lookup"><span data-stu-id="a6e21-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="a6e21-176">與**replaceEntity**和**mergeEntity**，如果正在更新的 hello 實體不存在，hello 更新作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a6e21-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="a6e21-177">如果您想 toostore 不論是否已經存在的實體，因此使用**insertOrReplaceEntity**或**insertOrMergeEntity**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="a6e21-178">hello`result`成功的更新作業將會包含 hello **Etag** hello 更新實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="a6e21-179">使用實體群組</span><span class="sxs-lookup"><span data-stu-id="a6e21-179">Work with groups of entities</span></span>
<span data-ttu-id="a6e21-180">有時它可讓意義 toosubmit 多個作業一起批次 tooensure 中不可部分完成 hello 伺服器所處理。</span><span class="sxs-lookup"><span data-stu-id="a6e21-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="a6e21-181">可使用 hello tooaccomplish **TableBatch**類別 toocreate 批次中，然後使用 hello **executeBatch**方法**TableService** tooperform hello 批次作業。</span><span class="sxs-lookup"><span data-stu-id="a6e21-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="a6e21-182">下列範例中的 hello 示範提交批次中的兩個實體：</span><span class="sxs-lookup"><span data-stu-id="a6e21-182">hello following example demonstrates submitting two entities in a batch:</span></span>

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

<span data-ttu-id="a6e21-183">成功的批次作業`result`會包含 hello 批次中每個作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e21-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="a6e21-184">處理批次作業</span><span class="sxs-lookup"><span data-stu-id="a6e21-184">Work with batched operations</span></span>
<span data-ttu-id="a6e21-185">新增作業可以由檢視 hello 檢查 tooa 批次`operations`屬性。</span><span class="sxs-lookup"><span data-stu-id="a6e21-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="a6e21-186">您也可以使用下列方法 toowork 與作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6e21-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="a6e21-187">**clear** - 清除批次中的所有操作</span><span class="sxs-lookup"><span data-stu-id="a6e21-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="a6e21-188">**getOperations** -取得作業從 hello 批次</span><span class="sxs-lookup"><span data-stu-id="a6e21-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="a6e21-189">**hasOperations** -如果 hello 批次包含作業會傳回 true</span><span class="sxs-lookup"><span data-stu-id="a6e21-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="a6e21-190">**removeOperations** - 移除操作</span><span class="sxs-lookup"><span data-stu-id="a6e21-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="a6e21-191">**大小**-傳回 hello hello 批次中的作業數目</span><span class="sxs-lookup"><span data-stu-id="a6e21-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="a6e21-192">依索引鍵擷取實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-192">Retrieve an entity by key</span></span>
<span data-ttu-id="a6e21-193">特定實體根據 hello tooreturn **PartitionKey**和**RowKey**，使用 hello **retrieveEntity**方法。</span><span class="sxs-lookup"><span data-stu-id="a6e21-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="a6e21-194">這項作業完成之後，`result`將包含 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="a6e21-195">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="a6e21-195">Query a set of entities</span></span>
<span data-ttu-id="a6e21-196">tooquery 資料表時，使用 hello **TableQuery**物件 toobuild 向上查詢運算式，使用下列子句 hello:</span><span class="sxs-lookup"><span data-stu-id="a6e21-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="a6e21-197">**選取**-hello 欄位 toobe 查詢所傳回的 hello</span><span class="sxs-lookup"><span data-stu-id="a6e21-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="a6e21-198">**其中**-hello 其中子句</span><span class="sxs-lookup"><span data-stu-id="a6e21-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="a6e21-199">**and** - `and` where 條件</span><span class="sxs-lookup"><span data-stu-id="a6e21-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="a6e21-200">**or** - `or` where 條件</span><span class="sxs-lookup"><span data-stu-id="a6e21-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="a6e21-201">**top** -hello toofetch 項目數目</span><span class="sxs-lookup"><span data-stu-id="a6e21-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="a6e21-202">hello 下列範例建立一個查詢會傳回前五個項目與 PartitionKey 的 'hometasks' hello。</span><span class="sxs-lookup"><span data-stu-id="a6e21-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="a6e21-203">因為沒有使用 **select** ，所以會傳回所有欄位。</span><span class="sxs-lookup"><span data-stu-id="a6e21-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="a6e21-204">針對每個資料表，使用 tooperform hello 查詢**queryEntities**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="a6e21-205">hello 下列範例會使用 'mytable' 來自這個查詢 tooreturn 實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="a6e21-206">如果成功的話，`result.entries`會包含符合 hello 查詢的實體的陣列。</span><span class="sxs-lookup"><span data-stu-id="a6e21-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="a6e21-207">如果無法 tooreturn hello 查詢所有實體，`result.continuationToken`將非*null* ，可以用來當做 hello 第三個參數**queryEntities** tooretrieve 取得更多結果。</span><span class="sxs-lookup"><span data-stu-id="a6e21-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="a6e21-208">Hello 初始查詢中，使用*null* hello 第三個參數。</span><span class="sxs-lookup"><span data-stu-id="a6e21-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="a6e21-209">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="a6e21-209">Query a subset of entity properties</span></span>
<span data-ttu-id="a6e21-210">查詢 tooa 資料表可以從實體擷取幾個欄位。</span><span class="sxs-lookup"><span data-stu-id="a6e21-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="a6e21-211">這可以減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="a6e21-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="a6e21-212">使用 hello**選取**hello 欄位 toobe 子句和傳遞 hello 名稱傳回。</span><span class="sxs-lookup"><span data-stu-id="a6e21-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="a6e21-213">例如，hello 下列查詢會傳回只 hello**描述**和**dueDate**欄位。</span><span class="sxs-lookup"><span data-stu-id="a6e21-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="a6e21-214">刪除實體</span><span class="sxs-lookup"><span data-stu-id="a6e21-214">Delete an entity</span></span>
<span data-ttu-id="a6e21-215">您可以使用實體的資料分割和資料列索引鍵來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a6e21-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="a6e21-216">在此範例中，hello **task1**物件包含 hello **RowKey**和**PartitionKey** hello 實體 toobe 刪除的值。</span><span class="sxs-lookup"><span data-stu-id="a6e21-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="a6e21-217">然後 hello 物件會傳遞 toohello **deleteEntity**方法。</span><span class="sxs-lookup"><span data-stu-id="a6e21-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

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
> <span data-ttu-id="a6e21-218">請考慮刪除項目，項目 hello 的 tooensure 尚未由其他處理序修改時使用的 Etag。</span><span class="sxs-lookup"><span data-stu-id="a6e21-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="a6e21-219">請參閱 [更新實體](#update-an-entity) ，以取得使用 ETag 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e21-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="a6e21-220">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="a6e21-220">Delete a table</span></span>
<span data-ttu-id="a6e21-221">下列程式碼的 hello 從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="a6e21-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="a6e21-222">如果您不確定 hello 資料表是否存在，請使用**deleteTableIfExists**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="a6e21-223">使用接續 Token</span><span class="sxs-lookup"><span data-stu-id="a6e21-223">Use continuation tokens</span></span>
<span data-ttu-id="a6e21-224">當您查詢大量結果的資料表時，請尋找接續 Token。</span><span class="sxs-lookup"><span data-stu-id="a6e21-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="a6e21-225">可能有大量的資料可供您可能不知道是否您不要建置 toorecognize 接續 token 存在時的查詢。</span><span class="sxs-lookup"><span data-stu-id="a6e21-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="a6e21-226">hello 結果物件期間查詢的實體集傳回`continuationToken`語彙基元時存在的屬性。</span><span class="sxs-lookup"><span data-stu-id="a6e21-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="a6e21-227">您可以再使用此跨 hello 資料分割和資料表實體執行查詢 toocontinue toomove 時。</span><span class="sxs-lookup"><span data-stu-id="a6e21-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="a6e21-228">在查詢時，可能會 hello 查詢物件執行個體與 hello 回呼函式之間提供 continuationToken 參數：</span><span class="sxs-lookup"><span data-stu-id="a6e21-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

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

<span data-ttu-id="a6e21-229">如果您檢查 hello`continuationToken`物件，您會發現屬性例如`nextPartitionKey`，`nextRowKey`和`targetLocation`，可能會使用的 tooiterate 透過 hello 的所有結果。</span><span class="sxs-lookup"><span data-stu-id="a6e21-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="a6e21-230">另外還有 hello GitHub 上的 Azure 儲存體 Node.js 儲存機制內的接續範例。</span><span class="sxs-lookup"><span data-stu-id="a6e21-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="a6e21-231">尋找 `examples/samples/continuationsample.js`。</span><span class="sxs-lookup"><span data-stu-id="a6e21-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="a6e21-232">使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="a6e21-232">Work with shared access signatures</span></span>
<span data-ttu-id="a6e21-233">共用的存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tootables，但未提供您的儲存體帳戶名稱或索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a6e21-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="a6e21-234">SAS 通常是使用的 tooprovide 有限存取 tooyour 資料，例如 tooquery 記錄允許行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6e21-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="a6e21-235">信任的應用程式，例如雲端服務會產生 SAS 使用 hello **generateSharedAccessSignature**的 hello **TableService**，然後將其提供 tooan 不受信任或非完全信任的應用程式例如，行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6e21-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="a6e21-236">hello SAS 會產生使用原則描述 hello 開始和結束日期的 hello 期間 SAS 有效，以及 hello 存取層級授與的 toohello SAS 持有者。</span><span class="sxs-lookup"><span data-stu-id="a6e21-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="a6e21-237">hello 下列範例會產生新的共用的存取原則，可讓 SAS 持有者 ('r') tooquery hello 資料表 hello 與到期之後建立的 hello 時 100 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a6e21-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="a6e21-238">請注意 hello 主機資訊必須提供此外，視需要當 hello SAS 持有者嘗試 tooaccess hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="a6e21-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="a6e21-239">hello 用戶端應用程式，然後使用 hello 與 SAS **TableServiceWithSAS** tooperform hello 資料表作業。</span><span class="sxs-lookup"><span data-stu-id="a6e21-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="a6e21-240">下列範例中的 hello 連接 toohello 資料表，並執行查詢。</span><span class="sxs-lookup"><span data-stu-id="a6e21-240">hello following example connects toohello table and performs a query.</span></span>

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

<span data-ttu-id="a6e21-241">Hello SAS 產生後有只查詢存取，嘗試進行 tooinsert 更新或刪除實體，則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="a6e21-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="a6e21-242">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="a6e21-242">Access Control Lists</span></span>
<span data-ttu-id="a6e21-243">您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。</span><span class="sxs-lookup"><span data-stu-id="a6e21-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="a6e21-244">如果您想 tooallow 多個用戶端 tooaccess hello 資料表，但每個用戶端提供不同的存取原則，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="a6e21-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="a6e21-245">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a6e21-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="a6e21-246">hello 下列範例會定義兩個原則，一個用於 'user1'，'user2' 其中一個：</span><span class="sxs-lookup"><span data-stu-id="a6e21-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="a6e21-247">下列範例取得 hello hello hello 的目前 ACL **hometasks**資料表，並將 hello 新原則使用**setTableAcl**。</span><span class="sxs-lookup"><span data-stu-id="a6e21-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="a6e21-248">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="a6e21-248">This approach allows:</span></span>

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

<span data-ttu-id="a6e21-249">一次 hello 已設定 ACL，然後您可以建立根據 hello 識別碼原則 SAS。</span><span class="sxs-lookup"><span data-stu-id="a6e21-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="a6e21-250">hello 下列範例會建立新的 SAS 'user2':</span><span class="sxs-lookup"><span data-stu-id="a6e21-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="a6e21-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6e21-251">Next steps</span></span>
<span data-ttu-id="a6e21-252">如需詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="a6e21-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="a6e21-253">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="a6e21-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="a6e21-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a6e21-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="a6e21-255">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="a6e21-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="a6e21-256">建立及部署 Node.js 應用程式 tooan Azure 網站</span><span class="sxs-lookup"><span data-stu-id="a6e21-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
