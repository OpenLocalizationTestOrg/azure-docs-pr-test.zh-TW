---
title: "aaa\"Azure 批次工作開始事件 |Microsoft 文件 」"
description: "Batch 工作開始事件的參考。"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>工作開始事件

 此事件就會發出工作已排定的 toostart 計算節點上後，由 hello 排程器。 請注意，是否 hello 將工作重試或排入佇列將會發出這個事件一次 hello 相同的工作，但 hello 重試計數和系統工作的版本會隨之更新。


 hello 下列範例顯示 hello 主體工作開始事件。

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
        "retryCount": 0
    }
}
```

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|jobId|String|hello hello 作業包含 hello 工作識別碼。|
|id|String|hello hello 工作識別碼。|
|taskType|String|hello hello 工作類型。 可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。|
|systemTaskVersion|Int32|這是在工作上的 hello 內部重試計數器。 在內部 hello 批次服務可以重試工作 tooaccount 暫時性的問題。 這些問題可以包含內部排程錯誤或嘗試 toorecover 從運算節點處於錯誤狀態。|
|[nodeInfo](#nodeInfo)|複雜類型|包含 hello 計算節點的 hello 工作已執行的相關資訊。|
|[multiInstanceSettings](#multiInstanceSettings)|複雜類型|指定該 hello 工作需要多個計算節點的多個執行個體工作。  請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。|
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
|numberOfInstances|int|hello hello 工作所需的運算節點數目。|

###  <a name="constraints"></a> constraints

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|hello hello 工作可能會重試的次數上限。 如果它的結束代碼是非零值 hello 批次服務會重試工作。<br /><br /> 請注意，這個值會特別控制 hello 重試次數。 hello 批次服務將嘗試 hello 工作一次，並重試可能向上 toothis 限制。 例如，如果 hello 最大重試計數為 3，批次會嘗試向上 too4 時間 （一個初始再試一次和重試 3 次） 的工作。<br /><br /> 如果 hello 最大重試計數為 0，hello 批次服務不會重試工作。<br /><br /> 如果 hello 重試次數上限為-1，hello 批次服務將重試無限制的工作。<br /><br /> hello 預設值為 0 （無重試）。|

###  <a name="executionInfo"></a> executionInfo

|元素名稱|類型|注意事項|
|------------------|----------|-----------|
|retryCount|Int32|hello hello 工作已 hello 批次服務重試次數。 如果它，則為非零結束代碼，結束 toohello 上指定的 MaxTaskRetryCount，則重試 hello 工作|
