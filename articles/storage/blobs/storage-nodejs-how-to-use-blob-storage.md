---
title: "如何使用 Node.js 中的 Blob 儲存體 | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: e83ad647f6b7c70f34ef0c69b5bf322da5b6d60d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="aa53e-103">如何使用 Node.js 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="aa53e-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="aa53e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="aa53e-104">Overview</span></span>
<span data-ttu-id="aa53e-105">本文章示範如何使用 Blob 儲存體執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="aa53e-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="aa53e-106">這些範例透過 Node.js API 撰寫。</span><span class="sxs-lookup"><span data-stu-id="aa53e-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="aa53e-107">涵蓋的案例包括如何上傳、列出、下載及刪除 blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="aa53e-108">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa53e-108">Create a Node.js application</span></span>
<span data-ttu-id="aa53e-109">如需如何建立 Node.js 應用程式的相關指示，請參閱 [在 Azure App Service 中建立 Node.js Web 應用程式]、[使用 Windows PowerShell 建立 Node.js 應用程式並部署至 Azure 雲端服務](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)，或[使用 Web Matrix 建立 Node.js Web 應用程式並部署至 Azure](https://www.microsoft.com/web/webmatrix/)。</span><span class="sxs-lookup"><span data-stu-id="aa53e-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="aa53e-110">設定您的應用程式以存取儲存體</span><span class="sxs-lookup"><span data-stu-id="aa53e-110">Configure your application to access storage</span></span>
<span data-ttu-id="aa53e-111">若要使用 Azure 儲存體，您需要 Azure Storage SDK for Node.js，這包含一組便利程式庫，能與儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="aa53e-112">使用 Node Package Manager (NPM) 取得封裝</span><span class="sxs-lookup"><span data-stu-id="aa53e-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="aa53e-113">使用命令列介面，例如 **PowerShell** (Windows)、**[終端機]** \(Mac) 或 **Bash** \(Unix)，瀏覽到您建立範例應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa53e-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="aa53e-114">在命令視窗中輸入 **npm install azure-storage** 。</span><span class="sxs-lookup"><span data-stu-id="aa53e-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="aa53e-115">此命令的輸出類似下列程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="aa53e-115">Output from the command is similar to the following code example.</span></span>

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
3. <span data-ttu-id="aa53e-116">您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa53e-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="aa53e-117">在該資料夾中找出 **azure-storage** 封裝，當中包含存取儲存體所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="aa53e-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="aa53e-118">匯入封裝</span><span class="sxs-lookup"><span data-stu-id="aa53e-118">Import the package</span></span>
<span data-ttu-id="aa53e-119">使用記事本或其他文字編輯器，將以下內容新增至您要使用儲存體之應用程式的 **server.js** 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="aa53e-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="aa53e-120">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="aa53e-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="aa53e-121">Azure 模組會讀取環境變數 `AZURE_STORAGE_ACCOUNT` 及 `AZURE_STORAGE_ACCESS_KEY`，或讀取 `AZURE_STORAGE_CONNECTION_STRING` 以取得連接 Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="aa53e-122">如果未設定這些環境變數，則呼叫 **createBlobService**時必須指定帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="aa53e-123">如需針對 Azure Web 應用程式在 [Azure 入口網站](https://portal.azure.com)中設定環境變數的範例，請參閱[使用 Azure 表格服務的 Node.js Web 應用程式](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="aa53e-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="aa53e-124">建立容器</span><span class="sxs-lookup"><span data-stu-id="aa53e-124">Create a container</span></span>
<span data-ttu-id="aa53e-125">**BlobService** 物件讓您能使用容器及 blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="aa53e-126">下列程式碼會建立 **BlobService** 物件。</span><span class="sxs-lookup"><span data-stu-id="aa53e-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="aa53e-127">將下列內容新增至接近 **server.js**的頂端：</span><span class="sxs-lookup"><span data-stu-id="aa53e-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="aa53e-128">使用 **createBlobServiceAnonymous** 並提供主機位址，可匿名存取 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="aa53e-129">例如，使用 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`。</span><span class="sxs-lookup"><span data-stu-id="aa53e-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="aa53e-130">若要建立新的容器，請使用 **createContainerIfNotExists**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="aa53e-131">以下程式碼範例會建立一個名為 'mycontainer' 的新容器：</span><span class="sxs-lookup"><span data-stu-id="aa53e-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="aa53e-132">如果是新建立的容器， `result.created` 為 true。</span><span class="sxs-lookup"><span data-stu-id="aa53e-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="aa53e-133">如果容器已存在，則 `result.created` 為 false。</span><span class="sxs-lookup"><span data-stu-id="aa53e-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="aa53e-134">`response` 包含作業的相關資訊，包括容器的 ETag 資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="aa53e-135">容器安全性</span><span class="sxs-lookup"><span data-stu-id="aa53e-135">Container security</span></span>
<span data-ttu-id="aa53e-136">依預設，新的容器屬私人性質，無法以匿名方式存取。</span><span class="sxs-lookup"><span data-stu-id="aa53e-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="aa53e-137">若要將容器變成公開，以便以匿名方式進行存取，您可以將容器的存取等級設為 **blob** 或 **container**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="aa53e-138">**blob** - 允許對此容器內的 Blob 內容和中繼資料的匿名讀取存取，但不包含對容器中繼資料的匿名讀取存取，例如列出容器內的所有 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="aa53e-139">**container** - 允許對 Blob 內容和中繼資料及容器中繼資料的匿名讀取存取</span><span class="sxs-lookup"><span data-stu-id="aa53e-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="aa53e-140">下列程式碼範例示範將存取等級設為 **blob**：</span><span class="sxs-lookup"><span data-stu-id="aa53e-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="aa53e-141">或者，您可以使用 **setContainerAcl** 指定存取等級，以修改容器的存取等級。</span><span class="sxs-lookup"><span data-stu-id="aa53e-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="aa53e-142">下列程式碼範例會將存取等級變更為 container：</span><span class="sxs-lookup"><span data-stu-id="aa53e-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="aa53e-143">結果包含操作的相關資訊，包括容器的目前 **ETag** 。</span><span class="sxs-lookup"><span data-stu-id="aa53e-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="aa53e-144">篩選器</span><span class="sxs-lookup"><span data-stu-id="aa53e-144">Filters</span></span>
<span data-ttu-id="aa53e-145">您可以將選用的篩選作業套用到使用 **BlobService** 執行的作業。</span><span class="sxs-lookup"><span data-stu-id="aa53e-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="aa53e-146">篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：</span><span class="sxs-lookup"><span data-stu-id="aa53e-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="aa53e-147">在對要求選項進行前處理之後，方法需要呼叫 "next" 並傳遞具有下列簽章的回呼：</span><span class="sxs-lookup"><span data-stu-id="aa53e-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="aa53e-148">在此回呼中，以及處理 returnObject (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是直接叫用 finalCallback 結束服務叫用。</span><span class="sxs-lookup"><span data-stu-id="aa53e-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="aa53e-149">Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="aa53e-150">以下會建立使用 **ExponentialRetryPolicyFilter** 的 **BlobService** 物件：</span><span class="sxs-lookup"><span data-stu-id="aa53e-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="aa53e-151">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="aa53e-151">Upload a blob into a container</span></span>
<span data-ttu-id="aa53e-152">有三種類型的 Blob：區塊 Blob、分頁 Blob 和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="aa53e-153">Block Blob 可讓您更有效率地上傳大型資料。</span><span class="sxs-lookup"><span data-stu-id="aa53e-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="aa53e-154">附加 Blob 已針對附加作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="aa53e-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="aa53e-155">分頁 Blob 已針對讀/寫作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="aa53e-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="aa53e-156">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="aa53e-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="aa53e-157">區塊 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-157">Block blobs</span></span>
<span data-ttu-id="aa53e-158">若要將資料上傳至區塊 Blob，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="aa53e-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="aa53e-159">**createBlockBlobFromLocalFile** - 建立新的區塊 Blob 並上傳檔案的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="aa53e-160">**createBlockBlobFromStream** - 建立新的區塊 Blob 並上傳串流的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="aa53e-161">**createBlockBlobFromText** - 建立新的區塊 Blob 並上傳字串的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="aa53e-162">**createWriteStreamToBlockBlob** - 提供對區塊 Blob 的寫入串流</span><span class="sxs-lookup"><span data-stu-id="aa53e-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="aa53e-163">下列程式碼範例會將 **test.txt** 檔的內容上傳至 **myblob**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="aa53e-164">這些方法傳回的 `result` 包含作業的相關資訊，例如 Blob 的 **ETag** 。</span><span class="sxs-lookup"><span data-stu-id="aa53e-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="aa53e-165">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-165">Append blobs</span></span>
<span data-ttu-id="aa53e-166">若要將資料上傳至附加 Blob，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="aa53e-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="aa53e-167">**createAppendBlobFromLocalFile** - 建立新的附加 Blob 並上傳檔案的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="aa53e-168">**createAppendBlobFromStream** - 建立新的附加 Blob 並上傳串流的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="aa53e-169">**createAppendBlobFromText** - 建立新的附加 Blob 並上傳字串的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="aa53e-170">**createWriteStreamToNewAppendBlob** - 建立新的附加 Blob，然後提供串流來寫入它</span><span class="sxs-lookup"><span data-stu-id="aa53e-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="aa53e-171">下列程式碼範例會將 **test.txt** 檔案的內容上傳至 **myappendblob**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="aa53e-172">若要將區塊附加到現有附加 Blob，請使用下列方法︰</span><span class="sxs-lookup"><span data-stu-id="aa53e-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="aa53e-173">**appendFromLocalFile** - 將檔案的內容附加到現有附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="aa53e-174">**appendFromStream** - 將串流的內容附加到現有附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="aa53e-175">**appendFromText** - 將字串的內容附加到現有附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="aa53e-176">**appendBlockFromStream** - 將串流的內容附加到現有附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="aa53e-177">**appendBlockFromText** - 將字串的內容附加到現有附加 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="aa53e-178">appendFromXXX API 會讓部分用戶端驗證立即失敗，以避免不必要的伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="aa53e-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="aa53e-179">appendBlockFromXXX 則否。</span><span class="sxs-lookup"><span data-stu-id="aa53e-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="aa53e-180">下列程式碼範例會將 **test.txt** 檔案的內容上傳至 **myappendblob**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="aa53e-181">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-181">Page blobs</span></span>
<span data-ttu-id="aa53e-182">若要將資料上傳至分頁 Blob，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="aa53e-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="aa53e-183">**createPageBlob** - 建立特定長度的新分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="aa53e-184">**createPageBlobFromLocalFile** - 建立新的分頁 Blob 並上傳檔案的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="aa53e-185">**createPageBlobFromStream** - 建立新的分頁 Blob 並上傳串流的內容</span><span class="sxs-lookup"><span data-stu-id="aa53e-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="aa53e-186">**createWriteStreamToExistingPageBlob** - 提供對現有分頁 Blob 的寫入串流</span><span class="sxs-lookup"><span data-stu-id="aa53e-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="aa53e-187">**createWriteStreamToNewPageBlob** - 建立新的分頁 Blob，然後提供串流來寫入它</span><span class="sxs-lookup"><span data-stu-id="aa53e-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="aa53e-188">下列程式碼範例會將 **test.txt** 檔的內容上傳至 **mypageblob**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="aa53e-189">分頁 Blob 由 512 位元組的「分頁」組成。</span><span class="sxs-lookup"><span data-stu-id="aa53e-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="aa53e-190">如果上傳的資料大小不是 512 的倍數，則會接收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa53e-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="aa53e-191">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-191">List the blobs in a container</span></span>
<span data-ttu-id="aa53e-192">若要列出容器中的 Blob，請使用 **listBlobsSegmented** 方法。</span><span class="sxs-lookup"><span data-stu-id="aa53e-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="aa53e-193">若要傳回具有特定首碼的 Blob，請使用 **listBlobsSegmentedWithPrefix**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="aa53e-194">`result` 包含 `entries` 集合，此集合是描述每個 Blob 的物件陣列。</span><span class="sxs-lookup"><span data-stu-id="aa53e-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="aa53e-195">若無法傳回所有 Blob，`result` 也會提供 `continuationToken`，其可作為第二個參數來擷取更多項目。</span><span class="sxs-lookup"><span data-stu-id="aa53e-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="aa53e-196">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-196">Download blobs</span></span>
<span data-ttu-id="aa53e-197">若要從 Blob 下載資料，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="aa53e-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="aa53e-198">**getBlobToLocalFile** - 將 Blob 內容寫入檔案</span><span class="sxs-lookup"><span data-stu-id="aa53e-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="aa53e-199">**getBlobToStream** - 將 Blob 內容寫入串流</span><span class="sxs-lookup"><span data-stu-id="aa53e-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="aa53e-200">**getBlobToText** - 將 Blob 內容寫入字串</span><span class="sxs-lookup"><span data-stu-id="aa53e-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="aa53e-201">**createReadStream** - 提供串流來讀取 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="aa53e-202">下列程式碼範例示範使用 **getBlobToStream** 來下載 **myblob** Blob 的內容，並使用串流存放到 **output.txt** 檔案：</span><span class="sxs-lookup"><span data-stu-id="aa53e-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="aa53e-203">`result` 包含 Blob 的相關資訊，包括 **ETag** 資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="aa53e-204">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="aa53e-204">Delete a blob</span></span>
<span data-ttu-id="aa53e-205">最後，呼叫 **deleteBlob**以刪除 blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="aa53e-206">下列程式碼範例會刪除名為 **myblob**的 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="aa53e-207">並行存取</span><span class="sxs-lookup"><span data-stu-id="aa53e-207">Concurrent access</span></span>
<span data-ttu-id="aa53e-208">若要支援從多個用戶端或多個程序執行個體並行存取 Blob，您可以使用 **ETags** 或「租用」。</span><span class="sxs-lookup"><span data-stu-id="aa53e-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="aa53e-209">**Etag** - 提供方法來偵測 Blob 或容器已被另一個程序修改過</span><span class="sxs-lookup"><span data-stu-id="aa53e-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="aa53e-210">**租用** - 提供方法來取得在一段時間內對 Blob 的獨佔、可更新、寫入或刪除存取權</span><span class="sxs-lookup"><span data-stu-id="aa53e-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="aa53e-211">ETag</span><span class="sxs-lookup"><span data-stu-id="aa53e-211">ETag</span></span>
<span data-ttu-id="aa53e-212">若您需要允許多個用戶端或執行個體同時寫入區塊 Blob 或分頁 Blob，請使用 ETag。</span><span class="sxs-lookup"><span data-stu-id="aa53e-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="aa53e-213">ETag 可讓您判斷容器或 Blob 自從您最初讀取或建立它之後是否已修改，這樣可讓您避免覆寫另一個用戶端或程序已認可的變更。</span><span class="sxs-lookup"><span data-stu-id="aa53e-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="aa53e-214">使用選用的 `options.accessConditions` 參數，可以設定 ETag 條件。</span><span class="sxs-lookup"><span data-stu-id="aa53e-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="aa53e-215">只有在 Blob 已存在，且 `etagToMatch` 中包含 ETag 值時，下列程式碼範例才會上傳 **test.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="aa53e-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="aa53e-216">使用 ETag 時，一般模式為：</span><span class="sxs-lookup"><span data-stu-id="aa53e-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="aa53e-217">取得執行建立、列出或取得操作之後的 ETag。</span><span class="sxs-lookup"><span data-stu-id="aa53e-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="aa53e-218">執行動作，檢查 ETag 值未被修改。</span><span class="sxs-lookup"><span data-stu-id="aa53e-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="aa53e-219">若值已被修改，這表示另一個用戶端或執行個體自從您取得 ETag 值之後已修改 Blob 或容器。</span><span class="sxs-lookup"><span data-stu-id="aa53e-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="aa53e-220">租用</span><span class="sxs-lookup"><span data-stu-id="aa53e-220">Lease</span></span>
<span data-ttu-id="aa53e-221">使用 **acquireLease** 方法，並指定您要取得租用的 Blob 或容器，即可取得新的租用。</span><span class="sxs-lookup"><span data-stu-id="aa53e-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="aa53e-222">例如，下列程式碼可取得 **myblob**的租用。</span><span class="sxs-lookup"><span data-stu-id="aa53e-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="aa53e-223">**myblob** 的後續作業必須提供 `options.leaseId` 參數。</span><span class="sxs-lookup"><span data-stu-id="aa53e-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="aa53e-224">租用識別碼會從 **acquireLease** 作為 `result.id` 傳回。</span><span class="sxs-lookup"><span data-stu-id="aa53e-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="aa53e-225">依預設，租用期間無限制。</span><span class="sxs-lookup"><span data-stu-id="aa53e-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="aa53e-226">若要指定有限期間 (15 到 60 秒)，您可以提供 `options.leaseDuration` 參數。</span><span class="sxs-lookup"><span data-stu-id="aa53e-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="aa53e-227">若要移除租用，請使用 **releaseLease**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="aa53e-228">若要中止租用，但在原始期間到期之前不讓其他人取得新的租用，請使用 **breakLease**。</span><span class="sxs-lookup"><span data-stu-id="aa53e-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="aa53e-229">使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="aa53e-229">Work with shared access signatures</span></span>
<span data-ttu-id="aa53e-230">共用存取簽章 (SAS) 可安全地提供對 Blob 和容器的精確存取，而不必提供您的儲存體帳戶名稱或金鑰。</span><span class="sxs-lookup"><span data-stu-id="aa53e-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="aa53e-231">共用存取簽章通常用來提供對資料的有限存取，例如允許行動應用程式存取 Blob。</span><span class="sxs-lookup"><span data-stu-id="aa53e-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="aa53e-232">雖然您也可以用匿名方式存取 Blob，但共用存取簽章可讓您提供更受控制的存取，因為您必須產生 SAS。</span><span class="sxs-lookup"><span data-stu-id="aa53e-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="aa53e-233">信任的應用程式 (例如雲端型服務) 會使用 **BlobService** 的 **generateSharedAccessSignature** 來產生共用存取簽章，並提供它給不信任或不完全信任的應用程式 (例如行動應用程式)。</span><span class="sxs-lookup"><span data-stu-id="aa53e-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="aa53e-234">共用存取簽章是使用原則來產生，該原則描述共用存取簽章有效期間的開始和結束日期，以及授與共用存取簽章持有者的存取等級。</span><span class="sxs-lookup"><span data-stu-id="aa53e-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="aa53e-235">下列程式碼範例會產生新的共用存取原則，讓共用存取簽章持有者對 **myblob** Blob 執行讀取操作，並於建立它之後的 100 分鐘過期。</span><span class="sxs-lookup"><span data-stu-id="aa53e-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="aa53e-236">請注意，也必須提供主機資訊，因為共用存取簽章持有者嘗試存取容器時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="aa53e-237">用戶端應用程式接著以 **BlobServiceWithSAS** 來使用共用存取簽章，對 Blob 執行操作。</span><span class="sxs-lookup"><span data-stu-id="aa53e-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="aa53e-238">以下會取得 **myblob**的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa53e-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="aa53e-239">由於共用存取簽章是利用唯讀存取權所產生，如果嘗試修改 blob，就會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="aa53e-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="aa53e-240">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="aa53e-240">Access control lists</span></span>
<span data-ttu-id="aa53e-241">您也可以使用存取控制清單 (ACL) 來設定 SAS 的存取原則。</span><span class="sxs-lookup"><span data-stu-id="aa53e-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="aa53e-242">若您要允許用戶端存取容器，但對每個用戶端提供不同的存取原則，則這會很有用。</span><span class="sxs-lookup"><span data-stu-id="aa53e-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="aa53e-243">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa53e-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="aa53e-244">下列程式碼範例定義兩個原則，其中一個用於 'user1'，另一個用於 'user2'：</span><span class="sxs-lookup"><span data-stu-id="aa53e-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="aa53e-245">下列程式碼範例會取得 **mycontainer** 的目前 ACL，然後使用 **setBlobAcl** 來加入新的原則。</span><span class="sxs-lookup"><span data-stu-id="aa53e-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="aa53e-246">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="aa53e-246">This approach allows:</span></span>

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

<span data-ttu-id="aa53e-247">設定 ACL 之後，您可以根據原則的識別碼來建立共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="aa53e-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="aa53e-248">下列程式碼範例會為 'user2' 建立新的共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="aa53e-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="aa53e-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa53e-249">Next steps</span></span>
<span data-ttu-id="aa53e-250">如需詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="aa53e-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="aa53e-251">[Azure Storage SDK for Node API 參考][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="aa53e-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="aa53e-252">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="aa53e-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="aa53e-253">GitHub 上的 [Azure Storage SDK for Node][Azure Storage SDK for Node] 儲存機制</span><span class="sxs-lookup"><span data-stu-id="aa53e-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="aa53e-254">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="aa53e-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="aa53e-255">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="aa53e-255">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="aa53e-256">[使用 Azure 表格服務的 Node.js Web 應用程式](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="aa53e-256">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="aa53e-257">[使用 Web Matrix 建立 Node.js Web 應用程式並部署至 Azure]：https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="aa53e-257">[Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="aa53e-258">[使用 REST API]：http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure 入口網站]：https://portal.azure.com [建立 Node.js 應用程式並部署到 Azure 雲端服務](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure 儲存體團隊部落格]：http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API 參考]：http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="aa53e-258">[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
