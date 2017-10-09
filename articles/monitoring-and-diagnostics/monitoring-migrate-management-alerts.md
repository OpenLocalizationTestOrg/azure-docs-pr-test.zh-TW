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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="9807d-104">移轉 Azure 上管理事件 tooActivity 記錄警示的警示</span><span class="sxs-lookup"><span data-stu-id="9807d-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="9807d-105">管理事件的警示將於 10 月 1 日或之後關閉。</span><span class="sxs-lookup"><span data-stu-id="9807d-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="9807d-106">如果您有這些警示，並將其遷移，若是如此，請使用以下 toounderstand hello 方向。</span><span class="sxs-lookup"><span data-stu-id="9807d-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="9807d-107">變更內容</span><span class="sxs-lookup"><span data-stu-id="9807d-107">What is changing</span></span>

<span data-ttu-id="9807d-108">Azure 監視器 (先前稱為 Azure Insights) 提供了功能 toocreate 警示觸發開管理事件並產生通知 tooa webhook URL 或電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9807d-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="9807d-109">您已使用任何一種方法建立下列其中一種警示：</span><span class="sxs-lookup"><span data-stu-id="9807d-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="9807d-110">Hello 特定資源類型的 Azure 入口網站，在 監視-> 警示-> 加入警示，「 警示 」 設定的位置太 「 事件 」</span><span class="sxs-lookup"><span data-stu-id="9807d-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="9807d-111">執行 hello 新增 AzureRmLogAlertRule PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="9807d-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="9807d-112">直接使用[hello 警示的 REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type ="ManagementEventRuleCondition 」 和 dataSource.odata.type ="RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="9807d-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="9807d-113">hello 下列 PowerShell 指令碼傳回所有警示的清單上您在您的訂用帳戶，以及每個警示上所設定的 hello 條件的管理事件。</span><span class="sxs-lookup"><span data-stu-id="9807d-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="9807d-114">如果您不有任何警示管理事件上，上述的 hello PowerShell cmdlet 會輸出一系列的警告訊息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9807d-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="9807d-115">您可以忽略這些警告訊息。</span><span class="sxs-lookup"><span data-stu-id="9807d-115">These warning messages can be ignored.</span></span> <span data-ttu-id="9807d-116">如果您沒有警示管理事件，此 PowerShell cmdlet hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="9807d-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="9807d-117">以虛線分隔每個警示，且詳細資料包含 hello hello 警示和 hello 受監視的特定規則的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="9807d-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="9807d-118">這項功能已轉換太[Azure 監視活動記錄檔警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="9807d-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="9807d-119">這些新的警示會讓您 tooset 活動記錄檔事件上的條件，而且新的事件符合 hello 條件時收到通知。</span><span class="sxs-lookup"><span data-stu-id="9807d-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="9807d-120">管理事件的警示也有好幾項改善功能：</span><span class="sxs-lookup"><span data-stu-id="9807d-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="9807d-121">您可以在使用許多警示的重複使用您的通知收件者 （「 動作 」） 的群組[動作群組](monitoring-action-groups.md)，減少 hello 複雜度變更誰應該收到警示。</span><span class="sxs-lookup"><span data-stu-id="9807d-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="9807d-122">您可以使用簡訊搭配動作群組，直接在電話上接收通知。</span><span class="sxs-lookup"><span data-stu-id="9807d-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="9807d-123">您可以[使用 Resource Manager 範本建立活動記錄警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="9807d-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="9807d-124">您可以使用更大的彈性和複雜性 toomeet 建立條件，您的特定需求。</span><span class="sxs-lookup"><span data-stu-id="9807d-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="9807d-125">更快速地傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="9807d-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="9807d-126">如何 toomigrate</span><span class="sxs-lookup"><span data-stu-id="9807d-126">How toomigrate</span></span>
 
<span data-ttu-id="9807d-127">toocreate 新活動記錄警示，您可以：</span><span class="sxs-lookup"><span data-stu-id="9807d-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="9807d-128">請遵循[我們如何 toocreate 警示中的 hello Azure 入口網站上的指南](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="9807d-129">了解如何太[使用資源管理員範本建立警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="9807d-130">您先前建立的管理事件的警示將不會自動移轉的 tooActivity 記錄警示。</span><span class="sxs-lookup"><span data-stu-id="9807d-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="9807d-131">您需要 toouse hello 上述 PowerShell 指令碼 toolist hello 警示管理事件，您目前已設定，並以手動方式重新建立它們，為活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="9807d-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="9807d-132">這必須在 10 月 1 日之前完成，之後您的 Azure 訂用帳戶將不再顯示管理事件的警示。</span><span class="sxs-lookup"><span data-stu-id="9807d-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="9807d-133">其他類型的 Azure 警示，包括 Azure 監視器計量警示、Application Insights 警示，以及不受此變更影響的 Log Analytics 警示。</span><span class="sxs-lookup"><span data-stu-id="9807d-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="9807d-134">如果您有任何問題，將張貼到下面的 hello 註解。</span><span class="sxs-lookup"><span data-stu-id="9807d-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9807d-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9807d-135">Next steps</span></span>

* <span data-ttu-id="9807d-136">深入了解[活動記錄](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="9807d-137">[透過 Azure 入口網站設定活動記錄警示](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="9807d-138">[透過 Resource Manager 設定活動記錄警示](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="9807d-139">檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="9807d-140">深入了解[服務通知](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="9807d-141">深入了解[動作群組](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
