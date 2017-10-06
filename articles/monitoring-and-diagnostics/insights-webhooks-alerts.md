---
title: "在 Azure 度量的警示上 aaaConfigure webhook |Microsoft 文件"
description: "重設 Azure 警示 tooother 非 Azure 系統的路徑。"
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>針對 Azure 度量警示設定 Webhook
Webhook 可讓您 tooroute Azure 警示通知 tooother 系統後置處理或自訂動作。 您可以使用 webhook 警示 tooroute 它 tooservices 傳送 SMS，記錄錯誤、 通知聊天/傳訊服務，透過小組或執行任意數目的其他動作。 本文說明如何 tooset Azure 度量警示和 hello HTTP POST tooa webhook 哪些 hello 內容看起來像 webhook。 如需 hello 安裝程式與 Azure 活動記錄檔警示 （警示的事件） 的結構描述資訊[請改為參閱此頁面](insights-auditlog-to-webhook-email.md)。

Azure 警示 HTTP POST hello 警示內容以 JSON 格式，結構描述定義下面 tooa webhook 建立 hello 警示時，您所提供的 URI。 此 URI 必須是有效的 HTTP 或 HTTPS 端點。 當警示啟動時，Azure 會針對每個要求張貼一個項目。

## <a name="configuring-webhooks-via-hello-portal"></a>設定 webhook 透過 hello 入口網站
您可以新增或更新在 hello hello Create/Update 警示畫面中的 hello webhook URI[入口網站](https://portal.azure.com/)。

![新增警示規則](./media/insights-webhooks-alerts/Alertwebhook.png)

您也可以設定警示 toopost tooa webhook URI 使用 hello [Azure PowerShell Cmdlet](insights-powershell-samples.md#create-metric-alerts)，[跨平台 CLI](insights-cli-samples.md#work-with-alerts)，或[Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)。

## <a name="authenticating-hello-webhook"></a>驗證 hello webhook
hello webhook 可以使用語彙基元為基礎的授權來進行驗證。 hello webhook URI 會儲存權杖的識別碼，例如。 `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>承載結構描述
hello POST 作業包含下列 JSON 裝載和結構描述都以標準為基礎的警示 hello。

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| 欄位 | 強制 | 一組固定值 | 注意事項 |
|:--- |:--- |:--- |:--- |
| status |Y |“Activated”、“Resolved” |Hello 警示 hello 條件根據您設定的狀態。 |
| context |Y | |hello 警示內容。 |
| timestamp |Y | |hello 時間在哪一個 hello 觸發警示。 |
| id |Y | |每個警示規則都有唯一的識別碼。 |
| 名稱 |Y | |hello 警示名稱。 |
| 說明 |Y | |Hello 警示的描述。 |
| conditionType |Y |“Metric”、“Event” |支援兩種類型的警示。 其中一個根據度量的條件和 hello 其他 hello 活動記錄檔中的事件為基礎。 如果 hello 警示根據度量或事件，請使用此值 toocheck。 |
| condition |Y | |hello 特定欄位的 toocheck hello conditionType 為基礎。 |
| metricName |用於計量警示 | |監視 hello hello 度量定義哪些 hello 規則名稱。 |
| metricUnit |用於計量警示 |"Bytes"、"BytesPerSecond"、"Count"、"CountPerSecond"、"Percent"、"Seconds" |hello hello 標準中允許的單位。 [允許的值在此列出](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx)。 |
| metricValue |用於計量警示 | |hello 度量資訊會造成 hello 警示 hello 實際值。 |
| threshold |用於計量警示 | |hello 臨界值在哪一個 hello 啟動警示。 |
| windowSize |用於計量警示 | |hello 期間，使用的 toomonitor hello 臨界值為基礎的警示活動的時間。 必須介於 5 分鐘到 1 天之間。 ISO 8601 持續時間格式。 |
| timeAggregation |用於計量警示 |"Average"、"Last"、"Maximum"、"Minimum"、"None"、"Total" |如何收集 hello 資料應該隨著時間結合。 hello 預設值是 Average。 [允許的值在此列出](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx)。 |
| operator |用於計量警示 | |hello 運算子使用 toocompare hello 目前度量資料 toohello 設定的閾值。 |
| subscriptionId |Y | |Azure 訂用帳戶識別碼。 |
| resourceGroupName |Y | |Hello hello 資源群組名稱會影響資源。 |
| resourceName |Y | |資源名稱的 hello 影響資源。 |
| resourceType |Y | |資源類型的 hello 影響資源。 |
| resourceId |Y | |資源識別碼 hello 影響資源。 |
| resourceRegion |Y | |區域或位置的 hello 影響資源。 |
| portalLink |Y | |直接連結 toohello 入口網站資源摘要 頁面。 |
| 屬性 |N |選用 |一組`<Key, Value>`組 (也就是`Dictionary<String, String>`)，包括有關 hello 事件的詳細資料。 hello 屬性欄位是選擇性的。 自訂 UI 或邏輯為基礎的應用程式的工作流程中，使用者可以輸入可以透過 hello 裝載傳遞的索引鍵/值。 hello 替代方式 toopass 自訂屬性後 toohello webhook 是透過 hello webhook uri 本身 （做為查詢參數） |

> [!NOTE]
> hello 屬性欄位只能設定使用 hello [Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx)。
>
>

## <a name="next-steps"></a>後續步驟
* 深入了解 Azure 警示 」 和 「 hello 視訊中的 webhook[與 PagerDuty 整合 Azure 警示](http://go.microsoft.com/fwlink/?LinkId=627080)
* [對 Azure 警示執行 Azure 自動化指令碼 (Runbook)](http://go.microsoft.com/fwlink/?LinkId=627081)
* [使用邏輯應用程式 toosend Twilio 透過 SMS 從 Azure 警示](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [使用邏輯應用程式 toosend Slack 從 Azure 警示訊息](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [使用邏輯應用程式 toosend 從 Azure 警示訊息 tooan Azure 佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
