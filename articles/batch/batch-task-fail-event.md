---
title: "aaa\"Azure 批次工作失敗事件 |Microsoft 文件 」"
description: "Batch 工作失敗事件的參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: e92604671650900072ba27f807501b704329e865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-fail-event"></a>工作失敗事件

 當工作未成功完成時，就會發出此事件。 目前所有非零的結束代碼皆視為失敗。 會發出這個事件*除了*工作完成事件，而且可以是使用的 toodetect，工作失敗時。


 hello 下列範例顯示 hello 工作主體失敗事件。

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|jobId|String|hello hello 作業包含 hello 工作識別碼。|
|id|String|hello hello 工作識別碼。|
|taskType|String|hello hello 工作類型。 可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。 對於作業準備工作、作業發行工作或開始工作。不會發出此事件。|
|systemTaskVersion|Int32|這是在工作上的 hello 內部重試計數器。 在內部 hello 批次服務可以重試工作 tooaccount 暫時性的問題。 這些問題可以包含內部排程錯誤或嘗試 toorecover 從運算節點處於錯誤狀態。|
|[nodeInfo](#nodeInfo)|複雜類型|包含 hello 計算節點的 hello 工作已執行的相關資訊。|
|[multiInstanceSettings](#multiInstanceSettings)|複雜類型|指定該 hello 工作是多個執行個體工作需要多個計算節點。  請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。|
|[constraints](#constraints)|複雜類型|套用 toothis 工作 hello 執行條件約束。|
|[executionInfo](#executionInfo)|複雜類型|包含有關 hello hello 工作執行資訊。|

###  <a name="nodeInfo"></a> nodeInfo

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|poolId|String|hello hello 集區的 hello 工作已執行識別碼。|
|nodeId|String|hello hello 節點的 hello 工作已執行識別碼。|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|numberOfInstances|Int32|hello hello 工作所需的運算節點數目。|

###  <a name="constraints"></a> constraints

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|hello hello 工作可能會重試的次數上限。 如果它的結束代碼是非零值 hello 批次服務會重試工作。<br /><br /> 請注意，這個值會特別控制 hello 重試次數。 hello 批次服務將嘗試 hello 工作一次，並重試可能向上 toothis 限制。 例如，如果 hello 最大重試計數為 3，批次會嘗試向上 too4 時間 （一個初始再試一次和重試 3 次） 的工作。<br /><br /> 如果 hello 最大重試計數為 0，hello 批次服務不會重試工作。<br /><br /> 如果 hello 重試次數上限為-1，hello 批次服務將重試無限制的工作。<br /><br /> hello 預設值為 0 （無重試）。|


###  <a name="executionInfo"></a> executionInfo

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|startTime|DateTime|hello 開始執行的 hello 工作時間。 「 執行中 」 對應 toohello**執行**狀態，因此如果 hello 工作指定資源檔或應用程式封裝，然後 hello 開始時間就會反映 hello 啟動下載或部署這些哪個 hello 工作時間。  如果已重新啟動或重試 hello 工作，這是的 hello 最近一次在哪個 hello 工作開始執行。|
|EndTime|DateTime|hello hello 任務完成時間。|
|exitCode|Int32|hello hello 工作的結束代碼。|
|retryCount|Int32|hello hello 工作已 hello 批次服務重試次數。 它會結束，則為非零結束代碼，向上 toohello 指定 MaxTaskRetryCount 重試 hello 工作。|
|requeueCount|Int32|hello 的 hello 導致使用者要求 hello 工作排 hello 批次服務的次數。<br /><br /> 當 hello 使用者移除節點從集區 （調整大小或壓縮 hello 共用） 或 hello 作業時已停用，hello 使用者可以指定執行工作 hello 節點上執行排入佇列。 這個計數會追蹤多少次已排入佇列 hello 工作基於這些理由。|
