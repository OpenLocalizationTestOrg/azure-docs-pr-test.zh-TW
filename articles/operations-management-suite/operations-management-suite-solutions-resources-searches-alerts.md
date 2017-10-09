---
title: "aaaSaved 搜尋和 OMS 解決方案中的警示 |Microsoft 文件"
description: "OMS 中的解決方案通常會包含已儲存的搜尋 hello 解決方案所收集的記錄分析 tooanalyze 資料中。  它們可能也定義警示 toonotify hello 使用者或自動採取動作以回應 tooa 嚴重的問題。  本文說明如何 toodefine 記錄分析儲存搜尋和警示在 ARM 範本讓它們可以包含在管理解決方案。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>新增記錄分析儲存的搜尋和警示 tooOMS 管理方案 （預覽）

> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。   


[在 OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會包含[已儲存的搜尋](../log-analytics/log-analytics-log-searches.md)hello 解決方案所收集的記錄分析 tooanalyze 資料中。  它們也必須定義[警示](../log-analytics/log-analytics-alerts.md)toonotify hello 使用者或自動採取動作以回應 tooa 嚴重的問題。  本文說明如何 toodefine 記錄分析儲存搜尋和警示中的[資源管理範本](../resource-manager-template-walkthrough.md)以便包含在[管理解決方案](operations-management-suite-solutions-creating.md)。

> [!NOTE]
> hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>必要條件
本文假設您已經熟悉如何太[建立管理方案](operations-management-suite-solutions-creating.md)和 hello 結構[ARM 範本](../resource-group-authoring-templates.md)和方案檔案。


## <a name="log-analytics-workspace"></a>Log Analytics 工作區
Log Analytics 中的所有資源都包含於[工作區](../log-analytics/log-analytics-manage-access.md)中。  中所述[OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)hello 工作區不包含在 hello 管理解決方案，但必須先安裝 hello 解決方案。  如果它無法使用，hello 方案安裝將會失敗。

hello 工作區的 hello 名稱已在 hello 的每個記錄分析資源的名稱。  這是以 hello hello 方案**工作區**參數如 hello 下列 savedsearch 資源的範例所示。

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>儲存的搜尋
包含[已儲存的搜尋](../log-analytics/log-analytics-log-searches.md)方案 tooallow 使用者 tooquery 資料中收集您的方案。  已儲存搜尋會出現在**我的最愛**hello OMS 入口網站和**已儲存的搜尋**hello Azure 入口網站中。  每個警示也會需要儲存的搜尋。   

[記錄分析儲存搜尋](../log-analytics/log-analytics-log-searches.md)資源有一種`Microsoft.OperationalInsights/workspaces/savedSearches`而且具有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Hello 下表說明每個儲存搜尋的 hello 屬性。 

| 屬性 | 說明 |
|:--- |:--- |
| category | hello hello 已儲存搜尋的分類。  任何已儲存的搜尋 hello 通常也會共用相同的方案中為一個分類，一起群組在 hello 主控台。 |
| displayname | Hello 名稱 toodisplay hello 入口網站中儲存搜尋。 |
| query | 查詢 toorun。 |

> [!NOTE]
> 如果它包含無法解譯為 JSON 的字元，您可能需要在 hello 查詢 toouse 逸出字元。  比方說，如果您的查詢已**類型： AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**，它應該要撰寫 hello 方案檔案儲存為**類型： AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**。

## <a name="alerts"></a>Alerts
[Log Analytics 警示](../log-analytics/log-analytics-alerts.md)是由定期執行儲存之搜尋的警示規則所建立。  如果 hello hello 查詢結果符合指定的準則，就會建立警示的記錄，並執行一或多個動作。  

Hello 下列三個不同的資源是由管理解決方案中的警示規則所組成。

- **儲存的搜尋。**  定義將會執行的 hello 記錄搜尋。  多個警示規則可以共用單一儲存的搜尋。
- **排程。**  定義頻率 hello 記錄搜尋將會執行。  每個警示規則必須且只能有一個排程。
- **警示動作。**  每個警示規則不會有一個動作資源類型為**警示**，定義 hello hello 例如 hello 準則時將會建立警示的記錄，以及 hello 警示的嚴重性的警示詳細資料。  hello 動作資源會選擇性地定義郵件和 runbook 的回應。
- **Webhook 動作 (選擇性)。**  如果 hello 警示規則將會呼叫 webhook，則它需要執行其他動作資源類型為**Webhook**。    

儲存的搜尋資源如上所述。  hello 其他資源如下所述。


### <a name="schedule-resource"></a>排程資源

儲存的搜尋可以有一或多個排程，其中每個排程均代表不同的警示規則。 hello 排程會定義頻率 hello 搜尋執行和 hello 的 hello 透過擷取資料的時間間隔。  排程資源有一種`Microsoft.OperationalInsights/workspaces/savedSearches/schedules/`而且具有下列結構的 hello。 這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



排程資源的 hello 內容詳述於下表中的 hello。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| 已啟用       | 是 | 指定是否要在建立時，啟用 hello 警示。 |
| interval      | 是 | Hello 查詢執行的頻率以分鐘為單位。 |
| queryTimeSpan | 是 | 以分鐘為單位的 tooevaluate 結果上的時間長度。 |

hello 排程資源應該依存於儲存搜尋，以便建立 hello 排程之前的 hello。


### <a name="actions"></a>動作
有兩種類型的 hello 所指定的動作資源**類型**屬性。  排程需要一個**警示**動作，它會定義 hello hello 警示規則，並應採取的動作時建立警示詳細資料。  它也可以包含**Webhook**如果 webhook 應該呼叫 hello 警示中的動作。  

動作資源具有 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions` 類型。  

#### <a name="alert-actions"></a>警示動作

每個排程都會有一個**警示**動作。  這會定義 hello hello 警示及選擇性通知和補救動作的詳細資料。  通知會傳送電子郵件 tooone 或多個位址。  補救啟動的 Azure 自動化 tooattempt tooremediate hello 偵測到問題。

警示的動作有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

hello 下表說明警示動作資源的 hello 內容。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| 類型 | 是 | Hello 動作的類型。  這會是適用於警示動作的 **Alert**。 |
| 名稱 | 是 | Hello 警示的顯示名稱。  這是顯示 hello 警示規則的 hello 主控台中的 hello 名稱。 |
| 說明 | 否 | Hello 警示的選擇性描述。 |
| 嚴重性 | 是 | 嚴重性 hello 警示記錄中的 hello 下列值：<br><br> **Critical**<br>**警告**<br>**Informational** |


##### <a name="threshold"></a>閾值
此為必要區段。  它會定義 hello hello 警示臨界值的屬性。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| 運算子 | 是 | 從下列值的 hello hello 比較運算子：<br><br>**gt = 大於<br>lt = 少於** |
| 值 | 是 | hello 值 toocompare hello 結果。 |


##### <a name="metricstrigger"></a>MetricsTrigger
此為選擇性區段。  加入此區段以供計量計量警示使用。

> [!NOTE]
> 計量測量警示目前是處於公開預覽狀態。 

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| TriggerCondition | 是 | 指定是否 hello 臨界值是針對漏洞或連續的漏洞，從下列值的 hello 總數：<br><br>**Total<br>Consecutive** |
| 運算子 | 是 | 從下列值的 hello hello 比較運算子：<br><br>**gt = 大於<br>lt = 少於** |
| 值 | 是 | Hello hello 準則時間的數目必須符合的 tootrigger hello 警示。 |

##### <a name="throttling"></a>節流
此為選擇性區段。  如果您想 toosuppress 警示 hello 從相同的一段時間後建立警示規則，請包含這一節。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| DurationInMinutes | 如果包含 Throttling 元素，即為 Yes | 分鐘 toosuppress 警示之後從 hello 建立相同的警示規則的數目。 |

##### <a name="emailnotification"></a>EmailNotification
 此區段是選擇性包含它，如果您想 hello 警示 toosend 郵件 tooone 或多個收件者。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| 收件者 | 是 | 以逗號分隔的電子郵件位址清單 toosend 通知警示 hello 下列範例中建立這類時。<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| 主旨 | 是 | Hello 郵件主旨行。 |
| 附件 | 否 | 目前不支援附件。  如果包含此元素，就應該是 **None**。 |


##### <a name="remediation"></a>補救
此區段是選擇性包含它，如果您想要在回應 toohello 警示 runbook toostart。 |

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| RunbookName | 是 | Hello runbook toostart 的名稱。 |
| WebhookUri | 是 | Hello runbook 的 hello webhook 的 Uri。 |
| Expiry | 否 | 到期的日期和時間的 hello 補救。 |

#### <a name="webhook-actions"></a>Webhook 動作

Webhook 動作開始的程序呼叫的 URL，同時選擇性提供裝載 toobe 傳送。 它們是類似 tooRemediation 動作，但它們一定會用於可以叫用非 Azure 自動化 runbook 的程序的 webhook。 它們也提供其他選項可 hello 提供裝載 toobe 傳遞 toohello 遠端處理序。

如果您的警示將會呼叫 webhook，則它需要的動作資源類型為**Webhook**中新增 toohello**警示**動作資源。  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

hello 下表描述 hello Webhook 動作資源的屬性。

| 元素名稱 | 必要 | 說明 |
|:--|:--|:--|
| 類型 | 是 | Hello 動作的類型。  這會是適用於 Webhook 動作的 **Webhook**。 |
| 名稱 | 是 | Hello 動作顯示名稱。  這不會顯示在 hello 主控台。 |
| wehookUri | 是 | Hello webhook 的 Uri。 |
| customPayload | 否 | 自訂承載 toobe 傳送 toohello webhook。 hello 格式將取決於哪些 hello webhook 所預期。 |




## <a name="sample"></a>範例

以下是方案的範例，包括所包含的 hello 下列資源：

- 儲存的搜尋
- 排程
- 警示動作
- Webhook 動作

hello 範例會使用[標準方案參數](operations-management-suite-solutions-solution-file.md#parameters)通常做為方案中使用變數相對於 toohardcoding hello 資源定義中的值。

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


hello 下列參數檔會提供此解決方案的範例值。

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>後續步驟
* [加入檢視](operations-management-suite-solutions-resources-views.md)tooyour 管理解決方案。
* [將自動化 runbook 及其他資源新增](operations-management-suite-solutions-resources-automation.md)tooyour 管理解決方案。

