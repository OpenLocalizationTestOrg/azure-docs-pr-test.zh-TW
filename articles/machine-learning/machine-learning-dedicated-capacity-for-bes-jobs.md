---
title: "Machine Learning 批次執行服務作業的專用功能 | Microsoft Docs"
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
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="09b58-103">適用於 Machine Learning 作業的 Azure Batch 服務</span><span class="sxs-lookup"><span data-stu-id="09b58-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="09b58-104">Machine Learning 批次集區處理提供客戶管理的 Azure Machine Learning 批次執行服務級別。</span><span class="sxs-lookup"><span data-stu-id="09b58-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="09b58-105">機器學習服務的傳統批次處理發生於多租用戶環境中，其限制您可以提交的並行作業數目，而且作業會以先進先出為原則排入佇列中。</span><span class="sxs-lookup"><span data-stu-id="09b58-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="09b58-106">這種不確定性，表示您無法準確地預測何時會執行您的作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="09b58-107">批次集區處理可讓您建立集區，以便提交批次作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="09b58-108">您可控制集區的大小，以及作業要提交至哪個集區。</span><span class="sxs-lookup"><span data-stu-id="09b58-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="09b58-109">BES 作業會在自己的處理空間中執行，以提供可預測的處理效能以及建立資源集區 (對應至您提交的處理負載) 的功能。</span><span class="sxs-lookup"><span data-stu-id="09b58-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="09b58-110">如何使用批次集區處理</span><span class="sxs-lookup"><span data-stu-id="09b58-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="09b58-111">您目前無法透過 Azure 入口網站設定批次集區處理。</span><span class="sxs-lookup"><span data-stu-id="09b58-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="09b58-112">若要使用批次集區處理，您必須：</span><span class="sxs-lookup"><span data-stu-id="09b58-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="09b58-113">呼叫 CSS 以建立批次集區帳戶，並取得集區服務 URL 和授權金鑰</span><span class="sxs-lookup"><span data-stu-id="09b58-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="09b58-114">建立新的 Resource Manager 型 Web 服務和計費方案</span><span class="sxs-lookup"><span data-stu-id="09b58-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="09b58-115">若要建立帳戶，請連絡 Microsoft 客戶服務與支援中心 (CSS) 並提供您的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="09b58-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="09b58-116">CSS 將與您一起決定您案例的適當容量。</span><span class="sxs-lookup"><span data-stu-id="09b58-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="09b58-117">CSS 會接著設定您的帳戶：您可以建立的集區數目上限，以及您可以放在每個集區中的虛擬機器 (VM) 數目上限。</span><span class="sxs-lookup"><span data-stu-id="09b58-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="09b58-118">設定您的帳戶後，您便會取得集區服務 URL 和授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="09b58-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="09b58-119">建立您的帳戶之後，您可使用集區服務 URL 和授權金鑰，在您的批次集區上執行集區管理作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![批次集區服務架構。](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="09b58-121">您可以在 CSS 提供給您的集區服務 URL 上呼叫「建立集區」作業，以建立集區。</span><span class="sxs-lookup"><span data-stu-id="09b58-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="09b58-122">當您建立集區時，請指定 VM 數目和全新 Resource Manager 型 Machine Learning Web 服務的 swagger.json URL。</span><span class="sxs-lookup"><span data-stu-id="09b58-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="09b58-123">此 Web 服務可供建立計費關聯。</span><span class="sxs-lookup"><span data-stu-id="09b58-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="09b58-124">批次集區服務會使用 swagger.json 將集區與計費方案建立關聯。</span><span class="sxs-lookup"><span data-stu-id="09b58-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="09b58-125">您可以執行您在集區上選擇的任何 BES Web 服務 (全新 Resource Manager 型和傳統)。</span><span class="sxs-lookup"><span data-stu-id="09b58-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="09b58-126">您可以使用任何全新 Resource Manager 型 Web 服務，但請注意，作業是根據與該服務相關聯的計費方案收費。</span><span class="sxs-lookup"><span data-stu-id="09b58-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="09b58-127">您可以特別建立 Web 服務和新的計費方案，以便執行批次集區作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="09b58-128">如需關於建立 Web 服務的詳細資訊，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="09b58-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="09b58-129">建立集區後，您可使用 Web 服務的批次要求 URL 提交 BES 作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="09b58-130">您可以選擇將它提交至集區或傳統批次處理。</span><span class="sxs-lookup"><span data-stu-id="09b58-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="09b58-131">若要將作業提交至批次集區處理，請將下列參數新增至作業提交要求本文︰</span><span class="sxs-lookup"><span data-stu-id="09b58-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="09b58-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="09b58-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="09b58-133">如果您未新增此參數，則會在傳統批次處理環境中執行作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="09b58-134">如果集區有可用的資源，則會立即開始執行作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="09b58-135">如果集區沒有可用的資源，則作業會排入佇列，直到有可用的資源為止。</span><span class="sxs-lookup"><span data-stu-id="09b58-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="09b58-136">如果您發現您定期達到集區的容量而且需要更高的容量，您可以連絡 CSS 並與支援代表一起增加您的配額。</span><span class="sxs-lookup"><span data-stu-id="09b58-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="09b58-137">範例要求︰</span><span class="sxs-lookup"><span data-stu-id="09b58-137">Example Request:</span></span>

<span data-ttu-id="09b58-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="09b58-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="09b58-139">使用批次集區處理時的考量</span><span class="sxs-lookup"><span data-stu-id="09b58-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="09b58-140">批次集區處理是一項永遠開啟的計費服務，而且您必須將它與 Resource Manager 型計費方案建立關聯。</span><span class="sxs-lookup"><span data-stu-id="09b58-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="09b58-141">您只需支付集區執行的計算時數；不管該時間集區內執行的作業數目。</span><span class="sxs-lookup"><span data-stu-id="09b58-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="09b58-142">如果您建立集區，即使集區中沒有任何執行中的批次作業，您仍需支付集區中每部虛擬機器的計算時數，直到集區刪除為止。</span><span class="sxs-lookup"><span data-stu-id="09b58-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="09b58-143">虛擬機器會在完成佈建時開始計費，而在遭到刪除時停止計費。</span><span class="sxs-lookup"><span data-stu-id="09b58-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="09b58-144">您可以使用在 [Machine Learning 價格頁面](https://azure.microsoft.com/pricing/details/machine-learning/)找到的任何方案。</span><span class="sxs-lookup"><span data-stu-id="09b58-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="09b58-145">計費範例︰</span><span class="sxs-lookup"><span data-stu-id="09b58-145">Billing example:</span></span>

<span data-ttu-id="09b58-146">如果您建立包含 2 部虛擬機器的批次集區，並在 24 小時後將它刪除，您的計費方案會借記 48 個計算小時；不論該期間內執行了多少作業。</span><span class="sxs-lookup"><span data-stu-id="09b58-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="09b58-147">如果您建立包含 4 部虛擬機器的批次集區，並在 12 小時後將它刪除，您的計費方案也會借記 48 個計算小時。</span><span class="sxs-lookup"><span data-stu-id="09b58-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="09b58-148">我們建議您輪詢作業狀態以判斷作業何時完成。</span><span class="sxs-lookup"><span data-stu-id="09b58-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="09b58-149">當所有作業完成執行時，請呼叫「調整集區大小」作業，將集區中的虛擬機器數目設定為零。</span><span class="sxs-lookup"><span data-stu-id="09b58-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="09b58-150">如果集區資源不足，而您需要建立新的集區 (例如根據不同計費方案進行計費)，您可以在所有作業都完成執行時刪除集區。</span><span class="sxs-lookup"><span data-stu-id="09b58-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="09b58-151">**使用批次集區處理的時機**</span><span class="sxs-lookup"><span data-stu-id="09b58-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="09b58-152">**使用傳統批次處理的時機**</span><span class="sxs-lookup"><span data-stu-id="09b58-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="09b58-153">您需要執行大量的作業</span><span class="sxs-lookup"><span data-stu-id="09b58-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="09b58-154">或</span><span class="sxs-lookup"><span data-stu-id="09b58-154">Or</span></span><br/><span data-ttu-id="09b58-155">您需要知道您的作業將立即執行</span><span class="sxs-lookup"><span data-stu-id="09b58-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="09b58-156">或</span><span class="sxs-lookup"><span data-stu-id="09b58-156">Or</span></span><br/><span data-ttu-id="09b58-157">您需要保證的輸送量。</span><span class="sxs-lookup"><span data-stu-id="09b58-157">You need guaranteed throughput.</span></span> <span data-ttu-id="09b58-158">例如，您需要在指定的時間範圍內執行多項作業，而且想要相應放大計算資源以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="09b58-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="09b58-159">您正在執行一些作業</span><span class="sxs-lookup"><span data-stu-id="09b58-159">You are running just a few jobs</span></span><br/><span data-ttu-id="09b58-160">和</span><span class="sxs-lookup"><span data-stu-id="09b58-160">And</span></span><br/> <span data-ttu-id="09b58-161">您不需要立即執行作業</span><span class="sxs-lookup"><span data-stu-id="09b58-161">You don’t need the jobs to run immediately</span></span> |
