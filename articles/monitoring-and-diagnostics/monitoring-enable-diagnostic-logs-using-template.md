---
title: "aaaAutomatically 啟用診斷設定使用資源管理員範本 |Microsoft 文件"
description: "深入了解如何 toouse 資源管理員範本 toocreate 診斷設定，可讓您 toostream 您診斷記錄 tooEvent 中樞，或將它們儲存在儲存體帳戶。"
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
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="ba0ea-103">使用 Resource Manager 範本在建立資源時自動啟用診斷設定</span><span class="sxs-lookup"><span data-stu-id="ba0ea-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="ba0ea-104">本文章中我們示範如何使用[Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)tooconfigure 診斷設定時就會建立在資源上的。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="ba0ea-105">這可讓您 tooautomatically 開始串流處理您診斷記錄檔和度量的 tooEvent 集線器，將其封存儲存體帳戶，或將它們傳送 tooLog 分析，在建立資源。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="ba0ea-106">啟用診斷記錄檔使用資源管理員範本的 hello 方法取決於 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="ba0ea-107">**非計算** 資源 (例如，網路安全性群組、Logic Apps、自動化) 使用 [這篇文章中所述的診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="ba0ea-108">**計算**（WAD/年輕人為基礎） 的資源，請使用 hello [WAD/年輕人本文中所述的組態檔](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="ba0ea-109">這篇文章描述如何使用哪一種方法的 tooconfigure 診斷。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="ba0ea-110">hello 基本步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba0ea-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="ba0ea-111">為說明如何 toocreate hello 資源，並啟用診斷功能的 JSON 檔案建立範本。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="ba0ea-112">[部署使用的任何部署方法的 hello 範本](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="ba0ea-113">下面我們提供 hello 範本所需 toogenerate 非計算及運算資源的 JSON 檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="ba0ea-114">非計算資源範本</span><span class="sxs-lookup"><span data-stu-id="ba0ea-114">Non-Compute resource template</span></span>
<span data-ttu-id="ba0ea-115">如需非計算資源，您將需要 toodo 兩件事：</span><span class="sxs-lookup"><span data-stu-id="ba0ea-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="ba0ea-116">加入參數 toohello 參數 blob hello 儲存體帳戶名稱、 服務匯流排規則識別碼，及/或 OMS 記錄分析工作區識別碼 （啟用診斷記錄檔的封存資料流處理的記錄檔 tooEvent 集線器，及/或傳送記錄檔 tooLog 分析儲存體帳戶中）。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="ba0ea-117">Hello 資源陣列中的 hello 想 tooenable 診斷記錄檔的資源，新增類型的資源`[resource namespace]/providers/diagnosticSettings`。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="ba0ea-118">hello hello 診斷設定的內容 blob 遵循[本文中所述的 hello 格式](https://msdn.microsoft.com/library/azure/dn931931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="ba0ea-119">新增 hello`metrics`屬性可讓您 tooalso 傳送資源度量 toothese 相同會輸出，但前提是[hello 資源支援的 Azure 監視度量](monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="ba0ea-120">以下是完整的範例會建立邏輯應用程式，並開啟資料流 tooEvent 集線器和儲存體帳戶中的儲存體。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="ba0ea-121">計算資源範本</span><span class="sxs-lookup"><span data-stu-id="ba0ea-121">Compute resource template</span></span>
<span data-ttu-id="ba0ea-122">您需要計算資源，例如虛擬機器或 Service Fabric 叢集上的 tooenable 診斷：</span><span class="sxs-lookup"><span data-stu-id="ba0ea-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="ba0ea-123">新增 hello Azure 診斷擴充功能 toohello VM 資源定義。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="ba0ea-124">指定儲存體帳戶和/或事件中樞做為參數。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="ba0ea-125">將 hello 您 WADCfg XML 檔案的內容加入至 hello XMLCfg 屬性，正確逸出所有的 XML 字元。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="ba0ea-126">這最後一個步驟可以很難解釋 tooget 權限。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="ba0ea-127">[請參閱本文章](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables)分割 hello 診斷組態結構描述，到逸出，且格式正確的變數範例。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="ba0ea-128">hello 整個程序，包括範例，說明[本文](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ba0ea-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba0ea-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba0ea-129">Next Steps</span></span>
* [<span data-ttu-id="ba0ea-130">深入了解 Azure 診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="ba0ea-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="ba0ea-131">資料流 Azure 診斷記錄檔 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="ba0ea-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

