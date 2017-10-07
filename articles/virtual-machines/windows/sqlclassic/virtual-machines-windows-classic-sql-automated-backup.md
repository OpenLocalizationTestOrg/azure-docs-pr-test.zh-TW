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
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="002e1-103">Azure 虛擬機器中的 SQL Server 自動備份 (傳統)</span><span class="sxs-lookup"><span data-stu-id="002e1-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="002e1-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="002e1-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="002e1-105">傳統</span><span class="sxs-lookup"><span data-stu-id="002e1-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="002e1-106">自動的備份會自動設定[Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM 上的所有現有和新資料庫。</span><span class="sxs-lookup"><span data-stu-id="002e1-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="002e1-107">這可讓您利用持久 Azure blob 儲存體的 tooconfigure 一般資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="002e1-108">自動的備份取決於 hello [SQL Server IaaS 代理程式延伸模組](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="002e1-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="002e1-109">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="002e1-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="002e1-110">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="002e1-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="002e1-111">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="002e1-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="002e1-112">請參閱這篇文章，tooview hello 資源管理員版本[自動備份的 SQL Server 在 Azure 虛擬機器資源管理員](../sql/virtual-machines-windows-sql-automated-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="002e1-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="002e1-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="002e1-113">Prerequisites</span></span>
<span data-ttu-id="002e1-114">toouse 自動備份，請考慮下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="002e1-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="002e1-115">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="002e1-115">**Operating System**:</span></span>

* <span data-ttu-id="002e1-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="002e1-116">Windows Server 2012</span></span>
* <span data-ttu-id="002e1-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="002e1-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="002e1-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="002e1-118">Windows Server 2016</span></span>

<span data-ttu-id="002e1-119">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="002e1-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="002e1-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="002e1-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="002e1-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="002e1-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="002e1-122">尚未支援 SQL Server 2016 進行「自動備份」。</span><span class="sxs-lookup"><span data-stu-id="002e1-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="002e1-123">**資料庫組態**：</span><span class="sxs-lookup"><span data-stu-id="002e1-123">**Database configuration**:</span></span>

* <span data-ttu-id="002e1-124">目標資料庫必須使用 hello 完整復原模式。</span><span class="sxs-lookup"><span data-stu-id="002e1-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="002e1-125">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="002e1-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="002e1-126">[安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="002e1-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="002e1-127">**SQL Server IaaS 擴充功能**：</span><span class="sxs-lookup"><span data-stu-id="002e1-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="002e1-128">[安裝 SQL Server IaaS 延伸模組 hello](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="002e1-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="002e1-129">設定</span><span class="sxs-lookup"><span data-stu-id="002e1-129">Settings</span></span>
<span data-ttu-id="002e1-130">hello 下表說明可以設定為自動備份的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="002e1-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="002e1-131">對於傳統的 Vm，您必須使用 PowerShell tooconfigure 這些設定。</span><span class="sxs-lookup"><span data-stu-id="002e1-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="002e1-132">設定</span><span class="sxs-lookup"><span data-stu-id="002e1-132">Setting</span></span> | <span data-ttu-id="002e1-133">範圍 (預設值)</span><span class="sxs-lookup"><span data-stu-id="002e1-133">Range (Default)</span></span> | <span data-ttu-id="002e1-134">說明</span><span class="sxs-lookup"><span data-stu-id="002e1-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="002e1-135">**自動備份**</span><span class="sxs-lookup"><span data-stu-id="002e1-135">**Automated Backup**</span></span> |<span data-ttu-id="002e1-136">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="002e1-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="002e1-137">針對執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM，啟用或停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="002e1-138">**保留期限**</span><span class="sxs-lookup"><span data-stu-id="002e1-138">**Retention Period**</span></span> |<span data-ttu-id="002e1-139">1-30 天 (30 天)</span><span class="sxs-lookup"><span data-stu-id="002e1-139">1-30 days (30 days)</span></span> |<span data-ttu-id="002e1-140">hello 天 tooretain 備份數目。</span><span class="sxs-lookup"><span data-stu-id="002e1-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="002e1-141">**儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="002e1-141">**Storage Account**</span></span> |<span data-ttu-id="002e1-142">Azure 儲存體帳戶 （建立 hello 指定 VM hello 儲存體帳戶）</span><span class="sxs-lookup"><span data-stu-id="002e1-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="002e1-143">將自動備份檔案儲存在 blob 儲存體的 Azure 儲存體帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="002e1-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="002e1-144">所有備份檔案時，會在此位置 toostore 建立的容器。</span><span class="sxs-lookup"><span data-stu-id="002e1-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="002e1-145">hello 備份檔案命名慣例包括 hello 日期、 時間和電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="002e1-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="002e1-146">**加密**</span><span class="sxs-lookup"><span data-stu-id="002e1-146">**Encryption**</span></span> |<span data-ttu-id="002e1-147">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="002e1-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="002e1-148">啟用或停用加密。</span><span class="sxs-lookup"><span data-stu-id="002e1-148">Enables or disables encryption.</span></span> <span data-ttu-id="002e1-149">使用的 toorestore hello 備份位於 hello hello 憑證啟用加密時，指定儲存體帳戶中 hello 相同 automaticbackup 容器使用 hello 相同的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="002e1-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="002e1-150">如果 hello 密碼變更，與該密碼，產生新的憑證，但是 hello 舊的憑證會保留 toorestore 先前的備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="002e1-151">**密碼**</span><span class="sxs-lookup"><span data-stu-id="002e1-151">**Password**</span></span> |<span data-ttu-id="002e1-152">密碼文字 (無)</span><span class="sxs-lookup"><span data-stu-id="002e1-152">Password text (None)</span></span> |<span data-ttu-id="002e1-153">加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="002e1-153">A password for encryption keys.</span></span> <span data-ttu-id="002e1-154">唯有啟用加密時，才需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="002e1-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="002e1-155">順序 toorestore 中加密的備份，您必須擁有 hello 正確的密碼及相關的憑證所使用的 hello hello 備份執行的時間。</span><span class="sxs-lookup"><span data-stu-id="002e1-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="002e1-156">**備份系統資料庫**</span><span class="sxs-lookup"><span data-stu-id="002e1-156">**Backup system databases**</span></span> | <span data-ttu-id="002e1-157">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="002e1-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="002e1-158">完整備份 Master、Model 及 MSDB</span><span class="sxs-lookup"><span data-stu-id="002e1-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="002e1-159">**設定備份排程**</span><span class="sxs-lookup"><span data-stu-id="002e1-159">**Configure backup schedule**</span></span> | <span data-ttu-id="002e1-160">手動/自動化 (自動化)</span><span class="sxs-lookup"><span data-stu-id="002e1-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="002e1-161">選取**自動化**tooautomatically 採用完整和記錄檔記錄成長為基礎的備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="002e1-162">選取**手動**toospecify hello 排程完整和記錄備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="002e1-163">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="002e1-163">Configuration with PowerShell</span></span>
<span data-ttu-id="002e1-164">下列 PowerShell 範例 hello，在現有的 SQL Server 2014 VM 設定自動備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="002e1-165">hello**新增 AzureVMSqlServerAutoBackupConfig**命令會設定 hello 自動備份設定 toostore 備份 hello hello $storageaccount 變數所指定的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="002e1-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="002e1-166">這些備份將會保留 10 天。</span><span class="sxs-lookup"><span data-stu-id="002e1-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="002e1-167">hello**組 AzureVMSqlServerExtension**命令更新 hello Azure VM 指定這些設定。</span><span class="sxs-lookup"><span data-stu-id="002e1-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="002e1-168">它可能需要幾分鐘的時間 tooinstall，並設定 hello SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="002e1-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="002e1-169">tooenable 加密 hello CertificatePassword 參數修改 hello 前一個指令碼 toopass hello EnableEncryption 參數以及密碼 （安全字串）。</span><span class="sxs-lookup"><span data-stu-id="002e1-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="002e1-170">hello 下列指令碼就會啟用 hello hello 前一個範例中的自動備份設定，並新增加密。</span><span class="sxs-lookup"><span data-stu-id="002e1-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="002e1-171">toodisable 自動備份，執行相同指令碼沒有 hello 的 hello **-啟用**參數 toohello**新增 AzureVMSqlServerAutoBackupConfig**。</span><span class="sxs-lookup"><span data-stu-id="002e1-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="002e1-172">如同安裝時，可能需要幾分鐘的時間 toodisable 自動備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="002e1-173">停用及解除安裝 hello SQL Server IaaS 代理程式不會移除先前設定的 hello 受管理備份設定。</span><span class="sxs-lookup"><span data-stu-id="002e1-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="002e1-174">您應該停用或解除安裝 SQL Server IaaS Agent hello 之前，停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="002e1-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="002e1-175">Next steps</span></span>
<span data-ttu-id="002e1-176">自動備份會在 Azure VM 上設定受管理備份。</span><span class="sxs-lookup"><span data-stu-id="002e1-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="002e1-177">因此務必太[檢視 Managed Backup hello 文件](https://msdn.microsoft.com/library/dn449496.aspx)toounderstand hello 行為和影響。</span><span class="sxs-lookup"><span data-stu-id="002e1-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="002e1-178">您可以找到額外的備份和還原 Azure Vm 上的 SQL Server 的 hello 下列主題中的指導方針：[備份和還原 SQL server 在 Azure 虛擬機器](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="002e1-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="002e1-179">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="002e1-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="002e1-180">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="002e1-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

