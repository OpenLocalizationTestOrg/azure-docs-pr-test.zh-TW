---
title: "aaaRun Azure 批次工作負載符合成本效益的低優先順序 Vm （預覽） |Microsoft 文件"
description: "了解 tooprovision 低優先權 Vm tooreduce hello Azure 批次工作負載的成本。"
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="2c136-103">使用低優先順序的 VM 搭配 Batch (預覽)</span><span class="sxs-lookup"><span data-stu-id="2c136-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="2c136-104">Azure 批次提供批次工作負載的低先後虛擬機器 (Vm) tooreduce hello 的成本。</span><span class="sxs-lookup"><span data-stu-id="2c136-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="2c136-105">低優先順序的 VM 能提供大量的計算能力，同時也是經濟實惠的選擇，從而實現新的 Batch 工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="2c136-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="2c136-106">低優先順序的 VM 能善用 Azure 中的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="2c136-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="2c136-107">當您指定集區中的低優先順序 VM 時，Azure Batch 就會在有多餘的容量時自動加以使用。</span><span class="sxs-lookup"><span data-stu-id="2c136-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="2c136-108">使用低優先權 Vm hello 權衡取捨是使用在 Azure 中沒有多餘的容量時，可能佔用那些 Vm。</span><span class="sxs-lookup"><span data-stu-id="2c136-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="2c136-109">基於這個理由，低優先順序的 VM 最適合特定類型的工作負載。</span><span class="sxs-lookup"><span data-stu-id="2c136-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="2c136-110">批次和 hello 作業完成時間是有彈性且 hello 工作會分散到多個 Vm 的非同步處理工作負載使用低優先權的 Vm。</span><span class="sxs-lookup"><span data-stu-id="2c136-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="2c136-111">低優先順序 VM 的成本遠低於專用 VM。</span><span class="sxs-lookup"><span data-stu-id="2c136-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="2c136-112">如需定價詳細資料，請參閱 [Batch 定價](https://azure.microsoft.com/pricing/details/batch/)。</span><span class="sxs-lookup"><span data-stu-id="2c136-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="2c136-113">低優先順序 Vm 的其他討論，請參閱 hello 部落格文章公告：[批次計算花費少量 hello 價格](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)。</span><span class="sxs-lookup"><span data-stu-id="2c136-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c136-114">低優先順序的 VM 目前在預覽中，僅適用於 Batch 中執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="2c136-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="2c136-115">低優先順序 VM 的使用案例</span><span class="sxs-lookup"><span data-stu-id="2c136-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="2c136-116">提供的低優先順序 Vm hello 特性，哪些工作負載可以和無法使用它們？</span><span class="sxs-lookup"><span data-stu-id="2c136-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="2c136-117">一般情況下，批次處理工作負載就很適合，因為作業會區分成許多平行的工作，或是會將許多作業相應放大並分散於許多 VM。</span><span class="sxs-lookup"><span data-stu-id="2c136-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="2c136-118">在 Azure 的適當作業中的多餘容量 toomaximize 使用可以向外擴充。</span><span class="sxs-lookup"><span data-stu-id="2c136-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="2c136-119">偶爾 Vm 可能無法使用，或將會優先，會導致減少的容量，工作以及可能會導致 tootask 中斷和重播。</span><span class="sxs-lookup"><span data-stu-id="2c136-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="2c136-120">作業必須是彈性 hello toorun 花費的時間。</span><span class="sxs-lookup"><span data-stu-id="2c136-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="2c136-121">如果工作較長的作業受到中斷，可能就會影響較大。</span><span class="sxs-lookup"><span data-stu-id="2c136-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="2c136-122">如果長時間執行工作單位會實作檢查點 toosave 進度時，它們執行，則不中斷的影響會最少。</span><span class="sxs-lookup"><span data-stu-id="2c136-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="2c136-123">使用較短的時間執行工作通常 toowork 最適合低優先順序的 vm 為 hello 中斷的影響最少。</span><span class="sxs-lookup"><span data-stu-id="2c136-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="2c136-124">長時間執行 MPI 工作，利用多個 Vm 不適合的 toouse 低優先順序的 Vm 中當做一個先佔 VM 將會需要再次執行 toobe 可能負責人 toohello 整個作業。</span><span class="sxs-lookup"><span data-stu-id="2c136-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="2c136-125">批次處理的一些範例使用案例適合的 toouse 低優先順序的 Vm 為：</span><span class="sxs-lookup"><span data-stu-id="2c136-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="2c136-126">**開發與測試**︰特別是，如果您正在開發大規模的解決方案，就可實現可觀的成本節省。</span><span class="sxs-lookup"><span data-stu-id="2c136-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="2c136-127">所有的測試類型都能有所助益，但大規模的負載測試及迴歸測試都是很棒的用途。</span><span class="sxs-lookup"><span data-stu-id="2c136-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="2c136-128">**補充隨容量**： 低優先權的 Vm 可以用來補充 regular 專用的 Vm-可用時，工作可以和調整其規模較低的成本因此更快速完成; 時無法使用，hello 基準的專用 Vm 使用。</span><span class="sxs-lookup"><span data-stu-id="2c136-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="2c136-129">**彈性的工作執行時間**： 如果 hello 計時器工作沒有彈性 toocomplete，則可容許的容量可能會卸除; 不過，以 hello 加法的低優先順序 Vm 作業會經常執行更快速且更低的成本。</span><span class="sxs-lookup"><span data-stu-id="2c136-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="2c136-130">批次集區可以設定的 toouse 取決於 hello 彈性的低優先順序 Vm 有幾個方法，工作執行時間：</span><span class="sxs-lookup"><span data-stu-id="2c136-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="2c136-131">低優先順序的 VM 可以單獨用於集區中，Batch 只會在容量可用時，將任何佔用的容量復原。</span><span class="sxs-lookup"><span data-stu-id="2c136-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="2c136-132">這是 hello 最便宜的方式 tooexecute 作業，因為只有低優先順序的 Vm 所使用。</span><span class="sxs-lookup"><span data-stu-id="2c136-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="2c136-133">低優先順序的 VM 可以用來搭配專用 VM 的固定基準。</span><span class="sxs-lookup"><span data-stu-id="2c136-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="2c136-134">hello 固定的數目的專用的 Vm 可確保沒有一律某些容量 tookeep 工作進度。</span><span class="sxs-lookup"><span data-stu-id="2c136-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="2c136-135">可以有動態混合的專用和低優先順序的 Vm，以便可用時，成本較低的低優先順序 Vm 單獨使用，但 hello 全文價格專用 Vm 擴充規模，必要時，tookeep 容量可用 tookeep hello 作業的下限進度。</span><span class="sxs-lookup"><span data-stu-id="2c136-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="2c136-136">Batch 支援低優先順序的 VM</span><span class="sxs-lookup"><span data-stu-id="2c136-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="2c136-137">Azure 批次提供數項功能，可讓您輕鬆 tooconsume 及受益於低優先權的 Vm:</span><span class="sxs-lookup"><span data-stu-id="2c136-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="2c136-138">Batch 集區可以同時包含專用 VM 和低優先順序的 VM。</span><span class="sxs-lookup"><span data-stu-id="2c136-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="2c136-139">當集區會在建立或變更現有集區，使用 hello 明確的調整大小作業，或使用自動調整規模隨時都可以指定 hello 每種類型的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="2c136-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="2c136-140">作業和工作提交可以維持不變，而且不需要顧慮 hello 集區中的 hello VM 類型。</span><span class="sxs-lookup"><span data-stu-id="2c136-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="2c136-141">它也是可能 toohave 集區完全使用低優先權 Vm toorun 作業，但啟動專用 Vm 調整為廉價地如果 hello 容量低於下限臨界值，將執行的作業。</span><span class="sxs-lookup"><span data-stu-id="2c136-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="2c136-142">批次集區會自動搜尋低優先權 Vm toohello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="2c136-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="2c136-143">如果 Vm 被佔用，批次會嘗試 tooreplace hello 遺失容量及傳回 toohello 目標。</span><span class="sxs-lookup"><span data-stu-id="2c136-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="2c136-144">在工作被中斷的 hello 情況下，會偵測到批次，並將其自動工作 toobe 再次執行重新排入佇列中。</span><span class="sxs-lookup"><span data-stu-id="2c136-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="2c136-145">低優先順序 VM 具有核心配額，不同於專用 VM 的核心配額。</span><span class="sxs-lookup"><span data-stu-id="2c136-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="2c136-146">hello 引號的低優先順序的 Vm 是高於專用的 Vm，因為低優先權 Vm 成本也比較低。</span><span class="sxs-lookup"><span data-stu-id="2c136-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="2c136-147">如需詳細資訊，請參閱 [Batch 服務配額和限制](batch-quota-limit.md#resource-quotas)。</span><span class="sxs-lookup"><span data-stu-id="2c136-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="2c136-148">低優先順序 Vm 目前不支援批次帳戶 hello 集區配置模式下設定的位置太[使用者訂用帳戶](batch-account-create-portal.md#user-subscription-mode)。</span><span class="sxs-lookup"><span data-stu-id="2c136-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="2c136-149">建立和更新集區</span><span class="sxs-lookup"><span data-stu-id="2c136-149">Create and update pools</span></span>

<span data-ttu-id="2c136-150">批次集區可以包含專用和低優先順序的 Vm （也參考的 tooas 計算節點）。</span><span class="sxs-lookup"><span data-stu-id="2c136-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="2c136-151">您可以設定專用和低優先順序的 Vm 的運算節點的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="2c136-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="2c136-152">hello 目標節點的數目指定 hello 數目要 toohave hello 集區中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="2c136-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="2c136-153">比方說，使用 Azure 雲端服務 Vm 和 5 的目標集 toocreate 專用 Vm 和 20 低優先權的 Vm:</span><span class="sxs-lookup"><span data-stu-id="2c136-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="2c136-154">使用 Azure 虛擬機器 （在此情況下 Linux Vm） 具有 5 個目標集 toocreate 專用 Vm 和 20 低優先權的 Vm:</span><span class="sxs-lookup"><span data-stu-id="2c136-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="2c136-155">您可以取得專用和低優先順序的 Vm hello 目前節點的數目：</span><span class="sxs-lookup"><span data-stu-id="2c136-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="2c136-156">集區的節點具有屬性 tooindicate hello 節點是否為專用或低優先順序的 VM:</span><span class="sxs-lookup"><span data-stu-id="2c136-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="2c136-157">當集區中的一個或多個節點被佔用，集區清單節點的作業仍會傳回這些節點、 hello 的目前低優先權的節點數目會維持不變，但這些節點都有其狀態設定 toothe**先佔**狀態。</span><span class="sxs-lookup"><span data-stu-id="2c136-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="2c136-158">批次會嘗試 toofind 取代 Vm，而且如果成功的話，hello 節點將會瀏覽**建立**然後**起始**狀態才能成為可供工作執行方式就像是新節點。</span><span class="sxs-lookup"><span data-stu-id="2c136-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="2c136-159">調整包含低優先順序 VM 的集區</span><span class="sxs-lookup"><span data-stu-id="2c136-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="2c136-160">如同單獨組成專用的 Vm 集區，它是可能 tooscale 集區包含低優先權的 Vm，藉由呼叫 hello 調整方法或使用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="2c136-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="2c136-161">hello 集區調整大小作業採用第二個選擇性參數的值更新**targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="2c136-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="2c136-162">hello 集區自動調整規模公式支援低優先權 Vm 如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c136-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="2c136-163">您可以取得或設定 hello hello 服務定義的變數值**$TargetLowPriorityNodes**。</span><span class="sxs-lookup"><span data-stu-id="2c136-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="2c136-164">您可以取得 hello 服務定義變數的 hello 值**$CurrentLowPriorityNodes**。</span><span class="sxs-lookup"><span data-stu-id="2c136-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="2c136-165">您可以取得 hello 服務定義變數的 hello 值**$PreemptedNodeCount**。</span><span class="sxs-lookup"><span data-stu-id="2c136-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="2c136-166">此變數傳回 hello hello 中的節點數目佔用狀態，以及可讓您在相應增加或減少 hello 專用節點數目，而是根據 hello 先佔會無法使用的節點數目。</span><span class="sxs-lookup"><span data-stu-id="2c136-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="2c136-167">工作 (Job) 和工作 (Task)</span><span class="sxs-lookup"><span data-stu-id="2c136-167">Jobs and tasks</span></span>

<span data-ttu-id="2c136-168">工作與工作需要極少支援低優先權的節點。hello 僅支援如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c136-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="2c136-169">hello 工作 JobManagerTask 屬性已有新的屬性**AllowLowPriorityNode**。</span><span class="sxs-lookup"><span data-stu-id="2c136-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="2c136-170">這個屬性為 true 時，可以排定 hello 作業管理員工作專用或低優先順序的節點上。</span><span class="sxs-lookup"><span data-stu-id="2c136-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="2c136-171">如果此屬性為 false，hello 作業管理員工作將會只排程的 tooa 專用的節點。</span><span class="sxs-lookup"><span data-stu-id="2c136-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="2c136-172">[環境變數](batch-compute-node-environment-variables.md)是可用 tooa 工作應用程式，使它可以判斷它是否為低優先順序或專用節點上執行。</span><span class="sxs-lookup"><span data-stu-id="2c136-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="2c136-173">hello 環境變數是 AZ_BATCH_NODE_IS_DEDICATED。</span><span class="sxs-lookup"><span data-stu-id="2c136-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="2c136-174">處理優先佔用</span><span class="sxs-lookup"><span data-stu-id="2c136-174">Handling preemption</span></span>

<span data-ttu-id="2c136-175">Vm 偶爾可能會預先清空;當發生這種情況，批次未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="2c136-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="2c136-176">hello 先佔的 Vm 有其狀態也更新**先佔**。</span><span class="sxs-lookup"><span data-stu-id="2c136-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="2c136-177">如果工作上執行 hello 預先清空節點 Vm，則這些工作會排入佇列並再次執行。</span><span class="sxs-lookup"><span data-stu-id="2c136-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="2c136-178">有效地刪除 hello VM，這會導致 tooany 資料儲存在本機上 hello 遺失的 VM。</span><span class="sxs-lookup"><span data-stu-id="2c136-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="2c136-179">hello 集區會持續嘗試 tooreach hello 目標可用的低優先權的節點數目。</span><span class="sxs-lookup"><span data-stu-id="2c136-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="2c136-180">找到取代容量時，節點會保留其識別碼，但在可供工作排程使用之前，會先重新初始化，逐步進行**建立**和**啟動**狀態。</span><span class="sxs-lookup"><span data-stu-id="2c136-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="2c136-181">先佔計數可作為 hello Azure 入口網站中的度量。</span><span class="sxs-lookup"><span data-stu-id="2c136-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="2c136-182">度量</span><span class="sxs-lookup"><span data-stu-id="2c136-182">Metrics</span></span>

<span data-ttu-id="2c136-183">新的度量資訊是用於 hello [Azure 入口網站](https://portal.azure.com)低優先權的節點。</span><span class="sxs-lookup"><span data-stu-id="2c136-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="2c136-184">這些計量包括：</span><span class="sxs-lookup"><span data-stu-id="2c136-184">These metrics are:</span></span>

- <span data-ttu-id="2c136-185">低優先順序節點計數</span><span class="sxs-lookup"><span data-stu-id="2c136-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="2c136-186">低優先順序核心計數</span><span class="sxs-lookup"><span data-stu-id="2c136-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="2c136-187">先占節點計數</span><span class="sxs-lookup"><span data-stu-id="2c136-187">Preempted Node Count</span></span>

<span data-ttu-id="2c136-188">tooview hello Azure 入口網站中的度量：</span><span class="sxs-lookup"><span data-stu-id="2c136-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="2c136-189">巡覽 tooyour hello 入口網站中的批次帳戶，並檢視您的 Batch 帳戶的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="2c136-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="2c136-190">選取**度量**從 hello**監視**> 一節。</span><span class="sxs-lookup"><span data-stu-id="2c136-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="2c136-191">選取您想要的 hello 度量從 hello**可用的度量**清單。</span><span class="sxs-lookup"><span data-stu-id="2c136-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![低優先順序節點的計量](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="2c136-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c136-193">Next steps</span></span>

* <span data-ttu-id="2c136-194">讀取 hello[批次功能概觀，讓開發人員](batch-api-basics.md)，任何人準備 toouse 批次的重要資訊。</span><span class="sxs-lookup"><span data-stu-id="2c136-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="2c136-195">hello 發行項包含許多建置批次應用程式時，可以使用的 API 功能的批次服務資源集區、 節點、 工作和工作和 hello，如需詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="2c136-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="2c136-196">深入了解 hello[批次應用程式開發介面和工具](batch-apis-tools.md)可用來建置批次的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2c136-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
