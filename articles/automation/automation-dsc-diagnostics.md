---
title: "Azure 自動化 DSC 報告資料 tooOMS 記錄分析 aaaForward |Microsoft 文件"
description: "本文示範如何 toosend 預期狀態設定 (DSC) 報告資料 tooMicrosoft Operations Management Suite 記錄分析 toodeliver 見解，並管理。"
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>轉送 Azure 自動化 DSC 報告資料 tooOMS 記錄分析

自動化可以傳送 DSC 節點狀態資料 tooyour Microsoft Operations Management Suite (OMS) 的記錄分析工作區。  
相容性狀態會顯示在 hello Azure 入口網站或 PowerShell，針對節點和節點設定中個別的 DSC 資源。 透過 Log Analytics，您可以：

* 取得受管理節點與個別資源的合規性資訊
* 根據合規性狀態觸發電子郵件或警示
* 撰寫受管理節點之間的進階查詢
* 相互關聯自動化帳戶之間的合規性狀態
* 以視覺化方式呈現一段時間的合規性歷程記錄

## <a name="prerequisites"></a>必要條件

toostart 傳送自動化 DSC 報告 tooLog 分析，您需要：

* hello 2016 年 11 月版或更新版本的版本[Azure PowerShell](/powershell/azure/overview) (v2.3.0)。
* Azure 自動化帳戶。 如需詳細資訊，請參閱[開始使用 Azure 自動化](automation-offering-get-started.md)。
* 提供 [自動化與控制] 服務的 Log Analytics 工作區。 如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。
* 至少一個 Azure Automation DSC 節點。 如需詳細資訊，請參閱[將機器上架交由 Azure Automation DSC 管理](automation-dsc-onboarding.md)。 

## <a name="set-up-integration-with-log-analytics"></a>設定與 Log Analytics 整合

將資料匯入從 Azure Automation DSC 記錄分析，完成下列步驟的 hello toobegin:

1. 在 PowerShell 中的 Azure 帳戶登入 tooyour 中。 請參閱[使用 Azure PowerShell 登入](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. 取得 hello _ResourceId_您的自動化帳戶執行下列 PowerShell 命令的 hello: (如果您有多個自動化帳戶時，選擇 hello _ResourceID_ hello 您想要的帳戶tooconfigure)。

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. 取得 hello _ResourceId_的記錄分析工作區中執行下列 PowerShell 命令的 hello: (如果您有多個工作區中，選擇 hello _ResourceID_ hello 您想要的工作區tooconfigure)。

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. 下列 PowerShell 命令，取代執行的 hello`<AutomationResourceId>`和`<WorkspaceResourceId>`以 hello _ResourceId_ hello 前一步驟的每個值：

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

如果您想將資料匯入從 Azure Automation DSC 記錄分析 toostop，執行下列 PowerShell 命令的 hello。

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>檢視 hello DSC 記錄檔

Automation DSC 資料與記錄分析的整合設定之後**記錄搜尋**按鈕將會出現在 hello **DSC 節點**刀鋒視窗中的自動化帳戶。 按一下 hello**記錄搜尋**按鈕 tooview hello 記錄檔以取得 DSC 節點資料。

![記錄搜尋按鈕](media/automation-dsc-diagnostics/log-search-button.png)

hello**記錄搜尋**刀鋒視窗隨即開啟，而且您看見**DscNodeStatusData**每個 DSC 節點、 作業和**DscResourceStatusData**每個作業[DSC資源](https://msdn.microsoft.com/powershell/dsc/resources)呼叫 hello 節點組態套用的 toothat 節點中。

hello **DscResourceStatusData**作業包含失敗的任何 DSC 資源資訊時發生錯誤。

按一下 hello 清單 toosee hello 資料中的每項作業，該作業。

您也可以檢視 hello 記錄檔 [記錄分析搜尋。 請參閱[使用記錄搜尋尋找資料](../log-analytics/log-analytics-log-searches.md)。
型別 hello 下列查詢會 toofind 您 DSC 記錄檔：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

您也可以縮小 hello 查詢 hello 作業名稱。 例如：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>DSC 合規性檢查失敗時傳送電子郵件

我們最上層的客戶的要求是針對 hello 能力 toosend 電子郵件或文字時出錯 DSC 設定。   

toocreate 警示規則時，它會先建立應叫用 hello 警示的 hello DSC 報表記錄的記錄搜尋。  按一下 hello**警示**按鈕 toocreate 及設定 hello 警示規則。

1. 從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。
1. 輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  如果您已將設定從多個自動化帳戶或訂用帳戶 tooyour 工作區的記錄檔，您可以群組您的訂用帳戶和自動化帳戶的警示。  
  自動化帳戶名稱可以衍生自 DscNodeStatusData hello 搜尋中的 hello 資源欄位。  
1. tooopen hello**加入警示規則**畫面上，按一下**警示**hello 頁面頂端的 hello。 如需有關 hello 選項 tooconfigure hello 警示的詳細資訊，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。

### <a name="find-failed-dsc-resources-across-all-nodes"></a>在所有節點間尋找失敗的 DSC 資源

使用 Log Analytics 的優點之一，是您可以在所有節點間搜尋失敗的檢查。
toofind 失敗的 DSC 資源的所有執行個體。

1. 從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。
1. 輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>檢視歷程記錄 DSC 節點狀態

最後，您可能想 toovisualize DSC 節點狀態歷程記錄一段時間。  
您可以使用這個查詢 toosearch hello 狀態為您 DSC 節點的狀態，經過一段時間。

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

經過一段時間，這會顯示 hello 節點狀態的圖表。

## <a name="log-analytics-records"></a>Log Analytics 記錄

來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種記錄類別。

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| 屬性 | 說明 |
| --- | --- |
| TimeGenerated |日期和時間執行 hello 相容性檢查的時間。 |
| OperationName |DscNodeStatusData |
| ResultType |Hello 節點是否相容。 |
| NodeName_s |hello hello 受管理的節點名稱。 |
| NodeComplianceStatus_s |Hello 節點是否相容。 |
| DscReportStatus |Hello 相容性檢查是否已順利執行。 |
| ConfigurationMode | 如何 hello 設定是套用的 toohello 節點。 可能的值為 __"ApplyOnly"__、__"ApplyandMonitior"__ 和 __"ApplyandAutoCorrect"__。 <ul><li>__ApplyOnly__: DSC 會套用 hello 組態，並且不執行進一步除非新的設定已推送 toohello 目標節點，或當從伺服器提取新的設定。 初始套用新的設定之後，DSC 不會檢查先前設定的狀態是否漂移。 DSC 在成功完成之前嘗試 tooapply hello 組態__ApplyOnly__才會生效。 </li><li> __ApplyAndMonitor__： 這是 hello 預設值。 hello LCM 適用於任何新的設定。 初始新設定的應用程式之後, 如果 hello 目標節點偏離預期 hello 狀態，DSC 會報告記錄檔中的 hello 差異。 DSC 在成功完成之前嘗試 tooapply hello 組態__ApplyAndMonitor__才會生效。</li><li>__ApplyAndAutoCorrect__：DSC 會套用任何新的設定。 之後的新設定，如果 hello 目標節點偏離預期 hello 狀態，DSC 會報告記錄檔中的 hello 差異，然後重新套用目前設定的 hello。</li></ul> |
| HostName_s | hello hello 受管理的節點名稱。 |
| IPAddress | hello hello IPv4 位址受管理節點。 |
| 類別 | DscNodeStatus |
| 資源 | hello hello Azure 自動化帳戶名稱。 |
| Tenant_g | 識別 hello 呼叫端的 hello 租用戶的 GUID。 |
| NodeId_g |GUID，識別 hello 受管理的節點。 |
| DscReportId_g |GUID，識別 hello 報表。 |
| LastSeenTime_t |日期和上次檢視 hello 報表時的時間。 |
| ReportStartTime_t |日期和時間啟動 hello 報表時。 |
| ReportEndTime_t |日期和時間 hello 報表完成時。 |
| NumberOfResources_d |DSC 資源的 hello 數目稱為 hello 套用設定 toohello 節點中。 |
| SourceSystem | 記錄分析收集 hello 資料的方式。 針對 Azure 診斷，一律為 Azure 。 |
| ResourceId |指定 hello Azure 自動化帳戶。 |
| ResultDescription | hello 描述這項作業。 |
| SubscriptionId | hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。 |
| ResourceGroup | Hello 自動化帳戶 hello 資源群組名稱。 |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |為 hello hello 符合性報告的相互關聯識別碼的 GUID。 |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| 屬性 | 說明 |
| --- | --- |
| TimeGenerated |日期和時間執行 hello 相容性檢查的時間。 |
| OperationName |DscResourceStatusData|
| ResultType |Hello 資源是否相容。 |
| NodeName_s |hello hello 受管理的節點名稱。 |
| 類別 | DscNodeStatus |
| 資源 | hello hello Azure 自動化帳戶名稱。 |
| Tenant_g | 識別 hello 呼叫端的 hello 租用戶的 GUID。 |
| NodeId_g |GUID，識別 hello 受管理的節點。 |
| DscReportId_g |GUID，識別 hello 報表。 |
| DscResourceId_s |hello hello DSC 資源執行個體名稱。 |
| DscResourceName_s |hello hello DSC 資源名稱。 |
| DscResourceStatus_s |Hello DSC 資源是否處於相容性。 |
| DscModuleName_s |hello hello PowerShell 模組包含 hello DSC 資源的名稱。 |
| DscModuleVersion_s |hello hello PowerShell 模組包含 hello DSC 資源版本。 |
| DscConfigurationName_s |hello hello 組態名稱套用 toohello 節點。 |
| ErrorCode_s | hello 錯誤碼 hello 資源失敗。 |
| ErrorMessage_s |hello 的錯誤訊息如果 hello 資源失敗。 |
| DscResourceDuration_d |hello 時間 （秒），執行 hello DSC 資源。 |
| SourceSystem | 記錄分析收集 hello 資料的方式。 針對 Azure 診斷，一律為 Azure 。 |
| ResourceId |指定 hello Azure 自動化帳戶。 |
| ResultDescription | hello 描述這項作業。 |
| SubscriptionId | hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。 |
| ResourceGroup | Hello 自動化帳戶 hello 資源群組名稱。 |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |為 hello hello 符合性報告的相互關聯識別碼的 GUID。 |

## <a name="summary"></a>摘要

藉由傳送您的自動化 DSC 資料 tooLog 分析，您可以取得更深入 hello 由您 Automation DSC 的節點狀態：

* 設定警示 toonotify 您發生問題時
* 使用自訂檢視和搜尋查詢 toovisualize 您 runbook 結果、 runbook 工作狀態、 和其他相關的主要指標或度量。  

記錄分析會提供更大的操作的可見性 tooyour Automation DSC 資料，而且可以更快速地協助位址事件。  

## <a name="next-steps"></a>後續步驟

* toolearn 有關 tooconstruct 不同的搜尋查詢，並檢閱 hello Automation DSC 的詳細資訊，記錄和記錄分析，請參閱[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)
* toolearn 進一步了解使用 Azure 自動化 DSC，請參閱[開始使用 Azure 自動化 DSC](automation-dsc-getting-started.md)
* toolearn 深入了解 OMS 記錄分析和資料集合來源，請參閱[收集 Azure 儲存體中的資料記錄分析概觀](../log-analytics/log-analytics-azure-storage.md)

