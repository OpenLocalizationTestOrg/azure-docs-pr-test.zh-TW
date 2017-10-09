---
title: "Azure 活動記錄檔警示 webhook aaaCall |Microsoft 文件"
description: "路由活動記錄檔事件 tooother 服務的自訂動作。 例如傳送簡訊、記錄 Bug、或透過聊天/傳訊服務來通知團隊。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>針對 Azure 活動記錄警示呼叫 Webhook
Webhook 可讓您 tooroute Azure 警示通知 tooother 系統後置處理或自訂動作。 您可以使用 webhook 警示 tooroute 它 tooservices 傳送 SMS，記錄錯誤、 通知聊天/傳訊服務，透過小組或執行任意數目的其他動作。 本文說明 tooset webhook toobe 呼叫 Azure 活動記錄檔警示引發時的方式。 它也會顯示 hello HTTP POST tooa webhook 看起來像哪些 hello 裝載。 如需有關 hello 安裝程式並在 Azure 度量的警示，結構描述資訊[請改為參閱此頁面](insights-webhooks-alerts.md)。 您也可以設定活動記錄檔警示 toosend 電子郵件時啟動。

> [!NOTE]
> 這項功能目前為預覽狀態，並將在未來的 hello 在某個時間點移除。
>
>

您可以設定活動記錄檔警示使用 hello [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts)，[跨平台 CLI](insights-cli-samples.md#work-with-alerts)，或[Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)。 目前，您無法設定一個使用 hello Azure 入口網站。

## <a name="authenticating-hello-webhook"></a>驗證 hello webhook
hello webhook 可以使用其中一種方法進行驗證：

1. **權杖為基礎的授權**-hello 的 webhook URI 便可以 token 的識別碼，例如，`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **基本授權**-hello 的 webhook URI，例如儲存使用者名稱及密碼，`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>承載結構描述
hello POST 作業包含下列 JSON 裝載和結構描述的所有活動記錄檔為基礎的警示 hello。 此結構描述是類似 toohello 使用其中一種標準為基礎的警示。

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| 元素名稱 | 說明 |
| --- | --- |
| status |用於度量警示。 一定會設定太 「 啟動 」 的活動記錄檔的警示。 |
| context |Hello 事件的內容。 |
| resourceProviderName |hello 資源提供者的 hello 影響資源。 |
| conditionType |一律為「事件」。 |
| 名稱 |Hello 警示規則的名稱。 |
| id |Hello 警示的資源識別碼。 |
| 說明 |Hello 警示建立期間所設定警示描述。 |
| subscriptionId |Azure 訂用帳戶識別碼。 |
| timestamp |Hello 處理 hello 要求的 Azure 服務所產生的 hello 事件的時間。 |
| resourceId |資源識別碼 hello 影響資源。 |
| resourceGroupName |Hello hello 資源群組名稱會影響資源 |
| 屬性 |一組`<Key, Value>`組 (也就是`Dictionary<String, String>`)，包括有關 hello 事件的詳細資料。 |
| 事件 |包含有關 hello 事件的中繼資料元素。 |
| 授權 |hello hello 事件的 RBAC 屬性。 這些通常包括 hello 「 動作 」、 「 角色 」 和 hello 」 範圍中 」。 |
| category |Hello 事件類別目錄。 支援值包括︰管理、警示、安全性、ServiceHealth、建議。 |
| 呼叫者 |執行 hello 作業、 UPN 宣告或 SPN 宣告根據可用性的 hello 使用者的電子郵件地址。 特定系統呼叫可為 Null。 |
| correlationId |通常是字串格式的 GUID。 具有相互關聯識別碼的事件屬於 toohello 相同較大的動作，通常會共用的相互關聯識別碼。 |
| eventDescription |Hello 事件的靜態文字描述。 |
| eventDataId |Hello 事件的唯一識別碼。 |
| eventSource |名稱 hello Azure 服務或基礎結構產生的 hello 事件。 |
| httpRequest |通常包括 hello"clientRequestId"、"clientIpAddress"和"method"(例如 PUT HTTP 方法)。 |
| 層級 |Hello 下列值之一:"Critical"、"Error"、"Warning"、"Informational"和"Verbose"。 |
| operationId |通常是在對應 toosingle 作業 hello 事件之間共用的 GUID。 |
| operationName |Hello 作業的名稱。 |
| 屬性 |Hello 事件的屬性。 |
| status |字串。 Hello 作業的狀態。 常見的值包括︰「已啟動」、「進行中」、「成功」、「失敗」、「使用中」、「已解決」。 |
| 子狀態 |通常包含對應 REST 呼叫 hello hello HTTP 狀態碼。 它也可以包含其他描述子狀態的字串。 常見子狀態的值包括：確定 (HTTP 狀態碼︰200)，已建立 (HTTP 狀態碼︰201)、接受 (HTTP 狀態碼︰202)、沒有內容 (HTTP 狀態碼︰204)、不正確的要求 (HTTP 狀態碼︰400)、找不到 (HTTP 狀態碼︰404)，衝突 (HTTP 狀態碼︰409)、內部伺服器錯誤 (HTTP 狀態碼︰500)、服務無法使用 (HTTP 狀態碼︰503)、閘道逾時 (HTTP 狀態碼︰504) |

## <a name="next-steps"></a>後續步驟
* [深入了解 hello 活動記錄檔](monitoring-overview-activity-logs.md)
* [對 Azure 警示執行 Azure 自動化指令碼 (Runbook)](http://go.microsoft.com/fwlink/?LinkId=627081)
* [使用邏輯應用程式在從 Azure 警示 toosend Twilio 透過 SMS](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)。 這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。
* [使用邏輯應用程式 toosend Slack 訊息從 Azure 警示](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)。 這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。
* [使用邏輯應用程式 toosend 從 Azure 警示訊息 tooan Azure 佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)。 這個範例適用於度量的警示，但可能已修改的 toowork 活動記錄警示。
