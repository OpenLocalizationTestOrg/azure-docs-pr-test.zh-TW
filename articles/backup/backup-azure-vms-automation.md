---
title: "aaaDeploy 和資源管理員部署的 vm 使用 PowerShell 管理備份 |Microsoft 文件"
description: "使用 PowerShell toodeploy 及管理資源管理員部署的 Vm 在 Azure 中的備份"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>使用虛擬機器 AzureRM.RecoveryServices.Backup cmdlet tooback
> [!div class="op_single_selector"]
> * [資源管理員](backup-azure-vms-automation.md)
> * [傳統](backup-azure-vms-classic-automation.md)
>
>

本文章將示範如何設定 toouse Azure PowerShell cmdlet tooback 和復原 Azure 虛擬機器 (VM) 從 復原服務保存庫。 復原服務保存庫是 Azure 資源管理員資源，而且是使用的 tooprotect 資料和 Azure 備份和 Azure Site Recovery 服務中的資產。 您可以使用 Azure Service Manager 部署的 Vm，復原服務保存庫 tooprotect 和 Azure Resource Manager 部署的 Vm。

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文適用於使用 hello 資源管理員模型所建立的 vm。
>
>

這篇文章會引導您逐步使用 PowerShell tooprotect VM，並還原資料從復原點。

## <a name="concepts"></a>概念
如果您不熟悉 hello Azure Backup 服務，hello 服務的概觀，請參閱[什麼是 Azure 備份？](backup-introduction-to-azure-backup.md) 開始之前，請確定您涵蓋關於 Azure backup 的 hello 所需必要條件 toowork hello essentials 和 hello hello 目前 VM 的備份解決方案的限制。

toouse PowerShell 實際上，它是必要的 toounderstand hello 階層的物件，並從中 toostart。

![復原服務物件階層](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet 參考資料，請參閱 hello [Azure 備份-Recovery Services 指令程式](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup)hello Azure 文件庫中。

## <a name="setup-and-registration"></a>設定和註冊
toobegin:

1. [下載最新版的 PowerShell 中 hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello 所需的最低版本是： 1.4.0)
2. 輸入下列命令的 hello 尋找可用的 hello Azure 備份的 PowerShell cmdlet:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


可以使用 PowerShell 自動化 hello 下列工作：

* 建立復原服務保存庫
* 備份 Azure VM
* 觸發備份作業
* 監視備份作業
* 還原 Azure VM

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
hello 步驟會引導您完成建立復原服務保存庫。 復原服務保存庫不同於備份保存庫。

1. 如果您使用 Azure Backup hello 第一次，您必須使用 hello **[暫存器 AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure 復原服務提供者與您的訂用帳戶。

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. hello 復原服務保存庫是 「 資源管理員資源，因此您需要 tooplace 它資源群組內。 您可以使用現有的資源群組，或建立資源群組以 hello **[新增 AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet。 建立資源群組時，指定 hello 名稱和位置 hello 資源群組。  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. 使用 hello **[新增 AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate hello 復原服務保存庫。 請務必 toospecify hello hello 保存庫相同的位置，所用的 hello 資源群組。

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. 指定儲存體備援 toouse; hello 類型您可以使用[本機備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage)或[地理備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。 hello 下列範例顯示 hello testvault-BackupStorageRedundancy 選項設定 tooGeoRedundant。

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > 許多 Azure Backup cmdlet 需要 hello 復原服務保存庫的物件做為輸入。 基於這個理由，它是方便 toostore hello 備份復原服務保存庫在變數中。
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>檢視訂用帳戶中的 hello 保存庫
使用 **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello 份 hello 目前訂用帳戶中所有的保存庫。 您可以使用這個命令 toocheck，建立新的保存庫或 toosee hello hello 訂用帳戶中可用的保存庫。

執行所有的保存庫 hello 命令，Get-AzureRmRecoveryServicesVault tooview hello 訂用帳戶中。 hello 下列範例顯示 hello 資訊顯示每個保存庫。

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


## <a name="back-up-azure-vms"></a>備份 Azure VM
使用 復原服務保存庫 tooprotect 虛擬機器。 在您套用 hello 保護之前，設定 hello 保存庫內容 （hello 類型 hello 保存庫中受保護的資料），並確認 hello 保護原則。 hello 保護原則是 hello 排程 hello 備份工作執行時，每個備份快照集的保留時間長度。

### <a name="set-vault-context"></a>設定保存庫內容
再啟用 VM 上的保護，請使用**[組 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello 保存庫的內容。 一旦設定 hello 保存庫的內容之後，它會套用 tooall 後續的 cmdlet。 hello 下列範例會設定 hello hello 保存庫，保存庫內容*testvault*。

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>建立保護原則
當您建立復原服務保存庫時，它會隨附預設的保護和保留原則。 hello 預設保護原則會觸發備份工作在指定時間的每一天。 hello 預設保留原則會保留 30 天 hello 每日復原點。 您可以使用 hello 預設原則 tooquickly 保護您的 VM，然後編輯 hello 原則，稍後可以使用各種不同詳細資料。

使用 **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview hello 保護原則 hello 保存庫中的。 您可以使用這個指令程式 tooget 特定原則或工作負載類型相關聯的 tooview hello 原則。 下列範例中的 hello 取得工作負載類型，AzureVM 原則。

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> 在 PowerShell 中的 hello BackupTime 欄位的 hello 時區為 UTC。 不過，當 hello 備份時間所示為 hello Azure 入口網站，hello 時調整的 tooyour 本地時區。
>
>

備份保護原則至少與一個保留原則相關聯。 保留原則會定義復原點在被刪除之前要保留多久。 使用 **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello 預設保留原則。  同樣地，您可以使用 **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello 預設按排程時間原則。 hello **[新增 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet 會建立保留的備份原則資訊的 PowerShell 物件。 hello 排程和保留原則 物件就會當做輸入 toohello **[新增 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet。 hello 下列範例會儲存 hello 按排程時間原則和 hello 保留原則在變數中。 hello 範例會使用這些變數 toodefine hello 參數，當建立保護原則， *NewPolicy*。

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>啟用保護。
一旦您已經定義 hello 備份的保護原則，您仍然必須啟用 hello 原則項目。 使用**[啟用 AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable 保護。 啟用保護需要兩個物件-hello 項目和 hello 原則。 一旦 hello 原則已與 hello 保存庫相關聯，就會在 hello 原則排程所定義的 hello 時間觸發 hello 備份工作流程。

下列範例啟用項目的保護 hello，V2VM，使用 hello 原則，NewPolicy hello。 在非加密的資源管理員 Vm 上 tooenable hello 保護

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello 保護加密 （使用 BEK 和 KEK 加密） 的 Vm，您必須 toogive hello Azure 備份服務的權限 tooread 金鑰和秘密金鑰保存庫中。

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello 保護加密 （僅限使用 BEK 加密） 的 Vm，您必須 toogive hello Azure 備份服務的權限 tooread 秘密金鑰保存庫中。

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> 如果您使用 hello Azure 政府雲端，然後用於 hello 值 ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello 參數**-ServicePrincipalName**中[Set-azurermkeyvaultaccesspolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.
>
>

若為傳統 VM

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>修改保護原則
toomodify hello 保護原則，使用[組 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy 或 RetentionPolicy 物件。

hello 下例 hello 復原點保留 too365 天數。

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>觸發備份
您可以使用**[備份 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger 備份工作。 如果它是 hello 初始備份，則完整備份。 後續的備份會採用增量複本。 要確定 toouse **[組 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** 觸發 hello 備份作業之前 tooset hello 保存庫的內容。 下列範例中的 hello 假設設定保存庫的內容。

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> 在 PowerShell 中的 hello StartTime 和 EndTime 欄位的 hello 時區為 UTC。 不過，當 hello 時間所示為 hello Azure 入口網站，hello 時調整的 tooyour 本地時區。
>
>

## <a name="monitoring-a-backup-job"></a>監視備份工作
您可以監視長時間執行作業，例如備份作業，而不使用 hello Azure 入口網站。 為進行中工作時，使用 hello tooget hello 狀態 **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet。 此 cmdlet 會取得特定的保存庫的 hello 備份工作和 hello 保存庫的內容中指定該保存庫。 hello 下列範例取得 hello 的陣列，進行中工作的狀態，並儲存 hello 狀態 hello $joblist 變數中。

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

而不是輪詢-這是不需要額外的程式碼-完成這些作業使用 hello **[等候 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet。 這個指令程式暫停 hello 執行，直到 hello 作業完成或 hello 可讓您指定逾時值為止。

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>還原 Azure VM
沒有 hello 還原的 VM 使用 hello Azure 入口網站，並還原 VM，使用 PowerShell 的主要差異。 使用 PowerShell，hello 還原作業已完成，一旦建立 hello 磁碟和組態資訊從 hello 復原點。

> [!NOTE]
> hello 還原作業不會建立虛擬機器。
>
>

toocreate 從虛擬機器磁碟，請參閱 hello 區段[從預存的磁碟建立 hello VM](backup-azure-vms-automation.md#create-a-vm-from-stored-disks)。 hello Azure VM 的基本步驟 toorestore 如下：

* 選取 hello VM
* 選擇復原點
* 還原 hello 磁碟
* 從預存的磁碟建立 hello VM

hello 下圖顯示從 hello RecoveryServicesVault 向 toohello BackupRecoveryPoint hello 物件階層架構。

![顯示 BackupContainer 的復原服務物件階層](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore 備份的資料，找出 hello 備份項目和 hello 保存 hello 時間點資料的復原點。 使用 hello **[還原 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 資料 hello 從保存庫 toohello 客戶的帳戶。

### <a name="select-hello-vm"></a>選取 hello VM
tooget hello PowerShell 物件，可識別 hello 右備份項目、 啟動 hello 保存庫中的 hello 容器和由上至下 hello 物件階層架構。 代表 hello VM，使用 hello tooselect hello 容器 **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet 並使用管線傳送該 toohello  **[Get AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet。

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>選擇復原點
使用 hello  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  cmdlet toolist hello 備份項目的所有復原都點。 然後選擇 hello 復原點 toorestore。 如果您不確定哪一個復原點 toouse，是很好的作法 toochoose hello 最近 RecoveryPointType = AppConsistent hello 清單中的點。

在下列指令碼的 hello，hello 變數， **$rp**，是陣列的復原點，針對 hello 選取備份項目，從 hello 過去七天內。 hello 陣列是以反向順序排序的時間與 hello 最新復原點位於索引 0。 使用標準的 PowerShell 陣列索引 toopick hello 復原點。 在 hello 範例 $rp [0] 選取 hello 最新的復原點。

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>還原 hello 磁碟
使用 hello **[還原 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 備份項目資料和設定 tooa 復原點。 一旦您已識別復原點，使用它做 hello 值為 hello **New-recoverypoint**參數。 Hello 先前的範例程式碼**$rp [0]**已 hello 復原點 toouse。 在下列範例程式碼，hello **$rp [0]**是 hello 復原點 toouse 還原 hello 磁碟。

toorestore hello 磁碟和組態資訊：

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

使用 hello **[等候 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  hello 還原作業 toocomplete 的 cmdlet toowait。

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Hello 還原作業完成後，請使用 hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget hello 詳細資料的 hello 還原作業。 hello JobDetails 屬性有 hello 資訊所需的 toorebuild hello VM。

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

一旦還原 hello 磁碟時，請前往下一個區段 toocreate hello toohello VM。

## <a name="create-a-vm-from-restored-disks"></a>從還原的磁碟建立 VM
您已還原 hello 磁碟之後，使用這些步驟 toocreate，並設定從磁碟 hello 虛擬機器。

> [!NOTE]
> toocreate 加密從還原的磁碟 Vm，您的 Azure 角色必須具有的權限 tooperform hello 動作， **Microsoft.KeyVault/vaults/deploy/action**。 如果您的角色並沒有此權限，請使用此動作來建立自訂角色。 如需詳細資訊，請參閱 [Azure RBAC 中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。
>
>

1. 查詢 hello 還原 hello 工作詳細資料的磁碟內容。

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. 設定 hello Azure 儲存體的內容，並還原 hello JSON 組態檔。

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. 使用 hello JSON 組態檔 toocreate hello VM 組態。

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. 附加 hello OS 磁碟和資料磁碟。 根據您的 Vm 的 hello 組態，請按一下 hello 相關連結 tooview 個別 cmdlet: 
    - [非管理、 未加密的 Vm](#non-managed-non-encrypted-vms)
    - [非管理、 加密 Vm (只有 BEK)](#non-managed-encrypted-vms-bek-only)
    - [非管理、 加密的 Vm （BEK 和 KEK）](#non-managed-encrypted-vms-bek-and-kek)
    - [受管理、 未加密的 Vm](#managed-non-encrypted-vms)
    - [受管理的加密 Vm （BEK 和 KEK）](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>未受管理、未加密的 VM

    下列範例針對未受管理、 未加密的 Vm 使用 hello。

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>未受管理的已加密 VM (僅限 BEK)

    （僅限使用 BEK 加密） 的 Vm 未受管理的加密，您需要 toorestore hello toohello 秘密金鑰保存庫之前，您可以將附加磁碟。 如需詳細資訊，請參閱 hello 文章[從 Azure Backup 復原點還原加密的虛擬機器](backup-azure-restore-key-secret.md)。 hello 下列範例顯示如何 tooattach OS 和資料磁碟加密 Vm。

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>未受管理的已加密 VM (BEK 和 KEK)

    對於未受管理的加密 Vm （使用 BEK 和 KEK 加密），您需要 toorestore hello 金鑰和秘密 toohello 金鑰保存庫之前，您可以將附加磁碟。 如需詳細資訊，請參閱 hello 文章[從 Azure Backup 復原點還原加密的虛擬機器](backup-azure-restore-key-secret.md)。 hello 下列範例顯示如何 tooattach OS 和資料磁碟加密 Vm。

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>受管理、未加密的 VM

    對於受管理的非加密的 Vm，您將需要從 blob 儲存體，toocreate 管理磁碟，然後將附加 hello 磁碟。 深入資訊，請參閱 hello 文章[附加資料磁碟 tooa Windows VM 使用 PowerShell](../virtual-machines/windows/attach-disk-ps.md)。 hello 下列程式碼範例顯示如何 tooattach hello 的受管理的非加密 Vm 的資料磁碟。

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>受管理的已加密 VM (BEK 和 KEK)

    對於受管理的加密 Vm （使用 BEK 和 KEK 加密），您將需要從 blob 儲存體，toocreate 管理磁碟，然後將附加 hello 磁碟。 深入資訊，請參閱 hello 文章[附加資料磁碟 tooa Windows VM 使用 PowerShell](../virtual-machines/windows/attach-disk-ps.md)。 hello 下列範例程式碼示範如何 tooattach hello 的受管理的加密 Vm 的資料磁碟。

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. 設定 hello 網路設定。

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. 建立 hello 虛擬機器。

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>後續步驟
如果您偏好 toouse PowerShell tooengage 與您的 Azure 資源，請參閱 hello PowerShell 文件：[部署和管理適用於 Windows Server 的備份](backup-client-automation.md)。 如果您管理 DPM 備份，請參閱 hello 文章[部署和管理 DPM 的備份](backup-dpm-automation.md)。 這兩篇文章都有適用於 Resource Manager 部署和傳統部署的版本。  
