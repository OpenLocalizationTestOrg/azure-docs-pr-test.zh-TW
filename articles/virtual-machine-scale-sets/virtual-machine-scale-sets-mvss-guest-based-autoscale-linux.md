---
title: "在 Linux 擴展集範本中搭配客體計量使用 Azure 自動調整規模 | Microsoft Docs"
description: "了解如何在 Linux 虛擬機器擴展集範本中使用客體計量自動調整規模"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="8a45c-103">在 Linux 擴展集範本中使用客體計量自動調整規模</span><span class="sxs-lookup"><span data-stu-id="8a45c-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="8a45c-104">在 Azure 中蒐集自 VM 和擴展集的計量有兩種類型：部分來自主機 VM，其他則來自客體 VM。</span><span class="sxs-lookup"><span data-stu-id="8a45c-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="8a45c-105">主機計量不需要額外的安裝，因為它們會由主機 VM 所收集，而客體計量需要我們在客體 VM 中安裝 [Windows Azure 診斷擴充功能](../virtual-machines/windows/extensions-diagnostics-template.md)或 [Linux Azure 診斷擴充功能](../virtual-machines/linux/diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="8a45c-106">使用客體計量而非主機計量的一個常見原因是，客體計量會提供比主機計量更大的計量選取範圍。</span><span class="sxs-lookup"><span data-stu-id="8a45c-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="8a45c-107">記憶體耗用量計量即為一例，這類計量只能透過客體計量使用。</span><span class="sxs-lookup"><span data-stu-id="8a45c-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="8a45c-108">[這裡](../monitoring-and-diagnostics/monitoring-supported-metrics.md)會列出支援的主機度量，而常用的客體計量則列於[這裡](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="8a45c-109">本文將說明如何根據適用於 Linux 擴展集的客體計量來修改[最基本可行的擴展集範本](./virtual-machine-scale-sets-mvss-start.md)，以使用自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="8a45c-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="8a45c-110">變更範本定義</span><span class="sxs-lookup"><span data-stu-id="8a45c-110">Change the template definition</span></span>

<span data-ttu-id="8a45c-111">您可以在[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)看到最基本可行的擴展集範本，並在[這裡](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json)看到使用以客體為基礎之自動調整規模部署 Linux 擴展集的範本。</span><span class="sxs-lookup"><span data-stu-id="8a45c-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="8a45c-112">讓我們逐步檢查用來建立此範本 (`git diff minimum-viable-scale-set existing-vnet`) 的差異：</span><span class="sxs-lookup"><span data-stu-id="8a45c-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="8a45c-113">首先，我們會加入適用於 `storageAccountName` 和 `storageAccountSasToken` 的參數。</span><span class="sxs-lookup"><span data-stu-id="8a45c-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="8a45c-114">診斷代理程式會將計量資料儲存於此儲存體帳戶的[表格](../cosmos-db/table-storage-how-to-use-dotnet.md)中。</span><span class="sxs-lookup"><span data-stu-id="8a45c-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="8a45c-115">從 Linux 診斷代理程式 3.0 版開始，不再支援使用儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8a45c-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="8a45c-116">我們必須使用 [SAS 權杖](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

<span data-ttu-id="8a45c-117">接下來，我們會修改擴展集 `extensionProfile` 以包含診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8a45c-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="8a45c-118">在此設定中，我們會指定要從中收集計量之擴展集的資源識別碼，以及要用來儲存計量的儲存體帳戶和 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="8a45c-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="8a45c-119">此外，也會指定彙總計量資訊的頻率 (在此案例中為每隔一分鐘)，以及要追蹤的計量 (在此案例中為已使用記憶體的百分比)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="8a45c-120">如需此設定及已使用記憶體的百分比以外之計量的詳細資訊，請參閱[這份文件](../virtual-machines/linux/diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

<span data-ttu-id="8a45c-121">最後，會加入 `autoscaleSettings` 資源，以根據這些計量來設定自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="8a45c-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="8a45c-122">此資源含有 `dependsOn` 子句，其會參考擴展集以確定擴展集存在，然後再嘗試自動調整其規模。</span><span class="sxs-lookup"><span data-stu-id="8a45c-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="8a45c-123">如果我們選擇不同的計量來自動調整規模，可以使用來自診斷擴充功能設定的 `counterSpecifier`，作為自動調整規模設定中的 `metricName`。</span><span class="sxs-lookup"><span data-stu-id="8a45c-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="8a45c-124">如需自動調整規模設定的詳細資訊，請參閱[自動調整規模的最佳做法](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md)和 [Azure 監視器 REST API 參考文件](https://msdn.microsoft.com/library/azure/dn931928.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="8a45c-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a><span data-ttu-id="8a45c-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a45c-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
