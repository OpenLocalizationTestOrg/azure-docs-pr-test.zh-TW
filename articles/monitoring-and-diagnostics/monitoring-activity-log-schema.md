---
title: "aaaAzure 活動記錄檔事件結構描述 |Microsoft 文件"
description: "了解 hello 事件結構描述的資料發出到 hello 活動記錄檔"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Azure 活動記錄事件結構描述
hello **Azure 活動記錄檔**是提供深入了解 Azure 中所發生的任何訂用帳戶層級事件的記錄。 本文說明 hello 事件結構描述，每個分類的資料。

## <a name="administrative"></a>管理
這個類別所包含的所有 hello 記錄建立、 更新、 刪除和動作的作業執行透過資源管理員。 Hello 類型的事件，您會看到此類別中包含的範例 「 建立虛擬機器 」 和 「 刪除網路安全性群組 」 每個使用者所採取的動作，或使用資源管理員的應用程式會模型化為特定資源類型上的作業。 如果 hello 作業類型是寫入刪除或動作，hello 記錄 hello 開始和成功或失敗的作業都會記錄在 hello 系統管理類別。 hello 系統管理類別也會包含在訂閱中的任何變更 toorole 型存取控制。

### <a name="sample-event"></a>範例事件
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>屬性描述
| 元素名稱 | 說明 |
| --- | --- |
| 授權 |Blob hello 事件的 RBAC 屬性。 通常包含 hello 「 動作 」、 「 角色 」 和 「 範圍 」 屬性。 |
| 呼叫者 |已執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的電子郵件地址。 |
| 通道 |Hello 下列值之一: 「 系統管理 」、 「 作業 」 |
| claims |hello JWT token 是由 Active Directory tooauthenticate hello 使用者或應用程式 tooperform 資源管理員中的這項作業。 |
| correlationId |通常是 hello 字串格式 GUID。 共用的相互關聯識別碼的事件屬於 toohello 相同超級動作。 |
| 說明 |事件的靜態文字描述。 |
| eventDataId |事件的唯一識別碼。 |
| httpRequest |Blob 描述 hello Http 要求。 通常包括 hello"clientRequestId"、"clientIpAddress"和"method"（HTTP 方法。 例如，PUT)。 |
| 層級 |Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」 |
| resourceGroupName |Hello hello 資源群組名稱會影響資源。 |
| resourceProviderName |Hello hello 資源提供者的名稱會影響資源 |
| resourceId |資源識別碼 hello 影響資源。 |
| operationId |GUID 對應 tooa 單一作業的 hello 事件之間共用。 |
| operationName |Hello 作業的名稱。 |
| 屬性 |一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。 |
| status |描述 hello hello 作業狀態的字串。 常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。 |
| 子狀態 |通常 hello hello 對應 REST 呼叫的 HTTP 狀態碼，但也可能包含其他描述子狀態，例如這些常見的值的字串: [確定] (HTTP 狀態碼： 200)，建立 (HTTP 狀態碼： 201)、 接受 (HTTP 狀態碼： 202)，無內容 (HTTP狀態碼： 204)，不正確的要求 (HTTP 狀態碼： 400)、 找不到 (HTTP 狀態碼： 404)，衝突 (HTTP 狀態碼： 409)，內部伺服器錯誤 (HTTP 狀態碼： 500)，則 Service 無法使用 (HTTP 狀態碼： 503)，閘道逾時 (HTTP 狀態碼： 504)。 |
| eventTimestamp |Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。 |
| submissionTimestamp |時間戳記 hello 事件變成可供查詢。 |
| subscriptionId |Azure 訂用帳戶識別碼。 |

## <a name="service-health"></a>服務健康情況
這個類別所包含任何服務健全狀況事件發生在 Azure 中的 hello 的記錄。 舉例來說，hello 您將會看到此類別中類型是事件的"SQL Azure，在美國東部發生停機。 」 服務健全狀況事件有五種： 所需的動作、 協助復原、 事件、 維護、 資訊或安全性，和，才會出現您擁有 hello 訂用帳戶會受到 hello 事件中的資源。

### <a name="sample-event"></a>範例事件
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>屬性描述
元素名稱 | 說明
-------- | -----------
通道 | 是 hello 下列值之一: 「 系統管理 」、 「 作業 」
correlationId | 通常是 hello 字串格式的 GUID。 事件與屬於相同超級動作通常會共用的 toohello hello 相同的相互關聯識別碼。
說明 | Hello 事件的描述。
eventDataId | hello 事件的唯一識別項。
eventName | hello hello 事件標題。
層級 | Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」
resourceProviderName | Hello hello 資源提供者的名稱會影響資源。 如果未知，此參數會是 null。
resourceType| 資源的 hello hello 類型會影響資源。 如果未知，此參數會是 null。
子狀態 | 針對服務健康情況事件通常為 null。
eventTimestamp | 時間戳記 hello 記錄事件產生並提交 toohello 活動記錄檔。
submissionTimestamp |   時間戳記 hello 事件變成可在 hello 活動記錄檔中。
subscriptionId | hello 記錄這個事件的 Azure 訂用帳戶。
status | 描述 hello hello 作業狀態的字串。 某些常見的值為：Active、Resolved。
operationName | Hello 作業的名稱。 通常是 Microsoft.ServiceHealth/incident/action。
category | "ServiceHealth"
resourceId | 如果已知資源識別碼 hello 會影響資源。 否則會提供訂用帳戶識別碼。
Properties.title | 此通訊的 hello 當地語系化標題。 英文是 hello 預設語言。
Properties.communication | hello 當地語系化 hello 通訊以 HTML 標記的詳細資料。 英文是 hello 預設值。
Properties.incidentType | 可能的值：AssistedRecovery、ActionRequired、Information、Incident、Maintenance、Security
Properties.trackingId | 識別此事件相關聯的 hello 事件。 使用此 toocorrelate hello 事件相關的 tooan 事件。
Properties.impactedServices | 逸出的 JSON blob hello 服務和區域 hello 事件受影響的描述。 Services 清單 (每一份都有 ServiceName) 和 ImpactedRegions 清單 (每一份都有 RegionName)。
Properties.defaultLanguageTitle | 英文版的 hello 通訊
Properties.defaultLanguageContent | 做為 html 標記或純文字的英文版的 hello 通訊
Properties.stage | AssistedRecovery、ActionRequired、Information、Incident、Security 的可能值：Active、Resolved。 Maintenance 的可能值︰Active、Planned、InProgress、Canceled、Rescheduled、Resolved、Complete
Properties.communicationId | hello 通訊此事件是相關聯。

## <a name="alert"></a>警示
這個類別所包含所有啟用的 Azure 警示 hello 的記錄。 Hello 您將會看到此類別中類型的範例是事件的"myVM 上的 CPU 百分比已超過 80 hello 過去 5 分鐘。 」 各種 Azure 系統都有警示概念，您可以定義某種類型的規則，並在條件符合該規則時接收通知。 每次支援 Azure 的警示類型 '啟動，' 或 hello 條件都符合的 toogenerate 通知，hello 啟用的記錄也會推入 toothis 類別目錄的 hello 活動記錄檔。

### <a name="sample-event"></a>範例事件

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>屬性描述
| 元素名稱 | 說明 |
| --- | --- |
| 呼叫者 | 一律是 Microsoft.Insights/alertRules |
| 通道 | 一律是 “Admin, Operation” |
| claims | JSON 的 hello 警示引擎 hello SPN （服務主體的名稱） 或資源類型的 blob。 |
| correlationId | Hello 字串格式的 GUID。 |
| 說明 |Hello 警示事件的靜態文字描述。 |
| eventDataId |Hello 警示事件的唯一識別碼。 |
| 層級 |Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」 |
| resourceGroupName |Hello hello 資源群組名稱會影響資源是否度量的警示。 對於其他警示類型，這是 hello hello 包含本身 hello 警示的資源群組名稱。 |
| resourceProviderName |Hello hello 資源提供者的名稱會影響資源是否度量的警示。 對於其他警示類型，這是 hello hello 資源提供者名稱本身 hello 警示。 |
| resourceId | Hello hello 資源 ID 的名稱會影響資源是否度量的警示。 對於其他警示類型，這是 hello hello 警示資源本身的資源識別碼。 |
| operationId |GUID 對應 tooa 單一作業的 hello 事件之間共用。 |
| operationName |Hello 作業的名稱。 |
| 屬性 |一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。 |
| status |描述 hello hello 作業狀態的字串。 常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。 |
| 子狀態 | 針對警示通常為 null。 |
| eventTimestamp |Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。 |
| submissionTimestamp |時間戳記 hello 事件變成可供查詢。 |
| subscriptionId |Azure 訂用帳戶識別碼。 |

### <a name="properties-field-per-alert-type"></a>每個警示類型的屬性欄位
hello 屬性] 欄位會包含根據 hello 事件來源的 hello 警示有不同的值。 兩個常見的警示事件提供者為活動記錄警示和計量警示。

#### <a name="properties-for-activity-log-alerts"></a>活動記錄警示的屬性
| 元素名稱 | 說明 |
| --- | --- |
| properties.subscriptionId | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 訂用帳戶 ID。 |
| properties.eventDataId | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe 事件資料識別碼 hello。 |
| properties.resourceGroup | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 資源群組。 |
| properties.resourceId | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 資源識別碼。 |
| properties.eventTimestamp | hello 導致啟動此活動記錄檔的警示規則 toobe hello 活動記錄檔事件的事件時間戳記。 |
| properties.operationName | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 作業名稱。 |
| properties.status | 從 hello 活動記錄檔事件導致啟動此活動記錄檔的警示規則 toobe hello 狀態。|

#### <a name="properties-for-metric-alerts"></a>計量警示屬性
| 元素名稱 | 說明 |
| --- | --- |
| properties.RuleUri | Hello 度量的警示規則本身的資源識別碼。 |
| properties.RuleName | hello hello 度量的警示規則名稱。 |
| properties.RuleDescription | hello hello 度量警示的規則 （如 hello 警示規則中所定義） 的描述。 |
| properties.Threshold | hello hello 評估 hello 度量的警示規則中使用的臨界值。 |
| properties.WindowSizeInMinutes | 使用 hello 評估 hello 度量的警示規則中的 hello 視窗大小。 |
| properties.Aggregation | hello hello 度量的警示規則中所定義的彙總類型。 |
| properties.Operator | hello hello 評估 hello 度量的警示規則中使用條件式的運算子。 |
| properties.MetricName | 使用 hello 評估 hello 度量的警示規則中的 hello 度量 hello 度量名稱。 |
| properties.MetricUnit | 使用 hello 評估 hello 度量的警示規則中的 hello 度量 hello 度量單位。 |

## <a name="autoscale"></a>Autoscale
這個類別包含 hello 作業的記錄任何事件相關的 toohello hello 自動調整引擎根據您定義您的訂用帳戶中的任何自動調整規模設定。 Hello 您將會看到此類別中類型的範例是事件的 「 自動調整規模小數位數設定動作失敗。 」 使用自動調整規模，您可以自動向外擴充或調整在 hello 中支援的資源類型的執行個體的數目會根據使用自動調整規模設定的日期和/或負載 （標準） 的資料的時間。 Hello 條件符合時 tooscale 向上或向下 hello 開始，並成功或失敗的事件會記錄在此類別。

### <a name="sample-event"></a>範例事件
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>屬性描述
| 元素名稱 | 說明 |
| --- | --- |
| 呼叫者 | 一律是 Microsoft.Insights/autoscaleSettings |
| 通道 | 一律是 “Admin, Operation” |
| claims | JSON hello SPN （服務主體的名稱） 或資源的類型，hello 自動調整引擎的 blob。 |
| correlationId | Hello 字串格式的 GUID。 |
| 說明 |Hello 自動調整事件的靜態文字描述。 |
| eventDataId |Hello 自動調整事件的唯一識別碼。 |
| 層級 |Hello 事件層級。 Hello 下列值之一: 「 重大 」、 「 錯誤 」、 「 警告 」、 「 資訊 」 及 「 詳細資訊 」 |
| resourceGroupName |Hello 自動調整規模設定 hello 資源群組名稱。 |
| resourceProviderName |Hello 自動調整規模設定 hello 資源提供者名稱。 |
| resourceId |資源識別碼 hello 自動調整規模設定。 |
| operationId |GUID 對應 tooa 單一作業的 hello 事件之間共用。 |
| operationName |Hello 作業的名稱。 |
| 屬性 |一組`<Key, Value>`組 （也就是字典） 描述 hello hello 事件詳細資料。 |
| properties.Description | 詳細的描述哪些 hello 自動調整引擎正在進行的工作。 |
| properties.ResourceName | 資源識別碼 hello 影響資源 (hello 的 hello 正在執行調整動作的資源) |
| properties.OldInstancesCount | hello 自動調整規模動作之前的執行個體的 hello 數目所花費的效果。 |
| properties.NewInstancesCount | hello 自動調整規模動作之後的執行個體的 hello 數目所花費的效果。 |
| properties.LastScaleActionTime | hello 的 hello 自動調整規模動作發生時的時間戳記。 |
| status |描述 hello hello 作業狀態的字串。 常見的值包括︰Started、In Progress、Succeeded、Failed、Active、Resolved。 |
| 子狀態 | 針對自動調整通常為 null。 |
| eventTimestamp |Hello Azure 服務處理 hello 產生 hello 事件時的時間戳記要求相對應的 hello 事件。 |
| submissionTimestamp |時間戳記 hello 事件變成可供查詢。 |
| subscriptionId |Azure 訂用帳戶識別碼。 |

## <a name="next-steps"></a>後續步驟
* [深入了解 hello 活動記錄檔 （先前稱為稽核記錄檔）](monitoring-overview-activity-logs.md)
* [資料流 hello Azure 活動記錄檔 tooEvent 集線器](monitoring-stream-activity-logs-event-hubs.md)
