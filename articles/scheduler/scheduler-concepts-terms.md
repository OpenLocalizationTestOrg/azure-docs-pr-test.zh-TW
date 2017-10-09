---
title: "aaaScheduler 概念、 詞彙，以及實體 |Microsoft 文件"
description: "Azure 排程器概念、詞彙及實體階層，包括工作和工作集合。  顯示排程工作的完整範例。"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>排程器概念、術語及實體階層
## <a name="scheduler-entity-hierarchy"></a>排程器實體階層
hello 下表描述公開或使用排程器 API hello hello 主要資源：

| 資源 | 說明 |
| --- | --- |
| **工作集合** |工作集合包含的工作群組，並維護設定、 配額及流速 hello 集合內的工作所共用的。 作業集合是由訂用帳戶擁有者和群組工作一起根據使用方式或應用程式界限所建立的。 它是受條件約束的 tooone 區域。 它也可讓 hello 強制執行配額 tooconstrain hello 使用量的所有工作在該集合中。 hello 配額包含 MaxJobs 和 MaxRecurrence。 |
| **作業** |工作定義單一週期動作，以及簡單或複雜的執行策略。 動作可能包括 HTTP、儲存體佇列、服務匯流排佇列或服務匯流排主題要求。 |
| **工作歷程記錄** |工作歷程記錄代表工作的執行詳細資料。 它包含成功與失敗，以及任何回應詳細資料。 |

## <a name="scheduler-entity-management"></a>排程器實體管理
在高層級，hello 排程器和 hello 服務管理 API 會公開下列 hello 資源執行作業的 hello:

| 功能 | 描述和 URI 位址 |
| --- | --- |
| **工作集合管理** |GET、 PUT 和 DELETE 支援建立和修改工作集合和內含的 hello 工作。 工作集合是工作的容器，並將對應 tooquotas 和共用的設定。 稍後所述的配額範例為最大工作數目和最小週期間隔。 <p>PUT 和 DELETE：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **工作管理** |GET、PUT、POST、PATCH 和 DELETE 支援建立和修改雲端服務。 所有工作必須都屬於 tooa 工作集合已存在，因此沒有隱含建立。 <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **工作歷程記錄管理** |GET 支援擷取 60 天的工作執行歷程記錄，例如工作經歷時間和工作執行結果。 加入根據狀況和狀態篩選的查詢字串參數支援。 <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>工作類型
工作有多種類型︰HTTP 工作 (包括支援 SSL 的 HTTPS 工作)、儲存體佇列工作、服務匯流排佇列工作和服務匯流排主題工作。 如果您有現有的工作負載或服務的端點，則 HTTP 工作是理想的工作。 您可以使用儲存體佇列工作 toopost 訊息 toostorage 佇列，讓這些工作都適合用來儲存體佇列的工作負載。 同樣地，服務匯流排工作很適合用於使用服務匯流排佇列和主題的工作負載。

## <a name="hello-job-entity-in-detail"></a>在詳細資料中的 hello 「 工作 」 實體
在基本層級中，排程工作有幾個部分：

* hello 動作 tooperform hello 工作計時器啟動時  
* （選擇性） hello 時間 toorun hello 工作  
* （選擇性）時間和頻率 toorepeat hello 工作  
* （選擇性）動作 toofire hello 主要動作失敗時  

就內部而言，排程的工作也會包含系統提供的資料，例如 hello 下次排程執行時間。

下列程式碼的 hello 提供排程工作的完整範例。 後續章節將提供詳細資料。

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

Hello 範例排程工作上面所示，工作定義會有幾個部分：

* 開始時間 ("startTime")  
* 動作 ("action")，其中包含錯誤動作 ("errorAction")
* 週期 ("recurrence")  
* 狀況 (“state”)  
* 狀態 (“status”)  
* 重試原則 ("retryPolicy")  

讓我們詳細檢查每一種方式：

## <a name="starttime"></a>startTime
hello"startTime"是 hello 開始時間和時區時差中的 hello 網路上允許 hello 呼叫端 toospecify [ISO 8601 格式](http://en.wikipedia.org/wiki/ISO_8601)。

## <a name="action-and-erroraction"></a>action 和 errorAction
hello 「 動作 」 是每次叫用的 hello 動作，並描述服務叫用類型。 hello 動作是 hello 提供排程上可執行的內容。 排程器支援 HTTP、儲存體佇列、服務匯流排主題和服務匯流排佇列動作。

在上面的 hello 範例中的 hello 動作是 HTTP 動作。 以下是儲存體佇列動作的範例：

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

以下是服務匯流排主題動作的範例。

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

以下是服務匯流排佇列動作的範例：

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

hello"errorAction"是 hello 錯誤處理常式，hello hello 主要動作失敗時叫用的動作。 您可以使用此變數 toocall 錯誤處理端點，或傳送使用者通知。 這適用於該 hello 達到 hello 案例中的次要端點主要無法使用 （例如，在 hello 案例中損毀 hello 端點的站台時） 或可以用來通知錯誤處理端點。 如同主要動作 hello，hello 錯誤動作可以是根據其他動作的簡單或複合邏輯。 如何 toocreate SAS 權杖，參照太 toolearn[建立和使用共用存取簽章](https://msdn.microsoft.com/library/azure/jj721951.aspx)。

## <a name="recurrence"></a>週期
週期具有數個部分：

* 頻率：分鐘、小時、天、週、月、年的其中一個  
* 間隔： Hello 給 hello 循環頻率間隔  
* 指定的排程： 指定分鐘、 小時、 工作日、 月和間 hello 循環  
* 計數：週期的計數  
* 結束時間： hello 指定結束時間之後，會執行任何工作  

如果工作已在其 JSON 定義中指定週期物件，則工作會重複執行。 如果指定 count 和 endTime，被採用先發生的 hello 完成規則。

## <a name="state"></a>state
hello hello 工作狀態是四個值之一： 啟用、 停用、 已完成，或是發生錯誤。 您可以放入或修補程式的工作，為 tooupdate 它們 toohello 啟用或停用狀態。 如果作業已完成或發生錯誤，也就是最後的狀態，無法更新 （但仍可刪除 hello 作業）。 Hello 狀態屬性的範例如下所示：

        "state": "disabled", // enabled, disabled, completed, or faulted
已完成和發生錯誤的工作會在 60 天後刪除。

## <a name="status"></a>status
排程器工作啟動之後，將會傳回 hello hello 工作目前狀態的相關資訊。 此物件不是由 hello 使用者可設定 — hello 系統設定。 不過，它包含在 hello 工作物件 （而非個別連結的資源），使其中一個可以輕鬆地取得 hello 工作的狀態。

工作狀態包含 hello hello 先前執行時 （如果有的話），hello hello 下一個排程的執行 （適用於進行中作業） 的時間與 hello 作業 hello 執行計數。

## <a name="retrypolicy"></a>RetryPolicy
如果排程器工作失敗，則可能 toospecify 是否及如何 hello 動作重試一次重試原則 toodetermine。 這由 hello **retryType**物件 — 設定得**無**如果沒有重試原則，如上所示。 設定得**固定**如果重試原則。

tooset 重試原則，可指定其他兩個設定： 重試間隔 (**retryInterval**) 和 hello 重試次數 (**retryCount**)。

指定以 hello 的 hello 重試間隔**retryInterval**物件，為 hello 重試間隔。 其預設值為 30 秒、最小可設定值為 15 秒，而最大值為 18 個月。 免費作業集合中作業的最小可設定值為 1 小時。  它被定義在 hello ISO 8601 格式。 同樣地，指定 hello hello 重試次數值，以 hello **retryCount**物件; 它是嘗試重試的 hello 次數。 其預設值為 4，且其最大值 20\。 同時**retryInterval**和**retryCount**是選擇性的。 如果會指定其預設值**retryType**設定得**固定**和明確指定任何值。

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [排程 toobuild 複雜的方式與進階循環使用 Azure 排程器](scheduler-advanced-complexity.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

