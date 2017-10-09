---
title: "aaaGet 開始使用 Azure 堆疊儲存體程式開發工具"
description: "開始使用 Azure 堆疊儲存體程式開發工具的指引 tooget"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 0756ed1b9fad4aed0cca4cfd719ef3334dec6700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="d16d7-103">開始使用 Azure Stack 儲存體開發工具</span><span class="sxs-lookup"><span data-stu-id="d16d7-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="d16d7-104">Microsoft Azure Stack 提供一組儲存體服務，包括 Azure Blob、資料表和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="d16d7-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="d16d7-105">這篇文章提供如何快速指南 toostart 使用 Azure 堆疊儲存體程式開發工具。</span><span class="sxs-lookup"><span data-stu-id="d16d7-105">This article provides quick guidance on how toostart using Azure Stack Storage development tools.</span></span> <span data-ttu-id="d16d7-106">Hello 對應 Azure 儲存體教學課程中，您可以找到更多詳細的資訊和範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="d16d7-106">You can find more detailed information and sample code in hello corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="d16d7-107">Azure 儲存體和 Azure Stack 儲存體之間有一些已知的差異，包括每個平台的一些特定需求。</span><span class="sxs-lookup"><span data-stu-id="d16d7-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="d16d7-108">例如，Azure Stack 有特定的用戶端程式庫以及特定的端點尾碼需求。</span><span class="sxs-lookup"><span data-stu-id="d16d7-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="d16d7-109">如需詳細資訊，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。</span><span class="sxs-lookup"><span data-stu-id="d16d7-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="d16d7-110">Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="d16d7-110">Azure client libraries</span></span>
<span data-ttu-id="d16d7-111">Azure 堆疊儲存體的 hello 支援 REST API 版本為 2015年-04-05。</span><span class="sxs-lookup"><span data-stu-id="d16d7-111">hello supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="d16d7-112">沒有完整的同位檢查與 hello hello Azure 儲存體的 REST API 最新版本。</span><span class="sxs-lookup"><span data-stu-id="d16d7-112">It doesn’t have full parity with hello latest version of hello Azure Storage REST API.</span></span> <span data-ttu-id="d16d7-113">因此 hello 儲存體用戶端程式庫，您需要 toobe 留意 hello 版本相容的 REST API 2015-04-05。</span><span class="sxs-lookup"><span data-stu-id="d16d7-113">So for hello storage client libraries, you need toobe aware of hello version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="d16d7-114">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="d16d7-114">Client library</span></span>|<span data-ttu-id="d16d7-115">Azure Stack 支援的版本</span><span class="sxs-lookup"><span data-stu-id="d16d7-115">Azure Stack supported version</span></span>|<span data-ttu-id="d16d7-116">連結</span><span class="sxs-lookup"><span data-stu-id="d16d7-116">Link</span></span>|<span data-ttu-id="d16d7-117">端點規格</span><span class="sxs-lookup"><span data-stu-id="d16d7-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="d16d7-118">.NET</span><span class="sxs-lookup"><span data-stu-id="d16d7-118">.NET</span></span>     |<span data-ttu-id="d16d7-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-119">6.2.0</span></span>|<span data-ttu-id="d16d7-120">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-120">Nuget package:</span></span><br>[<span data-ttu-id="d16d7-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="d16d7-122">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-122">GitHub release:</span></span><br>[<span data-ttu-id="d16d7-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="d16d7-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="d16d7-124">app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="d16d7-124">app.config file</span></span>|
|<span data-ttu-id="d16d7-125">Java</span><span class="sxs-lookup"><span data-stu-id="d16d7-125">Java</span></span>|<span data-ttu-id="d16d7-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-126">4.1.0</span></span>|<span data-ttu-id="d16d7-127">Maven 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-127">Maven package:</span></span><br>[<span data-ttu-id="d16d7-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="d16d7-129">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-129">GitHub release:</span></span><br> [<span data-ttu-id="d16d7-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="d16d7-131">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="d16d7-131">Connection string setup</span></span>|
|<span data-ttu-id="d16d7-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="d16d7-132">Node.js</span></span>     |<span data-ttu-id="d16d7-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-133">1.1.0</span></span>|<span data-ttu-id="d16d7-134">NPM 連結：</span><span class="sxs-lookup"><span data-stu-id="d16d7-134">NPM link:</span></span><br>[<span data-ttu-id="d16d7-135">https://www.npmjs.com/package/azure-storage</span><span class="sxs-lookup"><span data-stu-id="d16d7-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="d16d7-136">(執行：`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="d16d7-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="d16d7-137">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-137">Github release:</span></span><br>[<span data-ttu-id="d16d7-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="d16d7-139">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="d16d7-139">Service instance declaration</span></span>||<span data-ttu-id="d16d7-140">C++</span><span class="sxs-lookup"><span data-stu-id="d16d7-140">C++</span></span>|<span data-ttu-id="d16d7-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-141">2.4.0</span></span>|<span data-ttu-id="d16d7-142">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-142">Nuget package:</span></span><br>[<span data-ttu-id="d16d7-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="d16d7-144">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-144">GitHub release:</span></span><br>[<span data-ttu-id="d16d7-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="d16d7-146">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="d16d7-146">Connection string setup</span></span>|
|<span data-ttu-id="d16d7-147">C++</span><span class="sxs-lookup"><span data-stu-id="d16d7-147">C++</span></span>|<span data-ttu-id="d16d7-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-148">2.4.0</span></span>|<span data-ttu-id="d16d7-149">Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-149">Nuget package:</span></span><br>[<span data-ttu-id="d16d7-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="d16d7-151">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-151">GitHub release:</span></span><br>[<span data-ttu-id="d16d7-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="d16d7-153">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="d16d7-153">Connection string setup</span></span>|
|<span data-ttu-id="d16d7-154">PHP</span><span class="sxs-lookup"><span data-stu-id="d16d7-154">PHP</span></span>|<span data-ttu-id="d16d7-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-155">0.15.0</span></span>|<span data-ttu-id="d16d7-156">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-156">GitHub release:</span></span><br>[<span data-ttu-id="d16d7-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="d16d7-158">透過編輯器安裝 (請參閱下面的詳細資料)</span><span class="sxs-lookup"><span data-stu-id="d16d7-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="d16d7-159">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="d16d7-159">Connection string setup</span></span>|
|<span data-ttu-id="d16d7-160">Python</span><span class="sxs-lookup"><span data-stu-id="d16d7-160">Python</span></span>     |<span data-ttu-id="d16d7-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-161">0.30.0</span></span>|<span data-ttu-id="d16d7-162">PIP 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-162">PIP package:</span></span><br> [<span data-ttu-id="d16d7-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="d16d7-164">(執行：`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="d16d7-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="d16d7-165">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-165">GitHub release:</span></span><br> [<span data-ttu-id="d16d7-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span><span class="sxs-lookup"><span data-stu-id="d16d7-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="d16d7-167">服務執行個體宣告</span><span class="sxs-lookup"><span data-stu-id="d16d7-167">Service instance declaration</span></span>|
|<span data-ttu-id="d16d7-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="d16d7-168">Ruby</span></span>|<span data-ttu-id="d16d7-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="d16d7-169">0.12.1</span></span><br><span data-ttu-id="d16d7-170">預覽</span><span class="sxs-lookup"><span data-stu-id="d16d7-170">Preview</span></span>|<span data-ttu-id="d16d7-171">RubyGems 套件：</span><span class="sxs-lookup"><span data-stu-id="d16d7-171">RubyGems package:</span></span><br> [<span data-ttu-id="d16d7-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span><span class="sxs-lookup"><span data-stu-id="d16d7-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="d16d7-173">GitHub 版本：</span><span class="sxs-lookup"><span data-stu-id="d16d7-173">GitHub release:</span></span><br> [<span data-ttu-id="d16d7-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span><span class="sxs-lookup"><span data-stu-id="d16d7-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="d16d7-175">連接字串設定</span><span class="sxs-lookup"><span data-stu-id="d16d7-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="d16d7-176">PHP 詳細資料</span><span class="sxs-lookup"><span data-stu-id="d16d7-176">PHP details</span></span><br><br>
><span data-ttu-id="d16d7-177">透過編輯器 tooinstall:</span><span class="sxs-lookup"><span data-stu-id="d16d7-177">tooinstall via Composer:</span></span>
>1. <span data-ttu-id="d16d7-178">建立名為`composer.json`hello hello 與下列程式碼的專案根目錄中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-178">Create a file named `composer.json` in hello root of hello project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="d16d7-179">下載[composer.phar](http://getcomposer.org/composer.phar)至 hello 專案根目錄。</span><span class="sxs-lookup"><span data-stu-id="d16d7-179">Download [composer.phar](http://getcomposer.org/composer.phar) into hello project root.</span></span>
>3. <span data-ttu-id="d16d7-180">執行：`php composer.phar install`。</span><span class="sxs-lookup"><span data-stu-id="d16d7-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="d16d7-181">端點宣告</span><span class="sxs-lookup"><span data-stu-id="d16d7-181">Endpoint declaration</span></span>
<span data-ttu-id="d16d7-182">Azure 堆疊端點包含兩個部分： hello 地區和 hello Azure 堆疊網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d16d7-182">An Azure Stack endpoint includes two parts: hello name of a region and hello Azure Stack domain.</span></span>
<span data-ttu-id="d16d7-183">在 hello Azure 堆疊開發套件，是 hello 預設端點**local.azurestack.external**。</span><span class="sxs-lookup"><span data-stu-id="d16d7-183">In hello Azure Stack Development Kit, hello default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="d16d7-184">如果不確定您的端點，請連絡您的雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d16d7-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="d16d7-185">範例</span><span class="sxs-lookup"><span data-stu-id="d16d7-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="d16d7-186">.NET</span><span class="sxs-lookup"><span data-stu-id="d16d7-186">.NET</span></span>

<span data-ttu-id="d16d7-187">針對 Azure 堆疊 hello 端點尾碼會指定在 hello app.config 檔案中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-187">For Azure Stack, hello endpoint suffix is specified in hello app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="d16d7-188">Java</span><span class="sxs-lookup"><span data-stu-id="d16d7-188">Java</span></span>

<span data-ttu-id="d16d7-189">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-189">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="d16d7-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="d16d7-190">Node.js</span></span>

<span data-ttu-id="d16d7-191">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 宣告執行個體：</span><span class="sxs-lookup"><span data-stu-id="d16d7-191">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="d16d7-192">C++</span><span class="sxs-lookup"><span data-stu-id="d16d7-192">C++</span></span>

<span data-ttu-id="d16d7-193">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-193">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="d16d7-194">PHP</span><span class="sxs-lookup"><span data-stu-id="d16d7-194">PHP</span></span>

<span data-ttu-id="d16d7-195">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-195">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="d16d7-196">Python</span><span class="sxs-lookup"><span data-stu-id="d16d7-196">Python</span></span>

<span data-ttu-id="d16d7-197">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 宣告執行個體：</span><span class="sxs-lookup"><span data-stu-id="d16d7-197">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="d16d7-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="d16d7-198">Ruby</span></span>

<span data-ttu-id="d16d7-199">針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：</span><span class="sxs-lookup"><span data-stu-id="d16d7-199">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="d16d7-200">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-200">Blob storage</span></span>

<span data-ttu-id="d16d7-201">hello 下列 Azure Blob 儲存體教學課程，適用 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d16d7-201">hello following Azure Blob storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d16d7-202">請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d16d7-202">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d16d7-203">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="d16d7-204">如何從 Java 的 Blob 儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="d16d7-204">How toouse Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="d16d7-205">如何 toouse Node.js 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-205">How toouse Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="d16d7-206">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-206">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d16d7-207">如何 toouse 來自 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-207">How toouse Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="d16d7-208">如何 toouse 來自 Python 的 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-208">How toouse Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="d16d7-209">如何 toouse Ruby 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-209">How toouse Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="d16d7-210">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-210">Queue storage</span></span>

<span data-ttu-id="d16d7-211">hello 下列 Azure 佇列儲存體教學課程，適用 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d16d7-211">hello following Azure Queue storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d16d7-212">請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d16d7-212">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d16d7-213">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="d16d7-214">如何從 Java 佇列儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="d16d7-214">How toouse Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="d16d7-215">如何 toouse 從 Node.js 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-215">How toouse Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="d16d7-216">如何 toouse 佇列儲存體從 c + +</span><span class="sxs-lookup"><span data-stu-id="d16d7-216">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="d16d7-217">如何 toouse 來自 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-217">How toouse Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="d16d7-218">如何 toouse 來自 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-218">How toouse Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="d16d7-219">如何 toouse Ruby 從佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-219">How toouse Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="d16d7-220">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-220">Table storage</span></span>

<span data-ttu-id="d16d7-221">hello 下列 Azure 資料表儲存體教學課程，適用 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d16d7-221">hello following Azure Table storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="d16d7-222">請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d16d7-222">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="d16d7-223">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="d16d7-224">如何從 Java 資料表儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="d16d7-224">How toouse Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="d16d7-225">如何 toouse 從 Node.js 的 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-225">How toouse Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="d16d7-226">如何 toouse 從 c + + 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-226">How toouse Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="d16d7-227">如何 toouse 來自 PHP 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-227">How toouse Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="d16d7-228">如何 toouse Python 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-228">How toouse Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="d16d7-229">如何 toouse Ruby 從資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-229">How toouse Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="d16d7-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d16d7-230">Next steps</span></span>

* [<span data-ttu-id="d16d7-231">簡介 tooMicrosoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="d16d7-231">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)
