---
title: "aaaCollect Azure 記錄分析服務記錄檔和度量 |Microsoft 文件"
description: "在 Azure 資源 toowrite 記錄檔和度量 tooLog 分析設定診斷功能。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>收集 Azure 服務的記錄和計量以便使用於 Log Analytics

有四種不同的方式可收集 Azure 服務的記錄和度量︰

1. Azure 診斷直接 tooLog 分析 (*診斷*hello 下表中)
2. Azure 診斷 tooAzure 儲存體 tooLog 分析 (*儲存體*hello 下表中)
3. Azure 服務的連接器 (*連接器*hello 下表中)
4. 和編寫指令碼 toocollect 然後張貼資料到記錄分析 （空白下表中的 hello 和未列出的服務）


| 服務                 | 資源類型                           | 記錄檔        | 度量     | 方案 |
| --- | --- | --- | --- | --- |
| 應用程式閘道    | Microsoft.Network/applicationGateways   | 診斷 | 診斷 | [Azure 應用程式閘道分析](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application insights    |                                         | 連接器   | 連接器   | [Application Insights Connector (Application Insights 連接器)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (預覽) |
| 自動化帳戶     | Microsoft.Automation/AutomationAccounts | 診斷 |             | [詳細資訊](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Batch 帳戶          | Microsoft.Batch/batchAccounts           | 診斷 | 診斷 | |
| 傳統雲端服務  |                                         | 儲存體     |             | [詳細資訊](log-analytics-azure-storage-iis-table.md) |
| 辨識服務      | Microsoft.CognitiveServices/accounts    |             | 診斷 | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | 診斷 |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | 診斷 |             | |
| 事件中樞命名空間     | Microsoft.EventHub/namespaces           | 診斷 | 診斷 | |
| IoT 中樞                | Microsoft.Devices/IotHubs               |             | 診斷 | |
| 金鑰保存庫               | Microsoft.KeyVault/vaults               | 診斷 |             | [金鑰保存庫分析](log-analytics-azure-key-vault.md) |
| 負載平衡器          | Microsoft.Network/loadBalancers         | 診斷 |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | 診斷 | 診斷 | |
| 網路安全性群組 | Microsoft.Network/networksecuritygroups | 診斷 |             | [Azure 網路安全性群組分析](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| 復原保存庫         | Microsoft.RecoveryServices/vaults       |             |             | [Azure 復原服務分析 (預覽)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| 搜尋服務         | Microsoft.Search/searchServices         | 診斷 | 診斷 | |
| 服務匯流排命名空間   | Microsoft.ServiceBus/namespaces         | 診斷 | 診斷 | [服務匯流排分析 (預覽)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | 儲存體     |             | [Service Fabric Analytics (Service Fabric 分析) (預覽)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | 診斷 | [Azure SQL Analytics (預覽)](log-analytics-azure-sql.md) |
| 儲存體                 |                                         |             | 指令碼      | [Azure 儲存體分析 (預覽)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| 虛擬機器        | Microsoft.Compute/virtualMachines       | 分機   | 分機 <br> 診斷  | |
| 虛擬機器擴展集 | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | 診斷 | |
| Web 伺服器陣列        | Microsoft.Web/serverfarms               |             | 診斷 | |
| 網站               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | 診斷 | [Azure Web Apps 分析 (預覽)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> 我們建議您監視 Azure 虛擬機器 （Linux 和 Windows），安裝 hello[記錄分析 VM 延伸模組](log-analytics-azure-vm-extension.md)。 hello 代理程式為您提供從收集您的虛擬機器內的深入資訊。 您也可以使用 hello 擴充功能的虛擬機器規模集。
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>直接 tooLog 分析 azure 診斷
許多 Azure 資源都可以 toowrite 診斷記錄檔和度量直接 tooLog 分析，而這是慣用的 hello 方式收集 hello 資料以供分析。 當使用 Azure 診斷，資料會寫入立即 tooLog 分析，而且沒有任何需要 toofirst 寫入 hello 資料 toostorage。

支援的 azure 資源[Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)可以傳送其記錄檔和度量直接 tooLog 分析。

* Hello hello 可用度量的詳細資訊，請參閱太[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。
* Hello 的 hello 可用的記錄檔的詳細資訊，請參閱太[支援診斷記錄檔的服務和結構描述](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)。

### <a name="enable-diagnostics-with-powershell"></a>啟用 PowerShell 的診斷功能
您需要 hello 年 11 月 2016 (v2.3.0) 或更新版本的版本[Azure PowerShell](/powershell/azure/overview)。

hello 下列 PowerShell 範例會示範如何 toouse[組 AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable 診斷上的網路安全性群組。 hello 相同的方法適用於所有支援的資源-設定`$resourceId`toohello 想 tooenable 診斷的 hello 資源的資源識別碼。

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>使用 Resource Manager 範本啟用診斷

tooenable 診斷而建立，而且有 hello 診斷傳送 tooyour 記錄分析工作區，您可以使用其中一個範本類似 toohello 下方時，在資源上。 這個範例是針對自動化帳戶，但也適用於所有支援的資源類型。

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Azure 診斷 toostorage 然後 tooLog 分析

收集來自某些資源內的記錄檔，可能 toosend hello 記錄檔 tooAzure 儲存體，並接著設定從儲存體的記錄分析 tooread hello 記錄檔。

記錄分析可使用此方法 toocollect 診斷從 Azure 儲存體 hello 下列資源和記錄檔：

| 資源 | 記錄檔 |
| --- | --- |
| Service Fabric |ETWEvent <br> 運作事件 <br> Reliable Actor 事件 <br> Reliable Service 事件 |
| 虛擬機器 |Linux Syslog <br> Windows 事件 <br> IIS 記錄 <br> Windows ETWEvent |
| Web 角色 <br> 背景工作角色 |Linux Syslog <br> Windows 事件 <br> IIS 記錄 <br> Windows ETWEvent |

> [!NOTE]
> 您會將一般的 Azure 資料或是儲存和交易，當您將診斷傳送 tooa 儲存體帳戶，以及當記錄分析儲存體帳戶讀取 hello 資料支付費用。
>
>

請參閱[事件的 IIS 和資料表儲存體使用 blob 儲存體](log-analytics-azure-storage-iis-table.md)toolearn 深入了解如何收集記錄分析這些記錄檔。

## <a name="connectors-for-azure-services"></a>Azure 服務的連接器

沒有 Application Insights，可讓傳送 tooLog 分析的 Application Insights toobe 所收集資料的連接器。

深入了解 hello [Application Insights 連接器](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)。

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>指令碼 toocollect 和 post 資料 tooLog 分析

Azure 服務不提供直接的方式 toosend 記錄檔和度量 tooLog 分析，您可以使用 Azure 自動化指令碼 toocollect hello 記錄和度量。 hello 指令碼可以再傳送嗨資料 tooLog 分析使用 hello[資料收集器 API](log-analytics-data-collector-api.md)

hello Azure 範本庫具有[使用 Azure 自動化的範例](https://azure.microsoft.com/en-us/resources/templates/?term=OMS)toocollect 資料服務，將它傳送 tooLog 分析。

## <a name="next-steps"></a>後續步驟

* [事件的 IIS 和資料表儲存體使用 blob 儲存體](log-analytics-azure-storage-iis-table.md)tooread hello 記錄檔寫入 tootable 診斷儲存體或 IIS 記錄檔中寫入的 tooblob 儲存體的 Azure 服務。
* [啟用方案](log-analytics-add-solutions.md)tooprovide 深入了解 hello 資料。
* [使用搜尋查詢](log-analytics-log-searches.md)tooanalyze hello 資料。
