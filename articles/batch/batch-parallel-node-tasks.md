---
title: "平行執行工作以便有效率地使用計算資源 - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="a518d-103">並行執行工作以充分使用 Batch 計算節點</span><span class="sxs-lookup"><span data-stu-id="a518d-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="a518d-104">藉由在 Azure Batch 集區的每個計算模式同時執行一個以上的工作，您可以用較少的集中區節點將資源使用量最大化。</span><span class="sxs-lookup"><span data-stu-id="a518d-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="a518d-105">對於某些工作負載來說，這會產生縮短作業時間和降低成本的效益。</span><span class="sxs-lookup"><span data-stu-id="a518d-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="a518d-106">雖然某些案例受益於將節點的所有資源配置給單一工作，但是許多案例受益於允許多個工作共用這些資源：</span><span class="sxs-lookup"><span data-stu-id="a518d-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="a518d-107">**最小化資料傳輸** 。</span><span class="sxs-lookup"><span data-stu-id="a518d-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="a518d-108">在此案例中，您可以將共用資料複製到較少數量的節點，並在每個節點上平行執行工作，以大幅降低資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="a518d-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="a518d-109">此做法尤其適用於當要複製到每個節點的資料必須在地理區域之間傳輸時。</span><span class="sxs-lookup"><span data-stu-id="a518d-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="a518d-110">**最大化記憶體使用量** ，但是只有在短時間之內，以及在執行期間的變數時間。</span><span class="sxs-lookup"><span data-stu-id="a518d-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="a518d-111">您可以運用具有更多記憶體的較少但較大的計算節點，有效率地處理這類高峰流量。</span><span class="sxs-lookup"><span data-stu-id="a518d-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="a518d-112">這些節點會有在每個節點上執行的平行工作，但是每個工作會在不同的時間利用節點的大量記憶體。</span><span class="sxs-lookup"><span data-stu-id="a518d-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="a518d-113">**緩和節點數目限制** 。</span><span class="sxs-lookup"><span data-stu-id="a518d-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="a518d-114">目前，針對節點間通訊設定的集區限制為 50 個計算節點。</span><span class="sxs-lookup"><span data-stu-id="a518d-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="a518d-115">如果這類集區中的每個節點能夠以平行方式執行工作，則可以同時執行較多的工作。</span><span class="sxs-lookup"><span data-stu-id="a518d-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="a518d-116">**複寫內部部署計算叢集**，例如當您第一次將計算環境移至 Azure 時。</span><span class="sxs-lookup"><span data-stu-id="a518d-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="a518d-117">如果目前的內部部署解決方案在每個計算節點執行多個工作，您可以增加節點工作的數目上限，以更密切地反映該組態。</span><span class="sxs-lookup"><span data-stu-id="a518d-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="a518d-118">範例案例</span><span class="sxs-lookup"><span data-stu-id="a518d-118">Example scenario</span></span>
<span data-ttu-id="a518d-119">為了舉例說明平行工作執行的優點，讓我們假設您的工作應用程式 CPU 和記憶體需求的 [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) 節點大小是足夠的。</span><span class="sxs-lookup"><span data-stu-id="a518d-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="a518d-120">但是為了在要求的時間內完成作業，需要 1000 個這類節點。</span><span class="sxs-lookup"><span data-stu-id="a518d-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="a518d-121">如果不使用 Standard\_D1 節點 (具有 1 個 CPU 核心)，您可以採用具有 16 個核心的 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 節點，並啟用平行工作執行。</span><span class="sxs-lookup"><span data-stu-id="a518d-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="a518d-122">因此，不需使用 1000 個節點，而只需 63 個節點，用量「少了16 倍」  。</span><span class="sxs-lookup"><span data-stu-id="a518d-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="a518d-123">此外，由於資料只需複製到 16 個節點，如果每個節點都需要大型應用程式檔案或參考資料，那麼作業持續時間和效率均能再次獲得改善。</span><span class="sxs-lookup"><span data-stu-id="a518d-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="a518d-124">啟用平行工作執行</span><span class="sxs-lookup"><span data-stu-id="a518d-124">Enable parallel task execution</span></span>
<span data-ttu-id="a518d-125">您可以針對集區層級的平行工作執行，設定計算節點。</span><span class="sxs-lookup"><span data-stu-id="a518d-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="a518d-126">使用 Batch .NET 程式庫時，請在建立集區時設定 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 屬性。</span><span class="sxs-lookup"><span data-stu-id="a518d-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="a518d-127">如果您使用 Batch REST API，請在集區建立期間於要求本文中設定 [maxTasksPerNode][rest_addpool] 元素。</span><span class="sxs-lookup"><span data-stu-id="a518d-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="a518d-128">Azure Batch 允許您將每個節點的最大工作數目設定為多達節點核心數目的 4 倍 (4x)。</span><span class="sxs-lookup"><span data-stu-id="a518d-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="a518d-129">例如，如果集區設定的節點大小為 [大] \(四個核心)，則 `maxTasksPerNode` 可以設定為 16。</span><span class="sxs-lookup"><span data-stu-id="a518d-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="a518d-130">如需每個節點大小的核心數目的詳細資料，請參閱 [雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="a518d-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="a518d-131">如需服務限制的詳細資訊，請參閱 [Azure Batch 服務的配額和限制](batch-quota-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="a518d-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="a518d-132">為您的集區建構[自動調整公式][enable_autoscaling]時，請務必考慮 `maxTasksPerNode` 值。</span><span class="sxs-lookup"><span data-stu-id="a518d-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="a518d-133">例如，評估 `$RunningTasks` 的公式可能大幅受到每個節點的工作增加的影響。</span><span class="sxs-lookup"><span data-stu-id="a518d-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="a518d-134">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的運算節點](batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="a518d-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="a518d-135">工作的分佈</span><span class="sxs-lookup"><span data-stu-id="a518d-135">Distribution of tasks</span></span>
<span data-ttu-id="a518d-136">在集區內的計算節點能夠同時執行工作時，請務必指定您希望在集區內進行跨節點分佈工作的方式。</span><span class="sxs-lookup"><span data-stu-id="a518d-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="a518d-137">使用 [CloudPool.TaskSchedulingPolicy][task_schedule] 屬性，您可以指定工作應該跨集區中的所有節點平均指派 (「散佈」)。</span><span class="sxs-lookup"><span data-stu-id="a518d-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="a518d-138">或者，您可以在工作指派到集區中其他節點之前，盡可能將最多工作指派給每個節點 (「封裝」)。</span><span class="sxs-lookup"><span data-stu-id="a518d-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="a518d-139">做為這項功能有何重要的範例，請考慮上述範例中 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 節點的集區，以 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 的值 16 進行設定。</span><span class="sxs-lookup"><span data-stu-id="a518d-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="a518d-140">如果 [CloudPool.TaskSchedulingPolicy][task_schedule] 以 [ComputeNodeFillType][fill_type] 為 *Pack* 進行設定，它會最大化每個節點全部 16 個核心的使用量，並且允許[自動調整集區](batch-automatic-scaling.md)從集區剪除未使用的節點 (未指派任何工作的節點)。</span><span class="sxs-lookup"><span data-stu-id="a518d-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="a518d-141">這可最小化資源使用量和節省金錢。</span><span class="sxs-lookup"><span data-stu-id="a518d-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="a518d-142">Batch .NET 範例</span><span class="sxs-lookup"><span data-stu-id="a518d-142">Batch .NET example</span></span>
<span data-ttu-id="a518d-143">這個 [Batch .NET][api_net] API 程式碼片段示範建立集區的要求，該集區包含四個大型節點，而每個節點最多有四項工作。</span><span class="sxs-lookup"><span data-stu-id="a518d-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="a518d-144">它會指定工作排程原則，該原則會先以工作填滿每個節點，再將工作指派給集區中的其他節點。</span><span class="sxs-lookup"><span data-stu-id="a518d-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="a518d-145">如需有關使用 Batch .NET API 新增集區的詳細資訊，請參閱 [BatchClient.PoolOperations.CreatePool][poolcreate_net]。</span><span class="sxs-lookup"><span data-stu-id="a518d-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="a518d-146">Batch REST 範例</span><span class="sxs-lookup"><span data-stu-id="a518d-146">Batch REST example</span></span>
<span data-ttu-id="a518d-147">這個 [Batch REST][api_rest] API 程式碼片段示範建立集區的要求，該集區包含兩個大型節點，而每個節點最多有四項工作。</span><span class="sxs-lookup"><span data-stu-id="a518d-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="a518d-148">如需有關如何使用 REST API 新增集區的詳細資訊，請參閱[將集區新增至帳戶][rest_addpool]。</span><span class="sxs-lookup"><span data-stu-id="a518d-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="a518d-149">您只能在建立集區時設定 `maxTasksPerNode` 元素和 [MaxTasksPerComputeNode][maxtasks_net] 屬性。</span><span class="sxs-lookup"><span data-stu-id="a518d-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="a518d-150">建立集區後無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="a518d-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="a518d-151">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a518d-151">Code sample</span></span>
<span data-ttu-id="a518d-152">GitHub 上的 [ParallelNodeTasks][parallel_tasks_sample] 專案提供使用 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 屬性的說明。</span><span class="sxs-lookup"><span data-stu-id="a518d-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="a518d-153">這個 C# 主控台應用程式使用 [Batch .NET][api_net] 程式庫來建立具有一或多個計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="a518d-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="a518d-154">它會在這些節點上執行可設定數目的工作，以模擬可變負載。</span><span class="sxs-lookup"><span data-stu-id="a518d-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="a518d-155">應用程式的輸出會指定哪些節點執行每個工作。</span><span class="sxs-lookup"><span data-stu-id="a518d-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="a518d-156">此應用程式也會提供作業參數和持續時間的摘要。</span><span class="sxs-lookup"><span data-stu-id="a518d-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="a518d-157">兩個不同的範例應用程式執行的輸出摘要部分會在下方顯示。</span><span class="sxs-lookup"><span data-stu-id="a518d-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="a518d-158">首次執行範例應用程式會顯示該部分與集區中的單一節點，以及每個節點一項作業的預設設定，作業持續時間超過 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a518d-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="a518d-159">第二次執行範例會顯示作業持續時間大幅降低。</span><span class="sxs-lookup"><span data-stu-id="a518d-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="a518d-160">這是因為集區已設定為每個節點四項工作，可允許平行工作執行以在近一季的時間完成作業。</span><span class="sxs-lookup"><span data-stu-id="a518d-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="a518d-161">在上述摘要中的作業持續時間不包括集區建立時間。</span><span class="sxs-lookup"><span data-stu-id="a518d-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="a518d-162">上述的每個作業已提交至先前建立的集區，其運算節點在提交時間處於 [閒置]  狀態。</span><span class="sxs-lookup"><span data-stu-id="a518d-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a518d-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a518d-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="a518d-164">Batch 總管熱圖</span><span class="sxs-lookup"><span data-stu-id="a518d-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="a518d-165">[Azure Batch 總管][batch_explorer]包含「熱圖」功能，是 Azure Batch 的其中一個[範例應用程式][github_samples]，提供工作執行的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="a518d-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="a518d-166">執行 [ParallelTasks][parallel_tasks_sample] 範例應用程式時，您可以使用熱圖功能輕易地視覺化每個節點上的平行工作執行。</span><span class="sxs-lookup"><span data-stu-id="a518d-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Batch 總管熱圖][1]

<span data-ttu-id="a518d-168">*顯示包含四個節點的集區的Batch 總管熱圖，每個節點目前正在執行四個工作*</span><span class="sxs-lookup"><span data-stu-id="a518d-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
