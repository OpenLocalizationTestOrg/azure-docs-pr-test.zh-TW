---
title: "如何使用 Node.js 中的 Azure 資料表儲存體 | Microsoft Docs"
description: "使用 Azure 表格儲存體 (NoSQL 資料存放區) 將結構化的資料儲存在雲端。"
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
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="5343d-103">如何使用 Node.js 的 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="5343d-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="5343d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5343d-104">Overview</span></span>
<span data-ttu-id="5343d-105">本主題示範如何使用 Node.js 應用程式中的 Azure 表格服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="5343d-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="5343d-106">本主題中的程式碼範例假設您已經有 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5343d-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="5343d-107">如需如何在 Azure 中建立 Node.js 應用程式的資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="5343d-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="5343d-108">在 Azure App Service 中建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5343d-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="5343d-109">使用 WebMatrix 來建立 Node.js Web 應用程式並部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="5343d-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="5343d-110">[建置 Node.js 應用程式並部署到 Azure 雲端服務](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (使用 Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5343d-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="5343d-111">設定您的應用程式以存取 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5343d-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="5343d-112">若要使用 Azure 儲存體，您需要 Azure Storage SDK for Node.js，這包含一組便利程式庫，能與儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="5343d-113">使用 Node Package Manager (NPM) 安裝封裝</span><span class="sxs-lookup"><span data-stu-id="5343d-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="5343d-114">使用命令列介面，例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Unix)，瀏覽至儲存所建立應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5343d-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="5343d-115">在命令視窗中輸入 **npm install azure-storage** 。</span><span class="sxs-lookup"><span data-stu-id="5343d-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="5343d-116">此命令的輸出類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="5343d-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="5343d-117">您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5343d-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="5343d-118">該資料夾中有 **azure-storage** 封裝，當中包含存取儲存體所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="5343d-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="5343d-119">匯入封裝</span><span class="sxs-lookup"><span data-stu-id="5343d-119">Import the package</span></span>
<span data-ttu-id="5343d-120">將下列程式碼加在應用程式中的 **server.js** 檔案之上：</span><span class="sxs-lookup"><span data-stu-id="5343d-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5343d-121">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="5343d-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="5343d-122">azure 模組會讀取環境變數 AZURE\_STORAGE\_ACCOUNT 和 AZURE\_STORAGE\_ACCESS\_KEY，或 AZURE\_STORAGE\_CONNECTION\_STRING，以取得連接 Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="5343d-123">如果未設定這些環境變數，則呼叫 **TableService**時必須指定帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="5343d-124">如需針對 Azure 網站在 [Azure 入口網站](https://portal.azure.com)中設定環境變數的範例，請參閱[使用 Azure 表格服務的 Node.js Web 應用程式](../app-service-web/storage-nodejs-use-table-storage-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="5343d-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="5343d-125">建立資料表</span><span class="sxs-lookup"><span data-stu-id="5343d-125">Create a table</span></span>
<span data-ttu-id="5343d-126">下列程式碼會建立 **TableService** 物件，並使用該物件建立新資料表。</span><span class="sxs-lookup"><span data-stu-id="5343d-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="5343d-127">將下列內容新增至接近 **server.js**的頂端。</span><span class="sxs-lookup"><span data-stu-id="5343d-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="5343d-128">呼叫 **createTableIfNotExists** 會以指定的名稱建立新的資料表 (若尚未建立)。</span><span class="sxs-lookup"><span data-stu-id="5343d-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="5343d-129">如果名為 'mytable' 的資料表尚不存在，下列範例便會建立這個新資料表：</span><span class="sxs-lookup"><span data-stu-id="5343d-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="5343d-130">如果建立新資料表，`result.created` 將是 `true`，如果資料表已存在，則為 `false`。</span><span class="sxs-lookup"><span data-stu-id="5343d-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="5343d-131">`response` 會包含要求的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="5343d-132">篩選器</span><span class="sxs-lookup"><span data-stu-id="5343d-132">Filters</span></span>
<span data-ttu-id="5343d-133">可以將選用性的篩選操作套用到使用 **TableService** 執行的操作。</span><span class="sxs-lookup"><span data-stu-id="5343d-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="5343d-134">篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：</span><span class="sxs-lookup"><span data-stu-id="5343d-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="5343d-135">在對要求選項進行前處理之後，方法需要呼叫 "next" 並傳遞具有下列簽章的回呼：</span><span class="sxs-lookup"><span data-stu-id="5343d-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="5343d-136">在此回呼中，以及處理 returnObject (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是就改為叫用 finalCallback 結束服務叫用。</span><span class="sxs-lookup"><span data-stu-id="5343d-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="5343d-137">Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="5343d-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="5343d-138">以下會建立使用 **ExponentialRetryPolicyFilter** 的 **TableService** 物件：</span><span class="sxs-lookup"><span data-stu-id="5343d-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="5343d-139">將實體加入至資料表</span><span class="sxs-lookup"><span data-stu-id="5343d-139">Add an entity to a table</span></span>
<span data-ttu-id="5343d-140">若要新增實體，請先建立一個定義實體屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="5343d-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="5343d-141">所有實體必須包含 **PartitionKey** 和 **RowKey**，這些是實體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="5343d-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="5343d-142">**PartitionKey** - 決定儲存實體的資料分割。</span><span class="sxs-lookup"><span data-stu-id="5343d-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="5343d-143">**RowKey** - 在資料分割內唯一地識別實體</span><span class="sxs-lookup"><span data-stu-id="5343d-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="5343d-144">**PartitionKey** 和 **RowKey** 都必須是字串值。</span><span class="sxs-lookup"><span data-stu-id="5343d-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="5343d-145">如需詳細資訊，請參閱 [了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5343d-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="5343d-146">以下是定義實體的範例。</span><span class="sxs-lookup"><span data-stu-id="5343d-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="5343d-147">請注意，**dueDate** 定義為 **Edm.DateTime** 類型。</span><span class="sxs-lookup"><span data-stu-id="5343d-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="5343d-148">可選擇是否指定型別，若未指定，則會推斷型別。</span><span class="sxs-lookup"><span data-stu-id="5343d-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="5343d-149">每筆記錄還有 [時間戳記] 欄位，插入或更新實體時，Azure 會設定此欄位。</span><span class="sxs-lookup"><span data-stu-id="5343d-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="5343d-150">您也可以使用 **entityGenerator** 來建立實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="5343d-151">下列範例使用 **entityGenerator**建立相同的工作實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="5343d-152">若要將實體新增至資料表，請將實體物件傳給 **insertEntity** 方法。</span><span class="sxs-lookup"><span data-stu-id="5343d-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="5343d-153">若作業成功，`result` 會包含已插入記錄的 [ETag](http://en.wikipedia.org/wiki/HTTP_ETag)，`response` 則會包含作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="5343d-154">範例回應：</span><span class="sxs-lookup"><span data-stu-id="5343d-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="5343d-155">根據預設，**insertEntity** 不會將已插入的實體包含在 `response` 資訊中傳回。</span><span class="sxs-lookup"><span data-stu-id="5343d-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="5343d-156">若您打算對此實體執行其他作業，或想要快取資訊，將此實體包含在 `result`中傳回會是個不錯的方式。</span><span class="sxs-lookup"><span data-stu-id="5343d-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="5343d-157">您可以啟用 **echoContent** 來達成目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5343d-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="5343d-158">更新實體</span><span class="sxs-lookup"><span data-stu-id="5343d-158">Update an entity</span></span>
<span data-ttu-id="5343d-159">有多種方法可以用來更新現有的實體：</span><span class="sxs-lookup"><span data-stu-id="5343d-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="5343d-160">**replaceEntity** - 藉由取代來更新現有實體</span><span class="sxs-lookup"><span data-stu-id="5343d-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="5343d-161">**mergeEntity** - 藉由將新的屬性值合併到現有實體來更新現有實體</span><span class="sxs-lookup"><span data-stu-id="5343d-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="5343d-162">**insertOrReplaceEntity** - 藉由取代來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="5343d-163">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="5343d-164">**insertOrMergeEntity** - 藉由將新的屬性值合併到現有實體來更新現有實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="5343d-165">如果實體不存在，將會插入新的實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="5343d-166">下列範例示範使用 **replaceEntity**來更新實體：</span><span class="sxs-lookup"><span data-stu-id="5343d-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="5343d-167">依預設，更新實體並不會檢查正在更新的資料先前是否被另一個程序修改過。</span><span class="sxs-lookup"><span data-stu-id="5343d-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="5343d-168">若要支援並行更新：</span><span class="sxs-lookup"><span data-stu-id="5343d-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="5343d-169">取得正在更新之物件的 ETag。</span><span class="sxs-lookup"><span data-stu-id="5343d-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="5343d-170">系統會針對實體相關的作業將 ETag 包含在 `response` 中傳回，且可透過 `response['.metadata'].etag` 擷取 ETag。</span><span class="sxs-lookup"><span data-stu-id="5343d-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="5343d-171">對實體執行更新操作時，請將先前擷取的 ETag 資訊新增至新的實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="5343d-172">例如：</span><span class="sxs-lookup"><span data-stu-id="5343d-172">For example:</span></span>
>
>       <span data-ttu-id="5343d-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="5343d-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="5343d-174">執行更新操作。</span><span class="sxs-lookup"><span data-stu-id="5343d-174">Perform the update operation.</span></span> <span data-ttu-id="5343d-175">如果擷取 ETag 值之後，實體 (例如您應用程式的其他執行個體) 進行了修改，系統會傳回 `error` ，表示不符合要求中指定的更新條件。</span><span class="sxs-lookup"><span data-stu-id="5343d-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="5343d-176">使用 **replaceEntity** 和 **mergeEntity** 時，如果正在更新的實體不存在，則更新作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="5343d-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="5343d-177">因此，如果您要儲存一個實體，而不管它是否已存在，您應該改用 **insertOrReplaceEntity** 或 **insertOrMergeEntity**。</span><span class="sxs-lookup"><span data-stu-id="5343d-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="5343d-178">更新作業成功的 `result` 將包含已更新實體的 **Etag** 。</span><span class="sxs-lookup"><span data-stu-id="5343d-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="5343d-179">使用實體群組</span><span class="sxs-lookup"><span data-stu-id="5343d-179">Work with groups of entities</span></span>
<span data-ttu-id="5343d-180">有時候批次提交多個操作是有意義的，可以確保伺服器會進行不可部分完成的處理。</span><span class="sxs-lookup"><span data-stu-id="5343d-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="5343d-181">若要達到此目的，請使用 **TableBatch** 類別建立批次，然後使用 **TableService** 的 **executeBatch** 方法執行批次作業。</span><span class="sxs-lookup"><span data-stu-id="5343d-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="5343d-182">下列範例示範在批次中提交兩個實體：</span><span class="sxs-lookup"><span data-stu-id="5343d-182">The following example demonstrates submitting two entities in a batch:</span></span>

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

<span data-ttu-id="5343d-183">成功的批次作業的 `result` 將包含批次中每個作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="5343d-184">處理批次作業</span><span class="sxs-lookup"><span data-stu-id="5343d-184">Work with batched operations</span></span>
<span data-ttu-id="5343d-185">若要檢查新增至批次的操作，您可以檢視 `operations` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5343d-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="5343d-186">您也可以使用下列方法來處理操作：</span><span class="sxs-lookup"><span data-stu-id="5343d-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="5343d-187">**clear** - 清除批次中的所有操作</span><span class="sxs-lookup"><span data-stu-id="5343d-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="5343d-188">**getOperations** - 從批次取得操作</span><span class="sxs-lookup"><span data-stu-id="5343d-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="5343d-189">**hasOperations** - 若批次包含操作，則傳回 true</span><span class="sxs-lookup"><span data-stu-id="5343d-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="5343d-190">**removeOperations** - 移除操作</span><span class="sxs-lookup"><span data-stu-id="5343d-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="5343d-191">**size** - 傳回批次中的操作數目</span><span class="sxs-lookup"><span data-stu-id="5343d-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="5343d-192">依索引鍵擷取實體</span><span class="sxs-lookup"><span data-stu-id="5343d-192">Retrieve an entity by key</span></span>
<span data-ttu-id="5343d-193">若要根據 **PartitionKey** 和 **RowKey** 傳回特定的實體，請使用 **retrieveEntity** 方法。</span><span class="sxs-lookup"><span data-stu-id="5343d-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="5343d-194">此作業完成時， `result` 將包含實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="5343d-195">查詢實體集合</span><span class="sxs-lookup"><span data-stu-id="5343d-195">Query a set of entities</span></span>
<span data-ttu-id="5343d-196">若要查詢資料表，請透過 **TableQuery** 物件使用下列子句建置查詢運算式：</span><span class="sxs-lookup"><span data-stu-id="5343d-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="5343d-197">**select** - 要從查詢傳回的欄位</span><span class="sxs-lookup"><span data-stu-id="5343d-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="5343d-198">**where** - where 子句</span><span class="sxs-lookup"><span data-stu-id="5343d-198">**where** - the where clause</span></span>

  * <span data-ttu-id="5343d-199">**and** - `and` where 條件</span><span class="sxs-lookup"><span data-stu-id="5343d-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="5343d-200">**or** - `or` where 條件</span><span class="sxs-lookup"><span data-stu-id="5343d-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="5343d-201">**top** - 要提取的項目數</span><span class="sxs-lookup"><span data-stu-id="5343d-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="5343d-202">下列範例建立的查詢會傳回 PartitionKey 為 'hometasks' 的前 5 個項目。</span><span class="sxs-lookup"><span data-stu-id="5343d-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="5343d-203">因為沒有使用 **select** ，所以會傳回所有欄位。</span><span class="sxs-lookup"><span data-stu-id="5343d-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="5343d-204">若要對資料表執行查詢，請使用 **queryEntities**。</span><span class="sxs-lookup"><span data-stu-id="5343d-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="5343d-205">下列範例使用此查詢從 'mytable' 傳回實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="5343d-206">如果作業成功， `result.entries` 將包含符合查詢的實體陣列。</span><span class="sxs-lookup"><span data-stu-id="5343d-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="5343d-207">若查詢無法傳回所有實體，則 `result.continuationToken` 將為非*Null* ，並且可作為 **queryEntities** 的第三個參數來擷取更多結果。</span><span class="sxs-lookup"><span data-stu-id="5343d-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="5343d-208">在初始查詢中，第三個參數請使用 *null* 。</span><span class="sxs-lookup"><span data-stu-id="5343d-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="5343d-209">查詢實體屬性的子集</span><span class="sxs-lookup"><span data-stu-id="5343d-209">Query a subset of entity properties</span></span>
<span data-ttu-id="5343d-210">一項資料表查詢可以只擷取實體的少數欄位。</span><span class="sxs-lookup"><span data-stu-id="5343d-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="5343d-211">這可以減少頻寬並提高查詢效能 (尤其是對大型實體而言)。</span><span class="sxs-lookup"><span data-stu-id="5343d-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="5343d-212">請使用 **select** 子句並傳遞要傳回的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="5343d-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="5343d-213">例如，下列查詢只會傳回 **description** 和 **dueDate** 欄位。</span><span class="sxs-lookup"><span data-stu-id="5343d-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="5343d-214">刪除實體</span><span class="sxs-lookup"><span data-stu-id="5343d-214">Delete an entity</span></span>
<span data-ttu-id="5343d-215">您可以使用實體的資料分割和資料列索引鍵來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="5343d-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="5343d-216">在本例中，**task1** 物件包含待刪除實體的 **RowKey** 及 **PartitionKey** 值。</span><span class="sxs-lookup"><span data-stu-id="5343d-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="5343d-217">然後物件會傳給 **deleteEntity** 方法。</span><span class="sxs-lookup"><span data-stu-id="5343d-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="5343d-218">刪除項目時應該考慮使用 ETag，以確保項目未被另一個程序修改過。</span><span class="sxs-lookup"><span data-stu-id="5343d-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="5343d-219">請參閱 [更新實體](#update-an-entity) ，以取得使用 ETag 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="5343d-220">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="5343d-220">Delete a table</span></span>
<span data-ttu-id="5343d-221">下列程式碼會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="5343d-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="5343d-222">若不確定資料表是否存在，請使用 **deleteTableIfExists**。</span><span class="sxs-lookup"><span data-stu-id="5343d-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="5343d-223">使用接續 Token</span><span class="sxs-lookup"><span data-stu-id="5343d-223">Use continuation tokens</span></span>
<span data-ttu-id="5343d-224">當您查詢大量結果的資料表時，請尋找接續 Token。</span><span class="sxs-lookup"><span data-stu-id="5343d-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="5343d-225">因為您的查詢可能會產生大量可用的資料，如果該查詢並非可識別接續權杖存在的查詢，可能會無法得知。</span><span class="sxs-lookup"><span data-stu-id="5343d-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="5343d-226">當此類權杖存在時，在查詢實體設定 `continuationToken` 屬性期間，系統便會傳回結果物件。</span><span class="sxs-lookup"><span data-stu-id="5343d-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="5343d-227">您可以在執行查詢使用此方法以繼續在分割和資料表實體之間移動。</span><span class="sxs-lookup"><span data-stu-id="5343d-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="5343d-228">查詢時，系統可能會將 continuationToken 參數放在查詢物件執行個體和回呼函數之間：</span><span class="sxs-lookup"><span data-stu-id="5343d-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="5343d-229">如果您檢查 `continuationToken` 物件，您會找到像是 `nextPartitionKey`、`nextRowKey` 和 `targetLocation` 的屬性，這些屬性可以用來逐一查看所有結果。</span><span class="sxs-lookup"><span data-stu-id="5343d-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="5343d-230">GitHub 上的 Azure 儲存體 Node.js 儲存機制中也有接續範例。</span><span class="sxs-lookup"><span data-stu-id="5343d-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="5343d-231">尋找 `examples/samples/continuationsample.js`。</span><span class="sxs-lookup"><span data-stu-id="5343d-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="5343d-232">使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="5343d-232">Work with shared access signatures</span></span>
<span data-ttu-id="5343d-233">共用存取簽章 (SAS) 可安全地提供對資料表的精確存取，而不必提供您的儲存體帳戶名稱或金鑰。</span><span class="sxs-lookup"><span data-stu-id="5343d-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="5343d-234">SAS 通常用來提供對資料的有限存取，例如允許行動應用程式查詢記錄。</span><span class="sxs-lookup"><span data-stu-id="5343d-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="5343d-235">信任的應用程式 (例如雲端型服務) 會使用 **TableService** 的 **generateSharedAccessSignature** 來產生 SAS，並提供它給不信任或不完全信任的應用程式 (例如行動應用程式)。</span><span class="sxs-lookup"><span data-stu-id="5343d-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="5343d-236">SAS 是使用原則來產生，該原則描述 SAS 有效期間的開始和結束日期，以及授與 SAS 持有者的存取等級。</span><span class="sxs-lookup"><span data-stu-id="5343d-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="5343d-237">下列範例會產生新的共用存取原則，讓 SAS 持有者查詢 ('r') 資料表，並於建立它之後的 100 分鐘過期。</span><span class="sxs-lookup"><span data-stu-id="5343d-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="5343d-238">請注意，也必須提供主機資訊，因為 SAS 持有者嘗試存取資料表時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="5343d-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="5343d-239">用戶端應用程式接著以 **TableServiceWithSAS** 來使用 SAS，對資料表執行操作。</span><span class="sxs-lookup"><span data-stu-id="5343d-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="5343d-240">下列範例會連線到資料表並執行查詢。</span><span class="sxs-lookup"><span data-stu-id="5343d-240">The following example connects to the table and performs a query.</span></span>

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

<span data-ttu-id="5343d-241">因為產生的 SAS 只有查詢權限，若嘗試插入、更新或刪除實體，則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="5343d-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="5343d-242">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="5343d-242">Access Control Lists</span></span>
<span data-ttu-id="5343d-243">您也可以使用存取控制清單 (ACL) 來設定 SAS 的存取原則。</span><span class="sxs-lookup"><span data-stu-id="5343d-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="5343d-244">若您要允許用戶端存取資料表，但對每個用戶端提供不同的存取原則，則這會很有用。</span><span class="sxs-lookup"><span data-stu-id="5343d-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="5343d-245">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5343d-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="5343d-246">下列範例定義兩個原則，其中一個用於 'user1'，另一個用於 'user2'：</span><span class="sxs-lookup"><span data-stu-id="5343d-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="5343d-247">下列範例會取得 **hometasks**資料表的目前 ACL，然後使用 **setTableAcl** 來加入新的原則。</span><span class="sxs-lookup"><span data-stu-id="5343d-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="5343d-248">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="5343d-248">This approach allows:</span></span>

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

<span data-ttu-id="5343d-249">設定 ACL 之後，您可以根據原則的識別碼來建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="5343d-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="5343d-250">下列範例會建立 'user2' 的新 SAS：</span><span class="sxs-lookup"><span data-stu-id="5343d-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="5343d-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5343d-251">Next steps</span></span>
<span data-ttu-id="5343d-252">如需詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="5343d-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="5343d-253">[Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="5343d-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="5343d-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5343d-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="5343d-255">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="5343d-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="5343d-256">建立 Node.js 應用程式並部署到 Azure 網站</span><span class="sxs-lookup"><span data-stu-id="5343d-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)