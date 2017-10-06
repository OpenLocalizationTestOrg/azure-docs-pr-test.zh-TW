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
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>計數工作狀態 toomonitor 作業的進度 （預覽）

Azure 批次提供有效率的方式 toomonitor hello 工作的進度，執行其工作。 您可以呼叫 hello[取得工作計數][ rest_get_task_counts]出多少工作處於作用中、 執行中或已完成狀態，以及有多少作業 toofind 成功或失敗。 透過計算 hello 數項工作中每個狀態，您可以更輕鬆地顯示 hello 作業的進度 tooa 使用者，或偵測到未預期的延遲或可能會影響 hello 作業失敗。

> [!IMPORTANT]
> hello 取得工作計數作業目前為預覽狀態，和尚無法使用 Azure 政府、 Azure China 和 Azure 德國中。 
>
>

## <a name="how-tasks-are-counted"></a>工作的計算方式

hello 取得工作計數作業會依照狀態、 工作計算，如下所示：

- 工作會計算為**active**當它排入佇列，而且要能 toorun，但目前尚未指派 tooa 計算節點。 如果工作相依於尚未完成的父工作，也會算作是**作用中**的工作。 如需有關工作相依性的詳細資訊，請參閱[toorun 工作相依於其他工作建立工作的相依性](batch-task-dependencies.md)。 
- 工作會計算為**執行**當它已被指派 tooa 計算節點，但尚未完成。 工作會計算為**執行**當其狀態是`preparing`或`running`、 由 hello[取得工作的相關資訊][ rest_get_task]作業。
- 工作會計算為**完成**時不會再合格 toorun。 算作是**已完成**的工作通常已順利完成，或未順利完成且也已達到其重試限制。 

hello 取得工作計數作業也會報告多少工作已成功或失敗。 批次判斷工作是否成功或失敗藉由檢查 hello**結果**hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] 屬性屬性：

    - 工作會計算為**成功**如果 hello 工作執行結果為`success`。
    - 工作會計算為**失敗**如果 hello 工作執行結果為`failure`。

如需工作狀態的詳細資訊，請參閱[取得工作相關資訊][rest_get_task]。

hello 下列.NET 程式碼範例示範如何 tooretrieve 工作計算的狀態： 

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
> 您可以使用其他類似的模式和 tooget 工作會計算作業的其他支援的語言。 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>工作計數的一致性檢查

hello 批次服務彙總工作計數，從非同步分散式系統的多個部分收集資料。 工作計數的 tooensure 正確無誤，批次的計數執行一致性檢查針對 hello 系統的多個元件的狀態，提供額外的驗證。 只要 hello 作業中有超過 200,000 工作批次會執行一致性檢查。 在 hello 罕見事件中 hello 一致性檢查，會找到錯誤，批次更正 hello 作業結果的 hello 取得工作計數根據 hello 的 hello 一致性檢查的結果。 hello 一致性檢查是客戶依賴 hello 取得工作計數作業取得 hello 正確的資訊，這些方案需要額外的量值 tooensure。

hello **validationStatus** hello 回應中的屬性會指出批次是否執行 hello 一致性檢查。 如果批次尚未針對 hello hello 系統中保留的實際狀態可以 toocheck 狀態計數，然後 hello **validationStatus**屬性設定太`unvalidated`。 基於效能考量，批次將不會執行 hello 一致性檢查，如果 hello 工作包含超過 200,000 」 工作，因此 hello **validationStatus**屬性可能設定太`unvalidated`在此情況下。 不過，hello 工作計數不一定是錯誤在此情況下，因為即使非常有限的資料遺失就會不太可能。 

當工作變更狀態時，hello 彙總管線會處理 hello 變更幾秒鐘內。 hello 取得工作計數的作業會反映在該期間內的 hello 更新工作計數。 不過，hello 彙總管線遺漏工作狀態的變更，然後變更不被註冊直到 hello 下驗證階段。 在此期間，工作計數可能稍微不正確，因為 toohello 遺失的事件，但它們在下一步 驗證階段 hello 更正。

## <a name="best-practices-for-counting-a-jobs-tasks"></a>計算作業之工作的最佳做法

呼叫 hello 取得工作計數作業，是最有效率的方式 tooreturn hello 基本作業的工作狀態的計數。 如果您使用批次服務版本 2017年-06-01.5.1，則建議您撰寫或更新您的程式碼 toouse 取得工作計數。

hello 取得工作計數作業不適用於批次服務版本早於 2017年-06-01.5.1。 如果您使用較舊版本的 hello 服務，然後改用清單查詢 toocount 工作中的工作。 如需詳細資訊，請參閱[有效率地建立查詢 toolist 批次資源](batch-efficient-list-queries.md)。

## <a name="next-steps"></a>後續步驟

* 請參閱 hello[批次功能概觀](batch-api-basics.md)toolearn 更多關於批次服務概念和功能。 hello 文章討論 hello 主要批次資源集區、 計算節點、 工作和工作，例如，並提供 hello 服務功能的概觀。
* 了解 hello 基本概念的開發批次啟用應用程式使用 hello[批次.NET 用戶端程式庫](batch-dotnet-get-started.md)或[Python](batch-python-tutorial.md)。 這些入門文件引導您完成使用 hello 批次服務 tooexecute 的工作應用程式工作負載在多個計算節點上。


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
