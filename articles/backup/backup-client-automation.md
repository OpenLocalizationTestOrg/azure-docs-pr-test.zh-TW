---
title: "設定 Windows Server tooAzure aaaUse PowerShell tooback |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理使用 PowerShell 的 Azure 備份"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>部署和管理備份 tooAzure 使用 PowerShell 的 Windows 伺服器/Windows 用戶端
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [傳統](backup-client-automation-classic.md)
>
>

本文章將示範如何 toouse PowerShell for Azure 備份 Windows Server 或 Windows 用戶端上所設定和管理備份和復原。

## <a name="install-azure-powershell"></a>安裝 Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

本文著重在 hello Azure 資源管理員 (ARM) 和 hello MS 線上備份的 PowerShell cmdlet 可讓您 toouse 復原服務保存庫的資源群組中。

在 2015 年 10 月，Azure PowerShell 1.0 已發行。 此版本中成功 hello 為 0.9.8 版，並讓它們回到相關的某些重要的變更，尤其是在 hello hello 指令程式的命名模式。 1.0 cmdlet 後續 hello 命名模式 {動詞}-AzureRm {名詞};而 hello 為 0.9.8 名稱不包含**Rm** (例如，而不是新增 AzureResourceGroup 的新增-AzureRmResourceGroup)。 使用 Azure PowerShell 為 0.9.8 時，您必須先啟用 hello Resource Manager 模式執行 hello **Switch-azuremode AzureResourceManager**命令。 1.0 或更新版本不需要執行此命令。

如果您想 toouse 您撰寫的 hello 1.0 或更新版本的環境中的 hello 為 0.9.8 環境的指令碼應該仔細更新及預先生產環境中測試 hello 指令碼，然後才使用生產 tooavoid 中預期的影響。

[下載最新 PowerShell 版本 hello](https://github.com/Azure/azure-powershell/releases) (所需的最低版本是： 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
hello 步驟會引導您完成建立復原服務保存庫。 復原服務保存庫不同於備份保存庫。

1. 如果您使用 Azure Backup hello 第一次，您必須使用 hello**暫存器 AzureRMResourceProvider** cmdlet tooregister hello Azure 復原服務提供者與您的訂用帳戶。

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. hello 復原服務保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。 您可以使用現有的資源群組，或建立一個新的群組。 建立新的資源群組時，指定 hello 名稱和位置 hello 資源群組。  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. 使用 hello**新增 AzureRmRecoveryServicesVault** cmdlet toocreate hello 新的保存庫。 請務必 toospecify hello hello 保存庫相同的位置，所用的 hello 資源群組。

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. 指定儲存體備援 toouse; hello 類型您可以使用[本機備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage)或[地理備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。 hello 下列範例顯示 hello testVault-BackupStorageRedundancy 選項設定 tooGeoRedundant。

   > [!TIP]
   > 許多 Azure Backup cmdlet 需要 hello 復原服務保存庫的物件做為輸入。 基於這個理由，它是方便 toostore hello 備份復原服務保存庫在變數中。
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>檢視訂用帳戶中的 hello 保存庫
使用**Get AzureRmRecoveryServicesVault** tooview hello 份 hello 目前訂用帳戶中所有的保存庫。 您可以使用，則已建立新的保存庫，此命令 toocheck 或 toosee hello 訂用帳戶中有哪些保存庫。

執行 hello 命令**Get AzureRmRecoveryServicesVault**，並列出 hello 訂用帳戶中所有的保存庫。

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent"></a>安裝 hello Azure Backup agent
安裝 hello Azure Backup agent 之前，您需要 toohave hello 安裝程式，下載和 hello Windows Server 上也一樣。 收到 hello 的 hello 最新版本的 hello installer [Microsoft Download Center](http://aka.ms/azurebackup_agent)或從 hello 復原服務保存庫的 [儀表板] 頁面。 儲存 hello installer tooan 更容易存取的位置，例如 * C:\Downloads\*。

或者，使用 PowerShell tooget hello 程式下載程式：
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

tooinstall hello 代理程式，執行下列命令，在提升權限的 PowerShell 主控台中的 hello:

```
PS C:\> MARSAgentInstaller.exe /q
```

這會 hello 代理程式安裝與所有 hello 預設選項。 hello 安裝需要幾分鐘 hello 背景。 如果您未指定 hello */nu*選項則 hello **Windows Update**視窗隨即開啟的任何更新的 hello 安裝 toocheck hello 結尾。 安裝之後，安裝程式的 hello 清單會顯示 hello 代理程式。

toosee hello 列出已安裝的程式，請移過**控制台** > **程式** > **程式和功能**。

![已安裝代理程式](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>安裝選項
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

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>註冊 Windows Server 或 Windows 用戶端機器 tooa 復原服務保存庫
建立 hello 復原服務保存庫之後，請下載 hello 最新的代理程式 」 和 「 hello 保存庫認證，並將它儲存在方便的位置，例如 C:\Downloads。

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

在 hello Windows Server 或 Windows 用戶端電腦上，執行 hello [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) hello 保存庫 cmdlet tooregister hello 機器。
這個及其他指令程式使用的備份，會從 hello MSONLINE 模組 hello 安裝程序的一部分加入的 Mars AgentInstaller 哪些 hello。 

hello 代理程式安裝程式不會更新 hello $Env: PSModulePath 變數。 這表示模組自動載入會失敗。 tooresolve 這樣，您可以 hello 下列：

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

或者，您可以手動載入 hello 模組在您的指令碼，如下所示：

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

一旦您載入 hello Online Backup cmdlet，您會註冊 hello 保存庫認證：


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> 請勿使用相對路徑 toospecify hello 保存庫認證檔案。 您必須提供絕對路徑做為輸入的 toohello cmdlet。
>
>

## <a name="networking-settings"></a>網路設定
Hello 連線 hello 的 Windows 電腦的 toohello 網際網路是透過 proxy 伺服器，當 hello proxy 設定也可以提供 toohello 代理程式。 本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。

頻寬使用也可以控制與 hello 選項```work hour bandwidth```和```non-work hour bandwidth```一組指定的 hello 一週天數。

設定 hello proxy 和頻寬詳細資料是使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>加密設定
hello 傳送備份資料 tooAzure 備份是加密的 tooprotect hello hello 資料機密性。 hello 加密複雜密碼是還原的 hello 「 密碼 」 toodecrypt hello 資料在 hello 階段。

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> 安全及安全一旦設定之後，保留 hello 複雜密碼資訊。 您無法將資料從 Azure 可以 toorestore 沒有此複雜密碼。
>
>

## <a name="back-up-files-and-folders"></a>備份檔案和資料夾
從 Windows 伺服器和用戶端 tooAzure 備份的所有備份都受到原則。 hello 原則包含三個部分：

1. A**備份排程**，指定當備份需要 toobe 採取和與 hello 服務同步處理。
2. A**保留排程**指定 tooretain hello 復原點在 Azure 中的時間長度。
3. **檔案包含/排除規格** ，指出要備份的項目。

本文件中要說明如何將備份自動化，因此我們假設還未設定任何選項。 一開始我們先建立新的備份原則使用 hello [New-obpolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet。

```
PS C:\> $newpolicy = New-OBPolicy
```

在此時間 hello 原則是空的其他指令程式會需要的 toodefine、 哪些項目會包含或排除備份會執行，且其中 hello 時將儲存備份。

### <a name="configuring-hello-backup-schedule"></a>設定 hello 備份排程
第一次 hello hello 原則的 3 組件是 hello 備份排程，會建立使用 hello[新增 OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet。 hello 備份排程會定義當備份需要採取 toobe。 建立排程時您會需要 toospecify 2 輸入的參數：

* **Hello 一周天數**該 hello 應該執行備份。 您可以執行 hello 上只要一天的備份作業或 hello 週中的每日兩者之間的任何組合。
* **Hello 每天時間**hello 備份何時應執行。 您可以定義總 too3 hello 備份將會觸發時機的 hello 每天不同時間。

例如，您可以設定每週六和日下午 4 點執行備份原則。

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

hello 備份排程必須 toobe 與原則相關聯，而且這可藉由使用 hello [Set-obschedule](https://technet.microsoft.com/library/hh770407) cmdlet。

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>設定保留原則
hello 保留原則定義多久的復原點建立的備份作業都會保留下來。 當建立新的保留原則，使用 hello[新增 OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet，您可以指定 hello 的天數 hello 備份復原點需要使用 Azure 備份保留 toobe。 下列的 hello 範例設定為 7 天的保留原則。

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

hello 保留原則必須關聯與 hello 主要原則使用 hello cmdlet[組 OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>包含和排除檔案 toobe 備份
```OBFileSpec```物件會定義 hello 檔案 toobe 包含和排除在備份中。 這是一組規則範圍出 hello 保護檔案和電腦上的資料夾。 您可以設定所需數量的檔案包含或排除規則，並建立其與原則的關聯。 建立新的 OBFileSpec 物件時，您可以：

* 指定包含 hello 檔案和資料夾 toobe
* 指定排除 hello 檔案和資料夾 toobe
* 指定最多的遞迴備份的資料夾 （或） 中是否只 hello 最上層資料夾中的檔案 hello 指定應該要備份的資料。

hello 後者是利用 hello New-obfilespec 命令 hello-非遞迴旗標來達成。

在 hello 下列範例中，我們將備份磁碟區 c： 和 d:，並排除 hello hello Windows 資料夾和任何暫存資料夾中的 OS 二進位檔。 讓我們將建立兩個檔案規格使用 hello toodo [New-obfilespec](https://technet.microsoft.com/library/hh770408) cmdlet-包含和排除。 一旦已建立 hello 檔案規格，它們相關聯 hello 原則使用 hello [Add-obfilespec](https://technet.microsoft.com/library/hh770424) cmdlet。

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>套用 hello 原則
現在 hello 原則物件已完成，並具有相關聯的備份排程、 保留原則，以及檔案的包含/排除清單。 此原則現在可以針對 Azure Backup toouse 認可。 原則在套用新建立的 hello 之前請確認沒有任何現有的備份原則，使用 hello 與 hello 伺服器相關聯[移除 OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet。 移除 hello 原則將會提示您確認。 tooskip hello 確認使用 hello```-Confirm:$false```與 hello 指令的旗標。

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

調配 hello 原則物件是使用 hello [Set-obpolicy](https://technet.microsoft.com/library/hh770421) cmdlet。 系統將提示您進行確認。 tooskip hello 確認使用 hello```-Confirm:$false```與 hello 指令的旗標。

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

您可以檢視 hello 詳細資料的 hello 現有的備份原則使用 hello [Get-obpolicy](https://technet.microsoft.com/library/hh770406) cmdlet。 您可以向下鑽研進一步使用 hello [Get OBSchedule](https://technet.microsoft.com/library/hh770423) hello 備份排程和 hello cmdlet [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello 保留原則的 cmdlet

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>執行臨機操作備份
一旦已設定備份原則 hello 備份會依 hello 排程。 觸發臨機操作備份，您也可以使用 hello[開始 OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>從 Azure 備份還原資料
本節將引導您 hello 步驟自動化從 Azure 備份復原資料。 其中涉及 hello 下列步驟：

1. 挑選 hello 來源磁碟區
2. 選擇備份的點 toorestore
3. 選擇項目 toorestore
4. 觸發程序 hello 還原程序

### <a name="picking-hello-source-volume"></a>挑選 hello 來源磁碟區
在訂單 toorestore Azure Backup 中的項目，您必須先 tooidentify hello hello 項目的來源。 我們正在 Windows Server 或 Windows 用戶端 hello 內容中執行 hello 命令，因為已經識別 hello 機器。 hello 下一個步驟來識別 hello 來源是包含它的 tooidentify hello 磁碟區。 一份磁碟區或來源備份從這部電腦可以擷取執行 hello [Get-obrecoverablesource](https://technet.microsoft.com/library/hh770410) cmdlet。 此命令會傳回所有 hello 來源備份來源伺服器/用戶端的陣列。

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>選擇備份點從哪些 toorestore
擷取一份備份時間點執行 hello [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet 搭配適當的參數。 在本例中，我們將選擇 hello 最新備份點 hello 來源磁碟區*d:* ，並用 toorecover 特定檔案。

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
hello 物件```$rps```是備份的點陣列。 hello 第一個元素是 hello 最新的點而 hello 第 n 個項目是 hello 最舊的點。 toochoose hello 最新的點，我們將使用```$rps[0]```。

### <a name="choosing-an-item-toorestore"></a>選擇項目 toorestore
以遞迴方式 tooidentify hello 確實的檔案或資料夾 toorestore，使用 hello [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet。 該方式 hello 資料夾階層可瀏覽單獨使用 hello ```Get-OBRecoverableItem```。

在此範例中，如果我們想要 toorestore hello 檔*finances.xls*我們可以參考使用 hello 物件```$filesFolders[1]```。

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

您也可以搜尋項目 toorestore 使用 hello ```Get-OBRecoverableItem``` cmdlet。 在本例中，針對 toosearch *finances.xls*我們無法取得的控制代碼 hello 檔案上執行此命令：

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>觸發 hello 還原程序
tootrigger hello 還原程序，我們必須先 toospecify hello 復原選項。 這可以經由使用 hello[新增 OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet。 例如，假設我們想 toorestore hello 檔案太*C:\temp*。我們也假設我們想要在 hello 目的地資料夾已存在 tooskip 檔案*C:\temp*。 toocreate 這類復原選項，使用下列命令的 hello:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

現在使用 hello 觸發 hello 還原程序[Start-obrecovery](https://technet.microsoft.com/library/hh770402.aspx) hello 選取命令```$item```hello hello 輸出```Get-OBRecoverableItem```cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>解除安裝 hello Azure 備份代理程式
解除安裝 hello Azure 備份代理程式可以使用下列命令的 hello:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Hello 機器上解除安裝 hello 代理程式二進位檔有某些後果 tooconsider:

* 移除 hello 機器 hello 檔案篩選器，並會停止追蹤的變更。
* 從 hello 機器，移除所有原則資訊，但仍繼續 toobe 儲存在 hello 服務中的 hello 原則資訊。
* 會移除所有備份排程，且不再進行任何備份。

不過，hello 會維持為 Azure 中儲存的資料，而且您根據 hello 保留原則設定會保留。 較舊的時間點會自動過時。

## <a name="remote-management"></a>遠端管理
可以透過 PowerShell 遠端執行所有 hello 管理周圍 hello Azure 備份代理程式、 原則和資料來源。 需要 toobe 備妥正確的 hello 機器將從遠端管理。

根據預設，hello WinRM 服務設定為手動啟動。 hello 啟動類型必須設定得*自動*和 hello 服務應該啟動。 tooverify 的 hello WinRM 服務正在執行，hello hello Status 屬性值應該是*執行*。

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

應該將 PowerShell 設定為可以遠端執行。

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

hello 電腦現在可以管理遠端-從 hello hello 代理程式安裝。 例如，下列指令碼的 hello 複製 hello 代理程式 toohello 遠端電腦，並將它安裝。

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>後續步驟
如需 Windows Server/用戶端的 Azure 備份詳細資訊，請參閱

* [簡介 tooAzure 備份](backup-introduction-to-azure-backup.md)
* [備份 Windows 伺服器](backup-configure-vault.md)
