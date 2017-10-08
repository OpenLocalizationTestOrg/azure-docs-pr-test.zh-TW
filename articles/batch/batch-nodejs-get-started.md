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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>開始使用適用於 Node.js 的 Batch SDK

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

了解建立批次中的用戶端使用 Node.js 的 hello 基本概念[Azure 批次 Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)。 我們會逐步了解批次應用程式的案例，然後使用 Node.js 用戶端加以設定。  

## <a name="prerequisites"></a>必要條件
本文假設您已具備 Node.js 的使用知識並熟悉 Linux。 它也假設您有存取權限 toocreate 批次和儲存體服務的 Azure 帳戶設定。

建議您閱讀[Azure 批次技術概觀](batch-technical-overview.md)您瀏覽之前 hello 步驟所述這篇文章。

## <a name="hello-tutorial-scenario"></a>hello 教學課程案例
讓我們了解 hello 批次工作流程的案例。 我們有簡單的指令碼，以撰寫的 Python 下載所有 csv 檔案的 Azure Blob 儲存體容器 tooJSON 需要進行轉換。 tooprocess 多個儲存體帳戶容器以平行方式時，我們可以部署以 Azure 批次作業的形式 hello 指令碼。

## <a name="azure-batch-architecture"></a>Azure Batch 架構
hello 下列圖表描述我們可以調整使用 Azure 批次和 Node.js 用戶端 hello Python 指令碼的方式。

![Azure Batch 案例](./media/batch-nodejs-get-started/BatchScenario.png)

hello node.js 用戶端會將批次工作部署的準備工作 （稍後說明的詳細資料），以及一組工作，而是根據 hello hello 儲存體帳戶中容器的數目。 您可以從 hello github 儲存機制下載 hello 指令碼。

* [Node.js 用戶端](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [準備工作 Shell 指令碼](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Python csv tooJSON 處理器](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> 指定的 hello 連結中的 hello Node.js client 不包含部署為 Azure 函式應用程式的特定程式碼 toobe。 您可以參考 toohello 下列其中一個指示 toocreate 的連結。
> - [建立函式應用程式](../azure-functions/functions-create-first-azure-function.md)
> - [建立計時器觸發程序函式](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>建置 hello 應用程式

現在，讓我們遵循 hello 程序逐步解說到建置 hello Node.js 用戶端：

### <a name="step-1-install-azure-batch-sdk"></a>步驟 1：安裝 Azure Batch SDK

您可以安裝 Azure 批次 SDK for Node.js 使用 hello npm install 命令。

`npm install azure-batch`

此命令會安裝 hello azure 批次節點 SDK 最新版本。

>[!Tip]
> 在 Azure 函式應用程式，您可以跳過 「 Kudu 主控台 」 中 hello Azure 函式的設定 索引標籤 toorun hello npm 安裝命令。 在此案例 tooinstall Azure 批次 SDK for Node.js。
>
>

### <a name="step-2-create-an-azure-batch-account"></a>步驟 2：建立 Azure Batch 帳戶

您可以建立從 hello [Azure 入口網站](batch-account-create-portal.md)或從命令列 ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview))。

以下是 hello 命令 toocreate 一個透過 Azure CLI。

建立資源群組，請略過此步驟，如果您已經有想 toocreate hello Batch 帳戶：

`az group create -n "<resource-group-name>" -l "<location>"`

接下來，建立 Azure Batch 帳戶。

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

每個 Batch 帳戶有其對應的存取金鑰。 這些索引鍵是所需的 toocreate 進一步 Azure 批次帳戶中的資源。 實際執行環境的好作法是 toouse Azure 金鑰保存庫 toostore 這些機碼。 然後您可以建立服務主體的 hello 應用程式。 使用此服務主體的 hello 應用程式可以從 hello 金鑰保存庫中建立的 OAuth 語彙基元 tooaccess 索引鍵。

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

複製並儲存 hello 金鑰 toobe hello 後續步驟中使用。

### <a name="step-3-create-an-azure-batch-service-client"></a>步驟 3︰建立 Azure Batch 服務用戶端
下列程式碼片段會先匯入 hello azure 批次 Node.js 模組，並接著會建立批次服務用戶端。 您需要 toofirst SharedKeyCredentials 物件建立 hello hello 以上一個步驟複製的批次帳戶金鑰。

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

hello hello Azure 入口網站的 [概觀] 索引標籤中，可以找到 hello Azure 批次的 URI。 它是 hello 格式：

`https://accountname.location.batch.azure.com`

Toohello 螢幕擷取畫面，請參閱：

![Azure Batch URI](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>步驟 4︰建立 Azure Batch 集區
Azure Batch 集區是由多個 VM (也稱為 Batch 節點) 所組成。 Azure 批次服務將部署兩個節點上的 hello 工作和管理它們。 您可以定義 hello 遵循您的集區的組態參數。

* 虛擬機器映像的類型
* 虛擬機器節點的大小
* 虛擬機器節點的數目

> [!Tip]
> hello 大小和虛擬機器的節點數目主要取決於您想要在 toorun 平行和也 hello 工作本身的工作的 hello 數目。 我們建議您測試 toodetermine hello 理想數目和大小。
>
>

hello 下列程式碼片段會建立 hello 組態參數物件。

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
> Linux VM 映像可供 Azure 批次和其 SKU 識別碼 hello 清單，請參閱[的虛擬機器映像清單](batch-linux-nodes.md#list-of-virtual-machine-images)。
>
>

一旦定義 hello 集區設定之後，您可以建立 hello Azure Batch 集區。 hello 批次集區的命令會建立 Azure 虛擬機器的節點，並以準備讓 toobe 準備 tooreceive 工作 tooexecute。 每個集區都應該有後續步驟中參考的唯一識別碼。

下列程式碼片段的 hello 建立 Azure Batch 集區。

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

您可以檢查 hello hello 建立集區的狀態，並請確認 hello 狀態處於 「 作用中 」 之前繼續進行送出工作 toothat 集區。

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

以下是 hello pool.get 函數所傳回的範例結果物件。

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


### <a name="step-4-submit-an-azure-batch-job"></a>步驟 4︰提交 Azure Batch 作業
Azure Batch 作業是相似工作的邏輯群組。 在我們的案例，它是 「"處理程序 csv tooJSON。 這裡的每個工作都可能會處理每個 Azure 儲存體容器中存在的 csv 檔案。

這些工作會以平行方式執行，並部署到多個節點，由 hello Azure 批次服務協調。

> [!Tip]
> 您可以使用 hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add)屬性 toospecify 最大數目的單一節點可同時執行的工作。
>
>

#### <a name="preparation-task"></a>準備工作

建立 hello VM 節點是空白的 Ubuntu 節點。 通常，您需要一組程式 tooinstall 做為必要條件。
一般而言，Linux 節點，您可以讓安裝 hello 必要條件 hello 實際執行的工作之前的殼層指令碼。 不過，它可能是任何可程式化的可執行檔。
hello[殼層指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh)在此範例中會安裝 Python pip 和 hello Azure 儲存體 SDK for Python。

您可以上傳至 Azure 儲存體帳戶上的 hello 指令碼，以及產生 SAS URI tooaccess hello 指令碼。 此程序也可以使用 Azure 儲存體 Node.js SDK hello 進行自動化。

> [!Tip]
> 作業的準備工作只會在執行 hello VM 節點 hello 特定工作需要 toorun 的地方。 如果您希望不論 hello 工作在其上執行的所有節點上安裝的必要條件 toobe，您可以使用 hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add)加入集區時的屬性。 您可以使用下列參考的準備工作定義的 hello。
>
>

Azure 批次工作 hello 提交期間指定準備工作。 下列是 hello 準備工作組態參數：

* **識別碼**: hello 準備工作的唯一識別碼
* **commandLine**： 命令列 tooexecute hello 工作可執行檔
* **resourceFiles**： 提供檔案的詳細資料的物件陣列所需下載此工作 toorun toobe。  其選項如下：
    - blobSource: hello hello 檔案的 SAS URI
    - filePath： 本機路徑 toodownload 儲存 hello 檔案
    - fileMode︰僅適用於 Linux 節點，fileMode 為八進位格式 (預設值是 0770)
* **waitForSuccess**： 如果組 tootrue，hello 工作不會執行準備工作失敗
* **runElevated**： 設定 tootrue 提高的權限時所需的 toorun hello 工作。

下列程式碼片段顯示 hello 準備工作的指令碼組態範例：

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

如果不沒有針對工作 toorun 安裝任何必要條件 toobe，您可以略過 hello 準備工作。 下列程式碼會建立一項作業，其顯示名稱為「處理 csv 檔案」。

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>步驟 5︰提交作業的 Azure 批次工作

現在已建立處理 csv 作業，讓我們為該作業建立工作。 我們假設我們有四個容器，有 toocreate 四項工作，每個容器一個。

如果看一下 hello [Python 指令碼](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py)，它接受兩個參數：

* 容器名稱： hello 從儲存體容器 toodownload 檔案
* 模式︰檔案名稱模式的選擇性參數

假設我們有四個容器"con1"、"con2"、"con3"，"con4"下列程式碼送出工作 toohello Azure 批次作業 」 程序 csv 「 我們稍早建立的顯示。

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

hello 程式碼加入多個工作 toohello 集區。 而每個 hello 工作 hello 的 Vm 建立的集區中的節點上執行。 如果 hello 工作數目超過 hello Vm 數目在集區或 hello maxTasksPerNode 屬性中的，hello 工作等候節點可用。 Azure Batch 會自動處理此協調流程。

hello 入口網站有詳細 hello 工作和工作狀態的檢視。 您也可以使用 hello 清單，並在 hello Azure 節點 SDK 中取得函式。 Hello 文件中提供詳細資料[連結](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html)。

## <a name="next-steps"></a>後續步驟

- 檢閱 hello [Azure Batch 概觀功能](batch-api-basics.md)發行項，我們建議您是否新增 toohello 服務。
- 請參閱 hello[批次 Node.js 參考](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/)tooexplore hello 批次 API。

