---
title: "aaaAutomatically 小數位數中的計算節點的 Azure Batch 集區 |Microsoft 文件"
description: "啟用自動調整上雲端的集區 toodynamically 調整 hello hello 集區中的運算節點數目。"
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
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a><span data-ttu-id="133b4-103">建立自動調整公式來調整 Batch 集區中的計算節點</span><span class="sxs-lookup"><span data-stu-id="133b4-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span></span>

<span data-ttu-id="133b4-104">Azure Batch 可以根據您定義的參數自動調整集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-104">Azure Batch can automatically scale pools based on parameters that you define.</span></span> <span data-ttu-id="133b4-105">自動縮放，批次以動態方式新增節點 tooa 集區做為工作需求增加，並移除計算節點，它們會降低。</span><span class="sxs-lookup"><span data-stu-id="133b4-105">With automatic scaling, Batch dynamically adds nodes tooa pool as task demands increase, and removes compute nodes as they decrease.</span></span> <span data-ttu-id="133b4-106">您可以節省時間和金錢自動調整 hello 批次應用程式所使用的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-106">You can save both time and money by automatically adjusting hello number of compute nodes used by your Batch application.</span></span> 

<span data-ttu-id="133b4-107">您可讓您定義的「自動調整公式」與計算節點的集區產生關聯，以在該集區上啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span></span> <span data-ttu-id="133b4-108">hello 批次服務會使用您的工作負載的運算節點所需的 tooexecute hello 自動調整公式 toodetermine hello 數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-108">hello Batch service uses hello autoscale formula toodetermine hello number of compute nodes that are needed tooexecute your workload.</span></span> <span data-ttu-id="133b4-109">計算節點可以是專用節點或[低優先順序節點](batch-low-pri-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="133b4-109">Compute nodes may be dedicated nodes or [low-priority nodes](batch-low-pri-vms.md).</span></span> <span data-ttu-id="133b4-110">批次回應 tooservice 定期收集的度量資料。</span><span class="sxs-lookup"><span data-stu-id="133b4-110">Batch responds tooservice metrics data that is collected periodically.</span></span> <span data-ttu-id="133b4-111">使用此度量資料時，批次會調整運算節點，根據您的公式，並可設定的間隔 hello 集區中的 hello 的數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-111">Using this metrics data, Batch adjusts hello number of compute nodes in hello pool based on your formula and at a configurable interval.</span></span>

<span data-ttu-id="133b4-112">您可以在建立集區時或在現有的集區上啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-112">You can enable automatic scaling either when a pool is created, or on an existing pool.</span></span> <span data-ttu-id="133b4-113">您也可以變更已針對自動調整設定之集區上的現有公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-113">You can also change an existing formula on a pool that is configured for autoscaling.</span></span> <span data-ttu-id="133b4-114">批次，可讓您執行之前將其指派 toopools 和 toomonitor hello 狀態自動調整公式的 tooevaluate。</span><span class="sxs-lookup"><span data-stu-id="133b4-114">Batch enables you tooevaluate your formulas before assigning them toopools and toomonitor hello status of automatic scaling runs.</span></span>

<span data-ttu-id="133b4-115">這篇文章討論 hello 構成您的自動調整公式，包括變數、 運算子、 作業和函式的各種實體。</span><span class="sxs-lookup"><span data-stu-id="133b4-115">This article discusses hello various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span></span> <span data-ttu-id="133b4-116">我們將討論如何 tooobtain 各種計算資源和工作批次內的度量。</span><span class="sxs-lookup"><span data-stu-id="133b4-116">We discuss how tooobtain various compute resource and task metrics within Batch.</span></span> <span data-ttu-id="133b4-117">您可以使用這些度量 tooadjust，集區的節點計數根據資源使用量和工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="133b4-117">You can use these metrics tooadjust your pool's node count based on resource usage and task status.</span></span> <span data-ttu-id="133b4-118">我們接著說明如何 tooconstruct 公式，並啟用自動調整集區上同時使用 hello 批次 REST 和.NET 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="133b4-118">We then describe how tooconstruct a formula and enable automatic scaling on a pool by using both hello Batch REST and .NET APIs.</span></span> <span data-ttu-id="133b4-119">最後，我們會完成幾個範例公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-119">Finally, we finish up with a few example formulas.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="133b4-120">當您建立的批次帳戶時，您可以指定 hello[帳戶組態](batch-api-basics.md#account)，以決定是否將集區，配置在批次服務訂用帳戶 （hello 預設值），或您使用者訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="133b4-120">When you create a Batch account, you can specify hello [account configuration](batch-api-basics.md#account), which determines whether pools are allocated in a Batch service subscription (hello default), or in your user subscription.</span></span> <span data-ttu-id="133b4-121">如果您建立您的 Batch 帳戶與 hello 預設批次服務組態，您的帳戶是有限的 tooa 可以用於處理的核心數目上限。</span><span class="sxs-lookup"><span data-stu-id="133b4-121">If you created your Batch account with hello default Batch Service configuration, then your account is limited tooa maximum number of cores that can be used for processing.</span></span> <span data-ttu-id="133b4-122">hello 批次服務縮放只向上 toothat 核心限制的計算節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-122">hello Batch service scales compute nodes only up toothat core limit.</span></span> <span data-ttu-id="133b4-123">基於這個理由，hello 批次服務可能無法到達自動調整公式所指定的運算節點的 hello 目標的數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-123">For this reason, hello Batch service may not reach hello target number of compute nodes specified by an autoscale formula.</span></span> <span data-ttu-id="133b4-124">請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)的檢視，並增加您的帳戶配額的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="133b4-124">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span></span>
>
><span data-ttu-id="133b4-125">如果您建立您的帳戶與 hello 使用者訂用帳戶設定，然後您的帳戶中的共用 hello hello 訂用帳戶的核心配額。</span><span class="sxs-lookup"><span data-stu-id="133b4-125">If you created your account with hello User Subscription configuration, then your account shares in hello core quota for hello subscription.</span></span> <span data-ttu-id="133b4-126">如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)中的 [虛擬機器限制](../azure-subscription-service-limits.md#virtual-machines-limits)。</span><span class="sxs-lookup"><span data-stu-id="133b4-126">For more information, see [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
>
>

## <a name="automatic-scaling-formulas"></a><span data-ttu-id="133b4-127">自動調整公式</span><span class="sxs-lookup"><span data-stu-id="133b4-127">Automatic scaling formulas</span></span>
<span data-ttu-id="133b4-128">自動調整公式是您定義的字串值，其中包含一或多個陳述式。</span><span class="sxs-lookup"><span data-stu-id="133b4-128">An automatic scaling formula is a string value that you define that contains one or more statements.</span></span> <span data-ttu-id="133b4-129">hello 自動調整公式會指派集區 tooa [autoScaleFormula] [ rest_autoscaleformula]元素 (批次 REST) 或[CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula]屬性 (批次.NET)。</span><span class="sxs-lookup"><span data-stu-id="133b4-129">hello autoscale formula is assigned tooa pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span></span> <span data-ttu-id="133b4-130">hello 批次服務會使用您公式 toodetermine hello 目標數目計算節點 hello 集區中的 hello 下一個處理間隔。</span><span class="sxs-lookup"><span data-stu-id="133b4-130">hello Batch service uses your formula toodetermine hello target number of compute nodes in hello pool for hello next interval of processing.</span></span> <span data-ttu-id="133b4-131">hello 公式字串不能超過 8 KB 的可以包括安裝 too100 陳述式，以分號分隔，而且可包含分行符號及註解。</span><span class="sxs-lookup"><span data-stu-id="133b4-131">hello formula string cannot exceed 8 KB, can include up too100 statements that are separated by semicolons, and can include line breaks and comments.</span></span>

<span data-ttu-id="133b4-132">您可以將自動調整公式視為 Batch 自動調整「語言」。</span><span class="sxs-lookup"><span data-stu-id="133b4-132">You can think of automatic scaling formulas as a Batch autoscale "language."</span></span> <span data-ttu-id="133b4-133">公式的陳述式是自由格式的運算式，可以包括服務定義的變數 （hello 批次服務所定義的變數） 及使用者定義的變數 （您所定義的變數）。</span><span class="sxs-lookup"><span data-stu-id="133b4-133">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by hello Batch service) and user-defined variables (variables that you define).</span></span> <span data-ttu-id="133b4-134">它們可以使用內建類型、運算子和函式對這些值執行各種作業。</span><span class="sxs-lookup"><span data-stu-id="133b4-134">They can perform various operations on these values by using built-in types, operators, and functions.</span></span> <span data-ttu-id="133b4-135">例如，陳述式可能會接受下列表單的 hello:</span><span class="sxs-lookup"><span data-stu-id="133b4-135">For example, a statement might take hello following form:</span></span>

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

<span data-ttu-id="133b4-136">公式通常包含多個陳述式，其可對在先前陳述式中取得的值執行作業。</span><span class="sxs-lookup"><span data-stu-id="133b4-136">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span></span> <span data-ttu-id="133b4-137">例如，在我們取得的值第一次`variable1`，然後將它傳遞 tooa 函式 toopopulate `variable2`:</span><span class="sxs-lookup"><span data-stu-id="133b4-137">For example, first we obtain a value for `variable1`, then pass it tooa function toopopulate `variable2`:</span></span>

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

<span data-ttu-id="133b4-138">在您的自動調整公式 tooarrive 在計算節點的目標中包含這些陳述式。</span><span class="sxs-lookup"><span data-stu-id="133b4-138">Include these statements in your autoscale formula tooarrive at a target number of compute nodes.</span></span> <span data-ttu-id="133b4-139">專用節點與低優先順序節點各有自己的目標設定，因此您可以為每個節點類型定義目標。</span><span class="sxs-lookup"><span data-stu-id="133b4-139">Dedicated nodes and low-priority nodes each have their own target settings, so that you can define a target for each type of node.</span></span> <span data-ttu-id="133b4-140">自動調整公式可以包含專用節點目標值、低優先順序節點目標值，或同時包含兩者。</span><span class="sxs-lookup"><span data-stu-id="133b4-140">An autoscale formula can include a target value for dedicated nodes, a target value for low-priority nodes, or both.</span></span>

<span data-ttu-id="133b4-141">節點的 hello 目標數目可能較高、 低，或 hello 與 hello 目前的 hello 集區中的該類型的節點數目相同。</span><span class="sxs-lookup"><span data-stu-id="133b4-141">hello target number of nodes may be higher, lower, or hello same as hello current number of nodes of that type in hello pool.</span></span> <span data-ttu-id="133b4-142">Batch 服務會在特定間隔評估集區的自動調整公式 (請參閱[自動調整間隔](#automatic-scaling-interval))。</span><span class="sxs-lookup"><span data-stu-id="133b4-142">Batch evaluates a pool's autoscale formula at a specific interval (see [automatic scaling intervals](#automatic-scaling-interval)).</span></span> <span data-ttu-id="133b4-143">批次調整每個 hello 評估 hello 時指定自動調整公式的集區 toohello 號碼中的節點類型的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-143">Batch adjusts hello target number of each type of node in hello pool toohello number that your autoscale formula specifies at hello time of evaluation.</span></span>

### <a name="sample-autoscale-formula"></a><span data-ttu-id="133b4-144">自動調整公式範例</span><span class="sxs-lookup"><span data-stu-id="133b4-144">Sample autoscale formula</span></span>

<span data-ttu-id="133b4-145">以下是可在大部分情況下的調整的 toowork 自動調整公式的範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-145">Here is an example of an autoscale formula that can be adjusted toowork for most scenarios.</span></span> <span data-ttu-id="133b4-146">hello 變數`startingNumberOfVMs`和`maxNumberofVMs`在 hello 範例公式可調整的 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="133b4-146">hello variables `startingNumberOfVMs` and `maxNumberofVMs` in hello example formula can be adjusted tooyour needs.</span></span> <span data-ttu-id="133b4-147">這個公式縮放專用的節點，但是可以修改的 tooapply tooscale 低優先權的節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-147">This formula scales dedicated nodes, but can be modified tooapply tooscale low-priority nodes as well.</span></span> 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

<span data-ttu-id="133b4-148">使用此自動調整公式的單一 VM 一開始建立 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-148">With this autoscale formula, hello pool is initially created with a single VM.</span></span> <span data-ttu-id="133b4-149">hello`$PendingTasks`度量定義 hello 執行或佇列工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-149">hello `$PendingTasks` metric defines hello number of tasks that are running or queued.</span></span> <span data-ttu-id="133b4-150">hello 公式 hello 的平均數目暫止工作在找到 hello 過去 180 秒，並設定 hello`$TargetDedicatedNodes`變數據此。</span><span class="sxs-lookup"><span data-stu-id="133b4-150">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets hello `$TargetDedicatedNodes` variable accordingly.</span></span> <span data-ttu-id="133b4-151">hello 公式可確保 hello 目標數目專用的節點永遠不會超過 25 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="133b4-151">hello formula ensures that hello target number of dedicated nodes never exceeds 25 VMs.</span></span> <span data-ttu-id="133b4-152">當提交新的工作，hello 集區自動成長。</span><span class="sxs-lookup"><span data-stu-id="133b4-152">As new tasks are submitted, hello pool automatically grows.</span></span> <span data-ttu-id="133b4-153">做為工作完成，Vm 會變成可用逐一和 hello 自動調整公式壓縮 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-153">As tasks complete, VMs become free one by one and hello autoscaling formula shrinks hello pool.</span></span>

## <a name="variables"></a><span data-ttu-id="133b4-154">變數</span><span class="sxs-lookup"><span data-stu-id="133b4-154">Variables</span></span>
<span data-ttu-id="133b4-155">您可以在自動調整公式中同時使用**服務定義**和**使用者定義**的變數。</span><span class="sxs-lookup"><span data-stu-id="133b4-155">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span></span> <span data-ttu-id="133b4-156">hello 服務定義的變數是內建的 toohello 批次服務。</span><span class="sxs-lookup"><span data-stu-id="133b4-156">hello service-defined variables are built in toohello Batch service.</span></span> <span data-ttu-id="133b4-157">有些服務定義的變數是讀寫，有些是唯讀。</span><span class="sxs-lookup"><span data-stu-id="133b4-157">Some service-defined variables are read-write, and some are read-only.</span></span> <span data-ttu-id="133b4-158">使用者定義的變數是您定義的變數。</span><span class="sxs-lookup"><span data-stu-id="133b4-158">User-defined variables are variables that you define.</span></span> <span data-ttu-id="133b4-159">在顯示 hello 前一節中的 hello 範例公式`$TargetDedicatedNodes`和`$PendingTasks`是服務定義的變數。</span><span class="sxs-lookup"><span data-stu-id="133b4-159">In hello example formula shown in hello previous section, `$TargetDedicatedNodes` and `$PendingTasks` are service-defined variables.</span></span> <span data-ttu-id="133b4-160">`startingNumberOfVMs` 和 `maxNumberofVMs` 變數是使用者定義的變數。</span><span class="sxs-lookup"><span data-stu-id="133b4-160">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span></span>

> [!NOTE]
> <span data-ttu-id="133b4-161">服務定義的變數前面一律會加上貨幣符號 ($)。</span><span class="sxs-lookup"><span data-stu-id="133b4-161">Service-defined variables are always preceded by a dollar sign ($).</span></span> <span data-ttu-id="133b4-162">針對使用者自訂變數，hello 貨幣符號是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="133b4-162">For user-defined variables, hello dollar sign is optional.</span></span>
>
>

<span data-ttu-id="133b4-163">下表中的 hello 顯示同時讀寫和唯讀變數所定義的 hello 批次服務。</span><span class="sxs-lookup"><span data-stu-id="133b4-163">hello following tables show both read-write and read-only variables that are defined by hello Batch service.</span></span>

<span data-ttu-id="133b4-164">您可以取得及設定 hello 這些變數的值定義服務集區中的運算節點 toomanage hello 數目：</span><span class="sxs-lookup"><span data-stu-id="133b4-164">You can get and set hello values of these service-defined variables toomanage hello number of compute nodes in a pool:</span></span>

| <span data-ttu-id="133b4-165">讀寫服務定義變數</span><span class="sxs-lookup"><span data-stu-id="133b4-165">Read-write service-defined variables</span></span> | <span data-ttu-id="133b4-166">說明</span><span class="sxs-lookup"><span data-stu-id="133b4-166">Description</span></span> |
| --- | --- |
| <span data-ttu-id="133b4-167">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-167">$TargetDedicatedNodes</span></span> |<span data-ttu-id="133b4-168">hello 目標數目專用計算 hello 集區的節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-168">hello target number of dedicated compute nodes for hello pool.</span></span> <span data-ttu-id="133b4-169">hello 專用的節點數目被指定做為目標，因為集區可能無法永遠達成 hello 預期的節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-169">hello number of dedicated nodes is specified as a target because a pool may not always achieve hello desired number of nodes.</span></span> <span data-ttu-id="133b4-170">比方說，如果 hello 目標專用的節點已修改的自動調整規模評估 hello 之前由集區已達到 hello 初始目標，然後 hello 集區可能無法到達 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="133b4-170">For example, if hello target number of dedicated nodes is modified by an autoscale evaluation before hello pool has reached hello initial target, then hello pool may not reach hello target.</span></span> <br /><br /> <span data-ttu-id="133b4-171">如果 hello 目標超過批次帳戶節點或核心配額，與 hello 批次服務組態建立的帳戶中的集區可能無法達成其目標。</span><span class="sxs-lookup"><span data-stu-id="133b4-171">A pool in an account created with hello Batch Service configuration may not achieve its target if hello target exceeds a Batch account node or core quota.</span></span> <span data-ttu-id="133b4-172">建立與 hello 使用者訂用帳戶設定的帳戶中的集區可能無法達成其目標，如果 hello 目標超過 hello hello 訂用帳戶的共用的核心配額。</span><span class="sxs-lookup"><span data-stu-id="133b4-172">A pool in an account created with hello User Subscription configuration may not achieve its target if hello target exceeds hello shared core quota for hello subscription.</span></span>|
| <span data-ttu-id="133b4-173">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-173">$TargetLowPriorityNodes</span></span> |<span data-ttu-id="133b4-174">低優先順序的 hello 目標數目計算 hello 集區的節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-174">hello target number of low-priority compute nodes for hello pool.</span></span> <span data-ttu-id="133b4-175">hello 低優先權的節點數目被指定做為目標，因為集區可能無法永遠達成 hello 預期的節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-175">hello number of low-priority nodes is specified as a target because a pool may not always achieve hello desired number of nodes.</span></span> <span data-ttu-id="133b4-176">比方說，如果修改 hello 目標數目低優先權的節點，便自動調整規模評估 hello 之前由集區已達到 hello 初始目標，然後 hello 集區可能無法到達 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="133b4-176">For example, if hello target number of low-priority nodes is modified by an autoscale evaluation before hello pool has reached hello initial target, then hello pool may not reach hello target.</span></span> <span data-ttu-id="133b4-177">如果 hello 目標超過批次帳戶節點或核心配額，則集區可能也無法達成其目標。</span><span class="sxs-lookup"><span data-stu-id="133b4-177">A pool may also not achieve its target if hello target exceeds a Batch account node or core quota.</span></span> <br /><br /> <span data-ttu-id="133b4-178">如需有關低優先順序計算節點的詳細資訊，請參閱[搭配 Batch 使用低優先順序 VM (預覽)](batch-low-pri-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="133b4-178">For more information on low-priority compute nodes, see [Use low-priority VMs with Batch (Preview)](batch-low-pri-vms.md).</span></span> |
| <span data-ttu-id="133b4-179">$NodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="133b4-179">$NodeDeallocationOption</span></span> |<span data-ttu-id="133b4-180">hello 從集區移除運算節點時，就會發生的動作。</span><span class="sxs-lookup"><span data-stu-id="133b4-180">hello action that occurs when compute nodes are removed from a pool.</span></span> <span data-ttu-id="133b4-181">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="133b4-181">Possible values are:</span></span><ul><li><span data-ttu-id="133b4-182">**排入佇列**-會立即終止工作並將它們放入 hello 工作佇列，以便重新排定它們。</span><span class="sxs-lookup"><span data-stu-id="133b4-182">**requeue**--Terminates tasks immediately and puts them back on hello job queue so that they are rescheduled.</span></span><li><span data-ttu-id="133b4-183">**終止**-會立即終止工作並將其從 hello 工作佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="133b4-183">**terminate**--Terminates tasks immediately and removes them from hello job queue.</span></span><li><span data-ttu-id="133b4-184">**taskcompletion**-等候目前正在執行工作 toofinish，然後從 hello 集區中移除 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-184">**taskcompletion**--Waits for currently running tasks toofinish and then removes hello node from hello pool.</span></span><li><span data-ttu-id="133b4-185">**retaineddata**-所有 hello 上的本機工作保留資料 hello 節點 toobe 等候清除之前移除 hello 集區中的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-185">**retaineddata**--Waits for all hello local task-retained data on hello node toobe cleaned up before removing hello node from hello pool.</span></span></ul> |

<span data-ttu-id="133b4-186">您可以取得服務定義的變數 toomake 調整 hello 批次服務的度量資訊為基礎的 hello 的值：</span><span class="sxs-lookup"><span data-stu-id="133b4-186">You can get hello value of these service-defined variables toomake adjustments that are based on metrics from hello Batch service:</span></span>

| <span data-ttu-id="133b4-187">唯讀服務定義變數</span><span class="sxs-lookup"><span data-stu-id="133b4-187">Read-only service-defined variables</span></span> | <span data-ttu-id="133b4-188">說明</span><span class="sxs-lookup"><span data-stu-id="133b4-188">Description</span></span> |
| --- | --- |
| <span data-ttu-id="133b4-189">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="133b4-189">$CPUPercent</span></span> |<span data-ttu-id="133b4-190">hello 平均 CPU 使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="133b4-190">hello average percentage of CPU usage.</span></span> |
| <span data-ttu-id="133b4-191">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="133b4-191">$WallClockSeconds</span></span> |<span data-ttu-id="133b4-192">hello 耗用的秒數。</span><span class="sxs-lookup"><span data-stu-id="133b4-192">hello number of seconds consumed.</span></span> |
| <span data-ttu-id="133b4-193">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-193">$MemoryBytes</span></span> |<span data-ttu-id="133b4-194">hello 平均 mb 數使用。</span><span class="sxs-lookup"><span data-stu-id="133b4-194">hello average number of megabytes used.</span></span> |
| <span data-ttu-id="133b4-195">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-195">$DiskBytes</span></span> |<span data-ttu-id="133b4-196">hello 平均 gb 數 hello 本機磁碟上使用。</span><span class="sxs-lookup"><span data-stu-id="133b4-196">hello average number of gigabytes used on hello local disks.</span></span> |
| <span data-ttu-id="133b4-197">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-197">$DiskReadBytes</span></span> |<span data-ttu-id="133b4-198">hello 讀取的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-198">hello number of bytes read.</span></span> |
| <span data-ttu-id="133b4-199">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-199">$DiskWriteBytes</span></span> |<span data-ttu-id="133b4-200">hello 寫入的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-200">hello number of bytes written.</span></span> |
| <span data-ttu-id="133b4-201">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="133b4-201">$DiskReadOps</span></span> |<span data-ttu-id="133b4-202">執行 hello 讀取的磁碟操作次數。</span><span class="sxs-lookup"><span data-stu-id="133b4-202">hello count of read disk operations performed.</span></span> |
| <span data-ttu-id="133b4-203">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="133b4-203">$DiskWriteOps</span></span> |<span data-ttu-id="133b4-204">執行的寫入磁碟作業的 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="133b4-204">hello count of write disk operations performed.</span></span> |
| <span data-ttu-id="133b4-205">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-205">$NetworkInBytes</span></span> |<span data-ttu-id="133b4-206">hello 輸入位元組數。</span><span class="sxs-lookup"><span data-stu-id="133b4-206">hello number of inbound bytes.</span></span> |
| <span data-ttu-id="133b4-207">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-207">$NetworkOutBytes</span></span> |<span data-ttu-id="133b4-208">hello 輸出的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-208">hello number of outbound bytes.</span></span> |
| <span data-ttu-id="133b4-209">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="133b4-209">$SampleNodeCount</span></span> |<span data-ttu-id="133b4-210">hello 的運算節點的計數。</span><span class="sxs-lookup"><span data-stu-id="133b4-210">hello count of compute nodes.</span></span> |
| <span data-ttu-id="133b4-211">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-211">$ActiveTasks</span></span> |<span data-ttu-id="133b4-212">hello 準備 tooexecute 但還未執行的工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-212">hello number of tasks that are ready tooexecute but are not yet executing.</span></span> <span data-ttu-id="133b4-213">hello $ActiveTasks 計數包含 hello 作用中狀態以及已滿足其相依性的所有工作。</span><span class="sxs-lookup"><span data-stu-id="133b4-213">hello $ActiveTasks count includes all tasks that are in hello active state and whose dependencies have been satisfied.</span></span> <span data-ttu-id="133b4-214">Hello 作用中狀態，但未滿足其相依性的工作會排除 hello $ActiveTasks 計數。</span><span class="sxs-lookup"><span data-stu-id="133b4-214">Any tasks that are in hello active state but whose dependencies have not been satisfied are excluded from hello $ActiveTasks count.</span></span>|
| <span data-ttu-id="133b4-215">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-215">$RunningTasks</span></span> |<span data-ttu-id="133b4-216">hello 處於執行中狀態的工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-216">hello number of tasks in a running state.</span></span> |
| <span data-ttu-id="133b4-217">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-217">$PendingTasks</span></span> |<span data-ttu-id="133b4-218">$ActiveTasks 和 $RunningTasks hello 總和。</span><span class="sxs-lookup"><span data-stu-id="133b4-218">hello sum of $ActiveTasks and $RunningTasks.</span></span> |
| <span data-ttu-id="133b4-219">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-219">$SucceededTasks</span></span> |<span data-ttu-id="133b4-220">hello 已順利完成的工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-220">hello number of tasks that finished successfully.</span></span> |
| <span data-ttu-id="133b4-221">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-221">$FailedTasks</span></span> |<span data-ttu-id="133b4-222">hello 失敗的工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-222">hello number of tasks that failed.</span></span> |
| <span data-ttu-id="133b4-223">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-223">$CurrentDedicatedNodes</span></span> |<span data-ttu-id="133b4-224">hello 目前數目專用計算節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-224">hello current number of dedicated compute nodes.</span></span> |
| <span data-ttu-id="133b4-225">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-225">$CurrentLowPriorityNodes</span></span> |<span data-ttu-id="133b4-226">hello 目前數目低優先順序的計算節點，包括任何已插播的節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-226">hello current number of low-priority compute nodes, including any nodes that have been pre-empted.</span></span> |
| <span data-ttu-id="133b4-227">$PreemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="133b4-227">$PreemptedNodeCount</span></span> | <span data-ttu-id="133b4-228">hello hello 集區中就會處於插播的節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-228">hello number of nodes in hello pool that are in a pre-empted state.</span></span> |

> [!TIP]
> <span data-ttu-id="133b4-229">hello hello 上表所示的唯讀、 服務定義的變數是*物件*tooaccess 每個相關聯的資料提供各種方法。</span><span class="sxs-lookup"><span data-stu-id="133b4-229">hello read-only, service-defined variables that are shown in hello previous table are *objects* that provide various methods tooaccess data associated with each.</span></span> <span data-ttu-id="133b4-230">如需詳細資訊，請參閱本文稍後的[取得範例資料](#getsampledata)。</span><span class="sxs-lookup"><span data-stu-id="133b4-230">For more information, see [Obtain sample data](#getsampledata) later in this article.</span></span>
>
>

## <a name="types"></a><span data-ttu-id="133b4-231">類型</span><span class="sxs-lookup"><span data-stu-id="133b4-231">Types</span></span>
<span data-ttu-id="133b4-232">公式中支援以下類型：</span><span class="sxs-lookup"><span data-stu-id="133b4-232">These types are supported in a formula:</span></span>

* <span data-ttu-id="133b4-233">double</span><span class="sxs-lookup"><span data-stu-id="133b4-233">double</span></span>
* <span data-ttu-id="133b4-234">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-234">doubleVec</span></span>
* <span data-ttu-id="133b4-235">doubleVecList</span><span class="sxs-lookup"><span data-stu-id="133b4-235">doubleVecList</span></span>
* <span data-ttu-id="133b4-236">字串</span><span class="sxs-lookup"><span data-stu-id="133b4-236">string</span></span>
* <span data-ttu-id="133b4-237">時間戳記-時間戳記是一種複合結構包含下列成員的 hello:</span><span class="sxs-lookup"><span data-stu-id="133b4-237">timestamp--timestamp is a compound structure that contains hello following members:</span></span>

  * <span data-ttu-id="133b4-238">年</span><span class="sxs-lookup"><span data-stu-id="133b4-238">year</span></span>
  * <span data-ttu-id="133b4-239">month (1-12)</span><span class="sxs-lookup"><span data-stu-id="133b4-239">month (1-12)</span></span>
  * <span data-ttu-id="133b4-240">day (1-31)</span><span class="sxs-lookup"><span data-stu-id="133b4-240">day (1-31)</span></span>
  * <span data-ttu-id="133b4-241">週間日 (hello 格式的數字，例如，1 代表星期一)</span><span class="sxs-lookup"><span data-stu-id="133b4-241">weekday (in hello format of number; for example, 1 for Monday)</span></span>
  * <span data-ttu-id="133b4-242">hour (以 24 小時制數字格式表示，例如 13 代表下午 1:00)</span><span class="sxs-lookup"><span data-stu-id="133b4-242">hour (in 24-hour number format; for example, 13 means 1 PM)</span></span>
  * <span data-ttu-id="133b4-243">minute (00-59)</span><span class="sxs-lookup"><span data-stu-id="133b4-243">minute (00-59)</span></span>
  * <span data-ttu-id="133b4-244">second (00-59)</span><span class="sxs-lookup"><span data-stu-id="133b4-244">second (00-59)</span></span>
* <span data-ttu-id="133b4-245">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-245">timeinterval</span></span>

  * <span data-ttu-id="133b4-246">TimeInterval_Zero</span><span class="sxs-lookup"><span data-stu-id="133b4-246">TimeInterval_Zero</span></span>
  * <span data-ttu-id="133b4-247">TimeInterval_100ns</span><span class="sxs-lookup"><span data-stu-id="133b4-247">TimeInterval_100ns</span></span>
  * <span data-ttu-id="133b4-248">TimeInterval_Microsecond</span><span class="sxs-lookup"><span data-stu-id="133b4-248">TimeInterval_Microsecond</span></span>
  * <span data-ttu-id="133b4-249">TimeInterval_Millisecond</span><span class="sxs-lookup"><span data-stu-id="133b4-249">TimeInterval_Millisecond</span></span>
  * <span data-ttu-id="133b4-250">TimeInterval_Second</span><span class="sxs-lookup"><span data-stu-id="133b4-250">TimeInterval_Second</span></span>
  * <span data-ttu-id="133b4-251">TimeInterval_Minute</span><span class="sxs-lookup"><span data-stu-id="133b4-251">TimeInterval_Minute</span></span>
  * <span data-ttu-id="133b4-252">TimeInterval_Hour</span><span class="sxs-lookup"><span data-stu-id="133b4-252">TimeInterval_Hour</span></span>
  * <span data-ttu-id="133b4-253">TimeInterval_Day</span><span class="sxs-lookup"><span data-stu-id="133b4-253">TimeInterval_Day</span></span>
  * <span data-ttu-id="133b4-254">TimeInterval_Week</span><span class="sxs-lookup"><span data-stu-id="133b4-254">TimeInterval_Week</span></span>
  * <span data-ttu-id="133b4-255">TimeInterval_Year</span><span class="sxs-lookup"><span data-stu-id="133b4-255">TimeInterval_Year</span></span>

## <a name="operations"></a><span data-ttu-id="133b4-256">作業</span><span class="sxs-lookup"><span data-stu-id="133b4-256">Operations</span></span>
<span data-ttu-id="133b4-257">列出 hello 前一節中的 hello 類型都允許這些作業。</span><span class="sxs-lookup"><span data-stu-id="133b4-257">These operations are allowed on hello types that are listed in hello previous section.</span></span>

| <span data-ttu-id="133b4-258">作業</span><span class="sxs-lookup"><span data-stu-id="133b4-258">Operation</span></span> | <span data-ttu-id="133b4-259">支援的運算子</span><span class="sxs-lookup"><span data-stu-id="133b4-259">Supported operators</span></span> | <span data-ttu-id="133b4-260">結果類型</span><span class="sxs-lookup"><span data-stu-id="133b4-260">Result type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="133b4-261">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="133b4-261">double *operator* double</span></span> |<span data-ttu-id="133b4-262">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="133b4-262">+, -, *, /</span></span> |<span data-ttu-id="133b4-263">double</span><span class="sxs-lookup"><span data-stu-id="133b4-263">double</span></span> |
| <span data-ttu-id="133b4-264">double 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-264">double *operator* timeinterval</span></span> |* |<span data-ttu-id="133b4-265">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-265">timeinterval</span></span> |
| <span data-ttu-id="133b4-266">doubleVec 運算子  double</span><span class="sxs-lookup"><span data-stu-id="133b4-266">doubleVec *operator* double</span></span> |<span data-ttu-id="133b4-267">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="133b4-267">+, -, *, /</span></span> |<span data-ttu-id="133b4-268">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-268">doubleVec</span></span> |
| <span data-ttu-id="133b4-269">doubleVec 運算子  doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-269">doubleVec *operator* doubleVec</span></span> |<span data-ttu-id="133b4-270">+、-、*、/</span><span class="sxs-lookup"><span data-stu-id="133b4-270">+, -, *, /</span></span> |<span data-ttu-id="133b4-271">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-271">doubleVec</span></span> |
| <span data-ttu-id="133b4-272">timeinterval 運算子  double</span><span class="sxs-lookup"><span data-stu-id="133b4-272">timeinterval *operator* double</span></span> |<span data-ttu-id="133b4-273">*、/</span><span class="sxs-lookup"><span data-stu-id="133b4-273">*, /</span></span> |<span data-ttu-id="133b4-274">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-274">timeinterval</span></span> |
| <span data-ttu-id="133b4-275">timeinterval 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-275">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="133b4-276">+、-</span><span class="sxs-lookup"><span data-stu-id="133b4-276">+, -</span></span> |<span data-ttu-id="133b4-277">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-277">timeinterval</span></span> |
| <span data-ttu-id="133b4-278">timeinterval 運算子  timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-278">timeinterval *operator* timestamp</span></span> |+ |<span data-ttu-id="133b4-279">timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-279">timestamp</span></span> |
| <span data-ttu-id="133b4-280">timestamp 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-280">timestamp *operator* timeinterval</span></span> |+ |<span data-ttu-id="133b4-281">timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-281">timestamp</span></span> |
| <span data-ttu-id="133b4-282">timestamp  timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-282">timestamp *operator* timestamp</span></span> |- |<span data-ttu-id="133b4-283">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-283">timeinterval</span></span> |
| <span data-ttu-id="133b4-284">double</span><span class="sxs-lookup"><span data-stu-id="133b4-284">*operator*double</span></span> |<span data-ttu-id="133b4-285">-、!</span><span class="sxs-lookup"><span data-stu-id="133b4-285">-, !</span></span> |<span data-ttu-id="133b4-286">double</span><span class="sxs-lookup"><span data-stu-id="133b4-286">double</span></span> |
| <span data-ttu-id="133b4-287">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-287">*operator*timeinterval</span></span> |- |<span data-ttu-id="133b4-288">timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-288">timeinterval</span></span> |
| <span data-ttu-id="133b4-289">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="133b4-289">double *operator* double</span></span> |<span data-ttu-id="133b4-290"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="133b4-290"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="133b4-291">double</span><span class="sxs-lookup"><span data-stu-id="133b4-291">double</span></span> |
| <span data-ttu-id="133b4-292">string  string</span><span class="sxs-lookup"><span data-stu-id="133b4-292">string *operator* string</span></span> |<span data-ttu-id="133b4-293"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="133b4-293"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="133b4-294">double</span><span class="sxs-lookup"><span data-stu-id="133b4-294">double</span></span> |
| <span data-ttu-id="133b4-295">timestamp  timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-295">timestamp *operator* timestamp</span></span> |<span data-ttu-id="133b4-296"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="133b4-296"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="133b4-297">double</span><span class="sxs-lookup"><span data-stu-id="133b4-297">double</span></span> |
| <span data-ttu-id="133b4-298">timeinterval 運算子  timeinterval</span><span class="sxs-lookup"><span data-stu-id="133b4-298">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="133b4-299"><、<=、==、>=、>、!=</span><span class="sxs-lookup"><span data-stu-id="133b4-299"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="133b4-300">double</span><span class="sxs-lookup"><span data-stu-id="133b4-300">double</span></span> |
| <span data-ttu-id="133b4-301">double 運算子  double</span><span class="sxs-lookup"><span data-stu-id="133b4-301">double *operator* double</span></span> |<span data-ttu-id="133b4-302">&&, &#124;&#124;</span><span class="sxs-lookup"><span data-stu-id="133b4-302">&&, &#124;&#124;</span></span> |<span data-ttu-id="133b4-303">double</span><span class="sxs-lookup"><span data-stu-id="133b4-303">double</span></span> |

<span data-ttu-id="133b4-304">測試具有三元運算子的雙精準數 (`double ? statement1 : statement2`) 時，非零為 **true**，而零則為 **false**。</span><span class="sxs-lookup"><span data-stu-id="133b4-304">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span></span>

## <a name="functions"></a><span data-ttu-id="133b4-305">Functions</span><span class="sxs-lookup"><span data-stu-id="133b4-305">Functions</span></span>
<span data-ttu-id="133b4-306">這些預先定義**函式**可供您 toouse 定義自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-306">These predefined **functions** are available for you toouse in defining an automatic scaling formula.</span></span>

| <span data-ttu-id="133b4-307">函式</span><span class="sxs-lookup"><span data-stu-id="133b4-307">Function</span></span> | <span data-ttu-id="133b4-308">傳回類型</span><span class="sxs-lookup"><span data-stu-id="133b4-308">Return type</span></span> | <span data-ttu-id="133b4-309">說明</span><span class="sxs-lookup"><span data-stu-id="133b4-309">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="133b4-310">avg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-310">avg(doubleVecList)</span></span> |<span data-ttu-id="133b4-311">double</span><span class="sxs-lookup"><span data-stu-id="133b4-311">double</span></span> |<span data-ttu-id="133b4-312">傳回 hello hello doubleVecList 中所有值的平均值。</span><span class="sxs-lookup"><span data-stu-id="133b4-312">Returns hello average value for all values in hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-313">len(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-313">len(doubleVecList)</span></span> |<span data-ttu-id="133b4-314">double</span><span class="sxs-lookup"><span data-stu-id="133b4-314">double</span></span> |<span data-ttu-id="133b4-315">傳回 hello 從 hello doubleVecList 建立 hello 向量的長度。</span><span class="sxs-lookup"><span data-stu-id="133b4-315">Returns hello length of hello vector that is created from hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-316">lg(double)</span><span class="sxs-lookup"><span data-stu-id="133b4-316">lg(double)</span></span> |<span data-ttu-id="133b4-317">double</span><span class="sxs-lookup"><span data-stu-id="133b4-317">double</span></span> |<span data-ttu-id="133b4-318">傳回 hello 記錄檔基底 2 的 hello double。</span><span class="sxs-lookup"><span data-stu-id="133b4-318">Returns hello log base 2 of hello double.</span></span> |
| <span data-ttu-id="133b4-319">lg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-319">lg(doubleVecList)</span></span> |<span data-ttu-id="133b4-320">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-320">doubleVec</span></span> |<span data-ttu-id="133b4-321">會傳回基底 2 的 hello doubleVecList hello component-wise 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="133b4-321">Returns hello component-wise log base 2 of hello doubleVecList.</span></span> <span data-ttu-id="133b4-322">Hello 參數必須明確傳遞 vec(double)。</span><span class="sxs-lookup"><span data-stu-id="133b4-322">A vec(double) must be explicitly passed for hello parameter.</span></span> <span data-ttu-id="133b4-323">否則，會假定 hello double lg （double） 版本。</span><span class="sxs-lookup"><span data-stu-id="133b4-323">Otherwise, hello double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="133b4-324">ln(double)</span><span class="sxs-lookup"><span data-stu-id="133b4-324">ln(double)</span></span> |<span data-ttu-id="133b4-325">double</span><span class="sxs-lookup"><span data-stu-id="133b4-325">double</span></span> |<span data-ttu-id="133b4-326">傳回 hello hello double 的自然對數。</span><span class="sxs-lookup"><span data-stu-id="133b4-326">Returns hello natural log of hello double.</span></span> |
| <span data-ttu-id="133b4-327">ln(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-327">ln(doubleVecList)</span></span> |<span data-ttu-id="133b4-328">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-328">doubleVec</span></span> |<span data-ttu-id="133b4-329">會傳回基底 2 的 hello doubleVecList hello component-wise 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="133b4-329">Returns hello component-wise log base 2 of hello doubleVecList.</span></span> <span data-ttu-id="133b4-330">Hello 參數必須明確傳遞 vec(double)。</span><span class="sxs-lookup"><span data-stu-id="133b4-330">A vec(double) must be explicitly passed for hello parameter.</span></span> <span data-ttu-id="133b4-331">否則，會假定 hello double lg （double） 版本。</span><span class="sxs-lookup"><span data-stu-id="133b4-331">Otherwise, hello double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="133b4-332">log(double)</span><span class="sxs-lookup"><span data-stu-id="133b4-332">log(double)</span></span> |<span data-ttu-id="133b4-333">double</span><span class="sxs-lookup"><span data-stu-id="133b4-333">double</span></span> |<span data-ttu-id="133b4-334">傳回 hello 記錄 10 為底數 hello double。</span><span class="sxs-lookup"><span data-stu-id="133b4-334">Returns hello log base 10 of hello double.</span></span> |
| <span data-ttu-id="133b4-335">log(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-335">log(doubleVecList)</span></span> |<span data-ttu-id="133b4-336">doubleVec</span><span class="sxs-lookup"><span data-stu-id="133b4-336">doubleVec</span></span> |<span data-ttu-id="133b4-337">傳回 hello component-wise 記錄 hello doubleVecList 的基底 10。</span><span class="sxs-lookup"><span data-stu-id="133b4-337">Returns hello component-wise log base 10 of hello doubleVecList.</span></span> <span data-ttu-id="133b4-338">Vec(double) hello 單一 double 參數必須明確地傳遞。</span><span class="sxs-lookup"><span data-stu-id="133b4-338">A vec(double) must be explicitly passed for hello single double parameter.</span></span> <span data-ttu-id="133b4-339">否則，會假定 hello double log(double) 版本。</span><span class="sxs-lookup"><span data-stu-id="133b4-339">Otherwise, hello double log(double) version is assumed.</span></span> |
| <span data-ttu-id="133b4-340">max(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-340">max(doubleVecList)</span></span> |<span data-ttu-id="133b4-341">double</span><span class="sxs-lookup"><span data-stu-id="133b4-341">double</span></span> |<span data-ttu-id="133b4-342">傳回 hello hello doubleVecList 中的最大值。</span><span class="sxs-lookup"><span data-stu-id="133b4-342">Returns hello maximum value in hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-343">min(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-343">min(doubleVecList)</span></span> |<span data-ttu-id="133b4-344">double</span><span class="sxs-lookup"><span data-stu-id="133b4-344">double</span></span> |<span data-ttu-id="133b4-345">傳回 hello hello doubleVecList 中的最小值。</span><span class="sxs-lookup"><span data-stu-id="133b4-345">Returns hello minimum value in hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-346">norm(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-346">norm(doubleVecList)</span></span> |<span data-ttu-id="133b4-347">double</span><span class="sxs-lookup"><span data-stu-id="133b4-347">double</span></span> |<span data-ttu-id="133b4-348">傳回 hello 2 範數從 hello doubleVecList 建立的 hello 向量。</span><span class="sxs-lookup"><span data-stu-id="133b4-348">Returns hello two-norm of hello vector that is created from hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-349">percentile(doubleVec v, double p)</span><span class="sxs-lookup"><span data-stu-id="133b4-349">percentile(doubleVec v, double p)</span></span> |<span data-ttu-id="133b4-350">double</span><span class="sxs-lookup"><span data-stu-id="133b4-350">double</span></span> |<span data-ttu-id="133b4-351">傳回 hello hello 向量 v 的百分位數元素。</span><span class="sxs-lookup"><span data-stu-id="133b4-351">Returns hello percentile element of hello vector v.</span></span> |
| <span data-ttu-id="133b4-352">rand()</span><span class="sxs-lookup"><span data-stu-id="133b4-352">rand()</span></span> |<span data-ttu-id="133b4-353">double</span><span class="sxs-lookup"><span data-stu-id="133b4-353">double</span></span> |<span data-ttu-id="133b4-354">傳回介於 0.0 到 1.0 之間的隨機值。</span><span class="sxs-lookup"><span data-stu-id="133b4-354">Returns a random value between 0.0 and 1.0.</span></span> |
| <span data-ttu-id="133b4-355">range(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-355">range(doubleVecList)</span></span> |<span data-ttu-id="133b4-356">double</span><span class="sxs-lookup"><span data-stu-id="133b4-356">double</span></span> |<span data-ttu-id="133b4-357">傳回 hello doubleVecList 中的 hello hello 最小和最大值之間的差異。</span><span class="sxs-lookup"><span data-stu-id="133b4-357">Returns hello difference between hello min and max values in hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-358">std(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-358">std(doubleVecList)</span></span> |<span data-ttu-id="133b4-359">double</span><span class="sxs-lookup"><span data-stu-id="133b4-359">double</span></span> |<span data-ttu-id="133b4-360">傳回 hello hello doubleVecList 中的 hello 值的樣本標準差。</span><span class="sxs-lookup"><span data-stu-id="133b4-360">Returns hello sample standard deviation of hello values in hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-361">stop()</span><span class="sxs-lookup"><span data-stu-id="133b4-361">stop()</span></span> | |<span data-ttu-id="133b4-362">停止 hello 自動調整運算式的評估。</span><span class="sxs-lookup"><span data-stu-id="133b4-362">Stops evaluation of hello autoscaling expression.</span></span> |
| <span data-ttu-id="133b4-363">sum(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="133b4-363">sum(doubleVecList)</span></span> |<span data-ttu-id="133b4-364">double</span><span class="sxs-lookup"><span data-stu-id="133b4-364">double</span></span> |<span data-ttu-id="133b4-365">傳回 hello 的 hello doubleVecList 的所有 hello 元件的總和。</span><span class="sxs-lookup"><span data-stu-id="133b4-365">Returns hello sum of all hello components of hello doubleVecList.</span></span> |
| <span data-ttu-id="133b4-366">time(string dateTime="")</span><span class="sxs-lookup"><span data-stu-id="133b4-366">time(string dateTime="")</span></span> |<span data-ttu-id="133b4-367">timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-367">timestamp</span></span> |<span data-ttu-id="133b4-368">如果沒有參數傳遞，或 hello hello dateTime 字串的時間戳記，如果它通過，傳回 hello 時間戳記的 hello 目前時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-368">Returns hello time stamp of hello current time if no parameters are passed, or hello time stamp of hello dateTime string if it is passed.</span></span> <span data-ttu-id="133b4-369">支援的 dateTime 格式為 W3C-DTF 和 RFC 1123。</span><span class="sxs-lookup"><span data-stu-id="133b4-369">Supported dateTime formats are W3C-DTF and RFC 1123.</span></span> |
| <span data-ttu-id="133b4-370">val(doubleVec v, double i)</span><span class="sxs-lookup"><span data-stu-id="133b4-370">val(doubleVec v, double i)</span></span> |<span data-ttu-id="133b4-371">double</span><span class="sxs-lookup"><span data-stu-id="133b4-371">double</span></span> |<span data-ttu-id="133b4-372">傳回 hello hello 元素位於位置 i 向量 v 中以零起始索引值。</span><span class="sxs-lookup"><span data-stu-id="133b4-372">Returns hello value of hello element that is at location i in vector v, with a starting index of zero.</span></span> |

<span data-ttu-id="133b4-373">一些 hello 上表所述的 hello 函式可接受清單做為引數。</span><span class="sxs-lookup"><span data-stu-id="133b4-373">Some of hello functions that are described in hello previous table can accept a list as an argument.</span></span> <span data-ttu-id="133b4-374">hello 以逗號分隔清單是任何組合*double*和*doubleVec*。</span><span class="sxs-lookup"><span data-stu-id="133b4-374">hello comma-separated list is any combination of *double* and *doubleVec*.</span></span> <span data-ttu-id="133b4-375">例如：</span><span class="sxs-lookup"><span data-stu-id="133b4-375">For example:</span></span>

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

<span data-ttu-id="133b4-376">hello *doubleVecList*值是單一轉換的 tooa *doubleVec*之前評估。</span><span class="sxs-lookup"><span data-stu-id="133b4-376">hello *doubleVecList* value is converted tooa single *doubleVec* before evaluation.</span></span> <span data-ttu-id="133b4-377">例如，如果`v = [1,2,3]`，然後呼叫`avg(v)`是相等的 toocalling `avg(1,2,3)`。</span><span class="sxs-lookup"><span data-stu-id="133b4-377">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent toocalling `avg(1,2,3)`.</span></span> <span data-ttu-id="133b4-378">呼叫`avg(v, 7)`是相等的 toocalling `avg(1,2,3,7)`。</span><span class="sxs-lookup"><span data-stu-id="133b4-378">Calling `avg(v, 7)` is equivalent toocalling `avg(1,2,3,7)`.</span></span>

## <span data-ttu-id="133b4-379"><a name="getsampledata"></a>取得樣本資料</span><span class="sxs-lookup"><span data-stu-id="133b4-379"><a name="getsampledata"></a>Obtain sample data</span></span>
<span data-ttu-id="133b4-380">自動調整公式會作用於 hello 批次服務所提供的度量資料 （範例）。</span><span class="sxs-lookup"><span data-stu-id="133b4-380">Autoscale formulas act on metrics data (samples) that is provided by hello Batch service.</span></span> <span data-ttu-id="133b4-381">公式成長或壓縮根據 hello 值，它會從 hello 服務取得的集區大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-381">A formula grows or shrinks pool size based on hello values that it obtains from hello service.</span></span> <span data-ttu-id="133b4-382">hello 服務定義的變數所描述的先前是提供各種方法 tooaccess 資料，該物件相關聯的物件。</span><span class="sxs-lookup"><span data-stu-id="133b4-382">hello service-defined variables that were described previously are objects that provide various methods tooaccess data that is associated with that object.</span></span> <span data-ttu-id="133b4-383">例如，hello 下列運算式會顯示要求 tooget hello 的 CPU 使用量的前五分鐘：</span><span class="sxs-lookup"><span data-stu-id="133b4-383">For example, hello following expression shows a request tooget hello last five minutes of CPU usage:</span></span>

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| <span data-ttu-id="133b4-384">方法</span><span class="sxs-lookup"><span data-stu-id="133b4-384">Method</span></span> | <span data-ttu-id="133b4-385">說明</span><span class="sxs-lookup"><span data-stu-id="133b4-385">Description</span></span> |
| --- | --- |
| <span data-ttu-id="133b4-386">GetSample()</span><span class="sxs-lookup"><span data-stu-id="133b4-386">GetSample()</span></span> |<span data-ttu-id="133b4-387">hello`GetSample()`方法傳回的資料樣本的向量。</span><span class="sxs-lookup"><span data-stu-id="133b4-387">hello `GetSample()` method returns a vector of data samples.</span></span><br/><br/><span data-ttu-id="133b4-388">一個樣本有 30 秒的度量資料。</span><span class="sxs-lookup"><span data-stu-id="133b4-388">A sample is 30 seconds worth of metrics data.</span></span> <span data-ttu-id="133b4-389">換句話說，每隔 30 秒會取得範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-389">In other words, samples are obtained every 30 seconds.</span></span> <span data-ttu-id="133b4-390">但是，如以下所述，沒有收集樣本時與時使用 tooa 公式之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="133b4-390">But as noted below, there is a delay between when a sample is collected and when it is available tooa formula.</span></span> <span data-ttu-id="133b4-391">因此，並非一段指定時間內的所有樣本都可供公式評估。</span><span class="sxs-lookup"><span data-stu-id="133b4-391">As such, not all samples for a given time period may be available for evaluation by a formula.</span></span><ul><li>`doubleVec GetSample(double count)`<br/><span data-ttu-id="133b4-392">指定 hello 範例 tooobtain hello 所收集的最新樣本數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-392">Specifies hello number of samples tooobtain from hello most recent samples that were collected.</span></span><br/><br/><span data-ttu-id="133b4-393">`GetSample(1)`傳回 hello 最後一個可用的範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-393">`GetSample(1)` returns hello last available sample.</span></span> <span data-ttu-id="133b4-394">針對度量類似`$CPUPercent`，不過，這應該不能因為它是不可能 tooknow*時*收集 hello 樣本。</span><span class="sxs-lookup"><span data-stu-id="133b4-394">For metrics like `$CPUPercent`, however, this should not be used because it is impossible tooknow *when* hello sample was collected.</span></span> <span data-ttu-id="133b4-395">此範例可能是最新的，也可能因為系統問題，是更舊的。</span><span class="sxs-lookup"><span data-stu-id="133b4-395">It might be recent, or, because of system issues, it might be much older.</span></span> <span data-ttu-id="133b4-396">最好是在這種情況下 toouse 如下所示的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="133b4-396">It is better in such cases toouse a time interval as shown below.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/><span data-ttu-id="133b4-397">指定收集樣本資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="133b4-397">Specifies a time frame for gathering sample data.</span></span> <span data-ttu-id="133b4-398">（選擇性），它也指定 hello 百分比的 hello 中必須有的範例要求的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="133b4-398">Optionally, it also specifies hello percentage of samples that must be available in hello requested time frame.</span></span><br/><br/><span data-ttu-id="133b4-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)`如果 hello 過去 10 分鐘內的所有範例都都存在於 hello CPUPercent 歷程記錄時，就會傳回 20 的範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for hello last 10 minutes are present in hello CPUPercent history.</span></span> <span data-ttu-id="133b4-400">如果 hello 過去一分鐘的記錄無法使用，不過，只有 18 箱範例則會傳回。</span><span class="sxs-lookup"><span data-stu-id="133b4-400">If hello last minute of history was not available, however, only 18 samples would be returned.</span></span> <span data-ttu-id="133b4-401">在此案例中：</span><span class="sxs-lookup"><span data-stu-id="133b4-401">In this case:</span></span><br/><br/><span data-ttu-id="133b4-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`就會失敗，因為只有 90%的 hello 範例可供使用。</span><span class="sxs-lookup"><span data-stu-id="133b4-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of hello samples are available.</span></span><br/><br/><span data-ttu-id="133b4-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` 會成功。</span><span class="sxs-lookup"><span data-stu-id="133b4-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/><span data-ttu-id="133b4-404">指定收集資料的時間範圍 (含開始時間和結束時間)。</span><span class="sxs-lookup"><span data-stu-id="133b4-404">Specifies a time frame for gathering data, with both a start time and an end time.</span></span><br/><br/><span data-ttu-id="133b4-405">如上面所述，沒有收集樣本時與時使用 tooa 公式之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="133b4-405">As mentioned above, there is a delay between when a sample is collected and when it is available tooa formula.</span></span> <span data-ttu-id="133b4-406">請考慮此延遲時間，當您使用 hello`GetSample`方法。</span><span class="sxs-lookup"><span data-stu-id="133b4-406">Consider this delay when you use hello `GetSample` method.</span></span> <span data-ttu-id="133b4-407">請參閱下文中的 `GetSamplePercent`。</span><span class="sxs-lookup"><span data-stu-id="133b4-407">See `GetSamplePercent` below.</span></span> |
| <span data-ttu-id="133b4-408">GetSamplePeriod()</span><span class="sxs-lookup"><span data-stu-id="133b4-408">GetSamplePeriod()</span></span> |<span data-ttu-id="133b4-409">傳回 hello 的期間所執行的範例中的歷程記錄的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="133b4-409">Returns hello period of samples that were taken in a historical sample data set.</span></span> |
| <span data-ttu-id="133b4-410">Count()</span><span class="sxs-lookup"><span data-stu-id="133b4-410">Count()</span></span> |<span data-ttu-id="133b4-411">傳回 hello hello 度量歷程記錄中的樣本總數。</span><span class="sxs-lookup"><span data-stu-id="133b4-411">Returns hello total number of samples in hello metric history.</span></span> |
| <span data-ttu-id="133b4-412">HistoryBeginTime()</span><span class="sxs-lookup"><span data-stu-id="133b4-412">HistoryBeginTime()</span></span> |<span data-ttu-id="133b4-413">傳回 hello hello 最早可用的資料範例 hello 度量的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="133b4-413">Returns hello time stamp of hello oldest available data sample for hello metric.</span></span> |
| <span data-ttu-id="133b4-414">GetSamplePercent()</span><span class="sxs-lookup"><span data-stu-id="133b4-414">GetSamplePercent()</span></span> |<span data-ttu-id="133b4-415">傳回 hello 百分比在指定的時間間隔內所提供的範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-415">Returns hello percentage of samples that are available for a given time interval.</span></span> <span data-ttu-id="133b4-416">例如：</span><span class="sxs-lookup"><span data-stu-id="133b4-416">For example:</span></span><br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/><span data-ttu-id="133b4-417">因為 hello`GetSample`方法失敗的傳回的樣本 hello 百分比是否小於 hello`samplePercent`指定，您可以使用 hello`GetSamplePercent`方法 toocheck 第一次。</span><span class="sxs-lookup"><span data-stu-id="133b4-417">Because hello `GetSample` method fails if hello percentage of samples returned is less than hello `samplePercent` specified, you can use hello `GetSamplePercent` method toocheck first.</span></span> <span data-ttu-id="133b4-418">然後您可以執行替代的動作，如果沒有足夠的樣本不存在，而不暫停 hello 自動縮放評估。</span><span class="sxs-lookup"><span data-stu-id="133b4-418">Then you can perform an alternate action if insufficient samples are present, without halting hello automatic scaling evaluation.</span></span> |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a><span data-ttu-id="133b4-419">範例、 範例百分比和 hello *GetSample()*方法</span><span class="sxs-lookup"><span data-stu-id="133b4-419">Samples, sample percentage, and hello *GetSample()* method</span></span>
<span data-ttu-id="133b4-420">自動調整公式 hello 核心作業 tooobtain 工作和資源計量資料，然後再調整集區的大小，根據該資料。</span><span class="sxs-lookup"><span data-stu-id="133b4-420">hello core operation of an autoscale formula is tooobtain task and resource metric data and then adjust pool size based on that data.</span></span> <span data-ttu-id="133b4-421">因此，很重要的 toohave 清楚了解如何自動調整公式互動度量資料 （範例）。</span><span class="sxs-lookup"><span data-stu-id="133b4-421">As such, it is important toohave a clear understanding of how autoscale formulas interact with metrics data (samples).</span></span>

<span data-ttu-id="133b4-422">**範例**</span><span class="sxs-lookup"><span data-stu-id="133b4-422">**Samples**</span></span>

<span data-ttu-id="133b4-423">hello 批次服務會定期接受的工作和資源度量的範例，並使其可用 tooyour 自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-423">hello Batch service periodically takes samples of task and resource metrics and makes them available tooyour autoscale formulas.</span></span> <span data-ttu-id="133b4-424">這些範例 hello 批次服務會記錄每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="133b4-424">These samples are recorded every 30 seconds by hello Batch service.</span></span> <span data-ttu-id="133b4-425">不過，則通常延遲之間時記錄這些樣本數，且它們可供使用太 （且可讀取） 時，自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-425">However, there is typically a delay between when those samples were recorded and when they are made available too(and can be read by) your autoscale formulas.</span></span> <span data-ttu-id="133b4-426">此外，由於 toovarious 因素，例如網路或其他基礎結構問題，範例就不會記錄特定的間隔。</span><span class="sxs-lookup"><span data-stu-id="133b4-426">Additionally, due toovarious factors such as network or other infrastructure issues, samples may not be recorded for a particular interval.</span></span>

<span data-ttu-id="133b4-427">**樣本百分比**</span><span class="sxs-lookup"><span data-stu-id="133b4-427">**Sample percentage**</span></span>

<span data-ttu-id="133b4-428">當`samplePercent`傳遞 toohello`GetSample()`方法或 hello`GetSamplePercent()`呼叫方法時，_百分比_參考 tooa hello 可能的樣本總數 hello 批次服務所記錄的比較和hello 是可用 tooyour 自動調整公式的樣本數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-428">When `samplePercent` is passed toohello `GetSample()` method or hello `GetSamplePercent()` method is called, _percent_ refers tooa comparison between hello total possible number of samples that are recorded by hello Batch service and hello number of samples that are available tooyour autoscale formula.</span></span>

<span data-ttu-id="133b4-429">讓我們以 10 分鐘的時間範圍為例。</span><span class="sxs-lookup"><span data-stu-id="133b4-429">Let's look at a 10-minute timespan as an example.</span></span> <span data-ttu-id="133b4-430">範例會記錄在 10 分鐘的時間範圍內每隔 30 秒，因為 hello 最大的樣本總數所記錄的批次，就會是 20 範例 (每分鐘 2)。</span><span class="sxs-lookup"><span data-stu-id="133b4-430">Because samples are recorded every 30 seconds within a 10-minute timespan, hello maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span></span> <span data-ttu-id="133b4-431">不過，由於 toohello 固有延遲的 hello 報告機制，並在 Azure 中的其他問題，可能有只 15 會讀取可用 tooyour 自動調整公式的範例。</span><span class="sxs-lookup"><span data-stu-id="133b4-431">However, due toohello inherent latency of hello reporting mechanism and other issues within Azure, there may be only 15 samples that are available tooyour autoscale formula for reading.</span></span> <span data-ttu-id="133b4-432">因此，比方說，該 10 分鐘期間內，只有 75%的 hello 樣本總數記錄可能是可用 tooyour 公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-432">So, for example, for that 10-minute period, only 75% of hello total number of samples recorded may be available tooyour formula.</span></span>

<span data-ttu-id="133b4-433">**GetSample() 和樣本範圍**</span><span class="sxs-lookup"><span data-stu-id="133b4-433">**GetSample() and sample ranges**</span></span>

<span data-ttu-id="133b4-434">自動調整公式會進行 toobe 擴張和縮小您的集區&mdash;加入節點或移除節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-434">Your autoscale formulas are going toobe growing and shrinking your pools &mdash; adding nodes or removing nodes.</span></span> <span data-ttu-id="133b4-435">因為節點需付費，您會想 tooensure 公式使用一種智慧型的足夠資料為基礎的分析方法。</span><span class="sxs-lookup"><span data-stu-id="133b4-435">Because nodes cost you money, you want tooensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span></span> <span data-ttu-id="133b4-436">因此，建議您在公式中使用趨勢類型分析。</span><span class="sxs-lookup"><span data-stu-id="133b4-436">Therefore, we recommend that you use a trending-type analysis in your formulas.</span></span> <span data-ttu-id="133b4-437">此類型會根據所收集樣本的範圍來擴大和縮減集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-437">This type grows and shrinks your pools based on a range of collected samples.</span></span>

<span data-ttu-id="133b4-438">因此，使用 toodo `GetSample(interval look-back start, interval look-back end)` tooreturn 向量的範例：</span><span class="sxs-lookup"><span data-stu-id="133b4-438">toodo so, use `GetSample(interval look-back start, interval look-back end)` tooreturn a vector of samples:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

<span data-ttu-id="133b4-439">批次所評估 hello 線條上方時，它會傳回範圍的範例為值的向量。</span><span class="sxs-lookup"><span data-stu-id="133b4-439">When hello above line is evaluated by Batch, it returns a range of samples as a vector of values.</span></span> <span data-ttu-id="133b4-440">例如：</span><span class="sxs-lookup"><span data-stu-id="133b4-440">For example:</span></span>

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

<span data-ttu-id="133b4-441">一旦您已收集的樣本 hello 向量，您可以使用函式，例如`min()`， `max()`，和`avg()`tooderive 有意義的值從 hello 收集的範圍。</span><span class="sxs-lookup"><span data-stu-id="133b4-441">Once you've collected hello vector of samples, you can then use functions like `min()`, `max()`, and `avg()` tooderive meaningful values from hello collected range.</span></span>

<span data-ttu-id="133b4-442">為了增加安全性，您可以強制公式評估 toofail 如果某個範例百分比小於可用的特定時間週期。</span><span class="sxs-lookup"><span data-stu-id="133b4-442">For additional security, you can force a formula evaluation toofail if less than a certain sample percentage is available for a particular time period.</span></span> <span data-ttu-id="133b4-443">當您強制評估公式 toofail 時，您可以指示批次 toocease 進一步評估 hello 公式如果 hello 指定百分比的樣本就無法使用。</span><span class="sxs-lookup"><span data-stu-id="133b4-443">When you force a formula evaluation toofail, you instruct Batch toocease further evaluation of hello formula if hello specified percentage of samples is not available.</span></span> <span data-ttu-id="133b4-444">在此情況下，不會變更 toohello 集區大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-444">In this case, no change is made toohello pool size.</span></span> <span data-ttu-id="133b4-445">toospecify 的 hello 評估 toosucceed，如範例所需的百分比指定它，如太 hello 第三個參數`GetSample()`。</span><span class="sxs-lookup"><span data-stu-id="133b4-445">toospecify a required percentage of samples for hello evaluation toosucceed, specify it as hello third parameter too`GetSample()`.</span></span> <span data-ttu-id="133b4-446">以下指定了 75% 的樣本需求：</span><span class="sxs-lookup"><span data-stu-id="133b4-446">Here, a requirement of 75 percent of samples is specified:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

<span data-ttu-id="133b4-447">因為範例可用性可能會有延遲，務必 tooalways 指定時間範圍超過一分鐘的外觀後開始時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-447">Because there may be a delay in sample availability, it is important tooalways specify a time range with a look-back start time that is older than one minute.</span></span> <span data-ttu-id="133b4-448">花費大約一分鐘的 hello 範圍中的範例 toopropagate 透過 hello 系統，因此範例`(0 * TimeInterval_Second, 60 * TimeInterval_Second)`可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="133b4-448">It takes approximately one minute for samples toopropagate through hello system, so samples in hello range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span></span> <span data-ttu-id="133b4-449">同樣地，您可以使用 hello 百分比參數`GetSample()`tooforce 特定範例百分比需求。</span><span class="sxs-lookup"><span data-stu-id="133b4-449">Again, you can use hello percentage parameter of `GetSample()` tooforce a particular sample percentage requirement.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="133b4-450">我們**強烈建議**您***避免「只」*`GetSample(1)`依賴自動調整公式中的** 。</span><span class="sxs-lookup"><span data-stu-id="133b4-450">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span></span> <span data-ttu-id="133b4-451">這是因為`GetSample(1)`基本上是說： toohello 批次服務，「 讓我 hello 最後一個範例，無論擷取多久以前。 」</span><span class="sxs-lookup"><span data-stu-id="133b4-451">This is because `GetSample(1)` essentially says toohello Batch service, "Give me hello last sample you have, no matter how long ago you retrieved it."</span></span> <span data-ttu-id="133b4-452">由於它是單一樣本，而且可能是較舊的範例，它可能無法代表 hello 放大圖片的最新的工作或資源狀態。</span><span class="sxs-lookup"><span data-stu-id="133b4-452">Since it is only a single sample, and it may be an older sample, it may not be representative of hello larger picture of recent task or resource state.</span></span> <span data-ttu-id="133b4-453">如果您使用`GetSample(1)`，請確定它是較大的陳述式的一部分，並不 hello 公式依賴資料點。</span><span class="sxs-lookup"><span data-stu-id="133b4-453">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not hello only data point that your formula relies on.</span></span>
>
>

## <a name="metrics"></a><span data-ttu-id="133b4-454">度量</span><span class="sxs-lookup"><span data-stu-id="133b4-454">Metrics</span></span>
<span data-ttu-id="133b4-455">您可以在定義公式時使用資源和工作計量。</span><span class="sxs-lookup"><span data-stu-id="133b4-455">You can use both resource and task metrics when you're defining a formula.</span></span> <span data-ttu-id="133b4-456">您調整專用的節點，根據 hello 度量資料所取得，並評估 hello 集區中的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-456">You adjust hello target number of dedicated nodes in hello pool based on hello metrics data that you obtain and evaluate.</span></span> <span data-ttu-id="133b4-457">請參閱 hello[變數](#variables)節，如需有關每個度量。</span><span class="sxs-lookup"><span data-stu-id="133b4-457">See hello [Variables](#variables) section above for more information on each metric.</span></span>

<table>
  <tr>
    <th><span data-ttu-id="133b4-458">計量</span><span class="sxs-lookup"><span data-stu-id="133b4-458">Metric</span></span></th>
    <th><span data-ttu-id="133b4-459">說明</span><span class="sxs-lookup"><span data-stu-id="133b4-459">Description</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="133b4-460"><b>Resource</b></span><span class="sxs-lookup"><span data-stu-id="133b4-460"><b>Resource</b></span></span></td>
    <td><p><span data-ttu-id="133b4-461">資源計量根據 hello CPU、 hello 頻寬、 hello 的運算節點的記憶體使用量和 hello 的節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-461">Resource metrics are based on hello CPU, hello bandwidth, hello memory usage of compute nodes, and hello number of nodes.</span></span></p>
        <p> <span data-ttu-id="133b4-462">這些服務定義的變數適合用於根據節點計數進行調整：</span><span class="sxs-lookup"><span data-stu-id="133b4-462">These service-defined variables are useful for making adjustments based on node count:</span></span></p>
    <p><ul>
            <li><span data-ttu-id="133b4-463">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-463">$TargetDedicatedNodes</span></span></li>
            <li><span data-ttu-id="133b4-464">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-464">$TargetLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="133b4-465">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-465">$CurrentDedicatedNodes</span></span></li>
            <li><span data-ttu-id="133b4-466">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="133b4-466">$CurrentLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="133b4-467">$preemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="133b4-467">$preemptedNodeCount</span></span></li>
            <li><span data-ttu-id="133b4-468">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="133b4-468">$SampleNodeCount</span></span></li>
    </ul></p>
    <p><span data-ttu-id="133b4-469">這些服務定義的變數適合用於根據節點資源使用量進行調整：</span><span class="sxs-lookup"><span data-stu-id="133b4-469">These service-defined variables are useful for making adjustments based on node resource usage:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="133b4-470">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="133b4-470">$CPUPercent</span></span></li>
      <li><span data-ttu-id="133b4-471">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="133b4-471">$WallClockSeconds</span></span></li>
      <li><span data-ttu-id="133b4-472">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-472">$MemoryBytes</span></span></li>
      <li><span data-ttu-id="133b4-473">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-473">$DiskBytes</span></span></li>
      <li><span data-ttu-id="133b4-474">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-474">$DiskReadBytes</span></span></li>
      <li><span data-ttu-id="133b4-475">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-475">$DiskWriteBytes</span></span></li>
      <li><span data-ttu-id="133b4-476">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="133b4-476">$DiskReadOps</span></span></li>
      <li><span data-ttu-id="133b4-477">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="133b4-477">$DiskWriteOps</span></span></li>
      <li><span data-ttu-id="133b4-478">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-478">$NetworkInBytes</span></span></li>
      <li><span data-ttu-id="133b4-479">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="133b4-479">$NetworkOutBytes</span></span></li></ul></p>
  </tr>
  <tr>
    <td><span data-ttu-id="133b4-480"><b>Task</b></span><span class="sxs-lookup"><span data-stu-id="133b4-480"><b>Task</b></span></span></td>
    <td><p><span data-ttu-id="133b4-481">工作度量資訊為基礎的工作，例如作用中的 hello 狀態暫止狀態，且在完成。</span><span class="sxs-lookup"><span data-stu-id="133b4-481">Task metrics are based on hello status of tasks, such as Active, Pending, and Completed.</span></span> <span data-ttu-id="133b4-482">hello 下列服務定義的變數可用於進行根據工作度量的集區大小調整：</span><span class="sxs-lookup"><span data-stu-id="133b4-482">hello following service-defined variables are useful for making pool-size adjustments based on task metrics:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="133b4-483">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-483">$ActiveTasks</span></span></li>
      <li><span data-ttu-id="133b4-484">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-484">$RunningTasks</span></span></li>
      <li><span data-ttu-id="133b4-485">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-485">$PendingTasks</span></span></li>
      <li><span data-ttu-id="133b4-486">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-486">$SucceededTasks</span></span></li>
            <li><span data-ttu-id="133b4-487">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="133b4-487">$FailedTasks</span></span></li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a><span data-ttu-id="133b4-488">撰寫自動調整公式</span><span class="sxs-lookup"><span data-stu-id="133b4-488">Write an autoscale formula</span></span>
<span data-ttu-id="133b4-489">您藉由形成使用 hello 元件，上面的陳述式來建置自動調整公式，然後合併這些陳述式完成公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-489">You build an autoscale formula by forming statements that use hello above components, then combine those statements into a complete formula.</span></span> <span data-ttu-id="133b4-490">在本節中，我們會建立可以執行一些真實世界調整決策的範例自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-490">In this section, we create an example autoscale formula that can perform some real-world scaling decisions.</span></span>

<span data-ttu-id="133b4-491">首先，讓我們來定義新的自動調整公式的 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="133b4-491">First, let's define hello requirements for our new autoscale formula.</span></span> <span data-ttu-id="133b4-492">應該 hello 公式：</span><span class="sxs-lookup"><span data-stu-id="133b4-492">hello formula should:</span></span>

1. <span data-ttu-id="133b4-493">如果 CPU 使用率偏高，請增加集區中的專用的運算節點的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-493">Increase hello target number of dedicated compute nodes in a pool if CPU usage is high.</span></span>
2. <span data-ttu-id="133b4-494">CPU 使用率較低時，請減少集區中的專用的運算節點的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-494">Decrease hello target number of dedicated compute nodes in a pool when CPU usage is low.</span></span>
3. <span data-ttu-id="133b4-495">永遠限制 hello too400 專用的節點數目上限。</span><span class="sxs-lookup"><span data-stu-id="133b4-495">Always restrict hello maximum number of dedicated nodes too400.</span></span>

<span data-ttu-id="133b4-496">在高 CPU 使用量，節點的 tooincrease hello 數目定義填入使用者定義變數的 hello 陳述式 (`$totalDedicatedNodes`) 的值，如果是 110%的 hello 目標的目前專用節點數目，但僅限於 hello 最小值的平均 CPU 使用量期間 hello 過去 10 分鐘內為百分之 70。</span><span class="sxs-lookup"><span data-stu-id="133b4-496">tooincrease hello number of nodes during high CPU usage, define hello statement that populates a user-defined variable (`$totalDedicatedNodes`) with a value that is 110 percent of hello current target number of dedicated nodes, but only if hello minimum average CPU usage during hello last 10 minutes was above 70 percent.</span></span> <span data-ttu-id="133b4-497">否則，請使用 hello 值 hello 目前專用的節點數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-497">Otherwise, use hello value for hello current number of dedicated nodes.</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

<span data-ttu-id="133b4-498">太*減少*hello 低 CPU 使用率在專用的節點數目，在我們的公式集 hello 的下一個陳述式相同的 hello`$totalDedicatedNodes`變數 too90 百分比的專用的節點，如果 hello hello 目前目標數目的平均 CPU 使用量在 hello 過去的 60 分鐘底下是 20%。</span><span class="sxs-lookup"><span data-stu-id="133b4-498">too*decrease* hello number of dedicated nodes during low CPU usage, hello next statement in our formula sets hello same `$totalDedicatedNodes` variable too90 percent of hello current target number of dedicated nodes if hello average CPU usage in hello past 60 minutes was under 20 percent.</span></span> <span data-ttu-id="133b4-499">否則，請使用 hello 目前值`$totalDedicatedNodes`我們 hello 上面的陳述式中擴展。</span><span class="sxs-lookup"><span data-stu-id="133b4-499">Otherwise, use hello current value of `$totalDedicatedNodes` that we populated in hello statement above.</span></span>

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

<span data-ttu-id="133b4-500">現在限制專用的運算節點 tooa 最大值為 400 hello 目標數目：</span><span class="sxs-lookup"><span data-stu-id="133b4-500">Now limit hello target number of dedicated compute nodes tooa maximum of 400:</span></span>

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

<span data-ttu-id="133b4-501">以下是 hello 完整的公式：</span><span class="sxs-lookup"><span data-stu-id="133b4-501">Here's hello complete formula:</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a><span data-ttu-id="133b4-502">使用 .NET 建立已啟用自動調整的集區</span><span class="sxs-lookup"><span data-stu-id="133b4-502">Create an autoscale-enabled pool with .NET</span></span>

<span data-ttu-id="133b4-503">toocreate 在.NET 中，啟用自動調整集區，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="133b4-503">toocreate a pool with autoscaling enabled in .NET, follow these steps:</span></span>

1. <span data-ttu-id="133b4-504">建立具有 hello 集區[BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool)。</span><span class="sxs-lookup"><span data-stu-id="133b4-504">Create hello pool with [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).</span></span>
2. <span data-ttu-id="133b4-505">設定 hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled)屬性太`true`。</span><span class="sxs-lookup"><span data-stu-id="133b4-505">Set hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) property too`true`.</span></span>
3. <span data-ttu-id="133b4-506">設定 hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula)具有自動調整公式的內容。</span><span class="sxs-lookup"><span data-stu-id="133b4-506">Set hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) property with your autoscale formula.</span></span>
4. <span data-ttu-id="133b4-507">（選擇性）設定 hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval)屬性 （預設為 15 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="133b4-507">(Optional) Set hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) property (default is 15 minutes).</span></span>
5. <span data-ttu-id="133b4-508">認可 hello 集區與[CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit)或[CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync)。</span><span class="sxs-lookup"><span data-stu-id="133b4-508">Commit hello pool with [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) or [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).</span></span>

<span data-ttu-id="133b4-509">hello 下列程式碼片段會建立啟用自動調整集區在.NET 中。</span><span class="sxs-lookup"><span data-stu-id="133b4-509">hello following code snippet creates an autoscale-enabled pool in .NET.</span></span> <span data-ttu-id="133b4-510">hello 集區的自動調整公式集 hello 目標數目，從星期一，專用的節點 too5 和 1 hello 當週的一天。</span><span class="sxs-lookup"><span data-stu-id="133b4-510">hello pool's autoscale formula sets hello target number of dedicated nodes too5 on Mondays, and 1 on every other day of hello week.</span></span> <span data-ttu-id="133b4-511">hello[自動調整間隔](#automatic-scaling-interval)是設定 too30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="133b4-511">hello [automatic scaling interval](#automatic-scaling-interval) is set too30 minutes.</span></span> <span data-ttu-id="133b4-512">在此與其他 C# 程式碼片段在本文中的 hello `myBatchClient` hello 的正確初始化執行個體[BatchClient] [ net_batchclient]類別。</span><span class="sxs-lookup"><span data-stu-id="133b4-512">In this and hello other C# snippets in this article, `myBatchClient` is a properly initialized instance of hello [BatchClient][net_batchclient] class.</span></span>

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
> <span data-ttu-id="133b4-513">當您建立啟用自動調整集區時，請勿指定 hello _targetDedicatedComputeNodes_參數或 hello _targetLowPriorityComputeNodes_ hello 參數呼叫太**CreatePool**。</span><span class="sxs-lookup"><span data-stu-id="133b4-513">When you create an autoscale-enabled pool, do not specify hello _targetDedicatedComputeNodes_ parameter or hello _targetLowPriorityComputeNodes_ parameter on hello call too**CreatePool**.</span></span> <span data-ttu-id="133b4-514">請改為指定 hello **AutoScaleEnabled**和**AutoScaleFormula** hello 集區上的屬性。</span><span class="sxs-lookup"><span data-stu-id="133b4-514">Instead, specify hello **AutoScaleEnabled** and **AutoScaleFormula** properties on hello pool.</span></span> <span data-ttu-id="133b4-515">這些屬性的 hello 值決定每個節點類型的 hello 目標數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-515">hello values for these properties determine hello target number of each type of node.</span></span> <span data-ttu-id="133b4-516">另外，toomanually 調整啟用自動調整集區 (比方說，使用[BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync])、 第一個**停用**上的自動調整hello 集區，然後調整其大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-516">Also, toomanually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), first **disable** automatic scaling on hello pool, then resize it.</span></span>
>
>

<span data-ttu-id="133b4-517">此外 tooBatch.NET 中，您可以使用任何其他 hello[批次 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development)，[批次 REST](https://docs.microsoft.com/rest/api/batchservice/)，[批次的 PowerShell cmdlet](batch-powershell-cmdlets-get-started.md)，和 hello[批次 CLI](batch-cli-get-started.md)tooconfigure 自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-517">In addition tooBatch .NET, you can use any of hello other [Batch SDKs](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and hello [Batch CLI](batch-cli-get-started.md) tooconfigure autoscaling.</span></span>


### <a name="automatic-scaling-interval"></a><span data-ttu-id="133b4-518">自動調整間隔</span><span class="sxs-lookup"><span data-stu-id="133b4-518">Automatic scaling interval</span></span>
<span data-ttu-id="133b4-519">根據預設，hello 批次服務會調整集區的大小根據 tooits 自動調整公式每隔 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="133b4-519">By default, hello Batch service adjusts a pool's size according tooits autoscale formula every 15 minutes.</span></span> <span data-ttu-id="133b4-520">此間隔是可設定使用下列屬性集區的 hello:</span><span class="sxs-lookup"><span data-stu-id="133b4-520">This interval is configurable by using hello following pool properties:</span></span>

* <span data-ttu-id="133b4-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="133b4-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span></span>
* <span data-ttu-id="133b4-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span><span class="sxs-lookup"><span data-stu-id="133b4-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span></span>

<span data-ttu-id="133b4-523">hello 最小間隔為 5 分鐘，並 hello 最大值為 168 小時。</span><span class="sxs-lookup"><span data-stu-id="133b4-523">hello minimum interval is five minutes, and hello maximum is 168 hours.</span></span> <span data-ttu-id="133b4-524">如果指定的間隔，在這個範圍之外，hello 批次服務會傳回不正確的要求 (400) 錯誤。</span><span class="sxs-lookup"><span data-stu-id="133b4-524">If an interval outside this range is specified, hello Batch service returns a Bad Request (400) error.</span></span>

> [!NOTE]
> <span data-ttu-id="133b4-525">自動調整在少於一分鐘內，不是目前預期的 toorespond toochanges 但而不是為您執行工作負載時逐漸適合 tooadjust hello 大小的集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-525">Autoscaling is not currently intended toorespond toochanges in less than a minute, but rather is intended tooadjust hello size of your pool gradually as you run a workload.</span></span>
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a><span data-ttu-id="133b4-526">在現有集區啟用自動調整</span><span class="sxs-lookup"><span data-stu-id="133b4-526">Enable autoscaling on an existing pool</span></span>

<span data-ttu-id="133b4-527">每個批次 SDK 提供方式 tooenable 自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-527">Each Batch SDK provides a way tooenable autoscaling.</span></span> <span data-ttu-id="133b4-528">例如：</span><span class="sxs-lookup"><span data-stu-id="133b4-528">For example:</span></span>

* <span data-ttu-id="133b4-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="133b4-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span></span>
* <span data-ttu-id="133b4-530">[在自動調整中啟用集區][rest_enableautoscale] (REST API)</span><span class="sxs-lookup"><span data-stu-id="133b4-530">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span></span>

<span data-ttu-id="133b4-531">當您啟用自動調整現有的集區上時，請遵循點注意 hello:</span><span class="sxs-lookup"><span data-stu-id="133b4-531">When you enable autoscaling on an existing pool, keep in mind hello following points:</span></span>

* <span data-ttu-id="133b4-532">如果自動調整為目前已停用 hello 集區上發出 hello 要求 tooenable 自動調整時，您必須指定有效的自動調整公式，當發出 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="133b4-532">If automatic scaling is currently disabled on hello pool when you issue hello request tooenable autoscaling, you must specify a valid autoscale formula when you issue hello request.</span></span> <span data-ttu-id="133b4-533">您可以選擇性地指定自動調整評估間隔。</span><span class="sxs-lookup"><span data-stu-id="133b4-533">You can optionally specify an autoscale evaluation interval.</span></span> <span data-ttu-id="133b4-534">如果您未指定間隔，則會使用 hello 預設值 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="133b4-534">If you do not specify an interval, hello default value of 15 minutes is used.</span></span>
* <span data-ttu-id="133b4-535">如果目前 hello 集區上啟用自動調整規模，您可以指定自動調整公式、 評估間隔，或兩者。</span><span class="sxs-lookup"><span data-stu-id="133b4-535">If autoscale is currently enabled on hello pool, you can specify an autoscale formula, an evaluation interval, or both.</span></span> <span data-ttu-id="133b4-536">您必須至少指定其中一個屬性。</span><span class="sxs-lookup"><span data-stu-id="133b4-536">You must specify at least one of these properties.</span></span>

  * <span data-ttu-id="133b4-537">如果您指定新的自動調整規模評估間隔，然後 hello 現有評估排程就會停止並啟動新的排程。</span><span class="sxs-lookup"><span data-stu-id="133b4-537">If you specify a new autoscale evaluation interval, then hello existing evaluation schedule is stopped and a new schedule is started.</span></span> <span data-ttu-id="133b4-538">hello 新排程的開始時間是哪些 hello 要求 tooenable 自動調整的發出 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-538">hello new schedule's start time is hello time at which hello request tooenable autoscaling was issued.</span></span>
  * <span data-ttu-id="133b4-539">如果您省略任一 hello 自動調整公式或評估間隔，hello 批次服務會繼續 toouse hello 目前的設定值。</span><span class="sxs-lookup"><span data-stu-id="133b4-539">If you omit either hello autoscale formula or evaluation interval, hello Batch service continues toouse hello current value of that setting.</span></span>

> [!NOTE]
> <span data-ttu-id="133b4-540">如果您指定的值為 hello *targetDedicatedComputeNodes*或*targetLowPriorityComputeNodes* hello 參數**CreatePool**方法，當您建立 hello評估 hello 自動調整公式時，會忽略在.NET 中，或另一種語言，則這些值中的 hello 比較參數集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-540">If you specified values for hello *targetDedicatedComputeNodes* or *targetLowPriorityComputeNodes* parameters of hello **CreatePool** method when you created hello pool in .NET, or for hello comparable parameters in another language, then those values are ignored when hello automatic scaling formula is evaluated.</span></span>
>
>

<span data-ttu-id="133b4-541">此 C# 程式碼片段會使用 hello[批次.NET] [ net_api]現有集區上的 [程式庫 tooenable 自動調整：</span><span class="sxs-lookup"><span data-stu-id="133b4-541">This C# code snippet uses hello [Batch .NET][net_api] library tooenable autoscaling on an existing pool:</span></span>

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a><span data-ttu-id="133b4-542">更新自動調整公式</span><span class="sxs-lookup"><span data-stu-id="133b4-542">Update an autoscale formula</span></span>

<span data-ttu-id="133b4-543">現有啟用自動調整集區上，呼叫 hello 作業 tooenable 自動調整一次與 hello 新公式 tooupdate hello 公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-543">tooupdate hello formula on an existing autoscale-enabled pool, call hello operation tooenable autoscaling again with hello new formula.</span></span> <span data-ttu-id="133b4-544">例如，如果已啟用自動調整`myexistingpool`hello 下列.NET 程式碼執行時，其自動調整公式會取代 hello 內容`myNewFormula`。</span><span class="sxs-lookup"><span data-stu-id="133b4-544">For example, if autoscaling is already enabled on `myexistingpool` when hello following .NET code is executed, its autoscale formula is replaced with hello contents of `myNewFormula`.</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a><span data-ttu-id="133b4-545">更新 hello 自動調整間隔</span><span class="sxs-lookup"><span data-stu-id="133b4-545">Update hello autoscale interval</span></span>

<span data-ttu-id="133b4-546">tooupdate hello 自動調整規模評估間隔的現有啟用自動調整集區，呼叫 hello 作業 tooenable 自動調整一次與 hello 新的間隔。</span><span class="sxs-lookup"><span data-stu-id="133b4-546">tooupdate hello autoscale evaluation interval of an existing autoscale-enabled pool, call hello operation tooenable autoscaling again with hello new interval.</span></span> <span data-ttu-id="133b4-547">例如，tooset hello 自動調整規模評估間隔 too60 分鐘數已在.NET 中啟用自動調整集區：</span><span class="sxs-lookup"><span data-stu-id="133b4-547">For example, tooset hello autoscale evaluation interval too60 minutes for a pool that's already autoscale-enabled in .NET:</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a><span data-ttu-id="133b4-548">評估自動調整公式</span><span class="sxs-lookup"><span data-stu-id="133b4-548">Evaluate an autoscale formula</span></span>

<span data-ttu-id="133b4-549">您可以評估公式之後才套用 tooa 集區。</span><span class="sxs-lookup"><span data-stu-id="133b4-549">You can evaluate a formula before applying it tooa pool.</span></span> <span data-ttu-id="133b4-550">如此一來，您可以測試 hello 公式 toosee hello 公式進入生產環境之前，其陳述式如何評估。</span><span class="sxs-lookup"><span data-stu-id="133b4-550">In this way, you can test hello formula toosee how its statements evaluate before you put hello formula into production.</span></span>

<span data-ttu-id="133b4-551">tooevaluate 自動調整公式，您必須先啟用 hello 與有效的公式的集區上的自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-551">tooevaluate an autoscale formula, you must first enable autoscaling on hello pool with a valid formula.</span></span> <span data-ttu-id="133b4-552">啟用 tootest 上還沒有自動調整集區的公式，使用 hello 一行公式`$TargetDedicatedNodes = 0`當您第一次啟用自動調整。</span><span class="sxs-lookup"><span data-stu-id="133b4-552">tootest a formula on a pool that doesn't yet have autoscaling enabled, use hello one-line formula `$TargetDedicatedNodes = 0` when you first enable autoscaling.</span></span> <span data-ttu-id="133b4-553">然後，使用其中一種 hello 下列想 tootest tooevaluate hello 公式：</span><span class="sxs-lookup"><span data-stu-id="133b4-553">Then, use one of hello following tooevaluate hello formula you want tootest:</span></span>

* <span data-ttu-id="133b4-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 或 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span><span class="sxs-lookup"><span data-stu-id="133b4-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) or [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span></span>

    <span data-ttu-id="133b4-555">這些批次.NET 方法需要現有的集區和包含 hello 自動調整公式 tooevaluate 字串 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="133b4-555">These Batch .NET methods require hello ID of an existing pool and a string containing hello autoscale formula tooevaluate.</span></span>

* [<span data-ttu-id="133b4-556">評估自動調整公式</span><span class="sxs-lookup"><span data-stu-id="133b4-556">Evaluate an automatic scaling formula</span></span>](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    <span data-ttu-id="133b4-557">在 REST API 要求中，指定在 hello URI 中的 hello 集區識別碼和 hello hello 中的自動調整公式*autoScaleFormula* hello 要求本文的元素。</span><span class="sxs-lookup"><span data-stu-id="133b4-557">In this REST API request, specify hello pool ID in hello URI, and hello autoscale formula in hello *autoScaleFormula* element of hello request body.</span></span> <span data-ttu-id="133b4-558">hello 回應 hello 作業包含可能是相關的 toohello 公式任何錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="133b4-558">hello response of hello operation contains any error information that might be related toohello formula.</span></span>

<span data-ttu-id="133b4-559">在這個 [Batch .NET][net_api] 程式碼片段中，我們會評估自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-559">In this [Batch .NET][net_api] code snippet, we evaluate an autoscale formula.</span></span> <span data-ttu-id="133b4-560">如果 hello 集區並沒有啟用自動調整，我們先將啟用它。</span><span class="sxs-lookup"><span data-stu-id="133b4-560">If hello pool does not have autoscaling enabled, we enable it first.</span></span>

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

<span data-ttu-id="133b4-561">成功評估 hello 這個程式碼片段所示的公式會產生類似的結果：</span><span class="sxs-lookup"><span data-stu-id="133b4-561">Successful evaluation of hello formula shown in this code snippet produces results similar to:</span></span>

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a><span data-ttu-id="133b4-562">取得自動調整執行的相關資訊</span><span class="sxs-lookup"><span data-stu-id="133b4-562">Get information about autoscale runs</span></span>

<span data-ttu-id="133b4-563">預期 tooensure 做為執行您的公式，我們建議您定期查看 hello hello 自動調整執行批次執行您的集區的結果。</span><span class="sxs-lookup"><span data-stu-id="133b4-563">tooensure that your formula is performing as expected, we recommend that you periodically check hello results of hello autoscaling runs that Batch performs on your pool.</span></span> <span data-ttu-id="133b4-564">toodo，get （或重新整理） 參考 toohello 集區，並檢查其執行的最後一個自動調整規模的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="133b4-564">toodo so, get (or refresh) a reference toohello pool, and examine hello properties of its last autoscale run.</span></span>

<span data-ttu-id="133b4-565">在批次.NET hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun)屬性具有可提供 hello 最新自動調整規模資訊 hello 集區執行執行數個屬性：</span><span class="sxs-lookup"><span data-stu-id="133b4-565">In Batch .NET, hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) property has several properties that provide information about hello latest automatic scaling run performed on hello pool:</span></span>

* [<span data-ttu-id="133b4-566">AutoScaleRun.Timestamp</span><span class="sxs-lookup"><span data-stu-id="133b4-566">AutoScaleRun.Timestamp</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [<span data-ttu-id="133b4-567">AutoScaleRun.Results</span><span class="sxs-lookup"><span data-stu-id="133b4-567">AutoScaleRun.Results</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [<span data-ttu-id="133b4-568">AutoScaleRun.Error</span><span class="sxs-lookup"><span data-stu-id="133b4-568">AutoScaleRun.Error</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

<span data-ttu-id="133b4-569">在 hello REST API，hello[取得集區的相關資訊](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool)要求傳回 hello 集區，其中包括 hello 最新自動縮放比例在 hello 中執行資訊的相關資訊[autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun)屬性。</span><span class="sxs-lookup"><span data-stu-id="133b4-569">In hello REST API, hello [Get information about a pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) request returns information about hello pool, which includes hello latest automatic scaling run information in hello [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) property.</span></span>

<span data-ttu-id="133b4-570">hello 下列 C# 程式碼片段會使用 hello 批次.NET 程式庫 tooprint 相關資訊 hello 最後一個自動調整集區執行_myPool_:</span><span class="sxs-lookup"><span data-stu-id="133b4-570">hello following C# code snippet uses hello Batch .NET library tooprint information about hello last autoscaling run on pool _myPool_:</span></span>

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

<span data-ttu-id="133b4-571">上述程式碼片段的 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="133b4-571">Sample output of hello preceding snippet:</span></span>

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

## <a name="example-autoscale-formulas"></a><span data-ttu-id="133b4-572">自動調整公式範例</span><span class="sxs-lookup"><span data-stu-id="133b4-572">Example autoscale formulas</span></span>
<span data-ttu-id="133b4-573">讓我們看看顯示不同的方式 tooadjust hello 數量的計算資源集區中的幾個公式。</span><span class="sxs-lookup"><span data-stu-id="133b4-573">Let's look at a few formulas that show different ways tooadjust hello amount of compute resources in a pool.</span></span>

### <a name="example-1-time-based-adjustment"></a><span data-ttu-id="133b4-574">範例 1：以時間為基礎的調整</span><span class="sxs-lookup"><span data-stu-id="133b4-574">Example 1: Time-based adjustment</span></span>
<span data-ttu-id="133b4-575">假設您想要根據 hello hello 週間日和時間 tooadjust hello 集區大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-575">Suppose you want tooadjust hello pool size based on hello day of hello week and time of day.</span></span> <span data-ttu-id="133b4-576">這個範例會示範如何 tooincrease 或減少 hello 中節點數目 hello 集據以區。</span><span class="sxs-lookup"><span data-stu-id="133b4-576">This example shows how tooincrease or decrease hello number of nodes in hello pool accordingly.</span></span>

<span data-ttu-id="133b4-577">hello 公式會先取得 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-577">hello formula first obtains hello current time.</span></span> <span data-ttu-id="133b4-578">如果它是一週工作日期 (1-5) 和工作小時內 (上午 8 點 too6 PM)，設定 too20 節點 hello 目標集區大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-578">If it's a weekday (1-5) and within working hours (8 AM too6 PM), hello target pool size is set too20 nodes.</span></span> <span data-ttu-id="133b4-579">否則，它已設定 too10 節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-579">Otherwise, it's set too10 nodes.</span></span>

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a><span data-ttu-id="133b4-580">範例 2：以工作為基礎的調整</span><span class="sxs-lookup"><span data-stu-id="133b4-580">Example 2: Task-based adjustment</span></span>
<span data-ttu-id="133b4-581">在此範例中，hello 集區大小是根據調整 hello hello 佇列中的工作數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-581">In this example, hello pool size is adjusted based on hello number of tasks in hello queue.</span></span> <span data-ttu-id="133b4-582">公式字串中接受註解和換行。</span><span class="sxs-lookup"><span data-stu-id="133b4-582">Both comments and line breaks are acceptable in formula strings.</span></span>

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a><span data-ttu-id="133b4-583">範例 3：考量平行工作</span><span class="sxs-lookup"><span data-stu-id="133b4-583">Example 3: Accounting for parallel tasks</span></span>
<span data-ttu-id="133b4-584">這個範例會調整 hello 工作數目為基礎的 hello 集區大小。</span><span class="sxs-lookup"><span data-stu-id="133b4-584">This example adjusts hello pool size based on hello number of tasks.</span></span> <span data-ttu-id="133b4-585">這個公式也會列入帳戶 hello [MaxTasksPerComputeNode] [ net_maxtasks] hello 集區已設定的值。</span><span class="sxs-lookup"><span data-stu-id="133b4-585">This formula also takes into account hello [MaxTasksPerComputeNode][net_maxtasks] value that has been set for hello pool.</span></span> <span data-ttu-id="133b4-586">已在集區上啟用[平行工作執行](batch-parallel-node-tasks.md)的情況下，這個方法很有用。</span><span class="sxs-lookup"><span data-stu-id="133b4-586">This approach is useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span></span>

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a><span data-ttu-id="133b4-587">範例 4：設定初始集區大小</span><span class="sxs-lookup"><span data-stu-id="133b4-587">Example 4: Setting an initial pool size</span></span>
<span data-ttu-id="133b4-588">此範例顯示 C# 程式碼片段，以設定自動調整公式 hello 集區大小 tooa 第一段時間針對指定節點的數目。</span><span class="sxs-lookup"><span data-stu-id="133b4-588">This example shows a C# code snippet with an autoscale formula that sets hello pool size tooa specified number of nodes for an initial time period.</span></span> <span data-ttu-id="133b4-589">然後它就會調整根據執行的 hello 數目 hello 集區的大小並經過 hello 初始時間週期之後，作用中工作。</span><span class="sxs-lookup"><span data-stu-id="133b4-589">Then it adjusts hello pool size based on hello number of running and active tasks after hello initial time period has elapsed.</span></span>

<span data-ttu-id="133b4-590">在下列程式碼片段的 hello hello 公式：</span><span class="sxs-lookup"><span data-stu-id="133b4-590">hello formula in hello following code snippet:</span></span>

* <span data-ttu-id="133b4-591">設定 hello 初始集區大小 toofour 節點。</span><span class="sxs-lookup"><span data-stu-id="133b4-591">Sets hello initial pool size toofour nodes.</span></span>
* <span data-ttu-id="133b4-592">不需要調整 hello 集區的大小內 hello hello 集區的生命週期的第一個 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="133b4-592">Does not adjust hello pool size within hello first 10 minutes of hello pool's lifecycle.</span></span>
* <span data-ttu-id="133b4-593">在 10 分鐘之後, 會取得 hello 最大值內 hello 工作執行的數字和作用中的 hello 過去 60 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-593">After 10 minutes, obtains hello max value of hello number of running and active tasks within hello past 60 minutes.</span></span>
  * <span data-ttu-id="133b4-594">如果這兩個值是 0 （表示中的任何工作已執行或作用中的 hello 過去的 60 分鐘），hello 集區大小是設定 too0。</span><span class="sxs-lookup"><span data-stu-id="133b4-594">If both values are 0 (indicating that no tasks were running or active in hello last 60 minutes), hello pool size is set too0.</span></span>
  * <span data-ttu-id="133b4-595">如果其中一個值大於零，則不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="133b4-595">If either value is greater than zero, no change is made.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="133b4-596">後續步驟</span><span class="sxs-lookup"><span data-stu-id="133b4-596">Next steps</span></span>
* <span data-ttu-id="133b4-597">[Azure Batch 計算資源使用率與並行節點工作最大化](batch-parallel-node-tasks.md)包含有關如何您可以執行多個工作同時在集區中的 hello 計算節點上的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="133b4-597">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on hello compute nodes in your pool.</span></span> <span data-ttu-id="133b4-598">此外 tooautoscaling，這項功能可能有助於 toolower 某些工作負載，節省您的工作持續時間。</span><span class="sxs-lookup"><span data-stu-id="133b4-598">In addition tooautoscaling, this feature may help toolower job duration for some workloads, saving you money.</span></span>
* <span data-ttu-id="133b4-599">另一個的效率提升器，請確定您的批次應用程式查詢 hello hello 大部分的最佳方式中的批次服務。</span><span class="sxs-lookup"><span data-stu-id="133b4-599">For another efficiency booster, ensure that your Batch application queries hello Batch service in hello most optimal way.</span></span> <span data-ttu-id="133b4-600">請參閱[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)toolearn toolimit hello 跨越 hello 網路時，查詢可能數千個 hello 狀態的資料數量如何計算節點或工作。</span><span class="sxs-lookup"><span data-stu-id="133b4-600">See [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) toolearn how toolimit hello amount of data that crosses hello wire when you query hello status of potentially thousands of compute nodes or tasks.</span></span>

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
