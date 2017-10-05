---
title: "使用 PowerShell 部署和管理 Azure VM 的備份 | Microsoft Docs"
description: "了解如何使用 PowerShell 部署和管理 Azure 備份。"
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
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a>使用 AzureRM.Backup Cmdlet 備份虛擬機器
> [!div class="op_single_selector"]
> * [資源管理員](backup-azure-vms-automation.md)
> * [傳統](backup-azure-vms-classic-automation.md)
>
>

本文說明如何使用 Azure PowerShell 來備份和復原 Azure VM。 Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。 本文說明如何使用傳統部署模型來將資料備份到備份保存庫。 如果您尚未在訂用帳戶中建立備份保存庫，請參閱[使用 AzureRM.RecoveryServices.Backup Cmdlet 備份虛擬機器](backup-azure-vms-automation.md)這篇文章的 Resource Manager 版本。 Microsoft 建議讓大部分的新部署使用資源管理員模式。

> [!IMPORTANT]
> 您現在可以將備份保存庫升級至復原服務保存庫。 如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。 Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。<br/> 在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有其餘的備份保存庫都會自動升級至復原服務保存庫。
>- 您將無法在傳統入口網站中存取您的備份資料。 相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。
>

## <a name="concepts"></a>概念
本文章提供用來備份虛擬機器之 PowerShell Cmdlet 的特定資訊。 如需有關保護 Azure VM 的基本資訊，請參閱 [Plan your VM backup infrastructure in Azure (在 Azure 中規劃 VM 備份基礎結構)](backup-azure-vms-introduction.md)。

> [!NOTE]
> 開始之前，請閱讀使用 Azure 備份所需的[必要條件](backup-azure-vms-prepare.md)，以及目前 VM 備份解決方案的[限制](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)。
>
>

若要有效地使用 PowerShell，請花一點時間了解物件的階層以及從何處開始。

![物件階層](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

最重要的兩個流程是啟用 VM 保護，以及從復原點還原資料。 本文的重點是協助您熟練 PowerShell Cmdlet 來支援這兩種情況。

## <a name="setup-and-registration"></a>設定和註冊
開始：

1. [下載最新版 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需的基本版本為：1.0.0)
2. 輸入下列命令，以找到可用的 Azure 備份 PowerShell Cmdlet：

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

PowerShell 可以自動化下列設定和註冊工作：

* 建立備份保存庫
* 向 Azure 備份服務註冊 VM

### <a name="create-a-backup-vault"></a>建立備份保存庫
> [!WARNING]
> 對於第一次使用 Azure 備份的客戶，您需要註冊 Azure 備份提供者以搭配您的訂用帳戶使用。 這可以透過執行下列命令來完成：Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"
>
>

您可以使用 **New-AzureRmBackupVault** Cmdlet，來建立新的備份保存庫。 備份保存庫是 ARM 資源，因此您必須將它放在資源群組內。 在提高權限的 Azure PowerShell 主控台中，執行下列命令：

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

您可以使用 **Get-AzureRmBackupVault** Cmdlet，來取得特定訂用帳戶中所有備份保存庫的清單。

> [!NOTE]
> 將備份保存庫物件儲存到變數中會很方便。 許多 Azure 備份 Cmdlet 都需要保存庫物件做為輸入。
>
>

### <a name="registering-the-vms"></a>註冊 VM
使用 Azure 備份來設定備份的第一個步驟是向 Azure 備份保存庫註冊您的電腦或 VM。 **Register-AzureRmBackupContainer** Cmdlet 會取用 Azure IaaS 虛擬機器的輸入資訊，並對指定的保存庫進行註冊。 註冊作業會將 Azure 虛擬機器與備份保存庫相關聯，並於整個備份生命週期內追蹤 VM。

向 Azure 備份服務註冊您的 VM 會建立最上層的容器物件。 一個容器通常包含多個可備份的項目，但以 VM 而言，容器只有一個備份項目。

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>備份 Azure VM
### <a name="create-a-protection-policy"></a>建立保護原則
啟動 VM 的備份並不一定要建立新的保護原則。 保存庫隨附「預設原則」，可用來快速啟用保護，稍後再編輯正確的細節。 您可以使用 **Get-AzureRmBackupProtectionPolicy** Cmdlet，來取得保存庫中可用的原則清單：

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> PowerShell 中 BackupTime 欄位的時區是 UTC。 不過，當備份時間顯示在 Azure 入口網站中時，時區會對應您的本機系統與 UTC 時差。
>
>

備份原則至少與一個保留原則相關聯。 保留原則定義復原點在 Azure 備份中保留的時間長度。 **New-AzureRmBackupRetentionPolicy** Cmdlet 會建立可儲存保留原則資訊的 PowerShell 物件。 這些保留原則物件會用來做為 *New-AzureRmBackupProtectionPolicy* Cmdlet 的輸入，或直接與 *Enable-AzureRmBackupProtection* Cmdlet 搭配使用。

備份原則定義項目備份的時間和頻率。 **New-AzureRmBackupProtectionPolicy** Cmdlet 會建立可儲存備份原則資訊的 PowerShell 物件。 備份原則會用來做為 *Enable-AzureRmBackupProtection* Cmdlet 的輸入。

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>啟用保護。
啟用保護牽涉到兩個物件：項目和原則，兩者都必須屬於相同的保存庫。 一旦原則與項目相關聯，備份工作流程將依定義的排程開始運作。

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>初始備份
備份排程會負責執行項目的完整初始複製，以及後續備份的增量複製。 但如果您想要在特定時間強制進行初始備份，甚至是立即開始，請使用 **Backup-AzureRmBackupItem** Cmdlet：

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> 在 PowerShell 中顯示的 StartTime 和 EndTime 欄位的時間為 UTC。 不過，當類似資訊顯示在 Azure 入口網站中時，時區會對應您的本機系統時鐘。
>
>

### <a name="monitoring-a-backup-job"></a>監視備份工作
Azure 備份中長時間執行的大部分作業都模擬成工作。 如此就很容易追蹤進度，而不需要一直開啟 Azure 入口網站。

若要取得進行中作業的最新狀態，請使用 **Get-AzureRmBackupJob** Cmdlet。

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

因為需要額外的程式碼且並非必要，所以不輪詢這些作業是否完成，而是更簡單地改用 **Wait-AzureRmBackupJob** Cmdlet。 在指令碼中使用此 Cmdlet 會暫停執行，直到工作完成或達到指定的逾時值為止。

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>還原 Azure VM
若要還原備份資料，您需要識別備份的「項目」和保存時間點資料的「復原點」。 這項資訊會提供給 Restore-AzureRmBackupItem Cmdlet，開始從保存庫將資料還原到客戶的帳戶。

### <a name="select-the-vm"></a>選取 VM
若要取得可識別正確備份項目的 PowerShell 物件，您需要從保存庫中的「容器」開始，向下深入物件階層。 若要選取代表 VM 的容器，請使用 **Get-AzureRmBackupContainer** Cmdlet，並透過管道將它傳送到 **Get-AzureRmBackupItem** Cmdlet。

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>選擇復原點
您現在可以使用 **Get-AzureRmBackupRecoveryPoint** Cmdlet，列出備份項目的所有復原點，並選擇要還原的復原點。 使用者通常會從清單中選擇最近的 *AppConsistent* 點。

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

變數 ```$rp``` 是所選取之備份項目的復原點陣列，以時間的回推順序排序 - 最近的復原點位於索引 0。 使用標準 PowerShell 陣列索引來挑選復原點。 例如： ```$rp[0]``` 將會選取最新的復原點。

### <a name="restoring-disks"></a>還原磁碟
透過 Azure 入口網站或透過 Azure PowerShell 執行還原作業，兩者之間有一項重要差異。 如果使用 PowerShell，從復原點還原磁碟及組態資訊時，還原作業會停止。 不會建立虛擬機器。

> [!WARNING]
> Restore-AzureRmBackupItem 不會建立 VM。 只會將磁碟還原到指定的儲存體帳戶。 這與 Azure 入口網站中的行為不同。
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

完成還原作業之後，可以使用 **Get-AzureRmBackupJobDetails** Cmdlet 來取得還原作業的詳細資料。 *ErrorDetails* 屬性會有重建 VM 所需的資訊。

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a>建置 VM
如果要從還原的磁碟建置 VM，您可以使用較舊的 Azure 服務管理 PowerShell Cmdlet、新的 Azure Resource Manager 範本，或甚至使用 Azure 入口網站。 在快速的範例中，我們將說明如何使用 Azure 服務管理 Cmdlet 來達到目的。

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

如需如何從還原的磁碟建置 VM 的詳細資訊，請參閱下列 Cmdlet：

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>程式碼範例
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a>1.取得作業子工作的完成狀態
若要追蹤個別子作業的完成狀態，可以使用 **Get-AzureRmBackupJobDetails** Cmdlet：

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2.建立備份作業的每日/每週報表
系統管理員通常想要知道備份作業在過去 24 小時的執行情況，以及那些備份作業的狀態。 此外，傳輸的資料量提供系統管理員一種預估其每月資料使用量的方式。 下列指令碼會從 Azure 備份服務提取原始資料，並將資訊顯示在 PowerShell 主控台上。

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
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

如果想要將製作圖表的功能加入這個報表輸出，請參閱 TechNet 部落格文章 [Charting with PowerShell (使用 PowerShell 製作圖表)](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>後續步驟
如果您偏好使用 PowerShell 來與您的 Azure 資源交流，請參閱保護 Windows Server 的 PowerShell 文章：[部署和管理 Windows Server 的備份](backup-client-automation-classic.md)。 另請參閱管理 DPM 備份的 PowerShell 文章：[部署和管理 DPM 的備份](backup-dpm-automation-classic.md)。 這兩篇文章都有適用於 Resource Manager 部署以及傳統部署的版本。
