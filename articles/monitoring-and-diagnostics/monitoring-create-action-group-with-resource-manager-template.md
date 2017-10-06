---
title: "aaaCreate 動作群組具有資源管理員範本 |Microsoft 文件"
description: "了解如何 toocreate 動作群組使用 Azure Resource Manager 範本。"
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>使用 Resource Manager 範本建立動作群組
本文章將示範如何 toouse [Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)tooconfigure 動作群組。 您可以使用範本自動設定可在特定類型的警示中重複使用的動作群組。 這些動作群組，請確定所有 hello 正確時觸發警示時，會收到通知的合作對象。

hello 基本步驟如下：

1. 建立範本，為描述如何 toocreate hello 動作群組的 JSON 檔案。

2. 使用部署 hello 範本[任何部署方法](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。

首先，我們將描述如何 toocreate Resource Manager 範本使用的動作群組 hello 動作定義是硬式編碼 hello 範本中。 其次，我們將描述如何 toocreate 採用 hello webhook 組態資訊的範本輸入參數部署 hello 範本時。

## <a name="resource-manager-templates-for-an-action-group"></a>動作群組的 Resource Manager 範本

toocreate 動作群組，使用資源管理員範本，建立 hello 類型的資源`Microsoft.Insights/actionGroups`。 然後要填入所有相關的屬性。 以下是兩個建立動作群組的範例範本。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>後續步驟
* 深入了解[動作群組](monitoring-action-groups.md)。
* 深入了解[警示](monitoring-overview-alerts.md)。
* 深入了解如何 tooadd[警示使用資源管理員範本](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。
