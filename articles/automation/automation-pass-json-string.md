---
title: "aaaPass JSON 物件 tooan Azure 自動化 runbook |Microsoft 文件"
description: "如何 toopass 參數 tooa runbook 以 JSON 物件"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell, runbook, json, azure 自動化"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>傳遞 JSON 物件 tooan Azure 自動化 runbook

它可以是您想要在 JSON 檔案中的 toopass tooa runbook 的實用 toostore 資料。
例如，您可能會建立包含所有 hello 參數的 JSON 檔案想 toopass tooa runbook。
toodo，您有 tooconvert hello JSON tooa 字串，然後將傳遞其內容 toohello runbook 之前的轉換 hello 字串 tooa PowerShell 物件。

在此範例中，我們將建立 PowerShell 指令碼中呼叫[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart PowerShell runbook，傳遞 hello hello JSON toohello runbook 內容。
hello PowerShell runbook 啟動 Azure VM 中，從 hello 傳入的 JSON 取得 hello VM hello 參數。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要遵循的 hello:

* Azure 訂用帳戶。 如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。
* [自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。  此帳戶必須具有權限 toostart，停止 hello 虛擬機器。
* Azure 虛擬機器。 我們會停止並啟動這部電腦，因此它不該是生產 VM。
* 本機電腦上安裝的 Azure Powershell。 請參閱[安裝和設定 Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)如需有關資訊 tooget Azure PowerShell。

## <a name="create-hello-json-file"></a>建立 hello JSON 檔案

輸入 hello 下列測試在文字檔案，並將它儲存成`test.json`本機電腦上的某個地方。

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>建立 hello runbook

在 Azure 自動化中建立名為 "Test-Json" 的新 PowerShell Runbook。
如何 toocreate 新的 PowerShell runbook，請參閱的 toolearn[我的第一個 PowerShell runbook](automation-first-runbook-textual-powershell.md)。

tooaccept hello JSON 資料，hello runbook 必須採用物件作為輸入參數。

hello runbook 可以接著使用 hello hello JSON 中定義的屬性。

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 在您的自動化帳戶中儲存並發佈此 Runbook。

## <a name="call-hello-runbook-from-powershell"></a>從 PowerShell 呼叫 hello runbook

現在您可以使用 Azure PowerShell，從本機電腦呼叫 hello runbook。
執行下列 PowerShell 命令的 hello:

1. 登入 tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    您會提示的 tooenter 您的 Azure 認證。
1. 取得 hello hello JSON 檔案內容，並將它轉換 tooa 字串：
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`是 hello hello JSON 檔案的儲存位置的路徑。
1. 轉換字串內容 hello `$json` tooa PowerShell 物件：
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. 建立雜湊表 hello 參數`Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   請注意，您要設定的 hello 值`Parameters`toohello PowerShell 物件，其中包含 hello JSON 檔案中的 hello 值。 
1. 啟動 hello runbook
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

hello runbook 會使用 hello JSON 檔案 toostart VM hello 值。

## <a name="next-steps"></a>後續步驟

* 進一步了解使用文字編輯器，編輯 PowerShell 和 PowerShell 工作流程 runbook toolearn 看到[編輯 Azure 自動化中的文字 runbook](automation-edit-textual-runbook.md) 
* toolearn 深入了解建立和匯入 runbook，請參閱[建立或匯入在 Azure 自動化 runbook](automation-creating-importing-runbook.md)


