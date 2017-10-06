---
title: "aaaUse Azure Resource Manager 範本 tooCreate 及設定記錄分析工作區 |Microsoft 文件"
description: "您可以使用 Azure Resource Manager 範本 toocreate，並設定記錄分析工作區。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: c8f413e982f5eeed73f463524ff6f239f26c9127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="849a1-103">使用 Azure Resource Manager 範本管理 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="849a1-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="849a1-104">您可以使用[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toocreate 及設定記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="849a1-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toocreate and configure Log Analytics workspaces.</span></span> <span data-ttu-id="849a1-105">您可以使用範本執行的 hello 工作的範例包括：</span><span class="sxs-lookup"><span data-stu-id="849a1-105">Examples of hello tasks you can perform with templates include:</span></span>

* <span data-ttu-id="849a1-106">建立工作區</span><span class="sxs-lookup"><span data-stu-id="849a1-106">Create a workspace</span></span>
* <span data-ttu-id="849a1-107">新增解決方案</span><span class="sxs-lookup"><span data-stu-id="849a1-107">Add a solution</span></span>
* <span data-ttu-id="849a1-108">建立已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="849a1-108">Create saved searches</span></span>
* <span data-ttu-id="849a1-109">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="849a1-109">Create a computer group</span></span>
* <span data-ttu-id="849a1-110">啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="849a1-110">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="849a1-111">從 Linux 和 Windows 電腦收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="849a1-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="849a1-112">在 Linux 電腦上收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="849a1-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="849a1-113">從 Windows 事件記錄檔收集事件</span><span class="sxs-lookup"><span data-stu-id="849a1-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="849a1-114">收集自訂事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="849a1-114">Collect custom event logs</span></span>
* <span data-ttu-id="849a1-115">新增 hello 記錄分析代理程式 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="849a1-115">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="849a1-116">設定使用 Azure 診斷收集記錄檔分析 tooindex 資料</span><span class="sxs-lookup"><span data-stu-id="849a1-116">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="849a1-117">本文章提供範本的範例將示範一些您可以從範本執行的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="849a1-117">This article provides a template samples that illustrate some of hello configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="849a1-118">建立及設定 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="849a1-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="849a1-119">hello 下列範本 」 範例將說明如何：</span><span class="sxs-lookup"><span data-stu-id="849a1-119">hello following template sample illustrates how to:</span></span>

1. <span data-ttu-id="849a1-120">建立工作區，包括設定資料保留</span><span class="sxs-lookup"><span data-stu-id="849a1-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="849a1-121">新增解決方案 toohello 工作區</span><span class="sxs-lookup"><span data-stu-id="849a1-121">Add solutions toohello workspace</span></span>
3. <span data-ttu-id="849a1-122">建立已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="849a1-122">Create saved searches</span></span>
4. <span data-ttu-id="849a1-123">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="849a1-123">Create a computer group</span></span>
5. <span data-ttu-id="849a1-124">啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="849a1-124">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
6. <span data-ttu-id="849a1-125">從 Linux 電腦收集邏輯磁碟效能計數器 (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="849a1-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="849a1-126">從 Linux 電腦收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="849a1-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="849a1-127">從 Windows 電腦的 hello 應用程式事件記錄檔收集錯誤和警告事件</span><span class="sxs-lookup"><span data-stu-id="849a1-127">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="849a1-128">從 Windows 電腦收集記憶體可用 Mb 效能計數器</span><span class="sxs-lookup"><span data-stu-id="849a1-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="849a1-129">收集自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="849a1-129">Collect a custom log</span></span> 
11. <span data-ttu-id="849a1-130">收集 IIS 記錄檔和 Azure 診斷 tooa 儲存體帳戶所撰寫的 Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="849a1-130">Collect IIS logs and Windows Event logs written by Azure diagnostics tooa storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of hello storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "hello resource group name containing hello storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-hello-sample-template"></a><span data-ttu-id="849a1-131">部署的 hello 範例範本</span><span class="sxs-lookup"><span data-stu-id="849a1-131">Deploying hello sample template</span></span>
<span data-ttu-id="849a1-132">toodeploy hello 範例範本：</span><span class="sxs-lookup"><span data-stu-id="849a1-132">toodeploy hello sample template:</span></span>

1. <span data-ttu-id="849a1-133">將 hello 附加的範例儲存在檔案中例如`azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="849a1-133">Save hello attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="849a1-134">編輯您想要的 hello 範本 toohave hello 組態</span><span class="sxs-lookup"><span data-stu-id="849a1-134">Edit hello template toohave hello configuration you want</span></span>
3. <span data-ttu-id="849a1-135">使用 PowerShell 或 hello 命令列 toodeploy hello 範本</span><span class="sxs-lookup"><span data-stu-id="849a1-135">Use PowerShell or hello command line toodeploy hello template</span></span>

#### <a name="powershell"></a><span data-ttu-id="849a1-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="849a1-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="849a1-137">命令列</span><span class="sxs-lookup"><span data-stu-id="849a1-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="849a1-138">範例 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="849a1-138">Example Resource Manager templates</span></span>
<span data-ttu-id="849a1-139">hello Azure 快速入門範本組件庫包含數個範本，供記錄分析，包括：</span><span class="sxs-lookup"><span data-stu-id="849a1-139">hello Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="849a1-140">部署虛擬機器執行 Windows 的 hello 記錄分析 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="849a1-140">Deploy a virtual machine running Windows with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="849a1-141">部署虛擬機器執行 Linux 與 hello 記錄分析 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="849a1-141">Deploy a virtual machine running Linux with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="849a1-142">使用現有 Log Analytics 工作區監視 Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="849a1-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="849a1-143">使用現有 Log Analytics 工作區監視 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="849a1-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="849a1-144">使用現有 Log Analytics 工作區監視 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="849a1-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="849a1-145">部署 Service Fabric 叢集，並以現有 Log Analytics 工作區監視它</span><span class="sxs-lookup"><span data-stu-id="849a1-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="849a1-146">部署 Service Fabric 叢集，並建立記錄分析工作區 toomonitor 它</span><span class="sxs-lookup"><span data-stu-id="849a1-146">Deploy a Service Fabric cluster and create a Log Analytics workspace toomonitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="849a1-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="849a1-147">Next steps</span></span>
* [<span data-ttu-id="849a1-148">使用 Resource Manager 範本將代理程式部署到 Azure VM</span><span class="sxs-lookup"><span data-stu-id="849a1-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

