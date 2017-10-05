---
title: "SQL Server 虛擬機器的自動備份 (傳統) | Microsoft Docs"
description: "說明在使用 Resource Manager 的 Azure 虛擬機器中執行的 SQL Server 自動備份功能。 "
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
ms.openlocfilehash: f7664291c2f45c422d52f682d08dbb67ab32b099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="7783a-103">Azure 虛擬機器中的 SQL Server 自動備份 (傳統)</span><span class="sxs-lookup"><span data-stu-id="7783a-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7783a-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="7783a-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="7783a-105">傳統</span><span class="sxs-lookup"><span data-stu-id="7783a-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="7783a-106">自動備份會針對執行 SQL Server 2014 Standard 或 Enterprise 之 Azure VM 上所有現存和新的資料庫，自動設定 [Managed Backup 到 Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="7783a-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="7783a-107">這可讓您設定採用持久性 Azure Blob 儲存體的一般資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="7783a-108">自動備份相依於 [SQL Server IaaS 代理程式擴充](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7783a-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7783a-109">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="7783a-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7783a-110">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="7783a-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7783a-111">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="7783a-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7783a-112">若要檢視這篇文章的 Resource Manager 版本，請參閱 [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md) (Azure 虛擬機器的 SQL Server 自動備份 (Resource Manager))。</span><span class="sxs-lookup"><span data-stu-id="7783a-112">To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7783a-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7783a-113">Prerequisites</span></span>
<span data-ttu-id="7783a-114">若要使用自動備份，請考慮下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="7783a-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="7783a-115">**作業系統**：</span><span class="sxs-lookup"><span data-stu-id="7783a-115">**Operating System**:</span></span>

* <span data-ttu-id="7783a-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7783a-116">Windows Server 2012</span></span>
* <span data-ttu-id="7783a-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7783a-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="7783a-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7783a-118">Windows Server 2016</span></span>

<span data-ttu-id="7783a-119">**SQL Server 版本**：</span><span class="sxs-lookup"><span data-stu-id="7783a-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="7783a-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="7783a-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="7783a-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="7783a-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="7783a-122">尚未支援 SQL Server 2016 進行「自動備份」。</span><span class="sxs-lookup"><span data-stu-id="7783a-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="7783a-123">**資料庫組態**：</span><span class="sxs-lookup"><span data-stu-id="7783a-123">**Database configuration**:</span></span>

* <span data-ttu-id="7783a-124">目標資料庫必須使用完整復原模型。</span><span class="sxs-lookup"><span data-stu-id="7783a-124">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="7783a-125">**Azure PowerShell**：</span><span class="sxs-lookup"><span data-stu-id="7783a-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="7783a-126">[安裝最新的 Azure PowerShell 命令](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7783a-126">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="7783a-127">**SQL Server IaaS 擴充功能**：</span><span class="sxs-lookup"><span data-stu-id="7783a-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="7783a-128">[安裝 SQL Server IaaS 擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="7783a-128">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="7783a-129">Settings</span><span class="sxs-lookup"><span data-stu-id="7783a-129">Settings</span></span>
<span data-ttu-id="7783a-130">下表說明可以為自動備份設定的選項。</span><span class="sxs-lookup"><span data-stu-id="7783a-130">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="7783a-131">針對傳統 VM，您必須使用 PowerShell 來設定這些設定。</span><span class="sxs-lookup"><span data-stu-id="7783a-131">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="7783a-132">設定</span><span class="sxs-lookup"><span data-stu-id="7783a-132">Setting</span></span> | <span data-ttu-id="7783a-133">範圍 (預設值)</span><span class="sxs-lookup"><span data-stu-id="7783a-133">Range (Default)</span></span> | <span data-ttu-id="7783a-134">說明</span><span class="sxs-lookup"><span data-stu-id="7783a-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7783a-135">**自動備份**</span><span class="sxs-lookup"><span data-stu-id="7783a-135">**Automated Backup**</span></span> |<span data-ttu-id="7783a-136">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7783a-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="7783a-137">針對執行 SQL Server 2014 Standard 或 Enterprise 的 Azure VM，啟用或停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="7783a-138">**保留期限**</span><span class="sxs-lookup"><span data-stu-id="7783a-138">**Retention Period**</span></span> |<span data-ttu-id="7783a-139">1-30 天 (30 天)</span><span class="sxs-lookup"><span data-stu-id="7783a-139">1-30 days (30 days)</span></span> |<span data-ttu-id="7783a-140">保留備份的天數。</span><span class="sxs-lookup"><span data-stu-id="7783a-140">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="7783a-141">**儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="7783a-141">**Storage Account**</span></span> |<span data-ttu-id="7783a-142">Azure 儲存體帳戶 (針對指定 VM 建立的儲存體帳戶)</span><span class="sxs-lookup"><span data-stu-id="7783a-142">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="7783a-143">將自動備份檔案儲存在 Blob 儲存體中時，所使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7783a-143">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="7783a-144">這個位置會建立一個容器來儲存所有備份檔案。</span><span class="sxs-lookup"><span data-stu-id="7783a-144">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="7783a-145">備份檔案命名慣例包括日期、時間和電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="7783a-145">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="7783a-146">**加密**</span><span class="sxs-lookup"><span data-stu-id="7783a-146">**Encryption**</span></span> |<span data-ttu-id="7783a-147">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7783a-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="7783a-148">啟用或停用加密。</span><span class="sxs-lookup"><span data-stu-id="7783a-148">Enables or disables encryption.</span></span> <span data-ttu-id="7783a-149">啟用加密時，用來還原備份的憑證會放在與使用相同命名慣例之相同 automaticbackup 容器中的指定儲存體帳戶裡。</span><span class="sxs-lookup"><span data-stu-id="7783a-149">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="7783a-150">如果密碼變更，就會以該密碼產生新的憑證，但是舊的憑證還是會保留，以還原先前的備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-150">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="7783a-151">**密碼**</span><span class="sxs-lookup"><span data-stu-id="7783a-151">**Password**</span></span> |<span data-ttu-id="7783a-152">密碼文字 (無)</span><span class="sxs-lookup"><span data-stu-id="7783a-152">Password text (None)</span></span> |<span data-ttu-id="7783a-153">加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="7783a-153">A password for encryption keys.</span></span> <span data-ttu-id="7783a-154">唯有啟用加密時，才需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="7783a-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="7783a-155">若要還原加密的備份，您必須要有建立備份時所使用的正確密碼和相關憑證。</span><span class="sxs-lookup"><span data-stu-id="7783a-155">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="7783a-156">**備份系統資料庫**</span><span class="sxs-lookup"><span data-stu-id="7783a-156">**Backup system databases**</span></span> | <span data-ttu-id="7783a-157">啟用/停用 (已停用)</span><span class="sxs-lookup"><span data-stu-id="7783a-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="7783a-158">完整備份 Master、Model 及 MSDB</span><span class="sxs-lookup"><span data-stu-id="7783a-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="7783a-159">**設定備份排程**</span><span class="sxs-lookup"><span data-stu-id="7783a-159">**Configure backup schedule**</span></span> | <span data-ttu-id="7783a-160">手動/自動化 (自動化)</span><span class="sxs-lookup"><span data-stu-id="7783a-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="7783a-161">若要根據記錄檔的成長情況自動執行完整或記錄備份，請選取 [手動]。</span><span class="sxs-lookup"><span data-stu-id="7783a-161">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="7783a-162">若要指定完整或記錄備份的排程，請選取 [手動]。</span><span class="sxs-lookup"><span data-stu-id="7783a-162">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="7783a-163">使用 PowerShell 進行設定</span><span class="sxs-lookup"><span data-stu-id="7783a-163">Configuration with PowerShell</span></span>
<span data-ttu-id="7783a-164">在下列 PowerShell 範例中，是針對現有的 SQL Server 2014 VM 設定自動備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-164">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="7783a-165">**New-AzureVMSqlServerAutoBackupConfig** 命令會設定自動備份設定，以在 $storageaccount 變數所指定的 Azure 儲存體帳戶中儲存備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-165">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="7783a-166">這些備份將會保留 10 天。</span><span class="sxs-lookup"><span data-stu-id="7783a-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="7783a-167">**Set-AzureVMSqlServerExtension** 命令會使用這些設定更新指定的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="7783a-167">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="7783a-168">可能需要幾分鐘的時間來安裝及設定 SQL Server IaaS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7783a-168">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="7783a-169">若要啟用加密，請修改先前的指令碼，為 CertificatePassword 參數傳遞 EnableEncryption 參數和密碼 (安全字串)。</span><span class="sxs-lookup"><span data-stu-id="7783a-169">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="7783a-170">下列指令碼會啟用上述範例中的自動備份設定，並新增加密。</span><span class="sxs-lookup"><span data-stu-id="7783a-170">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="7783a-171">若要停用自動備份，請執行相同的指令碼，但不要對 **New-AzureVMSqlServerAutoBackupConfig** 使用 **-Enable** 參數。</span><span class="sxs-lookup"><span data-stu-id="7783a-171">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="7783a-172">和安裝一樣，可能需要幾分鐘的時間來停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-172">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="7783a-173">停用及解除安裝 SQL Server IaaS 代理程式不會移除先前設定的受管理備份設定。</span><span class="sxs-lookup"><span data-stu-id="7783a-173">Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings.</span></span> <span data-ttu-id="7783a-174">在停用或解除安裝 SQL Server IaaS 代理程式之前，應先停用自動備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-174">You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7783a-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7783a-175">Next steps</span></span>
<span data-ttu-id="7783a-176">自動備份會在 Azure VM 上設定受管理備份。</span><span class="sxs-lookup"><span data-stu-id="7783a-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="7783a-177">因此，請務必 [檢閱受管理備份的文件](https://msdn.microsoft.com/library/dn449496.aspx) ，以了解其行為和隱含意義。</span><span class="sxs-lookup"><span data-stu-id="7783a-177">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="7783a-178">您可以在下列主題中找到 Azure VM 上 SQL Server 的其他備份和還原指引： [Azure 虛擬機器中的 SQL Server 備份和還原](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7783a-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="7783a-179">如需有關其他可用之自動化工作的資訊，請參閱 [SQL Server IaaS 代理程式擴充功能](../classic/sql-server-agent-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="7783a-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="7783a-180">如需有關在 Azure VM 上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7783a-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

