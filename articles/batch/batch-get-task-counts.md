---
title: "作業的進度，來計算工作的狀態-Azure 批次的 aaaMonitor |Microsoft 文件"
description: "藉由工作呼叫 hello 取得工作計數作業 toocount 工作監視 hello 作業的進度。 您可以取得作用中、執行中和已完成工作的計數，並依照成功或失敗的工作計算。"
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a><span data-ttu-id="8e5e4-104">計數工作狀態 toomonitor 作業的進度 （預覽）</span><span class="sxs-lookup"><span data-stu-id="8e5e4-104">Count tasks by state toomonitor a job's progress (Preview)</span></span>

<span data-ttu-id="8e5e4-105">Azure 批次提供有效率的方式 toomonitor hello 工作的進度，執行其工作。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-105">Azure Batch provides an efficient way toomonitor hello progress of a job as it runs its tasks.</span></span> <span data-ttu-id="8e5e4-106">您可以呼叫 hello[取得工作計數][ rest_get_task_counts]出多少工作處於作用中、 執行中或已完成狀態，以及有多少作業 toofind 成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-106">You can call hello [Get Task Counts][rest_get_task_counts] operation toofind out how many tasks are in an active, running, or completed state, and how many have succeeded or failed.</span></span> <span data-ttu-id="8e5e4-107">透過計算 hello 數項工作中每個狀態，您可以更輕鬆地顯示 hello 作業的進度 tooa 使用者，或偵測到未預期的延遲或可能會影響 hello 作業失敗。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-107">By counting hello number of tasks in each state, you can more easily display hello job's progress tooa user, or detect unexpected delays or failures that may affect hello job.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e5e4-108">hello 取得工作計數作業目前為預覽狀態，和尚無法使用 Azure 政府、 Azure China 和 Azure 德國中。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-108">hello Get Task Counts operation is currently in preview, and is not yet available in Azure Government, Azure China, and Azure Germany.</span></span> 
>
>

## <a name="how-tasks-are-counted"></a><span data-ttu-id="8e5e4-109">工作的計算方式</span><span class="sxs-lookup"><span data-stu-id="8e5e4-109">How tasks are counted</span></span>

<span data-ttu-id="8e5e4-110">hello 取得工作計數作業會依照狀態、 工作計算，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8e5e4-110">hello Get Task Counts operation counts tasks by state, as follows:</span></span>

- <span data-ttu-id="8e5e4-111">工作會計算為**active**當它排入佇列，而且要能 toorun，但目前尚未指派 tooa 計算節點。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-111">A task is counted as **active** when it is queued and able toorun, but is not currently assigned tooa compute node.</span></span> <span data-ttu-id="8e5e4-112">如果工作相依於尚未完成的父工作，也會算作是**作用中**的工作。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-112">A task is also counted as **active** if it is dependent on a parent task that has not yet completed.</span></span> <span data-ttu-id="8e5e4-113">如需有關工作相依性的詳細資訊，請參閱[toorun 工作相依於其他工作建立工作的相依性](batch-task-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-113">For more information on task dependencies, see [Create task dependencies toorun tasks that depend on other tasks](batch-task-dependencies.md).</span></span> 
- <span data-ttu-id="8e5e4-114">工作會計算為**執行**當它已被指派 tooa 計算節點，但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-114">A task is counted as **running** when it has been assigned tooa compute node, but has not yet completed.</span></span> <span data-ttu-id="8e5e4-115">工作會計算為**執行**當其狀態是`preparing`或`running`、 由 hello[取得工作的相關資訊][ rest_get_task]作業。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-115">A task is counted as **running** when its state is either `preparing` or `running`, as indicated by hello [Get information about a task][rest_get_task] operation.</span></span>
- <span data-ttu-id="8e5e4-116">工作會計算為**完成**時不會再合格 toorun。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-116">A task is counted as **completed** when it is no longer eligible toorun.</span></span> <span data-ttu-id="8e5e4-117">算作是**已完成**的工作通常已順利完成，或未順利完成且也已達到其重試限制。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-117">A task counted as **completed** has typically either finished successfully, or has finished unsuccessfully and has also exhausted its retry limit.</span></span> 

<span data-ttu-id="8e5e4-118">hello 取得工作計數作業也會報告多少工作已成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-118">hello Get Task Counts operation also reports how many tasks have succeeded or failed.</span></span> <span data-ttu-id="8e5e4-119">批次判斷工作是否成功或失敗藉由檢查 hello**結果**hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] 屬性屬性：</span><span class="sxs-lookup"><span data-stu-id="8e5e4-119">Batch determines whether a task has succeeded or failed by checking hello **result** property of hello [executionInfo][https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] property:</span></span>

    - <span data-ttu-id="8e5e4-120">工作會計算為**成功**如果 hello 工作執行結果為`success`。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-120">A task is counted as **succeeded** if hello result of task execution is `success`.</span></span>
    - <span data-ttu-id="8e5e4-121">工作會計算為**失敗**如果 hello 工作執行結果為`failure`。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-121">A task is counted as **failed** if hello result of task execution is `failure`.</span></span>

<span data-ttu-id="8e5e4-122">如需工作狀態的詳細資訊，請參閱[取得工作相關資訊][rest_get_task]。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-122">For more information about task states, see [Get information about a task][rest_get_task].</span></span>

<span data-ttu-id="8e5e4-123">hello 下列.NET 程式碼範例示範如何 tooretrieve 工作計算的狀態：</span><span class="sxs-lookup"><span data-stu-id="8e5e4-123">hello following .NET code sample shows how tooretrieve task counts by state:</span></span> 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> <span data-ttu-id="8e5e4-124">您可以使用其他類似的模式和 tooget 工作會計算作業的其他支援的語言。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-124">You can use a similar pattern for REST and other supported languages tooget task counts for a job.</span></span> 
> 
> 

## <a name="consistency-checking-for-task-counts"></a><span data-ttu-id="8e5e4-125">工作計數的一致性檢查</span><span class="sxs-lookup"><span data-stu-id="8e5e4-125">Consistency checking for task counts</span></span>

<span data-ttu-id="8e5e4-126">hello 批次服務彙總工作計數，從非同步分散式系統的多個部分收集資料。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-126">hello Batch service aggregates task counts by gathering data from multiple parts of an asynchronous distributed system.</span></span> <span data-ttu-id="8e5e4-127">工作計數的 tooensure 正確無誤，批次的計數執行一致性檢查針對 hello 系統的多個元件的狀態，提供額外的驗證。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-127">tooensure that task counts are correct, Batch provides additional validation for state counts by performing consistency checks against multiple components of hello system.</span></span> <span data-ttu-id="8e5e4-128">只要 hello 作業中有超過 200,000 工作批次會執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-128">Batch performs these consistency checks as long as there are fewer than 200,000 tasks in hello job.</span></span> <span data-ttu-id="8e5e4-129">在 hello 罕見事件中 hello 一致性檢查，會找到錯誤，批次更正 hello 作業結果的 hello 取得工作計數根據 hello 的 hello 一致性檢查的結果。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-129">In hello unlikely event that hello consistency check finds errors, Batch corrects hello result of hello Get Tasks Counts operation based on hello results of hello consistency check.</span></span> <span data-ttu-id="8e5e4-130">hello 一致性檢查是客戶依賴 hello 取得工作計數作業取得 hello 正確的資訊，這些方案需要額外的量值 tooensure。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-130">hello consistency check is an extra measure tooensure that customers who rely on hello Get Task Counts operation get hello right information they need for their solution.</span></span>

<span data-ttu-id="8e5e4-131">hello **validationStatus** hello 回應中的屬性會指出批次是否執行 hello 一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-131">hello **validationStatus** property in hello response indicates whether Batch has performed hello consistency check.</span></span> <span data-ttu-id="8e5e4-132">如果批次尚未針對 hello hello 系統中保留的實際狀態可以 toocheck 狀態計數，然後 hello **validationStatus**屬性設定太`unvalidated`。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-132">If Batch has not been able toocheck state counts against hello actual states held in hello system, then hello **validationStatus** property is set too`unvalidated`.</span></span> <span data-ttu-id="8e5e4-133">基於效能考量，批次將不會執行 hello 一致性檢查，如果 hello 工作包含超過 200,000 」 工作，因此 hello **validationStatus**屬性可能設定太`unvalidated`在此情況下。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-133">For performance reasons, Batch will not perform hello consistency check if hello job includes more than 200,000 tasks, so hello **validationStatus** property may be set too`unvalidated` in this case.</span></span> <span data-ttu-id="8e5e4-134">不過，hello 工作計數不一定是錯誤在此情況下，因為即使非常有限的資料遺失就會不太可能。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-134">However, hello task count is not necessarily wrong in this case, as even a very limited data loss is highly unlikely.</span></span> 

<span data-ttu-id="8e5e4-135">當工作變更狀態時，hello 彙總管線會處理 hello 變更幾秒鐘內。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-135">When a task changes state, hello aggregation pipeline processes hello change within few seconds.</span></span> <span data-ttu-id="8e5e4-136">hello 取得工作計數的作業會反映在該期間內的 hello 更新工作計數。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-136">hello Get Task Counts operation reflects hello updated task counts within that period.</span></span> <span data-ttu-id="8e5e4-137">不過，hello 彙總管線遺漏工作狀態的變更，然後變更不被註冊直到 hello 下驗證階段。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-137">However, if hello aggregation pipeline misses a change in a task state, then that change is not registered until hello next validation pass.</span></span> <span data-ttu-id="8e5e4-138">在此期間，工作計數可能稍微不正確，因為 toohello 遺失的事件，但它們在下一步 驗證階段 hello 更正。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-138">During this time, task counts may be slightly inaccurate due toohello missed event, but they are corrected on hello next validation pass.</span></span>

## <a name="best-practices-for-counting-a-jobs-tasks"></a><span data-ttu-id="8e5e4-139">計算作業之工作的最佳做法</span><span class="sxs-lookup"><span data-stu-id="8e5e4-139">Best practices for counting a job's tasks</span></span>

<span data-ttu-id="8e5e4-140">呼叫 hello 取得工作計數作業，是最有效率的方式 tooreturn hello 基本作業的工作狀態的計數。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-140">Calling hello Get Task Counts operation is hello most efficient way tooreturn a basic count of a job's tasks by state.</span></span> <span data-ttu-id="8e5e4-141">如果您使用批次服務版本 2017年-06-01.5.1，則建議您撰寫或更新您的程式碼 toouse 取得工作計數。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-141">If you are using Batch service version 2017-06-01.5.1, we recommend writing or updating your code toouse Get Task Counts.</span></span>

<span data-ttu-id="8e5e4-142">hello 取得工作計數作業不適用於批次服務版本早於 2017年-06-01.5.1。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-142">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="8e5e4-143">如果您使用較舊版本的 hello 服務，然後改用清單查詢 toocount 工作中的工作。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-143">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span> <span data-ttu-id="8e5e4-144">如需詳細資訊，請參閱[有效率地建立查詢 toolist 批次資源](batch-efficient-list-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-144">For more information, see [Create queries toolist Batch resources efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e5e4-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e5e4-145">Next steps</span></span>

* <span data-ttu-id="8e5e4-146">請參閱 hello[批次功能概觀](batch-api-basics.md)toolearn 更多關於批次服務概念和功能。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-146">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="8e5e4-147">hello 文章討論 hello 主要批次資源集區、 計算節點、 工作和工作，例如，並提供 hello 服務功能的概觀。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-147">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features.</span></span>
* <span data-ttu-id="8e5e4-148">了解 hello 基本概念的開發批次啟用應用程式使用 hello[批次.NET 用戶端程式庫](batch-dotnet-get-started.md)或[Python](batch-python-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-148">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="8e5e4-149">這些入門文件引導您完成使用 hello 批次服務 tooexecute 的工作應用程式工作負載在多個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="8e5e4-149">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes.</span></span>


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
