---
title: "自動調整 Azure Batch 集區中的計算節點 | Microsoft Docs"
description: "在雲端集區上啟用自動調整，以動態調整集區中的計算節點數目。"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0e49cd8a64a48c53f5b6104703164a597c797f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a><span data-ttu-id="a6e17-103">建立自動調整公式來調整 Batch 集區中的計算節點</span><span class="sxs-lookup"><span data-stu-id="a6e17-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span></span>

<span data-ttu-id="a6e17-104">Azure Batch 可以根據您定義的參數自動調整集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-104">Azure Batch can automatically scale pools based on parameters that you define.</span></span> <span data-ttu-id="a6e17-105">使用自動調整，Batch 會隨著工作需求增加，動態地將節點新增至集區，以及隨著工作需求減少而移除計算節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-105">With automatic scaling, Batch dynamically adds nodes to a pool as task demands increase, and removes compute nodes as they decrease.</span></span> <span data-ttu-id="a6e17-106">自動調整 Batch 應用程式所使用的計算節點數目，可讓您節省時間與金錢。</span><span class="sxs-lookup"><span data-stu-id="a6e17-106">You can save both time and money by automatically adjusting the number of compute nodes used by your Batch application.</span></span> 

<span data-ttu-id="a6e17-107">您可讓您定義的「自動調整公式」與計算節點的集區產生關聯，以在該集區上啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span></span> <span data-ttu-id="a6e17-108">Batch 服務會使用自動調整公式來判斷要執行您的工作負載所需的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-108">The Batch service uses the autoscale formula to determine the number of compute nodes that are needed to execute your workload.</span></span> <span data-ttu-id="a6e17-109">計算節點可以是專用節點或[低優先順序節點](batch-low-pri-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-109">Compute nodes may be dedicated nodes or [low-priority nodes](batch-low-pri-vms.md).</span></span> <span data-ttu-id="a6e17-110">Batch 會回應定期收集的服務計量資料。</span><span class="sxs-lookup"><span data-stu-id="a6e17-110">Batch responds to service metrics data that is collected periodically.</span></span> <span data-ttu-id="a6e17-111">使用此計量資料，Batch 會根據您的公式以可設定的間隔調整集區中的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-111">Using this metrics data, Batch adjusts the number of compute nodes in the pool based on your formula and at a configurable interval.</span></span>

<span data-ttu-id="a6e17-112">您可以在建立集區時或在現有的集區上啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-112">You can enable automatic scaling either when a pool is created, or on an existing pool.</span></span> <span data-ttu-id="a6e17-113">您也可以變更已針對自動調整設定之集區上的現有公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-113">You can also change an existing formula on a pool that is configured for autoscaling.</span></span> <span data-ttu-id="a6e17-114">Batch 可讓您在將公式指派給集區之前評估公式，以及監視自動調整回合的狀態。</span><span class="sxs-lookup"><span data-stu-id="a6e17-114">Batch enables you to evaluate your formulas before assigning them to pools and to monitor the status of automatic scaling runs.</span></span>

<span data-ttu-id="a6e17-115">本文會討論構成自動調整公式的各種實體，包括變數、運算子、作業和函式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-115">This article discusses the various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span></span> <span data-ttu-id="a6e17-116">我們討論如何取得 Batch 內的各種計算資源和工作計量。</span><span class="sxs-lookup"><span data-stu-id="a6e17-116">We discuss how to obtain various compute resource and task metrics within Batch.</span></span> <span data-ttu-id="a6e17-117">您可以使用這些計量，根據資源使用量和工作狀態調整集區的節點計數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-117">You can use these metrics to adjust your pool's node count based on resource usage and task status.</span></span> <span data-ttu-id="a6e17-118">然後，我們會說明如何藉由使用 Batch REST 和 .NET API，建立公式以及對集區啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-118">We then describe how to construct a formula and enable automatic scaling on a pool by using both the Batch REST and .NET APIs.</span></span> <span data-ttu-id="a6e17-119">最後，我們會完成幾個範例公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-119">Finally, we finish up with a few example formulas.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6e17-120">當您建立 Batch 帳戶時，您可以指定[帳戶設定](batch-api-basics.md#account)，該設定會決定集區是配置在 Batch 服務訂用帳戶 (預設值)，或是您的使用者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6e17-120">When you create a Batch account, you can specify the [account configuration](batch-api-basics.md#account), which determines whether pools are allocated in a Batch service subscription (the default), or in your user subscription.</span></span> <span data-ttu-id="a6e17-121">如果您使用預設 Batch 服務設定來建立 Batch 帳戶，則您的帳戶受限為可用於處理的核心數目上限。</span><span class="sxs-lookup"><span data-stu-id="a6e17-121">If you created your Batch account with the default Batch Service configuration, then your account is limited to a maximum number of cores that can be used for processing.</span></span> <span data-ttu-id="a6e17-122">Batch 服務只會將計算節點調整為最多達到該核心限制。</span><span class="sxs-lookup"><span data-stu-id="a6e17-122">The Batch service scales compute nodes only up to that core limit.</span></span> <span data-ttu-id="a6e17-123">基於這個理由，Batch 服務不會達到自動調整公式所指定的目標計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-123">For this reason, the Batch service may not reach the target number of compute nodes specified by an autoscale formula.</span></span> <span data-ttu-id="a6e17-124">如需檢視和增加帳戶配額的相關資訊，請參閱 [Azure Batch 服務的配額和限制](batch-quota-limit.md) 。</span><span class="sxs-lookup"><span data-stu-id="a6e17-124">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span></span>
>
><span data-ttu-id="a6e17-125">如果您以使用者訂用帳戶設定建立您的帳戶，則您的帳戶會共用訂用帳戶的核心配額。</span><span class="sxs-lookup"><span data-stu-id="a6e17-125">If you created your account with the User Subscription configuration, then your account shares in the core quota for the subscription.</span></span> <span data-ttu-id="a6e17-126">如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)中的 [虛擬機器限制](../azure-subscription-service-limits.md#virtual-machines-limits)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-126">For more information, see [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
>
>

## <a name="automatic-scaling-formulas"></a><span data-ttu-id="a6e17-127">自動調整公式</span><span class="sxs-lookup"><span data-stu-id="a6e17-127">Automatic scaling formulas</span></span>
<span data-ttu-id="a6e17-128">自動調整公式是您定義的字串值，其中包含一或多個陳述式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-128">An automatic scaling formula is a string value that you define that contains one or more statements.</span></span> <span data-ttu-id="a6e17-129">自動調整公式已指派給集區的 [autoScaleFormula][rest_autoscaleformula] 元素 (Batch REST) 或 [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] 屬性 (Batch .NET)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-129">The autoscale formula is assigned to a pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span></span> <span data-ttu-id="a6e17-130">Batch 集區會使用您的公式來決定集區中可供下一個間隔處理的目標計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-130">The Batch service uses your formula to determine the target number of compute nodes in the pool for the next interval of processing.</span></span> <span data-ttu-id="a6e17-131">公式字串不得超過 8 KB、最多只能包含 100 個陳述式 (以分號隔開)，而且可以包含換行和註解。</span><span class="sxs-lookup"><span data-stu-id="a6e17-131">The formula string cannot exceed 8 KB, can include up to 100 statements that are separated by semicolons, and can include line breaks and comments.</span></span>

<span data-ttu-id="a6e17-132">您可以將自動調整公式視為 Batch 自動調整「語言」。</span><span class="sxs-lookup"><span data-stu-id="a6e17-132">You can think of automatic scaling formulas as a Batch autoscale "language."</span></span> <span data-ttu-id="a6e17-133">公式陳述式是自由格式的運算式，可以包括服務定義的變數 (Batch 服務所定義的變數) 和使用者定義的變數 (您所定義的變數)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-133">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by the Batch service) and user-defined variables (variables that you define).</span></span> <span data-ttu-id="a6e17-134">它們可以使用內建類型、運算子和函式對這些值執行各種作業。</span><span class="sxs-lookup"><span data-stu-id="a6e17-134">They can perform various operations on these values by using built-in types, operators, and functions.</span></span> <span data-ttu-id="a6e17-135">例如，陳述式可能會採用下列格式：</span><span class="sxs-lookup"><span data-stu-id="a6e17-135">For example, a statement might take the following form:</span></span>

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

<span data-ttu-id="a6e17-136">公式通常包含多個陳述式，其可對在先前陳述式中取得的值執行作業。</span><span class="sxs-lookup"><span data-stu-id="a6e17-136">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span></span> <span data-ttu-id="a6e17-137">例如，首先我們會取得 `variable1` 的值，然後將它傳遞至函式以填入 `variable2`：</span><span class="sxs-lookup"><span data-stu-id="a6e17-137">For example, first we obtain a value for `variable1`, then pass it to a function to populate `variable2`:</span></span>

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

<span data-ttu-id="a6e17-138">在您的自動調整公式中包含這些陳述式，以達成目標計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-138">Include these statements in your autoscale formula to arrive at a target number of compute nodes.</span></span> <span data-ttu-id="a6e17-139">專用節點與低優先順序節點各有自己的目標設定，因此您可以為每個節點類型定義目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-139">Dedicated nodes and low-priority nodes each have their own target settings, so that you can define a target for each type of node.</span></span> <span data-ttu-id="a6e17-140">自動調整公式可以包含專用節點目標值、低優先順序節點目標值，或同時包含兩者。</span><span class="sxs-lookup"><span data-stu-id="a6e17-140">An autoscale formula can include a target value for dedicated nodes, a target value for low-priority nodes, or both.</span></span>

<span data-ttu-id="a6e17-141">目標節點數目可能會更高、更低，或與集區中該類型目前的節點數目相同。</span><span class="sxs-lookup"><span data-stu-id="a6e17-141">The target number of nodes may be higher, lower, or the same as the current number of nodes of that type in the pool.</span></span> <span data-ttu-id="a6e17-142">Batch 服務會在特定間隔評估集區的自動調整公式 (請參閱[自動調整間隔](#automatic-scaling-interval))。</span><span class="sxs-lookup"><span data-stu-id="a6e17-142">Batch evaluates a pool's autoscale formula at a specific interval (see [automatic scaling intervals](#automatic-scaling-interval)).</span></span> <span data-ttu-id="a6e17-143">Batch 會將集區中每個節點類型的目標數目調整為自動調整公式在評估時指定的數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-143">Batch adjusts the target number of each type of node in the pool to the number that your autoscale formula specifies at the time of evaluation.</span></span>

### <a name="sample-autoscale-formula"></a><span data-ttu-id="a6e17-144">自動調整公式範例</span><span class="sxs-lookup"><span data-stu-id="a6e17-144">Sample autoscale formula</span></span>

<span data-ttu-id="a6e17-145">以下是可加以調整以適用於大部分情況的自動調整公式範例。</span><span class="sxs-lookup"><span data-stu-id="a6e17-145">Here is an example of an autoscale formula that can be adjusted to work for most scenarios.</span></span> <span data-ttu-id="a6e17-146">您可以依照需求調整範例公式中的 `startingNumberOfVMs` 和 `maxNumberofVMs` 變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-146">The variables `startingNumberOfVMs` and `maxNumberofVMs` in the example formula can be adjusted to your needs.</span></span> <span data-ttu-id="a6e17-147">此公式會調整專用節點，但是可加以修改，套用來調整低優先順序節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-147">This formula scales dedicated nodes, but can be modified to apply to scale low-priority nodes as well.</span></span> 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

<span data-ttu-id="a6e17-148">使用此自動調整公式，一開始會建立包含單一 VM 的集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-148">With this autoscale formula, the pool is initially created with a single VM.</span></span> <span data-ttu-id="a6e17-149">`$PendingTasks` 計量會定義執行中或已排入佇列的工作數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-149">The `$PendingTasks` metric defines the number of tasks that are running or queued.</span></span> <span data-ttu-id="a6e17-150">公式會尋找過去 180 秒內的平均擱置中工作數目，並據以設定 `$TargetDedicatedNodes` 變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-150">The formula finds the average number of pending tasks in the last 180 seconds and sets the `$TargetDedicatedNodes` variable accordingly.</span></span> <span data-ttu-id="a6e17-151">公式會確保目標專用節點數目絕不會超出 25 部 VM。</span><span class="sxs-lookup"><span data-stu-id="a6e17-151">The formula ensures that the target number of dedicated nodes never exceeds 25 VMs.</span></span> <span data-ttu-id="a6e17-152">集區會隨著新工作的提交而自動成長。</span><span class="sxs-lookup"><span data-stu-id="a6e17-152">As new tasks are submitted, the pool automatically grows.</span></span> <span data-ttu-id="a6e17-153">隨著工作完成，VM 會逐一變成可用，且自動調整公式會縮小集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-153">As tasks complete, VMs become free one by one and the autoscaling formula shrinks the pool.</span></span>

## <a name="variables"></a><span data-ttu-id="a6e17-154">變數</span><span class="sxs-lookup"><span data-stu-id="a6e17-154">Variables</span></span>
<span data-ttu-id="a6e17-155">您可以在自動調整公式中同時使用**服務定義**和**使用者定義**的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-155">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span></span> <span data-ttu-id="a6e17-156">服務定義的變數內建在 Batch 服務中。</span><span class="sxs-lookup"><span data-stu-id="a6e17-156">The service-defined variables are built in to the Batch service.</span></span> <span data-ttu-id="a6e17-157">有些服務定義的變數是讀寫，有些是唯讀。</span><span class="sxs-lookup"><span data-stu-id="a6e17-157">Some service-defined variables are read-write, and some are read-only.</span></span> <span data-ttu-id="a6e17-158">使用者定義的變數是您定義的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-158">User-defined variables are variables that you define.</span></span> <span data-ttu-id="a6e17-159">在上一節中所示的範例公式中，`$TargetDedicatedNodes` 和 `$PendingTasks` 是服務定義的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-159">In the example formula shown in the previous section, `$TargetDedicatedNodes` and `$PendingTasks` are service-defined variables.</span></span> <span data-ttu-id="a6e17-160">`startingNumberOfVMs` 和 `maxNumberofVMs` 變數是使用者定義的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-160">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span></span>

> [!NOTE]
> <span data-ttu-id="a6e17-161">服務定義的變數前面一律會加上貨幣符號 ($)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-161">Service-defined variables are always preceded by a dollar sign ($).</span></span> <span data-ttu-id="a6e17-162">針對使用者定義的變數而言，貨幣符號是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a6e17-162">For user-defined variables, the dollar sign is optional.</span></span>
>
>

<span data-ttu-id="a6e17-163">下表顯示 Batch 服務所定義的讀寫和唯讀變數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-163">The following tables show both read-write and read-only variables that are defined by the Batch service.</span></span>

<span data-ttu-id="a6e17-164">您可以取得並設定這些這些服務定義的變數值，以管理集區中的計算節點：</span><span class="sxs-lookup"><span data-stu-id="a6e17-164">You can get and set the values of these service-defined variables to manage the number of compute nodes in a pool:</span></span>

| <span data-ttu-id="a6e17-165">讀寫服務定義變數</span><span class="sxs-lookup"><span data-stu-id="a6e17-165">Read-write service-defined variables</span></span> | <span data-ttu-id="a6e17-166">說明</span><span class="sxs-lookup"><span data-stu-id="a6e17-166">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6e17-167">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-167">$TargetDedicatedNodes</span></span> |<span data-ttu-id="a6e17-168">集區之專用計算節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-168">The target number of dedicated compute nodes for the pool.</span></span> <span data-ttu-id="a6e17-169">專用節點數目被指定作為目標，因為集區不一定會達到想要的節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-169">The number of dedicated nodes is specified as a target because a pool may not always achieve the desired number of nodes.</span></span> <span data-ttu-id="a6e17-170">例如，如果在集區達到初始目標之前，自動調整評估修改目標專用節點數目，則集區可能未達到目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-170">For example, if the target number of dedicated nodes is modified by an autoscale evaluation before the pool has reached the initial target, then the pool may not reach the target.</span></span> <br /><br /> <span data-ttu-id="a6e17-171">如果目標超過 Batch 帳戶節點或核心配額，以 Batch 服務設定建立之帳戶中的集區可能未達到其目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-171">A pool in an account created with the Batch Service configuration may not achieve its target if the target exceeds a Batch account node or core quota.</span></span> <span data-ttu-id="a6e17-172">如果目標超過訂用帳戶的共用核心配額，以使用者訂用帳戶設定建立之帳戶中的集區可能未達到其目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-172">A pool in an account created with the User Subscription configuration may not achieve its target if the target exceeds the shared core quota for the subscription.</span></span>|
| <span data-ttu-id="a6e17-173">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-173">$TargetLowPriorityNodes</span></span> |<span data-ttu-id="a6e17-174">集區之低優先順序計算節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-174">The target number of low-priority compute nodes for the pool.</span></span> <span data-ttu-id="a6e17-175">低優先順序節點數目被指定作為目標，因為集區不一定會達到想要的節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-175">The number of low-priority nodes is specified as a target because a pool may not always achieve the desired number of nodes.</span></span> <span data-ttu-id="a6e17-176">例如，如果在集區達到初始目標之前，自動調整評估修改目標低優先順序節點數目，則集區可能未達到目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-176">For example, if the target number of low-priority nodes is modified by an autoscale evaluation before the pool has reached the initial target, then the pool may not reach the target.</span></span> <span data-ttu-id="a6e17-177">如果目標超過 Batch 帳戶節點或核心配額，則集區也可能未達到其目標。</span><span class="sxs-lookup"><span data-stu-id="a6e17-177">A pool may also not achieve its target if the target exceeds a Batch account node or core quota.</span></span> <br /><br /> <span data-ttu-id="a6e17-178">如需有關低優先順序計算節點的詳細資訊，請參閱[搭配 Batch 使用低優先順序 VM (預覽)](batch-low-pri-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-178">For more information on low-priority compute nodes, see [Use low-priority VMs with Batch (Preview)](batch-low-pri-vms.md).</span></span> |
| <span data-ttu-id="a6e17-179">$NodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="a6e17-179">$NodeDeallocationOption</span></span> |<span data-ttu-id="a6e17-180">計算節點從集區移除時所發生的動作。</span><span class="sxs-lookup"><span data-stu-id="a6e17-180">The action that occurs when compute nodes are removed from a pool.</span></span> <span data-ttu-id="a6e17-181">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="a6e17-181">Possible values are:</span></span><ul><li><span data-ttu-id="a6e17-182">**requeue**：立即終止工作，並將這些工作放回工作佇列，為它們重新排程。</span><span class="sxs-lookup"><span data-stu-id="a6e17-182">**requeue**--Terminates tasks immediately and puts them back on the job queue so that they are rescheduled.</span></span><li><span data-ttu-id="a6e17-183">**terminate**：立即終止工作，並從作業佇列移除這些工作。</span><span class="sxs-lookup"><span data-stu-id="a6e17-183">**terminate**--Terminates tasks immediately and removes them from the job queue.</span></span><li><span data-ttu-id="a6e17-184">**taskcompletion**：等待目前執行中的工作完成，然後再從集區中移除該節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-184">**taskcompletion**--Waits for currently running tasks to finish and then removes the node from the pool.</span></span><li><span data-ttu-id="a6e17-185">**retaineddata**：等待所有本機工作保留在節點上的資料先清除，再從集區移除節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-185">**retaineddata**--Waits for all the local task-retained data on the node to be cleaned up before removing the node from the pool.</span></span></ul> |

<span data-ttu-id="a6e17-186">您可以取得這些服務定義的變數值，以根據 Batch 服務提供的計量進行調整：</span><span class="sxs-lookup"><span data-stu-id="a6e17-186">You can get the value of these service-defined variables to make adjustments that are based on metrics from the Batch service:</span></span>

| <span data-ttu-id="a6e17-187">唯讀服務定義變數</span><span class="sxs-lookup"><span data-stu-id="a6e17-187">Read-only service-defined variables</span></span> | <span data-ttu-id="a6e17-188">說明</span><span class="sxs-lookup"><span data-stu-id="a6e17-188">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6e17-189">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="a6e17-189">$CPUPercent</span></span> |<span data-ttu-id="a6e17-190">CPU 使用量的平均百分比。</span><span class="sxs-lookup"><span data-stu-id="a6e17-190">The average percentage of CPU usage.</span></span> |
| <span data-ttu-id="a6e17-191">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="a6e17-191">$WallClockSeconds</span></span> |<span data-ttu-id="a6e17-192">已耗用的秒數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-192">The number of seconds consumed.</span></span> |
| <span data-ttu-id="a6e17-193">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-193">$MemoryBytes</span></span> |<span data-ttu-id="a6e17-194">已使用的平均 MB 數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-194">The average number of megabytes used.</span></span> |
| <span data-ttu-id="a6e17-195">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-195">$DiskBytes</span></span> |<span data-ttu-id="a6e17-196">已在本機磁碟上使用的平均 GB 數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-196">The average number of gigabytes used on the local disks.</span></span> |
| <span data-ttu-id="a6e17-197">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-197">$DiskReadBytes</span></span> |<span data-ttu-id="a6e17-198">已讀取的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-198">The number of bytes read.</span></span> |
| <span data-ttu-id="a6e17-199">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-199">$DiskWriteBytes</span></span> |<span data-ttu-id="a6e17-200">已寫入的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-200">The number of bytes written.</span></span> |
| <span data-ttu-id="a6e17-201">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="a6e17-201">$DiskReadOps</span></span> |<span data-ttu-id="a6e17-202">已執行的讀取磁碟作業計數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-202">The count of read disk operations performed.</span></span> |
| <span data-ttu-id="a6e17-203">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="a6e17-203">$DiskWriteOps</span></span> |<span data-ttu-id="a6e17-204">已執行的寫入磁碟作業計數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-204">The count of write disk operations performed.</span></span> |
| <span data-ttu-id="a6e17-205">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-205">$NetworkInBytes</span></span> |<span data-ttu-id="a6e17-206">輸入位元組的數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-206">The number of inbound bytes.</span></span> |
| <span data-ttu-id="a6e17-207">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-207">$NetworkOutBytes</span></span> |<span data-ttu-id="a6e17-208">輸出位元組的數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-208">The number of outbound bytes.</span></span> |
| <span data-ttu-id="a6e17-209">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="a6e17-209">$SampleNodeCount</span></span> |<span data-ttu-id="a6e17-210">計算節點的計數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-210">The count of compute nodes.</span></span> |
| <span data-ttu-id="a6e17-211">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-211">$ActiveTasks</span></span> |<span data-ttu-id="a6e17-212">準備好執行但還未執行的工作數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-212">The number of tasks that are ready to execute but are not yet executing.</span></span> <span data-ttu-id="a6e17-213">$ActiveTasks 計數包含處於作用中狀態，而且已滿足其相依性的所有工作。</span><span class="sxs-lookup"><span data-stu-id="a6e17-213">The $ActiveTasks count includes all tasks that are in the active state and whose dependencies have been satisfied.</span></span> <span data-ttu-id="a6e17-214">處於作用中狀態但未滿足其相依性的任何工作會從 $ActiveTasks 計數排除。</span><span class="sxs-lookup"><span data-stu-id="a6e17-214">Any tasks that are in the active state but whose dependencies have not been satisfied are excluded from the $ActiveTasks count.</span></span>|
| <span data-ttu-id="a6e17-215">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-215">$RunningTasks</span></span> |<span data-ttu-id="a6e17-216">處於執行中狀態的工作數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-216">The number of tasks in a running state.</span></span> |
| <span data-ttu-id="a6e17-217">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-217">$PendingTasks</span></span> |<span data-ttu-id="a6e17-218">$ActiveTasks 和 $RunningTasks 的總和。</span><span class="sxs-lookup"><span data-stu-id="a6e17-218">The sum of $ActiveTasks and $RunningTasks.</span></span> |
| <span data-ttu-id="a6e17-219">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-219">$SucceededTasks</span></span> |<span data-ttu-id="a6e17-220">已成功完成的工作數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-220">The number of tasks that finished successfully.</span></span> |
| <span data-ttu-id="a6e17-221">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-221">$FailedTasks</span></span> |<span data-ttu-id="a6e17-222">失敗的工作數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-222">The number of tasks that failed.</span></span> |
| <span data-ttu-id="a6e17-223">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-223">$CurrentDedicatedNodes</span></span> |<span data-ttu-id="a6e17-224">目前的專用計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-224">The current number of dedicated compute nodes.</span></span> |
| <span data-ttu-id="a6e17-225">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-225">$CurrentLowPriorityNodes</span></span> |<span data-ttu-id="a6e17-226">低優先順序計算節點的目前數目，包括任何已被優先佔用的節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-226">The current number of low-priority compute nodes, including any nodes that have been pre-empted.</span></span> |
| <span data-ttu-id="a6e17-227">$PreemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="a6e17-227">$PreemptedNodeCount</span></span> | <span data-ttu-id="a6e17-228">優先佔用狀態的集區中之節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-228">The number of nodes in the pool that are in a pre-empted state.</span></span> |

> [!TIP]
> <span data-ttu-id="a6e17-229">上表中服務定義的唯讀變數是可提供各種方法來存取相關聯資料的物件。</span><span class="sxs-lookup"><span data-stu-id="a6e17-229">The read-only, service-defined variables that are shown in the previous table are *objects* that provide various methods to access data associated with each.</span></span> <span data-ttu-id="a6e17-230">如需詳細資訊，請參閱本文稍後的[取得範例資料](#getsampledata)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-230">For more information, see [Obtain sample data](#getsampledata) later in this article.</span></span>
>
>

## <a name="types"></a><span data-ttu-id="a6e17-231">類型</span><span class="sxs-lookup"><span data-stu-id="a6e17-231">Types</span></span>
<span data-ttu-id="a6e17-232">公式中支援以下類型：</span><span class="sxs-lookup"><span data-stu-id="a6e17-232">These types are supported in a formula:</span></span>

* <span data-ttu-id="a6e17-233">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-233">double</span></span>
* <span data-ttu-id="a6e17-234">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-234">doubleVec</span></span>
* <span data-ttu-id="a6e17-235">doubleVecList</span><span class="sxs-lookup"><span data-stu-id="a6e17-235">doubleVecList</span></span>
* <span data-ttu-id="a6e17-236">string</span><span class="sxs-lookup"><span data-stu-id="a6e17-236">string</span></span>
* <span data-ttu-id="a6e17-237">timestamp：timestamp 是包含下列成員的複合結構：</span><span class="sxs-lookup"><span data-stu-id="a6e17-237">timestamp--timestamp is a compound structure that contains the following members:</span></span>

  * <span data-ttu-id="a6e17-238">年</span><span class="sxs-lookup"><span data-stu-id="a6e17-238">year</span></span>
  * <span data-ttu-id="a6e17-239">month (1-12)</span><span class="sxs-lookup"><span data-stu-id="a6e17-239">month (1-12)</span></span>
  * <span data-ttu-id="a6e17-240">day (1-31)</span><span class="sxs-lookup"><span data-stu-id="a6e17-240">day (1-31)</span></span>
  * <span data-ttu-id="a6e17-241">weekday (以數字格式表示，例如 1 代表星期一)</span><span class="sxs-lookup"><span data-stu-id="a6e17-241">weekday (in the format of number; for example, 1 for Monday)</span></span>
  * <span data-ttu-id="a6e17-242">hour (以 24 小時制數字格式表示，例如 13 代表下午 1:00)</span><span class="sxs-lookup"><span data-stu-id="a6e17-242">hour (in 24-hour number format; for example, 13 means 1 PM)</span></span>
  * <span data-ttu-id="a6e17-243">minute (00-59)</span><span class="sxs-lookup"><span data-stu-id="a6e17-243">minute (00-59)</span></span>
  * <span data-ttu-id="a6e17-244">second (00-59)</span><span class="sxs-lookup"><span data-stu-id="a6e17-244">second (00-59)</span></span>
* <span data-ttu-id="a6e17-245">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-245">timeinterval</span></span>

  * <span data-ttu-id="a6e17-246">TimeInterval_Zero</span><span class="sxs-lookup"><span data-stu-id="a6e17-246">TimeInterval_Zero</span></span>
  * <span data-ttu-id="a6e17-247">TimeInterval_100ns</span><span class="sxs-lookup"><span data-stu-id="a6e17-247">TimeInterval_100ns</span></span>
  * <span data-ttu-id="a6e17-248">TimeInterval_Microsecond</span><span class="sxs-lookup"><span data-stu-id="a6e17-248">TimeInterval_Microsecond</span></span>
  * <span data-ttu-id="a6e17-249">TimeInterval_Millisecond</span><span class="sxs-lookup"><span data-stu-id="a6e17-249">TimeInterval_Millisecond</span></span>
  * <span data-ttu-id="a6e17-250">TimeInterval_Second</span><span class="sxs-lookup"><span data-stu-id="a6e17-250">TimeInterval_Second</span></span>
  * <span data-ttu-id="a6e17-251">TimeInterval_Minute</span><span class="sxs-lookup"><span data-stu-id="a6e17-251">TimeInterval_Minute</span></span>
  * <span data-ttu-id="a6e17-252">TimeInterval_Hour</span><span class="sxs-lookup"><span data-stu-id="a6e17-252">TimeInterval_Hour</span></span>
  * <span data-ttu-id="a6e17-253">TimeInterval_Day</span><span class="sxs-lookup"><span data-stu-id="a6e17-253">TimeInterval_Day</span></span>
  * <span data-ttu-id="a6e17-254">TimeInterval_Week</span><span class="sxs-lookup"><span data-stu-id="a6e17-254">TimeInterval_Week</span></span>
  * <span data-ttu-id="a6e17-255">TimeInterval_Year</span><span class="sxs-lookup"><span data-stu-id="a6e17-255">TimeInterval_Year</span></span>

## <a name="operations"></a><span data-ttu-id="a6e17-256">作業</span><span class="sxs-lookup"><span data-stu-id="a6e17-256">Operations</span></span>
<span data-ttu-id="a6e17-257">上一節列出的類型允許這些作業。</span><span class="sxs-lookup"><span data-stu-id="a6e17-257">These operations are allowed on the types that are listed in the previous section.</span></span>

| <span data-ttu-id="a6e17-258">作業</span><span class="sxs-lookup"><span data-stu-id="a6e17-258">Operation</span></span> | <span data-ttu-id="a6e17-259">支援的運算子</span><span class="sxs-lookup"><span data-stu-id="a6e17-259">Supported operators</span></span> | <span data-ttu-id="a6e17-260">結果類型</span><span class="sxs-lookup"><span data-stu-id="a6e17-260">Result type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6e17-261">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="a6e17-261">double *operator* double</span></span> |<span data-ttu-id="a6e17-262">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="a6e17-262">+, -, *, /</span></span> |<span data-ttu-id="a6e17-263">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-263">double</span></span> |
| <span data-ttu-id="a6e17-264">double 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-264">double *operator* timeinterval</span></span> |* |<span data-ttu-id="a6e17-265">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-265">timeinterval</span></span> |
| <span data-ttu-id="a6e17-266">doubleVec 運算子  double</span><span class="sxs-lookup"><span data-stu-id="a6e17-266">doubleVec *operator* double</span></span> |<span data-ttu-id="a6e17-267">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="a6e17-267">+, -, *, /</span></span> |<span data-ttu-id="a6e17-268">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-268">doubleVec</span></span> |
| <span data-ttu-id="a6e17-269">doubleVec 運算子  doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-269">doubleVec *operator* doubleVec</span></span> |<span data-ttu-id="a6e17-270">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="a6e17-270">+, -, *, /</span></span> |<span data-ttu-id="a6e17-271">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-271">doubleVec</span></span> |
| <span data-ttu-id="a6e17-272">timeinterval 運算子  double</span><span class="sxs-lookup"><span data-stu-id="a6e17-272">timeinterval *operator* double</span></span> |<span data-ttu-id="a6e17-273">*、/</span><span class="sxs-lookup"><span data-stu-id="a6e17-273">*, /</span></span> |<span data-ttu-id="a6e17-274">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-274">timeinterval</span></span> |
| <span data-ttu-id="a6e17-275">timeinterval 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-275">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="a6e17-276">+、-</span><span class="sxs-lookup"><span data-stu-id="a6e17-276">+, -</span></span> |<span data-ttu-id="a6e17-277">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-277">timeinterval</span></span> |
| <span data-ttu-id="a6e17-278">timeinterval 運算子  timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-278">timeinterval *operator* timestamp</span></span> |+ |<span data-ttu-id="a6e17-279">timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-279">timestamp</span></span> |
| <span data-ttu-id="a6e17-280">timestamp 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-280">timestamp *operator* timeinterval</span></span> |+ |<span data-ttu-id="a6e17-281">timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-281">timestamp</span></span> |
| <span data-ttu-id="a6e17-282">timestamp  timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-282">timestamp *operator* timestamp</span></span> |- |<span data-ttu-id="a6e17-283">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-283">timeinterval</span></span> |
| <span data-ttu-id="a6e17-284">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-284">*operator*double</span></span> |<span data-ttu-id="a6e17-285">-、!</span><span class="sxs-lookup"><span data-stu-id="a6e17-285">-, !</span></span> |<span data-ttu-id="a6e17-286">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-286">double</span></span> |
| <span data-ttu-id="a6e17-287">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-287">*operator*timeinterval</span></span> |- |<span data-ttu-id="a6e17-288">timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-288">timeinterval</span></span> |
| <span data-ttu-id="a6e17-289">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="a6e17-289">double *operator* double</span></span> |<span data-ttu-id="a6e17-290"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="a6e17-290"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="a6e17-291">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-291">double</span></span> |
| <span data-ttu-id="a6e17-292">string  string</span><span class="sxs-lookup"><span data-stu-id="a6e17-292">string *operator* string</span></span> |<span data-ttu-id="a6e17-293"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="a6e17-293"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="a6e17-294">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-294">double</span></span> |
| <span data-ttu-id="a6e17-295">timestamp  timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-295">timestamp *operator* timestamp</span></span> |<span data-ttu-id="a6e17-296"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="a6e17-296"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="a6e17-297">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-297">double</span></span> |
| <span data-ttu-id="a6e17-298">timeinterval 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="a6e17-298">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="a6e17-299"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="a6e17-299"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="a6e17-300">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-300">double</span></span> |
| <span data-ttu-id="a6e17-301">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="a6e17-301">double *operator* double</span></span> |<span data-ttu-id="a6e17-302">&&, &#124;&#124;</span><span class="sxs-lookup"><span data-stu-id="a6e17-302">&&, &#124;&#124;</span></span> |<span data-ttu-id="a6e17-303">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-303">double</span></span> |

<span data-ttu-id="a6e17-304">測試具有三元運算子的雙精準數 (`double ? statement1 : statement2`) 時，非零為 **true**，而零則為 **false**。</span><span class="sxs-lookup"><span data-stu-id="a6e17-304">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span></span>

## <a name="functions"></a><span data-ttu-id="a6e17-305">Functions</span><span class="sxs-lookup"><span data-stu-id="a6e17-305">Functions</span></span>
<span data-ttu-id="a6e17-306">這些預先定義的 **函式** 可供您用來定義自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-306">These predefined **functions** are available for you to use in defining an automatic scaling formula.</span></span>

| <span data-ttu-id="a6e17-307">函式</span><span class="sxs-lookup"><span data-stu-id="a6e17-307">Function</span></span> | <span data-ttu-id="a6e17-308">傳回類型</span><span class="sxs-lookup"><span data-stu-id="a6e17-308">Return type</span></span> | <span data-ttu-id="a6e17-309">說明</span><span class="sxs-lookup"><span data-stu-id="a6e17-309">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6e17-310">avg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-310">avg(doubleVecList)</span></span> |<span data-ttu-id="a6e17-311">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-311">double</span></span> |<span data-ttu-id="a6e17-312">傳回 doubleVecList 中所有值的平均值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-312">Returns the average value for all values in the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-313">len(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-313">len(doubleVecList)</span></span> |<span data-ttu-id="a6e17-314">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-314">double</span></span> |<span data-ttu-id="a6e17-315">傳回 doubleVecList 建立的向量的長度。</span><span class="sxs-lookup"><span data-stu-id="a6e17-315">Returns the length of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-316">lg(double)</span><span class="sxs-lookup"><span data-stu-id="a6e17-316">lg(double)</span></span> |<span data-ttu-id="a6e17-317">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-317">double</span></span> |<span data-ttu-id="a6e17-318">傳回 double 的對數底數 2。</span><span class="sxs-lookup"><span data-stu-id="a6e17-318">Returns the log base 2 of the double.</span></span> |
| <span data-ttu-id="a6e17-319">lg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-319">lg(doubleVecList)</span></span> |<span data-ttu-id="a6e17-320">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-320">doubleVec</span></span> |<span data-ttu-id="a6e17-321">傳回 doubleVecList 的全元件對數底數 2。</span><span class="sxs-lookup"><span data-stu-id="a6e17-321">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="a6e17-322">vec(double) 必須針對此參數明確傳遞。</span><span class="sxs-lookup"><span data-stu-id="a6e17-322">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="a6e17-323">否則會假設為 double lg(double) 版本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-323">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="a6e17-324">ln(double)</span><span class="sxs-lookup"><span data-stu-id="a6e17-324">ln(double)</span></span> |<span data-ttu-id="a6e17-325">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-325">double</span></span> |<span data-ttu-id="a6e17-326">傳回 double 的自然底數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-326">Returns the natural log of the double.</span></span> |
| <span data-ttu-id="a6e17-327">ln(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-327">ln(doubleVecList)</span></span> |<span data-ttu-id="a6e17-328">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-328">doubleVec</span></span> |<span data-ttu-id="a6e17-329">傳回 doubleVecList 的全元件對數底數 2。</span><span class="sxs-lookup"><span data-stu-id="a6e17-329">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="a6e17-330">vec(double) 必須針對此參數明確傳遞。</span><span class="sxs-lookup"><span data-stu-id="a6e17-330">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="a6e17-331">否則會假設為 double lg(double) 版本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-331">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="a6e17-332">log(double)</span><span class="sxs-lookup"><span data-stu-id="a6e17-332">log(double)</span></span> |<span data-ttu-id="a6e17-333">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-333">double</span></span> |<span data-ttu-id="a6e17-334">傳回 double 的對數底數 10。</span><span class="sxs-lookup"><span data-stu-id="a6e17-334">Returns the log base 10 of the double.</span></span> |
| <span data-ttu-id="a6e17-335">log(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-335">log(doubleVecList)</span></span> |<span data-ttu-id="a6e17-336">doubleVec</span><span class="sxs-lookup"><span data-stu-id="a6e17-336">doubleVec</span></span> |<span data-ttu-id="a6e17-337">傳回 doubleVecList 的全元件對數底數 10。</span><span class="sxs-lookup"><span data-stu-id="a6e17-337">Returns the component-wise log base 10 of the doubleVecList.</span></span> <span data-ttu-id="a6e17-338">vec(double) 必須針對單一 double 參數明確傳遞。</span><span class="sxs-lookup"><span data-stu-id="a6e17-338">A vec(double) must be explicitly passed for the single double parameter.</span></span> <span data-ttu-id="a6e17-339">否則，會假設為 double log (double) 版本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-339">Otherwise, the double log(double) version is assumed.</span></span> |
| <span data-ttu-id="a6e17-340">max(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-340">max(doubleVecList)</span></span> |<span data-ttu-id="a6e17-341">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-341">double</span></span> |<span data-ttu-id="a6e17-342">傳回 doubleVecList 中的最大值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-342">Returns the maximum value in the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-343">min(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-343">min(doubleVecList)</span></span> |<span data-ttu-id="a6e17-344">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-344">double</span></span> |<span data-ttu-id="a6e17-345">傳回 doubleVecList 中的最小值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-345">Returns the minimum value in the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-346">norm(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-346">norm(doubleVecList)</span></span> |<span data-ttu-id="a6e17-347">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-347">double</span></span> |<span data-ttu-id="a6e17-348">傳回 doubleVecList 建立的向量的 2-norm。</span><span class="sxs-lookup"><span data-stu-id="a6e17-348">Returns the two-norm of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-349">percentile(doubleVec v, double p)</span><span class="sxs-lookup"><span data-stu-id="a6e17-349">percentile(doubleVec v, double p)</span></span> |<span data-ttu-id="a6e17-350">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-350">double</span></span> |<span data-ttu-id="a6e17-351">傳回向量 v 的百分位數元素。</span><span class="sxs-lookup"><span data-stu-id="a6e17-351">Returns the percentile element of the vector v.</span></span> |
| <span data-ttu-id="a6e17-352">rand()</span><span class="sxs-lookup"><span data-stu-id="a6e17-352">rand()</span></span> |<span data-ttu-id="a6e17-353">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-353">double</span></span> |<span data-ttu-id="a6e17-354">傳回介於 0.0 到 1.0 之間的隨機值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-354">Returns a random value between 0.0 and 1.0.</span></span> |
| <span data-ttu-id="a6e17-355">range(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-355">range(doubleVecList)</span></span> |<span data-ttu-id="a6e17-356">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-356">double</span></span> |<span data-ttu-id="a6e17-357">傳回 doubleVecList 中最小和最大值之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a6e17-357">Returns the difference between the min and max values in the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-358">std(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-358">std(doubleVecList)</span></span> |<span data-ttu-id="a6e17-359">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-359">double</span></span> |<span data-ttu-id="a6e17-360">傳回 doubleVecList 中值的標準差範例。</span><span class="sxs-lookup"><span data-stu-id="a6e17-360">Returns the sample standard deviation of the values in the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-361">stop()</span><span class="sxs-lookup"><span data-stu-id="a6e17-361">stop()</span></span> | |<span data-ttu-id="a6e17-362">停止評估自動調整運算式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-362">Stops evaluation of the autoscaling expression.</span></span> |
| <span data-ttu-id="a6e17-363">sum(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="a6e17-363">sum(doubleVecList)</span></span> |<span data-ttu-id="a6e17-364">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-364">double</span></span> |<span data-ttu-id="a6e17-365">傳回 doubleVecList 所有元件的總和。</span><span class="sxs-lookup"><span data-stu-id="a6e17-365">Returns the sum of all the components of the doubleVecList.</span></span> |
| <span data-ttu-id="a6e17-366">time(string dateTime="")</span><span class="sxs-lookup"><span data-stu-id="a6e17-366">time(string dateTime="")</span></span> |<span data-ttu-id="a6e17-367">timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-367">timestamp</span></span> |<span data-ttu-id="a6e17-368">如果未傳遞參數，則傳回目前時間的時間戳記，如果有傳遞參數，則為 dateTime 字串的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="a6e17-368">Returns the time stamp of the current time if no parameters are passed, or the time stamp of the dateTime string if it is passed.</span></span> <span data-ttu-id="a6e17-369">支援的 dateTime 格式為 W3C-DTF 和 RFC 1123。</span><span class="sxs-lookup"><span data-stu-id="a6e17-369">Supported dateTime formats are W3C-DTF and RFC 1123.</span></span> |
| <span data-ttu-id="a6e17-370">val(doubleVec v, double i)</span><span class="sxs-lookup"><span data-stu-id="a6e17-370">val(doubleVec v, double i)</span></span> |<span data-ttu-id="a6e17-371">double</span><span class="sxs-lookup"><span data-stu-id="a6e17-371">double</span></span> |<span data-ttu-id="a6e17-372">傳回向量 v 中位置 i 的元素值，起始索引為零。</span><span class="sxs-lookup"><span data-stu-id="a6e17-372">Returns the value of the element that is at location i in vector v, with a starting index of zero.</span></span> |

<span data-ttu-id="a6e17-373">上表中所述的某些函式可以接受清單作為引數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-373">Some of the functions that are described in the previous table can accept a list as an argument.</span></span> <span data-ttu-id="a6e17-374">逗號分隔清單是 *double* 和 *doubleVec* 的任意組合。</span><span class="sxs-lookup"><span data-stu-id="a6e17-374">The comma-separated list is any combination of *double* and *doubleVec*.</span></span> <span data-ttu-id="a6e17-375">例如：</span><span class="sxs-lookup"><span data-stu-id="a6e17-375">For example:</span></span>

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

<span data-ttu-id="a6e17-376">評估之前，*doubleVecList* 值會轉換成單一的 *doubleVec*。</span><span class="sxs-lookup"><span data-stu-id="a6e17-376">The *doubleVecList* value is converted to a single *doubleVec* before evaluation.</span></span> <span data-ttu-id="a6e17-377">例如，如果 `v = [1,2,3]`，呼叫 `avg(v)` 就相當於呼叫 `avg(1,2,3)`。</span><span class="sxs-lookup"><span data-stu-id="a6e17-377">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent to calling `avg(1,2,3)`.</span></span> <span data-ttu-id="a6e17-378">呼叫 `avg(v, 7)` 就相當於呼叫 `avg(1,2,3,7)`。</span><span class="sxs-lookup"><span data-stu-id="a6e17-378">Calling `avg(v, 7)` is equivalent to calling `avg(1,2,3,7)`.</span></span>

## <span data-ttu-id="a6e17-379"><a name="getsampledata"></a>取得樣本資料</span><span class="sxs-lookup"><span data-stu-id="a6e17-379"><a name="getsampledata"></a>Obtain sample data</span></span>
<span data-ttu-id="a6e17-380">自動調整公式會對 Batch 服務所提供的度量資料 (範例) 產生作用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-380">Autoscale formulas act on metrics data (samples) that is provided by the Batch service.</span></span> <span data-ttu-id="a6e17-381">公式會根據從服務取得的值擴大或縮減集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-381">A formula grows or shrinks pool size based on the values that it obtains from the service.</span></span> <span data-ttu-id="a6e17-382">上述服務定義的變數是可提供各種方法來存取與該物件相關聯資料的物件。</span><span class="sxs-lookup"><span data-stu-id="a6e17-382">The service-defined variables that were described previously are objects that provide various methods to access data that is associated with that object.</span></span> <span data-ttu-id="a6e17-383">例如，下列運算式顯示取得最後五分鐘的 CPU 使用量的要求：</span><span class="sxs-lookup"><span data-stu-id="a6e17-383">For example, the following expression shows a request to get the last five minutes of CPU usage:</span></span>

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| <span data-ttu-id="a6e17-384">方法</span><span class="sxs-lookup"><span data-stu-id="a6e17-384">Method</span></span> | <span data-ttu-id="a6e17-385">說明</span><span class="sxs-lookup"><span data-stu-id="a6e17-385">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6e17-386">GetSample()</span><span class="sxs-lookup"><span data-stu-id="a6e17-386">GetSample()</span></span> |<span data-ttu-id="a6e17-387">`GetSample()` 方法會傳回資料樣本的向量。</span><span class="sxs-lookup"><span data-stu-id="a6e17-387">The `GetSample()` method returns a vector of data samples.</span></span><br/><br/><span data-ttu-id="a6e17-388">一個樣本有 30 秒的度量資料。</span><span class="sxs-lookup"><span data-stu-id="a6e17-388">A sample is 30 seconds worth of metrics data.</span></span> <span data-ttu-id="a6e17-389">換句話說，每隔 30 秒會取得範例。</span><span class="sxs-lookup"><span data-stu-id="a6e17-389">In other words, samples are obtained every 30 seconds.</span></span> <span data-ttu-id="a6e17-390">如下所述，從收集樣本到可用於公式之間會延遲。</span><span class="sxs-lookup"><span data-stu-id="a6e17-390">But as noted below, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="a6e17-391">因此，並非一段指定時間內的所有樣本都可供公式評估。</span><span class="sxs-lookup"><span data-stu-id="a6e17-391">As such, not all samples for a given time period may be available for evaluation by a formula.</span></span><ul><li>`doubleVec GetSample(double count)`<br/><span data-ttu-id="a6e17-392">指定要從最近收集的樣本中取得的樣本數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-392">Specifies the number of samples to obtain from the most recent samples that were collected.</span></span><br/><br/><span data-ttu-id="a6e17-393">`GetSample(1)` 會傳回最後一個可用的樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-393">`GetSample(1)` returns the last available sample.</span></span> <span data-ttu-id="a6e17-394">不過，這不適用於 `$CPUPercent` 之類的度量，因為不可能知道「何時」收集到樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-394">For metrics like `$CPUPercent`, however, this should not be used because it is impossible to know *when* the sample was collected.</span></span> <span data-ttu-id="a6e17-395">此範例可能是最新的，也可能因為系統問題，是更舊的。</span><span class="sxs-lookup"><span data-stu-id="a6e17-395">It might be recent, or, because of system issues, it might be much older.</span></span> <span data-ttu-id="a6e17-396">在此情況下，最好使用如下所示的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="a6e17-396">It is better in such cases to use a time interval as shown below.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/><span data-ttu-id="a6e17-397">指定收集樣本資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a6e17-397">Specifies a time frame for gathering sample data.</span></span> <span data-ttu-id="a6e17-398">它也會選擇性地指定在要求的時間範圍內必須可用的樣本數百分比。</span><span class="sxs-lookup"><span data-stu-id="a6e17-398">Optionally, it also specifies the percentage of samples that must be available in the requested time frame.</span></span><br/><br/><span data-ttu-id="a6e17-399">如果 CPUPercent 歷程記錄中有最後 10 分鐘的所有樣本，則 `$CPUPercent.GetSample(TimeInterval_Minute * 10)` 會傳回 20 個樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for the last 10 minutes are present in the CPUPercent history.</span></span> <span data-ttu-id="a6e17-400">不過，如果最後一分鐘的歷程記錄無法使用，則只會傳回 18 個樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-400">If the last minute of history was not available, however, only 18 samples would be returned.</span></span> <span data-ttu-id="a6e17-401">在此案例中：</span><span class="sxs-lookup"><span data-stu-id="a6e17-401">In this case:</span></span><br/><br/><span data-ttu-id="a6e17-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` 會失敗，因為只有 90% 的樣本可用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of the samples are available.</span></span><br/><br/><span data-ttu-id="a6e17-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` 會成功。</span><span class="sxs-lookup"><span data-stu-id="a6e17-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/><span data-ttu-id="a6e17-404">指定收集資料的時間範圍 (含開始時間和結束時間)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-404">Specifies a time frame for gathering data, with both a start time and an end time.</span></span><br/><br/><span data-ttu-id="a6e17-405">如上所述，從收集樣本到可用於公式之間會延遲。</span><span class="sxs-lookup"><span data-stu-id="a6e17-405">As mentioned above, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="a6e17-406">當您使用 `GetSample` 方法時，請考慮此延遲。</span><span class="sxs-lookup"><span data-stu-id="a6e17-406">Consider this delay when you use the `GetSample` method.</span></span> <span data-ttu-id="a6e17-407">請參閱下文中的 `GetSamplePercent`。</span><span class="sxs-lookup"><span data-stu-id="a6e17-407">See `GetSamplePercent` below.</span></span> |
| <span data-ttu-id="a6e17-408">GetSamplePeriod()</span><span class="sxs-lookup"><span data-stu-id="a6e17-408">GetSamplePeriod()</span></span> |<span data-ttu-id="a6e17-409">傳回歷史範例資料集中取得範例的期間。</span><span class="sxs-lookup"><span data-stu-id="a6e17-409">Returns the period of samples that were taken in a historical sample data set.</span></span> |
| <span data-ttu-id="a6e17-410">Count()</span><span class="sxs-lookup"><span data-stu-id="a6e17-410">Count()</span></span> |<span data-ttu-id="a6e17-411">傳回度量歷程記錄中的範例總數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-411">Returns the total number of samples in the metric history.</span></span> |
| <span data-ttu-id="a6e17-412">HistoryBeginTime()</span><span class="sxs-lookup"><span data-stu-id="a6e17-412">HistoryBeginTime()</span></span> |<span data-ttu-id="a6e17-413">傳回度量的最舊可用資料範例的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="a6e17-413">Returns the time stamp of the oldest available data sample for the metric.</span></span> |
| <span data-ttu-id="a6e17-414">GetSamplePercent()</span><span class="sxs-lookup"><span data-stu-id="a6e17-414">GetSamplePercent()</span></span> |<span data-ttu-id="a6e17-415">傳回指定的時間間隔內可用的樣本百分比。</span><span class="sxs-lookup"><span data-stu-id="a6e17-415">Returns the percentage of samples that are available for a given time interval.</span></span> <span data-ttu-id="a6e17-416">例如：</span><span class="sxs-lookup"><span data-stu-id="a6e17-416">For example:</span></span><br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/><span data-ttu-id="a6e17-417">因為 `GetSample` 方法在傳回樣本的百分比小於指定的 `samplePercent` 時會失敗，因此，您可以先使用 `GetSamplePercent` 方法進行檢查。</span><span class="sxs-lookup"><span data-stu-id="a6e17-417">Because the `GetSample` method fails if the percentage of samples returned is less than the `samplePercent` specified, you can use the `GetSamplePercent` method to check first.</span></span> <span data-ttu-id="a6e17-418">然後您可以在樣本不足時執行替代動作，而不暫停自動調整評估。</span><span class="sxs-lookup"><span data-stu-id="a6e17-418">Then you can perform an alternate action if insufficient samples are present, without halting the automatic scaling evaluation.</span></span> |

### <a name="samples-sample-percentage-and-the-getsample-method"></a><span data-ttu-id="a6e17-419">樣本、樣本百分比和 GetSample()  方法</span><span class="sxs-lookup"><span data-stu-id="a6e17-419">Samples, sample percentage, and the *GetSample()* method</span></span>
<span data-ttu-id="a6e17-420">自動調整公式的核心是要取得工作和資源度量資料，然後根據該資料調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-420">The core operation of an autoscale formula is to obtain task and resource metric data and then adjust pool size based on that data.</span></span> <span data-ttu-id="a6e17-421">因此，請務必清楚了解自動調整公式如何與計量資料 (樣本) 互動。</span><span class="sxs-lookup"><span data-stu-id="a6e17-421">As such, it is important to have a clear understanding of how autoscale formulas interact with metrics data (samples).</span></span>

<span data-ttu-id="a6e17-422">**範例**</span><span class="sxs-lookup"><span data-stu-id="a6e17-422">**Samples**</span></span>

<span data-ttu-id="a6e17-423">Batch 服務會定期取得工作和資源計量的樣本，使其可供自動調整公式使用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-423">The Batch service periodically takes samples of task and resource metrics and makes them available to your autoscale formulas.</span></span> <span data-ttu-id="a6e17-424">Batch 服務會每隔 30 秒記錄一次這些樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-424">These samples are recorded every 30 seconds by the Batch service.</span></span> <span data-ttu-id="a6e17-425">不過，記錄樣本的時間與樣本可供自動調整公式使用 (與讀取) 的時間之間有所延遲。</span><span class="sxs-lookup"><span data-stu-id="a6e17-425">However, there is typically a delay between when those samples were recorded and when they are made available to (and can be read by) your autoscale formulas.</span></span> <span data-ttu-id="a6e17-426">此外，由於各種因素 (例如網路或其他基礎結構問題)，可能未在特定間隔內記錄樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-426">Additionally, due to various factors such as network or other infrastructure issues, samples may not be recorded for a particular interval.</span></span>

<span data-ttu-id="a6e17-427">**樣本百分比**</span><span class="sxs-lookup"><span data-stu-id="a6e17-427">**Sample percentage**</span></span>

<span data-ttu-id="a6e17-428">將 `samplePercent` 傳遞至 `GetSample()` 方法，或呼叫 `GetSamplePercent()` 方法時，_percent_ 是指 Batch 服務可能記錄的樣本總數，與自動調整公式實際可用的樣本數目之間的比較。</span><span class="sxs-lookup"><span data-stu-id="a6e17-428">When `samplePercent` is passed to the `GetSample()` method or the `GetSamplePercent()` method is called, _percent_ refers to a comparison between the total possible number of samples that are recorded by the Batch service and the number of samples that are available to your autoscale formula.</span></span>

<span data-ttu-id="a6e17-429">讓我們以 10 分鐘的時間範圍為例。</span><span class="sxs-lookup"><span data-stu-id="a6e17-429">Let's look at a 10-minute timespan as an example.</span></span> <span data-ttu-id="a6e17-430">因為會每隔 30 秒記錄一次樣本，所以在 10 分鐘的時間範圍內，Batch 服務所記錄的樣本總數就已達到 20 個樣本 (每分鐘 2 個)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-430">Because samples are recorded every 30 seconds within a 10-minute timespan, the maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span></span> <span data-ttu-id="a6e17-431">不過，由於回報機制固有的延遲，以及 Azure 中的其他問題，可能只有 15 個樣本可供自動調整公式讀取。</span><span class="sxs-lookup"><span data-stu-id="a6e17-431">However, due to the inherent latency of the reporting mechanism and other issues within Azure, there may be only 15 samples that are available to your autoscale formula for reading.</span></span> <span data-ttu-id="a6e17-432">因此，舉例來說，在這 10 分鐘的期間內，記錄的樣本總數只有 75% 可供您的公式使用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-432">So, for example, for that 10-minute period, only 75% of the total number of samples recorded may be available to your formula.</span></span>

<span data-ttu-id="a6e17-433">**GetSample() 和樣本範圍**</span><span class="sxs-lookup"><span data-stu-id="a6e17-433">**GetSample() and sample ranges**</span></span>

<span data-ttu-id="a6e17-434">您的自動調整公式即將擴大和縮減您的集區 &mdash; 新增節點或移除節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-434">Your autoscale formulas are going to be growing and shrinking your pools &mdash; adding nodes or removing nodes.</span></span> <span data-ttu-id="a6e17-435">因為節點為付費使用，您想要確保您的公式使用根據充足資料的明智的分析方法。</span><span class="sxs-lookup"><span data-stu-id="a6e17-435">Because nodes cost you money, you want to ensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span></span> <span data-ttu-id="a6e17-436">因此，建議您在公式中使用趨勢類型分析。</span><span class="sxs-lookup"><span data-stu-id="a6e17-436">Therefore, we recommend that you use a trending-type analysis in your formulas.</span></span> <span data-ttu-id="a6e17-437">此類型會根據所收集樣本的範圍來擴大和縮減集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-437">This type grows and shrinks your pools based on a range of collected samples.</span></span>

<span data-ttu-id="a6e17-438">若要這樣做，請使用 `GetSample(interval look-back start, interval look-back end)` 傳回樣本的向量：</span><span class="sxs-lookup"><span data-stu-id="a6e17-438">To do so, use `GetSample(interval look-back start, interval look-back end)` to return a vector of samples:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

<span data-ttu-id="a6e17-439">Batch 評估上述程式碼後，它會以值的向量形式傳回樣本範圍。</span><span class="sxs-lookup"><span data-stu-id="a6e17-439">When the above line is evaluated by Batch, it returns a range of samples as a vector of values.</span></span> <span data-ttu-id="a6e17-440">例如：</span><span class="sxs-lookup"><span data-stu-id="a6e17-440">For example:</span></span>

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

<span data-ttu-id="a6e17-441">收集樣本向量後，您便可使用 `min()`、`max()` 和 `avg()` 等函式從所收集的範圍衍生出有意義的值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-441">Once you've collected the vector of samples, you can then use functions like `min()`, `max()`, and `avg()` to derive meaningful values from the collected range.</span></span>

<span data-ttu-id="a6e17-442">若要增加安全性，如果特定一段時間可用的樣本小於特定百分比，您可以強制公式評估為失敗。</span><span class="sxs-lookup"><span data-stu-id="a6e17-442">For additional security, you can force a formula evaluation to fail if less than a certain sample percentage is available for a particular time period.</span></span> <span data-ttu-id="a6e17-443">強制公式評估為失敗會指示 Batch 在指定的樣本百分比無法使用時停止進一步評估公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-443">When you force a formula evaluation to fail, you instruct Batch to cease further evaluation of the formula if the specified percentage of samples is not available.</span></span> <span data-ttu-id="a6e17-444">在此情況下，不會變更集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-444">In this case, no change is made to the pool size.</span></span> <span data-ttu-id="a6e17-445">若要指定評估成功所需的樣本百分比，請將其指定為 `GetSample()`的第三個參數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-445">To specify a required percentage of samples for the evaluation to succeed, specify it as the third parameter to `GetSample()`.</span></span> <span data-ttu-id="a6e17-446">以下指定了 75% 的樣本需求：</span><span class="sxs-lookup"><span data-stu-id="a6e17-446">Here, a requirement of 75 percent of samples is specified:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

<span data-ttu-id="a6e17-447">因為樣本可用性可能延遲，所以請務必記得指定回顧開始時間早於一分鐘的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a6e17-447">Because there may be a delay in sample availability, it is important to always specify a time range with a look-back start time that is older than one minute.</span></span> <span data-ttu-id="a6e17-448">樣本需要花大約一分鐘的時間才能傳播到整個系統，所以通常無法使用 `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` 範圍中的樣本。</span><span class="sxs-lookup"><span data-stu-id="a6e17-448">It takes approximately one minute for samples to propagate through the system, so samples in the range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span></span> <span data-ttu-id="a6e17-449">同樣地，您可以使用 `GetSample()` 的百分比參數來強制特定樣本百分比需求。</span><span class="sxs-lookup"><span data-stu-id="a6e17-449">Again, you can use the percentage parameter of `GetSample()` to force a particular sample percentage requirement.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6e17-450">我們**強烈建議**您***避免「只」*`GetSample(1)`依賴自動調整公式中的** 。</span><span class="sxs-lookup"><span data-stu-id="a6e17-450">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span></span> <span data-ttu-id="a6e17-451">這是因為 `GetSample(1)` 基本上會向 Batch 服務表示：「不論您多久以前擷取最後一個樣本，請將它提供給我」。</span><span class="sxs-lookup"><span data-stu-id="a6e17-451">This is because `GetSample(1)` essentially says to the Batch service, "Give me the last sample you have, no matter how long ago you retrieved it."</span></span> <span data-ttu-id="a6e17-452">因為它只是單一樣本，而且可能是較舊的樣本，所以可能無法代表最近工作或資源狀態的全貌。</span><span class="sxs-lookup"><span data-stu-id="a6e17-452">Since it is only a single sample, and it may be an older sample, it may not be representative of the larger picture of recent task or resource state.</span></span> <span data-ttu-id="a6e17-453">如果您使用 `GetSample(1)`，請確定它是較大的陳述式，而且不是您的公式所依賴的唯一資料點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-453">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not the only data point that your formula relies on.</span></span>
>
>

## <a name="metrics"></a><span data-ttu-id="a6e17-454">度量</span><span class="sxs-lookup"><span data-stu-id="a6e17-454">Metrics</span></span>
<span data-ttu-id="a6e17-455">您可以在定義公式時使用資源和工作計量。</span><span class="sxs-lookup"><span data-stu-id="a6e17-455">You can use both resource and task metrics when you're defining a formula.</span></span> <span data-ttu-id="a6e17-456">您會根據您取得和評估的度量資料來調整集區中專用節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-456">You adjust the target number of dedicated nodes in the pool based on the metrics data that you obtain and evaluate.</span></span> <span data-ttu-id="a6e17-457">如需每個度量的詳細資訊，請參閱上面的 [變數](#variables) 一節。</span><span class="sxs-lookup"><span data-stu-id="a6e17-457">See the [Variables](#variables) section above for more information on each metric.</span></span>

<table>
  <tr>
    <th><span data-ttu-id="a6e17-458">度量</span><span class="sxs-lookup"><span data-stu-id="a6e17-458">Metric</span></span></th>
    <th><span data-ttu-id="a6e17-459">說明</span><span class="sxs-lookup"><span data-stu-id="a6e17-459">Description</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="a6e17-460"><b>Resource</b></span><span class="sxs-lookup"><span data-stu-id="a6e17-460"><b>Resource</b></span></span></td>
    <td><p><span data-ttu-id="a6e17-461">資源計量是以計算節點的 CPU、頻寬和記憶體使用量以及節點數目為基礎。</span><span class="sxs-lookup"><span data-stu-id="a6e17-461">Resource metrics are based on the CPU, the bandwidth, the memory usage of compute nodes, and the number of nodes.</span></span></p>
        <p> <span data-ttu-id="a6e17-462">這些服務定義的變數適合用於根據節點計數進行調整：</span><span class="sxs-lookup"><span data-stu-id="a6e17-462">These service-defined variables are useful for making adjustments based on node count:</span></span></p>
    <p><ul>
            <li><span data-ttu-id="a6e17-463">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-463">$TargetDedicatedNodes</span></span></li>
            <li><span data-ttu-id="a6e17-464">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-464">$TargetLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="a6e17-465">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-465">$CurrentDedicatedNodes</span></span></li>
            <li><span data-ttu-id="a6e17-466">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="a6e17-466">$CurrentLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="a6e17-467">$preemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="a6e17-467">$preemptedNodeCount</span></span></li>
            <li><span data-ttu-id="a6e17-468">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="a6e17-468">$SampleNodeCount</span></span></li>
    </ul></p>
    <p><span data-ttu-id="a6e17-469">這些服務定義的變數適合用於根據節點資源使用量進行調整：</span><span class="sxs-lookup"><span data-stu-id="a6e17-469">These service-defined variables are useful for making adjustments based on node resource usage:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="a6e17-470">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="a6e17-470">$CPUPercent</span></span></li>
      <li><span data-ttu-id="a6e17-471">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="a6e17-471">$WallClockSeconds</span></span></li>
      <li><span data-ttu-id="a6e17-472">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-472">$MemoryBytes</span></span></li>
      <li><span data-ttu-id="a6e17-473">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-473">$DiskBytes</span></span></li>
      <li><span data-ttu-id="a6e17-474">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-474">$DiskReadBytes</span></span></li>
      <li><span data-ttu-id="a6e17-475">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-475">$DiskWriteBytes</span></span></li>
      <li><span data-ttu-id="a6e17-476">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="a6e17-476">$DiskReadOps</span></span></li>
      <li><span data-ttu-id="a6e17-477">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="a6e17-477">$DiskWriteOps</span></span></li>
      <li><span data-ttu-id="a6e17-478">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-478">$NetworkInBytes</span></span></li>
      <li><span data-ttu-id="a6e17-479">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="a6e17-479">$NetworkOutBytes</span></span></li></ul></p>
  </tr>
  <tr>
    <td><span data-ttu-id="a6e17-480"><b>Task</b></span><span class="sxs-lookup"><span data-stu-id="a6e17-480"><b>Task</b></span></span></td>
    <td><p><span data-ttu-id="a6e17-481">工作計量是根據工作的狀態，例如作用中、暫止和已完成。</span><span class="sxs-lookup"><span data-stu-id="a6e17-481">Task metrics are based on the status of tasks, such as Active, Pending, and Completed.</span></span> <span data-ttu-id="a6e17-482">下列服務定義的變數適合用於根據工作度量進行集區大小調整：</span><span class="sxs-lookup"><span data-stu-id="a6e17-482">The following service-defined variables are useful for making pool-size adjustments based on task metrics:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="a6e17-483">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-483">$ActiveTasks</span></span></li>
      <li><span data-ttu-id="a6e17-484">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-484">$RunningTasks</span></span></li>
      <li><span data-ttu-id="a6e17-485">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-485">$PendingTasks</span></span></li>
      <li><span data-ttu-id="a6e17-486">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-486">$SucceededTasks</span></span></li>
            <li><span data-ttu-id="a6e17-487">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="a6e17-487">$FailedTasks</span></span></li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a><span data-ttu-id="a6e17-488">撰寫自動調整公式</span><span class="sxs-lookup"><span data-stu-id="a6e17-488">Write an autoscale formula</span></span>
<span data-ttu-id="a6e17-489">您建置自動調整公式的方式是使用上述元件撰寫陳述式，再將這些陳述式結合成完整的公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-489">You build an autoscale formula by forming statements that use the above components, then combine those statements into a complete formula.</span></span> <span data-ttu-id="a6e17-490">在本節中，我們會建立可以執行一些真實世界調整決策的範例自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-490">In this section, we create an example autoscale formula that can perform some real-world scaling decisions.</span></span>

<span data-ttu-id="a6e17-491">首先，讓我們定義新自動調整公式的需求。</span><span class="sxs-lookup"><span data-stu-id="a6e17-491">First, let's define the requirements for our new autoscale formula.</span></span> <span data-ttu-id="a6e17-492">公式應該︰</span><span class="sxs-lookup"><span data-stu-id="a6e17-492">The formula should:</span></span>

1. <span data-ttu-id="a6e17-493">如果 CPU 使用率偏高，則增加集區中專用計算節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-493">Increase the target number of dedicated compute nodes in a pool if CPU usage is high.</span></span>
2. <span data-ttu-id="a6e17-494">如果 CPU 使用率偏低，則減少集區中專用計算節點的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-494">Decrease the target number of dedicated compute nodes in a pool when CPU usage is low.</span></span>
3. <span data-ttu-id="a6e17-495">一律以 400 為專用節點的數目上限。</span><span class="sxs-lookup"><span data-stu-id="a6e17-495">Always restrict the maximum number of dedicated nodes to 400.</span></span>

<span data-ttu-id="a6e17-496">為了在高 CPU 使用率期間增加節點數目，將陳述式定義為在使用者定義的變數 (`$totalDedicatedNodes`) 中填入 110% 的專用節點目前目標數目值，但僅限在過去 10 分鐘期間平均 CPU 使用率下限大於 70%。</span><span class="sxs-lookup"><span data-stu-id="a6e17-496">To increase the number of nodes during high CPU usage, define the statement that populates a user-defined variable (`$totalDedicatedNodes`) with a value that is 110 percent of the current target number of dedicated nodes, but only if the minimum average CPU usage during the last 10 minutes was above 70 percent.</span></span> <span data-ttu-id="a6e17-497">否則，請使用專用節點目前數目值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-497">Otherwise, use the value for the current number of dedicated nodes.</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

<span data-ttu-id="a6e17-498">為了減少低 CPU 使用率期間的專用節點數目，如果在過去 60 分鐘內平均 CPU 使用率低於 20%，公式中的下一個陳述式會將相同的 `$totalDedicatedNodes` 變數設定為 90% 的專用節點目前目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-498">To *decrease* the number of dedicated nodes during low CPU usage, the next statement in our formula sets the same `$totalDedicatedNodes` variable to 90 percent of the current target number of dedicated nodes if the average CPU usage in the past 60 minutes was under 20 percent.</span></span> <span data-ttu-id="a6e17-499">否則，使用我們在上述陳述式中填入的目前 `$totalDedicatedNodes` 值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-499">Otherwise, use the current value of `$totalDedicatedNodes` that we populated in the statement above.</span></span>

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

<span data-ttu-id="a6e17-500">現在將專用計算節點的目標數目設定為上限 400 個：</span><span class="sxs-lookup"><span data-stu-id="a6e17-500">Now limit the target number of dedicated compute nodes to a maximum of 400:</span></span>

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

<span data-ttu-id="a6e17-501">以下是完整的公式：</span><span class="sxs-lookup"><span data-stu-id="a6e17-501">Here's the complete formula:</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a><span data-ttu-id="a6e17-502">使用 .NET 建立已啟用自動調整的集區</span><span class="sxs-lookup"><span data-stu-id="a6e17-502">Create an autoscale-enabled pool with .NET</span></span>

<span data-ttu-id="a6e17-503">若要在 .NET 中建立已啟用自動調整的集區，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6e17-503">To create a pool with autoscaling enabled in .NET, follow these steps:</span></span>

1. <span data-ttu-id="a6e17-504">使用 [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool) 建立集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-504">Create the pool with [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).</span></span>
2. <span data-ttu-id="a6e17-505">將 [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="a6e17-505">Set the [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) property to `true`.</span></span>
3. <span data-ttu-id="a6e17-506">使用自動調整公式來設定 [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) 屬性。</span><span class="sxs-lookup"><span data-stu-id="a6e17-506">Set the [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) property with your autoscale formula.</span></span>
4. <span data-ttu-id="a6e17-507">(選擇性) 設定 [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) 屬性 (預設值為 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="a6e17-507">(Optional) Set the [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) property (default is 15 minutes).</span></span>
5. <span data-ttu-id="a6e17-508">使用 [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) 或 [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync) 認可集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-508">Commit the pool with [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) or [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).</span></span>

<span data-ttu-id="a6e17-509">下列程式碼片段在 .NET 中建立已啟用自動調整的集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-509">The following code snippet creates an autoscale-enabled pool in .NET.</span></span> <span data-ttu-id="a6e17-510">集區的自動調整公式會將星期一的專用節點目標數目設定為 5，而將一週其他各天的節點目標數目設定為 1。</span><span class="sxs-lookup"><span data-stu-id="a6e17-510">The pool's autoscale formula sets the target number of dedicated nodes to 5 on Mondays, and 1 on every other day of the week.</span></span> <span data-ttu-id="a6e17-511">[自動調整間隔](#automatic-scaling-interval) 設定為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a6e17-511">The [automatic scaling interval](#automatic-scaling-interval) is set to 30 minutes.</span></span> <span data-ttu-id="a6e17-512">在本文中的此部分與其他 C# 程式碼片段中，`myBatchClient` 是適當初始化的 [BatchClient][net_batchclient] 類別執行個體。</span><span class="sxs-lookup"><span data-stu-id="a6e17-512">In this and the other C# snippets in this article, `myBatchClient` is a properly initialized instance of the [BatchClient][net_batchclient] class.</span></span>

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="a6e17-513">當您建立已啟用自動調整的集區時，請勿在對 **CreatePool** 的呼叫上指定 _targetDedicatedComputeNodes_ 參數或 _targetLowPriorityComputeNodes_ 參數。</span><span class="sxs-lookup"><span data-stu-id="a6e17-513">When you create an autoscale-enabled pool, do not specify the _targetDedicatedComputeNodes_ parameter or the _targetLowPriorityComputeNodes_ parameter on the call to **CreatePool**.</span></span> <span data-ttu-id="a6e17-514">請改為在集區上指定 **AutoScaleEnabled** 和 **AutoScaleFormula** 屬性。</span><span class="sxs-lookup"><span data-stu-id="a6e17-514">Instead, specify the **AutoScaleEnabled** and **AutoScaleFormula** properties on the pool.</span></span> <span data-ttu-id="a6e17-515">這些屬性的值會判斷每個節點類型的目標數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-515">The values for these properties determine the target number of each type of node.</span></span> <span data-ttu-id="a6e17-516">此外，若要對已啟用自動調整的集區手動調整大小 (例如使用 [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync])，請先在集區**停用**自動調整，然後調整其大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-516">Also, to manually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), first **disable** automatic scaling on the pool, then resize it.</span></span>
>
>

<span data-ttu-id="a6e17-517">除了 Batch .NET，您可以使用任何其他 [Batch SDK](batch-apis-tools.md#azure-accounts-for-batch-development)、[Batch REST](https://docs.microsoft.com/rest/api/batchservice/)、[Batch PowerShell Cmdlet](batch-powershell-cmdlets-get-started.md) 和 [Batch CLI](batch-cli-get-started.md) 來設定自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-517">In addition to Batch .NET, you can use any of the other [Batch SDKs](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and the [Batch CLI](batch-cli-get-started.md) to configure autoscaling.</span></span>


### <a name="automatic-scaling-interval"></a><span data-ttu-id="a6e17-518">自動調整間隔</span><span class="sxs-lookup"><span data-stu-id="a6e17-518">Automatic scaling interval</span></span>
<span data-ttu-id="a6e17-519">依預設，Batch 服務會根據其自動調整公式每隔 15 分鐘調整集區的大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-519">By default, the Batch service adjusts a pool's size according to its autoscale formula every 15 minutes.</span></span> <span data-ttu-id="a6e17-520">可使用下列的集區屬性設定此間隔：</span><span class="sxs-lookup"><span data-stu-id="a6e17-520">This interval is configurable by using the following pool properties:</span></span>

* <span data-ttu-id="a6e17-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="a6e17-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span></span>
* <span data-ttu-id="a6e17-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span><span class="sxs-lookup"><span data-stu-id="a6e17-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span></span>

<span data-ttu-id="a6e17-523">最小間隔為 5 分鐘，而最大間隔為 168 小時。</span><span class="sxs-lookup"><span data-stu-id="a6e17-523">The minimum interval is five minutes, and the maximum is 168 hours.</span></span> <span data-ttu-id="a6e17-524">如果指定此範圍以外的時間間隔，則 Batch 服務會傳回「不正確的要求 (400)」錯誤。</span><span class="sxs-lookup"><span data-stu-id="a6e17-524">If an interval outside this range is specified, the Batch service returns a Bad Request (400) error.</span></span>

> [!NOTE]
> <span data-ttu-id="a6e17-525">自動調整目前不適合作為低於一分鐘的變更回應，而是要在您執行工作負載時逐步調整您的集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-525">Autoscaling is not currently intended to respond to changes in less than a minute, but rather is intended to adjust the size of your pool gradually as you run a workload.</span></span>
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a><span data-ttu-id="a6e17-526">在現有集區啟用自動調整</span><span class="sxs-lookup"><span data-stu-id="a6e17-526">Enable autoscaling on an existing pool</span></span>

<span data-ttu-id="a6e17-527">每個 Batch SDK 會提供啟用自動調整的方法。</span><span class="sxs-lookup"><span data-stu-id="a6e17-527">Each Batch SDK provides a way to enable autoscaling.</span></span> <span data-ttu-id="a6e17-528">例如：</span><span class="sxs-lookup"><span data-stu-id="a6e17-528">For example:</span></span>

* <span data-ttu-id="a6e17-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="a6e17-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span></span>
* <span data-ttu-id="a6e17-530">[在自動調整中啟用集區][rest_enableautoscale] (REST API)</span><span class="sxs-lookup"><span data-stu-id="a6e17-530">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span></span>

<span data-ttu-id="a6e17-531">當您在現有集區啟用自動調整時，請記住下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a6e17-531">When you enable autoscaling on an existing pool, keep in mind the following points:</span></span>

* <span data-ttu-id="a6e17-532">如果在您發出啟用自動調整要求時，集區的自動調整目前已停用，您必須在發出要求時指定有效的自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-532">If automatic scaling is currently disabled on the pool when you issue the request to enable autoscaling, you must specify a valid autoscale formula when you issue the request.</span></span> <span data-ttu-id="a6e17-533">您可以選擇性地指定自動調整評估間隔。</span><span class="sxs-lookup"><span data-stu-id="a6e17-533">You can optionally specify an autoscale evaluation interval.</span></span> <span data-ttu-id="a6e17-534">如果您未指定間隔，則會使用預設值 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a6e17-534">If you do not specify an interval, the default value of 15 minutes is used.</span></span>
* <span data-ttu-id="a6e17-535">如果集區的自動調整目前已啟用，您可以指定自動調整公式、評估間隔，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="a6e17-535">If autoscale is currently enabled on the pool, you can specify an autoscale formula, an evaluation interval, or both.</span></span> <span data-ttu-id="a6e17-536">您必須至少指定其中一個屬性。</span><span class="sxs-lookup"><span data-stu-id="a6e17-536">You must specify at least one of these properties.</span></span>

  * <span data-ttu-id="a6e17-537">如果您指定新的自動調整評估間隔，則會停止現有的評估排程並啟動新的排程。</span><span class="sxs-lookup"><span data-stu-id="a6e17-537">If you specify a new autoscale evaluation interval, then the existing evaluation schedule is stopped and a new schedule is started.</span></span> <span data-ttu-id="a6e17-538">新排程的開始時間是發出啟用自動調整要求的時間。</span><span class="sxs-lookup"><span data-stu-id="a6e17-538">The new schedule's start time is the time at which the request to enable autoscaling was issued.</span></span>
  * <span data-ttu-id="a6e17-539">如果您省略自動調整公式或評估間隔，則 Batch 服務會繼續使用該設定目前的值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-539">If you omit either the autoscale formula or evaluation interval, the Batch service continues to use the current value of that setting.</span></span>

> [!NOTE]
> <span data-ttu-id="a6e17-540">如果當您在 .NET 中建立集區時，指定 **CreatePool** 方法之 *targetDedicatedComputeNodes* 或 *targetLowPriorityComputeNodes* 參數的值，或在其他語言中指定相當的參數，則在評估自動調整公式時會略過這些值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-540">If you specified values for the *targetDedicatedComputeNodes* or *targetLowPriorityComputeNodes* parameters of the **CreatePool** method when you created the pool in .NET, or for the comparable parameters in another language, then those values are ignored when the automatic scaling formula is evaluated.</span></span>
>
>

<span data-ttu-id="a6e17-541">此 C# 程式碼片段使用 [Batch .NET][net_api] 程式庫，在現有的集區上啟用自動調整：</span><span class="sxs-lookup"><span data-stu-id="a6e17-541">This C# code snippet uses the [Batch .NET][net_api] library to enable autoscaling on an existing pool:</span></span>

```csharp
// Define the autoscaling formula. This formula sets the target number of nodes
// to 5 on Mondays, and 1 on every other day of the week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set the autoscale formula on the existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a><span data-ttu-id="a6e17-542">更新自動調整公式</span><span class="sxs-lookup"><span data-stu-id="a6e17-542">Update an autoscale formula</span></span>

<span data-ttu-id="a6e17-543">若要更新現有已啟用自動調整集區上的公式，呼叫作業以使用新的公式再次啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-543">To update the formula on an existing autoscale-enabled pool, call the operation to enable autoscaling again with the new formula.</span></span> <span data-ttu-id="a6e17-544">例如，如果在執行下列 .NET 程式碼時，已在 `myexistingpool` 上啟用自動調整，則會以 `myNewFormula` 的內容取代其自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-544">For example, if autoscaling is already enabled on `myexistingpool` when the following .NET code is executed, its autoscale formula is replaced with the contents of `myNewFormula`.</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-the-autoscale-interval"></a><span data-ttu-id="a6e17-545">更新自動調整間隔</span><span class="sxs-lookup"><span data-stu-id="a6e17-545">Update the autoscale interval</span></span>

<span data-ttu-id="a6e17-546">若要更新現有已啟用自動調整集區的自動調整評估間隔，呼叫作業以使用新的間隔再次啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-546">To update the autoscale evaluation interval of an existing autoscale-enabled pool, call the operation to enable autoscaling again with the new interval.</span></span> <span data-ttu-id="a6e17-547">例如，若要針對在 .NET 中已啟用自動調整的集區，將自動調整評估間隔設定為 60 分鐘︰</span><span class="sxs-lookup"><span data-stu-id="a6e17-547">For example, to set the autoscale evaluation interval to 60 minutes for a pool that's already autoscale-enabled in .NET:</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a><span data-ttu-id="a6e17-548">評估自動調整公式</span><span class="sxs-lookup"><span data-stu-id="a6e17-548">Evaluate an autoscale formula</span></span>

<span data-ttu-id="a6e17-549">您可以先評估公式，再將它套用至集區。</span><span class="sxs-lookup"><span data-stu-id="a6e17-549">You can evaluate a formula before applying it to a pool.</span></span> <span data-ttu-id="a6e17-550">如此一來，您可以測試公式，以在將公式放入生產環境前，查看其陳述式的評估情況。</span><span class="sxs-lookup"><span data-stu-id="a6e17-550">In this way, you can test the formula to see how its statements evaluate before you put the formula into production.</span></span>

<span data-ttu-id="a6e17-551">若要評估自動調整公式，您必須先使用有效的公式在集區啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="a6e17-551">To evaluate an autoscale formula, you must first enable autoscaling on the pool with a valid formula.</span></span> <span data-ttu-id="a6e17-552">若要在尚未啟用自動調整的集區上測試公式，在第一次啟用自動調整時使用一行公式 `$TargetDedicatedNodes = 0`。</span><span class="sxs-lookup"><span data-stu-id="a6e17-552">To test a formula on a pool that doesn't yet have autoscaling enabled, use the one-line formula `$TargetDedicatedNodes = 0` when you first enable autoscaling.</span></span> <span data-ttu-id="a6e17-553">然後，使用下列其中之一來評估您想要測試的公式︰</span><span class="sxs-lookup"><span data-stu-id="a6e17-553">Then, use one of the following to evaluate the formula you want to test:</span></span>

* <span data-ttu-id="a6e17-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 或 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span><span class="sxs-lookup"><span data-stu-id="a6e17-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) or [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span></span>

    <span data-ttu-id="a6e17-555">這些 Batch .NET 方法都需要現有集區的識別碼以及包含要評估之自動調整公式的字串。</span><span class="sxs-lookup"><span data-stu-id="a6e17-555">These Batch .NET methods require the ID of an existing pool and a string containing the autoscale formula to evaluate.</span></span>

* [<span data-ttu-id="a6e17-556">評估自動調整公式</span><span class="sxs-lookup"><span data-stu-id="a6e17-556">Evaluate an automatic scaling formula</span></span>](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    <span data-ttu-id="a6e17-557">在這個 REST 要求中，於 URI 中指定集區識別碼，以及於要求主體的 *autoScaleFormula* 元素中指定自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-557">In this REST API request, specify the pool ID in the URI, and the autoscale formula in the *autoScaleFormula* element of the request body.</span></span> <span data-ttu-id="a6e17-558">作業的回應會包含可能與公式相關的任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e17-558">The response of the operation contains any error information that might be related to the formula.</span></span>

<span data-ttu-id="a6e17-559">在這個 [Batch .NET][net_api] 程式碼片段中，我們會評估自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-559">In this [Batch .NET][net_api] code snippet, we evaluate an autoscale formula.</span></span> <span data-ttu-id="a6e17-560">如果集區並未啟用自動調整，我們會先加以啟用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-560">If the pool does not have autoscaling enabled, we enable it first.</span></span>

```csharp
// First obtain a reference to an existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on the pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula to enable autoscaling on the
    // pool. This formula is valid, but won't resize the pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls to once every 30 seconds.
    // Because we want to apply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here to ensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh the properties of the pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on the pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // The formula to evaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform the autoscale formula evaluation. Note that this code does not
    // actually apply the formula to the pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print the results of the AutoScaleRun.
        // This will display the values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply the formula to the pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output the message associated with the error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

<span data-ttu-id="a6e17-561">成功評估此程式碼片段所顯示的公式會產生類似以下的結果：</span><span class="sxs-lookup"><span data-stu-id="a6e17-561">Successful evaluation of the formula shown in this code snippet produces results similar to:</span></span>

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a><span data-ttu-id="a6e17-562">取得自動調整執行的相關資訊</span><span class="sxs-lookup"><span data-stu-id="a6e17-562">Get information about autoscale runs</span></span>

<span data-ttu-id="a6e17-563">若要確保您的公式如預期般執行，我們建議您定期檢查 Batch 對您的集區執行之自動調整執行的結果。</span><span class="sxs-lookup"><span data-stu-id="a6e17-563">To ensure that your formula is performing as expected, we recommend that you periodically check the results of the autoscaling runs that Batch performs on your pool.</span></span> <span data-ttu-id="a6e17-564">若要這麼做，請取得 (或重新整理) 集區的參考，並檢查其上次自動調整執行的內容。</span><span class="sxs-lookup"><span data-stu-id="a6e17-564">To do so, get (or refresh) a reference to the pool, and examine the properties of its last autoscale run.</span></span>

<span data-ttu-id="a6e17-565">在 Batch .NET 中，[CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) 屬性有數個屬性，可提供最近在集區上執行之自動調整的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="a6e17-565">In Batch .NET, the [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) property has several properties that provide information about the latest automatic scaling run performed on the pool:</span></span>

* [<span data-ttu-id="a6e17-566">AutoScaleRun.Timestamp</span><span class="sxs-lookup"><span data-stu-id="a6e17-566">AutoScaleRun.Timestamp</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [<span data-ttu-id="a6e17-567">AutoScaleRun.Results</span><span class="sxs-lookup"><span data-stu-id="a6e17-567">AutoScaleRun.Results</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [<span data-ttu-id="a6e17-568">AutoScaleRun.Error</span><span class="sxs-lookup"><span data-stu-id="a6e17-568">AutoScaleRun.Error</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

<span data-ttu-id="a6e17-569">在 REST API 中，[取得集區的相關資訊](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool)要求會傳回集區的相關資訊，其中包含 [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) 屬性中最近執行的自動調整資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e17-569">In the REST API, the [Get information about a pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) request returns information about the pool, which includes the latest automatic scaling run information in the [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) property.</span></span>

<span data-ttu-id="a6e17-570">下列 C# 程式碼片段會使用 Batch .NET 程式庫來列印集區 _myPool_ 上次自動調整執行的相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="a6e17-570">The following C# code snippet uses the Batch .NET library to print information about the last autoscaling run on pool _myPool_:</span></span>

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

<span data-ttu-id="a6e17-571">上述程式碼片段的範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="a6e17-571">Sample output of the preceding snippet:</span></span>

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a><span data-ttu-id="a6e17-572">自動調整公式範例</span><span class="sxs-lookup"><span data-stu-id="a6e17-572">Example autoscale formulas</span></span>
<span data-ttu-id="a6e17-573">讓我們看看下面幾個公式，其顯示調整集區中計算資源數量的不同方式。</span><span class="sxs-lookup"><span data-stu-id="a6e17-573">Let's look at a few formulas that show different ways to adjust the amount of compute resources in a pool.</span></span>

### <a name="example-1-time-based-adjustment"></a><span data-ttu-id="a6e17-574">範例 1：以時間為基礎的調整</span><span class="sxs-lookup"><span data-stu-id="a6e17-574">Example 1: Time-based adjustment</span></span>
<span data-ttu-id="a6e17-575">假設您想要根據一週的天數和一天的時間，調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-575">Suppose you want to adjust the pool size based on the day of the week and time of day.</span></span> <span data-ttu-id="a6e17-576">這個範例示範如何據以增加或減少集區中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-576">This example shows how to increase or decrease the number of nodes in the pool accordingly.</span></span>

<span data-ttu-id="a6e17-577">此公式會先取得目前的時間。</span><span class="sxs-lookup"><span data-stu-id="a6e17-577">The formula first obtains the current time.</span></span> <span data-ttu-id="a6e17-578">如果是工作日 (1-5) 且在上班時間內 (上午 8:00 - 下午 6:00)，則將目標集區大小設為 20 個節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-578">If it's a weekday (1-5) and within working hours (8 AM to 6 PM), the target pool size is set to 20 nodes.</span></span> <span data-ttu-id="a6e17-579">否則，它會設定為 10 個節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-579">Otherwise, it's set to 10 nodes.</span></span>

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a><span data-ttu-id="a6e17-580">範例 2：以工作為基礎的調整</span><span class="sxs-lookup"><span data-stu-id="a6e17-580">Example 2: Task-based adjustment</span></span>
<span data-ttu-id="a6e17-581">在此範例中，是根據佇列中的工作數目調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-581">In this example, the pool size is adjusted based on the number of tasks in the queue.</span></span> <span data-ttu-id="a6e17-582">公式字串中接受註解和換行。</span><span class="sxs-lookup"><span data-stu-id="a6e17-582">Both comments and line breaks are acceptable in formula strings.</span></span>

```csharp
// Get pending tasks for the past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use the last sample point,
// otherwise we use the maximum of last sample point and the history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM to pending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// The pool size is capped at 20, if target VM value is more than that, set it
// to 20. This value should be adjusted according to your use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a><span data-ttu-id="a6e17-583">範例 3：考量平行工作</span><span class="sxs-lookup"><span data-stu-id="a6e17-583">Example 3: Accounting for parallel tasks</span></span>
<span data-ttu-id="a6e17-584">此範例會根據工作數目調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-584">This example adjusts the pool size based on the number of tasks.</span></span> <span data-ttu-id="a6e17-585">此公式也會考慮集區已設定的 [MaxTasksPerComputeNode][net_maxtasks] 值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-585">This formula also takes into account the [MaxTasksPerComputeNode][net_maxtasks] value that has been set for the pool.</span></span> <span data-ttu-id="a6e17-586">已在集區上啟用[平行工作執行](batch-parallel-node-tasks.md)的情況下，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="a6e17-586">This approach is useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span></span>

```csharp
// Determine whether 70 percent of the samples have been recorded in the past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set the number of nodes to add to one-fourth the number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set to 4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt to grow the number of compute nodes to match the number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep the nodes active until the tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a><span data-ttu-id="a6e17-587">範例 4：設定初始集區大小</span><span class="sxs-lookup"><span data-stu-id="a6e17-587">Example 4: Setting an initial pool size</span></span>
<span data-ttu-id="a6e17-588">此範例顯示的 C# 程式碼片段具有自動調整公式，其在初始期間將集區大小設為指定的節點數目。</span><span class="sxs-lookup"><span data-stu-id="a6e17-588">This example shows a C# code snippet with an autoscale formula that sets the pool size to a specified number of nodes for an initial time period.</span></span> <span data-ttu-id="a6e17-589">然後在初始期間經過之後，再根據執行中和作用中的工作數目來調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-589">Then it adjusts the pool size based on the number of running and active tasks after the initial time period has elapsed.</span></span>

<span data-ttu-id="a6e17-590">下列程式碼片段中的公式：</span><span class="sxs-lookup"><span data-stu-id="a6e17-590">The formula in the following code snippet:</span></span>

* <span data-ttu-id="a6e17-591">將初始的集區大小設為 4 個節點。</span><span class="sxs-lookup"><span data-stu-id="a6e17-591">Sets the initial pool size to four nodes.</span></span>
* <span data-ttu-id="a6e17-592">在集區生命週期的最初 10 分鐘內不調整集區大小。</span><span class="sxs-lookup"><span data-stu-id="a6e17-592">Does not adjust the pool size within the first 10 minutes of the pool's lifecycle.</span></span>
* <span data-ttu-id="a6e17-593">10 分鐘後，取得過去 60 分鐘內執行中和作用中工作數目的最大值。</span><span class="sxs-lookup"><span data-stu-id="a6e17-593">After 10 minutes, obtains the max value of the number of running and active tasks within the past 60 minutes.</span></span>
  * <span data-ttu-id="a6e17-594">如果這兩個值都是 0 (表示過去 60 分鐘沒有執行或作用中的工作)，集區大小就設為 0。</span><span class="sxs-lookup"><span data-stu-id="a6e17-594">If both values are 0 (indicating that no tasks were running or active in the last 60 minutes), the pool size is set to 0.</span></span>
  * <span data-ttu-id="a6e17-595">如果其中一個值大於零，則不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="a6e17-595">If either value is greater than zero, no change is made.</span></span>

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a><span data-ttu-id="a6e17-596">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6e17-596">Next steps</span></span>
* <span data-ttu-id="a6e17-597">[使用並行節點工作最大化 Azure Batch 計算資源使用量](batch-parallel-node-tasks.md) 包含有關如何對集區中的計算節點同時執行多項工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6e17-597">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on the compute nodes in your pool.</span></span> <span data-ttu-id="a6e17-598">除了自動調整，這項功能有助於減少某些工作負載的作業持續時間，進而節省金錢。</span><span class="sxs-lookup"><span data-stu-id="a6e17-598">In addition to autoscaling, this feature may help to lower job duration for some workloads, saving you money.</span></span>
* <span data-ttu-id="a6e17-599">另一種效率提升方式，則是確定您的 Batch 應用程式以最佳方式查詢 Batch 服務。</span><span class="sxs-lookup"><span data-stu-id="a6e17-599">For another efficiency booster, ensure that your Batch application queries the Batch service in the most optimal way.</span></span> <span data-ttu-id="a6e17-600">請參閱[有效率地查詢 Azure Batch 服務](batch-efficient-list-queries.md)，以了解如何在查詢可能數千個計算節點或工作的狀態時，限制越過網路的資料量。</span><span class="sxs-lookup"><span data-stu-id="a6e17-600">See [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to learn how to limit the amount of data that crosses the wire when you query the status of potentially thousands of compute nodes or tasks.</span></span>

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
