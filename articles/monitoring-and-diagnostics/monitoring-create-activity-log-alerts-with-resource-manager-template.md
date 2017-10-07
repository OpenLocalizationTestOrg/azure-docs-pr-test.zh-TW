---
title: "aaaCreate Resource Manager 範本之活動記錄檔警示 |Microsoft 文件"
description: "在 Azure 資源建立時取得通知。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>使用 Resource Manager 範本建立活動記錄警示
本文章將示範如何 toouse [Azure Resource Manager 範本](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates)tooconfigure 活動記錄檔的警示。 您可以使用範本輕鬆地設定許多警示，會以您自動部署程序中特定的活動記錄事件條件作為基礎加以啟動。

hello 基本步驟如下：

1. 建立範本，為描述如何 toocreate hello 活動記錄警示的 JSON 檔案。

2. 使用部署 hello 範本[任何部署方法](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。

## <a name="resource-manager-template-for-an-activity-log-alert"></a>活動記錄警示的 Resource Manager 範本
toocreate 活動記錄檔警示使用資源管理員範本，建立 hello 類型的資源`microsoft.insights/activityLogAlerts`。 然後要填入所有相關的屬性。 以下是建立活動記錄警示的範本。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

請瀏覽我們的 [Azure 快速入門資源庫](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights)，取得活動記錄警示範本的一些範例。

## <a name="next-steps"></a>後續步驟
- 深入了解[警示](monitoring-overview-alerts.md)。
- 深入了解如何 tooadd[動作群組，使用資源管理員範本](monitoring-create-action-group-with-resource-manager-template.md)。
- 了解如何太[訂用帳戶上的所有自動調整引擎作業建立活動記錄檔警示 toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)。
- 了解如何太[訂用帳戶上的所有失敗的自動調整規模輸入/向外作業建立活動記錄檔警示 toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。
