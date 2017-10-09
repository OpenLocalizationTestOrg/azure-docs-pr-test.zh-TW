---
title: "管理事件 tooActivity 記錄檔警示上的 aaaMigrate Azure 警示 |Microsoft 文件"
description: "管理事件的警示將於 10 月 1 日移除。 藉由移轉現有警示來做準備。"
author: johnkemnetz
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
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>移轉 Azure 上管理事件 tooActivity 記錄警示的警示


> [!WARNING]
> 管理事件的警示將於 10 月 1 日或之後關閉。 如果您有這些警示，並將其遷移，若是如此，請使用以下 toounderstand hello 方向。
>
> 

## <a name="what-is-changing"></a>變更內容

Azure 監視器 (先前稱為 Azure Insights) 提供了功能 toocreate 警示觸發開管理事件並產生通知 tooa webhook URL 或電子郵件地址。 您已使用任何一種方法建立下列其中一種警示：
* Hello 特定資源類型的 Azure 入口網站，在 監視-> 警示-> 加入警示，「 警示 」 設定的位置太 「 事件 」
* 執行 hello 新增 AzureRmLogAlertRule PowerShell cmdlet
* 直接使用[hello 警示的 REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type ="ManagementEventRuleCondition 」 和 dataSource.odata.type ="RuleManagementEventDataSource"
 
hello 下列 PowerShell 指令碼傳回所有警示的清單上您在您的訂用帳戶，以及每個警示上所設定的 hello 條件的管理事件。

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

如果您不有任何警示管理事件上，上述的 hello PowerShell cmdlet 會輸出一系列的警告訊息，如下所示：

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

您可以忽略這些警告訊息。 如果您沒有警示管理事件，此 PowerShell cmdlet hello 輸出看起來像這樣：

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

以虛線分隔每個警示，且詳細資料包含 hello hello 警示和 hello 受監視的特定規則的資源識別碼。

這項功能已轉換太[Azure 監視活動記錄檔警示](monitoring-activity-log-alerts.md)。 這些新的警示會讓您 tooset 活動記錄檔事件上的條件，而且新的事件符合 hello 條件時收到通知。 管理事件的警示也有好幾項改善功能：
* 您可以在使用許多警示的重複使用您的通知收件者 （「 動作 」） 的群組[動作群組](monitoring-action-groups.md)，減少 hello 複雜度變更誰應該收到警示。
* 您可以使用簡訊搭配動作群組，直接在電話上接收通知。
* 您可以[使用 Resource Manager 範本建立活動記錄警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。
* 您可以使用更大的彈性和複雜性 toomeet 建立條件，您的特定需求。
* 更快速地傳遞通知。
 
## <a name="how-toomigrate"></a>如何 toomigrate
 
toocreate 新活動記錄警示，您可以：
* 請遵循[我們如何 toocreate 警示中的 hello Azure 入口網站上的指南](monitoring-activity-log-alerts.md)
* 了解如何太[使用資源管理員範本建立警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
您先前建立的管理事件的警示將不會自動移轉的 tooActivity 記錄警示。 您需要 toouse hello 上述 PowerShell 指令碼 toolist hello 警示管理事件，您目前已設定，並以手動方式重新建立它們，為活動記錄警示。 這必須在 10 月 1 日之前完成，之後您的 Azure 訂用帳戶將不再顯示管理事件的警示。 其他類型的 Azure 警示，包括 Azure 監視器計量警示、Application Insights 警示，以及不受此變更影響的 Log Analytics 警示。 如果您有任何問題，將張貼到下面的 hello 註解。


## <a name="next-steps"></a>後續步驟

* 深入了解[活動記錄](monitoring-overview-activity-logs.md)
* [透過 Azure 入口網站設定活動記錄警示](monitoring-activity-log-alerts.md)
* [透過 Resource Manager 設定活動記錄警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* 檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)
* 深入了解[服務通知](monitoring-service-notifications.md)
* 深入了解[動作群組](monitoring-action-groups.md)
