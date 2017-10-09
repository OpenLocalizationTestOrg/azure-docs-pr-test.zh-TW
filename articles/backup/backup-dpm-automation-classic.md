---
title: "Azure 備份： DPM 工作負載備份使用 PowerShell tooback |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理 Azure 備份的 Data Protection Manager (DPM) 使用 PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>部署和管理備份 tooAzure Data Protection Manager (DPM) 伺服器使用 PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [傳統](backup-dpm-automation-classic.md)
>
>

這篇文章說明如何 toouse PowerShell tooback 及復原 DPM 資料從備份保存庫。 Microsoft 建議讓大部分的新部署使用復原服務保存庫。 如果您是新的 Azure 備份使用者，使用 hello 文章[部署和管理使用 PowerShell 的 Data Protection Manager 資料 tooAzure](backup-dpm-automation.md)，因此您將資料儲存在復原服務保存庫中。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="setting-up-hello-powershell-environment"></a>設定 hello PowerShell 環境
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

您可以使用從 Data Protection Manager tooAzure PowerShell toomanage 備份之前，您必須在 PowerShell 中的 toohave hello 右環境。 在 hello 開頭 hello PowerShell 工作階段，請確定您執行下列命令 tooimport hello 右模組 hello 和 toocorrectly 參考 hello DPM 指令程式可讓您：

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>設定和註冊
toobegin:

1. [下載最新的 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需最低版本為：1.0.0)
2. 啟用 hello Azure 備份指令程式，藉由切換太*AzureResourceManager*模式使用 hello **Switch-azuremode**指令程式：

```
PS C:\> Switch-AzureMode AzureResourceManager
```

hello 下列安裝和註冊工作可以自動化使用 PowerShell:

* 建立備份保存庫
* 安裝 hello Azure Backup agent
* 註冊以 hello Azure 備份服務
* 網路設定
* 加密設定

### <a name="create-a-backup-vault"></a>建立備份保存庫
> [!WARNING]
> Hello 第一次使用 Azure Backup 的客戶，您需要 tooregister hello Azure 備份提供者 toobe 搭配您的訂用帳戶。 這可藉由執行下列命令的 hello： 暫存器 AzureProvider ProviderNamespace"Microsoft.Backup"
>
>

您可以建立新的備份保存庫使用 hello**新增 AzureRMBackupVault**指令程式。 hello 備份保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。 在提升權限的 Azure PowerShell 主控台中，執行下列命令的 hello:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

您可以取得一份所有 hello 備份保存庫中指定的訂用帳戶使用 hello **Get AzureRMBackupVault**指令程式。

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>在 DPM 伺服器上安裝 hello Azure Backup agent
安裝 hello Azure Backup agent 之前，您需要 toohave hello 安裝程式，下載和 hello Windows Server 上也一樣。 收到 hello 的 hello 最新版本的 hello installer [Microsoft Download Center](http://aka.ms/azurebackup_agent)或從 hello 備份保存庫的 [儀表板] 頁面。 儲存 hello installer tooan 更容易存取的位置，例如 * C:\Downloads\*。

tooinstall hello 代理程式，執行下列命令，在提升權限的 PowerShell 主控台中的 hello **hello DPM 伺服器上**:

```
PS C:\> MARSAgentInstaller.exe /q
```

這會 hello 代理程式安裝與所有 hello 預設選項。 hello 安裝需要幾分鐘 hello 背景。 如果您未指定 hello */nu*選項 hello **Windows Update**視窗隨即開啟的任何更新的 hello 安裝 toocheck hello 結尾。

hello 代理程式會顯示 hello 的安裝程式的清單中。 toosee hello 列出已安裝的程式，請移過**控制台** > **程式** > **程式和功能**。

![已安裝代理程式](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>安裝選項
toosee 所有 hello 選項可透過使用 hello 命令列，請使用下列命令的 hello:

```
PS C:\> MARSAgentInstaller.exe /?
```

hello 可用的選項包括：

| 選項 | 詳細資料 | 預設值 |
| --- | --- | --- |
| /q |無訊息安裝 |- |
| /p:"location" |路徑 toohello hello Azure Backup agent 的安裝資料夾。 |C:\Program Files\Microsoft Azure Recovery Services Agent |
| /s:"location" |路徑 toohello hello Azure 備份代理程式的快取資料夾。 |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |選擇加入 tooMicrosoft 更新 |- |
| /nu |安裝完成後不要檢查更新 |- |
| /d |解除安裝 Microsoft Azure 復原服務代理程式 |- |
| /ph |Proxy 主機位址 |- |
| /po |Proxy 主機連接埠號碼 |- |
| /pu |Proxy 主機使用者名稱 |- |
| /pw |Proxy 密碼 |- |

### <a name="registering-with-hello-azure-backup-service"></a>註冊以 hello Azure 備份服務
您可以向 hello Azure 備份服務之前，您需要 tooensure 該 hello[必要條件](backup-azure-dpm-introduction.md)符合。 您必須：

* 具備有效的 Azure 訂用帳戶
* 具備備份保存庫

toodownload hello 保存庫認證，執行 hello **Get AzureBackupVaultCredentials** cmdlet，它在方便的位置類似 Azure PowerShell 主控台和存放區中 * C:\Downloads\*。

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Hello 保存庫註冊 hello 機器是使用 hello[開始 DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

這會向 Microsoft Azure 保存庫，使用指定的 hello hello DPM 伺服器名為"TestingServer 」 保存庫認證。

> [!IMPORTANT]
> 請勿使用相對路徑 toospecify hello 保存庫認證檔案。 您必須提供絕對路徑做為輸入的 toohello cmdlet。
>
>

### <a name="initial-configuration-settings"></a>初始組態設定
一旦 hello DPM 伺服器已向 hello Azure 備份保存庫，就會開始使用預設訂用帳戶設定。 這些訂用帳戶設定包括網路、 加密和 hello 暫存區域。 toobegin 變更 hello 訂用帳戶設定需要 toofirst 取得的控制代碼上 hello 現有 （預設值） 的設定使用 hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

所有修改都都本機 PowerShell 物件提出的 toothis ```$setting``` hello 完整物件則不認可的 tooDPM 和 Azure 備份 toosave 它們使用 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。 您需要 toouse hello ```–Commit``` hello 變更的旗標 tooensure 會保存。 hello 設定將不套用，Azure 備份所使用，除非已認可。

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>網路
如果 hello DPM 機器 toohello hello 上的 Azure 備份服務的 hello 連線網際網路，透過 proxy 伺服器 hello proxy 伺服器設定應該提供的備份 toosucceed。 這是使用 hello ```-ProxyServer```， ```-ProxyPort```，```-ProxyUsername```和 hello```ProxyPassword```參數以 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。 本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

頻寬使用也可以控制選項的```-WorkHourBandwidth```和```-NonWorkHourBandwidth```一組指定的 hello 一週天數。 本範例未設定任何節流。

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a>設定 hello 臨時區域
hello DPM 伺服器上執行的 hello Azure 備份代理程式需要暫存位置，還原從 hello 雲端 （本機臨時區域） 的資料。 設定使用 hello hello 臨時區域[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet 和 hello```-StagingAreaPath```參數。

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Hello 上述範例中，在 hello 臨時區域將太設定*C:\StagingArea* hello PowerShell 物件中```$setting```。 請確定 hello 指定的資料夾已經存在，否則 hello 最終認可的 hello 訂用帳戶設定將會失敗。

### <a name="encryption-settings"></a>加密設定
hello 傳送備份資料 tooAzure 備份是加密的 tooprotect hello hello 資料機密性。 hello 加密複雜密碼是還原的 hello 「 密碼 」 toodecrypt hello 資料在 hello 階段。 它是重要 tookeep 此資訊安全，而且一旦設定保護。

Hello 下列範例中，在 hello 第一個命令會將轉換字串 hello ```passphrase123456789``` tooa 安全字串，並指派 hello 安全字串 toohello 名為變數```$Passphrase```。 hello 第二個命令設定安全字串的 hello```$Passphrase```當做 hello 密碼加密備份。

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> 安全及安全一旦設定之後，保留 hello 複雜密碼資訊。 您不會將資料從 Azure 可以 toorestore 沒有此複雜密碼。
>
>

此時，您應該做所有所需的 hello 變更 toohello```$setting```物件。 請記住 toocommit hello 變更。

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>保護資料 tooAzure 備份
在本節中，您將加入實際執行伺服器 tooDPM，然後保護 hello 資料 toolocal DPM 存放裝置，然後 tooAzure 備份。 Hello 範例中，我們將示範如何 tooback 檔案及資料夾。 hello 邏輯很容易就能擴充的 toobackup 任何 DPM 支援的資料來源。 所有 DPM 備份皆受到保護群組 (PG) 所控管，並且由四個部分構成：

1. **群組成員**是所有的 hello 可保護物件的清單 (也稱為*Datasources*在 DPM 中) 您想在 hello tooprotect 相同的保護群組。 比方說，您可能想 tooprotect 生產 Vm 一個保護群組與另一個保護群組中的 SQL Server 資料庫中，因為它們可能會有不同的備份需求。 您可以在實際伺服器上備份任何資料來源必須先確定 toomake hello hello 伺服器上安裝 DPM 代理程式，並由 DPM 管理。 請依照下列步驟 hello[安裝 hello DPM 代理程式](https://technet.microsoft.com/library/bb870935.aspx)並將其連結 toohello 適當的 DPM 伺服器。
2. **資料保護方式**指定 hello 目標備份位置-磁帶、 磁碟和雲端。 在本例中，我們會保護資料 toohello 本機磁碟和 toohello 雲端。
3. A**備份排程**，會指定備份時需要採取 toobe hello 資料應該同步處理頻率 hello DPM 伺服器與 hello 實際執行伺服器之間。
4. A**保留排程**指定 tooretain hello 復原點在 Azure 中的時間長度。

### <a name="creating-a-protection-group"></a>建立保護群組
開始建立新的保護群組使用 hello[新增 DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet。

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

hello 以上指令程式會建立名為保護群組*ProtectGroup01*。 現有的保護群組也可以修改更新 tooadd 備份 toohello Azure 雲端。 不過，toomake 的任何變更 toohello 新保護群組的或現有的-我們需要 tooget 控制代碼上*可修改*物件使用 hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet。

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>加入群組成員 toohello 保護群組
每個 DPM 代理程式知道 hello hello 其安裝所在的伺服器上的資料來源的清單。 tooadd datasource toohello 保護群組，DPM 代理程式需求 toofirst hello 傳送 hello 資料來源後 toohello DPM 伺服器的清單。 一或多個資料來源會選取並加入 toohello 保護群組。 hello PowerShell 所需的步驟 tooget 來達成此：

1. 擷取由 DPM 管理透過 hello DPM 代理程式的所有伺服器清單。
2. 選擇特定伺服器。
3. 擷取 hello 伺服器上的所有資料來源的清單。
4. 選擇一或多個資料來源，並將其新增 toohello 保護群組

伺服器的 hello DPM 代理程式已安裝且受 DPM 伺服器 hello hello 清單取得以 hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet。 在此範例中，我們將篩選並只設定名稱為 *productionserver01* 的 PS 來進行備份。

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

上的 立即擷取的資料來源的 hello 清單```$server```使用 hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet。 在此範例中我們會篩選 hello 磁碟區 * d:\*我們想要備份的 tooconfigure。 此資料來源，然後會加入 toohello 保護群組使用 hello[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet。 請記住 toouse hello *modifable*保護群組物件```$MPG```toomake hello 新增項目。

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

重複此步驟，視需要多次直到您已經新增所有 hello 選擇資料來源 toohello 保護群組。 您也可以只有一個資料來源，以及用於建立 hello 保護群組的完整 hello 工作流程的開頭，並在稍後加入更多的資料來源 toohello 保護群組。

### <a name="selecting-hello-data-protection-method"></a>選取 hello 資料保護方式
一旦 hello 資料來源已加入 toohello 保護群組，hello 下一個步驟是使用 hello toospecify hello 保護方法[組 DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet。 在此範例中，hello 保護群組將會安裝本機磁碟和雲端備份。 您也需要您想使用 hello tooprotect toocloud toospecify hello datasource[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet 搭配-線上旗標。

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>設定 hello 保留範圍
設定使用 hello hello 備份點 hello 保留[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。 雖然看起來奇數 tooset hello 保留之前 hello 備份排程已定義，使用 hello```Set-DPMPolicyObjective```指令程式會自動設定預設的備份排程，其可以加以修改。 它永遠是可能 tooset hello 備份排程第一次，並 hello 之後保留原則。

Hello 下列範例中，在 hello cmdlet 會設定 hello 保持參數對於磁碟備份。 這將會保留備份的 10 天，並同步處理資料之間 hello 實際伺服器與 hello DPM 伺服器每隔 6 小時。 hello```SynchronizationFrequencyMinutes```頻率備份點建立時，如何但不會定義通常資料會複製的 toohello DPM 伺服器，如此可防止備份變得太大。

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

備份將的 tooAzure （DPM 會參照為線上備份 toothese） hello 的保留範圍可以設定成[長期的保留使用祖父-父親-Son 配置 (GFS)](backup-azure-backup-cloud-as-tape.md)。 也就是說，您可以定義結合的保留原則，包含每日、每週、每月和每年保留原則。 在此範例中，我們建立陣列，表示我們想要的 hello 複雜的保留配置，然後設定使用 hello hello 保留範圍[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>設定 hello 的備份排程
DPM 預設備份的排程自動設定如果您指定使用 hello hello 保護目標```Set-DPMPolicyObjective```cmdlet。 toochange hello 預設排程，使用 hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet 加 hello[組 DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet。

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

在 hello 上述範例中，```$onlineSch```是四個元素陣列，其中包含 hello 現有的線上保護排程 hello GFS 配置中的 hello 保護群組：

1. ```$onlineSch[0]```將包含 hello 每日排程
2. ```$onlineSch[1]```將包含 hello 每週排程
3. ```$onlineSch[2]```將包含 hello 每月排程
4. ```$onlineSch[3]```將包含 hello 每年的排程

因此，如果您需要 toomodify hello 每週排程，您需要 toorefer toohello ```$onlineSch[1]```。

### <a name="initial-backup"></a>初始備份
當第一次備份 hello 的資料來源，DPM 需要 toocreate 這將會建立一份 hello datasource toobe 受保護的 DPM 複本磁碟區上的初始複本。 此活動可以特定的時間，排程，或可以觸發以手動方式，使用 hello[組 DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet 搭配 hello 參數```-NOW```。

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>變更 hello 的 DPM 複本與復原點磁碟區的大小
您也可以變更的 DPM 複本磁碟區，以及陰影複製磁碟區使用的 hello 大小[組 DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet，如下列範例中的 hello 所示： Get-datasourcediskallocation Datasource $DSSet-datasourcediskallocation-Datasource $DS-ProtectionGroup $MPG-手動 ReplicaArea (2 gb) ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>認可 hello 變更 toohello 保護群組
最後，hello 變更需要 toobe 認可 DPM 才會每個新保護群組組態 hello hello 備份。 這是使用 hello[組 DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet。

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>檢視 hello 備份點
您可以使用 hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget 一份所有資料來源的復原點。 在此範例中，我們將會：

* 擷取所有的 hello PGs hello DPM 伺服器會儲存在陣列上```$PG```
* 取得 hello 資料來源對應 toohello```$PG[0]```
* 取得資料來源中的 hello 的所有復原點。

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>還原在 Azure 上保護的資料
還原資料是 ```RecoverableItem``` 物件和 ```RecoveryOption``` 物件的組合。 Hello 前一節中得到 hello 備份點清單的資料來源。

在 hello 下列範例中，我們示範 toorestore HYPER-V 虛擬機器，從 Azure Backup 以 hello 結合備份點進行復原的目標。 其中包括：

* 建立的復原選項使用 hello[新增 DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet。
* 使用 hello 的備份點擷取 hello 陣列```Get-DPMRecoveryPoint```cmdlet。
* 選擇從備份點 toorestore。

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

任何資料來源類型時，可以輕鬆地擴充 hello 命令。

## <a name="next-steps"></a>後續步驟
* 如需 Azure 備份的 DPM，請參閱[簡介 tooDPM 備份](backup-azure-dpm-introduction.md)
