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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>在 Linux 擴展集範本中使用客體計量自動調整規模

有兩種類型的度量資訊在 Azure 中的 Vm 所傳來蒐集和調整規模設定： 某些伴隨 hello 從裝載 VM 和其他項目來自 hello 客體 VM。 主機計量不需要額外的安裝程式因為它們會收集 hello 主機 VM，而客體度量需要我們 tooinstall hello [Windows Azure 診斷擴充功能](../virtual-machines/windows/extensions-diagnostics-template.md)或 hello [Linux Azure 診斷延伸模組](../virtual-machines/linux/diagnostic-extension.md)hello 在客體 VM。 一個常見原因 toouse 客體度量資訊而不是度量的主機計量是度量的客體度量會提供比主機計量較大選取範圍。 記憶體耗用量計量即為一例，這類計量只能透過客體計量使用。 hello 支援主機度量資訊會列出[這裡](../monitoring-and-diagnostics/monitoring-supported-metrics.md)，並列出常用的客體度量[這裡](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。 本文將說明如何 toomodify hello[可行的最小小數位數設定範本](./virtual-machine-scale-sets-mvss-start.md)toouse 自動調整規模規則根據來賓 Linux 規模集的度量。

## <a name="change-hello-template-definition"></a>變更 hello 樣板定義

可以看到我們可行的最小小數位數的設定範本[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)，而且可以看到我們的範本部署與來賓型自動調整規模設定的 hello Linux 比例[這裡](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json)。 讓我們來檢查此範本 hello 差異比對使用 toocreate (`git diff minimum-viable-scale-set existing-vnet`) 逐一：

首先，我們會加入適用於 `storageAccountName` 和 `storageAccountSasToken` 的參數。 hello 診斷代理程式會儲存在度量資料[資料表](../cosmos-db/table-storage-how-to-use-dotnet.md)此儲存體帳戶中。 為準，hello Linux 診斷代理程式 3.0 版，不再支援使用儲存體存取金鑰。 我們必須使用 [SAS 權杖](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

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

接下來，我們會修改 hello 規模集`extensionProfile`tooinclude hello 診斷延伸模組。 在此組態中，我們指定 hello 資源識別碼 hello 標尺集 toocollect 度量資訊，以及儲存體帳戶和 SAS 權杖 toouse toostore hello 度量 hello。 此外，我們也會指定頻率 hello 度量會彙總 （在此情況下每隔一分鐘） 和 （在此案例的百分比用記憶體） 的度量 tootrack。 如需此設定及已使用記憶體的百分比以外之計量的詳細資訊，請參閱[這份文件](../virtual-machines/linux/diagnostic-extension.md)。

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

最後，我們會加入`autoscaleSettings`資源 tooconfigure 自動調整規模根據這些度量。 這項資源`dependsOn`可參考 hello 小數位數設定 tooensure hello 規模集存在，然後再嘗試 tooautoscale 它。 如果我們選擇不同的度量 tooautoscale 上時，我們會使用 hello`counterSpecifier`從 hello 診斷延伸模組設定為 hello `metricName` hello 自動調整規模設定中。 如需自動調整規模設定的詳細資訊，請參閱 hello[自動調整規模的最佳作法](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md)和 hello [Azure 監視 REST API 參考文件](https://msdn.microsoft.com/library/azure/dn931928.aspx)。

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





## <a name="next-steps"></a>後續步驟

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
