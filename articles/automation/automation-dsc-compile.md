---
title: "在 Azure Automation DSC aaaCompiling 組態 |Microsoft 文件"
description: "本文說明如何 toocompile 預期狀態設定 (DSC) 設定 Azure 自動化。"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>編譯 Azure 自動化 DSC 中的組態

您可以編譯為預期狀態設定 (DSC) 設定與 Azure 自動化有兩種： hello Azure 入口網站，並使用 Windows PowerShell。 hello 下列表格可協助您判斷何時 toouse 哪一種方法會根據每個 hello 特性：

### <a name="azure-portal"></a>Azure 入口網站

* 互動式使用者介面的最簡單方法
* 表單 tooprovide 簡單的參數值
* 輕鬆追蹤工作狀態
* 使用 Azure 登入資訊驗證存取

### <a name="windows-powershell"></a>Windows PowerShell

* 使用 Windows PowerShell Cmdlet 從命令列呼叫
* 可以包含在具有多個步驟的自動化解決方案中
* 提供簡單和複雜的參數值
* 追蹤工作狀態
* 所需的用戶端 toosupport PowerShell cmdlet
* 傳遞 ConfigurationData
* 編譯使用認證的組態

一旦您決定編譯方法上，您可以依照以下 toostart 編譯 hello 個別的程序。

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>編譯 DSC 設定以 hello Azure 入口網站

1. 從您的自動化帳戶中，按一下 [DSC 組態]。
2. 按一下 設定 tooopen 其刀鋒視窗。
3. 按一下 [編譯] 。
4. 如果 hello 設定沒有任何參數，則會提示的 tooconfirm 是否要將 toocompile 它。 如果 hello 組態有參數，hello**編譯組態**刀鋒視窗會開啟，以便您可以提供參數值。 請參閱 hello [**基本參數**](#basic-parameters)下面章節以取得參數的詳細資料。
5. hello**編譯工作**刀鋒視窗中開啟，讓您可以追蹤 hello 編譯作業的狀態，並 hello 節點組態 （MOF 設定文件） 則因為 toobe 置於 hello Azure Automation DSC 提取伺服器。

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>使用 Windows PowerShell 編譯 DSC 組態

您可以使用[ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart 編譯使用 Windows PowerShell。 下列範例程式碼的 hello 啟動編譯 DSC 設定，稱為**SampleConfig**。

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`傳回編譯作業，您可以使用 tootrack 其狀態的物件。 然後，您可以使用此編譯作業物件搭配[ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) hello 編譯工作，toodetermine hello 狀態和[ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview 其資料流 （輸出）。 下列範例程式碼的 hello 啟動的 hello 編譯**SampleConfig**組態中，等候直到它已完成，並接著會顯示其資料流。

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>基本參數
在 DSC 設定，包含參數型別和運作的內容中的參數宣告 hello 相同如同 Azure 自動化 runbook。 請參閱[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md) toolearn 深入了解 runbook 參數。

hello 下列範例會使用兩個參數呼叫**FeatureName**和**IsPresent**，toodetermine hello 中 hello 屬性值**ParametersExample.sample**節點設定中，在編譯期間產生。

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

您可以編譯 DSC 設定在 hello Azure Automation DSC 入口網站或 Azure PowerShell，使用基本參數：

### <a name="portal"></a>入口網站

在 hello 入口網站中，您可以輸入參數值之後按**編譯**。

![替代文字](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell 要求中的參數[雜湊表](http://technet.microsoft.com/library/hh847780.aspx)hello 索引鍵符合 hello 參數名稱，而 hello 值等於 hello 參數值。

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

如需如何將 PSCredentials 傳入作為參數的相關資訊，請參閱下方的 <a href="#credential-assets">**認證資產**</a> 。

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData**可讓您從任何環境的特定設定時使用的 PowerShell DSC tooseparate 結構化設定。 請參閱[「 什麼 」 隔開"Where"PowerShell dsc](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn 更多關於**ConfigurationData**。

> [!NOTE]
> 您可以使用**ConfigurationData**編譯中使用 Azure PowerShell 的 Azure 自動化 DSC，但不是在 hello Azure 入口網站時。

hello 下列範例 DSC 設定使用**ConfigurationData**透過 hello **$ConfigurationData**和**$AllNodes**關鍵字。 您還需要 hello [ **xWebAdministration**模組](https://www.powershellgallery.com/packages/xWebAdministration/)此範例中：

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

您可以編譯上述使用 PowerShell 的 hello DSC 設定。 hello PowerShell 底下加入兩個節點組態 toohello Azure Automation DSC 提取伺服器： **ConfigurationDataSample.MyVM1**和**ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Assets

資產的參考是 hello Azure 自動化 DSC 設定和 runbook 中相同。 Hello 下列如需詳細資訊，請參閱：

* [憑證](automation-certificates.md)
* [連線](automation-connections.md)
* [認證](automation-credentials.md)
* [變數](automation-variables.md)

### <a name="credential-assets"></a>認證資產

雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AzureRmAutomationCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。 如果組態使用的參數**PSCredential**類型，則您需要 Azure 自動化認證資產 toopass hello 字串名稱做為該參數的值，而不是 PSCredential 物件。 Hello 幕後 hello Azure 自動化認證資產具有該名稱將會擷取和傳遞 toohello 組態。

保留認證安全節點組態 （MOF 設定文件） 需要加密 hello 節點設定 MOF 檔案中的 hello 認證。 Azure 自動化會進一步採用此步驟，並且加密 hello 整個 MOF 檔案。 不過，目前必須告知 PowerShell DSC 沒有關係的節點設定 MOF 在產生期間，輸出以純文字認證 toobe 因為 PowerShell DSC 並不知道 Azure 自動化會加密後的 hello 整個 MOF 檔案及其產生透過編譯工作。

您可以告訴 PowerShell DSC 是否可以供輸出中產生的 hello 節點設定 Mof 內的純文字認證 toobe 使用[ **ConfigurationData**](#configurationdata)。 您應該傳遞`PSDscAllowPlainTextPassword = $true`透過**ConfigurationData** hello DSC 組態中會出現，並使用認證的每個節點區塊的名稱。

hello 下列範例顯示使用自動化認證資產的 DSC 設定。

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

您可以編譯上述使用 PowerShell 的 hello DSC 設定。 hello PowerShell 底下加入兩個節點組態 toohello Azure Automation DSC 提取伺服器： **CredentialSample.MyVM1**和**CredentialSample.MyVM2**。

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>匯入節點組態

您也可以匯入在 Azure 外部完成編譯的節點組態 (MOF)。 這樣做的優點之一就是可以簽署節點組態。
帶正負號的節點驗證的設定在本機上受管理的節點 hello DSC 代理程式，確保正在套用的 toohello 節點該 hello 組態來自授權來源。

> [!NOTE]
> 您可以將簽署的組態匯入到您的 Azure 自動化帳戶，但 Azure 自動化目前不支援編譯簽署的組態。

> [!NOTE]
> 節點組態檔必須是不能大於 1 MB tooallow 它 toobe 匯入到 Azure 自動化。

您可以了解如何在 https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module toosign 節點設定。

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>匯入 hello Azure 入口網站中的節點設定

1. 從您的自動化帳戶中，按一下 [DSC 節點組態]。

    ![DSC 節點組態](./media/automation-dsc-compile/node-config.png)
2. 在 hello **DSC 節點組態**刀鋒視窗中，按一下 **新增 NodeConfiguration**。
3. 在 hello**匯入**刀鋒視窗中，按一下 hello 資料夾圖示的 下一步 toohello**節點組態檔**節點組態檔 (MOF) 在本機電腦上的文字方塊中 toobrowse。

    ![瀏覽本機檔案](./media/automation-dsc-compile/import-browse.png)
4. 輸入的名稱在 hello**組態名稱**文字方塊。 此名稱必須符合 hello hello 組態從中編譯 hello 節點組態名稱。
5. 按一下 [確定] 。

### <a name="importing-a-node-configuration-with-powershell"></a>使用 PowerShell 匯入節點組態

您可以使用 hello[匯入 AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport 到您的自動化帳戶的節點設定。

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



