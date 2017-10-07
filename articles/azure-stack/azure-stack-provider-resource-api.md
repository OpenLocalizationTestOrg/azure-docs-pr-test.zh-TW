---
title: "資源使用量 API aaaProvider |Microsoft 文件"
description: "資源使用情況 API (用以擷取 Azure Stack 使用情況資訊) 的參考。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 7cc2d7af27e6abc86e247b2ed0ab1bc236fdb1af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provider-resource-usage-api"></a>提供者資源使用狀況 API
hello 詞彙提供者適用於 toohello 服務系統管理員和委派 tooany 提供者。 服務系統管理員和委派的提供者可以使用其直接租用戶的提供者使用量 API tooview hello 使用方式。 例如，P0 可以呼叫 hello 提供者 API tooget 使用量資訊上的 P1 和 P2 的直接使用，而且 P1 可以呼叫 P3 和第 4 頁上的使用方式資訊。

![提供者階層的概念模型](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>API 呼叫參考
### <a name="request"></a>要求
hello 要求取得耗用量詳細資料的 hello 要求訂用帳戶，以及 hello 要求的時間範圍。 沒有要求主體。

這個應用程式開發介面的使用方式是提供者 API，因此 hello 呼叫端必須指派 hello 提供者的訂用帳戶中的擁有者、 參與者或讀取器角色。

| **方法** | **要求 URI** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>引數
| **引數** | **說明** |
| --- | --- |
| *armendpoint* |您 Azure Stack 環境的 Azure Resource Manager 端點。 hello Azure 堆疊的慣例是該 hello 名稱的 Azure 資源管理員端點的 hello 格式`https://adminmanagement.{domain-name}`。 例如，如果 hello 網域名稱是 local.azurestack.external，則 hello 資源管理員端點是`https://adminmanagement.local.azurestack.external`。 |
| *subId* |正在進行 hello 呼叫 hello 使用者訂用帳戶識別碼。 |
| *reportedStartTime* |Hello 查詢的開始時間。 hello 值*DateTime*應該以 utc 格式且開頭 hello hello 小時的時間，例如： 13:00。 對於每日彙總，設定此值 tooUTC 午夜。 hello 格式是*逸出*ISO 8601，例如，2015年-06-16t18%3a53%3a11%2b00 %3a00z，其中冒號會逸出太 %3a 和加上逸出太 %2b，讓它變成易記的 URI。 |
| *reportedEndTime* |Hello 查詢的結束時間。 hello 太套用的條件約束*reportedStartTime*也適用於 toothis 引數。 hello 值*reportedEndTime*不可在未來的 hello 或 hello 目前的日期。 如果是，hello 結果設定太 「 處理不完整。 」 |
| *aggregationGranularity* |這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。 Hello 值建議，其中在每日資料粒度，則傳回 hello 資料和其他 hello 是每小時的解析度。 hello 預設 hello 每日的選項。 |
| *subscriberId* |訂用帳戶 ID。 tooget 已篩選資料，無須 hello 的直接 hello 提供者的租用戶的訂用帳戶 ID。 如果訂用帳戶 ID 未不指定任何參數，hello 呼叫就會傳回所有 hello 提供者的直接租用戶使用量資料。 |
| *api-version* |使用的 toomake hello 通訊協定版本此要求。 這個值會設定 too2015-06-01-預覽。 |
| *continuationToken* |從 hello 最後一個呼叫 toohello 使用量 API 提供者擷取權杖。 回應是大於 1000 的行，它做為 hello 進度的書籤時，就需要這個語彙基元。 如果不存在的話，會根據傳入的 hello 資料粒度的 hello 開頭的 hello 天或小時，從擷取資料的 hello。 |

### <a name="response"></a>Response
GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1",

"name": "sub1.1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1.1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\

":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

"quantity":2.4000000000,

"meterId":"meterID1"

}

},

…

### <a name="response-details"></a>回應詳細資料
| **引數** | **說明** |
| --- | --- |
| *id* |Hello 的彙總使用方式的唯一識別碼 |
| *name* |Hello 使用量彙總名稱 |
| *type* |資源定義 |
| *subscriptionId* |Hello Azure 堆疊使用者訂用帳戶識別碼 |
| *usageStartTime* |UTC 的開始時間 hello 這個使用方式彙總所屬的使用方式值區 toowhich |
| *usageEndTime* |UTC 結束時間的這個使用方式彙總所屬的 hello 使用量值區 toowhich |
| *instanceData* |執行個體詳細資料的機碼值組 (新格式)：<br> *resourceUri*： 完整資源識別碼，其中包括 hello 資源群組和 hello 執行個體名稱 <br> *location*：此服務執行所在的區域 <br> *標記*: hello 使用者所指定資源標記 <br> *additionalInfo*： 更詳細 hello 資源耗用，例如作業系統版本或映像類型 |
| *quantity* |此時間範圍內發生的資源取用數量 |
| *meterId* |所耗用的 hello 資源的唯一識別碼 (也稱為*ResourceID*) |

## <a name="next-steps"></a>後續步驟
[租用戶資源使用狀況 API 參考](azure-stack-tenant-resource-usage-api.md)

[使用狀況相關常見問題集](azure-stack-usage-related-faq.md)

