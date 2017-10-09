---
title: "備份 SQL Server 2014 Azure 虛擬機器的 aaaAutomated |Microsoft 文件"
description: "用於在 Azure 中執行的 SQL Server 2014 Vm 說明 hello 自動備份功能。 本文是特定 tooVMs 使用 hello 資源管理員。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>SQL Server 2014 虛擬機器的自動備份 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

自動的備份會自動設定[Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM 上的所有現有和新資料庫。 這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。 自動的備份取決於 hello [SQL Server IaaS 代理程式延伸模組](virtual-machines-windows-sql-server-agent-extension.md)。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>必要條件
toouse 自動備份，請考慮下列必要條件 hello:

**作業系統**：

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**SQL Server 版本**：

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> 「自動備份」可與 SQL Server 2014 搭配運作。 如果您使用 SQL Server 2016，您可以使用自動備份 v2 tooback 資料庫。 如需詳細資訊，請參閱 [SQL Server 2016 Azure 虛擬機器的自動備份 v2](virtual-machines-windows-sql-automated-backup-v2.md)。

**資料庫組態**：

- 目標資料庫必須使用 hello 完整復原模式。 如需詳細資訊 hello 影響 hello 完整復原模式的備份，請參閱[備份在 hello 完整復原模式](https://technet.microsoft.com/library/ms190217.aspx)。
- 目標資料庫必須位於 hello 預設 SQL Server 執行個體上。 hello SQL Server IaaS 延伸模組不支援具名執行個體。

**Azure 部署模型**：

- Resource Manager

**Azure PowerShell**：

- [安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)如果您計劃 tooconfigure 使用 PowerShell 的自動化備份。

> [!NOTE]
> 自動的備份依賴 hello SQL Server IaaS 代理程式延伸模組。 目前的 SQL 虛擬機器資源庫映像預設會新增這項擴充。 如需詳細資訊，請參閱 [SQL Server IaaS 代理程式擴充](virtual-machines-windows-sql-server-agent-extension.md)。

## <a name="settings"></a>設定

hello 下表說明可以設定為自動備份的 hello 選項。 hello 實際的組態步驟，視您使用 hello Azure 入口網站或 Azure Windows PowerShell 命令而有所不同。

| 設定 | 範圍 (預設值) | 說明 |
| --- | --- | --- |
| **自動備份** | 啟用/停用 (已停用) | 針對執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM，啟用或停用自動備份。 |
| **保留期限** | 1-30 天 (30 天) | hello 天 tooretain 備份數目。 |
| **儲存體帳戶** | Azure 儲存體帳戶 | 將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。 所有備份檔案時，會在此位置 toostore 建立的容器。 hello 備份檔案命名慣例包括 hello 日期、 時間和電腦名稱。 |
| **加密** | 啟用/停用 (已停用) | 啟用或停用加密。 啟用加密時，在指定 hello 位於 hello 使用憑證 toorestore hello 備份儲存體帳戶中 hello 相同`automaticbackup`容器使用 hello 相同的命名慣例。 如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。 |
| **密碼** | 密碼文字 | 加密金鑰的密碼。 唯有啟用加密時，才需要此密碼。 順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。 |

## <a name="configuration-in-hello-portal"></a>Hello 入口網站中的組態

在佈建期間，或用於現有的 SQL Server 2014 Vm，您可以使用 hello Azure 入口網站 tooconfigure 自動備份。

### <a name="new-vms"></a>新的 VM

當您建立新的 SQL Server 2014 虛擬機器在 hello Resource Manager 部署模型時，請使用 hello Azure 入口網站 tooconfigure 自動備份。

在 hello **SQL Server 設定**刀鋒視窗中，選取**自動化備份**。 hello 下列 Azure 入口網站螢幕擷取畫面顯示 hello **SQL 自動備份**刀鋒視窗。

![在 Azure 入口網站中設定 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

針對內容，請參閱 hello 完整主題[佈建 Azure 中的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

### <a name="existing-vms"></a>現有的 VM

如果是現有的 SQL Server 虛擬機器，請選取您的 SQL Server 虛擬機器。 然後選取 hello **SQL Server 組態**區段 hello**設定**刀鋒視窗。

![現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

在 hello **SQL Server 組態**刀鋒視窗中，按一下 hello**編輯**hello 中的按鈕自動化備份 > 一節。

![設定現有 VM 的 SQL 自動備份](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

完成後，請按一下 hello **[確定]**上 hello hello 底部的按鈕**SQL Server 組態**刀鋒視窗 toosave 您的變更。

如果您要啟用自動備份 hello 第一次，Azure 會在 hello 背景設定 hello SQL Server IaaS 代理程式。 在此期間，hello Azure 入口網站可能不會顯示已設定自動備份。 等待幾分鐘的時間安裝，hello 代理程式 toobe 設定。 之後的 hello Azure 入口網站將會反映 hello 新設定。

> [!NOTE]
> 您也可以使用範本來設定「自動備份」。 如需詳細資訊，請參閱 [適用於自動備份的 Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)。

## <a name="configuration-with-powershell"></a>使用 PowerShell 進行設定

您可以使用 PowerShell tooconfigure 自動備份。 開始進行之前，您必須：

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
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

如果您的輸出顯示**啟用**設定得**False**，就會有 tooenable 自動的備份。 hello 好消息是您啟用並設定自動備份 hello 中相同的方式。 請參閱這項資訊的 hello 下一節。

> [!NOTE] 
> 如果您檢查 hello 設定進行變更後立即，很可能，您將會回到 hello 舊組態值。 等待幾分鐘的時間，並檢查 hello 設定一次 toomake 確定已套用的變更。

### <a name="configure-automated-backup"></a>設定自動備份
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

然後使用 hello**新增 AzureRmVMSqlServerAutoBackupConfig**命令 tooenable 並設定 hello Azure 儲存體帳戶中的 hello 自動備份設定 toostore 備份。 在此範例中，hello 備份設定 toobe 保留 10 天。 hello 第二個命令，**組 AzureRmVMSqlServerExtension**，更新 hello Azure VM 指定這些設定。

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。

> [!NOTE]
> 沒有其他設定**新增 AzureRmVMSqlServerAutoBackupConfig**套用只有 tooSQL Server 2016 和自動備份 v2。 SQL Server 2014 不支援下列設定的 hello: **BackupSystemDbs**， **BackupScheduleType**， **FullBackupFrequency**， **FullBackupStartHour**， **FullBackupWindowInHours**，和**LogBackupFrequencyInMinutes**。 如果您嘗試 tooconfigure SQL Server 2014 虛擬機器上的這些設定，沒有發生錯誤，但並不會套用 hello 設定。 如果您想 toouse SQL Server 2016 的虛擬機器上的這些設定，請參閱[適用於 SQL Server 2016 Azure 虛擬機器的自動備份 v2](virtual-machines-windows-sql-automated-backup-v2.md)。

tooenable 加密修改前一個指令碼 toopass hello hello **EnableEncryption**參數 hello 的密碼 （安全字串） 以及**CertificatePassword**參數。 hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>後續步驟

自動備份會在 Azure VM 上設定受管理備份。 因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。

您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](virtual-machines-windows-sql-backup-recovery.md)。

如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](virtual-machines-windows-sql-server-agent-extension.md)。

如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

