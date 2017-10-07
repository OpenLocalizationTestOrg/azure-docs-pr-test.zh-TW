---
title: "aaaAutomated 備份適用於 SQL Server 虛擬機器 （傳統） |Microsoft 文件"
description: "說明執行 Azure 虛擬機器中使用資源管理員的 SQL Server 的 hello 自動備份功能。 "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Azure 虛擬機器中的 SQL Server 自動備份 (傳統)
> [!div class="op_single_selector"]
> * [資源管理員](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [傳統](../classic/sql-automated-backup.md)
> 
> 

自動的備份會自動設定[Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM 上的所有現有和新資料庫。 這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。 自動的備份取決於 hello [SQL Server IaaS 代理程式延伸模組](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 請參閱這篇文章，tooview hello 資源管理員版本[自動備份的 SQL Server 在 Azure 虛擬機器資源管理員](../sql/virtual-machines-windows-sql-automated-backup.md)。

## <a name="prerequisites"></a>必要條件
toouse 自動備份，請考慮下列必要條件 hello:

**作業系統**：

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server 版本**：

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> 尚未支援 SQL Server 2016 進行「自動備份」。
> 
> 

**資料庫組態**：

* 目標資料庫必須使用 hello 完整復原模式。

**Azure PowerShell**：

* [安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。

**SQL Server IaaS 擴充功能**：

* [安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。

## <a name="settings"></a>設定
hello 下表說明可以設定為自動備份的 hello 選項。 對於傳統的 Vm，您必須使用 PowerShell tooconfigure 這些設定。

| 設定 | 範圍 (預設值) | 說明 |
| --- | --- | --- |
| **自動備份** |啟用/停用 (已停用) |針對執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM，啟用或停用自動備份。 |
| **保留期限** |1-30 天 (30 天) |hello 天 tooretain 備份數目。 |
| **儲存體帳戶** |Azure 儲存體帳戶 （建立 hello 指定 VM hello 儲存體帳戶） |將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。 所有備份檔案時，會在此位置 toostore 建立的容器。 hello 備份檔案命名慣例包括 hello 日期、 時間和電腦名稱。 |
| **加密** |啟用/停用 (已停用) |啟用或停用加密。 使用的 toorestore hello 備份位於 hello hello 憑證啟用加密時，指定儲存體帳戶中 hello 相同 automaticbackup 容器使用 hello 相同的命名慣例。 如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。 |
| **密碼** |密碼文字 (無) |加密金鑰的密碼。 唯有啟用加密時，才需要此密碼。 順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。 | **備份系統資料庫** | 啟用/停用 (已停用) | 完整備份 Master、Model 及 MSDB |
| **設定備份排程** | 手動/自動化 (自動化) | 選取**自動化**tooautomatically 採用完整和記錄檔記錄成長為基礎的備份。 選取**手動**toospecify hello 排程完整和記錄備份。 |

## <a name="configuration-with-powershell"></a>使用 PowerShell 進行設定
下列 PowerShell 範例 hello，在現有的 SQL Server 2014 VM 設定自動備份。 hello**新增 AzureVMSqlServerAutoBackupConfig**命令會設定 hello 自動備份設定 toostore 備份 hello hello $storageaccount 變數所指定的 Azure 儲存體帳戶。 這些備份將會保留 10 天。 hello**組 AzureVMSqlServerExtension**命令更新 hello Azure VM 指定這些設定。

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。

tooenable 加密 hello CertificatePassword 參數修改 hello 前一個指令碼 toopass hello EnableEncryption 參數以及密碼 （安全字串）。 hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable 自動備份，執行相同指令碼沒有 hello 的 hello **-啟用**參數 toohello**新增 AzureVMSqlServerAutoBackupConfig**。 如同安裝時，可能需要幾分鐘的時間 toodisable 自動備份。

> [!NOTE]
> 停用及解除安裝 hello SQL Server IaaS 代理程式不會移除先前設定的 hello 受管理備份設定。 您應該停用或解除安裝 SQL Server IaaS Agent hello 之前，停用自動備份。
> 
> 

## <a name="next-steps"></a>後續步驟
自動備份會在 Azure VM 上設定受管理備份。 因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。

您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。

如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。

如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

