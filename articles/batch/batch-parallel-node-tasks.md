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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Toomaximize 使用量的批次的運算節點同時執行工作 

Azure Batch 集區中每個計算節點上同時執行多個工作，您可以最大化 hello 集區中的節點數目較少的資源使用量。 對於某些工作負載來說，這會產生縮短作業時間和降低成本的效益。

專用的所有節點的資源 tooa 單一工作都受益於某些情況下，雖然幾種情況而都獲益允許多個工作 tooshare 這些資源：

* **最小化的資料傳輸**工作何時為可以 tooshare 資料。 在此案例中，您可以大幅降低資料傳輸費用複製共用的資料 tooa 較少的節點，並在每個節點上平行執行工作。 這特別適用於必須傳送 hello 資料 toobe 複製的 tooeach 節點之間的地理區域。
* **最大化記憶體使用量** ，但是只有在短時間之內，以及在執行期間的變數時間。 您可以採用較少但較大，計算節點的更多的記憶體 tooefficiently 處理這類高峰流量。 這些節點會有多個工作，每個節點上，以平行方式執行，但每一項工作會利用 hello 節點充足的記憶體在不同的時間。
* **緩和節點數目限制** 。 是目前的集區設定的節點間通訊限制的 too50 計算節點。 如果在集區中的每個節點可以 tooexecute 工作，以平行方式，可以同時執行大量的工作。
* **複寫在內部部署計算叢集**，例如當您第一次移動運算環境 tooAzure。 如果您目前的內部部署解決方案執行每個計算節點的多個工作，您可以增加 hello 最大數目的節點工作 toomore 密切鏡像該組態。

## <a name="example-scenario"></a>範例案例
做為範例 tooillustrate hello 平行工作執行的優點，假設您的工作應用程式的 CPU 和記憶體需求使[標準\_D1](../cloud-services/cloud-services-sizes-specs.md)節點已足夠。 但是，順序 toofinish hello 作業所需的 hello 時間中，這些節點的 1,000 所需。

如果不使用 Standard\_D1 節點 (具有 1 個 CPU 核心)，您可以採用具有 16 個核心的 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 節點，並啟用平行工作執行。 因此，不需使用 1000 個節點，而只需 63 個節點，用量「少了16 倍」  。 此外，如果大型應用程式的檔案或參考資料所需的每個節點，作業持續時間和效率會再次改進由於 hello 資料會複製的 tooonly 16 個節點。

## <a name="enable-parallel-task-execution"></a>啟用平行工作執行
您可以設定平行工作執行的計算節點在 hello 集區層級。 Hello 批次.NET 程式庫，以設定 hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net]時建立集區的屬性。 如果您使用 hello 批次 REST API，設定 hello [maxTasksPerNode] [ rest_addpool] hello 集區建立期間的要求主體中的項目。

Azure 批次，可讓您 tooset 最大的工作，每個節點組成 toofour 倍 (4 x) hello 節點核心數目。 例如，如果 hello 集區設定與節點的大小 「 大型 」 （四個核心），然後`maxTasksPerNode`設定 too16。 Hello 節點大小的每個核心的 hello 數目的詳細資訊，請參閱[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)。 如需服務限制的詳細資訊，請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。

> [!TIP]
> 要確定 tootake 到帳戶 hello`maxTasksPerNode`值在建構時[自動調整公式][ enable_autoscaling]集區。 例如，評估 `$RunningTasks` 的公式可能大幅受到每個節點的工作增加的影響。 如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的運算節點](batch-automatic-scaling.md) 。
>
>

## <a name="distribution-of-tasks"></a>工作的分佈
集區中的 hello 計算節點可以同時執行的工作，很重要 toospecify hello 工作 toobe 跨 hello 集區中的 hello 節點散佈的方式。

使用 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule]屬性，您可以指定，工作應該平均指派給 hello 集區 （「 分配"） 中的所有節點。 或者，您可以指定，儘可能多的工作應該指派 tooeach 節點之前工作指派 tooanother 節點區內 hello （「 壓縮 」）。

做為範例的情況下，這項功能會很有價值的方式，請考慮 hello 集區[標準\_D14](../cloud-services/cloud-services-sizes-specs.md)節點 （在上述範例 hello） 以設定[CloudPool.MaxTasksPerComputeNode] [maxtasks_net]值為 16。 如果 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule]設有[ComputeNodeFillType] [ fill_type]的*組件*，它會最大化所有 16 個核心的每個節點的使用量，並允許[自動調整集區](batch-automatic-scaling.md)tooprune hello 集區 （而不指派任何工作的節點） 中未使用的節點。 這可最小化資源使用量和節省金錢。

## <a name="batch-net-example"></a>Batch .NET 範例
這[批次.NET] [ api_net]應用程式開發介面程式碼片段示範要求 toocreate 包含四項工作每個節點最多四個大型節點的集區。 它會指定工作排程將會填滿工作先前 tooassigning 工作 tooanother 節點區內 hello 與每個節點的原則。 如需有關使用 hello 批次.NET API 加入集區的詳細資訊，請參閱[BatchClient.PoolOperations.CreatePool][poolcreate_net]。

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

## <a name="batch-rest-example"></a>Batch REST 範例
這[批次 REST] [ api_rest]應用程式開發介面程式碼片段示範要求 toocreate 包含四項工作每個節點最多兩個大型節點的集區。 如需有關如何使用 REST API hello 加入集區的詳細資訊，請參閱[加入集區 tooan 帳戶][rest_addpool]。

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
> 您可以設定 hello`maxTasksPerNode`項目和[MaxTasksPerComputeNode] [ maxtasks_net]屬性只能在集區建立期間。 建立集區後無法加以修改。
>
>

## <a name="code-sample"></a>程式碼範例
hello [ParallelNodeTasks] [ parallel_tasks_sample] GitHub 上的專案說明 hello hello 使用[CloudPool.MaxTasksPerComputeNode] [ maxtasks_net]屬性。

此 C# 主控台應用程式使用 hello[批次.NET] [ api_net]文件庫 toocreate 具有一或多個集區計算節點。 它會執行那些節點 toosimulate 可變負載的可設定的工作數目。 Hello 應用程式的輸出指定的節點執行每項工作。 hello 應用程式也提供 hello 作業參數和持續時間的摘要。 hello hello 輸出 hello 範例應用程式的兩個不同的回合的部份摘要下方會出現。

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

hello hello 範例應用程式第一次執行顯示 hello 集區和 hello 預設值為每個節點，一項工作中的單一節點與 hello 作業持續時間為過去 30 分鐘內。

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

第二次的 hello 範例會示範執行作業的持續時間大幅降低 hello。 這是因為 hello 集區設定中的每個節點，可讓平行工作執行 toocomplete hello 作業幾乎季 hello 時間的四項工作。

> [!NOTE]
> 上述的 hello 摘要中的 hello 作業持續時間不包括集區建立時間。 Hello 工作上述的每個已送出的 toopreviously 建立集區的計算節點都在 hello*閒置*次送出狀態。
>
>

## <a name="next-steps"></a>後續步驟
### <a name="batch-explorer-heat-map"></a>Batch 總管熱圖
hello [Azure 批次總管][batch_explorer]，hello Azure 批次的其中一個[範例應用程式][github_samples]，包含*熱度圖*功能，可提供工作執行的視覺效果。 當您要執行 hello [ParallelTasks] [ parallel_tasks_sample]範例應用程式，您可以使用 hello 熱門地圖功能 tooeasily 視覺化 hello 平行的工作，每個節點上執行。

![Batch 總管熱圖][1]

*顯示包含四個節點的集區的Batch 總管熱圖，每個節點目前正在執行四個工作*

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
