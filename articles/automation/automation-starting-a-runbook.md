---
title: "Azure 自動化中 runbook aaaStarting |Microsoft 文件"
description: "摘要說明 hello 不同的方法是使用的 toostart Azure 自動化中的 runbook，且提供詳細資料上使用這兩個 hello Azure 入口網站和 Windows PowerShell。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>在 Azure 自動化中啟動 Runbook
下表中的 hello 可協助您判斷 hello 方法 toostart 中是最適合 tooyour 特定案例的 Azure 自動化 runbook。 本文包含在 hello Azure 入口網站與 Windows PowerShell 啟動 runbook 的詳細資料。 詳細資料 hello 上您可以從下列 hello 連結存取其他文件中提供其他方法。

| **方法** | **特性** |
| --- | --- |
| [Azure 入口網站](#starting-a-runbook-with-the-azure-portal) |<li>互動式使用者介面的最簡單方法。<br> <li>表單 tooprovide 簡單的參數值。<br> <li>輕鬆追蹤工作狀態。<br> <li>使用 Azure 登入資訊驗證存取。 |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>使用 Windows PowerShell Cmdlet 從命令列呼叫。<br> <li>可以包含在具有多個步驟的自動化解決方案中。<br> <li>使用憑證或 OAuth 使用者主體/服務主體來驗證要求。<br> <li>提供簡單和複雜的參數值。<br> <li>追蹤工作狀態。<br> <li>用戶端需要 toosupport PowerShell cmdlet。 |
| [Azure 自動化 API](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>最有彈性的方法，但也最複雜。<br> <li>從任何可提出 HTTP 要求的自訂程式碼呼叫。<br> <li>使用憑證或 OAuth 使用者主體/服務主體來驗證要求。<br> <li>提供簡單和複雜的參數值。<br> <li>追蹤工作狀態。 |
| [Webhook](automation-webhooks.md) |<li>從單一 HTTP 要求啟動 Runbook。<br> <li>在 URL 中使用安全性權杖進行驗證。<br> <li>用戶端無法覆寫建立 Webhook 時指定的參數值。 Runbook 可以定義單一參數，其中會填入 hello HTTP 要求詳細資料。<br> <li>透過 webhook URL 沒有能力 tootrack 工作狀態。 |
| [回應 tooAzure 警示](../log-analytics/log-analytics-alerts.md) |<li>回應 tooAzure 警示中啟動 runbook。<br> <li>設定 webhook runbook，並將連結 tooalert。<br> <li>在 URL 中使用安全性權杖進行驗證。 |
| [排程](automation-schedules.md) |<li>每小時、每天、每週或每月排程，自動啟動 Runbook。<br> <li>透過 Azure 入口網站、PowerShell Cmdlet 或 Azure API 操縱排程。<br> <li>提供參數值 toobe 排程搭配使用。 |
| [另一個 Runbook](automation-child-runbooks.md) |<li>在另一個 Runbook 中使用 Runbook 作為活動。<br> <li>對多個 Runbook 使用的功能很有用。<br> <li>提供參數值 toochild runbook，然後在父 runbook 使用輸出。 |

hello 圖顯示詳細的逐步程序中的 runbook hello 生命週期。 它包含不同的方式在 Azure 自動化中啟動 runbook Hybrid Runbook Worker tooexecute Azure 自動化 runbook 和不同元件之間的互動所需的元件。 有關在您的資料中心中執行自動化 runbook toolearn 參照太[hybrid runbook worker](automation-hybrid-runbook-worker.md)

![Runbook 架構](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>啟動 runbook 以 hello Azure 入口網站
1. 在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。
2. 在 hello 中樞功能表中，選取  **Runbook**。
3. 在 hello **Runbook**刀鋒視窗中，選取 runbook，然後按一下**啟動**。
4. 如果 hello runbook 有參數，您將會提示的 tooprovide 文字方塊中的每個參數的值。 請參閱以下的 [Runbook 參數](#Runbook-parameters) ，以取得參數的進一步詳細資訊。
5. 在 hello**作業**刀鋒視窗中，您可以檢視 hello hello runbook 工作的狀態。

## <a name="starting-a-runbook-with-windows-powershell"></a>使用 Windows PowerShell 啟動 Runbook
您可以使用 hello[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart 使用 Windows PowerShell runbook。 hello 下列範例程式碼會啟動呼叫測試 Runbook 的 runbook。

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

開始 AzureRmAutomationRunbook 傳回工作物件，您可以使用 tootrack 其狀態 hello runbook 啟動之後。 然後，您可以使用此作業物件搭配[Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello hello 工作狀態和[Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget 其輸出。 下列範例程式碼的 hello 啟動名的測試 Runbook，等待它完成，並接著會顯示其輸出。

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

如果 hello runbook 需要參數，則您必須提供其作為[雜湊表](http://technet.microsoft.com/library/hh847780.aspx)hello hello 雜湊表索引鍵符合 hello 參數名稱和 hello 值的位置是 hello 參數值。 hello 下列範例顯示如何 toostart 具有兩個字串參數的 runbook 名為 FirstName 和 LastName、 名為 RepeatCount 的整數和名為 Show 的布林參數。 如需有關參數的詳細資訊，請參閱以下的 [Runbook 參數](#Runbook-parameters) 。

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Runbook 參數
當您從 hello Azure 入口網站或 Windows PowerShell 啟動 runbook 時，會透過 hello Azure 自動化 web 服務傳送 hello 指示。 此服務不支援具有複雜資料型別的參數。 如果您需要 tooprovide 值為複雜參數，則您必須呼叫它內嵌從另一個 runbook 中所述[Azure 自動化中的子系 runbook](automation-child-runbooks.md)。

hello Azure 自動化 web 服務會提供特殊功能，如 hello 下列各節中所述，使用特定資料類型的參數。

### <a name="named-values"></a>具名值
如果 hello 參數的資料類型 [object]，然後您可以使用下列 JSON 格式 toosend 其一份名稱為值的 hello: *{Name1: 'Value1'，Name2: 'Value2'，Name3: 'Value3'}*。 這些值必須是簡單型別。 hello runbook 將會收到 hello 參數做為[PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx)有屬性對應 tooeach 名稱為 value。

請考慮下列接受參數，呼叫使用者的測試 runbook 的 hello。

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

hello 下列文字無法用於 hello user 參數。

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

這會導致 hello 遵循輸出。

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>陣列
如果 hello 參數是陣列，例如 [array] 或 [string []]，，然後您可以使用 hello 下列 JSON 格式 toosend 它的值清單： *[Value1，Value2，Value3]*。 這些值必須是簡單型別。

請考慮下列接受參數的測試 runbook 的 hello*使用者*。

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

hello 下列文字無法用於 hello user 參數。

```
["Joe","Smith",2,true]
```

這會導致 hello 遵循輸出。

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>認證
如果 hello 參數的資料類型**PSCredential**，您就可以提供的 Azure 自動化的 hello 名稱[認證資產](automation-credentials.md)。 hello runbook 將會抓取具有您指定的 hello 名稱 hello 認證。

請考慮下列接受認證參數的測試 runbook 的 hello。

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

hello 下列文字可用於假設有認證資產的 hello 使用者參數*My Credential*。

```
My Credential
```

假設在 hello 認證中的 hello username *jsmith*，這會產生下列輸出的 hello。

```
jsmith
```

## <a name="next-steps"></a>後續步驟
* 目前的文件中的 hello runbook 架構會提供在 Azure 和內部部署與 hello 混合式 Runbook 背景工作中的 runbook 管理資源的高階概觀。  有關在您的資料中心中執行自動化 runbook toolearn 參照太[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)。
* 深入了解建立其他 runbook 所使用的特定或一般函式的模組化 runbook toobe hello toolearn 參照太[子系 Runbook](automation-child-runbooks.md)。

