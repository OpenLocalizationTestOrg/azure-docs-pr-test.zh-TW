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
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="f8ff0-103">使用 Resource Manager 範本建立動作群組</span><span class="sxs-lookup"><span data-stu-id="f8ff0-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="f8ff0-104">本文章將示範如何 toouse [Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)tooconfigure 動作群組。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="f8ff0-105">您可以使用範本自動設定可在特定類型的警示中重複使用的動作群組。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="f8ff0-106">這些動作群組，請確定所有 hello 正確時觸發警示時，會收到通知的合作對象。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="f8ff0-107">hello 基本步驟如下：</span><span class="sxs-lookup"><span data-stu-id="f8ff0-107">hello basic steps are:</span></span>

1. <span data-ttu-id="f8ff0-108">建立範本，為描述如何 toocreate hello 動作群組的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="f8ff0-109">使用部署 hello 範本[任何部署方法](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="f8ff0-110">首先，我們將描述如何 toocreate Resource Manager 範本使用的動作群組 hello 動作定義是硬式編碼 hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="f8ff0-111">其次，我們將描述如何 toocreate 採用 hello webhook 組態資訊的範本輸入參數部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="f8ff0-112">動作群組的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="f8ff0-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="f8ff0-113">toocreate 動作群組，使用資源管理員範本，建立 hello 類型的資源`Microsoft.Insights/actionGroups`。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="f8ff0-114">然後要填入所有相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-114">Then you fill in all related properties.</span></span> <span data-ttu-id="f8ff0-115">以下是兩個建立動作群組的範例範本。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-115">Here are two sample templates that create an action group.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f8ff0-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8ff0-116">Next steps</span></span>
* <span data-ttu-id="f8ff0-117">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="f8ff0-118">深入了解[警示](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="f8ff0-119">深入了解如何 tooadd[警示使用資源管理員範本](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="f8ff0-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
