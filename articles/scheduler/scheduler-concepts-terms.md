---
title: "排程器概念、條款和實體 | Microsoft Docs"
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
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>排程器概念、術語及實體階層
## <a name="scheduler-entity-hierarchy"></a>排程器實體階層
下表描述排程器 API 所公開或使用的主要資源：

| 資源 | 說明 |
| --- | --- |
| **工作集合** |工作集合包含工作群組，並維護集合內工作所共用的設定、配額及節流。 作業集合是由訂用帳戶擁有者和群組工作一起根據使用方式或應用程式界限所建立的。 它受限於一個區域。 它也允許強制執行配額，以限制該集合中所有工作的使用方式。 配額包含 MaxJobs 和 MaxRecurrence。 |
| **作業** |工作定義單一週期動作，以及簡單或複雜的執行策略。 動作可能包括 HTTP、儲存體佇列、服務匯流排佇列或服務匯流排主題要求。 |
| **工作歷程記錄** |工作歷程記錄代表工作的執行詳細資料。 它包含成功與失敗，以及任何回應詳細資料。 |

## <a name="scheduler-entity-management"></a>排程器實體管理
在高階中，排程器和服務管理 API 會在資源上公開下列作業：

| 功能 | 描述和 URI 位址 |
| --- | --- |
| **工作集合管理** |GET、PUT 和 DELETE 支援建立和修改工作集合及其內含的工作。 工作集合是工作的容器，並對應至配額和共用設定。 稍後所述的配額範例為最大工作數目和最小週期間隔。 <p>PUT 和 DELETE：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET：`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **工作管理** |GET、PUT、POST、PATCH 和 DELETE 支援建立和修改雲端服務。 所有工作都必須屬於已存在的工作集合，因此沒有隱含的建立。 <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **工作歷程記錄管理** |GET 支援擷取 60 天的工作執行歷程記錄，例如工作經歷時間和工作執行結果。 加入根據狀況和狀態篩選的查詢字串參數支援。 <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>工作類型
工作有多種類型︰HTTP 工作 (包括支援 SSL 的 HTTPS 工作)、儲存體佇列工作、服務匯流排佇列工作和服務匯流排主題工作。 如果您有現有的工作負載或服務的端點，則 HTTP 工作是理想的工作。 您可使用儲存體佇列工作將訊息公佈至儲存體佇列，因此那些工作非常適用於使用儲存體佇列的工作負載。 同樣地，服務匯流排工作很適合用於使用服務匯流排佇列和主題的工作負載。

## <a name="the-job-entity-in-detail"></a>詳細的「工作」實體
在基本層級中，排程工作有幾個部分：

* 要在工作計時器啟動時執行的動作  
* (選用) 執行工作的時間  
* (選用) 重複工作的時機和頻率  
* (選用) 主要動作失敗時要啟動的動作  

在內部，排定的工作也會包含系統提供的資料，例如下次排定的執行時間。

下列程式碼提供排程工作的完整範例。 後續章節將提供詳細資料。

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
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
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

如同上述範例排程器工作中所見，工作定義具有數個部分：

* 開始時間 ("startTime")  
* 動作 ("action")，其中包含錯誤動作 ("errorAction")
* 週期 ("recurrence")  
* 狀況 (“state”)  
* 狀態 (“status”)  
* 重試原則 ("retryPolicy")  

讓我們詳細檢查每一種方式：

## <a name="starttime"></a>startTime
"startTime" 是開始時間，可讓呼叫者以 [ISO 8601 格式](http://en.wikipedia.org/wiki/ISO_8601)指定線路上的時區位移。

## <a name="action-and-erroraction"></a>action 和 errorAction
“action” 是每次發生時叫用的動作，並描述服務叫用的類型。 動作是將在提供的排程上執行的動作。 排程器支援 HTTP、儲存體佇列、服務匯流排主題和服務匯流排佇列動作。

上述範例中的動作是 HTTP 動作。 以下是儲存體佇列動作的範例：

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

"errorAction" 是錯誤處理常式，即主要動作失敗時叫用的動作。 您可以使用這個變數，呼叫錯誤處理端點或傳送使用者通知。 如果主要端點無法使用 (例如端點的網站發生重大災難)，則這可用於連接次要端點，或可以用於通知錯誤處理端點。 如同主要動作，錯誤動作可以是根據其他動作的簡單或複合邏輯。 若要了解如何建立 SAS 權杖，請參閱 [建立和使用共用存取簽章](https://msdn.microsoft.com/library/azure/jj721951.aspx)。

## <a name="recurrence"></a>週期
週期具有數個部分：

* 頻率：分鐘、小時、天、週、月、年的其中一個  
* 間隔：週期特定頻率的間隔  
* 指定的排程：指定週期的分鐘、小時、工作日、月和月日  
* 計數：週期的計數  
* 結束時間：沒有工作將在指定的結束時間之後執行  

如果工作已在其 JSON 定義中指定週期物件，則工作會重複執行。 如果同時指定 count 和 endTime，則會遵守最先發生的完成規則。

## <a name="state"></a>state
工作的狀況是四個值之一：enabled、disabled、completed 或 faulted。 您可以 PUT 或 PATCH 工作，將它們更新為 enabled 或 disabled 狀況。 如果工作已完成或發生錯誤，這是無法更新的最終狀況 (雖然仍可刪除工作)。 state 屬性的範例如下：

        "state": "disabled", // enabled, disabled, completed, or faulted
已完成和發生錯誤的工作會在 60 天後刪除。

## <a name="status"></a>status
啟動排程器工作後，就會傳回目前工作狀態的相關資訊。 這個物件無法由使用者設定 – 它是由系統設定。 不過，它包含在工作物件 (而不是個別連結的資源)，以便可以輕鬆地取得工作的狀態。

工作狀態包含上次執行的時間 (如果有的話)、下次排定的執行時間 (適用於進行中工作)，以及工作的執行計數。

## <a name="retrypolicy"></a>RetryPolicy
如果排程器工作失敗，則可以指定重試原則，以判斷是否及如何重試動作。 這取決於 **retryType** 物件 – 如果沒有重試原則，則它會設定為 **none**，如上所示。 如果有重試原則，請將它設定為 **fixed** 。

若要設定重試原則，可以指定另外兩項設定：重試間隔 (**retryInterval**) 和重試次數 (**retryCount**)。

搭配 **retryInterval** 物件指定的重試間隔是重試的間隔。 其預設值為 30 秒、最小可設定值為 15 秒，而最大值為 18 個月。 免費作業集合中作業的最小可設定值為 1 小時。  它是以 ISO 8601 格式定義。 同樣地，搭配 **retryCount** 物件指定的重試次數值，它是重試的次數。 其預設值為 4，而最大值為 20。 **retryInterval** 和 **retryCount** 都是選擇性的。 如果 **retryType** 設定為 **fixed**，而且未明確地指定任何值，則會給與它們預設值。

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [在 Azure 入口網站中開始使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [如何使用 Azure 排程器建立複雜的排程和進階週期](scheduler-advanced-complexity.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

