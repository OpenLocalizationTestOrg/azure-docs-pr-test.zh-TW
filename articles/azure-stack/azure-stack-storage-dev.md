---
title: "開始使用 Azure Stack 儲存體開發工具"
description: "開始使用 Azure Stack 儲存體開發工具的指引"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: a4c1c316022f992750fe60d28b9be61b17242a64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="b9452-103">開始使用 Azure Stack 儲存體開發工具</span><span class="sxs-lookup"><span data-stu-id="b9452-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="b9452-104">Microsoft Azure Stack 提供一組儲存體服務，包括 Azure Blob、資料表和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="b9452-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="b9452-105">本文提供如何開始使用 Azure Stack 儲存體開發工具的快速指引。</span><span class="sxs-lookup"><span data-stu-id="b9452-105">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="b9452-106">您可以在對應的 Azure 儲存體教學課程中，找到更詳細的資訊和範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="b9452-106">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="b9452-107">Azure 儲存體和 Azure Stack 儲存體之間有一些已知的差異，包括每個平台的一些特定需求。</span><span class="sxs-lookup"><span data-stu-id="b9452-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="b9452-108">例如，Azure Stack 有特定的用戶端程式庫以及特定的端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="b9452-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="b9452-109">如需詳細資訊，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。</span><span class="sxs-lookup"><span data-stu-id="b9452-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="b9452-110">Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="b9452-110">Azure client libraries</span></span>
<span data-ttu-id="b9452-111">支援的 Azure Stack 儲存體 REST API 版本為 2015-04-05。</span><span class="sxs-lookup"><span data-stu-id="b9452-111">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="b9452-112">此版本異於最新版的 Azure 儲存體 REST API。</span><span class="sxs-lookup"><span data-stu-id="b9452-112">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="b9452-113">因此，針對儲存體用戶端程式庫，您需要知道與 REST API 2015-04-05 相容的版本。</span><span class="sxs-lookup"><span data-stu-id="b9452-113">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="b9452-114">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="b9452-114">Client library</span></span>|<span data-ttu-id="b9452-115">Azure Stack 支援的版本</span><span class="sxs-lookup"><span data-stu-id="b9452-115">Azure Stack supported version</span></span>|<span data-ttu-id="b9452-116">連結</span><span class="sxs-lookup"><span data-stu-id="b9452-116">Link</span></span>|<span data-ttu-id="b9452-117">端點規格</span><span class="sxs-lookup"><span data-stu-id="b9452-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="b9452-118">.NET</span><span class="sxs-lookup"><span data-stu-id="b9452-118">.NET</span></span>     |<span data-ttu-id="b9452-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="b9452-119">6.2.0</span></span>|<span data-ttu-id="b9452-120">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-120">Nuget package:</span></span><br>[<span data-ttu-id="b9452-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="b9452-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="b9452-122">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-122">GitHub release:</span></span><br>[<span data-ttu-id="b9452-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="b9452-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="b9452-124">app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="b9452-124">app.config file</span></span>|
|<span data-ttu-id="b9452-125">Java</span><span class="sxs-lookup"><span data-stu-id="b9452-125">Java</span></span>|<span data-ttu-id="b9452-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="b9452-126">4.1.0</span></span>|<span data-ttu-id="b9452-127">Maven 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-127">Maven package:</span></span><br>[<span data-ttu-id="b9452-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="b9452-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="b9452-129">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-129">GitHub release:</span></span><br> [<span data-ttu-id="b9452-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="b9452-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="b9452-131">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="b9452-131">Connection string setup</span></span>|
|<span data-ttu-id="b9452-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="b9452-132">Node.js</span></span>     |<span data-ttu-id="b9452-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b9452-133">1.1.0</span></span>|<span data-ttu-id="b9452-134">NPM 連結：</span><span class="sxs-lookup"><span data-stu-id="b9452-134">NPM link:</span></span><br>[<span data-ttu-id="b9452-135">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="b9452-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="b9452-136">(執行：`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="b9452-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="b9452-137">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-137">Github release:</span></span><br>[<span data-ttu-id="b9452-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="b9452-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="b9452-139">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="b9452-139">Service instance declaration</span></span>||<span data-ttu-id="b9452-140">C++</span><span class="sxs-lookup"><span data-stu-id="b9452-140">C++</span></span>|<span data-ttu-id="b9452-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-141">2.4.0</span></span>|<span data-ttu-id="b9452-142">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-142">Nuget package:</span></span><br>[<span data-ttu-id="b9452-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="b9452-144">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-144">GitHub release:</span></span><br>[<span data-ttu-id="b9452-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="b9452-146">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="b9452-146">Connection string setup</span></span>|
|<span data-ttu-id="b9452-147">C++</span><span class="sxs-lookup"><span data-stu-id="b9452-147">C++</span></span>|<span data-ttu-id="b9452-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-148">2.4.0</span></span>|<span data-ttu-id="b9452-149">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-149">Nuget package:</span></span><br>[<span data-ttu-id="b9452-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="b9452-151">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-151">GitHub release:</span></span><br>[<span data-ttu-id="b9452-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="b9452-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="b9452-153">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="b9452-153">Connection string setup</span></span>|
|<span data-ttu-id="b9452-154">PHP</span><span class="sxs-lookup"><span data-stu-id="b9452-154">PHP</span></span>|<span data-ttu-id="b9452-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="b9452-155">0.15.0</span></span>|<span data-ttu-id="b9452-156">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-156">GitHub release:</span></span><br>[<span data-ttu-id="b9452-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="b9452-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="b9452-158">透過編輯器安裝 (請參閱下面的詳細資料)</span><span class="sxs-lookup"><span data-stu-id="b9452-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="b9452-159">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="b9452-159">Connection string setup</span></span>|
|<span data-ttu-id="b9452-160">Python</span><span class="sxs-lookup"><span data-stu-id="b9452-160">Python</span></span>     |<span data-ttu-id="b9452-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="b9452-161">0.30.0</span></span>|<span data-ttu-id="b9452-162">PIP 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-162">PIP package:</span></span><br> [<span data-ttu-id="b9452-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="b9452-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="b9452-164">(執行：`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="b9452-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="b9452-165">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-165">GitHub release:</span></span><br> [<span data-ttu-id="b9452-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="b9452-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="b9452-167">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="b9452-167">Service instance declaration</span></span>|
|<span data-ttu-id="b9452-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="b9452-168">Ruby</span></span>|<span data-ttu-id="b9452-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="b9452-169">0.12.1</span></span><br><span data-ttu-id="b9452-170">預覽</span><span class="sxs-lookup"><span data-stu-id="b9452-170">Preview</span></span>|<span data-ttu-id="b9452-171">RubyGems 套件：</span><span class="sxs-lookup"><span data-stu-id="b9452-171">RubyGems package:</span></span><br> [<span data-ttu-id="b9452-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="b9452-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="b9452-173">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="b9452-173">GitHub release:</span></span><br> [<span data-ttu-id="b9452-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="b9452-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="b9452-175">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="b9452-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="b9452-176">PHP 詳細資料</span><span class="sxs-lookup"><span data-stu-id="b9452-176">PHP details</span></span><br><br>
><span data-ttu-id="b9452-177">透過編輯器安裝：</span><span class="sxs-lookup"><span data-stu-id="b9452-177">To install via Composer:</span></span>
>1. <span data-ttu-id="b9452-178">在專案的根目錄中，使用下列程式碼建立一個名為 `composer.json` 的檔案：</span><span class="sxs-lookup"><span data-stu-id="b9452-178">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="b9452-179">將 [composer.phar](http://getcomposer.org/composer.phar) 下載到專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="b9452-179">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="b9452-180">執行：`php composer.phar install`。</span><span class="sxs-lookup"><span data-stu-id="b9452-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="b9452-181">端點宣告</span><span class="sxs-lookup"><span data-stu-id="b9452-181">Endpoint declaration</span></span>
<span data-ttu-id="b9452-182">Azure Stack 端點包含兩個部分：區域的名稱和 Azure Stack 網域。</span><span class="sxs-lookup"><span data-stu-id="b9452-182">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="b9452-183">在 Azure Stack 開發套件中，預設端點是 **local.azurestack.external**。</span><span class="sxs-lookup"><span data-stu-id="b9452-183">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="b9452-184">如果不確定您的端點，請連絡您的雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b9452-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="b9452-185">範例</span><span class="sxs-lookup"><span data-stu-id="b9452-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="b9452-186">.NET</span><span class="sxs-lookup"><span data-stu-id="b9452-186">.NET</span></span>

<span data-ttu-id="b9452-187">若是 Azure Stack，在 app.config 檔案中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-187">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="b9452-188">Java</span><span class="sxs-lookup"><span data-stu-id="b9452-188">Java</span></span>

<span data-ttu-id="b9452-189">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-189">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="b9452-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="b9452-190">Node.js</span></span>

<span data-ttu-id="b9452-191">若是 Azure Stack，在宣告執行個體中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-191">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="b9452-192">C++</span><span class="sxs-lookup"><span data-stu-id="b9452-192">C++</span></span>

<span data-ttu-id="b9452-193">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-193">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="b9452-194">PHP</span><span class="sxs-lookup"><span data-stu-id="b9452-194">PHP</span></span>

<span data-ttu-id="b9452-195">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-195">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="b9452-196">Python</span><span class="sxs-lookup"><span data-stu-id="b9452-196">Python</span></span>

<span data-ttu-id="b9452-197">若是 Azure Stack，在宣告執行個體中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-197">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="b9452-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="b9452-198">Ruby</span></span>

<span data-ttu-id="b9452-199">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="b9452-199">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="b9452-200">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-200">Blob storage</span></span>

<span data-ttu-id="b9452-201">下列 Azure Blob 儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="b9452-201">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="b9452-202">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="b9452-202">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="b9452-203">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="b9452-204">如何使用 Java 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-204">How to use Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="b9452-205">如何使用 Node.js 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-205">How to use Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="b9452-206">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-206">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="b9452-207">如何使用 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-207">How to use Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="b9452-208">如何從 Python 使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-208">How to use Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="b9452-209">如何使用 Ruby 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-209">How to use Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="b9452-210">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-210">Queue storage</span></span>

<span data-ttu-id="b9452-211">下列 Azure 佇列儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="b9452-211">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="b9452-212">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="b9452-212">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="b9452-213">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="b9452-214">如何使用 Java 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-214">How to use Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="b9452-215">如何使用 Node.js 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-215">How to use Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="b9452-216">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-216">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b9452-217">如何使用 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-217">How to use Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="b9452-218">如何使用 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-218">How to use Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="b9452-219">如何使用 Ruby 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-219">How to use Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="b9452-220">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-220">Table storage</span></span>

<span data-ttu-id="b9452-221">下列 Azure 資料表儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="b9452-221">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="b9452-222">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="b9452-222">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="b9452-223">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="b9452-224">如何使用 Java 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-224">How to use Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="b9452-225">如何從 Node.js 使用 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-225">How to use Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="b9452-226">如何從 C++ 使用資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-226">How to use Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="b9452-227">如何使用 PHP 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-227">How to use Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="b9452-228">如何在 Python 中使用資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-228">How to use Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="b9452-229">如何使用 Ruby 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="b9452-229">How to use Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="b9452-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9452-230">Next steps</span></span>

* [<span data-ttu-id="b9452-231">Microsoft Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="b9452-231">Introduction to Microsoft Azure Storage</span></span>](../storage/common/storage-introduction.md)