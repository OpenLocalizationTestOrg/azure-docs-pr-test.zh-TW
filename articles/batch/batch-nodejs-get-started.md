---
title: "教學課程 - 使用適用於 Node.js 的 Azure Batch 用戶端程式庫 | Microsoft Docs"
description: "了解 Azure Batch 的基本概念和使用 Node.js 建置簡單的解決方案。"
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
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="f4bcb-103">開始使用適用於 Node.js 的 Batch SDK</span><span class="sxs-lookup"><span data-stu-id="f4bcb-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4bcb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f4bcb-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="f4bcb-105">Python</span><span class="sxs-lookup"><span data-stu-id="f4bcb-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="f4bcb-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f4bcb-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="f4bcb-107">了解如何使用 [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) 在 Node.js 中建置 Batch 用戶端的基本概念。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="f4bcb-108">我們會逐步了解批次應用程式的案例，然後使用 Node.js 用戶端加以設定。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f4bcb-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="f4bcb-109">Prerequisites</span></span>
<span data-ttu-id="f4bcb-110">本文假設您已具備 Node.js 的使用知識並熟悉 Linux。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="f4bcb-111">同時假設您的 Azure 帳戶設有存取權限，可建立 Batch 和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="f4bcb-112">建議您先閱讀 [Azure Batch 技術概觀](batch-technical-overview.md)，再進行本文概述的步驟。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="f4bcb-113">教學課程案例</span><span class="sxs-lookup"><span data-stu-id="f4bcb-113">The tutorial scenario</span></span>
<span data-ttu-id="f4bcb-114">讓我們一起了解 Batch 工作流程案例。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="f4bcb-115">我們有以 Python 撰寫的簡單指令碼，可從 Azure Blob 儲存體容器下載所有 csv 檔案並將它們轉換成 JSON。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="f4bcb-116">若要平行處理多個儲存體帳戶容器，我們可以將此指令碼部署為 Azure Batch 作業。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="f4bcb-117">Azure Batch 架構</span><span class="sxs-lookup"><span data-stu-id="f4bcb-117">Azure Batch Architecture</span></span>
<span data-ttu-id="f4bcb-118">下圖描述如何使用 Azure Batch 和 Node.js 用戶端調整 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch 案例](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="f4bcb-120">Node.js 用戶端會使用準備工作部署批次作業 (稍後詳細說明) 以及一組工作 (視儲存體帳戶中容器數目)。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="f4bcb-121">您可以從 GitHub 存放庫下載指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="f4bcb-122">Node.js 用戶端</span><span class="sxs-lookup"><span data-stu-id="f4bcb-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="f4bcb-123">準備工作 Shell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f4bcb-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="f4bcb-124">Python csv 至 JSON 處理器</span><span class="sxs-lookup"><span data-stu-id="f4bcb-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="f4bcb-125">指定連結中的 Node.js 用戶端不包含要部署為 Azure 函式應用程式的特定程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="f4bcb-126">您可以參考下列連結，以取得建立函式應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-126">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="f4bcb-127">建立函式應用程式</span><span class="sxs-lookup"><span data-stu-id="f4bcb-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="f4bcb-128">建立計時器觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="f4bcb-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="f4bcb-129">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="f4bcb-129">Build the application</span></span>

<span data-ttu-id="f4bcb-130">現在，我們要依照程序逐步建置 Node.js 用戶端︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="f4bcb-131">步驟 1：安裝 Azure Batch SDK</span><span class="sxs-lookup"><span data-stu-id="f4bcb-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="f4bcb-132">您可以使用 npm 安裝命令來安裝適用於 Node.js 的 Azure Batch SDK。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="f4bcb-133">此命令會安裝最新版的 azure-batch 節點 SDK。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="f4bcb-134">在 Azure Function 應用程式中，您可以移至 Azure Function 的 [設定] 索引標籤中的 [Kudu 主控台] 以執行 npm 安裝命令。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="f4bcb-135">在此情況下，安裝適用於 Node.js 的 Azure Batch SDK。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="f4bcb-136">步驟 2：建立 Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="f4bcb-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="f4bcb-137">您可以從 [Azure 入口網站](batch-account-create-portal.md)或從命令列 ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)) 加以建立。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="f4bcb-138">以下是透過 Azure CLI 命令建立 Batch 帳戶的命令。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="f4bcb-139">建立資源群組，如果您想要建立 Batch 帳戶的地方已經有一個，請略過此步驟︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="f4bcb-140">接下來，建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="f4bcb-141">每個 Batch 帳戶有其對應的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="f4bcb-142">需要有這些金鑰，才能在 Azure Batch 帳戶中建立進一步的資源。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="f4bcb-143">在生產環境中，最好使用 Azure Key Vault 來儲存這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="f4bcb-144">然後您可以建立應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="f4bcb-145">使用此服務主體，應用程式可以建立 OAuth 權杖以存取 Key Vault 中的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="f4bcb-146">複製並儲存要在後續步驟中使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="f4bcb-147">步驟 3︰建立 Azure Batch 服務用戶端</span><span class="sxs-lookup"><span data-stu-id="f4bcb-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="f4bcb-148">下列程式碼片段會先匯入 azure-batch Node.js 模組，然後建立 Batch 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="f4bcb-149">您必須先使用從上一個步驟複製的 Batch 帳戶金鑰來建立 SharedKeyCredentials 物件。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

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

<span data-ttu-id="f4bcb-150">在 Azure 入口網站的 [概觀] 索引標籤中可以找到 Azure Batch URI。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="f4bcb-151">其格式如下︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="f4bcb-152">請參考螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="f4bcb-152">Refer to the screenshot:</span></span>

![Azure Batch URI](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="f4bcb-154">步驟 4︰建立 Azure Batch 集區</span><span class="sxs-lookup"><span data-stu-id="f4bcb-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="f4bcb-155">Azure Batch 集區是由多個 VM (也稱為 Batch 節點) 所組成。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="f4bcb-156">Azure Batch 服務會在這些節點上部署工作並加以管理。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="f4bcb-157">您可以為您的集區定義下列組態參數。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="f4bcb-158">虛擬機器映像的類型</span><span class="sxs-lookup"><span data-stu-id="f4bcb-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="f4bcb-159">虛擬機器節點的大小</span><span class="sxs-lookup"><span data-stu-id="f4bcb-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="f4bcb-160">虛擬機器節點的數目</span><span class="sxs-lookup"><span data-stu-id="f4bcb-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="f4bcb-161">虛擬機器節點的大小和數目主要取決於您想要平行執行的工作數目以及工作本身。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="f4bcb-162">我們建議進行測試，以判斷理想的數目和大小。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="f4bcb-163">下列程式碼片段會建立組態參數物件。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="f4bcb-164">如需 Azure Batch 及其 SKU 識別碼可用的 Linux VM 映像清單，請參閱[虛擬機器映像清單](batch-linux-nodes.md#list-of-virtual-machine-images)。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="f4bcb-165">一旦定義集區組態，您就可以建立 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="f4bcb-166">Batch 集區命令會建立 Azure 虛擬機器節點，並備妥它們以便用於接收要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="f4bcb-167">每個集區都應該有後續步驟中參考的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="f4bcb-168">下列程式碼片段會建立 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="f4bcb-169">您可以檢查已建立的集區狀態，先確定狀態處於「作用中」，再繼續將作業提交至該集區。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

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

<span data-ttu-id="f4bcb-170">以下是 pool.get 函式所傳回的範例結果物件。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-170">Following is a sample result object returned by the pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="f4bcb-171">步驟 4︰提交 Azure Batch 作業</span><span class="sxs-lookup"><span data-stu-id="f4bcb-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="f4bcb-172">Azure Batch 作業是相似工作的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="f4bcb-173">在我們的案例中，這是「將 csv 處理成 JSON」。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="f4bcb-174">這裡的每個工作都可能會處理每個 Azure 儲存體容器中存在的 csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="f4bcb-175">這些工作會以平行方式執行並且部署於多個節點 (由 Azure Batch 服務協調)。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="f4bcb-176">您可以使用 [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 屬性來指定可以在單一節點上同時執行的工作數目上限。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="f4bcb-177">準備工作</span><span class="sxs-lookup"><span data-stu-id="f4bcb-177">Preparation task</span></span>

<span data-ttu-id="f4bcb-178">建立的 VM 節點是空白的 Ubuntu 節點。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="f4bcb-179">您通常需要安裝一組程式作為必要條件。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="f4bcb-180">一般來說，對於 Linux 節點，您可以有在實際工作執行前安裝先決條件的殼層指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="f4bcb-181">不過，它可能是任何可程式化的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="f4bcb-182">此範例中的[殼層指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh)會安裝 Python-pip 和適用於 Python 的 Azure 儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="f4bcb-183">您可以在 Azure 儲存體帳戶上傳指令碼，並產生 SAS URI 來存取指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="f4bcb-184">使用 Azure 儲存體 Node.js SDK 也可以自動執行此程序。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="f4bcb-185">作業的準備工作只會在需要執行特定工作的 VM 節點上執行。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="f4bcb-186">如果您想要在所有節點上安裝必要條件 (不管其上執行的工作為何)，可以在新增集區時使用 [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) 屬性。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="f4bcb-187">您可以使用下列準備工作定義以供參考。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="f4bcb-188">準備工作是在 Azure Batch 作業提交期間指定。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="f4bcb-189">以下是準備工作組態參數︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="f4bcb-190">**識別碼**︰準備工作的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="f4bcb-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="f4bcb-191">**命令列**︰要執行工作可執行檔的命令列</span><span class="sxs-lookup"><span data-stu-id="f4bcb-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="f4bcb-192">**resourceFiles**︰提供執行此工作所需下載之檔案詳細資料的物件陣列。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="f4bcb-193">其選項如下：</span><span class="sxs-lookup"><span data-stu-id="f4bcb-193">Following are its options</span></span>
    - <span data-ttu-id="f4bcb-194">blobSource︰檔案的 SAS URI</span><span class="sxs-lookup"><span data-stu-id="f4bcb-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="f4bcb-195">filePath︰要下載並儲存檔案的本機路徑</span><span class="sxs-lookup"><span data-stu-id="f4bcb-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="f4bcb-196">fileMode︰僅適用於 Linux 節點，fileMode 為八進位格式 (預設值是 0770)</span><span class="sxs-lookup"><span data-stu-id="f4bcb-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="f4bcb-197">**waitForSuccess**︰如果設為 true，此工作不會在準備工作失敗時執行</span><span class="sxs-lookup"><span data-stu-id="f4bcb-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="f4bcb-198">**runElevated**︰如果需要提高的權限才能執行工作，請將它設定為 true。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="f4bcb-199">下列程式碼片段顯示準備工作指令碼組態範例︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="f4bcb-200">如果不需安裝任何必要條件，您的工作即可執行，您可以略過準備工作。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="f4bcb-201">下列程式碼會建立一項作業，其顯示名稱為「處理 csv 檔案」。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="f4bcb-202">步驟 5︰提交作業的 Azure 批次工作</span><span class="sxs-lookup"><span data-stu-id="f4bcb-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="f4bcb-203">現在已建立處理 csv 作業，讓我們為該作業建立工作。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="f4bcb-204">假設我們有四個容器，我們必須建立四項工作，每個容器一項工作。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="f4bcb-205">如果我們查看 [Python 指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py)，它接受兩個參數︰</span><span class="sxs-lookup"><span data-stu-id="f4bcb-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="f4bcb-206">容器名稱︰要從中下載檔案的儲存體容器</span><span class="sxs-lookup"><span data-stu-id="f4bcb-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="f4bcb-207">模式︰檔案名稱模式的選擇性參數</span><span class="sxs-lookup"><span data-stu-id="f4bcb-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="f4bcb-208">假設我們有四個容器 "con1"、"con2"、"con3"、"con4"，下列程式碼顯示如何將工作提交至我們稍早建立的 Azure 批次作業「處理 csv」。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="f4bcb-209">此程式碼會將多個工作新增至集區。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="f4bcb-210">而每項工作會在所建立 VM 集區中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="f4bcb-211">如果工作數目超過集區或 maxTasksPerNode 屬性中的 VM 數目，工作會等到節點可用為止。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="f4bcb-212">Azure Batch 會自動處理此協調流程。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="f4bcb-213">入口網站有工作與作業狀態的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="f4bcb-214">您也可以使用此清單並取得 Azure 節點 SDK 中的函式。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="f4bcb-215">文件[連結](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html)中會提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4bcb-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4bcb-216">Next steps</span></span>

- <span data-ttu-id="f4bcb-217">如果您不熟悉這項服務，我們建議檢閱 [Azure Batch 功能概觀](batch-api-basics.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="f4bcb-218">請參閱 [Batch Node.js 參考](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)以探索 Batch API。</span><span class="sxs-lookup"><span data-stu-id="f4bcb-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

