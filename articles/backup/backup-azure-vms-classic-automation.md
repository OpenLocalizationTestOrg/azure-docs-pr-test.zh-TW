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
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="aa7b2-103">使用 AzureRM.Backup Cmdlet 備份虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aa7b2-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa7b2-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="aa7b2-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="aa7b2-105">傳統</span><span class="sxs-lookup"><span data-stu-id="aa7b2-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="aa7b2-106">本文說明如何使用 Azure PowerShell 來備份和復原 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="aa7b2-107">Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="aa7b2-108">本文說明如何使用傳統部署模型來將資料備份到備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="aa7b2-109">如果您尚未在訂用帳戶中建立備份保存庫，請參閱[使用 AzureRM.RecoveryServices.Backup Cmdlet 備份虛擬機器](backup-azure-vms-automation.md)這篇文章的 Resource Manager 版本。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="aa7b2-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa7b2-111">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="aa7b2-112">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="aa7b2-113">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="aa7b2-114">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="aa7b2-115">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="aa7b2-116">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="aa7b2-117">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="aa7b2-118">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="aa7b2-119">概念</span><span class="sxs-lookup"><span data-stu-id="aa7b2-119">Concepts</span></span>
<span data-ttu-id="aa7b2-120">本文章提供用來備份虛擬機器之 PowerShell Cmdlet 的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="aa7b2-121">如需有關保護 Azure VM 的基本資訊，請參閱 [Plan your VM backup infrastructure in Azure (在 Azure 中規劃 VM 備份基礎結構)](backup-azure-vms-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aa7b2-122">開始之前，請閱讀使用 Azure 備份所需的[必要條件](backup-azure-vms-prepare.md)，以及目前 VM 備份解決方案的[限制](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="aa7b2-123">若要有效地使用 PowerShell，請花一點時間了解物件的階層以及從何處開始。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![物件階層](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="aa7b2-125">最重要的兩個流程是啟用 VM 保護，以及從復原點還原資料。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="aa7b2-126">本文的重點是協助您熟練 PowerShell Cmdlet 來支援這兩種情況。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="aa7b2-127">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="aa7b2-127">Setup and Registration</span></span>
<span data-ttu-id="aa7b2-128">開始：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-128">To begin:</span></span>

1. <span data-ttu-id="aa7b2-129">[下載最新版 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需的基本版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="aa7b2-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="aa7b2-130">輸入下列命令，以找到可用的 Azure 備份 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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

<span data-ttu-id="aa7b2-131">PowerShell 可以自動化下列設定和註冊工作：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="aa7b2-132">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="aa7b2-132">Create a backup vault</span></span>
* <span data-ttu-id="aa7b2-133">向 Azure 備份服務註冊 VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="aa7b2-134">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="aa7b2-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="aa7b2-135">對於第一次使用 Azure 備份的客戶，您需要註冊 Azure 備份提供者以搭配您的訂用帳戶使用。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="aa7b2-136">這可以透過執行下列命令來完成：Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="aa7b2-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="aa7b2-137">您可以使用 **New-AzureRmBackupVault** Cmdlet，來建立新的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="aa7b2-138">備份保存庫是 ARM 資源，因此您必須將它放在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="aa7b2-139">在提高權限的 Azure PowerShell 主控台中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="aa7b2-140">您可以使用 **Get-AzureRmBackupVault** Cmdlet，來取得特定訂用帳戶中所有備份保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7b2-141">將備份保存庫物件儲存到變數中會很方便。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="aa7b2-142">許多 Azure 備份 Cmdlet 都需要保存庫物件做為輸入。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="aa7b2-143">註冊 VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-143">Registering the VMs</span></span>
<span data-ttu-id="aa7b2-144">使用 Azure 備份來設定備份的第一個步驟是向 Azure 備份保存庫註冊您的電腦或 VM。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="aa7b2-145">**Register-AzureRmBackupContainer** Cmdlet 會取用 Azure IaaS 虛擬機器的輸入資訊，並對指定的保存庫進行註冊。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="aa7b2-146">註冊作業會將 Azure 虛擬機器與備份保存庫相關聯，並於整個備份生命週期內追蹤 VM。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="aa7b2-147">向 Azure 備份服務註冊您的 VM 會建立最上層的容器物件。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="aa7b2-148">一個容器通常包含多個可備份的項目，但以 VM 而言，容器只有一個備份項目。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="aa7b2-149">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="aa7b2-150">建立保護原則</span><span class="sxs-lookup"><span data-stu-id="aa7b2-150">Create a protection policy</span></span>
<span data-ttu-id="aa7b2-151">啟動 VM 的備份並不一定要建立新的保護原則。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="aa7b2-152">保存庫隨附「預設原則」，可用來快速啟用保護，稍後再編輯正確的細節。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="aa7b2-153">您可以使用 **Get-AzureRmBackupProtectionPolicy** Cmdlet，來取得保存庫中可用的原則清單：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="aa7b2-154">PowerShell 中 BackupTime 欄位的時區是 UTC。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="aa7b2-155">不過，當備份時間顯示在 Azure 入口網站中時，時區會對應您的本機系統與 UTC 時差。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="aa7b2-156">備份原則至少與一個保留原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="aa7b2-157">保留原則定義復原點在 Azure 備份中保留的時間長度。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="aa7b2-158">**New-AzureRmBackupRetentionPolicy** Cmdlet 會建立可儲存保留原則資訊的 PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="aa7b2-159">這些保留原則物件會用來做為 *New-AzureRmBackupProtectionPolicy* Cmdlet 的輸入，或直接與 *Enable-AzureRmBackupProtection* Cmdlet 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="aa7b2-160">備份原則定義項目備份的時間和頻率。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="aa7b2-161">**New-AzureRmBackupProtectionPolicy** Cmdlet 會建立可儲存備份原則資訊的 PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="aa7b2-162">備份原則會用來做為 *Enable-AzureRmBackupProtection* Cmdlet 的輸入。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="aa7b2-163">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-163">Enable protection</span></span>
<span data-ttu-id="aa7b2-164">啟用保護牽涉到兩個物件：項目和原則，兩者都必須屬於相同的保存庫。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="aa7b2-165">一旦原則與項目相關聯，備份工作流程將依定義的排程開始運作。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="aa7b2-166">初始備份</span><span class="sxs-lookup"><span data-stu-id="aa7b2-166">Initial backup</span></span>
<span data-ttu-id="aa7b2-167">備份排程會負責執行項目的完整初始複製，以及後續備份的增量複製。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="aa7b2-168">但如果您想要在特定時間強制進行初始備份，甚至是立即開始，請使用 **Backup-AzureRmBackupItem** Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="aa7b2-169">在 PowerShell 中顯示的 StartTime 和 EndTime 欄位的時間為 UTC。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="aa7b2-170">不過，當類似資訊顯示在 Azure 入口網站中時，時區會對應您的本機系統時鐘。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="aa7b2-171">監視備份工作</span><span class="sxs-lookup"><span data-stu-id="aa7b2-171">Monitoring a backup job</span></span>
<span data-ttu-id="aa7b2-172">Azure 備份中長時間執行的大部分作業都模擬成工作。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="aa7b2-173">如此就很容易追蹤進度，而不需要一直開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="aa7b2-174">若要取得進行中作業的最新狀態，請使用 **Get-AzureRmBackupJob** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="aa7b2-175">因為需要額外的程式碼且並非必要，所以不輪詢這些作業是否完成，而是更簡單地改用 **Wait-AzureRmBackupJob** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="aa7b2-176">在指令碼中使用此 Cmdlet 會暫停執行，直到工作完成或達到指定的逾時值為止。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="aa7b2-177">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-177">Restore an Azure VM</span></span>
<span data-ttu-id="aa7b2-178">若要還原備份資料，您需要識別備份的「項目」和保存時間點資料的「復原點」。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="aa7b2-179">這項資訊會提供給 Restore-AzureRmBackupItem Cmdlet，開始從保存庫將資料還原到客戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="aa7b2-180">選取 VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-180">Select the VM</span></span>
<span data-ttu-id="aa7b2-181">若要取得可識別正確備份項目的 PowerShell 物件，您需要從保存庫中的「容器」開始，向下深入物件階層。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="aa7b2-182">若要選取代表 VM 的容器，請使用 **Get-AzureRmBackupContainer** Cmdlet，並透過管道將它傳送到 **Get-AzureRmBackupItem** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="aa7b2-183">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="aa7b2-183">Choose a recovery point</span></span>
<span data-ttu-id="aa7b2-184">您現在可以使用 **Get-AzureRmBackupRecoveryPoint** Cmdlet，列出備份項目的所有復原點，並選擇要還原的復原點。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="aa7b2-185">使用者通常會從清單中選擇最近的 *AppConsistent* 點。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="aa7b2-186">變數 ```$rp``` 是所選取之備份項目的復原點陣列，以時間的回推順序排序 - 最近的復原點位於索引 0。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="aa7b2-187">使用標準 PowerShell 陣列索引來挑選復原點。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="aa7b2-188">例如： ```$rp[0]``` 將會選取最新的復原點。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="aa7b2-189">還原磁碟</span><span class="sxs-lookup"><span data-stu-id="aa7b2-189">Restoring disks</span></span>
<span data-ttu-id="aa7b2-190">透過 Azure 入口網站或透過 Azure PowerShell 執行還原作業，兩者之間有一項重要差異。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="aa7b2-191">如果使用 PowerShell，從復原點還原磁碟及組態資訊時，還原作業會停止。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="aa7b2-192">不會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="aa7b2-193">Restore-AzureRmBackupItem 不會建立 VM。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="aa7b2-194">只會將磁碟還原到指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="aa7b2-195">這與 Azure 入口網站中的行為不同。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="aa7b2-196">完成還原作業之後，可以使用 **Get-AzureRmBackupJobDetails** Cmdlet 來取得還原作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="aa7b2-197">*ErrorDetails* 屬性會有重建 VM 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="aa7b2-198">建置 VM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-198">Build the VM</span></span>
<span data-ttu-id="aa7b2-199">如果要從還原的磁碟建置 VM，您可以使用較舊的 Azure 服務管理 PowerShell Cmdlet、新的 Azure Resource Manager 範本，或甚至使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="aa7b2-200">在快速的範例中，我們將說明如何使用 Azure 服務管理 Cmdlet 來達到目的。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="aa7b2-201">如需如何從還原的磁碟建置 VM 的詳細資訊，請參閱下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="aa7b2-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="aa7b2-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="aa7b2-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="aa7b2-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="aa7b2-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="aa7b2-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="aa7b2-205">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="aa7b2-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="aa7b2-206">1.取得作業子工作的完成狀態</span><span class="sxs-lookup"><span data-stu-id="aa7b2-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="aa7b2-207">若要追蹤個別子作業的完成狀態，可以使用 **Get-AzureRmBackupJobDetails** Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="aa7b2-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="aa7b2-208">2.建立備份作業的每日/每週報表</span><span class="sxs-lookup"><span data-stu-id="aa7b2-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="aa7b2-209">系統管理員通常想要知道備份作業在過去 24 小時的執行情況，以及那些備份作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="aa7b2-210">此外，傳輸的資料量提供系統管理員一種預估其每月資料使用量的方式。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="aa7b2-211">下列指令碼會從 Azure 備份服務提取原始資料，並將資訊顯示在 PowerShell 主控台上。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

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

<span data-ttu-id="aa7b2-212">如果想要將製作圖表的功能加入這個報表輸出，請參閱 TechNet 部落格文章 [Charting with PowerShell (使用 PowerShell 製作圖表)](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa7b2-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa7b2-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa7b2-213">Next steps</span></span>
<span data-ttu-id="aa7b2-214">如果您偏好使用 PowerShell 來與您的 Azure 資源交流，請參閱保護 Windows Server 的 PowerShell 文章：[部署和管理 Windows Server 的備份](backup-client-automation-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="aa7b2-215">另請參閱管理 DPM 備份的 PowerShell 文章：[部署和管理 DPM 的備份](backup-dpm-automation-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="aa7b2-216">這兩篇文章都有適用於 Resource Manager 部署以及傳統部署的版本。</span><span class="sxs-lookup"><span data-stu-id="aa7b2-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
