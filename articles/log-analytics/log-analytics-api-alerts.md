---
title: "aaaUsing OMS 記錄分析警示 REST API"
description: "hello 記錄分析警示 REST API 可讓您 toocreate 和管理記錄分析是一部分的 Operations Management Suite (OMS) 中的警示。  本文章提供 hello API 和幾個範例的詳細資料，執行不同的作業。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>使用 REST API 在 Log Analytics 中建立及管理警示規則
hello 記錄分析警示 REST API 可讓您 toocreate 和管理警示在 Operations Management Suite (OMS)。  本文章提供 hello API 和幾個範例的詳細資料，執行不同的作業。

hello 記錄分析搜尋 REST API 是 RESTful，而且可以透過 hello Azure 資源管理員 REST API 存取。 本文件中您會發現範例 hello 應用程式開發介面透過 PowerShell 命令列使用[ARMClient](https://github.com/projectkudu/ARMClient)，簡化叫用的開放原始碼命令列工具 hello Azure 資源管理員 API。 hello 使用 ARMClient 和 PowerShell 是許多選項 tooaccess hello 記錄分析搜尋 API 的其中一個。 這些工具，您可以利用 hello RESTful Azure 資源管理員 API toomake 呼叫 tooOMS 工作區，以及它們在執行搜尋命令。 hello API 會輸出搜尋結果 tooyou JSON 格式，可讓您 toouse hello 搜尋結果中許多不同的方式以程式設計的方式。

## <a name="prerequisites"></a>必要條件
目前，在 Log Analytics 中只能使用已儲存的搜尋來建立警示。  您可以使用參照 toohello[記錄搜尋 REST API](log-analytics-log-search-api.md)如需詳細資訊。

## <a name="schedules"></a>排程
一個已儲存的搜尋可以有一或多個排程。 hello 排程會定義 hello 搜尋執行的頻率，並識別哪一個準則，hello 透過 hello 時間間隔。
排程 hello 下表中都有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 間隔 |Hello 搜尋是的執行頻率。 以分鐘為單位。 |
| QueryTimeSpan |哪些 hello 準則評估 hello 時間間隔。 必須大於等於 tooor 間隔。 以分鐘為單位。 |
| 版本 |hello 所使用的 API 版本。  目前，這應一律設 too1。 |

例如，假設事件查詢的 Interval 是 15 分鐘，而 Timespan 是 30 分鐘。 在此情況下，hello 查詢會執行每隔 15 分鐘，且如果 hello 準則 tooresolve tootrue 透過在 30 分鐘的時間範圍，就會觸發警示。

### <a name="retrieving-schedules"></a>擷取排程
使用 hello 取得方法 tooretrieve 將已儲存搜尋的所有排程。

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

使用 hello 取得排程識別碼 tooretrieve 方法將已儲存搜尋的特定排程。

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

以下是排程的回應範例。

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>建立排程
使用新的排程的排程唯一識別碼 toocreate hello Put 方法。  請注意，兩個排程不能有 hello 相同識別碼即使它們與相關聯不同儲存的搜尋。  當您建立排程在 hello OMS 主控台中時，GUID 被建立 hello 排程識別碼。

> [!NOTE]
> 所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>編輯排程
使用現有的排程識別碼 hello 相同儲存搜尋排程的 toomodify hello Put 方法。  hello hello 要求主體必須包含 hello 排程 hello 的 etag。

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>刪除排程
使用排程的排程識別碼 toodelete hello Delete 方法。

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>動作
一個排程可以有多個動作。 動作可以定義一個或多個處理程序 tooperform，例如傳送郵件，或啟動 runbook，或它可能會定義的臨界值會決定當 hello 搜尋的結果符合某些準則。  使 hello 處理程序將會符合 hello 臨界值時，某些動作會同時定義。

所有動作都有 hello 屬性 hello 下表中。  不同類型的警示有不同的其他屬性，如下所述。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |Hello 動作的類型。  目前 hello 可能的值已設定警示和 Webhook。 |
| 名稱 |Hello 警示的顯示名稱。 |
| 版本 |hello 所使用的 API 版本。  目前，這應一律設 too1。 |

### <a name="retrieving-actions"></a>擷取動作
使用 hello 取得方法 tooretrieve 排程的所有動作。

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

使用 hello 取得 hello 動作識別碼 tooretrieve 方法排程的特定動作。

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>建立或編輯動作
使用唯一 toohello 排程 toocreate 新動作的動作識別碼 hello Put 方法。  當您建立動作 hello OMS 主控台中時，GUID 是 hello 動作識別碼。

> [!NOTE]
> 所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。

使用現有的動作識別碼 hello 相同儲存搜尋排程的 toomodify hello Put 方法。  hello hello 要求主體必須包含 hello 排程 hello 的 etag。

hello 要求格式來建立新的動作會因動作類型，因此 hello 的以下各節會提供這些範例。

### <a name="deleting-actions"></a>刪除動作
使用 hello 動作識別碼 toodelete 動作 hello Delete 方法。

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>警示動作
一個排程應該只有一個警示動作。  警示的動作都有一或多個 hello 下表中的 hello 區段。  以下進一步詳細說明每一個區段。

| 區段 | 說明 |
|:--- |:--- |
| 閾值 |Hello 動作執行時的準則。 |
| EmailNotification |傳送郵件 toomultiple 收件者。 |
| 補救 |在 Azure 自動化 tooattempt toocorrect 識別問題中啟動 runbook。 |

#### <a name="thresholds"></a>臨界值
一個警示動作應該只有一個臨界值。  當儲存搜尋的 hello 結果符合 hello 臨界值中搜尋相關聯的動作時，會執行該動作中的任何其他處理序。  動作也可以只包含臨界值，以便與不包含臨界值的其他類型動作一起搭配使用。

臨界值 hello 下表中都有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 運算子 |Hello 臨界值比較運算子。 <br> gt = 大於 <br> lt = 小於 |
| 值 |Hello 臨界值。 |

例如，假設事件查詢的間隔是 15 分鐘、時間範圍是 30 分鐘，而臨界值大於 10。 在此情況下，hello 執行查詢，會每隔 15 分鐘，並會觸發警示，如果它傳回 10 個透過在 30 分鐘的時間範圍所建立的事件。

以下是一個只包含臨界值的動作的回應範例。  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

使用唯一的動作識別碼 toocreate 新臨界值的動作的 hello Put 方法的排程。  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

使用現有的動作識別碼 toomodify 閾值動作的 hello Put 方法排程。  hello hello 要求主體必須包含 hello etag 的 hello 動作。

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>電子郵件通知
電子郵件通知傳送郵件 tooone 或多個收件者。  其中包含下表中的 hello hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 收件者 |郵件地址清單。 |
| 主旨 |hello hello 郵件主旨。 |
| 附件 |目前不支援附件，這個值永遠為 “None”。 |

以下是一個包含臨界值的電子郵件通知動作的回應範例。  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

使用唯一的動作識別碼 toocreate 新的電子郵件動作的 hello Put 方法的排程。  hello 下列範例會建立電子郵件通知與臨界值讓 hello hello 已儲存的搜尋結果超過 hello 臨界值時，會傳送 hello 郵件。

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

使用現有的動作識別碼 toomodify 電子郵件動作的 hello Put 方法的排程。  hello hello 要求主體必須包含 hello etag 的 hello 動作。

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>補救動作
修復會嘗試識別 hello 警示 toocorrect hello 問題的 Azure 自動化中啟動 runbook。  您必須建立 webhook hello runbook 使用的修復動作，然後 hello URI hello WebhookUri 屬性中。  當您建立使用 hello OMS 主控台，此動作時，hello runbook 自動建立新的 webhook。

補救 hello 下表中包含 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| RunbookName |Hello runbook 名稱。 這必須符合設定 hello OMS 工作區中的自動化方案中的 hello 自動化帳戶中已發佈的 runbook。 |
| WebhookUri |Hello webhook 的 URI。 |
| Expiry |hello 到期日期和時間的 hello webhook。  如果 hello webhook 沒有到期日，這可以是任何有效的未來日期。 |

以下是一個包含臨界值的補救動作的回應範例。

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

使用唯一的動作識別碼 toocreate 新的補救動作的 hello Put 方法的排程。  hello 下列範例會建立修復與臨界值讓 hello runbook 在啟動時的儲存搜尋的 hello hello 結果超過 hello 臨界值。

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

使用現有的動作識別碼 toomodify 的修復動作的 hello Put 方法的排程。  hello hello 要求主體必須包含 hello etag 的 hello 動作。

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>範例
以下是完整的範例 toocreate 新的電子郵件警示。  這會建立新的排程及一個包含臨界值和電子郵件的動作。

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Webhook 動作
Webhook 動作開始的程序呼叫的 URL，同時選擇性提供裝載 toobe 傳送。  它們是類似 tooRemediation 動作，但它們一定會用於可以叫用非 Azure 自動化 runbook 的程序的 webhook。  它們也提供其他選項可 hello 提供裝載 toobe 傳遞 toohello 遠端處理序。

Webhook 動作沒有臨界值，但應該改為加入 tooa 排程，其與臨界值警示動作。  您可以新增將會執行所有符合 hello 臨界值時的多個 Webhook 動作。

Webhook 動作會併入 hello 下表中的 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| WebhookUri |hello hello 郵件主旨。 |
| CustomPayload |自訂承載 toobe 傳送 toohello webhook。  hello 格式將取決於哪些 hello webhook 所預期。 |

以下是 webhook 動作及一個包含臨界值的相關聯警示動作的回應範例。

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>建立或編輯 webhook 動作
使用唯一的動作識別碼 toocreate 新 webhook 動作的 hello Put 方法的排程。  hello 下列範例會建立 Webhook 動作和警示的動作與臨界值，以便 hello hello 已儲存的搜尋結果超過 hello 臨界值時，將會觸發 hello webhook。

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

使用現有的動作識別碼 toomodify webhook 動作的 hello Put 方法的排程。  hello hello 要求主體必須包含 hello etag 的 hello 動作。

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>後續步驟
* 使用 hello [REST API tooperform 記錄搜尋](log-analytics-log-search-api.md)記錄分析中。

