---
title: "aaaTutorial-使用 hello Azure 批次用戶端程式庫 for Node.js |Microsoft 文件"
description: "了解 hello Azure Batch 基本概念，並建立簡單的解決方案使用 Node.js。"
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="f52e6-103">開始使用適用於 Node.js 的 Batch SDK</span><span class="sxs-lookup"><span data-stu-id="f52e6-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f52e6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f52e6-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="f52e6-105">Python</span><span class="sxs-lookup"><span data-stu-id="f52e6-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="f52e6-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f52e6-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="f52e6-107">了解建立批次中的用戶端使用 Node.js 的 hello 基本概念[Azure 批次 Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)。</span><span class="sxs-lookup"><span data-stu-id="f52e6-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="f52e6-108">我們會逐步了解批次應用程式的案例，然後使用 Node.js 用戶端加以設定。</span><span class="sxs-lookup"><span data-stu-id="f52e6-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f52e6-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="f52e6-109">Prerequisites</span></span>
<span data-ttu-id="f52e6-110">本文假設您已具備 Node.js 的使用知識並熟悉 Linux。</span><span class="sxs-lookup"><span data-stu-id="f52e6-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="f52e6-111">它也假設您有存取權限 toocreate 批次和儲存體服務的 Azure 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="f52e6-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="f52e6-112">建議您閱讀[Azure 批次技術概觀](batch-technical-overview.md)您瀏覽之前 hello 步驟所述這篇文章。</span><span class="sxs-lookup"><span data-stu-id="f52e6-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="f52e6-113">hello 教學課程案例</span><span class="sxs-lookup"><span data-stu-id="f52e6-113">hello tutorial scenario</span></span>
<span data-ttu-id="f52e6-114">讓我們了解 hello 批次工作流程的案例。</span><span class="sxs-lookup"><span data-stu-id="f52e6-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="f52e6-115">我們有簡單的指令碼，以撰寫的 Python 下載所有 csv 檔案的 Azure Blob 儲存體容器 tooJSON 需要進行轉換。</span><span class="sxs-lookup"><span data-stu-id="f52e6-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="f52e6-116">tooprocess 多個儲存體帳戶容器以平行方式時，我們可以部署以 Azure 批次作業的形式 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="f52e6-117">Azure Batch 架構</span><span class="sxs-lookup"><span data-stu-id="f52e6-117">Azure Batch Architecture</span></span>
<span data-ttu-id="f52e6-118">hello 下列圖表描述我們可以調整使用 Azure 批次和 Node.js 用戶端 hello Python 指令碼的方式。</span><span class="sxs-lookup"><span data-stu-id="f52e6-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch 案例](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="f52e6-120">hello node.js 用戶端會將批次工作部署的準備工作 （稍後說明的詳細資料），以及一組工作，而是根據 hello hello 儲存體帳戶中容器的數目。</span><span class="sxs-lookup"><span data-stu-id="f52e6-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="f52e6-121">您可以從 hello github 儲存機制下載 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="f52e6-122">Node.js 用戶端</span><span class="sxs-lookup"><span data-stu-id="f52e6-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="f52e6-123">準備工作 Shell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f52e6-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="f52e6-124">Python csv tooJSON 處理器</span><span class="sxs-lookup"><span data-stu-id="f52e6-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="f52e6-125">指定的 hello 連結中的 hello Node.js client 不包含部署為 Azure 函式應用程式的特定程式碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="f52e6-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="f52e6-126">您可以參考 toohello 下列其中一個指示 toocreate 的連結。</span><span class="sxs-lookup"><span data-stu-id="f52e6-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="f52e6-127">建立函式應用程式</span><span class="sxs-lookup"><span data-stu-id="f52e6-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="f52e6-128">建立計時器觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="f52e6-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="f52e6-129">建置 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="f52e6-129">Build hello application</span></span>

<span data-ttu-id="f52e6-130">現在，讓我們遵循 hello 程序逐步解說到建置 hello Node.js 用戶端：</span><span class="sxs-lookup"><span data-stu-id="f52e6-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="f52e6-131">步驟 1：安裝 Azure Batch SDK</span><span class="sxs-lookup"><span data-stu-id="f52e6-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="f52e6-132">您可以安裝 Azure 批次 SDK for Node.js 使用 hello npm install 命令。</span><span class="sxs-lookup"><span data-stu-id="f52e6-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="f52e6-133">此命令會安裝 hello azure 批次節點 SDK 最新版本。</span><span class="sxs-lookup"><span data-stu-id="f52e6-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="f52e6-134">在 Azure 函式應用程式，您可以跳過 「 Kudu 主控台 」 中 hello Azure 函式的設定 索引標籤 toorun hello npm 安裝命令。</span><span class="sxs-lookup"><span data-stu-id="f52e6-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="f52e6-135">在此案例 tooinstall Azure 批次 SDK for Node.js。</span><span class="sxs-lookup"><span data-stu-id="f52e6-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="f52e6-136">步驟 2：建立 Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="f52e6-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="f52e6-137">您可以建立從 hello [Azure 入口網站](batch-account-create-portal.md)或從命令列 ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview))。</span><span class="sxs-lookup"><span data-stu-id="f52e6-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="f52e6-138">以下是 hello 命令 toocreate 一個透過 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f52e6-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="f52e6-139">建立資源群組，請略過此步驟，如果您已經有想 toocreate hello Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="f52e6-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="f52e6-140">接下來，建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f52e6-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="f52e6-141">每個 Batch 帳戶有其對應的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f52e6-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="f52e6-142">這些索引鍵是所需的 toocreate 進一步 Azure 批次帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="f52e6-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="f52e6-143">實際執行環境的好作法是 toouse Azure 金鑰保存庫 toostore 這些機碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="f52e6-144">然後您可以建立服務主體的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52e6-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="f52e6-145">使用此服務主體的 hello 應用程式可以從 hello 金鑰保存庫中建立的 OAuth 語彙基元 tooaccess 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f52e6-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="f52e6-146">複製並儲存 hello 金鑰 toobe hello 後續步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="f52e6-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="f52e6-147">步驟 3︰建立 Azure Batch 服務用戶端</span><span class="sxs-lookup"><span data-stu-id="f52e6-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="f52e6-148">下列程式碼片段會先匯入 hello azure 批次 Node.js 模組，並接著會建立批次服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="f52e6-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="f52e6-149">您需要 toofirst SharedKeyCredentials 物件建立 hello hello 以上一個步驟複製的批次帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="f52e6-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="f52e6-150">hello hello Azure 入口網站的 [概觀] 索引標籤中，可以找到 hello Azure 批次的 URI。</span><span class="sxs-lookup"><span data-stu-id="f52e6-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="f52e6-151">它是 hello 格式：</span><span class="sxs-lookup"><span data-stu-id="f52e6-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="f52e6-152">Toohello 螢幕擷取畫面，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f52e6-152">Refer toohello screenshot:</span></span>

![Azure Batch URI](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="f52e6-154">步驟 4︰建立 Azure Batch 集區</span><span class="sxs-lookup"><span data-stu-id="f52e6-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="f52e6-155">Azure Batch 集區是由多個 VM (也稱為 Batch 節點) 所組成。</span><span class="sxs-lookup"><span data-stu-id="f52e6-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="f52e6-156">Azure 批次服務將部署兩個節點上的 hello 工作和管理它們。</span><span class="sxs-lookup"><span data-stu-id="f52e6-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="f52e6-157">您可以定義 hello 遵循您的集區的組態參數。</span><span class="sxs-lookup"><span data-stu-id="f52e6-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="f52e6-158">虛擬機器映像的類型</span><span class="sxs-lookup"><span data-stu-id="f52e6-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="f52e6-159">虛擬機器節點的大小</span><span class="sxs-lookup"><span data-stu-id="f52e6-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="f52e6-160">虛擬機器節點的數目</span><span class="sxs-lookup"><span data-stu-id="f52e6-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="f52e6-161">hello 大小和虛擬機器的節點數目主要取決於您想要在 toorun 平行和也 hello 工作本身的工作的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f52e6-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="f52e6-162">我們建議您測試 toodetermine hello 理想數目和大小。</span><span class="sxs-lookup"><span data-stu-id="f52e6-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="f52e6-163">hello 下列程式碼片段會建立 hello 組態參數物件。</span><span class="sxs-lookup"><span data-stu-id="f52e6-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="f52e6-164">Linux VM 映像可供 Azure 批次和其 SKU 識別碼 hello 清單，請參閱[的虛擬機器映像清單](batch-linux-nodes.md#list-of-virtual-machine-images)。</span><span class="sxs-lookup"><span data-stu-id="f52e6-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="f52e6-165">一旦定義 hello 集區設定之後，您可以建立 hello Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="f52e6-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="f52e6-166">hello 批次集區的命令會建立 Azure 虛擬機器的節點，並以準備讓 toobe 準備 tooreceive 工作 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="f52e6-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="f52e6-167">每個集區都應該有後續步驟中參考的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="f52e6-168">下列程式碼片段的 hello 建立 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="f52e6-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="f52e6-169">您可以檢查 hello hello 建立集區的狀態，並請確認 hello 狀態處於 「 作用中 」 之前繼續進行送出工作 toothat 集區。</span><span class="sxs-lookup"><span data-stu-id="f52e6-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="f52e6-170">以下是 hello pool.get 函數所傳回的範例結果物件。</span><span class="sxs-lookup"><span data-stu-id="f52e6-170">Following is a sample result object returned by hello pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="f52e6-171">步驟 4︰提交 Azure Batch 作業</span><span class="sxs-lookup"><span data-stu-id="f52e6-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="f52e6-172">Azure Batch 作業是相似工作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="f52e6-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="f52e6-173">在我們的案例，它是 「"處理程序 csv tooJSON。</span><span class="sxs-lookup"><span data-stu-id="f52e6-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="f52e6-174">這裡的每個工作都可能會處理每個 Azure 儲存體容器中存在的 csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="f52e6-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="f52e6-175">這些工作會以平行方式執行，並部署到多個節點，由 hello Azure 批次服務協調。</span><span class="sxs-lookup"><span data-stu-id="f52e6-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="f52e6-176">您可以使用 hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add)屬性 toospecify 最大數目的單一節點可同時執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f52e6-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="f52e6-177">準備工作</span><span class="sxs-lookup"><span data-stu-id="f52e6-177">Preparation task</span></span>

<span data-ttu-id="f52e6-178">建立 hello VM 節點是空白的 Ubuntu 節點。</span><span class="sxs-lookup"><span data-stu-id="f52e6-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="f52e6-179">通常，您需要一組程式 tooinstall 做為必要條件。</span><span class="sxs-lookup"><span data-stu-id="f52e6-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="f52e6-180">一般而言，Linux 節點，您可以讓安裝 hello 必要條件 hello 實際執行的工作之前的殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="f52e6-181">不過，它可能是任何可程式化的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f52e6-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="f52e6-182">hello[殼層指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh)在此範例中會安裝 Python pip 和 hello Azure 儲存體 SDK for Python。</span><span class="sxs-lookup"><span data-stu-id="f52e6-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="f52e6-183">您可以上傳至 Azure 儲存體帳戶上的 hello 指令碼，以及產生 SAS URI tooaccess hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f52e6-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="f52e6-184">此程序也可以使用 Azure 儲存體 Node.js SDK hello 進行自動化。</span><span class="sxs-lookup"><span data-stu-id="f52e6-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="f52e6-185">作業的準備工作只會在執行 hello VM 節點 hello 特定工作需要 toorun 的地方。</span><span class="sxs-lookup"><span data-stu-id="f52e6-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="f52e6-186">如果您希望不論 hello 工作在其上執行的所有節點上安裝的必要條件 toobe，您可以使用 hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add)加入集區時的屬性。</span><span class="sxs-lookup"><span data-stu-id="f52e6-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="f52e6-187">您可以使用下列參考的準備工作定義的 hello。</span><span class="sxs-lookup"><span data-stu-id="f52e6-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="f52e6-188">Azure 批次工作 hello 提交期間指定準備工作。</span><span class="sxs-lookup"><span data-stu-id="f52e6-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="f52e6-189">下列是 hello 準備工作組態參數：</span><span class="sxs-lookup"><span data-stu-id="f52e6-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="f52e6-190">**識別碼**: hello 準備工作的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="f52e6-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="f52e6-191">**commandLine**： 命令列 tooexecute hello 工作可執行檔</span><span class="sxs-lookup"><span data-stu-id="f52e6-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="f52e6-192">**resourceFiles**： 提供檔案的詳細資料的物件陣列所需下載此工作 toorun toobe。</span><span class="sxs-lookup"><span data-stu-id="f52e6-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="f52e6-193">其選項如下：</span><span class="sxs-lookup"><span data-stu-id="f52e6-193">Following are its options</span></span>
    - <span data-ttu-id="f52e6-194">blobSource: hello hello 檔案的 SAS URI</span><span class="sxs-lookup"><span data-stu-id="f52e6-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="f52e6-195">filePath： 本機路徑 toodownload 儲存 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="f52e6-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="f52e6-196">fileMode︰僅適用於 Linux 節點，fileMode 為八進位格式 (預設值是 0770)</span><span class="sxs-lookup"><span data-stu-id="f52e6-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="f52e6-197">**waitForSuccess**： 如果組 tootrue，hello 工作不會執行準備工作失敗</span><span class="sxs-lookup"><span data-stu-id="f52e6-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="f52e6-198">**runElevated**： 設定 tootrue 提高的權限時所需的 toorun hello 工作。</span><span class="sxs-lookup"><span data-stu-id="f52e6-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="f52e6-199">下列程式碼片段顯示 hello 準備工作的指令碼組態範例：</span><span class="sxs-lookup"><span data-stu-id="f52e6-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="f52e6-200">如果不沒有針對工作 toorun 安裝任何必要條件 toobe，您可以略過 hello 準備工作。</span><span class="sxs-lookup"><span data-stu-id="f52e6-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="f52e6-201">下列程式碼會建立一項作業，其顯示名稱為「處理 csv 檔案」。</span><span class="sxs-lookup"><span data-stu-id="f52e6-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="f52e6-202">步驟 5︰提交作業的 Azure 批次工作</span><span class="sxs-lookup"><span data-stu-id="f52e6-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="f52e6-203">現在已建立處理 csv 作業，讓我們為該作業建立工作。</span><span class="sxs-lookup"><span data-stu-id="f52e6-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="f52e6-204">我們假設我們有四個容器，有 toocreate 四項工作，每個容器一個。</span><span class="sxs-lookup"><span data-stu-id="f52e6-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="f52e6-205">如果看一下 hello [Python 指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py)，它接受兩個參數：</span><span class="sxs-lookup"><span data-stu-id="f52e6-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="f52e6-206">容器名稱： hello 從儲存體容器 toodownload 檔案</span><span class="sxs-lookup"><span data-stu-id="f52e6-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="f52e6-207">模式︰檔案名稱模式的選擇性參數</span><span class="sxs-lookup"><span data-stu-id="f52e6-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="f52e6-208">假設我們有四個容器"con1"、"con2"、"con3"，"con4"下列程式碼送出工作 toohello Azure 批次作業 」 程序 csv 「 我們稍早建立的顯示。</span><span class="sxs-lookup"><span data-stu-id="f52e6-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="f52e6-209">hello 程式碼加入多個工作 toohello 集區。</span><span class="sxs-lookup"><span data-stu-id="f52e6-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="f52e6-210">而每個 hello 工作 hello 的 Vm 建立的集區中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="f52e6-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="f52e6-211">如果 hello 工作數目超過 hello Vm 數目在集區或 hello maxTasksPerNode 屬性中的，hello 工作等候節點可用。</span><span class="sxs-lookup"><span data-stu-id="f52e6-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="f52e6-212">Azure Batch 會自動處理此協調流程。</span><span class="sxs-lookup"><span data-stu-id="f52e6-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="f52e6-213">hello 入口網站有詳細 hello 工作和工作狀態的檢視。</span><span class="sxs-lookup"><span data-stu-id="f52e6-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="f52e6-214">您也可以使用 hello 清單，並在 hello Azure 節點 SDK 中取得函式。</span><span class="sxs-lookup"><span data-stu-id="f52e6-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="f52e6-215">Hello 文件中提供詳細資料[連結](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html)。</span><span class="sxs-lookup"><span data-stu-id="f52e6-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f52e6-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f52e6-216">Next steps</span></span>

- <span data-ttu-id="f52e6-217">檢閱 hello [Azure Batch 概觀功能](batch-api-basics.md)發行項，我們建議您是否新增 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="f52e6-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="f52e6-218">請參閱 hello[批次 Node.js 參考](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)tooexplore hello 批次 API。</span><span class="sxs-lookup"><span data-stu-id="f52e6-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

