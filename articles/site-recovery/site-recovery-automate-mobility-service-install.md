---
title: "aaaDeploy hello 向 Azure 自動化 DSC 的站台復原行動服務 |Microsoft 文件"
description: "描述如何 toouse Azure Automation DSC tooautomatically 部署 hello Azure 站台復原行動服務和 Azure 代理程式適用於 VMware VM 和實體伺服器複寫 tooAzure"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>部署與 Azure Automation DSC 的 VM 複寫的 hello 行動服務
在 Operations Management Suite 中，我們提供您一個全方位的備份和災害復原解決方案，可供您融入到您的商務持續性計畫中。

我們使用「Hyper-V 複本」來與 Hyper-V 一起展開這個旅程。 但是，我們將展開的 toosupport 有異質的安裝程式，因為客戶在其雲端中有多個 hypervisor 和平台。

如果目前正在執行 VMware 的工作負載和 （或） 實體伺服器，管理伺服器執行所有 hello Azure Site Recovery 元件在您的環境 toohandle hello 通訊和資料複寫有了 Azure，Azure 時您的目的地。

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>使用 Automation DSC 部署 hello 站台復原行動服務
讓我們從快速分析此管理伺服器的作用著手︰

hello 管理伺服器會執行數個伺服器角色。 其中一個角色是「組態」 ，負責協調通訊及管理資料複寫與復原程序。

此外，hello*程序*角色做為複寫閘道。 這個角色接收複寫資料從受保護的來源機器、 最佳化與快取、 壓縮和加密，並再將它傳送 tooan Azure 儲存體帳戶。 其中一個 hello 處理角色的 hello 函式也 hello 行動服務 tooprotected 機器 toopush 安裝並執行的 VMware Vm 的自動探索。

如果沒有從 Azure 容錯回復，hello*主要目標*角色會處理 hello 複寫資料，這項作業的一部分。

對於受保護的 hello 機器我們依賴 hello*行動服務*。 此元件是已部署的 tooevery 機器 （VMware VM 或實體伺服器） 的 tooreplicate tooAzure。 它會擷取 hello 機器上的資料寫入，並將它們轉送 toohello management server （處理序角色）。

當您處理商務持續性時，很重要 toounderstand 牽涉到您的工作負載，您的基礎結構和 hello 元件。 您接著可以符合您的復原時間目標 (RTO) 和復原點目標 (RPO) 的 hello 需求。 在此情況下，hello 行動服務是金鑰 tooensuring 如您所預期，保護您的工作負載。

因此，您要如何在某些 Operations Management Suite 元件的協助下，以最佳化的方式確保您有可靠的受保護設定？

這篇文章提供範例將示範如何使用 Azure 自動化預期狀態設定 (DSC)，以及站台復原，tooensure 的：

* hello 行動服務和 Azure VM 代理程式是您想 tooprotect 部署的 toohello Windows 電腦。
* hello 複寫目標 Azure 時，一律會執行 hello 行動服務和 Azure VM 代理程式。

## <a name="prerequisites"></a>必要條件
* 儲存機制 toostore hello 必要設定
* 儲存機制 toostore hello 需要複雜密碼 tooregister 與 hello 管理伺服器

  > [!NOTE]
  > 系統會為每一部管理伺服器產生一個唯一的複雜密碼。 如果您正在 toodeploy 多部管理伺服器，您必須 tooensure 該 hello 正確複雜密碼儲存在 hello passphrase.txt 檔案。
  >
  >
* Windows Management Framework (WMF) 5.0 hello tooenable 需保護 （Automation dsc 的需求） 的電腦上安裝

  > [!NOTE]
  > 如果您想 toouse DSC 適用於 Windows 的電腦安裝 WMF 4.0，請參閱 hello 節[已中斷連線的環境中使用 DSC](## Use DSC in disconnected environments)。
  

hello 行動服務可透過 hello 命令列安裝，並接受數個引數。 這就是為什麼您需要 toohave hello 二進位檔 （解壓縮之後它們從您的安裝程式），並將其儲存在其中擷取這些使用 DSC 設定的地方。

## <a name="step-1-extract-binaries"></a>步驟 1：擷取二進位檔
1. 對於此設定，所需的 tooextract hello 檔案瀏覽 toohello 管理伺服器上下列目錄：

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    在此資料夾中，您應該會看到具有下列名稱的 MSI 檔案：

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    使用下列命令 tooextract hello installer hello:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. 選取 所有檔案，並將它們傳送 tooa 壓縮 (zipped) 資料夾。

您現在可以使用自動化 DSC，需要 tooautomate hello 安裝 hello 行動服務的 hello 二進位檔。

### <a name="passphrase"></a>複雜密碼
接下來，您需要的 toodetermine 想 tooplace 這個 zip 壓縮的資料夾。 您可以使用 Azure 儲存體帳戶，做為顯示更新的版本，toostore hello 複雜密碼所需的 hello 安裝程式。 hello 代理程式接著會向 hello 管理伺服器 hello 程序的一部分。

您已部署的 hello 管理伺服器時所得的 hello 複雜密碼可以儲存為 passphrase.txt tooa 文字檔案。

Hello zip 的資料夾和 hello 複雜密碼放置於容器 hello Azure 儲存體帳戶中的專用。

![資料夾位置](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

如果您偏好 tookeep 共用上的這些檔案在網路上，您可以這樣做。 您只需要 tooensure hello DSC 資源，稍後您將會使用有權存取，並可以取得 hello 安裝程式和複雜密碼。

## <a name="step-2-create-hello-dsc-configuration"></a>步驟 2： 建立 hello DSC 設定
hello 安裝 WMF 5.0 而定。 Hello 機器 toosuccessfully 適用於透過自動化 DSC hello 組態，WMF 5.0 toobe 存在。

hello 環境會使用下列範例 DSC 組態中的 hello:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
hello 組態將會執行下列 hello:

* hello 變數會告訴 hello 組態將 tooget hello 複雜密碼，而其中 toostore hello 輸出 tooget hello hello 行動服務與 hello Azure VM 代理程式，二進位檔的位置。
* hello 組態將會匯入 hello xPSDesiredStateConfiguration DSC 資源，好讓您可以使用`xRemoteFile`toodownload hello 檔案從 hello 儲存機制。
* hello 組態會建立您想要 toostore hello 二進位檔的目錄。
* hello 封存資源會從 hello 壓縮資料夾解壓縮 hello 檔案。
* hello 套件安裝資源將會從 hello UNIFIEDAGENT 安裝 hello 行動服務。EXE 安裝程式與 hello 特定引數。 （hello 建構 hello 引數的變數需要 tooreflect toobe 變更您的環境）。
* hello 套件 AzureAgent 資源將會安裝 hello Azure VM 代理程式，建議在 Azure 中執行每個 VM 上。 hello Azure VM 代理程式也可讓可能 tooadd 延伸 toohello VM 容錯移轉之後。
* hello 服務資源會確保 hello 相關的行動服務並 hello Azure 服務一律會持續執行。

儲存為 hello 設定**ASRMobilityService**。

> [!NOTE]
> 請記住 tooreplace hello CSIP 在您設定 tooreflect hello 實際管理伺服器中，以便 hello 代理程式將會正確地連接並將使用 hello 正確複雜密碼。
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>步驟 3： 上傳 tooAutomation DSC
因為您所做的 hello DSC 組態將會匯入必要的 DSC 資源模組 (xPSDesiredStateConfiguration)，您需要 tooimport 自動化中的該模組之前 hello DSC 組態上傳。

登入 tooyour 自動化帳戶中，瀏覽過**資產** > **模組**，然後按一下**瀏覽圖庫**。

您可以在這裡搜尋 hello 模組和 tooyour 帳戶匯入。

![匯入模組](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

當您完成此動作時，請移 tooyour 機器必須已安裝的 hello Azure 資源管理員模組，並繼續 tooimport hello 新建立的 DSC 設定。

### <a name="import-cmdlets"></a>匯入 Cmdlet
在 PowerShell 中，登入 tooyour Azure 訂用帳戶。 修改您的環境的 hello cmdlet tooreflect 和擷取您在變數中的自動化帳戶資訊：

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

使用下列 cmdlet 的 hello 傳 hello 設定 tooAutomation DSC:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Hello 設定自動化的 dsc 編譯
接著，您必須在自動化 DSC toocompile hello 組態，讓您可以啟動 tooregister 節點 tooit。 藉由執行下列 cmdlet 的 hello 達成此目標：

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

這可能需要幾分鐘的時間，因為基本上要部署的 hello 設定 toohello 裝載 DSC 提取服務。

編譯 hello 組態之後，您可以使用 PowerShell (Get AzureRmAutomationDscCompilationJob)，或使用 hello 擷取 hello 作業資訊[Azure 入口網站](https://portal.azure.com/)。

![擷取作業](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

您現在已成功發行並將上傳您的 DSC 組態 tooAutomation DSC。

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>步驟 4： 上架的機器 tooAutomation DSC
> [!NOTE]
> 完成此案例中的 hello 必要條件是 hello 最新版本的 WMF 會更新您的 Windows 電腦。 您可以下載並安裝您的平台從 hello hello 正確版本[下載中心](https://www.microsoft.com/download/details.aspx?id=50395)。
>
>

您即將建立 metaconfig dsc，所以要套用 tooyour 節點。 與這個 toosucceed，您需要 tooretrieve hello 端點 URL 和 hello 主索引鍵在 Azure 中您選取的自動化帳戶。 您可以找到這些值在**金鑰**上 hello**所有設定**刀鋒視窗中的 hello 自動化帳戶。

![金鑰值](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

在此範例中，您有 Windows Server 2012 R2 的實體伺服器，您想 tooprotect，使用站台復原。

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>檢查有任何暫止檔案重新命名作業 hello 登錄中
您開始 tooassociate hello 伺服器 hello Automation DSC 端點之前，我們建議您檢查有任何暫止檔案重新命名作業 hello 登錄中。 它們可能會禁止 hello 安裝程式完成到期 tooa 暫止的重新開機。

執行下列 cmdlet tooverify 是 hello 伺服器上沒有擱置的重新開機的 hello:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
如果這會顯示空白，您必須確定 tooproceed。 如果沒有，您應該解決此問題由 hello 伺服器重新啟動在維護期間。

tooapply hello 組態 hello 在伺服器上，啟動 hello PowerShell 整合式指令碼環境 (ISE)，並執行下列指令碼的 hello。 這是基本上 DSC 本機設定會指示以 hello Automation DSC 服務的 hello 本機設定管理員引擎 tooregister 並擷取 hello 特定組態 (ASRMobilityService.localhost)。

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

此設定會導致 hello 本機設定管理員本身引擎 tooregister 並且自動化 DSC。 它也會決定如何運作 hello 引擎應該時設定漂移 (ApplyAndAutoCorrect)，它應該執行的動作，應該如何進行 hello 組態是否需要重新開機。

執行這個指令碼之後，hello 節點開頭應該 tooregister Automation DSC。

![進行中的節點註冊](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

如果您往回 toohello Azure 入口網站，您可以看到該 hello 新註冊的節點現在已出現在 hello 入口網站。

![Hello 入口網站中已註冊的節點](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Hello 在伺服器上，您可以執行下列的 PowerShell 指令程式 tooverify hello 節點的正確登錄的 hello:

```powershell
Get-DscLocalConfigurationManager
```

Hello 設定已提取和套用 toohello 伺服器之後，您可以確認這藉由執行下列 cmdlet 的 hello:

```powershell
Get-DscConfigurationStatus
```

hello 輸出會顯示該 hello 伺服器已順利提取其組態：

![輸出](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

此外，hello 行動服務安裝程式已有它自己的記錄可以找到的*SystemDrive*\ProgramData\ASRSetupLogs。

就這麼簡單！ 您現在已成功部署並註冊您想 tooprotect，使用站台復原的 hello 電腦上的 hello 行動服務。 DSC 可確保一律執行所需的 hello 服務。

![部署成功](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Hello 管理伺服器偵測到 hello 成功部署之後，您可以設定保護，然後機器上啟用複寫 hello 使用站台復原。

## <a name="use-dsc-in-disconnected-environments"></a>在中斷連線的環境中使用 DSC
如果您的電腦無法連線的 toohello 網際網路，仍可以依賴 DSC toodeploy 及設定您想 tooprotect hello 工作負載的 hello 行動服務。

您可以在環境中執行個體化自己 DSC 提取伺服器 tooessentially 提供 hello 相同的功能，您會得到從 Automation DSC。 也就是說，hello 用戶端將會提取 hello 組態 （註冊） 後 toohello DSC 端點。 不過，另一個選項為 toomanually 發送 hello DSC 組態 tooyour 機器，在本機或遠端。

請注意，在此範例中，加入的參數 hello 電腦名稱。 必須能夠存取在遠端共用上的 tooprotect hello 機器現在位於 hello 遠端檔案。 hello hello 指令碼結尾制定 hello 組態，然後啟動 tooapply hello DSC 組態 toohello 目標電腦。

### <a name="prerequisites"></a>必要條件
請確定已安裝該 hello xPSDesiredStateConfiguration PowerShell 模組。 對於 Windows 電腦已安裝 WMF 5.0，您可以執行 hello hello 目標電腦上下列指令程式來安裝 hello xPSDesiredStateConfiguration 模組：

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

您也可以下載並儲存 hello 模組，以防您需要 toodistribute 它 tooWindows 機器安裝 WMF 4.0。 請在具有 PowerShellGet (WMF 5.0) 的機器上執行下列 Cmdlet︰

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

也 WMF 4.0，請確定該 hello [Windows 8.1 更新 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello 機器上安裝。

hello 下列組態可以推入安裝 WMF 5.0 和 WMF 4.0 的 tooWindows 電腦：

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

如果您想 tooinstantiate 自己 DSC 提取伺服器上，就可以從 Automation DSC 您公司網路 toomimic hello 的能力，請參閱[設定 DSC web 提取伺服器](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396)。

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>選擇性：使用 Azure Resource Manager 範本來部署 DSC 組態
本文著重在如何建立您自己的 DSC 組態 tooautomatically 部署 hello 行動服務與 hello Azure VM 代理程式-，以及確保它們執行 hello 機器上的 tooprotect。 我們也必須將部署此 DSC 組態 tooa 新的或現有 Azure 自動化帳戶的 Azure Resource Manager 範本。 hello 範本將會使用輸入的參數將包含您的環境的 hello 變數 toocreate 自動化資產。

部署 hello 範本之後，您可以直接參考 toostep 4 在此指南 tooonboard 您的電腦。

hello 範本將會執行下列 hello:

1. 使用現有的「自動化」帳戶或建立一個新帳戶
2. 採用下列各項的輸入參數︰
   * ASRRemoteFile-hello 位置 hello 行動服務安裝程式的儲存位置
   * ASRPassphrase-hello 位置 hello passphrase.txt 檔案的儲存位置
   * ASRCSEndpoint-hello 的管理伺服器的 IP 位址
3. 匯入 hello xPSDesiredStateConfiguration PowerShell 模組
4. 建立及編譯 hello DSC 設定

讓您可以啟動登入您的機器進行保護，將會在 hello 正確的順序，進行所有先前步驟的 hello。

hello 範本的指示部署中，位於[GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC)。

使用 PowerShell 部署 hello 範本：

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>後續步驟
在您部署的 hello 行動服務代理程式之後，您可以[啟用複寫](site-recovery-vmware-to-azure.md)hello 虛擬機器。
