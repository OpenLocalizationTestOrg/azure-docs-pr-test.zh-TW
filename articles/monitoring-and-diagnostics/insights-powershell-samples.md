---
title: "aaaAzure 監視 PowerShell 快速入門範例。 | Microsoft Docs"
description: "使用 PowerShell tooaccess Azure 監視功能，例如自動調整規模、 警示、 webhook 和搜尋活動記錄檔。"
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Azure 監視器 PowerShell 快速入門範例
此發行項會顯示範例 PowerShell 命令 toohelp 您存取 Azure 監視功能。 Azure 監視器可讓您 tooAutoScale 雲端服務、 虛擬機器和 Web 應用程式和 toosend 警示通知或呼叫 web Url 根據設定的遙測資料的值。

> [!NOTE]
> Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。 不過，hello 命名空間，因此 hello 遵循命令仍包含 hello"見解"。
> 
> 

## <a name="set-up-powershell"></a>設定 PowerShell
如果您還沒有這麼做，設定您的電腦上的 PowerShell toorun。 如需詳細資訊，請參閱[如何 tooInstall 和設定 PowerShell](/powershell/azure/overview)。

## <a name="examples-in-this-article"></a>本文中的範例
hello 文件中的 hello 範例說明如何使用 Azure 監視器 cmdlet。 您也可以檢閱 hello Azure 監視 PowerShell cmdlet，在整個清單[Azure 監視器 （深入剖析） Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx)。

## <a name="sign-in-and-use-subscriptions"></a>登入和使用訂用帳戶
首先，登入 tooyour Azure 訂用帳戶。

```PowerShell
Login-AzureRmAccount
```

這需要您 toosign 中。 一旦登入之後，就會顯示您的帳戶、TenantID 和預設的訂用帳戶識別碼。 所有 hello Azure cmdlet hello 內容的預設訂用帳戶中的工作。 您擁有存取權的訂用帳戶 tooview hello 清單，請使用下列命令的 hello。

```PowerShell
Get-AzureRmSubscription
```

toochange 您工作內容 tooa 不同訂用帳戶，下列命令使用 hello。

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>擷取訂用帳戶的活動記錄檔
使用 hello `Get-AzureRmLog` cmdlet。  hello 以下是一些常見的範例。

從這個日期/時間 toopresent 取得記錄項目：

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

取得某個時間/日期範圍間的記錄檔項目︰

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

取得特定資源群組中的記錄檔項目︰

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

從特定的資源提供者取得某個時間/日期範圍間的記錄檔項目︰

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

取得包含特定呼叫者的所有記錄檔項目︰

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

下列命令擷取 hello hello 活動記錄檔中的最近 1000 則事件 hello:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` 支援其他許多參數。 請參閱 hello`Get-AzureRmLog`參考，如需詳細資訊。

> [!NOTE]
> `Get-AzureRmLog` 只提供 15 天的歷程記錄。 使用 hello **-MaxEvents**參數可讓您 tooquery hello 最後 n 個事件，超過 15 天。 tooaccess 事件超過 15 天，都會使用 hello REST API 或 SDK （C# 範例使用 hello SDK）。 如果您未包含**StartTime**，hello 預設值為**EndTime**減一小時。 如果您未包含**EndTime**，hello 預設值為目前的時間。 所有時間都是採用 UTC 格式。
> 
> 

## <a name="retrieve-alerts-history"></a>擷取警示歷程記錄
所有警示的事件，您可以查詢的 tooview hello Azure 資源管理員記錄檔使用 hello 遵循範例。

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

tooview hello 記錄特定警示的規則，您可以使用 hello `Get-AzureRmAlertHistory` cmdlet，傳入 hello hello 警示規則的資源識別碼。

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

hello`Get-AzureRmAlertHistory`指令程式支援各種不同的參數。 如需詳細資訊，請參閱 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)。

## <a name="retrieve-information-on-alert-rules"></a>擷取警示規則的相關資訊
所有的下列命令的 hello 作用於名為"montest"的資源群組。

檢視所有 hello 屬性 hello 警示規則：

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

擷取資源群組上的所有警示︰

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

擷取針對目標資源設定的所有警示規則。 例如，在 VM 上設定的所有警示規則。

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` 支援其他參數。 如需詳細資訊，請參閱 [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 。

## <a name="create-metric-alerts"></a>建立計量警示
您可以使用 hello `Add-AlertRule` cmdlet toocreate 更新或停用警示規則。

您可以分別使用 `New-AzureRmAlertRuleEmail` 和 `New-AzureRmAlertRuleWebhook` 建立電子郵件和 Webhook 屬性。 在 hello 警示規則的 cmdlet，將指派為動作 toohello**動作**hello 警示規則的屬性。

hello 下表描述 hello 參數，以及值使用的 toocreate 使用度量的警示。

| 參數 | value |
| --- | --- |
| 名稱 |simpletestdiskwrite |
| 此警示規則的位置 |美國東部 |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName hello 警示所建立的 |\PhysicalDisk (_Total) \Disk writes/sec。請參閱 hello `Get-MetricDefinitions` cmdlet 關於 tooretrieve hello 確切的度量名稱的方式 |
| operator |GreaterThan |
| 臨界值 (此計量的計數/秒） |1 |
| WindowSize (hh:mm:ss 格式) |00:05:00 |
| 彙總工具 （hello 標準，在此情況下使用平均計數的統計資料） |平均值 |
| 自訂電子郵件 (字串陣列) |'foo@example.com','bar@example.com' |
| 傳送電子郵件 tooowners、 參與者與讀者 |-SendToServiceOwners |

建立電子郵件動作

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

建立 Webhook 動作

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

在傳統的 VM 上的 hello CPU %度量建立 hello 警示規則

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

擷取 hello 警示規則

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

如果警示規則已存在指定屬性的 hello hello 新增警示 cmdlet 也會更新 hello 規則。 toodisable 警示規則，包括 hello 參數**-DisableRule**。

## <a name="get-a-list-of-available-metrics-for-alerts"></a>取得可用警示計量的清單
您可以使用 hello `Get-AzureRmMetricDefinition` cmdlet tooview hello 清單的特定資源的所有度量。

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

hello 下列範例會產生包含 hello 度量名稱的資料表和它 hello 單位。

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

`Get-AzureRmMetricDefinition` 的可用選項完整清單可在 [Get MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)取得。

## <a name="create-and-manage-autoscale-settings"></a>建立和管理自動調整設定
諸如 Web 應用程式、VM、雲端服務或虛擬機器擴展集之類的資源只能設定一個自動調整設定。
不過，每個自動調整設定都可以有多個設定檔。 例如，一個用於以效能為基礎的調整設定檔，以及一個用於以排程為基礎的設定檔。 每個設定檔都可以設定多個規則。 如需自動調整規模的詳細資訊，請參閱[如何 tooAutoscale 應用程式](../cloud-services/cloud-services-how-to-scale.md)。

我們將使用的 hello 步驟如下：

1. 建立規則。
2. 建立設定檔對應 hello 規則您先前建立 toohello 設定檔。
3. 選擇性︰設定 Webhook 和電子郵件的屬性，以建立自動調整的通知。
4. 藉由對應 hello 設定檔和 hello 先前步驟中建立的通知 hello 目標資源的名稱建立的自動調整規模設定。

hello 下列範例將示範如何建立自動調整規模設定的虛擬機器擴展集使用 hello CPU 使用量度量的 Windows 作業系統。

首先，建立規則 tooscale 外，執行個體計數增加。

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

與執行個體計數減少，接下來，tooscale 中建立的規則。

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

接著，建立 hello 規則的設定檔。

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

建立 Webhook 屬性。

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

建立 hello hello 自動調整設定，包括電子郵件通知屬性和 hello 您先前建立的 webhook。

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

最後，建立 hello 自動調整規模設定 tooadd hello 設定檔，您先前所建立。

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

如需有關管理自動調整設定的詳細資訊，請參閱 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)。

## <a name="autoscale-history"></a>自動調整歷程記錄
hello 下列範例示範您可以檢視新的自動調整規模及警示事件的方式。 使用 hello 活動記錄檔搜尋 tooview hello 自動調整歷程記錄。

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

您可以使用 hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve 自動調整歷程記錄。

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

如需詳細資訊，請參閱 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)。

### <a name="view-details-for-an-autoscale-setting"></a>檢視自動調整設定的詳細資料
您可以使用 hello `Get-Autoscalesetting` cmdlet tooretrieve hello 自動調整規模設定的詳細資訊。

hello 下列範例顯示所有的自動調整規模設定的相關詳細資料中 hello 資源群組 'myrg1'。

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

hello 下列範例顯示 hello 資源群組 'myrg1' 中的所有自動調整規模設定的詳細，並特別 hello 名為 'MyScaleVMSSSetting' 的自動調整規模設定。

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>移除自動調整設定
您可以使用 hello `Remove-Autoscalesetting` cmdlet toodelete 自動調整規模設定。

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>管理活動記錄檔的記錄檔設定檔
您可以建立*記錄設定檔*和匯出資料，從 [活動記錄 tooa 儲存體帳戶，而且您可以為其設定資料保留。 （選擇性） 您也可以串流 hello 資料 tooyour 事件中心。 請注意，此功能目前處於預覽狀態，而且每個訂用帳戶只能建立一個記錄檔設定檔。 您可以使用下列指令程式，其目前的訂用帳戶 toocreate hello 和管理記錄檔設定檔。 您也可以選擇特定的訂用帳戶。 雖然 PowerShell 預設 toohello 目前訂用帳戶，您隨時可以變更該使用`Set-AzureRmContext`。 您可以設定活動記錄 tooroute 資料 tooany 儲存體帳戶或事件中心內該訂用帳戶。 資料會以 JSON 格式的 Blob 檔案寫入。

### <a name="get-a-log-profile"></a>取得記錄檔設定檔
toofetch 現有的記錄檔設定檔使用 hello `Get-AzureRmLogProfile` cmdlet。

### <a name="add-a-log-profile-without-data-retention"></a>新增沒有資料保留期的記錄檔設定檔
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>移除記錄檔設定檔
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>新增包含資料保留期的記錄檔設定檔
您可以指定 hello **-RetentionInDays** hello 數天內，為正整數，hello 資料會保留其中的內容。

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>新增包含保留期與 EventHub 的記錄檔設定檔
加法 toorouting 中您資料的 toostorage 帳戶，您可以也串流處理它 tooan 事件中心。 請注意，在此預覽版本和 hello 的儲存體帳戶設定是強制性事件中樞設定是選擇性的。

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>設定診斷記錄檔
許多 Azure 服務提供額外的記錄檔，可以是 Azure 儲存體帳戶中，設定的 toosave 資料的遙測傳送 tooEvent 中樞和/或傳送 tooan OMS 記錄分析工作區。 在資源層級只能執行該作業和 hello 儲存體帳戶或事件中心應該會出現在 hello 其中 hello 診斷設定與 hello 目標資源相同的區域。

### <a name="get-diagnostic-setting"></a>取得診斷設定
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

停用診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

啟用不含保留期的診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

啟用含保留期的診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

針對特定的記錄檔類別，啟用含保留期的診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

啟用事件中樞的診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

啟用 OMS 的診斷設定

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
