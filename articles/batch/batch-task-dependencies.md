---
title: "使用工作相依性以便在其他工作完成時執行工作 - Azure Batch | Microsoft Docs"
description: "建立相依於其他工作完成的工作，以便在 Azure Batch 中處理 MapReduce 樣式和類似的巨量資料工作負載。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="57bd1-103">建立工作相依性，以便執行相依於其他工作的工作</span><span class="sxs-lookup"><span data-stu-id="57bd1-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="57bd1-104">您可以定義工作相依性，只有在父系工作完成後才執行一項工作或一組工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="57bd1-105">一些實用的工作相依性案例包括︰</span><span class="sxs-lookup"><span data-stu-id="57bd1-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="57bd1-106">雲端中的 MapReduce 樣式工作負載。</span><span class="sxs-lookup"><span data-stu-id="57bd1-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="57bd1-107">資料處理工作可表示為有向非循環圖 (DAG) 的工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="57bd1-108">轉譯前和轉譯後程序，其中的每項工作必須在下一項工作開始前完成。</span><span class="sxs-lookup"><span data-stu-id="57bd1-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="57bd1-109">下游工作相依於上游工作輸出的任何其他工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="57bd1-110">您可以利用 Batch 工作相依性，建立排定於一或多項父系工作完成後，才在計算節點上執行的工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="57bd1-111">例如，您可以建立一個將 3D 電影的每個影格以個別、平行工作轉譯的工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="57bd1-112">在成功轉譯所有影格之後，最終工作「合併工作」會將轉譯的影格合併為一部完整的電影。</span><span class="sxs-lookup"><span data-stu-id="57bd1-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="57bd1-113">根據預設，相依工作會排定只會在父系工作順利完成之後執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="57bd1-114">您可以指定相依性動作，以覆寫預設行為，並且在父系工作失敗時執行工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="57bd1-115">如需詳細資訊，請參閱[相依性動作](#dependency-actions)一節。</span><span class="sxs-lookup"><span data-stu-id="57bd1-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="57bd1-116">您可以在一對一或一對多的關係中建立相依於其他工作的工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="57bd1-117">您也可以建立一個範圍相依性，其中的工作相依於在指定的工作識別碼範圍內完成的一組工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="57bd1-118">您可以結合這三種基本案例來建立多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="57bd1-119">Batch .NET 的工作相依性</span><span class="sxs-lookup"><span data-stu-id="57bd1-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="57bd1-120">在本文中，我們會討論如何使用 [Batch .NET][net_msdn] 程式庫設定工作相依性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="57bd1-121">我們會先告訴您如何對作業[啟用工作相依性](#enable-task-dependencies)，然後再示範如何[設定工作的相依性](#create-dependent-tasks)。</span><span class="sxs-lookup"><span data-stu-id="57bd1-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="57bd1-122">我們也說明如何指定相依性動作，以便在父系失敗時執行相依工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="57bd1-123">最後，我們將討論 Batch 支援的 [相依性案例](#dependency-scenarios) 。</span><span class="sxs-lookup"><span data-stu-id="57bd1-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="57bd1-124">啟用工作相依性</span><span class="sxs-lookup"><span data-stu-id="57bd1-124">Enable task dependencies</span></span>
<span data-ttu-id="57bd1-125">若要在 Batch 應用程式中使用工作相依性，您必須先將作業設定成使用工作相依性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="57bd1-126">在 Batch .NET 中，將作業的 [UsesTaskDependencies][net_usestaskdependencies] 屬性設定為 `true`，以對 [CloudJob][net_cloudjob] 啟用工作相依性：</span><span class="sxs-lookup"><span data-stu-id="57bd1-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="57bd1-127">在上述程式碼片段中，"batchClient" 是 [BatchClient][net_batchclient] 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="57bd1-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="57bd1-128">建立相依的工作</span><span class="sxs-lookup"><span data-stu-id="57bd1-128">Create dependent tasks</span></span>
<span data-ttu-id="57bd1-129">若要建立相依於一或多個父系工作完成的工作，您可以指定此工作「相依於」其他工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="57bd1-130">在 Batch .NET 中，在 [TaskDependencies][net_taskdependencies] 類別的執行個體上設定 [CloudTask][net_cloudtask].[DependsOn][net_dependson] 屬性︰</span><span class="sxs-lookup"><span data-stu-id="57bd1-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="57bd1-131">此程式碼片段會使用工作識別碼 "Flowers" 建立相依工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="57bd1-132">"Flowers" 工作相依於 "Rain" 和 "Sun" 工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="57bd1-133">"Flowers" 工作將排定為只會在 "Rain" 和 "Sun" 工作順利完成後，才於計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="57bd1-134">當工作處於**已完成**狀態且其**結束代碼** 是 `0` 時，才會將其視為已順利完成。</span><span class="sxs-lookup"><span data-stu-id="57bd1-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="57bd1-135">在 Batch .NET 中，這表示 [CloudTask][net_cloudtask].[State][net_taskstate] 屬性值為 `Completed`，而 CloudTask 的 [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] 屬性值為 `0`。</span><span class="sxs-lookup"><span data-stu-id="57bd1-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="57bd1-136">相依性案例</span><span class="sxs-lookup"><span data-stu-id="57bd1-136">Dependency scenarios</span></span>
<span data-ttu-id="57bd1-137">Azure Batch 中可使用的基本工作相依性案例有三種︰一對一、一對多、工作識別碼範圍相依性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="57bd1-138">結合這三種案例即可提供第四種案例，也就是多對多。</span><span class="sxs-lookup"><span data-stu-id="57bd1-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="57bd1-139">案例&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="57bd1-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="57bd1-140">範例</span><span class="sxs-lookup"><span data-stu-id="57bd1-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="57bd1-141">一對一</span><span class="sxs-lookup"><span data-stu-id="57bd1-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="57bd1-142">「taskB」相依於「taskA」</span><span class="sxs-lookup"><span data-stu-id="57bd1-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="57bd1-143">「taskB」要等到「taskA」順利完成後，才會排定執行</span><span class="sxs-lookup"><span data-stu-id="57bd1-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="57bd1-144">![圖表︰一對一工作相依性][1]</span><span class="sxs-lookup"><span data-stu-id="57bd1-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="57bd1-145">一對多</span><span class="sxs-lookup"><span data-stu-id="57bd1-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="57bd1-146">「taskC」同時相依於「taskA」和「taskB」</span><span class="sxs-lookup"><span data-stu-id="57bd1-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="57bd1-147">「taskC」要等到「taskA」和「taskB」順利完成後，才會排定執行</span><span class="sxs-lookup"><span data-stu-id="57bd1-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="57bd1-148">![圖表︰一對多工作相依性][2]</span><span class="sxs-lookup"><span data-stu-id="57bd1-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="57bd1-149">工作識別碼範圍</span><span class="sxs-lookup"><span data-stu-id="57bd1-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="57bd1-150">「taskD」相依於某一範圍的工作</span><span class="sxs-lookup"><span data-stu-id="57bd1-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="57bd1-151">「taskD」要等到識別碼「1」到「10」的工作順利完成後，才會排定執行</span><span class="sxs-lookup"><span data-stu-id="57bd1-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="57bd1-152">![圖表︰工作識別碼範圍相依性][3]</span><span class="sxs-lookup"><span data-stu-id="57bd1-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="57bd1-153">您可以建立**多對多**關聯性，例如工作 C、D、E 和 F 均相依於工作 A 和 B。舉例來說，在下游工作相依於多個上游工作輸出的平行前置處理案例中，這種關聯性就很有用。</span><span class="sxs-lookup"><span data-stu-id="57bd1-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="57bd1-154">在本節的範例中，相依工作只會在父系工作順利完成之後才執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="57bd1-155">這種行為是相依工作的預設行為。</span><span class="sxs-lookup"><span data-stu-id="57bd1-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="57bd1-156">指定相依性動作來覆寫預設行為，即可在父系工作失敗時執行相依工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="57bd1-157">如需詳細資訊，請參閱[相依性動作](#dependency-actions)一節。</span><span class="sxs-lookup"><span data-stu-id="57bd1-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="57bd1-158">一對一</span><span class="sxs-lookup"><span data-stu-id="57bd1-158">One-to-one</span></span>
<span data-ttu-id="57bd1-159">在一對一關聯性中，工作相依於一項父系工作的成功完成。</span><span class="sxs-lookup"><span data-stu-id="57bd1-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="57bd1-160">若要建立相依性，請在填入 [CloudTask][net_cloudtask] 的 [DependsOn][net_dependson] 屬性時，對 [TaskDependencies][net_taskdependencies].[OnId][net_onid] 靜態方法提供單一工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="57bd1-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="57bd1-161">一對多</span><span class="sxs-lookup"><span data-stu-id="57bd1-161">One-to-many</span></span>
<span data-ttu-id="57bd1-162">在一對多關聯性中，工作相依於多項父工作的完成。</span><span class="sxs-lookup"><span data-stu-id="57bd1-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="57bd1-163">若要建立相依性，請在填入 [CloudTask][net_cloudtask] 的 [DependsOn][net_dependson] 屬性時，對 [TaskDependencies][net_taskdependencies].[OnId][net_onids] 靜態方法提供工作識別碼集合。</span><span class="sxs-lookup"><span data-stu-id="57bd1-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="57bd1-164">工作識別碼範圍</span><span class="sxs-lookup"><span data-stu-id="57bd1-164">Task ID range</span></span>
<span data-ttu-id="57bd1-165">在父系工作範圍的相依性中，工作相依於識別碼落在範圍內之工作的完成。</span><span class="sxs-lookup"><span data-stu-id="57bd1-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="57bd1-166">若要建立相依性，請在填入 [CloudTask][net_cloudtask] 的 [DependsOn][net_dependson] 屬性時，對 [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] 靜態方法提供範圍中的第一個和最後一個工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="57bd1-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57bd1-167">當您針對相依性使用工作識別碼範圍時，該範圍內的工作識別碼「必須」是以字串表示的整數值。</span><span class="sxs-lookup"><span data-stu-id="57bd1-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="57bd1-168">範圍中的每項工作必須藉由下列方式來符合相依性：順利完成，或完成但對應至相依性動作的錯誤設定為 [符合]。</span><span class="sxs-lookup"><span data-stu-id="57bd1-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="57bd1-169">如需詳細資訊，請參閱[相依性動作](#dependency-actions)一節。</span><span class="sxs-lookup"><span data-stu-id="57bd1-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="57bd1-170">相依性動作</span><span class="sxs-lookup"><span data-stu-id="57bd1-170">Dependency actions</span></span>

<span data-ttu-id="57bd1-171">根據預設，只有在父系工作順利完成後，才會執行一項工作或一組工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="57bd1-172">在某些情況下，即使父系工作失敗，您也想要執行相依工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="57bd1-173">您可以指定相依性動作，以覆寫預設行為。</span><span class="sxs-lookup"><span data-stu-id="57bd1-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="57bd1-174">相依性動作會根據父系工作成功或失敗，指定相依工作是否有資格執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="57bd1-175">例如，假設相依工作正在等候上游工作完成的資料。</span><span class="sxs-lookup"><span data-stu-id="57bd1-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="57bd1-176">如果上游工作失敗，相依工作仍然可以使用較舊的資料來執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="57bd1-177">在此情況下，儘管父系工作失敗，相依性動作仍可指定相依工作是否有資格執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="57bd1-178">相依性動作是以父系工作的結束情況為基礎。</span><span class="sxs-lookup"><span data-stu-id="57bd1-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="57bd1-179">您可以指定下列任何一種結束情況的相依性動作；若為 .NET，請參閱 [ExitConditions][net_exitconditions] 類別，以取得詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="57bd1-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="57bd1-180">發生前置處理錯誤時。</span><span class="sxs-lookup"><span data-stu-id="57bd1-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="57bd1-181">發生檔案上傳錯誤時。</span><span class="sxs-lookup"><span data-stu-id="57bd1-181">When a file upload error occurs.</span></span> <span data-ttu-id="57bd1-182">如果工作結束時的結束代碼是透過 **exitCodes** 或 **exitCodeRanges** 所指定，又發生檔案上傳錯誤，則優先執行結束代碼指定的動作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="57bd1-183">工作結束時的結束代碼是由 **ExitCodes** 屬性所定義。</span><span class="sxs-lookup"><span data-stu-id="57bd1-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="57bd1-184">工作結束時的結束代碼落在 **ExitCodeRanges** 屬性所指定的範圍內。</span><span class="sxs-lookup"><span data-stu-id="57bd1-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="57bd1-185">預設的情況是，如果工作結束時的結束代碼不是由 **ExitCodes** 或 **ExitCodeRanges** 所定義，或如果工作結束時發生前置處理錯誤且未設定 **PreProcessingError** 屬性，或如果工作失敗並發生檔案上傳錯誤且未設定 **FileUploadError** 屬性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="57bd1-186">若要在 .NET 中指定相依性動作，請設定結束情況的 [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] 屬性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="57bd1-187">**DependencyAction** 屬性會採用兩個值之一︰</span><span class="sxs-lookup"><span data-stu-id="57bd1-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="57bd1-188">將 **DependencyAction** 屬性設定為 [符合]，表示如果父系工作結束時出現指定的錯誤，相依工作就有資格執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="57bd1-189">將 **DependencyAction** 屬性設定為 [封鎖]，表示相依工作沒有資格執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="57bd1-190">結束代碼 0 的**DependencyAction** 屬性預設設定為 [符合]，而所有其他結束情況的預設設定則為 [封鎖]。</span><span class="sxs-lookup"><span data-stu-id="57bd1-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="57bd1-191">下列程式碼片段可設定父系工作的 **DependencyAction** 屬性。</span><span class="sxs-lookup"><span data-stu-id="57bd1-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="57bd1-192">如果父系工作結束時發生前置處理錯誤，或出現指定的錯誤碼，則會封鎖相依工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="57bd1-193">如果父系工作結束時出現任何其他非零的錯誤，相依工作就有資格執行。</span><span class="sxs-lookup"><span data-stu-id="57bd1-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="57bd1-194">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="57bd1-194">Code sample</span></span>
<span data-ttu-id="57bd1-195">[TaskDependencies][github_taskdependencies] 範例專案是 GitHub 上的其中一個 [Azure Batch 程式碼範例][github_samples]。</span><span class="sxs-lookup"><span data-stu-id="57bd1-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="57bd1-196">此 Visual Studio 解決方案示範︰</span><span class="sxs-lookup"><span data-stu-id="57bd1-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="57bd1-197">如何啟用作業的工作相依性</span><span class="sxs-lookup"><span data-stu-id="57bd1-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="57bd1-198">如何建立相依於其他工作的工作</span><span class="sxs-lookup"><span data-stu-id="57bd1-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="57bd1-199">如何在運算節點集區上執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="57bd1-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57bd1-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57bd1-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="57bd1-201">應用程式部署</span><span class="sxs-lookup"><span data-stu-id="57bd1-201">Application deployment</span></span>
<span data-ttu-id="57bd1-202">Batch 的 [應用程式封裝](batch-application-packages.md) 功能提供了簡單的方法，供您部署您的工作在計算節點上執行的應用程式並設定其版本。</span><span class="sxs-lookup"><span data-stu-id="57bd1-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="57bd1-203">安裝應用程式和預備資料</span><span class="sxs-lookup"><span data-stu-id="57bd1-203">Installing applications and staging data</span></span>
<span data-ttu-id="57bd1-204">請參閱 Azure Batch 論壇中的[在 Batch 計算節點上安裝應用程式和預備資料][forum_post]，以取得準備節點以執行工作的方法概觀。</span><span class="sxs-lookup"><span data-stu-id="57bd1-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="57bd1-205">這篇文章是由 Azure Batch 小組的其中一名成員所撰寫，非常適合做為入門指南，讓您了解將應用程式、工作輸入資料和其他檔案複製到計算節點的不同方法。</span><span class="sxs-lookup"><span data-stu-id="57bd1-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="57bd1-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "圖表︰一對一相依性"</span><span class="sxs-lookup"><span data-stu-id="57bd1-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="57bd1-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "圖表︰一對多相依性"</span><span class="sxs-lookup"><span data-stu-id="57bd1-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="57bd1-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "圖表︰工作識別碼範圍相依性"</span><span class="sxs-lookup"><span data-stu-id="57bd1-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
