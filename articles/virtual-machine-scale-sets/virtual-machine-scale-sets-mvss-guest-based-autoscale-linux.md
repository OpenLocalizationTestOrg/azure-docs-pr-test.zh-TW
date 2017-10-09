---
title: "在 Linux 擴展集範本中搭配客體計量使用 Azure 自動調整規模 | Microsoft Docs"
description: "深入了解如何在 Linux 虛擬機器擴展集範本中使用客體度量 tooautoscale"
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
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="e289a-103">在 Linux 擴展集範本中使用客體計量自動調整規模</span><span class="sxs-lookup"><span data-stu-id="e289a-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="e289a-104">有兩種類型的度量資訊在 Azure 中的 Vm 所傳來蒐集和調整規模設定： 某些伴隨 hello 從裝載 VM 和其他項目來自 hello 客體 VM。</span><span class="sxs-lookup"><span data-stu-id="e289a-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="e289a-105">主機計量不需要額外的安裝程式因為它們會收集 hello 主機 VM，而客體度量需要我們 tooinstall hello [Windows Azure 診斷擴充功能](../virtual-machines/windows/extensions-diagnostics-template.md)或 hello [Linux Azure 診斷延伸模組](../virtual-machines/linux/diagnostic-extension.md)hello 在客體 VM。</span><span class="sxs-lookup"><span data-stu-id="e289a-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="e289a-106">一個常見原因 toouse 客體度量資訊而不是度量的主機計量是度量的客體度量會提供比主機計量較大選取範圍。</span><span class="sxs-lookup"><span data-stu-id="e289a-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="e289a-107">記憶體耗用量計量即為一例，這類計量只能透過客體計量使用。</span><span class="sxs-lookup"><span data-stu-id="e289a-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="e289a-108">hello 支援主機度量資訊會列出[這裡](../monitoring-and-diagnostics/monitoring-supported-metrics.md)，並列出常用的客體度量[這裡](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="e289a-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="e289a-109">本文將說明如何 toomodify hello[可行的最小小數位數設定範本](./virtual-machine-scale-sets-mvss-start.md)toouse 自動調整規模規則根據來賓 Linux 規模集的度量。</span><span class="sxs-lookup"><span data-stu-id="e289a-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="e289a-110">變更 hello 樣板定義</span><span class="sxs-lookup"><span data-stu-id="e289a-110">Change hello template definition</span></span>

<span data-ttu-id="e289a-111">可以看到我們可行的最小小數位數的設定範本[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)，而且可以看到我們的範本部署與來賓型自動調整規模設定的 hello Linux 比例[這裡](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="e289a-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="e289a-112">讓我們來檢查此範本 hello 差異比對使用 toocreate (`git diff minimum-viable-scale-set existing-vnet`) 逐一：</span><span class="sxs-lookup"><span data-stu-id="e289a-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="e289a-113">首先，我們會加入適用於 `storageAccountName` 和 `storageAccountSasToken` 的參數。</span><span class="sxs-lookup"><span data-stu-id="e289a-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="e289a-114">hello 診斷代理程式會儲存在度量資料[資料表](../cosmos-db/table-storage-how-to-use-dotnet.md)此儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e289a-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="e289a-115">為準，hello Linux 診斷代理程式 3.0 版，不再支援使用儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e289a-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="e289a-116">我們必須使用 [SAS 權杖](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="e289a-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="e289a-117">接下來，我們會修改 hello 規模集`extensionProfile`tooinclude hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e289a-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="e289a-118">在此組態中，我們指定 hello 資源識別碼 hello 標尺集 toocollect 度量資訊，以及儲存體帳戶和 SAS 權杖 toouse toostore hello 度量 hello。</span><span class="sxs-lookup"><span data-stu-id="e289a-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="e289a-119">此外，我們也會指定頻率 hello 度量會彙總 （在此情況下每隔一分鐘） 和 （在此案例的百分比用記憶體） 的度量 tootrack。</span><span class="sxs-lookup"><span data-stu-id="e289a-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="e289a-120">如需此設定及已使用記憶體的百分比以外之計量的詳細資訊，請參閱[這份文件](../virtual-machines/linux/diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="e289a-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="e289a-121">最後，我們會加入`autoscaleSettings`資源 tooconfigure 自動調整規模根據這些度量。</span><span class="sxs-lookup"><span data-stu-id="e289a-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="e289a-122">這項資源`dependsOn`可參考 hello 小數位數設定 tooensure hello 規模集存在，然後再嘗試 tooautoscale 它。</span><span class="sxs-lookup"><span data-stu-id="e289a-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="e289a-123">如果我們選擇不同的度量 tooautoscale 上時，我們會使用 hello`counterSpecifier`從 hello 診斷延伸模組設定為 hello `metricName` hello 自動調整規模設定中。</span><span class="sxs-lookup"><span data-stu-id="e289a-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="e289a-124">如需自動調整規模設定的詳細資訊，請參閱 hello[自動調整規模的最佳作法](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md)和 hello [Azure 監視 REST API 參考文件](https://msdn.microsoft.com/library/azure/dn931928.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e289a-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="e289a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e289a-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
