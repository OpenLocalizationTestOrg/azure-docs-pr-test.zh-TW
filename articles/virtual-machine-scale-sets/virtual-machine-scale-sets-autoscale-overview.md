---
title: "aaaAutomatic 縮放比例和虛擬機器擴充集 |Microsoft 文件"
description: "了解如何使用診斷和自動調整資源 tooautomatically 標尺虛擬機器規模集中的。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>如何 toouse 自動縮放比例和虛擬機器規模集
自動調整的虛擬機器規模集中的 hello 建立或刪除中設定為 hello 的機器所需 toomatch 效能需求。 當工作的 hello 數量增加時，應用程式可能需要額外的資源 tooenable 它 tooeffectively 執行工作。

自動調整是自動化程序，可協助減輕管理額外負荷。 透過減少額外負荷，您不需要 toocontinually 監視系統效能，或決定如何 toomanage 資源。 調整是一項彈性的程序。 Hello 負載增加時，可以加入更多資源。 還為視需要降低資源可以移除的 toominimize 成本和維護效能層級。

設定使用 Azure Resource Manager 範本、 Azure PowerShell、 Azure CLI 或 hello Azure 入口網站來設定標尺上的自動調整。

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>使用 Resource Manager 範本，設定調整
您不是分開部署與管理應用程式的每個資源，而是使用範本，藉此經由協調的單一作業來部署所有資源。 在 hello 範本中，應用程式的資源定義時，部署參數指定不同的環境。 hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。 toolearn 詳細資訊，看看[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。

在 hello 範本中，您可以指定 hello 容量項目：

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

容量識別 hello hello 集合中的虛擬機器數目。 您可以藉由部署具有不同值的範本手動變更 hello 容量。 如果您要部署範本 tooonly 變更 hello 容量，您可以包含 hello SKU 元素與 hello 更新容量。

hello 規模集的容量可以自動調整使用的 hello 組合**autoscaleSettings**資源和 hello 診斷延伸模組。

### <a name="configure-hello-azure-diagnostics-extension"></a>設定 hello Azure 診斷擴充功能
自動縮放只能夠如果度量收集是成功 hello 規模集中的每部虛擬機器上。 hello Azure 診斷擴充功能提供符合 hello 自動調整資源 hello 度量集合需求的 hello 監視和診斷功能。 您可以安裝 hello 延伸 hello Resource Manager 範本的一部分。

此範例會顯示 hello 範本 tooconfigure hello 診斷延伸模組中使用的 hello 變數：

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

部署 hello 範本時，會提供參數。 在此範例中，hello （儲存資料） 的 hello 儲存體帳戶名稱和 hello 提供 hello 規模集 （其中收集資料） 的名稱。 也在 Windows Server 本例中，會收集僅 hello 執行緒計數 」 效能計數器。 所有 hello 可用的效能計數器，在 Windows 或 Linux 可以是使用的 toocollect 診斷資訊，而且可以包含在 hello 延伸模組組態。

此範例會顯示 hello 範本中的 hello 延伸模組的 hello 定義：

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Hello 診斷延伸模組在執行時，要 hello 資料儲存及收集在資料表中，您指定的 hello 儲存體帳戶中。 在 hello **WADPerformanceCounters**資料表中，您可以找到 hello 收集資料：

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>設定 hello autoScaleSettings 資源
hello autoscaleSettings 資源使用 hello 診斷延伸模組 toodecide hello 資訊是否 tooincrease 或減少 hello 虛擬機器數目 hello 規模設定。

此範例顯示 hello 範本中的 hello 資源的 hello 設定：

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

在 hello 上述範例中，兩個規則會建立定義 hello 自動調整規模動作。 hello 第一項規則會定義 hello 向外延展動作和 hello 第二個規則定義 hello 標尺的動作。 Hello 規則提供這些值：

| 規則 | 說明 |
| ---- | ----------- |
| metricName        | 此值為 hello 與 hello 效能計數器，您在 hello 診斷延伸模組的 hello wadperfcounter 變數中定義相同的。 在 hello 上述範例中，會使用 hello 執行緒計數計數器。    |
| metricResourceUri | 此值為 hello 虛擬機器規模集的 hello 資源識別項。 此識別碼包含 hello hello 資源群組名稱、 hello hello 資源提供者名稱和 hello 小數位數組 tooscale hello 名稱。 |
| timeGrain         | 此值為 hello 的 hello 計量所收集的資料粒度。 在上述範例中的 hello，一分鐘的間隔收集資料。 此值是搭配 timeWindow 使用。 |
| statistic         | 這個值會決定如何 hello 度量資訊會結合的 tooaccommodate hello 自動調整規模動作。 hello 可能的值為： 平均值、 最小值、 最大值。 |
| timeWindow        | 此值為 hello 收集執行個體資料的時間範圍。 其值必須介於 5 分鐘到 12 小時之間。 |
| timeAggregation   | 這個值會決定如何隨著時間結合收集的 hello 資料。 hello 預設值是 Average。 hello 可能的值為： 平均、 最小值、 最大值、 最後一個、 總和、 計數。 |
| operator          | 這個值是使用的 toocompare hello 度量資料與 hello 臨界值的 hello 運算子。 hello 可能的值為： NotEquals、 GreaterThan、 GreaterThanOrEqual、 LessThan、 LessThanOrEqual 等於。 |
| threshold         | 此值為 hello 觸發 hello 調整規模動作。 會確定 tooprovide hello hello 臨界值之間有足夠的差異**向外延展**和**標尺中**動作。 如果這兩個動作的相同值，設定 hello，hello 系統將不常變更，而使它無法執行調整動作。 例如，在上述範例中的 hello 中設定兩個 too600 執行緒無法運作。 |
| direction         | 這個值會決定 hello 為止 hello 臨界值時所執行的動作。 hello 可能的值為增加或減少。 |
| 類型              | 此值為 hello 應該會發生，且必須設定 tooChangeCount 的動作類型。 |
| value             | 此值為 hello 加入 tooor 從 hello 規模調整集合中移除的虛擬機器數目。 此值必須是 1 或更大。 |
| cooldown          | Hello 下一個動作發生之前，這個值會是 hello 數量時間 toowait 自 hello 的最後一個調整動作。 此值必須介於一分鐘到一週之間。 |

Hello 效能計數器，根據使用的，某些 hello hello 範本組態中的項目會以不同的方式使用。 在上述範例中的 hello，hello 效能計數器是執行緒計數、 hello 臨界值會是向外延展動作，650 和 hello 臨界值是 550 hello 標尺的動作。 如果您使用如 %Processor Time 計數器，hello 臨界值會設定 toohello 判斷調整動作的 CPU 使用量百分比。

當觸發調整動作時，高負載，例如 hello 集合的 hello 容量會增加根據 hello hello 範本中的值。 比方說，在小數位數設定的 hello 容量設定 too3 而設定 too1 hello 的調整動作值：

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

當 hello 目前負載原因 hello 平均執行緒計數 toogo 超過 650 hello 閾值：

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A**向外延展**原因 hello hello 組 toobe 以一遞增的容量來觸發動作：

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

hello 結果會是虛擬機器加入 toohello 規模集：

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Cooldown 段五分鐘，如果 hello 平均數目的執行緒在 hello 機器上停留超過 600，另一部電腦新增後 toohello 組。 如果 hello 平均執行緒計數停留下方 550，hello 規模集的 hello 容量會減 1，並從 hello 集就會移除機器。

## <a name="set-up-scaling-using-azure-powershell"></a>使用 Azure PowerShell 設定調整

使用 PowerShell tooset 自動調整，向上的 toosee 範例查看[監視 Azure PowerShell，快速啟動範例](../monitoring-and-diagnostics/insights-powershell-samples.md)。

## <a name="set-up-scaling-using-azure-cli"></a>使用 Azure CLI 設定調整

使用 Azure CLI tooset 自動調整，向上的 toosee 範例查看[Azure 監視跨平台 CLI 快速啟動範例](../monitoring-and-diagnostics/insights-cli-samples.md)。

## <a name="set-up-scaling-using-hello-azure-portal"></a>設定調整使用 hello Azure 入口網站

toosee 的使用範例 hello Azure 入口網站的 tooset 設定自動調整，查看在[建立虛擬機器擴展集使用 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。

## <a name="investigate-scaling-actions"></a>調查調整動作

* **Azure 入口網站**  
目前，您可以取得使用 hello 入口網站的資訊數量有限。

* **Azure 資源總管**  
此工具為 hello 最適合瀏覽 hello 擴展集的目前狀態。 按照此路徑，您應該會看到您建立 hello hello 標尺的執行個體檢視集：  
**訂用帳戶 > {您的訂用帳戶} > resourceGroups > {您的資源群組} > 提供者 > Microsoft.Compute > virtualMachineScaleSets > {您的擴展集} > virtualMachines**

* **Azure PowerShell**  
使用此命令 tooget 一些資訊：

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Toohello jumpbox 虛擬機器連線，就像任何其他電腦，然後您可以從遠端存取 hello hello 小數位數組 toomonitor 個別處理程序中的虛擬機器時，一樣。

## <a name="next-steps"></a>後續步驟
* 查看[自動調整虛擬機器規模集中的機器](virtual-machine-scale-sets-windows-autoscale.md)toosee 如何 toocreate 小數位數設定自動調整設定的範例。

* 在 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)中找到 Azure 監視器監視功能的範例

* 了解通知功能[用於 Azure 監視的自動調整規模動作 toosend 電子郵件和 webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)。

* 深入了解如何太[使用稽核記錄 toosend 電子郵件和 webhook 警示通知，在 Azure 監視器](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* 深入了解 [進階自動調整案例](virtual-machine-scale-sets-advanced-autoscale.md)。
