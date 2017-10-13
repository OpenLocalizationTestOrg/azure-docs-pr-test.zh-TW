---
title: "開始使用 Azure Stack 儲存體開發工具"
description: "開始使用 Azure Stack 儲存體開發工具的指引"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="a07d8-103">開始使用 Azure Stack 儲存體開發工具</span><span class="sxs-lookup"><span data-stu-id="a07d8-103">Get started with Azure Stack Storage development tools</span></span>

<span data-ttu-id="a07d8-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="a07d8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>


<span data-ttu-id="a07d8-105">Microsoft Azure Stack 提供一組儲存體服務，包括 Azure Blob、資料表和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="a07d8-105">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="a07d8-106">本文提供如何開始使用 Azure Stack 儲存體開發工具的快速指引。</span><span class="sxs-lookup"><span data-stu-id="a07d8-106">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="a07d8-107">您可以在對應的 Azure 儲存體教學課程中，找到更詳細的資訊和範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="a07d8-107">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="a07d8-108">Azure 儲存體和 Azure Stack 儲存體之間有一些已知的差異，包括每個平台的一些特定需求。</span><span class="sxs-lookup"><span data-stu-id="a07d8-108">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="a07d8-109">例如，Azure Stack 有特定的用戶端程式庫以及特定的端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="a07d8-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="a07d8-110">如需詳細資訊，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。</span><span class="sxs-lookup"><span data-stu-id="a07d8-110">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="a07d8-111">Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a07d8-111">Azure client libraries</span></span>
<span data-ttu-id="a07d8-112">支援的 Azure Stack 儲存體 REST API 版本為 2015-04-05。</span><span class="sxs-lookup"><span data-stu-id="a07d8-112">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="a07d8-113">此版本異於最新版的 Azure 儲存體 REST API。</span><span class="sxs-lookup"><span data-stu-id="a07d8-113">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="a07d8-114">因此，針對儲存體用戶端程式庫，您需要知道與 REST API 2015-04-05 相容的版本。</span><span class="sxs-lookup"><span data-stu-id="a07d8-114">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="a07d8-115">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a07d8-115">Client library</span></span>|<span data-ttu-id="a07d8-116">Azure Stack 支援的版本</span><span class="sxs-lookup"><span data-stu-id="a07d8-116">Azure Stack supported version</span></span>|<span data-ttu-id="a07d8-117">連結</span><span class="sxs-lookup"><span data-stu-id="a07d8-117">Link</span></span>|<span data-ttu-id="a07d8-118">端點規格</span><span class="sxs-lookup"><span data-stu-id="a07d8-118">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="a07d8-119">.NET</span><span class="sxs-lookup"><span data-stu-id="a07d8-119">.NET</span></span>     |<span data-ttu-id="a07d8-120">6.2.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-120">6.2.0</span></span>|<span data-ttu-id="a07d8-121">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-121">Nuget package:</span></span><br>[<span data-ttu-id="a07d8-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="a07d8-123">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-123">GitHub release:</span></span><br>[<span data-ttu-id="a07d8-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="a07d8-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="a07d8-125">app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="a07d8-125">app.config file</span></span>|
|<span data-ttu-id="a07d8-126">Java</span><span class="sxs-lookup"><span data-stu-id="a07d8-126">Java</span></span>|<span data-ttu-id="a07d8-127">4.1.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-127">4.1.0</span></span>|<span data-ttu-id="a07d8-128">Maven 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-128">Maven package:</span></span><br>[<span data-ttu-id="a07d8-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="a07d8-130">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-130">GitHub release:</span></span><br> [<span data-ttu-id="a07d8-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="a07d8-132">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="a07d8-132">Connection string setup</span></span>|
|<span data-ttu-id="a07d8-133">Node.js</span><span class="sxs-lookup"><span data-stu-id="a07d8-133">Node.js</span></span>     |<span data-ttu-id="a07d8-134">1.1.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-134">1.1.0</span></span>|<span data-ttu-id="a07d8-135">NPM 連結：</span><span class="sxs-lookup"><span data-stu-id="a07d8-135">NPM link:</span></span><br>[<span data-ttu-id="a07d8-136">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="a07d8-136">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="a07d8-137">(執行：`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="a07d8-137">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="a07d8-138">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-138">Github release:</span></span><br>[<span data-ttu-id="a07d8-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="a07d8-140">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="a07d8-140">Service instance declaration</span></span>||<span data-ttu-id="a07d8-141">C++</span><span class="sxs-lookup"><span data-stu-id="a07d8-141">C++</span></span>|<span data-ttu-id="a07d8-142">2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-142">2.4.0</span></span>|<span data-ttu-id="a07d8-143">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-143">Nuget package:</span></span><br>[<span data-ttu-id="a07d8-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="a07d8-145">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-145">GitHub release:</span></span><br>[<span data-ttu-id="a07d8-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="a07d8-147">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="a07d8-147">Connection string setup</span></span>|
|<span data-ttu-id="a07d8-148">C++</span><span class="sxs-lookup"><span data-stu-id="a07d8-148">C++</span></span>|<span data-ttu-id="a07d8-149">2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-149">2.4.0</span></span>|<span data-ttu-id="a07d8-150">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-150">Nuget package:</span></span><br>[<span data-ttu-id="a07d8-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="a07d8-152">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-152">GitHub release:</span></span><br>[<span data-ttu-id="a07d8-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="a07d8-154">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="a07d8-154">Connection string setup</span></span>|
|<span data-ttu-id="a07d8-155">PHP</span><span class="sxs-lookup"><span data-stu-id="a07d8-155">PHP</span></span>|<span data-ttu-id="a07d8-156">0.15.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-156">0.15.0</span></span>|<span data-ttu-id="a07d8-157">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-157">GitHub release:</span></span><br>[<span data-ttu-id="a07d8-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="a07d8-159">透過編輯器安裝 (請參閱下面的詳細資料)</span><span class="sxs-lookup"><span data-stu-id="a07d8-159">Install via Composer (see details below)</span></span>|<span data-ttu-id="a07d8-160">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="a07d8-160">Connection string setup</span></span>|
|<span data-ttu-id="a07d8-161">Python</span><span class="sxs-lookup"><span data-stu-id="a07d8-161">Python</span></span>     |<span data-ttu-id="a07d8-162">0.30.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-162">0.30.0</span></span>|<span data-ttu-id="a07d8-163">PIP 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-163">PIP package:</span></span><br> [<span data-ttu-id="a07d8-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="a07d8-165">(執行：`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="a07d8-165">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="a07d8-166">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-166">GitHub release:</span></span><br> [<span data-ttu-id="a07d8-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="a07d8-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="a07d8-168">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="a07d8-168">Service instance declaration</span></span>|
|<span data-ttu-id="a07d8-169">Ruby</span><span class="sxs-lookup"><span data-stu-id="a07d8-169">Ruby</span></span>|<span data-ttu-id="a07d8-170">0.12.1</span><span class="sxs-lookup"><span data-stu-id="a07d8-170">0.12.1</span></span><br><span data-ttu-id="a07d8-171">預覽</span><span class="sxs-lookup"><span data-stu-id="a07d8-171">Preview</span></span>|<span data-ttu-id="a07d8-172">RubyGems 套件：</span><span class="sxs-lookup"><span data-stu-id="a07d8-172">RubyGems package:</span></span><br> [<span data-ttu-id="a07d8-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="a07d8-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="a07d8-174">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="a07d8-174">GitHub release:</span></span><br> [<span data-ttu-id="a07d8-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="a07d8-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="a07d8-176">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="a07d8-176">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="a07d8-177">PHP 詳細資料</span><span class="sxs-lookup"><span data-stu-id="a07d8-177">PHP details</span></span><br><br>
><span data-ttu-id="a07d8-178">透過編輯器安裝：</span><span class="sxs-lookup"><span data-stu-id="a07d8-178">To install via Composer:</span></span>
>1. <span data-ttu-id="a07d8-179">在專案的根目錄中，使用下列程式碼建立一個名為 `composer.json` 的檔案：</span><span class="sxs-lookup"><span data-stu-id="a07d8-179">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="a07d8-180">將 [composer.phar](http://getcomposer.org/composer.phar) 下載到專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="a07d8-180">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="a07d8-181">執行：`php composer.phar install`。</span><span class="sxs-lookup"><span data-stu-id="a07d8-181">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="a07d8-182">端點宣告</span><span class="sxs-lookup"><span data-stu-id="a07d8-182">Endpoint declaration</span></span>
<span data-ttu-id="a07d8-183">Azure Stack 端點包含兩個部分：區域的名稱和 Azure Stack 網域。</span><span class="sxs-lookup"><span data-stu-id="a07d8-183">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="a07d8-184">在 Azure Stack 開發套件中，預設端點是 **local.azurestack.external**。</span><span class="sxs-lookup"><span data-stu-id="a07d8-184">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="a07d8-185">如果不確定您的端點，請連絡您的雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="a07d8-185">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="a07d8-186">範例</span><span class="sxs-lookup"><span data-stu-id="a07d8-186">Examples</span></span>


### <a name="net"></a><span data-ttu-id="a07d8-187">.NET</span><span class="sxs-lookup"><span data-stu-id="a07d8-187">.NET</span></span>

<span data-ttu-id="a07d8-188">若是 Azure Stack，在 app.config 檔案中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-188">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="a07d8-189">Java</span><span class="sxs-lookup"><span data-stu-id="a07d8-189">Java</span></span>

<span data-ttu-id="a07d8-190">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-190">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="a07d8-191">Node.js</span><span class="sxs-lookup"><span data-stu-id="a07d8-191">Node.js</span></span>

<span data-ttu-id="a07d8-192">若是 Azure Stack，在宣告執行個體中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-192">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="a07d8-193">C++</span><span class="sxs-lookup"><span data-stu-id="a07d8-193">C++</span></span>

<span data-ttu-id="a07d8-194">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-194">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="a07d8-195">PHP</span><span class="sxs-lookup"><span data-stu-id="a07d8-195">PHP</span></span>

<span data-ttu-id="a07d8-196">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-196">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="a07d8-197">Python</span><span class="sxs-lookup"><span data-stu-id="a07d8-197">Python</span></span>

<span data-ttu-id="a07d8-198">若是 Azure Stack，在宣告執行個體中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-198">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="a07d8-199">Ruby</span><span class="sxs-lookup"><span data-stu-id="a07d8-199">Ruby</span></span>

<span data-ttu-id="a07d8-200">若是 Azure Stack，在連接字串設定中會指定端點尾碼：</span><span class="sxs-lookup"><span data-stu-id="a07d8-200">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="a07d8-201">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-201">Blob storage</span></span>

<span data-ttu-id="a07d8-202">下列 Azure Blob 儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="a07d8-202">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="a07d8-203">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="a07d8-203">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="a07d8-204">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-204">Get started with Azure Blob storage using .NET</span></span>](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="a07d8-205">如何使用 Java 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-205">How to use Blob storage from Java</span></span>](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* <span data-ttu-id="a07d8-206">[如何從 Node.js 使用 Blob 儲存體]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a07d8-206">[How to use Blob storage from Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span></span>
* [<span data-ttu-id="a07d8-207">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-207">How to use Blob storage from C++</span></span>](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="a07d8-208">如何使用 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-208">How to use Blob storage from PHP</span></span>](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="a07d8-209">如何從 Python 使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-209">How to use Azure Blob storage from Python</span></span>](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="a07d8-210">如何使用 Ruby 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-210">How to use Blob storage from Ruby</span></span>](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="a07d8-211">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-211">Queue storage</span></span>

<span data-ttu-id="a07d8-212">下列 Azure 佇列儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="a07d8-212">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="a07d8-213">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="a07d8-213">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="a07d8-214">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-214">Get started with Azure Queue storage using .NET</span></span>](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="a07d8-215">如何使用 Java 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-215">How to use Queue storage from Java</span></span>](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="a07d8-216">如何使用 Node.js 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-216">How to use Queue storage from Node.js</span></span>](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="a07d8-217">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-217">How to use Queue storage from C++</span></span>](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="a07d8-218">如何使用 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-218">How to use Queue storage from PHP</span></span>](../../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="a07d8-219">如何使用 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-219">How to use Queue storage from Python</span></span>](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="a07d8-220">如何使用 Ruby 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-220">How to use Queue storage from Ruby</span></span>](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="a07d8-221">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-221">Table storage</span></span>

<span data-ttu-id="a07d8-222">下列 Azure 資料表儲存體教學課程適用於 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="a07d8-222">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="a07d8-223">請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="a07d8-223">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="a07d8-224">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-224">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="a07d8-225">如何使用 Java 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-225">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="a07d8-226">如何從 Node.js 使用 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-226">How to use Azure Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="a07d8-227">如何從 C++ 使用資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-227">How to use Table storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="a07d8-228">如何使用 PHP 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-228">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="a07d8-229">如何在 Python 中使用資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-229">How to use Table storage in Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="a07d8-230">如何使用 Ruby 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="a07d8-230">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="a07d8-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a07d8-231">Next steps</span></span>

* [<span data-ttu-id="a07d8-232">Microsoft Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="a07d8-232">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)