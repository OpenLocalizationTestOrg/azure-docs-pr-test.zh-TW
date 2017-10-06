---
title: "在 Azure 自動化中的 aaaCredential 資產 |Microsoft 文件"
description: "在 Azure 自動化認證資產包含可能是使用的 tooauthenticate tooresources hello runbook 或 DSC 設定存取的安全性認證。 本文說明 toocreate 認證資產的方式，並將其用於 runbook 或 DSC 設定。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Azure 自動化中的認證資產
自動化認證資產會保存 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件，其中包含安全性認證，例如使用者名稱和密碼。 Runbook，而且當 DSC 組態可能使用指令程式可接受 PSCredential 物件，進行驗證，或它們可能會擷取 hello 使用者名稱和密碼的 hello PSCredential 物件 tooprovide toosome 應用程式或服務需要驗證。 認證的 hello 屬性會安全地儲存在 Azure 自動化中，而且可以存取在 hello runbook 或以 hello 的 DSC 組態中[Get-automationpscredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx)活動。

> [!NOTE]
> Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。 這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。 這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。 之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。  

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell Cmdlet
hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化認證資產。  這些 cmdlet 隨附 hello [Azure PowerShell 模組](/powershell/azure/overview)可用於自動化 runbook 和 DSC 設定。

| Cmdlet | 說明 |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |擷取認證資產的相關資訊。 您只能擷取 hello 認證本身從**Get-automationpscredential**活動。 |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |建立新的自動化認證。 |
| [Remove-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |移除自動化認證。 |
| [Set-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |設定 hello 現有自動化認證的屬性。 |

## <a name="runbook-activities"></a>Runbook 活動
hello 下表中的 hello 活動是 runbook 和 DSC 設定中的使用的 tooaccess 認證。

| 活動 | 說明 |
|:--- |:--- |
| Get-AutomationPSCredential |取得認證 toouse runbook 或 DSC 設定中。 傳回 [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件。 |

> [!NOTE]
> 您應該避免使用中的變數 hello – Name 參數 Get-automationpscredential 因為這可以使得探索 runbook 或 DSC 設定之間的相依性，並在設計階段認證資產。
> 
> 

## <a name="creating-a-new-credential-asset"></a>建立新的認證資產

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate hello Azure 入口網站使用新的認證資產
1. 從您的自動化帳戶，按一下 hello**資產**一部分 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**認證**一部分 tooopen hello**認證**刀鋒視窗。
3. 按一下**新增認證**在 hello hello 刀鋒視窗最上方。
4. 完成 hello 表單，然後按一下**建立**toosave hello 新的認證。

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate 使用 Windows PowerShell 的新認證資產
hello 下列命令範例示範如何 toocreate 新的自動化認證。 PSCredential 物件最初建立 hello 名稱和密碼，而且會用 toocreate hello 認證資產。 或者，您可以使用 hello **Get-credential** cmdlet toobe 提示 tootype 名稱和密碼。

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate hello Azure 傳統入口網站使用新的認證資產
1. 從您的自動化帳戶，按一下 **資產**hello hello 視窗上方。
2. 在 hello hello 視窗底部，按一下 **加入設定**。
3. 按一下 [ **加入認證**]。
4. 在 hello**認證類型**下拉式清單中，選取**PowerShell 認證**。
5. 完成 hello 精靈，然後按一下 [hello] 核取方塊 toosave hello 新認證。

## <a name="using-a-powershell-credential"></a>使用 PowerShell 認證
擷取 runbook 或 hello DSC 組態中的認證資產**Get-automationpscredential**活動。 這會傳回 [PSCredential 物件](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) ，您可以對需要 PSCredential 參數的活動或 Cmdlet 搭配使用此物件。 您也可以個別擷取 hello 認證物件 toouse hello 屬性。 hello 物件 hello 使用者名稱和 hello 安全密碼的屬性，或是您可以使用 hello **GetNetworkCredential**方法 tooreturn [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx)會提供不安全的物件hello 密碼版本。

### <a name="textual-runbook-sample"></a>文字式 Runbook 範例
hello 下列命令範例示範 toouse PowerShell runbook 中的認證。 在此範例中，會擷取 hello 認證，其使用者名稱和密碼指派 toovariables。

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>圖形化 Runbook 範例
您將加入**Get-automationpscredential**活動 tooa 圖形化 runbook 以滑鼠右鍵按一下 hello hello 圖形化編輯器和選取的程式庫 窗格中的 hello 認證**新增 toocanvas**。

![新增認證 toocanvas](media/automation-credentials/credential-add-canvas.png)

hello 下列影像顯示在圖形化 runbook 中使用認證的範例。  在此情況下，它正在使用的 tooprovide 驗證 runbook tooAzure 資源中所述[驗證 Azure AD 使用者帳戶的 Runbook](automation-create-aduser-account.md)。  hello 第一個活動擷取 hello 認證具有存取 toohello Azure 訂用帳戶。  hello **Add-azureaccount**活動接著會使用此認證 tooprovide 驗證針對緊跟在後的任何活動。  因為 [Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 需要單一物件，因此推出了 **管線連結** 。  

![新增認證 toocanvas](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>在 DSC 中使用 PowerShell 認證
雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AutomationPSCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。 如需詳細資訊，請參閱 [編譯 Azure Automation DSC 中的設定](automation-dsc-compile.md#credential-assets)。

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解連結在圖形化撰寫，請參閱[中圖形化撰寫連結](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello 不同的驗證方法，使用自動化，請參閱[Azure 自動化的安全性](automation-security-overview.md)
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md) 

