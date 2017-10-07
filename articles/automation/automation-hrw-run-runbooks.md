---
title: "在 Azure 自動化 Hybrid Runbook Worker aaaRun runbook |Microsoft 文件"
description: "本文章提供您的本機資料中心或雲端提供者與 hello 混合式 Runbook 背景工作角色中的電腦上執行 runbook 的相關資訊。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>在混合式 Runbook 背景工作角色上執行 Runbook 
沒有任何差異，在 Azure 自動化以及執行在混合式 Runbook 背景工作上執行之 runbook 的 hello 結構中。 您使用與每個 Runbook 最有可能大不相同但因為通常針對混合式 Runbook 背景工作的 runbook 管理資源本身的 hello 本機電腦上或針對 hello 本機環境中部署，在 runbook 中的資源在 Azure 自動化中通常管理 hello Azure 雲端中的資源。

您可以編輯 runbook 的 Hybrid Runbook Worker 在 Azure 自動化中，但如果可能會發生困難 tootest hello runbook hello 編輯器中的再試一次。  hello PowerShell 模組存取 hello 本機資源可能未安裝在您的 Azure 自動化環境中在此情況下，hello 測試將會失敗。  如果您安裝 hello 所需的模組，將 hello runbook 將會執行，但不是會完成的測試可以 tooaccess 本機資源。

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>在混合式 Runbook 背景工作角色上啟動 Runbook
[在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 描述啟動 Runbook 的不同方法。  加入 hybrid Runbook Worker **RunOn**選項，您可以在其中指定 hello 的混合式 Runbook 背景工作群組的名稱。  如果已指定群組，hello runbook 擷取，並執行該群組中的 hello 背景工作。  如果未指定此選項，則會正常在 Azure 自動化中執行。

當您啟動 runbook hello Azure 入口網站中時，您會有**上執行**選項，您可以在其中選取**Azure**或**Hybrid Worker**。  如果您選取**Hybrid Worker**，接著，您可以從下拉式清單中選取 hello 群組。

使用 hello **RunOn**參數。  您可以使用下列命令 toostart 名為一個名為 MyHybridGroup 使用 Windows PowerShell 的混合式 Runbook 背景工作群組上的測試 Runbook 的 runbook hello。

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> hello **RunOn**參數已加入 toohello **Start-azureautomationrunbook** 0.9.1 版 Microsoft Azure PowerShell cmdlet。  您應該[下載最新版本的 hello](https://azure.microsoft.com/downloads/)如果您有安裝較早的一個。  您只需要 tooinstall 其中您從 Windows PowerShell 啟動 hello runbook 的工作站上這個版本。  您不需要 tooinstall 它 hello 背景工作電腦上除非您想要從該電腦 toostart runbook。  目前您無法從另一個 runbook Hybrid Runbook Worker 上啟動 runbook，因為這會需要安裝在您的自動化帳戶的 Azure Powershell toobe hello 最新版本。  hello 最新版本會自動更新 Azure 自動化中，而自動推出推 toohello 背景工作。
>
>

## <a name="runbook-permissions"></a>Runbook 權限
混合式 Runbook 背景工作執行的 Runbook 無法使用 hello 相同方法，通常用於 runbook 驗證 tooAzure 資源，因為它們存取 Azure 外部的資源。  hello runbook 可以提供自己的驗證 toolocal 資源，或您可以指定的 RunAs 帳戶 tooprovide 所有 runbook 的使用者內容。

### <a name="runbook-authentication"></a>Runbook 驗證
根據預設，runbook 將會執行 hello hello 在內部部署電腦上，hello 本機系統帳戶內容中，讓使用者必須提供自己驗證 tooresources 它們將會存取。  

您可以使用[認證](http://msdn.microsoft.com/library/dn940015.aspx)和[憑證](http://msdn.microsoft.com/library/dn940013.aspx)cmdlet 可讓您 toospecify 認證，您可以驗證 toodifferent 資源與您在 runbook 中的資產。  hello 下列範例顯示會重新啟動電腦的 runbook 的一部分。  它會從變數資產 hello 電腦的認證資產和 hello 名稱擷取認證，然後 hello Restart-computer cmdlet 會使用這些值。

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

您也可以利用[InlineScript](automation-powershell-workflow.md#inlinescript)，可讓您的程式碼 toorun 區塊另一部電腦上以 hello 所指定的認證[PSCredential 一般參數](http://technet.microsoft.com/library/jj129719.aspx)。

### <a name="runas-account"></a>RunAs 帳戶
您不需要提供自己的驗證 toolocal 資源的 runbook，您可以指定**RunAs** Hybrid worker 群組的帳戶。  您指定[認證資產](automation-credentials.md)存取 toolocal 資源，且這些認證 hello 群組中的混合式 Runbook 背景工作執行時執行的所有 runbook。  

hello hello 認證的使用者名稱必須是其中一種 hello 下列格式：

* 網域\使用者名稱
* username@domain
* 使用者名稱 （適用於帳戶本機 toohello 在內部部署電腦）

使用下列程序 toospecify Hybrid worker 群組的 RunAs 帳戶的 hello:

1. 建立[認證資產](automation-credentials.md)存取 toolocal 資源。
2. 開啟 hello 自動化帳戶中的 hello Azure 入口網站。
3. 選取 hello **Hybrid Worker 群組**磚，，然後選取 hello 群組。
4. 選取 [所有設定]，然後選取 [Hybrid 背景工作角色群組設定]。
5. 變更**執行身分**從**預設**太**自訂**。
6. 選取 hello 認證，並按一下**儲存**。

### <a name="automation-run-as-account"></a>自動化執行身分帳戶
在您的自動化的建置程序部署在 Azure 中的資源，您可能需要存取 tooon 內部部署系統 toosupport 工作或一組步驟在您的部署序列。  toosupport 使用 hello 執行身分帳戶的 Azure 驗證，您需要執行身分帳戶憑證 tooinstall hello。  

hello 遵循 PowerShell runbook*匯出 RunAsCertificateToHybridWorker*、 從 Azure 自動化帳戶匯出憑證執行身分的 hello 和下載並匯入至 hello 本機憑證存放區上混合式背景工作連接 toohello 相同的帳戶。  完成該步驟之後，它會確認 hello 背景工作可順利驗證 tooAzure 使用 hello 執行身分帳戶。

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

儲存 hello*匯出 RunAsCertificateToHybridWorker* runbook tooyour 電腦`.ps1`延伸模組。  匯入您的自動化帳戶，並編輯 hello runbook，請變更 hello hello 變數值`$Password`與您自己的密碼。  發行，然後執行 hello runbook 目標 hello Hybrid Worker 群組執行並以驗證使用 hello 執行身分帳戶的 runbook。  hello 工作資料流報表 hello 嘗試 tooimport hello 憑證 hello 本機電腦存放區，並根據您的訂用帳戶中定義多少的自動化帳戶和驗證是否成功的多個行如下所示。  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>在 Hybrid Runbook Worker 上進行 Runbook 疑難排解
記錄檔儲存每一個混合式背景工作角色本機的 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes 中。  混合式背景工作也會記錄錯誤和事件中 hello Windows 事件記錄檔中**應用程式和服務 Logs\Microsoft SMA\Operational**。  相關事件寫入 toorunbooks hello 背景工作上執行太**應用程式和服務 Logs\Microsoft Automation\Operational**。  hello **Microsoft SMA**記錄中包含許多多個事件相關的 toohello runbook 作業推入的 toohello 背景工作 」 與 「 hello 處理 hello runbook。  Hello 時**Microsoft 自動化**協助 hello 疑難排解的 runbook 執行的詳細資料與事件記錄檔沒有許多事件，您至少會發現 hello hello runbook 工作的結果。  

[Runbook 輸出和訊息](automation-runbook-output-and-messages.md)傳送的 tooAzure 自動化作業從混合式背景工作只想在 hello 雲端中執行的 runbook 工作。  您也可以啟用 hello 詳細資訊，並進行資料流 hello 相同的方式其他 runbook。  

如果您的 runbook 沒有成功完成，而且 hello 工作摘要顯示的狀態**Suspended**，請檢閱 hello 疑難排解文章[Hybrid Runbook Worker: runbook 工作終止狀態為暫止](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended)。   

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解 hello 不同的方法可以使用的 toostart runbook，請參閱[Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)。  
* toounderstand hello 不同的程序使用 PowerShell 和 PowerShell 工作流程 runbook 在 Azure 自動化中使用 hello 文字編輯器 中，請參閱[編輯 Azure 自動化中的 Runbook](automation-edit-textual-runbook.md)
