---
title: "管理 Azure 自動化 DSC aaaOnboarding 機器 |Microsoft 文件"
description: "Toosetup 以使用 Azure 自動化 DSC 進行管理的電腦"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>上架由 Azure 自動化 DSC 管理的機器

## <a name="why-manage-machines-with-azure-automation-dsc"></a>為什麼要使用 Azure 自動化 DSC 管理機器？

如同 [PowerShell 期望的狀態設定](https://technet.microsoft.com/library/dn249912.aspx)，Azure 自動化期望的狀態設定在任何雲端或內部部署資料中心中是 DSC 節點 (實體和虛擬機器) 的一個簡單但強大的組態管理服務。 它可讓您從中央、安全的位置快速且輕鬆地延展性到數千部電腦。 您可以輕鬆地登入機器，它們的宣告式組態，並檢視報表，顯示每個電腦的指派的相容性 toohello 預期的狀態，您所指定。 hello Azure Automation DSC 管理層是 tooDSC hello Azure 自動化的管理圖層 tooPowerShell 指令碼。 換句話說，在 hello Azure 自動化可協助您的相同方式來管理 PowerShell 指令碼，也可協助您管理 DSC 設定。 請參閱深入了解使用 Azure 自動化 DSC，hello 優勢 toolearn [Azure Automation DSC 概觀](automation-dsc-overview.md)。

Azure 自動化 DSC 可以用的 toomanage 各種不同的機器：

* Azure 虛擬機器 (傳統)
* Azure 虛擬機器
* Amazon Web Services (AWS) 虛擬機器
* 位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦
* 位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器

此外，如果您不是從 hello 雲端準備 toomanage 機器組態，Azure 自動化 DSC 也可用做為報表專用端點。 這可讓您透過 DSC 內部 tooset (push) 所需的設定，而檢視豐富報表的詳細資料節點的相容性以 hello Azure 自動化中的狀態。

hello 下列各節簡述如何將產品上架機器 tooAzure Automation DSC 的每個型別。

## <a name="azure-virtual-machines-classic"></a>Azure 虛擬機器 (傳統)

向 Azure 自動化 DSC，您可以輕鬆地登入 Azure 虛擬機器 （傳統） 組態管理使用 hello Azure 入口網站或 PowerShell。 Hello 幕後並沒有需要 tooremote hello VM 到系統管理員，hello Azure VM Desired State Configuration 延伸模組會使用 Azure 自動化 DSC 註冊 hello VM。 Hello Azure VM Desired State Configuration 延伸模組以非同步方式執行步驟 tootrack 其進度，或疑難排解因為它提供在 hello [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding)下一節。

### <a name="azure-portal"></a>Azure 入口網站

在 hello [Azure 入口網站](http://portal.azure.com/)，按一下 **瀏覽** -> **虛擬機器 （傳統）**。 選取您想要 tooonboard Windows VM hello。 Hello 虛擬機器的儀表板] 刀鋒視窗中，按一下 [**所有設定** -> **延伸** -> **新增** ->  **Azure 自動化 DSC** -> **建立**。 輸入 hello [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)使用案例，您的自動化帳戶登錄機碼和登錄的 URL，並選擇性節點組態 tooassign toohello VM 所需。

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

toofind hello 註冊 URL 和 hello 自動化帳戶 tooonboard hello 機器金鑰，請參閱 hello [**安全註冊**](#secure-registration)下一節。

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Azure 虛擬機器

Azure 自動化 DSC 可讓您輕鬆地登入 Azure 虛擬機器組態管理使用 hello Azure 入口網站、 Azure Resource Manager 範本或 PowerShell。 Hello 幕後並沒有需要 tooremote hello VM 到系統管理員，hello Azure VM Desired State Configuration 延伸模組會使用 Azure 自動化 DSC 註冊 hello VM。 Hello Azure VM Desired State Configuration 延伸模組以非同步方式執行步驟 tootrack 其進度，或疑難排解因為它提供在 hello [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding)下一節。

### <a name="azure-portal"></a>Azure 入口網站

在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello 想 tooonboard 虛擬機器的 Azure 自動化帳戶。 在 hello 自動化帳戶儀表板，按一下  **DSC 節點** -> **新增 Azure VM**。

在下**選取虛擬機器 tooonboard**、 選取一或多個 Azure 虛擬機器 tooonboard。

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

在下**設定註冊資料**，輸入 hello [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)所需的使用案例中，並選擇性節點組態 tooassign toohello VM。

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本

您可以部署 azure 虛擬機器和 onboarded tooAzure Automation DSC 透過 Azure Resource Manager 範本。 請參閱[設定透過 DSC 延伸模組的 VM 和 Azure 自動化 DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/)範例範本該 onboards 現有的 VM tooAzure Automation DSC。 toofind hello 登錄機碼及註冊 URL 採取做為此範本中的輸入，請參閱 hello [**安全註冊**](#secure-registration)下一節。

### <a name="powershell"></a>PowerShell

hello[暫存器 AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode)指令程式可以使用的 tooonboard hello 透過 PowerShell 的 Azure 入口網站中的虛擬機器。

## <a name="amazon-web-services-aws-virtual-machines"></a>Amazon Web Services (AWS) 虛擬機器

您可以輕鬆加入 Amazon Web Services 虛擬機器組態管理 Azure 自動化 dsc 使用 hello AWS DSC 工具組。 您可以進一步了解 hello toolkit[這裡](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/)。

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦

在內部部署的 Windows 電腦以及 Windows （例如 Amazon Web Services) 的非 Azure 雲端中也可以是 onboarded tooAzure 自動化 DSC，只要有 toohello 對外存取網際網路，透過一些簡單的步驟：

1. 請確定 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝想 tooonboard tooAzure Automation DSC 在 hello 機器上。
2. 一節中的 hello 遵循[**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations)下方 toogenerate 需要一個資料夾包含 hello DSC 中繼設定。
3. 從遠端適用於您想 tooonboard hello PowerShell DSC 中繼設定 toohello 機器。 **此命令會從執行的 hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. 如果您無法從遠端套用 hello PowerShell DSC 中繼設定，請將 hello 中繼設定資料夾複製到每個機器 tooonboard 步驟 2 中。 然後呼叫**Set-dsclocalconfigurationmanager**在本機上每個機器 tooonboard。
5. 使用 hello Azure 入口網站或 cmdlet，您的 Azure 自動化帳戶中註冊的 hello 機器 tooonboard 現在顯示為 DSC 節點的核取。

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器

在內部部署 Linux 機器，Linux 機器，在 Azure 中，而且非 Azure 雲端中的 Linux 機器也可能 onboarded tooAzure 自動化 DSC，只要有 toohello 對外存取網際網路，透過一些簡單的步驟：

1. 請確定 hello 最新版本的[Linux 的 PowerShell 預期狀態設定](https://github.com/Microsoft/PowerShell-DSC-for-Linux)安裝想 tooonboard tooAzure Automation DSC 在 hello 機器上。
2. 如果 hello [PowerShell DSC 本機設定管理員的預設值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)符合您的使用案例，而且您想 tooonboard 機器例如它們**兩者**從提取和報告 tooAzure 自動化 DSC:

   + 在每個 Linux 機器 tooonboard tooAzure 自動化 DSC，使用 Register.py tooonboard 使用的 hello PowerShell DSC 本機設定管理員的預設值：

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello 登錄機碼及註冊 URL 為您的自動化帳戶，請參閱 hello [**安全註冊**](#secure-registration)下一節。

     如果 hello PowerShell DSC 本機設定管理員預設**不要****不**符合您的使用案例，或者您想 tooonboard 機器，它們只會報告 tooAzure 自動化 DSC，但不要提取設定或 PowerShell 模組，請遵循步驟 3 到 6。 否則，請繼續直接 toostep 6。

3. 依照指示進行 hello hello [**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations) toogenerate 下方區段包含所需的 hello DSC 中繼設定的資料夾。
4. 從遠端適用於您想 tooonboard hello PowerShell DSC 中繼設定 toohello 機器：

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

此命令會從執行的 hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝。

1. 如果您無法將 hello PowerShell DSC 中繼設定套用的每個 Linux 機器 tooonboard 的遠端電腦上，複製到 hello Linux 機器上的步驟 5 中的 hello 資料夾 hello 中繼設定對應 toothat 機器。 然後呼叫`SetDscLocalConfigurationManager.py`本機每部 Linux 機器上您想 tooonboard tooAzure 自動化 DSC:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. 使用 hello Azure 入口網站或 cmdlet，您的 Azure 自動化帳戶中註冊的 hello 機器 tooonboard 現在顯示為 DSC 節點的核取。

## <a name="generating-dsc-metaconfigurations"></a>產生 DSC 中繼設定

toogenerically 任何機器 tooAzure Automation DSC 的上架[DSC 中繼設定](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig)可以產生的當套用，告知 hello DSC 代理程式上從 hello 機器 toopull 及/或報告 tooAzure Automation DSC。 可以使用 PowerShell DSC 設定或 hello Azure 自動化的 PowerShell 指令程式會產生 Azure 自動化 DSC 的 DSC 中繼設定。

> [!NOTE]
> DSC 中繼設定會包含 hello 所需的秘密 tooonboard 機器 tooan 管理的自動化帳戶。 請確定 tooproperly 保護您建立時，任何 DSC 中繼設定，或在使用後刪除它們。

### <a name="using-a-dsc-configuration"></a>使用 DSC 設定

1. 開啟 hello 身為系統管理員的 PowerShell ISE 中的本機環境中的機器。 hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝。
2. 複製下列指令碼在本機的 hello。 此指令碼包含 PowerShell DSC 設定用於建立中繼設定和命令 tookick hello 中繼設定建立功能。

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. 為您的自動化帳戶，以及 hello 機器 tooonboard hello 名稱填入 hello 註冊金鑰和 URL。 所有其他參數都是選擇性的。 toofind hello 登錄機碼及註冊 URL 為您的自動化帳戶，請參閱 hello [**安全註冊**](#secure-registration)下一節。
4. 如果您想 hello 機器 tooreport DSC 狀態資訊 tooAzure 自動化 DSC，但不是會提取組態或 PowerShell 模組，設定 hello **ReportOnly**參數 tootrue。
5. 執行 hello 指令碼。 您現在應該會有一個名為資料夾**DscMetaConfigs**在您的工作目錄中包含的 hello 機器 tooonboard （以系統管理員身分） hello PowerShell DSC 中繼設定：

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>使用 hello Azure 自動化 cmdlet

如果 hello PowerShell DSC 本機設定管理員的預設值符合您的使用案例，而且希望 tooonboard 機器同時從提取，並且報告 tooAzure 自動化 DSC，hello Azure 自動化 cmdlet 提供簡化的方法，來產生 hello DSC所需的中繼設定：

1. Hello PowerShell 主控台或 PowerShell ISE 中系統管理員身分在中開啟您的本機環境中的機器。
2. TooAzure 資源管理員使用連接**新增 AzureRmAccount**
3. 您想要從 hello 自動化 tooonboard hello 機器帳戶 toowhich 想 tooonboard 節點，請下載 hello PowerShell DSC 中繼設定：

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. 您現在應該會有一個名為資料夾***DscMetaConfigs***，包含 hello PowerShell DSC 中繼設定，如 hello 機器 tooonboard （以系統管理員身分）：
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>安全註冊

電腦可以安全地登入 tooan 透過 hello WMF 5 DSC 註冊通訊協定，可讓 DSC 節點 tooauthenticate tooa PowerShell DSC V2 提取或報表伺服器 （包括 Azure Automation DSC） 的 Azure 自動化帳戶。 hello 節點註冊 toohello 伺服器**登錄 URL**、 驗證使用**登錄機碼**。 在註冊期間，hello DSC 節點和 DSC 提取/報表伺服器會交涉驗證 toohello 伺服器後註冊此節點 toouse 的唯一憑證。 此程序可避免上架的節點彼此模擬，例如當節點遭到入侵並且具有惡意行為。 註冊後，hello 登錄機碼不會用於驗證一次，並會刪除從 hello 節點。

您可以取得 hello 資訊所需的 hello DSC 註冊通訊協定從 hello**管理金鑰**hello Azure preview 入口網站中的刀鋒視窗。 Hello hello 上的索引鍵圖示，即可開啟此刀鋒視窗**Essentials** hello 自動化帳戶的面板。

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* 註冊 URL 是 hello 管理金鑰 刀鋒視窗中的 hello URL 欄位。
* 登錄機碼是在 hello 管理金鑰 刀鋒視窗的 hello 主要存取金鑰或次要存取金鑰。 可以使用這兩個金鑰。

為了提高安全性，hello 的自動化帳戶的主要和次要存取金鑰會重新產生在任何時間 (上 hello**管理金鑰**刀鋒視窗) tooprevent 未來的節點註冊使用前一個索引鍵。

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>疑難排解 Azure 虛擬機器上架

Azure Automation DSC 可讓您輕鬆地將 Azure Windows VM 上架以進行組態管理。 Hello 幕後 hello Azure VM Desired State Configuration 延伸模組會為使用的 tooregister hello 向 Azure 自動化 DSC VM。 Hello Azure VM Desired State Configuration 延伸模組會以非同步方式執行，因為追蹤進度及疑難排解其執行可能很重要。

> [!NOTE]
> 上架 Azure Windows VM tooAzure Automation DSC 使用 hello Azure VM Desired State Configuration 延伸模組可能需要向上 hello 節點 tooshow tooan 小時註冊 Azure 自動化中的任何方法。 這是因為 Windows Management Framework 5.0 上 hello VM hello Azure VM DSC 延伸模組，這是必要的 tooonboard hello VM tooAzure Automation DSC toohello 安裝。

hello hello Azure 入口網站中的 Azure VM Desired State Configuration 延伸模組或檢視表 tootroubleshoot hello 狀態瀏覽 toohello 進行入門訓練的 VM，然後按一下-> **所有設定** -> **擴充功能**  ->  **DSC**。 如需詳細資訊，您可以按一下 [檢視詳細狀態] 。

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>憑證到期日和重新註冊

註冊 Azure Automation DSC 的 DSC 節點的電腦之後, 有一些情況下您可能必須 tooreregister hello 中的該節點未來：

* 在註冊之後，每個節點會自動交涉唯一的驗證憑證，該憑證於一年之後到期。 目前，當它們即將到期，所以您一年的時間之後需要 tooreregister hello 節點 hello PowerShell DSC 註冊通訊協定無法自動更新憑證。 在重新登錄之前，請確定每個節點都正在執行 Windows Management Framework 5.0 RTM。 如果節點的驗證憑證過期，而且 hello 節點未重新註冊，hello 節點將無法與 Azure 自動化 toocommunicate，且將標示為 '無回應。' 更新間隔執行 90 天，或小於 hello 憑證到期時間，或在任何時間點 hello 憑證到期時間之後, 將會導致正在產生和使用新的憑證。
* toochange 任何[PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)hello 節點，例如 ConfigurationMode 初始註冊期間設定的。 目前，這些 DSC 代理程式值只可以透過重新註冊變更。 hello 有一個例外狀況為 hello 分派 toohello 節點的節點組態--這可以在 Azure Automation DSC 直接變更。

可以在 hello 本文描述您註冊 hello 節點一開始，使用任何 hello 入門訓練方法的相同方式執行登錄。 您不需要 toounregister 從 Azure Automation DSC 的節點然後再重新登錄它。

## <a name="related-articles"></a>相關文章

* [Azure 自動化 DSC 概觀](automation-dsc-overview.md)
* [Azure 自動化 DSC Cmdlet](/powershell/module/azurerm.automation/#automation)
* [Azure 自動化 DSC 價格](https://azure.microsoft.com/pricing/details/automation/)
