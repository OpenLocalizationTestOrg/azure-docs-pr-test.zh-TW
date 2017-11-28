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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="d6806-103">使用虛擬機器 AzureRM.RecoveryServices.Backup cmdlet tooback</span><span class="sxs-lookup"><span data-stu-id="d6806-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6806-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="d6806-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="d6806-105">傳統</span><span class="sxs-lookup"><span data-stu-id="d6806-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="d6806-106">本文章將示範如何設定 toouse Azure PowerShell cmdlet tooback 和復原 Azure 虛擬機器 (VM) 從 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="d6806-107">復原服務保存庫是 Azure 資源管理員資源，而且是使用的 tooprotect 資料和 Azure 備份和 Azure Site Recovery 服務中的資產。</span><span class="sxs-lookup"><span data-stu-id="d6806-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="d6806-108">您可以使用 Azure Service Manager 部署的 Vm，復原服務保存庫 tooprotect 和 Azure Resource Manager 部署的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d6806-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="d6806-109">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d6806-110">本文適用於使用 hello 資源管理員模型所建立的 vm。</span><span class="sxs-lookup"><span data-stu-id="d6806-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="d6806-111">這篇文章會引導您逐步使用 PowerShell tooprotect VM，並還原資料從復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="d6806-112">概念</span><span class="sxs-lookup"><span data-stu-id="d6806-112">Concepts</span></span>
<span data-ttu-id="d6806-113">如果您不熟悉 hello Azure Backup 服務，hello 服務的概觀，請參閱[什麼是 Azure 備份？](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="d6806-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="d6806-114">開始之前，請確定您涵蓋關於 Azure backup 的 hello 所需必要條件 toowork hello essentials 和 hello hello 目前 VM 的備份解決方案的限制。</span><span class="sxs-lookup"><span data-stu-id="d6806-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="d6806-115">toouse PowerShell 實際上，它是必要的 toounderstand hello 階層的物件，並從中 toostart。</span><span class="sxs-lookup"><span data-stu-id="d6806-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![復原服務物件階層](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="d6806-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet 參考資料，請參閱 hello [Azure 備份-Recovery Services 指令程式](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup)hello Azure 文件庫中。</span><span class="sxs-lookup"><span data-stu-id="d6806-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="d6806-118">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="d6806-118">Setup and Registration</span></span>
<span data-ttu-id="d6806-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="d6806-119">toobegin:</span></span>

1. <span data-ttu-id="d6806-120">[下載最新版的 PowerShell 中 hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello 所需的最低版本是： 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="d6806-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="d6806-121">輸入下列命令的 hello 尋找可用的 hello Azure 備份的 PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d6806-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="d6806-122">可以使用 PowerShell 自動化 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="d6806-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="d6806-123">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="d6806-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="d6806-124">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6806-124">Back up Azure VMs</span></span>
* <span data-ttu-id="d6806-125">觸發備份作業</span><span class="sxs-lookup"><span data-stu-id="d6806-125">Trigger a backup job</span></span>
* <span data-ttu-id="d6806-126">監視備份作業</span><span class="sxs-lookup"><span data-stu-id="d6806-126">Monitor a backup job</span></span>
* <span data-ttu-id="d6806-127">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6806-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d6806-128">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="d6806-128">Create a recovery services vault</span></span>
<span data-ttu-id="d6806-129">hello 步驟會引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="d6806-130">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="d6806-131">如果您使用 Azure Backup hello 第一次，您必須使用 hello **[暫存器 AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  cmdlet tooregister hello Azure 復原服務提供者與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6806-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="d6806-132">hello 復原服務保存庫是 「 資源管理員資源，因此您需要 tooplace 它資源群組內。</span><span class="sxs-lookup"><span data-stu-id="d6806-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="d6806-133">您可以使用現有的資源群組，或建立資源群組以 hello **[新增 AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="d6806-134">建立資源群組時，指定 hello 名稱和位置 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6806-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="d6806-135">使用 hello **[新增 AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="d6806-136">請務必 toospecify hello hello 保存庫相同的位置，所用的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6806-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="d6806-137">指定儲存體備援 toouse; hello 類型您可以使用[本機備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage)或[地理備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="d6806-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="d6806-138">hello 下列範例顯示 hello testvault-BackupStorageRedundancy 選項設定 tooGeoRedundant。</span><span class="sxs-lookup"><span data-stu-id="d6806-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="d6806-139">許多 Azure Backup cmdlet 需要 hello 復原服務保存庫的物件做為輸入。</span><span class="sxs-lookup"><span data-stu-id="d6806-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="d6806-140">基於這個理由，它是方便 toostore hello 備份復原服務保存庫在變數中。</span><span class="sxs-lookup"><span data-stu-id="d6806-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="d6806-141">檢視訂用帳戶中的 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="d6806-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="d6806-142">使用 **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello 份 hello 目前訂用帳戶中所有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="d6806-143">您可以使用這個命令 toocheck，建立新的保存庫或 toosee hello hello 訂用帳戶中可用的保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="d6806-144">執行所有的保存庫 hello 命令，Get-AzureRmRecoveryServicesVault tooview hello 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d6806-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="d6806-145">hello 下列範例顯示 hello 資訊顯示每個保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="d6806-146">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6806-146">Back up Azure VMs</span></span>
<span data-ttu-id="d6806-147">使用 復原服務保存庫 tooprotect 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d6806-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="d6806-148">在您套用 hello 保護之前，設定 hello 保存庫內容 （hello 類型 hello 保存庫中受保護的資料），並確認 hello 保護原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="d6806-149">hello 保護原則是 hello 排程 hello 備份工作執行時，每個備份快照集的保留時間長度。</span><span class="sxs-lookup"><span data-stu-id="d6806-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="d6806-150">設定保存庫內容</span><span class="sxs-lookup"><span data-stu-id="d6806-150">Set vault context</span></span>
<span data-ttu-id="d6806-151">再啟用 VM 上的保護，請使用**[組 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello 保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="d6806-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="d6806-152">一旦設定 hello 保存庫的內容之後，它會套用 tooall 後續的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="d6806-153">hello 下列範例會設定 hello hello 保存庫，保存庫內容*testvault*。</span><span class="sxs-lookup"><span data-stu-id="d6806-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="d6806-154">建立保護原則</span><span class="sxs-lookup"><span data-stu-id="d6806-154">Create a protection policy</span></span>
<span data-ttu-id="d6806-155">當您建立復原服務保存庫時，它會隨附預設的保護和保留原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="d6806-156">hello 預設保護原則會觸發備份工作在指定時間的每一天。</span><span class="sxs-lookup"><span data-stu-id="d6806-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="d6806-157">hello 預設保留原則會保留 30 天 hello 每日復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="d6806-158">您可以使用 hello 預設原則 tooquickly 保護您的 VM，然後編輯 hello 原則，稍後可以使用各種不同詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d6806-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="d6806-159">使用 **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview hello 保護原則 hello 保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="d6806-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="d6806-160">您可以使用這個指令程式 tooget 特定原則或工作負載類型相關聯的 tooview hello 原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="d6806-161">下列範例中的 hello 取得工作負載類型，AzureVM 原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="d6806-162">在 PowerShell 中的 hello BackupTime 欄位的 hello 時區為 UTC。</span><span class="sxs-lookup"><span data-stu-id="d6806-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="d6806-163">不過，當 hello 備份時間所示為 hello Azure 入口網站，hello 時調整的 tooyour 本地時區。</span><span class="sxs-lookup"><span data-stu-id="d6806-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="d6806-164">備份保護原則至少與一個保留原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="d6806-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="d6806-165">保留原則會定義復原點在被刪除之前要保留多久。</span><span class="sxs-lookup"><span data-stu-id="d6806-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="d6806-166">使用 **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  tooview hello 預設保留原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="d6806-167">同樣地，您可以使用 **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello 預設按排程時間原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="d6806-168">hello **[新增 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet 會建立保留的備份原則資訊的 PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="d6806-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="d6806-169">hello 排程和保留原則 物件就會當做輸入 toohello **[新增 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="d6806-170">hello 下列範例會儲存 hello 按排程時間原則和 hello 保留原則在變數中。</span><span class="sxs-lookup"><span data-stu-id="d6806-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="d6806-171">hello 範例會使用這些變數 toodefine hello 參數，當建立保護原則， *NewPolicy*。</span><span class="sxs-lookup"><span data-stu-id="d6806-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="d6806-172">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="d6806-172">Enable protection</span></span>
<span data-ttu-id="d6806-173">一旦您已經定義 hello 備份的保護原則，您仍然必須啟用 hello 原則項目。</span><span class="sxs-lookup"><span data-stu-id="d6806-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="d6806-174">使用**[啟用 AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable 保護。</span><span class="sxs-lookup"><span data-stu-id="d6806-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="d6806-175">啟用保護需要兩個物件-hello 項目和 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="d6806-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="d6806-176">一旦 hello 原則已與 hello 保存庫相關聯，就會在 hello 原則排程所定義的 hello 時間觸發 hello 備份工作流程。</span><span class="sxs-lookup"><span data-stu-id="d6806-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="d6806-177">下列範例啟用項目的保護 hello，V2VM，使用 hello 原則，NewPolicy hello。</span><span class="sxs-lookup"><span data-stu-id="d6806-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="d6806-178">在非加密的資源管理員 Vm 上 tooenable hello 保護</span><span class="sxs-lookup"><span data-stu-id="d6806-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d6806-179">tooenable hello 保護加密 （使用 BEK 和 KEK 加密） 的 Vm，您必須 toogive hello Azure 備份服務的權限 tooread 金鑰和秘密金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="d6806-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="d6806-180">tooenable hello 保護加密 （僅限使用 BEK 加密） 的 Vm，您必須 toogive hello Azure 備份服務的權限 tooread 秘密金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="d6806-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="d6806-181">如果您使用 hello Azure 政府雲端，然後用於 hello 值 ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello 參數**-ServicePrincipalName**中[Set-azurermkeyvaultaccesspolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d6806-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="d6806-182">若為傳統 VM</span><span class="sxs-lookup"><span data-stu-id="d6806-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="d6806-183">修改保護原則</span><span class="sxs-lookup"><span data-stu-id="d6806-183">Modify a protection policy</span></span>
<span data-ttu-id="d6806-184">toomodify hello 保護原則，使用[組 AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy 或 RetentionPolicy 物件。</span><span class="sxs-lookup"><span data-stu-id="d6806-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="d6806-185">hello 下例 hello 復原點保留 too365 天數。</span><span class="sxs-lookup"><span data-stu-id="d6806-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="d6806-186">觸發備份</span><span class="sxs-lookup"><span data-stu-id="d6806-186">Trigger a backup</span></span>
<span data-ttu-id="d6806-187">您可以使用**[備份 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger 備份工作。</span><span class="sxs-lookup"><span data-stu-id="d6806-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="d6806-188">如果它是 hello 初始備份，則完整備份。</span><span class="sxs-lookup"><span data-stu-id="d6806-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="d6806-189">後續的備份會採用增量複本。</span><span class="sxs-lookup"><span data-stu-id="d6806-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="d6806-190">要確定 toouse **[組 AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** 觸發 hello 備份作業之前 tooset hello 保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="d6806-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="d6806-191">下列範例中的 hello 假設設定保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="d6806-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="d6806-192">在 PowerShell 中的 hello StartTime 和 EndTime 欄位的 hello 時區為 UTC。</span><span class="sxs-lookup"><span data-stu-id="d6806-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="d6806-193">不過，當 hello 時間所示為 hello Azure 入口網站，hello 時調整的 tooyour 本地時區。</span><span class="sxs-lookup"><span data-stu-id="d6806-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="d6806-194">監視備份工作</span><span class="sxs-lookup"><span data-stu-id="d6806-194">Monitoring a backup job</span></span>
<span data-ttu-id="d6806-195">您可以監視長時間執行作業，例如備份作業，而不使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d6806-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="d6806-196">為進行中工作時，使用 hello tooget hello 狀態 **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d6806-197">此 cmdlet 會取得特定的保存庫的 hello 備份工作和 hello 保存庫的內容中指定該保存庫。</span><span class="sxs-lookup"><span data-stu-id="d6806-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="d6806-198">hello 下列範例取得 hello 的陣列，進行中工作的狀態，並儲存 hello 狀態 hello $joblist 變數中。</span><span class="sxs-lookup"><span data-stu-id="d6806-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d6806-199">而不是輪詢-這是不需要額外的程式碼-完成這些作業使用 hello **[等候 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="d6806-200">這個指令程式暫停 hello 執行，直到 hello 作業完成或 hello 可讓您指定逾時值為止。</span><span class="sxs-lookup"><span data-stu-id="d6806-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="d6806-201">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6806-201">Restore an Azure VM</span></span>
<span data-ttu-id="d6806-202">沒有 hello 還原的 VM 使用 hello Azure 入口網站，並還原 VM，使用 PowerShell 的主要差異。</span><span class="sxs-lookup"><span data-stu-id="d6806-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="d6806-203">使用 PowerShell，hello 還原作業已完成，一旦建立 hello 磁碟和組態資訊從 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="d6806-204">hello 還原作業不會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d6806-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="d6806-205">toocreate 從虛擬機器磁碟，請參閱 hello 區段[從預存的磁碟建立 hello VM](backup-azure-vms-automation.md#create-a-vm-from-stored-disks)。</span><span class="sxs-lookup"><span data-stu-id="d6806-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="d6806-206">hello Azure VM 的基本步驟 toorestore 如下：</span><span class="sxs-lookup"><span data-stu-id="d6806-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="d6806-207">選取 hello VM</span><span class="sxs-lookup"><span data-stu-id="d6806-207">Select hello VM</span></span>
* <span data-ttu-id="d6806-208">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="d6806-208">Choose a recovery point</span></span>
* <span data-ttu-id="d6806-209">還原 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="d6806-209">Restore hello disks</span></span>
* <span data-ttu-id="d6806-210">從預存的磁碟建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="d6806-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="d6806-211">hello 下圖顯示從 hello RecoveryServicesVault 向 toohello BackupRecoveryPoint hello 物件階層架構。</span><span class="sxs-lookup"><span data-stu-id="d6806-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![顯示 BackupContainer 的復原服務物件階層](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="d6806-213">toorestore 備份的資料，找出 hello 備份項目和 hello 保存 hello 時間點資料的復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="d6806-214">使用 hello **[還原 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 資料 hello 從保存庫 toohello 客戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6806-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="d6806-215">選取 hello VM</span><span class="sxs-lookup"><span data-stu-id="d6806-215">Select hello VM</span></span>
<span data-ttu-id="d6806-216">tooget hello PowerShell 物件，可識別 hello 右備份項目、 啟動 hello 保存庫中的 hello 容器和由上至下 hello 物件階層架構。</span><span class="sxs-lookup"><span data-stu-id="d6806-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="d6806-217">代表 hello VM，使用 hello tooselect hello 容器 **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet 並使用管線傳送該 toohello  **[Get AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6806-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="d6806-218">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="d6806-218">Choose a recovery point</span></span>
<span data-ttu-id="d6806-219">使用 hello  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  cmdlet toolist hello 備份項目的所有復原都點。</span><span class="sxs-lookup"><span data-stu-id="d6806-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="d6806-220">然後選擇 hello 復原點 toorestore。</span><span class="sxs-lookup"><span data-stu-id="d6806-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="d6806-221">如果您不確定哪一個復原點 toouse，是很好的作法 toochoose hello 最近 RecoveryPointType = AppConsistent hello 清單中的點。</span><span class="sxs-lookup"><span data-stu-id="d6806-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="d6806-222">在下列指令碼的 hello，hello 變數， **$rp**，是陣列的復原點，針對 hello 選取備份項目，從 hello 過去七天內。</span><span class="sxs-lookup"><span data-stu-id="d6806-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="d6806-223">hello 陣列是以反向順序排序的時間與 hello 最新復原點位於索引 0。</span><span class="sxs-lookup"><span data-stu-id="d6806-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="d6806-224">使用標準的 PowerShell 陣列索引 toopick hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="d6806-225">在 hello 範例 $rp [0] 選取 hello 最新的復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="d6806-226">還原 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="d6806-226">Restore hello disks</span></span>
<span data-ttu-id="d6806-227">使用 hello **[還原 AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore 備份項目資料和設定 tooa 復原點。</span><span class="sxs-lookup"><span data-stu-id="d6806-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="d6806-228">一旦您已識別復原點，使用它做 hello 值為 hello **New-recoverypoint**參數。</span><span class="sxs-lookup"><span data-stu-id="d6806-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="d6806-229">Hello 先前的範例程式碼**$rp [0]**已 hello 復原點 toouse。</span><span class="sxs-lookup"><span data-stu-id="d6806-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="d6806-230">在下列範例程式碼，hello **$rp [0]**是 hello 復原點 toouse 還原 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="d6806-231">toorestore hello 磁碟和組態資訊：</span><span class="sxs-lookup"><span data-stu-id="d6806-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="d6806-232">使用 hello **[等候 AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  hello 還原作業 toocomplete 的 cmdlet toowait。</span><span class="sxs-lookup"><span data-stu-id="d6806-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="d6806-233">Hello 還原作業完成後，請使用 hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  cmdlet tooget hello 詳細資料的 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="d6806-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="d6806-234">hello JobDetails 屬性有 hello 資訊所需的 toorebuild hello VM。</span><span class="sxs-lookup"><span data-stu-id="d6806-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="d6806-235">一旦還原 hello 磁碟時，請前往下一個區段 toocreate hello toohello VM。</span><span class="sxs-lookup"><span data-stu-id="d6806-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="d6806-236">從還原的磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="d6806-236">Create a VM from restored disks</span></span>
<span data-ttu-id="d6806-237">您已還原 hello 磁碟之後，使用這些步驟 toocreate，並設定從磁碟 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d6806-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="d6806-238">toocreate 加密從還原的磁碟 Vm，您的 Azure 角色必須具有的權限 tooperform hello 動作， **Microsoft.KeyVault/vaults/deploy/action**。</span><span class="sxs-lookup"><span data-stu-id="d6806-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="d6806-239">如果您的角色並沒有此權限，請使用此動作來建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="d6806-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="d6806-240">如需詳細資訊，請參閱 [Azure RBAC 中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="d6806-241">查詢 hello 還原 hello 工作詳細資料的磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="d6806-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="d6806-242">設定 hello Azure 儲存體的內容，並還原 hello JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="d6806-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="d6806-243">使用 hello JSON 組態檔 toocreate hello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="d6806-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="d6806-244">附加 hello OS 磁碟和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="d6806-245">根據您的 Vm 的 hello 組態，請按一下 hello 相關連結 tooview 個別 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d6806-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="d6806-246">非管理、 未加密的 Vm</span><span class="sxs-lookup"><span data-stu-id="d6806-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="d6806-247">非管理、 加密 Vm (只有 BEK)</span><span class="sxs-lookup"><span data-stu-id="d6806-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="d6806-248">非管理、 加密的 Vm （BEK 和 KEK）</span><span class="sxs-lookup"><span data-stu-id="d6806-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="d6806-249">受管理、 未加密的 Vm</span><span class="sxs-lookup"><span data-stu-id="d6806-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="d6806-250">受管理的加密 Vm （BEK 和 KEK）</span><span class="sxs-lookup"><span data-stu-id="d6806-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="d6806-251">未受管理、未加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d6806-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d6806-252">下列範例針對未受管理、 未加密的 Vm 使用 hello。</span><span class="sxs-lookup"><span data-stu-id="d6806-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="d6806-253">未受管理的已加密 VM (僅限 BEK)</span><span class="sxs-lookup"><span data-stu-id="d6806-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="d6806-254">（僅限使用 BEK 加密） 的 Vm 未受管理的加密，您需要 toorestore hello toohello 秘密金鑰保存庫之前，您可以將附加磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="d6806-255">如需詳細資訊，請參閱 hello 文章[從 Azure Backup 復原點還原加密的虛擬機器](backup-azure-restore-key-secret.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d6806-256">hello 下列範例顯示如何 tooattach OS 和資料磁碟加密 Vm。</span><span class="sxs-lookup"><span data-stu-id="d6806-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d6806-257">未受管理的已加密 VM (BEK 和 KEK)</span><span class="sxs-lookup"><span data-stu-id="d6806-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d6806-258">對於未受管理的加密 Vm （使用 BEK 和 KEK 加密），您需要 toorestore hello 金鑰和秘密 toohello 金鑰保存庫之前，您可以將附加磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="d6806-259">如需詳細資訊，請參閱 hello 文章[從 Azure Backup 復原點還原加密的虛擬機器](backup-azure-restore-key-secret.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="d6806-260">hello 下列範例顯示如何 tooattach OS 和資料磁碟加密 Vm。</span><span class="sxs-lookup"><span data-stu-id="d6806-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="d6806-261">受管理、未加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d6806-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="d6806-262">對於受管理的非加密的 Vm，您將需要從 blob 儲存體，toocreate 管理磁碟，然後將附加 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="d6806-263">深入資訊，請參閱 hello 文章[附加資料磁碟 tooa Windows VM 使用 PowerShell](../virtual-machines/windows/attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d6806-264">hello 下列程式碼範例顯示如何 tooattach hello 的受管理的非加密 Vm 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="d6806-265">受管理的已加密 VM (BEK 和 KEK)</span><span class="sxs-lookup"><span data-stu-id="d6806-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="d6806-266">對於受管理的加密 Vm （使用 BEK 和 KEK 加密），您將需要從 blob 儲存體，toocreate 管理磁碟，然後將附加 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="d6806-267">深入資訊，請參閱 hello 文章[附加資料磁碟 tooa Windows VM 使用 PowerShell](../virtual-machines/windows/attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="d6806-268">hello 下列範例程式碼示範如何 tooattach hello 的受管理的加密 Vm 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6806-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="d6806-269">設定 hello 網路設定。</span><span class="sxs-lookup"><span data-stu-id="d6806-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="d6806-270">建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d6806-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="d6806-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6806-271">Next steps</span></span>
<span data-ttu-id="d6806-272">如果您偏好 toouse PowerShell tooengage 與您的 Azure 資源，請參閱 hello PowerShell 文件：[部署和管理適用於 Windows Server 的備份](backup-client-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="d6806-273">如果您管理 DPM 備份，請參閱 hello 文章[部署和管理 DPM 的備份](backup-dpm-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="d6806-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="d6806-274">這兩篇文章都有適用於 Resource Manager 部署和傳統部署的版本。</span><span class="sxs-lookup"><span data-stu-id="d6806-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
