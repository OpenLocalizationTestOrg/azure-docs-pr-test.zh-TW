---
title: "aaaAutomated 備份 v2 適用於 SQL Server 2016 Azure 虛擬機器 |Microsoft 文件"
description: "用於在 Azure 中執行的 SQL Server 2016 Vm 說明 hello 自動備份功能。 本文是特定 tooVMs 使用 hello 資源管理員。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>SQL Server 2016 Azure 虛擬機器的自動備份 v2 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

會自動設定自動的備份 v2 [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2016 Standard、 Enterprise 或 Developer 版本的 Azure VM 上的所有現有和新資料庫。 這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。 自動化的備份 v2 取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>必要條件
自動備份 v2 toouse 檢閱 hello 下列必要條件：

**作業系統**：

- Windows Server 2012 R2
- Windows Server 2016

**SQL Server 版本**：

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> 「自動備份 v2」可與 SQL Server 2016 搭配運作。 如果您使用 SQL Server 2014，您可以使用自動備份 v1 tooback 資料庫。 如需詳細資訊，請參閱 [SQL Server 2014 Azure 虛擬機器的自動備份](virtual-machines-windows-sql-automated-backup.md)。

**資料庫組態**：

- 目標資料庫必須使用 hello 完整復原模式。 如需詳細資訊 hello 影響 hello 完整復原模式的備份，請參閱[備份在 hello 完整復原模式](https://technet.microsoft.com/library/ms190217.aspx)。
- 系統資料庫沒有 toouse 完整復原模式。 不過，如果您需要記錄備份 toobe 所花費的模型或 MSDB，您必須使用完整復原模式。
- 目標資料庫必須位於 hello 預設 SQL Server 執行個體上。 hello SQL Server IaaS 延伸模組不支援具名執行個體。

**Azure 部署模型**：

- Resource Manager

> [!NOTE]
> 自動的備份依賴 hello **SQL Server IaaS 代理程式延伸模組**。 目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。 如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。

## <a name="settings"></a>設定
hello 下表說明可以設定自動備份 v2 的 hello 選項。 hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。

### <a name="basic-settings"></a>基本設定

| 設定 | 範圍 (預設值) | 說明 |
| --- | --- | --- |
| **自動備份** | 啟用/停用 (已停用) | 針對執行 SQL Server 2016 Standard 或 Enterprise 的 Azure VM，啟用或停用「自動備份」。 |
| **保留期限** | 1-30 天 (30 天) | hello 天 tooretain 備份數目。 |
| **儲存體帳戶** | Azure 儲存體帳戶 | 將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。 所有備份檔案時，會在此位置 toostore 建立的容器。 hello 備份檔案命名慣例包括 hello 日期、 時間和資料庫的 GUID。 |
| **加密** |啟用/停用 (已停用) | 啟用或停用加密。 啟用加密時，在指定 hello 位於 hello 使用憑證 toorestore hello 備份儲存體帳戶中 hello 相同**automaticbackup**容器使用 hello 相同的命名慣例。 如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。 |
| **密碼** |密碼文字 | 加密金鑰的密碼。 唯有啟用加密時，才需要此密碼。 順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。 |

### <a name="advanced-settings"></a>進階設定

| 設定 | 範圍 (預設值) | 說明 |
| --- | --- | --- |
| **系統資料庫備份** | 啟用/停用 (已停用) | 啟用時，這項功能也會備份 hello 系統資料庫： Master、 MSDB 和模型。 Hello MSDB 和 Model 資料庫，確認它們會在完整復原模式下，是否您想要採取的記錄檔備份 toobe。 針對 Master 是一律不進行記錄備份。 而針對 TempDB 則不進行任何備份。 |
| **備份排程** | 手動/自動化 (自動化) | 根據預設，hello 備份排程將會自動判斷根據 hello 記錄成長。 手動備份的排程可讓您備份 hello 使用者 toospecify hello 時間視窗。 在此情況下，備份將只會發生在 hello 指定頻率，且在 hello 期間的某一天的時間間隔。 |
| **完整備份頻率** | 每天/每週 | 完整備份的頻率。 在這兩種情況下，完整備份會開始在 hello 下一個排定的時間間隔。 選取 [每週] 時，備份可以跨多天，直到所有資料庫都已順利備份為止。 |
| **完整備份開始時間** | 00:00 – 23:00 (01:00) | 可進行完整備份的特定一天開始時間期間。 |
| **完整備份時間範圍** | 1 – 23 小時 (1 小時) | Hello 的某一天的完整備份便可以執行的時間間隔的持續時間。 |
| **記錄備份頻率** | 5 – 60 分鐘 (60 分鐘) | 記錄備份的頻率。 |

## <a name="understanding-full-backup-frequency"></a>了解完整備份頻率
它會每日及每週完整備份的重要 toounderstand hello 差異。 為此，我們將逐步解說兩個範例案例。

### <a name="scenario-1-weekly-backups"></a>案例 1：每週備份
您有一部包含一些非常大型資料庫的 SQL Server VM。

在星期一，您可以啟用自動備份 v2 以 hello 下列設定：

- 備份排程：**自動**
- 完整備份頻率：**每週**
- 完整備份開始時間：**01:00**
- 完整備份時間範圍：**1 小時**

這表示該 hello 下一個可用備份時段星期二上午 1 小時 1。 到該時間，「自動備份」將開始逐一備份您的資料庫。 在此案例中，您的資料庫已經很大完整備份將會完成的第一個幾資料庫 hello。 不過，在一小時後不是所有的 hello 資料庫備份。

當發生這種情況時，就會開始自動備份，備份 hello 剩餘的資料庫 hello 隔天，星期三上午 1 小時 1。 如果並非所有的資料庫已在該時間備份，將會嘗試再次相同 hello hello 在隔天的時間。 這將會持續直到順利備份所有資料庫為止。

一旦再次到了星期二，「自動備份」就會重新開始再將所有資料庫都備份一遍。

此案例中會顯示自動備份只會在 hello 指定的時間視窗中，每個資料庫會備份每週的一次。 這也會顯示，有可能備份 toospan hello 中的多個天數的大小寫不可能 toocomplete 所有備份在一天。

### <a name="scenario-2-daily-backups"></a>案例 2：每天備份
您有一部包含一些非常大型資料庫的 SQL Server VM。

在星期一，您可以啟用自動備份 v2 以 hello 下列設定：

- 備份排程：手動
- 完整備份頻率：每天
- 完整備份開始時間：22:00
- 完整備份時間範圍：6 小時

這表示該 hello 下一個可用備份時段星期一下午 10 點長達 6 小時。 到該時間，「自動備份」將開始逐一備份您的資料庫。

然後，在星期二下午 10 點，將會重新開始進行所有資料庫的完整備份，持續時間為 6 小時。

> [!IMPORTANT]
> 當排定每日備份，建議您排程的所有資料庫都可以都備份此時間內寬時間視窗 tooensure。 這是最多有大量的資料 tooback hello 案例特別重要。

## <a name="configuration-in-hello-portal"></a>Hello 入口網站中的組態

您可以使用 hello Azure 入口網站 tooconfigure 自動備份 v2 期間佈建或現有的 SQL Server 2016 Vm。

### <a name="new-vms"></a>新的 VM

當您建立新的 SQL Server 2016 虛擬機器在 hello Resource Manager 部署模型時，請使用 hello Azure 入口網站 tooconfigure 自動備份 v2。 

在 hello **SQL Server 設定**刀鋒視窗中，選取**自動化備份**。 hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動備份**刀鋒視窗。

![在 Azure 入口網站中設定 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> 預設會停用「自動備份 v2」。

針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

### <a name="existing-vms"></a>現有的 VM

如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。 然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。

![現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 中的按鈕自動化備份 > 一節。

![設定現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。

如果您要啟用自動備份 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。 在此期間，hello Azure 入口網站可能不會顯示已設定自動備份。 等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。 之後的 hello Azure 入口網站將會反映 hello 新設定。

## <a name="configuration-with-powershell"></a>使用 PowerShell 進行設定

您可以使用 PowerShell tooconfigure 自動備份 v2。 開始進行之前，您必須：

- [下載並安裝最新 Azure PowerShell 的 hello](http://aka.ms/webpi-azps)。
- 開啟 Windows PowerShell 並將它與您的帳戶建立關聯。 您可以在 hello hello 步驟[設定您的訂用帳戶](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription)hello 佈建主題的章節。

### <a name="install-hello-sql-iaas-extension"></a>安裝 hello SQL IaaS 延伸模組
如果您佈建 SQL Server 虛擬機器從 hello Azure 入口網站時，應該已安裝 hello SQL Server IaaS 延伸模組。 您可以判斷是否它藉由呼叫安裝程式 vm **Get AzureRmVM**命令，並檢查 hello**延伸**屬性。

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

如果已安裝 hello SQL Server IaaS 代理程式延伸模組，您應該會看到它列為 「 SqlIaaSAgent"或"SQLIaaSExtension"。 **ProvisioningState** hello 延伸模組也應該顯示 「 成功 」。 

如果未安裝或無法 toobe 佈建，您可以使用下列命令的 hello 來進行安裝。 在加法 toohello VM 名稱和資源群組中，您也必須指定 hello 區域 (**$region**) 中，位於您的 VM。

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a> 確認目前的設定
如果您在佈建期間啟用自動的備份，您可以使用 PowerShell toocheck 您目前的設定。 執行 hello **Get AzureRmVMSqlServerExtension**命令，並檢查 hello **AutoBackupSettings**屬性：

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

您應該取得類似 toohello 下列輸出：

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

如果您的輸出顯示**啟用**設定得**False**，就會有 tooenable 自動的備份。 hello 好消息是您啟用並設定自動備份 hello 中相同的方式。 請參閱這項資訊的 hello 下一節。

> [!NOTE] 
> 如果您檢查 hello 設定進行變更後立即，很可能，您將會回到 hello 舊組態值。 等待幾分鐘的時間，並檢查 hello 設定一次 toomake 確定已套用的變更。

### <a name="configure-automated-backup-v2"></a>設定自動備份 v2
您可以使用 PowerShell tooenable 自動備份，以及 toomodify 其組態和行為在任何時間。 

首先，選取或建立 hello 的儲存體帳戶的備份檔案。 hello 下列指令碼會選取儲存體帳戶，或建立如果不存在。

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> 「自動備份」不支援將備份存放在進階儲存體中，但是可以從使用「進階儲存體」的 VM 磁碟進行備份。

然後使用 hello**新增 AzureRmVMSqlServerAutoBackupConfig**命令 tooenable 和 hello Azure 儲存體帳戶中設定自動備份 v2 hello 設定 toostore 備份。 在此範例中，hello 備份設定 toobe 保留 10 天。 系統資料庫備份已啟用。 完整備份是排定為每週執行，時間範圍是從 20:00 開始並持續 2 小時。 記錄備份是排定為每 30 分鐘執行一次。 hello 第二個命令，**組 AzureRmVMSqlServerExtension**，更新 hello Azure VM 指定這些設定。

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。 

tooenable 加密修改前一個指令碼 toopass hello hello **EnableEncryption**參數 hello 的密碼 （安全字串） 以及**CertificatePassword**參數。 hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

您的設定會套用，tooconfirm[確認 hello 自動備份組態](#verifysettings)。

### <a name="disable-automated-backup"></a>停用自動備份
自動備份，執行相同指令碼沒有 hello 的 hello toodisable **-啟用**參數 toohello**新增 AzureRmVMSqlServerAutoBackupConfig**命令。 hello 缺乏 hello **-啟用**參數訊號 hello 命令 toodisable hello 功能。 如同安裝時，可能需要幾分鐘的時間 toodisable 自動備份。

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>範例指令碼
hello 下列指令碼提供一組變數，您可以自訂 tooenable 及設定自動備份您的 VM。 在您的情況下，您可能需要 toocustomize hello 指令碼，根據您的需求。 例如，您會有 toomake 變更，如果您想 toodisable hello 系統資料庫備份，或啟用加密。

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>後續步驟
「自動備份 v2」會在 Azure VM 上設定 Managed Backup。 因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。

您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](virtual-machines-windows-sql-backup-recovery.md)。

如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。

如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

