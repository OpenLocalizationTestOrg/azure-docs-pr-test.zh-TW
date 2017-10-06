---
title: "aaaDeploy 及管理 Azure Vm 使用 PowerShell 備份 |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理使用 PowerShell 的 Azure 備份。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>使用虛擬機器 AzureRM.Backup cmdlet tooback
> [!div class="op_single_selector"]
> * [資源管理員](backup-azure-vms-automation.md)
> * [傳統](backup-azure-vms-classic-automation.md)
>
>

本文將說明如何備份及修復 Azure Vm 的 toouse Azure PowerShell。 Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。 本文說明如何使用 hello 傳統部署模型 tooback 資料 tooa 備份保存庫註冊。 如果您不在您的訂用帳戶中建立備份保存庫，請參閱這篇文章，hello 資源管理員版本[虛擬機器使用 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md)。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="concepts"></a>概念
這篇文章會提供特定 toohello PowerShell cmdlet 使用 tooback 虛擬機器資訊。 如需有關保護 Azure VM 的基本資訊，請參閱 [Plan your VM backup infrastructure in Azure (在 Azure 中規劃 VM 備份基礎結構)](backup-azure-vms-introduction.md)。

> [!NOTE]
> 開始之前，閱讀 hello[必要條件](backup-azure-vms-prepare.md)需要使用 Azure 備份 」 和 「 hello toowork[限制](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)hello 目前 VM 備份解決方案。
>
>

toouse PowerShell 實際上，需要目前 toounderstand hello 階層的物件和從哪裡 toostart。

![物件階層](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

hello 兩個最重要的流程會啟用保護的 vm，並從復原點還原資料。 這篇文章 hello 重點是 toohelp 您變得家 hello PowerShell cmdlet tooenable 使用這兩種情況。

## <a name="setup-and-registration"></a>設定和註冊
toobegin:

1. [下載最新的 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需最低版本為：1.0.0)
2. 輸入下列命令的 hello 尋找可用的 hello Azure 備份的 PowerShell cmdlet:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

hello 下列安裝和註冊工作可以自動化使用 PowerShell:

* 建立備份保存庫
* Hello Vm 向 hello Azure 備份服務

### <a name="create-a-backup-vault"></a>建立備份保存庫
> [!WARNING]
> Hello 第一次使用 Azure Backup 的客戶，您需要 tooregister hello Azure 備份提供者 toobe 搭配您的訂用帳戶。 這可藉由執行下列命令的 hello： 暫存器 AzureRmResourceProvider ProviderNamespace"Microsoft.Backup"
>
>

您可以建立新的備份保存庫使用 hello**新增 AzureRmBackupVault** cmdlet。 hello 備份保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。 在提升權限的 Azure PowerShell 主控台中，執行下列命令的 hello:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

您可以取得一份所有 hello 備份保存庫中指定的訂用帳戶使用 hello **Get AzureRmBackupVault** cmdlet。

> [!NOTE]
> 它是方便 toostore hello 備份保存庫物件放入變數中。 做為輸入，許多 Azure Backup cmdlet 需要 hello 保存庫的物件。
>
>

### <a name="registering-hello-vms"></a>註冊 hello Vm
hello 第一個步驟設定 Azure backup 備份是 tooregister 電腦或 VM 的 Azure 備份保存庫。 hello**暫存器 AzureRmBackupContainer** cmdlet 會採用 hello Azure IaaS 虛擬機器輸入的資訊與 hello 指定保存庫上登錄它。 hello 註冊作業會關聯 hello 備份保存庫中的 hello Azure 虛擬機器，並追蹤透過 hello 備份生命週期 hello VM。

以 hello Azure 備份服務註冊您的 VM 建立最上層的容器物件。 容器通常包含多個項目，可以備份，但是在 hello 案例中的 Vm 會 hello 容器只能有一個備份的項目。

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>備份 Azure VM
### <a name="create-a-protection-policy"></a>建立保護原則
不強制 toocreate 新 Vm 的保護原則 toostart 備份。 hello 保存庫隨附 「 '預設原則' 是使用的 tooquickly 啟用保護，且與 hello 右邊的詳細資料然後稍後編輯。 您可以取得一份提供 hello 保存庫中的 hello 原則使用 hello **Get AzureRmBackupProtectionPolicy** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> 在 PowerShell 中的 hello BackupTime 欄位的 hello 時區為 UTC。 不過，當 hello 備份時間所示為 hello Azure 入口網站，hello 時區是對齊的 tooyour 以及 hello UTC 位移的本機系統。
>
>

備份原則至少與一個保留原則相關聯。 hello 保留原則會定義復原點保留多久向 Azure 備份。 hello**新增 AzureRmBackupRetentionPolicy** cmdlet 會建立 PowerShell 物件的保留原則資訊。 這些保留原則物件會當做輸入 toohello*新增 AzureRmBackupProtectionPolicy* cmdlet，或直接與 hello*啟用 AzureRmBackupProtection* cmdlet。

備份原則會定義時間和頻率 hello 備份的項目完成。 hello**新增 AzureRmBackupProtectionPolicy** cmdlet 會建立保留的備份原則資訊的 PowerShell 物件。 hello 備份原則時，會輸入 toohello*啟用 AzureRmBackupProtection* cmdlet。

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>啟用保護。
啟用保護牽涉到兩個物件-hello 項目和 hello 原則和兩個需要 toobelong toohello 相同保存庫。 一旦 hello 原則已與 hello 項目相關聯，hello 備份工作流程會開始運作在 hello 定義的排程。

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>初始備份
hello 備份排程會負責種 hello 完整初始複製 hello 項目的 hello 累加複製 hello 後續備份。 不過，如果您想 tooforce hello 初始備份 toohappen 在一段時間，或甚至立即然後使用 hello**備份 AzureRmBackupItem** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> hello 時區的 hello StartTime 和 EndTime 欄位顯示在 PowerShell 中為 UTC。 不過，當 hello 類似的資訊會顯示 hello Azure 入口網站，hello 時區是對齊的 tooyour 本機系統時鐘。
>
>

### <a name="monitoring-a-backup-job"></a>監視備份工作
Azure 備份中長時間執行的大部分作業都模擬成工作。 這使得輕鬆 tootrack 進度而不需要隨時都能 tookeep hello Azure 入口網站開啟。

tooget hello 的最新狀態為進行中工作時，使用 hello **Get AzureRmBackupJob** cmdlet。

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

而不是輪詢-這是不需要額外的程式碼-完成這些工作是簡單 toouse hello**等候 AzureRmBackupJob** cmdlet。 指令碼中使用時，hello 指令程式將會暫停 hello 執行，直到 hello 作業完成或 hello 可讓您指定逾時值為止。

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>還原 Azure VM
在訂單 toorestore 備份資料，您需 tooidentify hello 備份項目和 hello 復原點存 hello 時間點資料。 這項資訊是提供的 toohello 還原 AzureRmBackupItem cmdlet tooinitiate hello 保存庫 toohello 客戶的帳戶中的資料的還原。

### <a name="select-hello-vm"></a>選取 hello VM
tooget hello PowerShell 物件，可識別 hello 正確的備份項目，您需要從 hello 保存庫中的 hello 容器 toostart，由上至下物件階層架構。 代表 hello VM，使用 hello tooselect hello 容器**Get AzureRmBackupContainer** cmdlet 並使用管線傳送該 toohello **Get AzureRmBackupItem** cmdlet。

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>選擇復原點
您現在可以列出所有 hello 復原點的 hello 備份項目使用 hello **Get AzureRmBackupRecoveryPoint** cmdlet，然後選擇 hello 復原點 toorestore。 使用者通常會選擇最新的 hello *AppConsistent*點 hello 清單中。

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

hello 變數```$rp```是陣列的復原點的 hello 選取備份項目，以相反順序排序的時間-hello 最新的復原點是在索引 0。 使用標準的 PowerShell 陣列索引 toopick hello 復原點。 例如：```$rp[0]```會選取 hello 最新的復原點。

### <a name="restoring-disks"></a>還原磁碟
沒有完成透過 hello Azure 入口網站和 Azure PowerShell，hello 還原作業之間的主要差異。 使用 PowerShell，hello 還原作業會在還原的 hello 磁碟和組態資訊從 hello 復原點停止。 不會建立虛擬機器。

> [!WARNING]
> hello 還原 AzureRmBackupItem 並不會建立 VM。 它只會還原 hello 磁碟 toohello 指定儲存體帳戶。 這不是 hello hello Azure 入口網站中，將會經歷相同的行為。
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

您可以取得 hello 詳細資料的 hello 還原作業使用 hello **Get AzureRmBackupJobDetails** cmdlet hello 還原作業完成。 hello *ErrorDetails*屬性會有 hello 資訊所需 toorebuild hello VM。

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>建置 hello VM
建置 hello VM 超出 hello 還原磁碟，才可以使用 hello 較舊的 Azure 服務管理 PowerShell cmdlet，hello 新的 Azure 資源管理員範本，或甚至使用 hello Azure 入口網站。 在簡單的範例，我們將示範如何 tooget 該處使用 hello Azure 服務管理 cmdlet。

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

如需有關如何將 VM 從 hello toobuild 還原磁碟的詳細資訊，請閱讀下列 cmdlet 的 hello:

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>程式碼範例
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1.取得 hello 作業子工作的完成狀態
tootrack hello 個別的子工作的完成狀態，您可以使用 hello **Get AzureRmBackupJobDetails** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2.建立備份作業的每日/每週報表
系統管理員通常會想的 tooknow hello 過去 24 小時，有哪些備份作業執行 hello 的這些備份工作的狀態。 此外，hello 傳輸的資料量會讓系統管理員的方式 tooestimate 他們每月的資料使用量。 下列指令碼 hello 會提取 hello 的 hello Azure 備份服務的未經處理資料，並顯示 hello PowerShell 主控台中的 hello 資訊。

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

如果您想 tooadd 圖表功能 toothis 報表輸出時，了解從 hello TechNet 部落格文章[圖表使用 PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>後續步驟
如果您喜歡使用 PowerShell tooengage 與您的 Azure 資源，請參閱 hello PowerShell 文件保護 Windows Server[部署和管理適用於 Windows Server 的備份](backup-client-automation-classic.md)。 另請參閱管理 DPM 備份的 PowerShell 文章：[部署和管理 DPM 的備份](backup-dpm-automation-classic.md)。 這兩篇文章都有適用於 Resource Manager 部署以及傳統部署的版本。
