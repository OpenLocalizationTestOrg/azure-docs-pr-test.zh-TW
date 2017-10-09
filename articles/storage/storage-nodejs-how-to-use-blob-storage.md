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
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="95fb1-103">如何 toouse Node.js 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="95fb1-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="95fb1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="95fb1-104">Overview</span></span>
<span data-ttu-id="95fb1-105">本文章將示範如何使用 Blob 儲存體 tooperform 常見案例。</span><span class="sxs-lookup"><span data-stu-id="95fb1-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="95fb1-106">透過 hello Node.js 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="95fb1-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="95fb1-107">涵蓋的 hello 案例包括 tooupload，列出、 下載及刪除 blob 的方式。</span><span class="sxs-lookup"><span data-stu-id="95fb1-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="95fb1-108">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="95fb1-108">Create a Node.js application</span></span>
<span data-ttu-id="95fb1-109">如需有關指示 toocreate Node.js 應用程式，請參閱[Node.js web 應用程式建立 Azure App Service 中]，[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan] -使用 Windows PowerShell或[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]。</span><span class="sxs-lookup"><span data-stu-id="95fb1-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="95fb1-110">設定您的應用程式 tooaccess 儲存體</span><span class="sxs-lookup"><span data-stu-id="95fb1-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="95fb1-111">toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="95fb1-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="95fb1-112">使用節點封裝管理員 (NPM) tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="95fb1-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="95fb1-113">使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Unix)，您用來建立您的範例 toonavigate toohello 資料夾應用程式。</span><span class="sxs-lookup"><span data-stu-id="95fb1-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="95fb1-114">型別**npm 安裝 azure 儲存體**hello 命令視窗中。</span><span class="sxs-lookup"><span data-stu-id="95fb1-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="95fb1-115">Hello 命令的輸出會類似下列程式碼範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="95fb1-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="95fb1-116">您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="95fb1-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="95fb1-117">在該資料夾中，找出 hello **azure 儲存體**套件，其中包含需要 tooaccess 儲存體的 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="95fb1-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="95fb1-118">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="95fb1-118">Import hello package</span></span>
<span data-ttu-id="95fb1-119">使用 [記事本] 或其他文字編輯器，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案，但您想 toouse 儲存體：</span><span class="sxs-lookup"><span data-stu-id="95fb1-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="95fb1-120">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="95fb1-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="95fb1-121">hello Azure 模組會讀取 hello 環境變數`AZURE_STORAGE_ACCOUNT`和`AZURE_STORAGE_ACCESS_KEY`，或`AZURE_STORAGE_CONNECTION_STRING`，資訊所需 tooconnect tooyour Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="95fb1-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="95fb1-122">如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**createBlobService**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="95fb1-123">如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure web 應用程式中，請參閱[Node.js web 應用程式使用 hello Azure 資料表服務]。</span><span class="sxs-lookup"><span data-stu-id="95fb1-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="95fb1-124">建立容器</span><span class="sxs-lookup"><span data-stu-id="95fb1-124">Create a container</span></span>
<span data-ttu-id="95fb1-125">hello **BlobService**物件可讓您使用容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="95fb1-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="95fb1-126">hello 下列程式碼會建立**BlobService**物件。</span><span class="sxs-lookup"><span data-stu-id="95fb1-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="95fb1-127">新增 hello 頂端附近的 hello 下列**立即轉譯 server.js**:</span><span class="sxs-lookup"><span data-stu-id="95fb1-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="95fb1-128">您可以使用匿名存取 blob **createBlobServiceAnonymous**並提供 hello 主機位址。</span><span class="sxs-lookup"><span data-stu-id="95fb1-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="95fb1-129">例如，使用 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`。</span><span class="sxs-lookup"><span data-stu-id="95fb1-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="95fb1-130">使用新的容器，toocreate **createContainerIfNotExists**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="95fb1-131">hello 下列程式碼範例會建立名為 'mycontainer' 的新容器：</span><span class="sxs-lookup"><span data-stu-id="95fb1-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="95fb1-132">如果剛新建 hello 容器，`result.created`為 true。</span><span class="sxs-lookup"><span data-stu-id="95fb1-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="95fb1-133">如果 hello 容器已經存在，`result.created`為 false。</span><span class="sxs-lookup"><span data-stu-id="95fb1-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="95fb1-134">`response`包含 hello 作業，包括 hello hello 容器的 ETag 資訊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="95fb1-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="95fb1-135">容器安全性</span><span class="sxs-lookup"><span data-stu-id="95fb1-135">Container security</span></span>
<span data-ttu-id="95fb1-136">依預設，新的容器屬私人性質，無法以匿名方式存取。</span><span class="sxs-lookup"><span data-stu-id="95fb1-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="95fb1-137">toomake hello 容器公用，以供匿名存取，您可以設定 hello 容器的存取層級太**blob**或**容器**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="95fb1-138">**blob** -匿名讀取權限 tooblob 內容和中繼資料內這個容器中，但不 toocontainer 中繼資料，例如列出容器內的所有 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="95fb1-139">**容器**-可讓匿名讀取權限 tooblob 內容和中繼資料，以及容器中繼資料</span><span class="sxs-lookup"><span data-stu-id="95fb1-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="95fb1-140">hello 下列程式碼範例示範設定 hello 存取層級太**blob**:</span><span class="sxs-lookup"><span data-stu-id="95fb1-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="95fb1-141">或者，您可以修改容器的 hello 存取層級使用**setContainerAcl** toospecify hello 存取層級。</span><span class="sxs-lookup"><span data-stu-id="95fb1-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="95fb1-142">hello 下列程式碼範例變更 hello 存取層級 toocontainer:</span><span class="sxs-lookup"><span data-stu-id="95fb1-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="95fb1-143">hello 結果包含 hello 作業資訊，包括 hello 目前**ETag** hello 容器。</span><span class="sxs-lookup"><span data-stu-id="95fb1-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="95fb1-144">篩選器</span><span class="sxs-lookup"><span data-stu-id="95fb1-144">Filters</span></span>
<span data-ttu-id="95fb1-145">您可以套用篩選作業選擇性使用 toooperations 執行**BlobService**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="95fb1-146">篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：</span><span class="sxs-lookup"><span data-stu-id="95fb1-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="95fb1-147">執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步，將回呼傳遞具有下列簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="95fb1-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="95fb1-148">Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback tooend hello 服務引動過程。</span><span class="sxs-lookup"><span data-stu-id="95fb1-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="95fb1-149">實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="95fb1-150">hello 下列範例會建立**BlobService**物件，使用 hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="95fb1-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="95fb1-151">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="95fb1-151">Upload a blob into a container</span></span>
<span data-ttu-id="95fb1-152">有三種類型的 Blob：區塊 Blob、分頁 Blob 和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="95fb1-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="95fb1-153">區塊 blob 可讓您 toomore 有效率地將大型的資料上傳。</span><span class="sxs-lookup"><span data-stu-id="95fb1-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="95fb1-154">附加 Blob 已針對附加作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="95fb1-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="95fb1-155">分頁 Blob 已針對讀/寫作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="95fb1-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="95fb1-156">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="95fb1-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="95fb1-157">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-157">Block blobs</span></span>
<span data-ttu-id="95fb1-158">tooupload 資料 tooa 區塊 blob，使用下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="95fb1-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="95fb1-159">**createBlockBlobFromLocalFile** -建立新的區塊 blob 並上傳檔案的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="95fb1-160">**createBlockBlobFromStream** -建立新的區塊 blob 並上傳的資料流的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="95fb1-161">**createBlockBlobFromText** -建立新的區塊 blob 並上傳 hello 字串的內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="95fb1-162">**createWriteStreamToBlockBlob** -提供寫入資料流 tooa 區塊 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="95fb1-163">hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="95fb1-164">hello`result`這些方法所傳回包含有關 hello 作業，例如 hello **ETag**的 hello blob。</span><span class="sxs-lookup"><span data-stu-id="95fb1-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="95fb1-165">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-165">Append blobs</span></span>
<span data-ttu-id="95fb1-166">tooupload 資料 tooa 新附加 blob，請使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="95fb1-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="95fb1-167">**createAppendBlobFromLocalFile** -建立新的附加 blob 並上傳檔案的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="95fb1-168">**createAppendBlobFromStream** -建立新的附加 blob 並上傳的資料流的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="95fb1-169">**createAppendBlobFromText** -建立新的附加 blob 並上傳 hello 字串的內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="95fb1-170">**createWriteStreamToNewAppendBlob** -建立新的附加 blob，並提供資料流 toowrite tooit</span><span class="sxs-lookup"><span data-stu-id="95fb1-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="95fb1-171">hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myappendblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="95fb1-172">tooappend 現有區塊 tooan 附加 blob，使用下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="95fb1-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="95fb1-173">**appendFromLocalFile** -附加 hello 內容的檔案 tooan 現有附加 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="95fb1-174">**appendFromStream** -附加 hello 內容的資料流 tooan 現有附加 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="95fb1-175">**appendFromText** -附加 hello 內容的字串 tooan 現有附加 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="95fb1-176">**appendBlockFromStream** -附加 hello 內容的資料流 tooan 現有附加 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="95fb1-177">**appendBlockFromText** -附加 hello 內容的字串 tooan 現有附加 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="95fb1-178">appendFromXXX Api 將會進行某些用戶端驗證 toofail 快速 tooavoid 不必要的伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="95fb1-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="95fb1-179">appendBlockFromXXX 則否。</span><span class="sxs-lookup"><span data-stu-id="95fb1-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="95fb1-180">hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**myappendblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="95fb1-181">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-181">Page blobs</span></span>
<span data-ttu-id="95fb1-182">tooupload 資料 tooa 分頁 blob，使用下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="95fb1-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="95fb1-183">**createPageBlob** - 建立特定長度的新分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="95fb1-184">**createPageBlobFromLocalFile** -建立新的分頁 blob 並上傳檔案的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="95fb1-185">**createPageBlobFromStream** -建立新的分頁 blob 並上傳的資料流的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="95fb1-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="95fb1-186">**createWriteStreamToExistingPageBlob** -提供寫入資料流 tooan 現有的分頁 blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="95fb1-187">**createWriteStreamToNewPageBlob** -建立新的分頁 blob，並提供資料流 toowrite tooit</span><span class="sxs-lookup"><span data-stu-id="95fb1-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="95fb1-188">hello 下列程式碼範例會將上傳的 hello hello 內容**test.txt**檔案**mypageblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="95fb1-189">分頁 Blob 由 512 位元組的「分頁」組成。</span><span class="sxs-lookup"><span data-stu-id="95fb1-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="95fb1-190">如果上傳的資料大小不是 512 的倍數，則會接收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="95fb1-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="95fb1-191">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-191">List hello blobs in a container</span></span>
<span data-ttu-id="95fb1-192">toolist hello blob 容器中的使用 hello **listBlobsSegmented**方法。</span><span class="sxs-lookup"><span data-stu-id="95fb1-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="95fb1-193">如果您想要以特定的前置詞 tooreturn blob，使用**listBlobsSegmentedWithPrefix**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="95fb1-194">hello`result`包含`entries`集合，其描述每一個 blob 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="95fb1-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="95fb1-195">如果無法傳回的所有 blob，hello`result`也提供`continuationToken`，而您可以使用做為 hello 第二個參數 tooretrieve 其他項目。</span><span class="sxs-lookup"><span data-stu-id="95fb1-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="95fb1-196">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-196">Download blobs</span></span>
<span data-ttu-id="95fb1-197">從 blob，toodownload 資料使用 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="95fb1-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="95fb1-198">**getBlobToLocalFile** -寫入 hello blob 內容 toofile</span><span class="sxs-lookup"><span data-stu-id="95fb1-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="95fb1-199">**getBlobToStream** -寫入 hello blob 內容 tooa 資料流</span><span class="sxs-lookup"><span data-stu-id="95fb1-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="95fb1-200">**getBlobToText** -hello blob 內容寫入 tooa 字串</span><span class="sxs-lookup"><span data-stu-id="95fb1-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="95fb1-201">**createReadStream** -提供從 hello blob 資料流 tooread</span><span class="sxs-lookup"><span data-stu-id="95fb1-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="95fb1-202">hello 下列程式碼範例示範如何使用**getBlobToStream** hello toodownload hello 內容**myblob** blob，並將它儲存 toohello **output.txt**所使用的檔案資料流：</span><span class="sxs-lookup"><span data-stu-id="95fb1-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="95fb1-203">hello`result`包含 hello blob 的相關資訊包括**ETag**資訊。</span><span class="sxs-lookup"><span data-stu-id="95fb1-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="95fb1-204">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-204">Delete a blob</span></span>
<span data-ttu-id="95fb1-205">最後，呼叫 toodelete blob， **deleteBlob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="95fb1-206">下列程式碼範例刪除 hello 名為 blob 的 hello **myblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="95fb1-207">並行存取</span><span class="sxs-lookup"><span data-stu-id="95fb1-207">Concurrent access</span></span>
<span data-ttu-id="95fb1-208">您可以使用從多個用戶端或多個處理序執行個體的並行存取 tooa blob toosupport， **Etag**或**租用**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="95fb1-209">**Etag** -提供 hello blob 或容器的方式 toodetect 已被另一個處理序</span><span class="sxs-lookup"><span data-stu-id="95fb1-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="95fb1-210">**租用**-提供方式 tooobtain 獨佔、 更新、 寫入或刪除的一段時間的存取 tooa blob</span><span class="sxs-lookup"><span data-stu-id="95fb1-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="95fb1-211">ETag</span><span class="sxs-lookup"><span data-stu-id="95fb1-211">ETag</span></span>
<span data-ttu-id="95fb1-212">如果您需要多個用戶端或執行個體 toowrite toohello 區塊 Blob 或分頁 Blob 同時 tooallow，使用 Etag。</span><span class="sxs-lookup"><span data-stu-id="95fb1-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="95fb1-213">hello ETag 可讓您 toodetermine 如果 hello 容器或 blob 已修改一開始讀取或建立，可讓您 tooavoid 覆寫其他用戶端或處理序認可的變更之後。</span><span class="sxs-lookup"><span data-stu-id="95fb1-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="95fb1-214">您可以使用選擇性的 hello 設定 ETag 條件`options.accessConditions`參數。</span><span class="sxs-lookup"><span data-stu-id="95fb1-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="95fb1-215">hello 下列程式碼範例只會將上傳 hello **test.txt**所包含的檔案，如果 hello blob 已經存在，而且具有 hello ETag 值`etagToMatch`。</span><span class="sxs-lookup"><span data-stu-id="95fb1-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="95fb1-216">當您使用的 Etag 時，hello 一般模式將會是：</span><span class="sxs-lookup"><span data-stu-id="95fb1-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="95fb1-217">取得 hello ETag hello 的建立、 清單或取得作業的結果。</span><span class="sxs-lookup"><span data-stu-id="95fb1-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="95fb1-218">執行動作，檢查該 hello ETag 值不修改。</span><span class="sxs-lookup"><span data-stu-id="95fb1-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="95fb1-219">如果已修改 hello 值，這表示另一個用戶端或執行個體修改 hello blob 或容器取得 hello ETag 值之後。</span><span class="sxs-lookup"><span data-stu-id="95fb1-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="95fb1-220">租用</span><span class="sxs-lookup"><span data-stu-id="95fb1-220">Lease</span></span>
<span data-ttu-id="95fb1-221">您可以取得新的租用，方式是使用 hello **acquireLease**方法，並指定 hello blob 或容器想 tooobtain 租用上。</span><span class="sxs-lookup"><span data-stu-id="95fb1-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="95fb1-222">例如，下列程式碼的 hello 上中取得的租用**myblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="95fb1-223">在後續作業**myblob**必須提供 hello`options.leaseId`參數。</span><span class="sxs-lookup"><span data-stu-id="95fb1-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="95fb1-224">做為傳回識別碼 hello 租用`result.id`從**acquireLease**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="95fb1-225">根據預設，hello 租用持續時間為無限。</span><span class="sxs-lookup"><span data-stu-id="95fb1-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="95fb1-226">您可以指定非無限期持續時間 （介於 15 到 60 秒為單位） 藉由提供 hello`options.leaseDuration`參數。</span><span class="sxs-lookup"><span data-stu-id="95fb1-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="95fb1-227">tooremove 租用，使用**releaseLease**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="95fb1-228">toobreak 租用，但防止其他 hello 原始期間過期之前，請取得新的租用，從使用**breakLease**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="95fb1-229">使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="95fb1-229">Work with shared access signatures</span></span>
<span data-ttu-id="95fb1-230">共用的存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tooblobs 和容器，但未提供您的儲存體帳戶名稱或索引鍵。</span><span class="sxs-lookup"><span data-stu-id="95fb1-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="95fb1-231">共用的存取簽章通常是使用的 tooprovide 有限存取 tooyour 資料，例如 tooaccess blob 允許行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="95fb1-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="95fb1-232">雖然您也可以允許匿名存取 tooblobs，共用的存取簽章可讓您 tooprovide 較受控制的存取權，您必須產生 hello SAS。</span><span class="sxs-lookup"><span data-stu-id="95fb1-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="95fb1-233">信任的應用程式，例如雲端服務會產生共用的存取簽章使用 hello **generateSharedAccessSignature**的 hello **BlobService**，然後將其提供 tooan 不受信任或非完全信任應用程式，例如行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="95fb1-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="95fb1-234">共用的存取簽章使用產生的原則，其中描述 hello 開始和結束日期的 hello 期間共用的存取簽章不正確，以及 hello 存取層級授與的 toohello 共用的存取簽章持有者。</span><span class="sxs-lookup"><span data-stu-id="95fb1-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="95fb1-235">hello 下列程式碼範例會產生新的共用的存取原則，可讓 hello 共用存取簽章持有者 tooperform 的讀取作業 hello **myblob** blob，而且已過期之後建立的 hello 時 100 分鐘。</span><span class="sxs-lookup"><span data-stu-id="95fb1-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="95fb1-236">請注意 hello 主機資訊必須提供此外，視需要當 hello 共用的存取簽章持有者嘗試 tooaccess hello 容器。</span><span class="sxs-lookup"><span data-stu-id="95fb1-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="95fb1-237">hello 用戶端應用程式接著會使用共用的存取簽章**BlobServiceWithSAS** tooperform hello blob 的作業。</span><span class="sxs-lookup"><span data-stu-id="95fb1-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="95fb1-238">hello 下列取得資訊的相關**myblob**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="95fb1-239">如果嘗試 toomodify hello blob hello 共用存取簽章產生具有唯讀存取權，因為將會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="95fb1-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="95fb1-240">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="95fb1-240">Access control lists</span></span>
<span data-ttu-id="95fb1-241">您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。</span><span class="sxs-lookup"><span data-stu-id="95fb1-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="95fb1-242">如果您想 tooallow 多個用戶端 tooaccess 容器，但每個用戶端提供不同的存取原則，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="95fb1-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="95fb1-243">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="95fb1-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="95fb1-244">hello，下列程式碼範例會定義兩個原則，一個用於 'user1'，'user2' 其中一個：</span><span class="sxs-lookup"><span data-stu-id="95fb1-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="95fb1-245">下列程式碼範例會取得 hello hello 目前 ACL **mycontainer**，並將 hello 新原則使用**setBlobAcl**。</span><span class="sxs-lookup"><span data-stu-id="95fb1-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="95fb1-246">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="95fb1-246">This approach allows:</span></span>

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

<span data-ttu-id="95fb1-247">一次 hello ACL 設定，然後您可以建立共用的存取簽章根據 hello 原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="95fb1-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="95fb1-248">hello，下列程式碼範例會建立新的共用的存取簽章 'user2':</span><span class="sxs-lookup"><span data-stu-id="95fb1-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="95fb1-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95fb1-249">Next steps</span></span>
<span data-ttu-id="95fb1-250">如需詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="95fb1-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="95fb1-251">[Azure Storage SDK for Node API 參考][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="95fb1-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="95fb1-252">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="95fb1-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="95fb1-253">GitHub 上的 [Azure Storage SDK for Node][Azure Storage SDK for Node] 儲存機制</span><span class="sxs-lookup"><span data-stu-id="95fb1-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="95fb1-254">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="95fb1-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="95fb1-255">使用 hello AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="95fb1-255">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Node.js web 應用程式建立 Azure App Service 中]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web 應用程式使用 hello Azure 資料表服務]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
