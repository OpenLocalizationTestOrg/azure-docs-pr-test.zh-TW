---
title: "資源使用量 API aaaTenant |Microsoft 文件"
description: "資源使用情況 API (用以擷取 Azure Stack 使用情況資訊) 的參考。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a>租用戶資源使用情況 API
租用戶可以使用 hello 租用戶 API tooview hello 租用戶專屬的資源使用狀況資料。 這個 API 已與 hello Azure 使用量 API 一致 （目前在私人預覽中）。

您可以使用 hello Windows PowerShell cmdlet **Get UsageAggregates** tooget 使用量資料會像在 Azure 中。

## <a name="api-call"></a>API 呼叫
### <a name="request"></a>要求
hello 要求取得耗用量詳細資料的 hello 要求訂用帳戶，以及 hello 要求的時間範圍。 沒有要求主體。

| **方法** | **要求 URI** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>引數
| **引數** | **說明** |
| --- | --- |
| *Armendpoint* |您 Azure Stack 環境的 Azure Resource Manager 端點。 hello Azure 堆疊的慣例是該 hello 名稱的 Azure 資源管理員端點的 hello 格式`https://management.{domain-name}`。 例如，如果 hello 網域名稱是 local.azurestack.external，則 hello 資源管理員端點是`https://management.local.azurestack.external`。 |
| *subId* |正在進行 hello 呼叫 hello 使用者訂用帳戶識別碼。 您可以使用此 API 只有 tooquery 單一訂用帳戶的使用方式。 提供者可以針對所有租用戶使用 hello 提供者資源使用量 API tooquery 使用方式。 |
| *reportedStartTime* |Hello 查詢的開始時間。 hello 值*DateTime*應該以 utc 格式且開頭 hello hello 小時的時間，例如： 13:00。 對於每日彙總，設定此值 tooUTC 午夜。 hello 格式是*逸出*ISO 8601，例如，2015年-06-16t18%3a53%3a11%2b00 %3a00z，其中冒號會逸出太 %3a 和加上逸出太 %2b，讓它變成易記的 URI。 |
| *reportedEndTime* |Hello 查詢的結束時間。 hello 太套用的條件約束*reportedStartTime*也適用於 toothis 引數。 hello 值*reportedEndTime*不可在未來的 hello。 |
| *aggregationGranularity* |這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。 Hello 值建議，其中在每日資料粒度，則傳回 hello 資料和其他 hello 是每小時的解析度。 hello 預設 hello 每日的選項。 |
| *api-version* |使用的 toomake hello 通訊協定版本此要求。 您必須使用 2015-06-01-preview。 |
| *continuationToken* |從 hello 最後一個呼叫 toohello 使用量 API 提供者擷取權杖。 回應大於 1000 行時就需要這個權杖，可作為進度的書籤。 如果不存在的話，會根據傳入的 hello 資料粒度的 hello 開頭的 hello 天或小時，從擷取資料的 hello。 |

### <a name="response"></a>Response
GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",

"name": "sub1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

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
| *subscriptionId* |Hello Azure 使用者的訂用帳戶識別碼 |
| *usageStartTime* |UTC 的開始時間 hello 這個使用方式彙總所屬的使用方式值區 toowhich |
| *usageEndTime* |UTC 結束時間的這個使用方式彙總所屬的 hello 使用量值區 toowhich |
| *instanceData* |執行個體詳細資料的機碼值組 (新格式)：<br>  *resourceUri*：完整資源識別碼，包含資源群組和執行個體名稱 <br>  *location*：此服務執行所在的區域 <br>  *標記*： 該 hello 使用者所指定的資源標記 <br>  *additionalInfo*： 更詳細 hello 資源耗用，例如作業系統版本或映像類型 |
| *quantity* |此時間範圍內發生的資源取用數量 |
| *meterId* |所耗用的 hello 資源的唯一識別碼 (也稱為*ResourceID*) |

## <a name="next-steps"></a>後續步驟
[提供者資源使用狀況 API](azure-stack-provider-resource-api.md)

[使用狀況相關常見問題集](azure-stack-usage-related-faq.md)

