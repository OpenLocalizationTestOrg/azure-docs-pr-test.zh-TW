---
title: "在平行 toouse aaaRun 工作計算資源有效率地-Azure 批次 |Microsoft 文件"
description: "在 Azure Batch 集區中的每個節點上執行並行工作時，使用較少的運算節點以增加效率和降低成本"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="c0cee-103">Toomaximize 使用量的批次的運算節點同時執行工作</span><span class="sxs-lookup"><span data-stu-id="c0cee-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="c0cee-104">Azure Batch 集區中每個計算節點上同時執行多個工作，您可以最大化 hello 集區中的節點數目較少的資源使用量。</span><span class="sxs-lookup"><span data-stu-id="c0cee-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="c0cee-105">對於某些工作負載來說，這會產生縮短作業時間和降低成本的效益。</span><span class="sxs-lookup"><span data-stu-id="c0cee-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="c0cee-106">專用的所有節點的資源 tooa 單一工作都受益於某些情況下，雖然幾種情況而都獲益允許多個工作 tooshare 這些資源：</span><span class="sxs-lookup"><span data-stu-id="c0cee-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="c0cee-107">**最小化的資料傳輸**工作何時為可以 tooshare 資料。</span><span class="sxs-lookup"><span data-stu-id="c0cee-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="c0cee-108">在此案例中，您可以大幅降低資料傳輸費用複製共用的資料 tooa 較少的節點，並在每個節點上平行執行工作。</span><span class="sxs-lookup"><span data-stu-id="c0cee-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="c0cee-109">這特別適用於必須傳送 hello 資料 toobe 複製的 tooeach 節點之間的地理區域。</span><span class="sxs-lookup"><span data-stu-id="c0cee-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="c0cee-110">**最大化記憶體使用量** ，但是只有在短時間之內，以及在執行期間的變數時間。</span><span class="sxs-lookup"><span data-stu-id="c0cee-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="c0cee-111">您可以採用較少但較大，計算節點的更多的記憶體 tooefficiently 處理這類高峰流量。</span><span class="sxs-lookup"><span data-stu-id="c0cee-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="c0cee-112">這些節點會有多個工作，每個節點上，以平行方式執行，但每一項工作會利用 hello 節點充足的記憶體在不同的時間。</span><span class="sxs-lookup"><span data-stu-id="c0cee-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="c0cee-113">**緩和節點數目限制** 。</span><span class="sxs-lookup"><span data-stu-id="c0cee-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="c0cee-114">是目前的集區設定的節點間通訊限制的 too50 計算節點。</span><span class="sxs-lookup"><span data-stu-id="c0cee-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="c0cee-115">如果在集區中的每個節點可以 tooexecute 工作，以平行方式，可以同時執行大量的工作。</span><span class="sxs-lookup"><span data-stu-id="c0cee-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="c0cee-116">**複寫在內部部署計算叢集**，例如當您第一次移動運算環境 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c0cee-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="c0cee-117">如果您目前的內部部署解決方案執行每個計算節點的多個工作，您可以增加 hello 最大數目的節點工作 toomore 密切鏡像該組態。</span><span class="sxs-lookup"><span data-stu-id="c0cee-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="c0cee-118">範例案例</span><span class="sxs-lookup"><span data-stu-id="c0cee-118">Example scenario</span></span>
<span data-ttu-id="c0cee-119">做為範例 tooillustrate hello 平行工作執行的優點，假設您的工作應用程式的 CPU 和記憶體需求使[標準\_D1](../cloud-services/cloud-services-sizes-specs.md)節點已足夠。</span><span class="sxs-lookup"><span data-stu-id="c0cee-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="c0cee-120">但是，順序 toofinish hello 作業所需的 hello 時間中，這些節點的 1,000 所需。</span><span class="sxs-lookup"><span data-stu-id="c0cee-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="c0cee-121">如果不使用 Standard\_D1 節點 (具有 1 個 CPU 核心)，您可以採用具有 16 個核心的 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 節點，並啟用平行工作執行。</span><span class="sxs-lookup"><span data-stu-id="c0cee-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="c0cee-122">因此，不需使用 1000 個節點，而只需 63 個節點，用量「少了16 倍」  。</span><span class="sxs-lookup"><span data-stu-id="c0cee-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="c0cee-123">此外，如果大型應用程式的檔案或參考資料所需的每個節點，作業持續時間和效率會再次改進由於 hello 資料會複製的 tooonly 16 個節點。</span><span class="sxs-lookup"><span data-stu-id="c0cee-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="c0cee-124">啟用平行工作執行</span><span class="sxs-lookup"><span data-stu-id="c0cee-124">Enable parallel task execution</span></span>
<span data-ttu-id="c0cee-125">您可以設定平行工作執行的計算節點在 hello 集區層級。</span><span class="sxs-lookup"><span data-stu-id="c0cee-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="c0cee-126">Hello 批次.NET 程式庫，以設定 hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net]時建立集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="c0cee-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="c0cee-127">如果您使用 hello 批次 REST API，設定 hello [maxTasksPerNode] [ rest_addpool] hello 集區建立期間的要求主體中的項目。</span><span class="sxs-lookup"><span data-stu-id="c0cee-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="c0cee-128">Azure 批次，可讓您 tooset 最大的工作，每個節點組成 toofour 倍 (4 x) hello 節點核心數目。</span><span class="sxs-lookup"><span data-stu-id="c0cee-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="c0cee-129">例如，如果 hello 集區設定與節點的大小 「 大型 」 （四個核心），然後`maxTasksPerNode`設定 too16。</span><span class="sxs-lookup"><span data-stu-id="c0cee-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="c0cee-130">Hello 節點大小的每個核心的 hello 數目的詳細資訊，請參閱[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="c0cee-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="c0cee-131">如需服務限制的詳細資訊，請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="c0cee-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="c0cee-132">要確定 tootake 到帳戶 hello`maxTasksPerNode`值在建構時[自動調整公式][ enable_autoscaling]集區。</span><span class="sxs-lookup"><span data-stu-id="c0cee-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="c0cee-133">例如，評估 `$RunningTasks` 的公式可能大幅受到每個節點的工作增加的影響。</span><span class="sxs-lookup"><span data-stu-id="c0cee-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="c0cee-134">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的運算節點](batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="c0cee-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="c0cee-135">工作的分佈</span><span class="sxs-lookup"><span data-stu-id="c0cee-135">Distribution of tasks</span></span>
<span data-ttu-id="c0cee-136">集區中的 hello 計算節點可以同時執行的工作，很重要 toospecify hello 工作 toobe 跨 hello 集區中的 hello 節點散佈的方式。</span><span class="sxs-lookup"><span data-stu-id="c0cee-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="c0cee-137">使用 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule]屬性，您可以指定，工作應該平均指派給 hello 集區 （「 分配"） 中的所有節點。</span><span class="sxs-lookup"><span data-stu-id="c0cee-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="c0cee-138">或者，您可以指定，儘可能多的工作應該指派 tooeach 節點之前工作指派 tooanother 節點區內 hello （「 壓縮 」）。</span><span class="sxs-lookup"><span data-stu-id="c0cee-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="c0cee-139">做為範例的情況下，這項功能會很有價值的方式，請考慮 hello 集區[標準\_D14](../cloud-services/cloud-services-sizes-specs.md)節點 （在上述範例 hello） 以設定[CloudPool.MaxTasksPerComputeNode] [maxtasks_net]值為 16。</span><span class="sxs-lookup"><span data-stu-id="c0cee-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="c0cee-140">如果 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule]設有[ComputeNodeFillType] [ fill_type]的*組件*，它會最大化所有 16 個核心的每個節點的使用量，並允許[自動調整集區](batch-automatic-scaling.md)tooprune hello 集區 （而不指派任何工作的節點） 中未使用的節點。</span><span class="sxs-lookup"><span data-stu-id="c0cee-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="c0cee-141">這可最小化資源使用量和節省金錢。</span><span class="sxs-lookup"><span data-stu-id="c0cee-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="c0cee-142">Batch .NET 範例</span><span class="sxs-lookup"><span data-stu-id="c0cee-142">Batch .NET example</span></span>
<span data-ttu-id="c0cee-143">這[批次.NET] [ api_net]應用程式開發介面程式碼片段示範要求 toocreate 包含四項工作每個節點最多四個大型節點的集區。</span><span class="sxs-lookup"><span data-stu-id="c0cee-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="c0cee-144">它會指定工作排程將會填滿工作先前 tooassigning 工作 tooanother 節點區內 hello 與每個節點的原則。</span><span class="sxs-lookup"><span data-stu-id="c0cee-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="c0cee-145">如需有關使用 hello 批次.NET API 加入集區的詳細資訊，請參閱[BatchClient.PoolOperations.CreatePool][poolcreate_net]。</span><span class="sxs-lookup"><span data-stu-id="c0cee-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="c0cee-146">Batch REST 範例</span><span class="sxs-lookup"><span data-stu-id="c0cee-146">Batch REST example</span></span>
<span data-ttu-id="c0cee-147">這[批次 REST] [ api_rest]應用程式開發介面程式碼片段示範要求 toocreate 包含四項工作每個節點最多兩個大型節點的集區。</span><span class="sxs-lookup"><span data-stu-id="c0cee-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="c0cee-148">如需有關如何使用 REST API hello 加入集區的詳細資訊，請參閱[加入集區 tooan 帳戶][rest_addpool]。</span><span class="sxs-lookup"><span data-stu-id="c0cee-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="c0cee-149">您可以設定 hello`maxTasksPerNode`項目和[MaxTasksPerComputeNode] [ maxtasks_net]屬性只能在集區建立期間。</span><span class="sxs-lookup"><span data-stu-id="c0cee-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="c0cee-150">建立集區後無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="c0cee-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="c0cee-151">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c0cee-151">Code sample</span></span>
<span data-ttu-id="c0cee-152">hello [ParallelNodeTasks] [ parallel_tasks_sample] GitHub 上的專案說明 hello hello 使用[CloudPool.MaxTasksPerComputeNode] [ maxtasks_net]屬性。</span><span class="sxs-lookup"><span data-stu-id="c0cee-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="c0cee-153">此 C# 主控台應用程式使用 hello[批次.NET] [ api_net]文件庫 toocreate 具有一或多個集區計算節點。</span><span class="sxs-lookup"><span data-stu-id="c0cee-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="c0cee-154">它會執行那些節點 toosimulate 可變負載的可設定的工作數目。</span><span class="sxs-lookup"><span data-stu-id="c0cee-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="c0cee-155">Hello 應用程式的輸出指定的節點執行每項工作。</span><span class="sxs-lookup"><span data-stu-id="c0cee-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="c0cee-156">hello 應用程式也提供 hello 作業參數和持續時間的摘要。</span><span class="sxs-lookup"><span data-stu-id="c0cee-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="c0cee-157">hello hello 輸出 hello 範例應用程式的兩個不同的回合的部份摘要下方會出現。</span><span class="sxs-lookup"><span data-stu-id="c0cee-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="c0cee-158">hello hello 範例應用程式第一次執行顯示 hello 集區和 hello 預設值為每個節點，一項工作中的單一節點與 hello 作業持續時間為過去 30 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="c0cee-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="c0cee-159">第二次的 hello 範例會示範執行作業的持續時間大幅降低 hello。</span><span class="sxs-lookup"><span data-stu-id="c0cee-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="c0cee-160">這是因為 hello 集區設定中的每個節點，可讓平行工作執行 toocomplete hello 作業幾乎季 hello 時間的四項工作。</span><span class="sxs-lookup"><span data-stu-id="c0cee-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="c0cee-161">上述的 hello 摘要中的 hello 作業持續時間不包括集區建立時間。</span><span class="sxs-lookup"><span data-stu-id="c0cee-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="c0cee-162">Hello 工作上述的每個已送出的 toopreviously 建立集區的計算節點都在 hello*閒置*次送出狀態。</span><span class="sxs-lookup"><span data-stu-id="c0cee-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c0cee-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0cee-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="c0cee-164">Batch 總管熱圖</span><span class="sxs-lookup"><span data-stu-id="c0cee-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="c0cee-165">hello [Azure 批次總管][batch_explorer]，hello Azure 批次的其中一個[範例應用程式][github_samples]，包含*熱度圖*功能，可提供工作執行的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c0cee-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="c0cee-166">當您要執行 hello [ParallelTasks] [ parallel_tasks_sample]範例應用程式，您可以使用 hello 熱門地圖功能 tooeasily 視覺化 hello 平行的工作，每個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c0cee-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Batch 總管熱圖][1]

<span data-ttu-id="c0cee-168">*顯示包含四個節點的集區的Batch 總管熱圖，每個節點目前正在執行四個工作*</span><span class="sxs-lookup"><span data-stu-id="c0cee-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
