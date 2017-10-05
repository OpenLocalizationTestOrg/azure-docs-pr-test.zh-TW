---
title: "在符合成本效益的低優先順序 VM 上執行 Azure Batch 工作負載 (預覽) | Microsoft Docs"
description: "了解如何佈建低優先順序的 VM，降低 Azure Batch 工作負載的成本。"
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
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="9580a-103">使用低優先順序的 VM 搭配 Batch (預覽)</span><span class="sxs-lookup"><span data-stu-id="9580a-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="9580a-104">Azure Batch 提供低優先權的虛擬機器 (VM)，可降低 Batch 工作負載的成本。</span><span class="sxs-lookup"><span data-stu-id="9580a-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="9580a-105">低優先順序的 VM 能提供大量的計算能力，同時也是經濟實惠的選擇，從而實現新的 Batch 工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="9580a-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="9580a-106">低優先順序的 VM 能善用 Azure 中的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="9580a-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="9580a-107">當您指定集區中的低優先順序 VM 時，Azure Batch 就會在有多餘的容量時自動加以使用。</span><span class="sxs-lookup"><span data-stu-id="9580a-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="9580a-108">使用低優先順序 VM 的權衡取捨，是當 Azure 中沒有多餘的容量時，可以將這些 VM 優先佔用。</span><span class="sxs-lookup"><span data-stu-id="9580a-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="9580a-109">基於這個理由，低優先順序的 VM 最適合特定類型的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9580a-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="9580a-110">低優先順序的 VM 是用於批次和非同步處理的工作負載，這種工作負載的作業完成時間很有彈性，且工作會分散於許多 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="9580a-111">低優先順序 VM 的成本遠低於專用 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="9580a-112">如需定價詳細資料，請參閱 [Batch 定價](https://azure.microsoft.com/pricing/details/batch/)。</span><span class="sxs-lookup"><span data-stu-id="9580a-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="9580a-113">如需低優先順序 VM 的其他討論，請參閱部落格文章公告：[依價格分數的 Batch 計算](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)。</span><span class="sxs-lookup"><span data-stu-id="9580a-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9580a-114">低優先順序的 VM 目前在預覽中，僅適用於 Batch 中執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9580a-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="9580a-115">低優先順序 VM 的使用案例</span><span class="sxs-lookup"><span data-stu-id="9580a-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="9580a-116">如果有低優先順序的 VM 的特性，哪些工作負載可以使用和無法使用它們？</span><span class="sxs-lookup"><span data-stu-id="9580a-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="9580a-117">一般情況下，批次處理工作負載就很適合，因為作業會區分成許多平行的工作，或是會將許多作業相應放大並分散於許多 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="9580a-118">若要充分使用 Azure 中的剩餘容量，可將適當的作業相應放大。</span><span class="sxs-lookup"><span data-stu-id="9580a-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="9580a-119">VM 偶爾可能會無法使用或被優先佔用，這會導致作業容量降低，且可能會導致工作中斷及重新執行。</span><span class="sxs-lookup"><span data-stu-id="9580a-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="9580a-120">因此，作業在可使用的時間內必須是有彈性的，才會將作業加以執行。</span><span class="sxs-lookup"><span data-stu-id="9580a-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="9580a-121">如果工作較長的作業受到中斷，可能就會影響較大。</span><span class="sxs-lookup"><span data-stu-id="9580a-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="9580a-122">如果長時間執行的工作在執行時實作檢查點來儲存進度，那麼中斷所造成的影響就會大幅降低。</span><span class="sxs-lookup"><span data-stu-id="9580a-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="9580a-123">時間執行較短的工作通常最適合低優先順序的 VM，因為中斷的影響會大幅降低。</span><span class="sxs-lookup"><span data-stu-id="9580a-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="9580a-124">利用多個 VM 長時間執行的 MPI 作業並不太適合使用低優先順序的 VM，因為一個優先佔用的 VM 有可能會導致整個作業必須重新執行一次。</span><span class="sxs-lookup"><span data-stu-id="9580a-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="9580a-125">適用於低優先順序 VM 的一些批次處理使用案例的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="9580a-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="9580a-126">**開發與測試**︰特別是，如果您正在開發大規模的解決方案，就可實現可觀的成本節省。</span><span class="sxs-lookup"><span data-stu-id="9580a-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="9580a-127">所有的測試類型都能有所助益，但大規模的負載測試及迴歸測試都是很棒的用途。</span><span class="sxs-lookup"><span data-stu-id="9580a-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="9580a-128">**補充隨選容量**︰低優先順序的 VM 可用來補充一般的專用 VM - 在可使用時，作業就能加以調整並從而以較低的成本加速完成；在無法使用時，就能使用專用 VM 的基準。</span><span class="sxs-lookup"><span data-stu-id="9580a-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="9580a-129">**彈性的作業執行時間**︰如果作業完成所需的時間有彈性，就能容許可能的容量下降；但新增了低優先順序的 VM 後，作業就會經常更快速執行，且成本更低。</span><span class="sxs-lookup"><span data-stu-id="9580a-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="9580a-130">有幾種方法可將 Batch 集區設為使用低優先順序的 VM，視作業執行時間的彈性而定︰</span><span class="sxs-lookup"><span data-stu-id="9580a-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="9580a-131">低優先順序的 VM 可以單獨用於集區中，Batch 只會在容量可用時，將任何佔用的容量復原。</span><span class="sxs-lookup"><span data-stu-id="9580a-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="9580a-132">這是執行作業最便宜的方式，因為只會使用低優先順序的 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="9580a-133">低優先順序的 VM 可以用來搭配專用 VM 的固定基準。</span><span class="sxs-lookup"><span data-stu-id="9580a-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="9580a-134">固定的專用 VM 數目可確保一律會有一些容量可保持作業進度。</span><span class="sxs-lookup"><span data-stu-id="9580a-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="9580a-135">可以將專用 VM 和低優先順序 VM 動態混用，如此就能在可用時單獨使用低成本低優先順序的 VM，但會視需要將原定價格的專用 VM 相應增加，讓可用的容量維持在最低量，從而保持作業進度。</span><span class="sxs-lookup"><span data-stu-id="9580a-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="9580a-136">Batch 支援低優先順序的 VM</span><span class="sxs-lookup"><span data-stu-id="9580a-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="9580a-137">Azure Batch 提供多項功能，能讓使用者輕鬆使用及受益於低優先順序的 VM：</span><span class="sxs-lookup"><span data-stu-id="9580a-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="9580a-138">Batch 集區可以同時包含專用 VM 和低優先順序的 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="9580a-139">您可以使用明確的調整大小作業或使用自動調整，在集區建立時指定每種類型的 VM 數目，或是針對現有集區隨時，將每種類型的 VM 數目加以變更。</span><span class="sxs-lookup"><span data-stu-id="9580a-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="9580a-140">作業和工作提交可維持不變，且無需擔心集區中的 VM 類型。</span><span class="sxs-lookup"><span data-stu-id="9580a-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="9580a-141">此外，也能盡可能以便宜的方式，讓集區完全使用低優先順序的 VM 來執行作業，但如果容量低於最小臨界值，就會運轉專用 VM，從而保持作業執行。</span><span class="sxs-lookup"><span data-stu-id="9580a-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="9580a-142">Batch 集區會自動搜尋低優先順序 VM 的目標數目。</span><span class="sxs-lookup"><span data-stu-id="9580a-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="9580a-143">如果 VM 被優先佔用，Batch 就會嘗試取代遺失的容量並回到目標。</span><span class="sxs-lookup"><span data-stu-id="9580a-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="9580a-144">在工作中斷的情況下，Batch 會偵測並自動將要再次執行的工作重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="9580a-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="9580a-145">低優先順序 VM 具有核心配額，不同於專用 VM 的核心配額。</span><span class="sxs-lookup"><span data-stu-id="9580a-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="9580a-146">低優先順序 VM 的配額高於專用 VM 的核心配額，因為低優先順序 VM 的成本較低。</span><span class="sxs-lookup"><span data-stu-id="9580a-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="9580a-147">如需詳細資訊，請參閱 [Batch 服務配額和限制](batch-quota-limit.md#resource-quotas)。</span><span class="sxs-lookup"><span data-stu-id="9580a-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="9580a-148">Batch 帳戶中的集區配置模式是設定為[使用者訂用帳戶](batch-account-create-portal.md#user-subscription-mode)，目前不支援低優先順序的 VM。</span><span class="sxs-lookup"><span data-stu-id="9580a-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="9580a-149">建立和更新集區</span><span class="sxs-lookup"><span data-stu-id="9580a-149">Create and update pools</span></span>

<span data-ttu-id="9580a-150">Batch 集區可以同時包含專用 VM 和低優先順序的 VM (亦稱為計算節點)。</span><span class="sxs-lookup"><span data-stu-id="9580a-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="9580a-151">您可以為專用 VM 和低優先順序的 VM 設定計算節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="9580a-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="9580a-152">節點的目標數目會指定您在集區中想要的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="9580a-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="9580a-153">例如，使用目標為 5 個專用 VM 和 20 個低優先順序 VM 的 Azure 雲端服務來建立集區：</span><span class="sxs-lookup"><span data-stu-id="9580a-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="9580a-154">使用目標為 5 個專用 VM 和 20 個低優先順序 VM 的 Azure 虛擬機器 (在此情況下為 Linux VM) 來建立集區：</span><span class="sxs-lookup"><span data-stu-id="9580a-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="9580a-155">您可以取得專用 VM 和低優先順序 VM 目前的節點數目：</span><span class="sxs-lookup"><span data-stu-id="9580a-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="9580a-156">集區節點的屬性可表示節點為專用的還是低優先順序的 VM：</span><span class="sxs-lookup"><span data-stu-id="9580a-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="9580a-157">當集區中的一個或多個節點被優先佔用時，集區上的清單節點作業仍會傳回這些節點，而目前的低優先順序節點數目將保持不變，但這些節點會將其狀態設定為**優先佔用**狀態。</span><span class="sxs-lookup"><span data-stu-id="9580a-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="9580a-158">Batch 會嘗試尋找取代 VM，如果成功，節點在變成可供工作執行前，會逐步進行**建立**和**啟動**狀態，就像新的節點一樣。</span><span class="sxs-lookup"><span data-stu-id="9580a-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="9580a-159">調整包含低優先順序 VM 的集區</span><span class="sxs-lookup"><span data-stu-id="9580a-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="9580a-160">如同由專用 VM 單獨組成的集區，可藉由呼叫調整大小方法或使用自動調整，將包含低優先順序 VM 的集區進行調整。</span><span class="sxs-lookup"><span data-stu-id="9580a-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="9580a-161">調整集區大小的作業會採用第二個選擇性參數，可更新 **targetLowPriorityNodes** 的值：</span><span class="sxs-lookup"><span data-stu-id="9580a-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="9580a-162">集區自動調整公式會支援低優先順序的 VM，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9580a-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="9580a-163">您可以取得或設定服務定義之 **$TargetLowPriorityNodes** 變數的值。</span><span class="sxs-lookup"><span data-stu-id="9580a-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="9580a-164">您可以取得服務定義之 **$CurrentLowPriorityNodes** 變數的值。</span><span class="sxs-lookup"><span data-stu-id="9580a-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="9580a-165">您可以取得服務定義之 **$PreemptedNodeCount** 變數的值。</span><span class="sxs-lookup"><span data-stu-id="9580a-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="9580a-166">此變數會傳回優先佔用狀態中的節點數目，並可依無法使用的優先佔用節點數目，將您的專用節點數目相應增加或相應減少。</span><span class="sxs-lookup"><span data-stu-id="9580a-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="9580a-167">工作 (Job) 和工作 (Task)</span><span class="sxs-lookup"><span data-stu-id="9580a-167">Jobs and tasks</span></span>

<span data-ttu-id="9580a-168">作業和工作幾乎都不需要低優先順序節點的支援；唯一的支援如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9580a-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="9580a-169">作業的 JobManagerTask 屬性都有新的屬性，**AllowLowPriorityNode**。</span><span class="sxs-lookup"><span data-stu-id="9580a-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="9580a-170">當這個屬性為 true 時，就可以在專用節點或低優先順序的節點上排程作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="9580a-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="9580a-171">如果這個屬性為 false，就只會將作業管理員工作將排到專用節點。</span><span class="sxs-lookup"><span data-stu-id="9580a-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="9580a-172">[環境變數](batch-compute-node-environment-variables.md)可供工作應用程式使用，因此它可以判斷是在低優先順序還是專用節點上執行。</span><span class="sxs-lookup"><span data-stu-id="9580a-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="9580a-173">環境變數是 AZ_BATCH_NODE_IS_DEDICATED。</span><span class="sxs-lookup"><span data-stu-id="9580a-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="9580a-174">處理優先佔用</span><span class="sxs-lookup"><span data-stu-id="9580a-174">Handling preemption</span></span>

<span data-ttu-id="9580a-175">VM 可能偶爾會被優先佔用；當這個情況發生時，Batch 會執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="9580a-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="9580a-176">優先佔用的 VM 都會將其狀態更新為**優先佔用**。</span><span class="sxs-lookup"><span data-stu-id="9580a-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="9580a-177">如果工作是在優先佔用的節點 VM 上執行，就會將這些工作重新排入佇列並再次執行。</span><span class="sxs-lookup"><span data-stu-id="9580a-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="9580a-178">VM 將會有效地刪除，導致本機儲存在上 VM 的任何資料遺失。</span><span class="sxs-lookup"><span data-stu-id="9580a-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="9580a-179">集區會繼續嘗試觸達可用的低優先順序節點之目標數目。</span><span class="sxs-lookup"><span data-stu-id="9580a-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="9580a-180">找到取代容量時，節點會保留其識別碼，但在可供工作排程使用之前，會先重新初始化，逐步進行**建立**和**啟動**狀態。</span><span class="sxs-lookup"><span data-stu-id="9580a-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="9580a-181">優先佔用計數會在 Azure 入口網站中作為計量提供使用。</span><span class="sxs-lookup"><span data-stu-id="9580a-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="9580a-182">度量</span><span class="sxs-lookup"><span data-stu-id="9580a-182">Metrics</span></span>

<span data-ttu-id="9580a-183">[Azure 入口網站](https://portal.azure.com)中有針對低優先順序節點提供的新計量。</span><span class="sxs-lookup"><span data-stu-id="9580a-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="9580a-184">這些計量包括：</span><span class="sxs-lookup"><span data-stu-id="9580a-184">These metrics are:</span></span>

- <span data-ttu-id="9580a-185">低優先順序節點計數</span><span class="sxs-lookup"><span data-stu-id="9580a-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="9580a-186">低優先順序核心計數</span><span class="sxs-lookup"><span data-stu-id="9580a-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="9580a-187">先占節點計數</span><span class="sxs-lookup"><span data-stu-id="9580a-187">Preempted Node Count</span></span>

<span data-ttu-id="9580a-188">若要檢視 Azure 入口網站中的計量：</span><span class="sxs-lookup"><span data-stu-id="9580a-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="9580a-189">在入口網站中瀏覽至您的 Batch 帳戶，並檢視 Batch 帳戶的設定。</span><span class="sxs-lookup"><span data-stu-id="9580a-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="9580a-190">從 [監視] 區段選取 [計量]。</span><span class="sxs-lookup"><span data-stu-id="9580a-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="9580a-191">從 [可用的計量] 清單中選取您所需的計量。</span><span class="sxs-lookup"><span data-stu-id="9580a-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![低優先順序節點的計量](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="9580a-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9580a-193">Next steps</span></span>

* <span data-ttu-id="9580a-194">請參閱 [適用於開發人員的 Batch 功能概觀](batch-api-basics.md)，這是任何準備使用 Batch 的人員不可或缺的資訊。</span><span class="sxs-lookup"><span data-stu-id="9580a-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="9580a-195">本文包含 Batch 服務資源 (例如集區、節點、作業和工作) 的詳細資訊，以及在建置 Batch 應用程式時可使用的許多 API 功能。</span><span class="sxs-lookup"><span data-stu-id="9580a-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="9580a-196">了解可用來建置 Batch 解決方案的 [Batch API 和工具](batch-apis-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="9580a-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
