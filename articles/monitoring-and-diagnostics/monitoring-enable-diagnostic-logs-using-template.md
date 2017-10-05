---
title: "使用 Resource Manager 範本自動啟用診斷設定 | Microsoft Docs"
description: "了解如何使用 Resource Manager 範本來建立診斷設定，以讓您將診斷記錄檔串流至事件中樞，或將它們儲存在儲存體帳戶中。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="b2d7a-103">使用 Resource Manager 範本在建立資源時自動啟用診斷設定</span><span class="sxs-lookup"><span data-stu-id="b2d7a-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="b2d7a-104">在本文中，我們示範如何在建立資源時使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md) 設定診斷設定。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="b2d7a-105">這可讓您在建立資源時，自動開始將您的診斷記錄檔和度量串流至事件中樞、將它們封存在儲存體帳戶中，或將它們傳送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="b2d7a-106">使用 Resource Manager 範本啟用診斷記錄檔的方法，取決於資源類型。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="b2d7a-107">**非計算** 資源 (例如，網路安全性群組、Logic Apps、自動化) 使用 [這篇文章中所述的診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="b2d7a-108">**計算** 資源 (以 WAD/LAD 為基礎) 使用 [本文中所述的WAD/LAD 組態檔](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="b2d7a-109">在本文中，我們會說明如何使用這兩種方法來設定診斷。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="b2d7a-110">基本步驟如下：</span><span class="sxs-lookup"><span data-stu-id="b2d7a-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="b2d7a-111">建立一個描述如何建立資源的 JSON 檔案做為範本，然後啟用診斷功能。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="b2d7a-112">[使用任何部署方法部署範本](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="b2d7a-113">以下提供產生非計算和計算資源所需的範本 JSON 檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="b2d7a-114">非計算資源範本</span><span class="sxs-lookup"><span data-stu-id="b2d7a-114">Non-Compute resource template</span></span>
<span data-ttu-id="b2d7a-115">如是非計算資源，您需要做兩件事︰</span><span class="sxs-lookup"><span data-stu-id="b2d7a-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="b2d7a-116">將參數加入儲存體帳戶名稱、服務匯流排規則識別碼，和/或 OMS Log Analytics 工作區識別碼的參數 blob (可啟用儲存體帳戶中診斷記錄檔的封存、串流記錄檔至事件中樞，和/或將記錄檔傳送至 Log Analytics)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="b2d7a-117">在您要啟用診斷記錄檔的資源的資源陣列中，加入 `[resource namespace]/providers/diagnosticSettings`類型的資源。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="b2d7a-118">診斷設定的屬性 blob 遵循 [這篇文章中所述的格式](https://msdn.microsoft.com/library/azure/dn931931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="b2d7a-119">新增 `metrics` 屬性可讓您同時傳送資源計量到這些相同的輸出，但前提是[資源支援 Azure 監視器計量](monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="b2d7a-120">以下的完整範例會建立邏輯應用程式，並開啟串流至事件中樞和儲存體帳戶中的儲存體。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="b2d7a-121">計算資源範本</span><span class="sxs-lookup"><span data-stu-id="b2d7a-121">Compute resource template</span></span>
<span data-ttu-id="b2d7a-122">若要啟用計算資源 (例如虛擬機器或 Service Fabric 叢集) 的診斷功能，您需要︰</span><span class="sxs-lookup"><span data-stu-id="b2d7a-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="b2d7a-123">將 Azure 診斷擴充功能加入 VM 資源定義。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="b2d7a-124">指定儲存體帳戶和/或事件中樞做為參數。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="b2d7a-125">將 WADCfg XML 檔案的內容加入 XMLCfg 屬性，適當地逸出所有 XML 字元。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="b2d7a-126">這最後一個步驟要做得正確可能會有點棘手。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="b2d7a-127">[請參閱這篇文章](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) 的範例，將診斷組態結構描述分割成正確逸出和格式正確的變數。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="b2d7a-128">在 [本文件中](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中會說明整個程序，包括範例。</span><span class="sxs-lookup"><span data-stu-id="b2d7a-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2d7a-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2d7a-129">Next Steps</span></span>
* [<span data-ttu-id="b2d7a-130">深入了解 Azure 診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="b2d7a-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="b2d7a-131">將 Azure 診斷記錄檔串流至事件中樞</span><span class="sxs-lookup"><span data-stu-id="b2d7a-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

