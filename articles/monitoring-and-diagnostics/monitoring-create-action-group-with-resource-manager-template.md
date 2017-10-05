---
title: "使用 Resource Manager 範本建立動作群組 | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 範本建立動作群組。"
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
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="50afc-103">使用 Resource Manager 範本建立動作群組</span><span class="sxs-lookup"><span data-stu-id="50afc-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="50afc-104">本文章將說明如何使用 [Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)設定動作群組。</span><span class="sxs-lookup"><span data-stu-id="50afc-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="50afc-105">您可以使用範本自動設定可在特定類型的警示中重複使用的動作群組。</span><span class="sxs-lookup"><span data-stu-id="50afc-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="50afc-106">這些動作群組能確定觸發警示時，所有正確的對象都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="50afc-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="50afc-107">基本步驟為：</span><span class="sxs-lookup"><span data-stu-id="50afc-107">The basic steps are:</span></span>

1. <span data-ttu-id="50afc-108">建立一個描述如何建立動作群組的範本作為 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="50afc-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="50afc-109">[使用任何部署方法部署範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="50afc-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="50afc-110">首先，我們會說明如何建立動作群組的 Resource Manager 範本，其中的動作定義是在範本中硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="50afc-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="50afc-111">其次，我們會說明如何建立範本部署時，採用 Webhook 組態資訊作為輸入參數的範本。</span><span class="sxs-lookup"><span data-stu-id="50afc-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="50afc-112">動作群組的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="50afc-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="50afc-113">若要使用 Resource Manager 範本建立動作群組，您要建立 `Microsoft.Insights/actionGroups` 類型的資源。</span><span class="sxs-lookup"><span data-stu-id="50afc-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="50afc-114">然後要填入所有相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="50afc-114">Then you fill in all related properties.</span></span> <span data-ttu-id="50afc-115">以下是兩個建立動作群組的範例範本。</span><span class="sxs-lookup"><span data-stu-id="50afc-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
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


## <a name="next-steps"></a><span data-ttu-id="50afc-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50afc-116">Next steps</span></span>
* <span data-ttu-id="50afc-117">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="50afc-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="50afc-118">深入了解[警示](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="50afc-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="50afc-119">了解如何[使用 Resource Manager 範本新增警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="50afc-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
