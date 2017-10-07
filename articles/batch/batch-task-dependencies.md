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
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>建立相依於其他工作的 toorun 工作的工作相依性

您可以定義工作相依性 toorun 工作或一組工作的父工作完成之後，才。 一些實用的工作相依性案例包括︰

* Hello 雲端中的 MapReduce 樣式工作負載。
* 資料處理工作可表示為有向非循環圖 (DAG) 的工作。
* 預先呈現和後置轉譯程序，其中每項工作必須完成才能開始進行 hello 下一項工作。
* 任何其他工作在其中下游工作是相依於 hello 上游工作輸出。

與批次工作相依性，您可以建立 hello 一或多個父工作完成後計算節點上執行的排程工作。 例如，您可以建立一個將 3D 電影的每個影格以個別、平行工作轉譯的工作。 hello 最後一項工作-hello 「 合併 」 工作-合併 hello 以框架轉譯為 hello 完成影片只在所有框架都成功轉換。

根據預設，相依的工作都會排定執行 hello 父工作已順利完成之後，才。 您可以指定相依性動作 toooverride hello 預設行為，並執行工作，當 hello 父工作會失敗。 請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。  

您可以在一對一或一對多的關係中建立相依於其他工作的工作。 您也可以建立範圍相依性，其中的工作取決於 hello 完成的工作識別碼的指定範圍內的工作群組。 您可以結合這些三個基本案例 toocreate 多對多關聯性。

## <a name="task-dependencies-with-batch-net"></a>Batch .NET 的工作相依性
在本文中，我們討論如何使用 tooconfigure 工作相依性 hello[批次.NET] [ net_msdn]程式庫。 我們第一次為您示範如何太[啟用工作相依性](#enable-task-dependencies)於您的作業，並接著示範如何太[具有相依性設定的工作](#create-dependent-tasks)。 我們也將描述影響 toospecify 相依性動作 toorun 相依工作如果 hello 父失敗。 最後，我們會討論 hello[相依性案例](#dependency-scenarios)批次支援。

## <a name="enable-task-dependencies"></a>啟用工作相依性
toouse 批次應用程式中的工作相依性，您必須先設定 hello 作業 toouse 工作相依性。 在批次.NET 中，啟用您[CloudJob] [ net_cloudjob]藉由設定其[UsesTaskDependencies] [ net_usestaskdependencies]屬性太`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

在上述程式碼片段的 hello，"batchClient 」 是 hello 的執行個體[BatchClient] [ net_batchclient]類別。

## <a name="create-dependent-tasks"></a>建立相依的工作
toocreate 取決於 hello 一或多個父工作完成的工作，您可以指定工作 」 取決於"hello，hello 其他工作。 在批次.NET 中，設定 hello [CloudTask][net_cloudtask]。[DependsOn] [ net_dependson]與 hello 的執行個體的屬性[TaskDependencies] [ net_taskdependencies]類別：

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

此程式碼片段會使用工作識別碼 "Flowers" 建立相依工作。 hello 「 花 」 工作相依於工作"Rain"和"Sun"。 工作 「 花 」"Rain"和"Sun 」 已順利完成的工作之後，才會排程的 toorun 計算節點上。

> [!NOTE]
> 工作會被視為 toobe 順利完成時在 hello**完成**狀態及其**結束代碼**是`0`。 在批次.NET 中，這表示[CloudTask][net_cloudtask]。[狀態][ net_taskstate]屬性值為`Completed`和 hello CloudTask 的[TaskExecutionInformation][net_taskexecutioninformation]。[ExitCode] [ net_exitcode]屬性值是`0`。
> 
> 

## <a name="dependency-scenarios"></a>相依性案例
Azure Batch 中可使用的基本工作相依性案例有三種︰一對一、一對多、工作識別碼範圍相依性。 這些可以是結合的 tooprovide 第四個案例中，多對多。

| 案例&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 範例 |  |
|:---:| --- | --- |
|  [一對一](#one-to-one) |「taskB」相依於「taskA」 <p/> 「taskB」要等到「taskA」順利完成後，才會排定執行 |![圖表︰一對一工作相依性][1] |
|  [一對多](#one-to-many) |「taskC」同時相依於「taskA」和「taskB」 <p/> 「taskC」要等到「taskA」和「taskB」順利完成後，才會排定執行 |![圖表︰一對多工作相依性][2] |
|  [工作識別碼範圍](#task-id-range) |「taskD」相依於某一範圍的工作 <p/> *taskD*且不會排定執行，直到使用識別碼 hello 工作*1*透過*10*已順利完成 |![圖表︰工作識別碼範圍相依性][3] |

> [!TIP]
> 您可以建立**多對多**關聯性，例如其中 C、 D、 E 和 F 每一個工作相依於工作 A 和 b。這非常有用，例如，在其中您下游的工作相依於上游的多個工作的 hello 輸出平行化的前置處理案例。
> 
> 在本節中的 hello 範例，hello 父工作順利完成之後，才會執行相依工作。 此行為是 hello 相依工作的預設行為。 父工作失敗時所指定相依性動作 toooverride hello 預設行為之後，您可以執行相依工作。 請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。

### <a name="one-to-one"></a>一對一
在一對一的關聯性中，工作取決於 hello 一個父工作順利完成。 toocreate hello 相依性，提供單一的工作識別碼 toohello [TaskDependencies][net_taskdependencies]。[OnId] [ net_onid]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask] [net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>一對多
在一對多關聯性的工作取決於 hello 已完成的多個父工作。 toocreate hello 相依性，提供集合的工作 Id toohello [TaskDependencies][net_taskdependencies]。[OnIds] [ net_onids]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask] [net_cloudtask].

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

### <a name="task-id-range"></a>工作識別碼範圍
在為範圍的父工作的相依性，工作取決於 hello hello 已完成的工作 Id 位於範圍內。
toocreate hello 相依性，第一次提供 hello 和上次 hello 範圍 toohello 中的工作 Id [TaskDependencies][net_taskdependencies]。[OnIdRange] [ net_onidrange]靜態方法，當您填入 hello [DependsOn] [ net_dependson]屬性[CloudTask][net_cloudtask].

> [!IMPORTANT]
> 當您使用工作識別碼範圍為相依性時，hello hello 範圍中的工作 Id*必須*是整數值的字串表示法。
> 
> Hello 範圍中的每項工作必須滿足 hello 相依性，無法順利完成，或完成與失敗的對應的 tooa 相依性動作設定得**符合**。 請參閱 hello[相依性動作](#dependency-actions)如需詳細資訊。
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

## <a name="dependency-actions"></a>相依性動作

根據預設，只有在父系工作順利完成後，才會執行一項工作或一組工作。 在某些情況下，您可能想 toorun 相依工作，即使 hello 父工作失敗。 您可以指定相依性動作，以覆寫 hello 預設行為。 相依性動作指定相依工作是否符合資格 toorun，根據 hello 成功或失敗的 hello 父工作。 

例如，假設相依工作正在等候來自 hello 工作完成的 hello 上游資料。 如果 hello 上游工作失敗，hello 相依工作仍可能無法 toorun 使用較舊的資料。 在此情況下，相依性動作可以指定該 hello 相依工作是合格 toorun 儘管 hello hello 父工作失敗。

相依性動作根據 hello 父工作的結束條件。 您可以指定的相依性動作，讓任何 hello 下列結束條件。for.NET，請參閱 hello [ExitConditions] [ net_exitconditions]類別，如需詳細資訊：

- 發生前置處理錯誤時。
- 發生檔案上傳錯誤時。 如果 hello 工作結束時，透過已指定的結束代碼**exitCodes**或**exitCodeRanges**，然後遇到檔案上傳錯誤、 hello hello 結束程式碼會優先採用所指定的動作。
- 當 hello 工作結束時出現 hello 所定義的結束代碼**ExitCodes**屬性。
- 當 hello 工作結束時出現 hello 所指定範圍內的結束代碼**ExitCodeRanges**屬性。
- hello 預設案例中，如果 hello 工作結束時出現未定義的結束代碼**ExitCodes**或**ExitCodeRanges**，或如果 hello 工作結束時出現的前置處理錯誤和 hello **PreProcessingError**未設定屬性，或如果 hello 工作失敗，並將檔案上傳錯誤和 hello **FileUploadError**屬性未設定。 

在.NET 中，設定 hello 的相依性動作 toospecify [ExitOptions][net_exitoptions]。[DependencyAction] [ net_dependencyaction] hello 結束條件的屬性。 hello **DependencyAction**屬性會接受兩個值之一：

- 設定 hello **DependencyAction**屬性太**符合**指出的相依工作才適合 toorun hello 父工作會結束與指定的錯誤。
- 設定 hello **DependencyAction**屬性太**區塊**指出相依工作不合格 toorun。

hello 預設值為 hello **DependencyAction**屬性是**符合**的結束代碼 0，和**區塊**所有其他的結束條件。

hello 下列程式碼片段設定 hello **DependencyAction**父工作的屬性。 如果 hello 父工作結束時，前置處理的錯誤，或以 hello 指定的錯誤代碼 hello 相依工作被封鎖。 任何其他非零的錯誤結束 hello 父工作，hello 相依工作符合資格 toorun。

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

## <a name="code-sample"></a>程式碼範例
hello [TaskDependencies] [ github_taskdependencies]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。 此 Visual Studio 解決方案示範︰

- 如何 tooenable 工作相依性的作業
- 如何 toocreate 的工作相依於其他工作
- 影響 tooexecute 那些工作上的運算節點的集區。

## <a name="next-steps"></a>後續步驟
### <a name="application-deployment"></a>應用程式部署
hello[應用程式封裝](batch-application-packages.md)批次功能提供 tooboth 部署簡單的方法和 hello 應用程式，您的工作上所執行的計算節點的版本。

### <a name="installing-applications-and-staging-data"></a>安裝應用程式和預備資料
請參閱[安裝應用程式和暫存批次的資料計算節點][ forum_post]方法，以準備您的節點 toorun 工作概觀的 hello Azure Batch 論壇中。 其中寫入 hello Azure 批次小組成員，這篇文章是實用的入門 hello 不同的方式 toocopy 應用程式上，輸入的工作的資料和其他檔案 tooyour 計算節點。

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
