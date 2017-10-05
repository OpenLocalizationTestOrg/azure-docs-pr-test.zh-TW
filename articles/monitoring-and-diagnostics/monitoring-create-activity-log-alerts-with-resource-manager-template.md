---
title: "使用 Resource Manager 範本建立活動記錄警示 | Microsoft Docs"
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
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="fc3b7-103">使用 Resource Manager 範本建立活動記錄警示</span><span class="sxs-lookup"><span data-stu-id="fc3b7-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="fc3b7-104">本文章將說明如何使用 [Azure Resource Manager 範本](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates)設定活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="fc3b7-105">您可以使用範本輕鬆地設定許多警示，會以您自動部署程序中特定的活動記錄事件條件作為基礎加以啟動。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="fc3b7-106">基本步驟為：</span><span class="sxs-lookup"><span data-stu-id="fc3b7-106">The basic steps are:</span></span>

1. <span data-ttu-id="fc3b7-107">建立一個以描述如何建立活動記錄警示的 JSON 檔案為形式的範本。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="fc3b7-108">[使用任何部署方法部署範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="fc3b7-109">活動記錄警示的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="fc3b7-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="fc3b7-110">若要使用 Resource Manager 範本建立活動記錄警示，您要建立 `microsoft.insights/activityLogAlerts` 類型的資源。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="fc3b7-111">然後要填入所有相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-111">Then you fill in all related properties.</span></span> <span data-ttu-id="fc3b7-112">以下是建立活動記錄警示的範本。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
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

<span data-ttu-id="fc3b7-113">請瀏覽我們的 [Azure 快速入門資源庫](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights)，取得活動記錄警示範本的一些範例。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc3b7-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc3b7-114">Next steps</span></span>
- <span data-ttu-id="fc3b7-115">深入了解[警示](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="fc3b7-116">了解如何[使用 Resource Manager 範本新增動作群組](monitoring-create-action-group-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="fc3b7-117">了解如何[建立活動記錄警示以監視訂用帳戶的所有自動調整引擎作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="fc3b7-118">了解如何[建立活動記錄警示以監視訂用帳戶中所有失敗的相應縮小/相應放大自動調整作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。</span><span class="sxs-lookup"><span data-stu-id="fc3b7-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
