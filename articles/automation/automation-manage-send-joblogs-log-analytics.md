---
title: "Azure 自動化工作資料 tooOMS 記錄分析 aaaForward |Microsoft 文件"
description: "本文示範 toosend 工作狀態和 runbook 工作資料流 tooMicrosoft Operations Management Suite 記錄分析 toodeliver 其他深入資訊和管理。"
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>從自動化 tooLog 分析 (OMS) 轉送作業的狀態和作業資料流
自動化可以傳送 runbook 工作狀態和作業資料流 tooyour Microsoft Operations Management Suite (OMS) 記錄分析工作區。  作業記錄和作業資料流會顯示在 hello Azure 入口網站，或使用 PowerShell，針對個別作業，而這可讓您 tooperform 簡單的調查。 現在透過 Log Analytics，您可以：

* 針對自動化工作取得深入解析
* 根據您的 Runbook 作業狀態 (例如已失敗或已暫停) 觸發電子郵件或警示
* 撰寫工作資料流之間的進階查詢
* 在自動化帳戶之間相互關聯工作
* 視覺化一段時間的工作歷程記錄     

## <a name="prerequisites-and-deployment-considerations"></a>先決條件和部署考量
傳送自動化 toostart 記錄 tooLog 分析，您需要：

1. hello 2016 年 11 月版或更新版本的版本[Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0)。
2. Log Analytics 工作區。 如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。 
3. hello ResourceId Azure 自動化帳戶

Azure 自動化帳戶，記錄分析工作區中，執行下列 PowerShell hello toofind hello ResourceId:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

如果您有多個自動化帳戶，或工作區、 hello 輸出中的 hello 上述命令，尋找 hello*名稱*您需要 tooconfigure 並複製 hello 值*ResourceId*。

如果您需要 toofind hello*名稱*自動化帳戶、 在 hello Azure 入口網站選取自動化帳戶從 hello**自動化帳戶**刀鋒視窗，然後選取**的所有設定**.  從 hello**所有設定**刀鋒視窗底下**帳戶設定**選取**屬性**。  在 hello**屬性**刀鋒視窗中，您可以注意這些值。<br> ![自動化帳戶屬性](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)。

## <a name="set-up-integration-with-log-analytics"></a>設定與 Log Analytics 整合
1. 在您的電腦上啟動**Windows PowerShell**從 hello**啟動**螢幕。  
2. 複製並貼上 hello 下列 PowerShell，然後編輯 hello 的 hello 值`$workspaceId`和`$automationAccountId`。  Hello`-Environment`參數，有效值為*AzureCloud*或*AzureUSGovernment*視您工作所在的 hello 雲端環境而定。     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

執行這個指令碼之後，您將會在寫入新 JobLogs 或 JobStreams 的 10 分鐘內，於 Log Analytics 中看見記錄。

toosee hello 記錄檔，執行下列查詢在記錄分析記錄搜尋中的 hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>驗證組態
tooconfirm 傳送您的自動化帳戶記錄 tooyour 記錄分析工作區，請檢查診斷上使用下列 PowerShell hello hello 自動化帳戶已正確設定：

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Hello 輸出中，請確定：
+ 在下*記錄*，hello 值*啟用*是*，則為 True*
+ hello 值*工作區識別碼*toohello ResourceId 記錄分析工作區的設定


## <a name="log-analytics-records"></a>Log Analytics 記錄
來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種類型的記錄，並標記為 **Type=AzureDiagnostics**。

### <a name="job-logs"></a>作業記錄檔
| 屬性 | 說明 |
| --- | --- |
| TimeGenerated |日期和時間 hello runbook 工作執行時。 |
| RunbookName_s |hello hello runbook 名稱。 |
| Caller_s |誰 hello 作業。  可能的值為電子郵件地址或排程作業的系統。 |
| Tenant_g | 識別 hello 呼叫端的 hello 租用戶的 GUID。 |
| JobId_g |為 hello 識別碼 hello runbook 工作的 GUID。 |
| ResultType |hello hello runbook 工作的狀態。  可能的值包括：<br>- Started (已啟動)<br>- Stopped (已停止)<br>- Suspended (暫止)<br>- Failed (失敗)<br>- Completed (已完成) |
| 類別 | Hello 的資料類型的分類。  自動化，hello 值為 JobLogs。 |
| OperationName | 指定在 Azure 中執行作業的 hello 型別。  自動化，hello 值會是工作。 |
| 資源 | Hello 自動化帳戶的名稱 |
| SourceSystem | 記錄分析收集 hello 資料的方式。 針對 Azure 診斷，一律為 Azure 。 |
| ResultDescription |描述 hello runbook 工作的結果狀態。  可能的值包括：<br>- Job is started (工作已啟動)<br>- Job Failed (工作失敗)<br>- Job Completed |
| CorrelationId |為 hello 相互關聯識別碼 hello runbook 工作的 GUID。 |
| ResourceId |指定 hello runbook hello Azure 自動化帳戶資源的 id。 |
| SubscriptionId | hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。 |
| ResourceGroup | Hello 自動化帳戶 hello 資源群組名稱。 |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>作業串流
| 屬性 | 說明 |
| --- | --- |
| TimeGenerated |日期和時間 hello runbook 工作執行時。 |
| RunbookName_s |hello hello runbook 名稱。 |
| Caller_s |誰 hello 作業。  可能的值為電子郵件地址或排程作業的系統。 |
| StreamType_s |hello 工作資料流類型。 可能的值包括：<br>-Progress (進度)<br>- Output (輸出)<br>- Warning (警告)<br>- Error (錯誤)<br>- Debug (偵錯)<br>- Verbose |
| Tenant_g | 識別 hello 呼叫端的 hello 租用戶的 GUID。 |
| JobId_g |為 hello 識別碼 hello runbook 工作的 GUID。 |
| ResultType |hello hello runbook 工作的狀態。  可能的值包括：<br>- In Progress |
| 類別 | Hello 的資料類型的分類。  自動化，hello 值為 JobStreams。 |
| OperationName | 指定在 Azure 中執行作業的 hello 型別。  自動化，hello 值會是工作。 |
| 資源 | Hello 自動化帳戶的名稱 |
| SourceSystem | 記錄分析收集 hello 資料的方式。 針對 Azure 診斷，一律為 Azure 。 |
| ResultDescription |包含從 hello runbook hello 輸出資料流。 |
| CorrelationId |為 hello 相互關聯識別碼 hello runbook 工作的 GUID。 |
| ResourceId |指定 hello runbook hello Azure 自動化帳戶資源的 id。 |
| SubscriptionId | hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。 |
| ResourceGroup | Hello 自動化帳戶 hello 資源群組名稱。 |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>在 Log Analytics 中檢視自動化記錄檔
既然您已經啟動傳送您的自動化作業記錄檔 tooLog 分析，我們來看看您可以使用達成這些記錄檔中記錄分析。

toosee hello 記錄檔，執行下列查詢的 hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>在 Runbook 工作失敗或暫停時傳送電子郵件
其中一個最上層客戶要求，是 hello 能力 toosend 電子郵件或文字時出錯 runbook 工作。   

toocreate 警示規則時，它會先建立 hello runbook 的記錄搜尋叫用 hello 警示的工作記錄。  按一下 hello**警示**按鈕 toocreate 及設定 hello 警示規則。

1. 從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。
2. 輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`您也可以依分組 hello RunbookName 使用：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   如果您已將設定從多個自動化帳戶或訂用帳戶 tooyour 工作區的記錄檔，您可以群組您的訂用帳戶和自動化帳戶的警示。  自動化帳戶名稱可以衍生自 JobLogs hello 搜尋中的 hello 資源欄位。  
3. tooopen hello**加入警示規則**畫面上，按一下**警示**hello 頁面頂端的 hello。 如需 hello 選項 tooconfigure hello 警示的詳細資訊，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。

### <a name="find-all-jobs-that-have-completed-with-errors"></a>尋找所有已完成但發生錯誤的工作
此外 tooalerting 失敗，您可以找到當 runbook 作業有一個非終止錯誤。 PowerShell 會在這些情況下產生的錯誤資料流，但不是會造成工作 toosuspend hello 非終止錯誤或失敗。    

1. 在 Log Analytics 工作區中，按一下 [記錄搜尋]。
2. 在 hello 查詢欄位中，輸入`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g`，然後按一下**搜尋**。

### <a name="view-job-streams-for-a-job"></a>檢視工作的工作資料流
當您偵錯工作時，您也可以 toolook hello 工作資料流。  hello 下列查詢顯示具有 GUID 2ebd22ea-e05e-4eb9-9 d 76 d73cbd4356e0 的單一作業的所有 hello 資料流：   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>檢視歷史工作狀態
最後，您可能想 toovisualize 作業記錄一段時間。  您可以使用這個查詢 toosearch hello 狀態為您的作業，一段時間。

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![OMS 歷史工作狀態圖表](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>摘要
藉由傳送您自動化工作的狀態和資料流資料 tooLog 分析，您可以取得更深入的自動化工作的 hello 狀態：
+ 設定警示 toonotify 您發生問題時
+ 使用自訂檢視和搜尋查詢 toovisualize 您 runbook 結果、 runbook 工作狀態、 和其他相關的主要指標或度量。  

記錄分析會提供操作可見度 tooyour 自動化工作，並可協助更快速地址事件。  

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解 tooconstruct 不同的搜尋查詢和檢閱 hello 自動化作業記錄檔記錄分析，請參閱[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)
* 如何 toocreate 並擷取輸出和錯誤訊息從 runbook，請參閱的 toounderstand [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)
* 深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)
* toolearn 深入了解 OMS 記錄分析和資料集合來源，請參閱[收集 Azure 儲存體中的資料記錄分析概觀](../log-analytics/log-analytics-azure-storage.md)
