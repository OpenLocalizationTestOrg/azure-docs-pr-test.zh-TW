---
title: "aaaUse 工作相依性 toorun 工作為基礎的其他工作-Azure 批次的 hello 完成 |Microsoft 文件"
description: "建立 hello 完成處理 MapReduce 模式和類似的巨量資料的其他工作而定的工作 Azure 批次中的工作負載。"
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="39bba-103">建立相依於其他工作的 toorun 工作的工作相依性</span><span class="sxs-lookup"><span data-stu-id="39bba-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="39bba-104">您可以定義工作相依性 toorun 工作或一組工作的父工作完成之後，才。</span><span class="sxs-lookup"><span data-stu-id="39bba-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="39bba-105">一些實用的工作相依性案例包括︰</span><span class="sxs-lookup"><span data-stu-id="39bba-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="39bba-106">Hello 雲端中的 MapReduce 樣式工作負載。</span><span class="sxs-lookup"><span data-stu-id="39bba-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="39bba-107">資料處理工作可表示為有向非循環圖 (DAG) 的工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="39bba-108">預先呈現和後置轉譯程序，其中每項工作必須完成才能開始進行 hello 下一項工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="39bba-109">任何其他工作在其中下游工作是相依於 hello 上游工作輸出。</span><span class="sxs-lookup"><span data-stu-id="39bba-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="39bba-110">與批次工作相依性，您可以建立 hello 一或多個父工作完成後計算節點上執行的排程工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="39bba-111">例如，您可以建立一個將 3D 電影的每個影格以個別、平行工作轉譯的工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="39bba-112">hello 最後一項工作-hello 「 合併 」 工作-合併 hello 以框架轉譯為 hello 完成影片只在所有框架都成功轉換。</span><span class="sxs-lookup"><span data-stu-id="39bba-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="39bba-113">根據預設，相依的工作都會排定執行 hello 父工作已順利完成之後，才。</span><span class="sxs-lookup"><span data-stu-id="39bba-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="39bba-114">您可以指定相依性動作 toooverride hello 預設行為，並執行工作，當 hello 父工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="39bba-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="39bba-115">請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="39bba-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="39bba-116">您可以在一對一或一對多的關係中建立相依於其他工作的工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="39bba-117">您也可以建立範圍相依性，其中的工作取決於 hello 完成的工作識別碼的指定範圍內的工作群組。</span><span class="sxs-lookup"><span data-stu-id="39bba-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="39bba-118">您可以結合這些三個基本案例 toocreate 多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="39bba-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="39bba-119">Batch .NET 的工作相依性</span><span class="sxs-lookup"><span data-stu-id="39bba-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="39bba-120">在本文中，我們討論如何使用 tooconfigure 工作相依性 hello[批次.NET] [ net_msdn]程式庫。</span><span class="sxs-lookup"><span data-stu-id="39bba-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="39bba-121">我們第一次為您示範如何太[啟用工作相依性](#enable-task-dependencies)於您的作業，並接著示範如何太[具有相依性設定的工作](#create-dependent-tasks)。</span><span class="sxs-lookup"><span data-stu-id="39bba-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="39bba-122">我們也將描述影響 toospecify 相依性動作 toorun 相依工作如果 hello 父失敗。</span><span class="sxs-lookup"><span data-stu-id="39bba-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="39bba-123">最後，我們會討論 hello[相依性案例](#dependency-scenarios)批次支援。</span><span class="sxs-lookup"><span data-stu-id="39bba-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="39bba-124">啟用工作相依性</span><span class="sxs-lookup"><span data-stu-id="39bba-124">Enable task dependencies</span></span>
<span data-ttu-id="39bba-125">toouse 批次應用程式中的工作相依性，您必須先設定 hello 作業 toouse 工作相依性。</span><span class="sxs-lookup"><span data-stu-id="39bba-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="39bba-126">在批次.NET 中，啟用您[CloudJob] [ net_cloudjob]藉由設定其[UsesTaskDependencies] [ net_usestaskdependencies]屬性太`true`:</span><span class="sxs-lookup"><span data-stu-id="39bba-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="39bba-127">在上述程式碼片段的 hello，"batchClient 」 是 hello 的執行個體[BatchClient] [ net_batchclient]類別。</span><span class="sxs-lookup"><span data-stu-id="39bba-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="39bba-128">建立相依的工作</span><span class="sxs-lookup"><span data-stu-id="39bba-128">Create dependent tasks</span></span>
<span data-ttu-id="39bba-129">toocreate 取決於 hello 一或多個父工作完成的工作，您可以指定工作 」 取決於"hello，hello 其他工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="39bba-130">在批次.NET 中，設定 hello [CloudTask][net_cloudtask]。[DependsOn] [ net_dependson]與 hello 的執行個體的屬性[TaskDependencies] [ net_taskdependencies]類別：</span><span class="sxs-lookup"><span data-stu-id="39bba-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="39bba-131">此程式碼片段會使用工作識別碼 "Flowers" 建立相依工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="39bba-132">hello 「 花 」 工作相依於工作"Rain"和"Sun"。</span><span class="sxs-lookup"><span data-stu-id="39bba-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="39bba-133">工作 「 花 」"Rain"和"Sun 」 已順利完成的工作之後，才會排程的 toorun 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="39bba-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="39bba-134">工作會被視為 toobe 順利完成時在 hello**完成**狀態及其**結束代碼**是`0`。</span><span class="sxs-lookup"><span data-stu-id="39bba-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="39bba-135">在批次.NET 中，這表示[CloudTask][net_cloudtask]。[狀態][ net_taskstate]屬性值為`Completed`和 hello CloudTask 的[TaskExecutionInformation][net_taskexecutioninformation]。[ExitCode] [ net_exitcode]屬性值是`0`。</span><span class="sxs-lookup"><span data-stu-id="39bba-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="39bba-136">相依性案例</span><span class="sxs-lookup"><span data-stu-id="39bba-136">Dependency scenarios</span></span>
<span data-ttu-id="39bba-137">Azure Batch 中可使用的基本工作相依性案例有三種︰一對一、一對多、工作識別碼範圍相依性。</span><span class="sxs-lookup"><span data-stu-id="39bba-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="39bba-138">這些可以是結合的 tooprovide 第四個案例中，多對多。</span><span class="sxs-lookup"><span data-stu-id="39bba-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="39bba-139">案例&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="39bba-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="39bba-140">範例</span><span class="sxs-lookup"><span data-stu-id="39bba-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="39bba-141">一對一</span><span class="sxs-lookup"><span data-stu-id="39bba-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="39bba-142">「taskB」相依於「taskA」</span><span class="sxs-lookup"><span data-stu-id="39bba-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="39bba-143">「taskB」要等到「taskA」順利完成後，才會排定執行</span><span class="sxs-lookup"><span data-stu-id="39bba-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="39bba-144">![圖表︰一對一工作相依性][1]</span><span class="sxs-lookup"><span data-stu-id="39bba-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="39bba-145">一對多</span><span class="sxs-lookup"><span data-stu-id="39bba-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="39bba-146">「taskC」同時相依於「taskA」和「taskB」</span><span class="sxs-lookup"><span data-stu-id="39bba-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="39bba-147">「taskC」要等到「taskA」和「taskB」順利完成後，才會排定執行</span><span class="sxs-lookup"><span data-stu-id="39bba-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="39bba-148">![圖表︰一對多工作相依性][2]</span><span class="sxs-lookup"><span data-stu-id="39bba-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="39bba-149">工作識別碼範圍</span><span class="sxs-lookup"><span data-stu-id="39bba-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="39bba-150">「taskD」相依於某一範圍的工作</span><span class="sxs-lookup"><span data-stu-id="39bba-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="39bba-151">*taskD*且不會排定執行，直到使用識別碼 hello 工作*1*透過*10*已順利完成</span><span class="sxs-lookup"><span data-stu-id="39bba-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="39bba-152">![圖表︰工作識別碼範圍相依性][3]</span><span class="sxs-lookup"><span data-stu-id="39bba-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="39bba-153">您可以建立**多對多**關聯性，例如其中 C、 D、 E 和 F 每一個工作相依於工作 A 和 b。這非常有用，例如，在其中您下游的工作相依於上游的多個工作的 hello 輸出平行化的前置處理案例。</span><span class="sxs-lookup"><span data-stu-id="39bba-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="39bba-154">在本節中的 hello 範例，hello 父工作順利完成之後，才會執行相依工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="39bba-155">此行為是 hello 相依工作的預設行為。</span><span class="sxs-lookup"><span data-stu-id="39bba-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="39bba-156">父工作失敗時所指定相依性動作 toooverride hello 預設行為之後，您可以執行相依工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="39bba-157">請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="39bba-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="39bba-158">一對一</span><span class="sxs-lookup"><span data-stu-id="39bba-158">One-to-one</span></span>
<span data-ttu-id="39bba-159">在一對一的關聯性中，工作取決於 hello 一個父工作順利完成。</span><span class="sxs-lookup"><span data-stu-id="39bba-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="39bba-160">toocreate hello 相依性，提供單一的工作識別碼 toohello [TaskDependencies][net_taskdependencies]。[OnId] [ net_onid]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="39bba-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="39bba-161">一對多</span><span class="sxs-lookup"><span data-stu-id="39bba-161">One-to-many</span></span>
<span data-ttu-id="39bba-162">在一對多關聯性的工作取決於 hello 已完成的多個父工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="39bba-163">toocreate hello 相依性，提供集合的工作 Id toohello [TaskDependencies][net_taskdependencies]。[OnIds] [ net_onids]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="39bba-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="39bba-164">工作識別碼範圍</span><span class="sxs-lookup"><span data-stu-id="39bba-164">Task ID range</span></span>
<span data-ttu-id="39bba-165">在為範圍的父工作的相依性，工作取決於 hello hello 已完成的工作 Id 位於範圍內。</span><span class="sxs-lookup"><span data-stu-id="39bba-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="39bba-166">toocreate hello 相依性，第一次提供 hello 和上次 hello 範圍 toohello 中的工作 Id [TaskDependencies][net_taskdependencies]。[OnIdRange] [ net_onidrange]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="39bba-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39bba-167">當您使用工作識別碼範圍為相依性時，hello hello 範圍中的工作 Id*必須*是整數值的字串表示法。</span><span class="sxs-lookup"><span data-stu-id="39bba-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="39bba-168">Hello 範圍中的每項工作必須滿足 hello 相依性，無法順利完成，或完成與失敗的對應的 tooa 相依性動作設定得**符合**。</span><span class="sxs-lookup"><span data-stu-id="39bba-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="39bba-169">請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="39bba-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="39bba-170">相依性動作</span><span class="sxs-lookup"><span data-stu-id="39bba-170">Dependency actions</span></span>

<span data-ttu-id="39bba-171">根據預設，只有在父系工作順利完成後，才會執行一項工作或一組工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="39bba-172">在某些情況下，您可能想 toorun 相依工作，即使 hello 父工作失敗。</span><span class="sxs-lookup"><span data-stu-id="39bba-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="39bba-173">您可以指定相依性動作，以覆寫 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="39bba-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="39bba-174">相依性動作指定相依工作是否符合資格 toorun，根據 hello 成功或失敗的 hello 父工作。</span><span class="sxs-lookup"><span data-stu-id="39bba-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="39bba-175">例如，假設相依工作正在等候來自 hello 工作完成的 hello 上游資料。</span><span class="sxs-lookup"><span data-stu-id="39bba-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="39bba-176">如果 hello 上游工作失敗，hello 相依工作仍可能無法 toorun 使用較舊的資料。</span><span class="sxs-lookup"><span data-stu-id="39bba-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="39bba-177">在此情況下，相依性動作可以指定該 hello 相依工作是合格 toorun 儘管 hello hello 父工作失敗。</span><span class="sxs-lookup"><span data-stu-id="39bba-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="39bba-178">相依性動作根據 hello 父工作的結束條件。</span><span class="sxs-lookup"><span data-stu-id="39bba-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="39bba-179">您可以指定的相依性動作，讓任何 hello 下列結束條件。for.NET，請參閱 hello [ExitConditions] [ net_exitconditions]類別，如需詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="39bba-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="39bba-180">發生前置處理錯誤時。</span><span class="sxs-lookup"><span data-stu-id="39bba-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="39bba-181">發生檔案上傳錯誤時。</span><span class="sxs-lookup"><span data-stu-id="39bba-181">When a file upload error occurs.</span></span> <span data-ttu-id="39bba-182">如果 hello 工作結束時，透過已指定的結束代碼**exitCodes**或**exitCodeRanges**，然後遇到檔案上傳錯誤、 hello hello 結束程式碼會優先採用所指定的動作。</span><span class="sxs-lookup"><span data-stu-id="39bba-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="39bba-183">當 hello 工作結束時出現 hello 所定義的結束代碼**ExitCodes**屬性。</span><span class="sxs-lookup"><span data-stu-id="39bba-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="39bba-184">當 hello 工作結束時出現 hello 所指定範圍內的結束代碼**ExitCodeRanges**屬性。</span><span class="sxs-lookup"><span data-stu-id="39bba-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="39bba-185">hello 預設案例中，如果 hello 工作結束時出現未定義的結束代碼**ExitCodes**或**ExitCodeRanges**，或如果 hello 工作結束時出現的前置處理錯誤和 hello **PreProcessingError**未設定屬性，或如果 hello 工作失敗，並將檔案上傳錯誤和 hello **FileUploadError**屬性未設定。</span><span class="sxs-lookup"><span data-stu-id="39bba-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="39bba-186">在.NET 中，設定 hello 的相依性動作 toospecify [ExitOptions][net_exitoptions]。[DependencyAction] [ net_dependencyaction] hello 結束條件的屬性。</span><span class="sxs-lookup"><span data-stu-id="39bba-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="39bba-187">hello **DependencyAction**屬性會接受兩個值之一：</span><span class="sxs-lookup"><span data-stu-id="39bba-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="39bba-188">設定 hello **DependencyAction**屬性太**符合**指出的相依工作才適合 toorun hello 父工作會結束與指定的錯誤。</span><span class="sxs-lookup"><span data-stu-id="39bba-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="39bba-189">設定 hello **DependencyAction**屬性太**區塊**指出相依工作不合格 toorun。</span><span class="sxs-lookup"><span data-stu-id="39bba-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="39bba-190">hello 預設值為 hello **DependencyAction**屬性是**符合**的結束代碼 0，和**區塊**所有其他的結束條件。</span><span class="sxs-lookup"><span data-stu-id="39bba-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="39bba-191">hello 下列程式碼片段設定 hello **DependencyAction**父工作的屬性。</span><span class="sxs-lookup"><span data-stu-id="39bba-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="39bba-192">如果 hello 父工作結束時，前置處理的錯誤，或以 hello 指定的錯誤代碼 hello 相依工作被封鎖。</span><span class="sxs-lookup"><span data-stu-id="39bba-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="39bba-193">任何其他非零的錯誤結束 hello 父工作，hello 相依工作符合資格 toorun。</span><span class="sxs-lookup"><span data-stu-id="39bba-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="39bba-194">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="39bba-194">Code sample</span></span>
<span data-ttu-id="39bba-195">hello [TaskDependencies] [ github_taskdependencies]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="39bba-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="39bba-196">此 Visual Studio 解決方案示範︰</span><span class="sxs-lookup"><span data-stu-id="39bba-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="39bba-197">如何 tooenable 工作相依性的作業</span><span class="sxs-lookup"><span data-stu-id="39bba-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="39bba-198">如何 toocreate 的工作相依於其他工作</span><span class="sxs-lookup"><span data-stu-id="39bba-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="39bba-199">影響 tooexecute 那些工作上的運算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="39bba-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39bba-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39bba-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="39bba-201">應用程式部署</span><span class="sxs-lookup"><span data-stu-id="39bba-201">Application deployment</span></span>
<span data-ttu-id="39bba-202">hello[應用程式封裝](batch-application-packages.md)批次功能提供 tooboth 部署簡單的方法和 hello 應用程式，您的工作上所執行的計算節點的版本。</span><span class="sxs-lookup"><span data-stu-id="39bba-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="39bba-203">安裝應用程式和預備資料</span><span class="sxs-lookup"><span data-stu-id="39bba-203">Installing applications and staging data</span></span>
<span data-ttu-id="39bba-204">請參閱[安裝應用程式和暫存批次的資料計算節點][ forum_post]方法，以準備您的節點 toorun 工作概觀的 hello Azure Batch 論壇中。</span><span class="sxs-lookup"><span data-stu-id="39bba-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="39bba-205">其中寫入 hello Azure 批次小組成員，這篇文章是實用的入門 hello 不同的方式 toocopy 應用程式上，輸入的工作的資料和其他檔案 tooyour 計算節點。</span><span class="sxs-lookup"><span data-stu-id="39bba-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "圖表︰一對一相依性"
[2]: ./media/batch-task-dependency/02_one_to_many.png "圖表︰一對多相依性"
[3]: ./media/batch-task-dependency/03_task_id_range.png "圖表︰工作識別碼範圍相依性"
