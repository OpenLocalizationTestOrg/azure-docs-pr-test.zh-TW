---
title: "機器學習批次執行服務作業的容量 aaaDedicated |Microsoft 文件"
description: "適用於 Machine Learning 作業的 Azure Batch 服務概觀。"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="7f79e-103">適用於 Machine Learning 作業的 Azure Batch 服務</span><span class="sxs-lookup"><span data-stu-id="7f79e-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="7f79e-104">機器學習批次集區處理 hello Azure 機器學習批次執行服務可提供客戶管理的小數位數。</span><span class="sxs-lookup"><span data-stu-id="7f79e-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="7f79e-105">機器學習的傳統批次處理發生在多租用戶環境中，並行處理作業，您可以提交，且作業哪些限制 hello 數目會排入佇列以先進先出為基礎。</span><span class="sxs-lookup"><span data-stu-id="7f79e-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="7f79e-106">這種不確定性，表示您無法準確地預測何時會執行您的作業。</span><span class="sxs-lookup"><span data-stu-id="7f79e-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="7f79e-107">批次集區處理可讓您 toocreate 集區，您可以提交批次作業。</span><span class="sxs-lookup"><span data-stu-id="7f79e-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="7f79e-108">控制 hello hello 集區的大小，而且 toowhich 集區 hello 作業傳送。</span><span class="sxs-lookup"><span data-stu-id="7f79e-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="7f79e-109">BES 工作會執行自己的處理空間提供可預測的處理效能和 hello 能力 toocreate 資源集區對應 toohello 您送出的處理負載。</span><span class="sxs-lookup"><span data-stu-id="7f79e-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="7f79e-110">如何 toouse 批次集區處理</span><span class="sxs-lookup"><span data-stu-id="7f79e-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="7f79e-111">無法透過 hello Azure 入口網站目前可用的批次進行處理集區設定。</span><span class="sxs-lookup"><span data-stu-id="7f79e-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="7f79e-112">toouse 批次集區處理，您必須：</span><span class="sxs-lookup"><span data-stu-id="7f79e-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="7f79e-113">呼叫 CSS toocreate 批次集區帳戶，並取得集區服務 URL 和授權金鑰</span><span class="sxs-lookup"><span data-stu-id="7f79e-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="7f79e-114">建立新的 Resource Manager 型 Web 服務和計費方案</span><span class="sxs-lookup"><span data-stu-id="7f79e-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="7f79e-115">toocreate 您的帳戶，呼叫 Microsoft 客戶服務及支援 (CSS)，並提供您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="7f79e-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="7f79e-116">CSS 將適用於您 toodetermine hello 適當容量，以您的案例。</span><span class="sxs-lookup"><span data-stu-id="7f79e-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="7f79e-117">然後，CSS 會設定您的帳戶與 hello 集區，您可以建立並 hello 可以在每個集區的虛擬機器 (Vm) 的最大數目的數目上限。</span><span class="sxs-lookup"><span data-stu-id="7f79e-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="7f79e-118">設定您的帳戶後，您便會取得集區服務 URL 和授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="7f79e-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="7f79e-119">建立您的帳戶之後，您會使用 hello 集區服務 URL 和授權金鑰 tooperform 集區上的管理作業批次集區。</span><span class="sxs-lookup"><span data-stu-id="7f79e-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![批次集區服務架構。](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="7f79e-121">您可以呼叫該 CSS 提供 tooyou hello hello 集區服務 URL 建立集區作業建立集區。</span><span class="sxs-lookup"><span data-stu-id="7f79e-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="7f79e-122">當您建立一個集區時，指定的 Vm 和 hello hello swagger.json 新資源管理員的 URL 的 hello 數目基礎的機器學習 web 服務。</span><span class="sxs-lookup"><span data-stu-id="7f79e-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="7f79e-123">此 web 服務提供 tooestablish hello 計費關聯。</span><span class="sxs-lookup"><span data-stu-id="7f79e-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="7f79e-124">hello 批次集區服務會使用計費的方案中的 hello swagger.json tooassociate hello 集區。</span><span class="sxs-lookup"><span data-stu-id="7f79e-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="7f79e-125">您可以執行任何 BES web 服務，這兩個新的資源管理員，以基礎而且傳統，您選擇 hello 集區上。</span><span class="sxs-lookup"><span data-stu-id="7f79e-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="7f79e-126">您可以使用任何基礎的新資源管理員的 web 服務，但請留意 hello 計費 hello 工作負責針對 hello 與該服務相關聯的計費方案。</span><span class="sxs-lookup"><span data-stu-id="7f79e-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="7f79e-127">您可能想的 toocreate web 服務和新的計費計劃，專門用來執行批次集區工作。</span><span class="sxs-lookup"><span data-stu-id="7f79e-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="7f79e-128">如需關於建立 Web 服務的詳細資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="7f79e-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="7f79e-129">當您建立集區之後時，您送出 hello BES hello web 服務工作使用 hello 批次要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="7f79e-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="7f79e-130">您可以選擇 toosubmit 它 tooa 集區或 tooclassic 批次的處理。</span><span class="sxs-lookup"><span data-stu-id="7f79e-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="7f79e-131">toosubmit 作業 tooBatch 集區處理，您會加入下列參數 toohello 工作提交要求主體的 hello:</span><span class="sxs-lookup"><span data-stu-id="7f79e-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="7f79e-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="7f79e-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="7f79e-133">如果您不需要新增 hello 參數，hello 作業會執行 hello 傳統的批次的處理序環境中。</span><span class="sxs-lookup"><span data-stu-id="7f79e-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="7f79e-134">如果 hello 集區有可用的資源，會啟動 hello 工作立即執行。</span><span class="sxs-lookup"><span data-stu-id="7f79e-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="7f79e-135">如果 hello 集區沒有可用的資源，您的工作會排入佇列，直到有可用的資源。</span><span class="sxs-lookup"><span data-stu-id="7f79e-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="7f79e-136">如果您發現，定期連線到您的集區的 hello 容量，您需要更高的容量，您可以連絡 CSS，並使用代表性 tooincrease 您的配額。</span><span class="sxs-lookup"><span data-stu-id="7f79e-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="7f79e-137">範例要求︰</span><span class="sxs-lookup"><span data-stu-id="7f79e-137">Example Request:</span></span>

<span data-ttu-id="7f79e-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="7f79e-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="7f79e-139">使用批次集區處理時的考量</span><span class="sxs-lookup"><span data-stu-id="7f79e-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="7f79e-140">批次進行處理集區是一直在計費服務，而且這需要您 tooassociate 它與資源管理員內以計費方案。</span><span class="sxs-lookup"><span data-stu-id="7f79e-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="7f79e-141">您僅支付 hello 時數計算 hello 集區正在執行;不論 hello 期間該階段集區執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="7f79e-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="7f79e-142">如果您建立一個集區，您所要支付 hello 運算時數的 hello 集區中每個虛擬機器直到刪除為止 hello 集區，即使 hello 集區中執行任何批次工作。</span><span class="sxs-lookup"><span data-stu-id="7f79e-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="7f79e-143">計費 hello 虛擬機器的佈建完成時啟動，並停止時已被刪除。</span><span class="sxs-lookup"><span data-stu-id="7f79e-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="7f79e-144">您可以使用任何 hello hello 上找不到方案[機器學習定價頁面](https://azure.microsoft.com/pricing/details/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="7f79e-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="7f79e-145">計費範例︰</span><span class="sxs-lookup"><span data-stu-id="7f79e-145">Billing example:</span></span>

<span data-ttu-id="7f79e-146">如果您建立包含 2 部虛擬機器的批次集區，並在 24 小時後將它刪除，您的計費方案會借記 48 個計算小時；不論該期間內執行了多少作業。</span><span class="sxs-lookup"><span data-stu-id="7f79e-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="7f79e-147">如果您建立包含 4 部虛擬機器的批次集區，並在 12 小時後將它刪除，您的計費方案也會借記 48 個計算小時。</span><span class="sxs-lookup"><span data-stu-id="7f79e-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="7f79e-148">我們建議您輪詢 hello 作業狀態 toodetermine，當工作完成。</span><span class="sxs-lookup"><span data-stu-id="7f79e-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="7f79e-149">當所有的作業完成執行時，呼叫 hello 調整集區大小作業 tooset hello 數目 hello 集區 toozero 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7f79e-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="7f79e-150">如果您是簡短的資源集區，而且您需要 toocreate 新的集區，例如 toobill 針對不同的計費方案，您可以刪除 hello 集區改為所有的作業完成執行。</span><span class="sxs-lookup"><span data-stu-id="7f79e-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="7f79e-151">**使用批次集區處理的時機**</span><span class="sxs-lookup"><span data-stu-id="7f79e-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="7f79e-152">**使用傳統批次處理的時機**</span><span class="sxs-lookup"><span data-stu-id="7f79e-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="7f79e-153">您需要 toorun 大量作業</span><span class="sxs-lookup"><span data-stu-id="7f79e-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="7f79e-154">或</span><span class="sxs-lookup"><span data-stu-id="7f79e-154">Or</span></span><br/><span data-ttu-id="7f79e-155">您需要您的作業會立即執行的 tooknow</span><span class="sxs-lookup"><span data-stu-id="7f79e-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="7f79e-156">或</span><span class="sxs-lookup"><span data-stu-id="7f79e-156">Or</span></span><br/><span data-ttu-id="7f79e-157">您需要保證的輸送量。</span><span class="sxs-lookup"><span data-stu-id="7f79e-157">You need guaranteed throughput.</span></span> <span data-ttu-id="7f79e-158">例如，您需要 toorun 中指定的時間範圍內，作業數目，並想 tooscale 您計算資源 toomeet 出您的需求。</span><span class="sxs-lookup"><span data-stu-id="7f79e-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="7f79e-159">您正在執行一些作業</span><span class="sxs-lookup"><span data-stu-id="7f79e-159">You are running just a few jobs</span></span><br/><span data-ttu-id="7f79e-160">和</span><span class="sxs-lookup"><span data-stu-id="7f79e-160">And</span></span><br/> <span data-ttu-id="7f79e-161">您不立即需要 hello 作業 toorun</span><span class="sxs-lookup"><span data-stu-id="7f79e-161">You don’t need hello jobs toorun immediately</span></span> |
