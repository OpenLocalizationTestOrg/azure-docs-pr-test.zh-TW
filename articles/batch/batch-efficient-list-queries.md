---
title: "aaaDesign 有效率清單查詢 Azure 批次 |Microsoft 文件"
description: "藉由在要求集區、作業、工作和計算節點等 Batch 資源的資訊時篩選查詢，以提高效能。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>有效率地建立查詢 toolist 批次資源

這裡您將學習如何 tooincrease Azure Batch 應用程式的效能，藉由減少查詢作業時，會將 hello 服務所傳回之資料的 hello 數量工作、 以及計算節點以 hello[批次.NET] [ api_net]程式庫。

幾乎所有的批次應用程式需要 tooperform 某種類型的查詢通常定期 hello 批次服務的監視或其他作業。 例如，toodetermine 是否有任何其餘作業中的佇列的工作，您必須取得資料 hello 工作中每個工作。 toodetermine hello 狀態的集區中的節點，您必須在 hello 集區中的每個節點上取得資料。 這篇文章說明如何 tooexecute 這類查詢在 hello 最有效率的方式。

> [!NOTE]
> hello 批次服務會提供特殊的應用程式開發介面支援 hello 常見的案例的計數中的工作的工作。 而不使用這些清單查詢，您可以呼叫 hello[取得工作計數][ rest_get_task_counts]作業。 「取得工作計數」會指出多少工作擱置中、執行中或已完成，以及有多少工作成功或失敗。 「取得工作計數」比清單查詢更有效率。 如需詳細資訊，請參閱[依狀態計算作業的工作 (預覽)](batch-get-task-counts.md)。 
>
> hello 取得工作計數作業不適用於批次服務版本早於 2017年-06-01.5.1。 如果您使用較舊版本的 hello 服務，然後改用清單查詢 toocount 工作中的工作。
>
> 

## <a name="meet-hello-detaillevel"></a>符合 hello DetailLevel
在實際執行批次應用程式，像是工作、 工作和計算節點的實體可以在 hello 千分位數字。 當您要求這些資源的詳細資訊時，可能會大量的資料必須 「 通用 hello wire"hello 批次服務 tooyour 應用程式上每個查詢。 藉由限制 hello 項目數目和類型的查詢所傳回的資訊，您可以增加 hello，將查詢的速度，並因此 hello 應用程式的效能。

這[批次.NET] [ api_net]應用程式開發介面程式碼片段清單*每*與作業，連同相關聯的工作*所有*的每個 hello 屬性工作：

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

您可以藉由套用 「 詳細資訊層級 」 tooyour 查詢，不過，執行更有效率的清單查詢。 您可以提供[ODATADetailLevel] [ odata]物件 toohello [JobOperations.ListTasks] [ net_list_tasks]方法。 這個程式碼片段會傳回識別碼 hello、 命令列和計算節點資訊屬性的已完成的工作：

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

在此範例案例，還有上千款 hello 作業中的工作如果 hello hello 第二個查詢結果通常會是速度快得多超過 hello 傳回第一次。 當您列出 hello 批次.NET API 的項目時，使用 ODATADetailLevel 詳細資訊就會包含[下方](#efficient-querying-in-batch-net)。

> [!IMPORTANT]
> 我們強烈建議您使用您*一律*提供 ODATADetailLevel 物件 tooyour.NET API 清單呼叫 tooensure 最大效率和應用程式的效能。 藉由指定詳細層級，您可以協助 toolower 批次服務的回應時間、 提高網路使用率和記憶體使用量降至最低用戶端應用程式。
> 
> 

## <a name="filter-select-and-expand"></a>篩選、選取及展開
hello[批次.NET] [ api_net]和[批次 REST] [ api_rest] Api 提供 hello 能力 tooreduce 項目在清單中，會傳回這兩個 hello 數目以及 hello 與每個傳回的資訊數量。 您可以藉由在執行清單查詢時指定**篩選**、**選取**和**展開字串**來執行此動作。

### <a name="filter"></a>Filter
hello 篩選字串是運算式，可降低 hello 傳回項目數目。 例如，清單只 hello 執行作業或清單只有計算節點是準備 toorun 工作的工作。

* hello 篩選字串包含一個或多個運算式，包含屬性名稱、 運算子和值的運算式。 hello 屬性可指定是在查詢時，特定 tooeach 實體型別是 hello 運算子所支援的每一個屬性。
* 使用 hello 邏輯運算子也可以結合多個運算式`and`和`or`。
* 此範例中篩選字串清單，僅執行 hello 的 「 轉譯 」 工作： `(state eq 'running') and startswith(id, 'renderTask')`。

### <a name="select"></a>選取
hello 選取字串限制所傳回的每個項目 hello 屬性值。 您指定的屬性名稱清單，而且只有這些屬性的值會傳回 hello hello 查詢結果中的項目。

* hello 選取字串包含屬性名稱的逗號分隔清單。 您可以指定任何 hello hello 您要查詢的實體類型的屬性。
* 此範例選取字串會指定應該針對每個工作只傳回三個屬性： `id, state, stateTransitionTime`。

### <a name="expand"></a>展開
hello 展開字串可減少需要的 tooobtain API 呼叫的 hello 數目特定資訊。 當您使用展開字串時，可以透過單一 API 呼叫取得每個項目的相關詳細資訊。 而不是第一次取得 hello 清單中的實體，則要求資訊 hello 清單中的每個項目，您可以使用擴充字串 tooobtain hello 單一 API 呼叫中的相同資訊。 較少的 API 呼叫表示較佳的效能。

* 類似 toohello 選取字串 hello 展開字串控制項是否包含特定資料查詢結果清單中。
* hello 展開字串僅適用於列出工作、 工作排程、 工作和集區時。 目前，它僅支援統計資訊。
* Hello 時需要的所有屬性，指定任何選取的字串，會展開字串*必須*使用的 tooget 統計資料資訊。 如果選取的字串是使用的 tooobtain 屬性的子集，則`stats`可以在 hello 選取字串中，指定與 hello 展開字串不需要指定 toobe。
* 這個範例會展開字串指定應傳回每個項目的 hello 清單中的統計資料資訊： `stats`。

> [!NOTE]
> 當建構 hello 的任何三個查詢字串型別 （篩選、 選取及展開），您必須確定 hello 屬性名稱和大小寫符合的 REST API 項目與其。 例如，當使用 hello.NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask)類別，您必須指定**狀態**而不是**狀態**，即使 hello.NET 屬性是[CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state)。 請參閱下方的 hello 資料表 hello.NET 和 REST Api 之間的屬性對應。
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>篩選、選取和展開字串的規則
* 屬性名稱，在篩選中，選取和展開字串應該會出現在 hello[批次 REST] [ api_rest] API-只有當您使用時，即使[批次.NET] [ api_net]或其中一個 hello 其他批次 Sdk。
* 所有屬性名稱都會區分大小寫，但屬性值不會區分大小寫。
* 日期/時間字串有兩種格式，開頭必須加上 `DateTime`。
  
  * W3C-DTF 格式範例：`creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * RFC 1123 格式範例：`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* 布林值字串為 `true` 或 `false`。
* 如果指定無效的屬性或運算子，將會導致 `400 (Bad Request)` 錯誤。

## <a name="efficient-querying-in-batch-net"></a>在 Batch .NET 中有效率地查詢
在 hello[批次.NET] [ api_net] API、 hello [ODATADetailLevel] [ odata]類別用來提供篩選、 選取和展開的字串toolist 作業。 hello ODataDetailLevel 類別有三個公用的字串屬性，可以指定在 hello 建構函式，或直接 hello 物件上設定。 您接著將 hello ODataDetailLevel 物件當做參數 toohello 各種清單作業，例如[ListPools][net_list_pools]， [ListJobs][net_list_jobs]，和[ListTasks][net_list_tasks]。

* [ODATADetailLevel][odata]。[FilterClause][odata_filter]: hello 傳回項目數目限制。
* [ODATADetailLevel][odata].[SelectClause][odata_select]：指定隨著每個項目一起傳回的屬性值。
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]：在單一 API 呼叫中擷取所有項目的資料，而不是針對每個項目個別呼叫。

hello 下列程式碼片段會使用 hello 批次.NET API tooefficiently hello 批次的查詢服務的一組特定的集區的 hello 統計資料。 在此案例中，hello 批次使用者已測試與實際的集區。 hello 測試集區識別碼前面會加上 「 測試 」，並 hello 生產集區識別碼前面會加上"prod"。 在 hello 片段*myBatchClient* hello 的正確初始化執行個體[BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient)類別。

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> 執行個體[ODATADetailLevel] [ odata] ，設定選取和展開子句也可以傳遞 tooappropriate Get 方法，例如[PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx)會傳回的資料 toolimit hello 數量。
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>批次 REST too.NET API 對應
篩選、選取和展開字串中的屬性名稱在名稱和大小寫方面， *必須* 反映其 REST API 對應項目。 下列的 hello 表格提供 hello.NET 和 REST API 的對應項目之間的對應。

### <a name="mappings-for-filter-strings"></a>篩選字串的對應
* **清單的.NET 方法**: hello.NET API 方法，這個資料行中的每個接受[ODATADetailLevel] [ odata]物件做為參數。
* **其餘列出要求**： 每個 REST API 頁面連結的 tooin 此資料行包含資料表中，指定 hello 屬性和作業中允許的*篩選*字串。 建構 [ODATADetailLevel.FilterClause][odata_filter] 字串時會使用這些屬性名稱和作業。

| .NET 清單方法 | REST 清單要求 |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[列出帳戶中的 hello 憑證][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[列出與工作相關聯的 hello 檔案][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[列示 hello 的 hello 作業準備及作業版本作業 」 工作的狀態][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[列出帳戶中的 hello 工作][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[在節點上的清單 hello 檔案][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[列出 hello 工作與工作相關聯][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[列出帳戶中的 hello 作業排程][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[列出 hello 工作相關聯的工作排程][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[清單 hello 計算集區中的節點][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[在帳戶中的清單 hello 集區][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>選取字串的對應
* **Batch .NET types**：Batch .NET API 類型。
* **REST API 實體**： 此資料行中的每個頁面包含一或多個資料表，列出 hello 類型 hello REST API 屬性的名稱。 建構「選取」  字串時會使用這些屬性名稱。 建構 [ODATADetailLevel.SelectClause][odata_select] 字串時會使用這些相同的屬性名稱。

| Batch .NET types | REST API entities |
| --- | --- |
| [憑證][net_cert] |[取得憑證的相關資訊][rest_get_cert] |
| [CloudJob][net_job] |[取得作業的相關資訊][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[取得作業排程的相關資訊][rest_get_schedule] |
| [ComputeNode][net_node] |[取得節點的相關資訊][rest_get_node] |
| [CloudPool][net_pool] |[取得集區的相關資訊][rest_get_pool] |
| [CloudTask][net_task] |[取得作業的相關資訊][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>範例：建構篩選字串
當您建構篩選字串[ODATADetailLevel.FilterClause][odata_filter]，請參閱底下 「 篩選字串對應 」 toofind hello REST API 文件頁面對應上方 hello 資料表您想 tooperform toohello 清單作業。 在 hello 第一個多重資料列的資料表在該頁面上，您會發現 hello 可篩選的屬性和其支援的運算子。 如果您想 tooretrieve 其結束碼為非零的所有工作，例如，此資料列上[清單與工作相關聯的 hello 工作][ rest_list_tasks]指定 hello 適用的屬性字串和允許的運算子：

| 屬性 | 允許的作業 | 類型 |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

因此，會是 hello 篩選條件字串，以列出所有工作，則為非零結束代碼：

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>範例：建構選取字串
tooconstruct [ODATADetailLevel.SelectClause][odata_select]，請參閱底下 「 選取的字串對應 」 上方 hello 資料表，並瀏覽 toohello 對應 toohello 型別之實體的 REST API 頁面，您列出。 在 hello 第一個多重資料列的資料表在該頁面上，您會發現 hello 可選取的屬性和其支援的運算子。 如果您想 tooretrieve 只有 hello 識別碼以及每項工作的命令列在清單中，比方說，您會發現這些資料列中 hello 適用的資料表上[取得工作的相關資訊][rest_get_task]:

| 屬性 | 類型 | 注意事項 |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

hello 選取字串，包括唯一識別碼 hello 和命令列與每個列出的工作將會是：

`id, commandLine`

## <a name="code-samples"></a>程式碼範例
### <a name="efficient-list-queries-code-sample"></a>有效率的清單查詢程式碼範例
簽出 hello [EfficientListQueries] [ efficient_query_sample] GitHub toosee 效率的範例專案清單查詢可能會影響應用程式中的效能。 此 C# 主控台應用程式建立，並將大量的工作 tooa 作業。 然後，它可讓多個呼叫 toohello [JobOperations.ListTasks] [ net_list_tasks]方法，並傳遞[ODATADetailLevel] [ odata]的物件設定為使用不同的屬性值 toovary hello 數量資料 toobe 傳回。 它會產生類似 toohello 下列輸出：

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Hello 經過時間所示，您可以大幅降低查詢回應時間，藉由限制 hello 屬性和項目所傳回的 hello 數目。 您可以在 hello 中找到這個和其他範例專案[azure 批次範例][ github_samples] GitHub 上的儲存機制。

### <a name="batchmetrics-library-and-code-sample"></a>BatchMetrics 程式庫和程式碼範例
此外 toohello EfficientListQueries 程式碼上述範例，您可以找到 hello [BatchMetrics] [ batch_metrics] hello 中的專案[azure 批次範例][ github_samples]GitHub 儲存機制。 hello BatchMetrics 範例專案會示範如何 tooefficiently 監視使用 hello 批次 API 的 Azure 批次工作進度。

hello [BatchMetrics] [ batch_metrics]範例包含.NET 類別庫專案的可合併到您自己的專案和簡單的命令列程式 tooexercise 和示範 hello 使用 hello程式庫。

hello 專案中的 hello 範例應用程式會示範下列作業的 hello:

1. 您選取特定的屬性順序 toodownload 只有 hello 屬性中需要
2. 篩選順序 toodownload 狀態轉換時間僅會變更 hello 上次查詢後

例如，下列方法的 hello 會出現在 hello BatchMetrics 程式庫。 它會傳回指定的唯一 hello ODATADetailLevel`id`和`state`應該查詢的 hello 實體取得內容。 它也會指定唯一的實體，其狀態已變更自指定的 hello`DateTime`應傳回參數。

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>後續步驟
### <a name="parallel-node-tasks"></a>平行節點工作
[Azure Batch 計算資源使用率與並行節點工作最大化](batch-parallel-node-tasks.md)是另一個發行項相關 tooBatch 應用程式效能。 某些類型的工作負載可以受益於在規模較大但數量較少的計算節點上執行平行工作。 簽出 hello[範例案例](batch-parallel-node-tasks.md#example-scenario)如需詳細資訊，在這類案例中的 hello 文件中。

### <a name="batch-forum"></a>Batch 論壇
hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。 請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job