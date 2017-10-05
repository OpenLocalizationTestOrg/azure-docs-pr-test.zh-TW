---
title: "使用 PowerShell 部署和管理 Resource Manager 部署之 VM 的備份 | Microsoft Docs"
description: "使用 PowerShell，在 Azure 中部署和管理 Resource Manager 部署之 VM 的備份"
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="45980-103">使用 AzureRM.RecoveryServices.Backup Cmdlet 備份虛擬機器</span><span class="sxs-lookup"><span data-stu-id="45980-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45980-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="45980-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="45980-105">傳統</span><span class="sxs-lookup"><span data-stu-id="45980-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="45980-106">本文說明如何使用 Azure PowerShell Cmdlet 從復原服務保存庫備份和復原 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="45980-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="45980-107">復原服務保存庫是一項 Azure Resource Manager 資源，可用來保護 Azure 備份和 Azure Site Recovery 服務中的資料和資產。</span><span class="sxs-lookup"><span data-stu-id="45980-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="45980-108">您可以使用復原服務保存庫，來保護 Azure Service Manager 部署的 VM 以及 Azure Resource Manager 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="45980-109">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="45980-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="45980-110">本文章適用於以 Resource Manager 模型建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="45980-111">本文章會引導您逐步完成使用 PowerShell 來保護 VM，以及從復原點還原資料的步驟。</span><span class="sxs-lookup"><span data-stu-id="45980-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="45980-112">概念</span><span class="sxs-lookup"><span data-stu-id="45980-112">Concepts</span></span>
<span data-ttu-id="45980-113">如果您不熟悉 Azure 備份服務，若需服務的概觀，請參閱[何謂 Azure 備份？](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="45980-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="45980-114">開始之前，請確定您已了解使用 Azure 備份需要的必要條件的重點，以及目前的 VM 備份解決方案的限制。</span><span class="sxs-lookup"><span data-stu-id="45980-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="45980-115">若要有效地使用 PowerShell，就必須了解物件的階層及從何處開始。</span><span class="sxs-lookup"><span data-stu-id="45980-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![復原服務物件階層](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="45980-117">若要檢視 AzureRm.RecoveryServices.Backup PowerShell Cmdlet 參考文件，請參閱 Azure 文件庫中的 [Azure 備份 - 復原服務 Cmdlet](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) 。</span><span class="sxs-lookup"><span data-stu-id="45980-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="45980-118">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="45980-118">Setup and Registration</span></span>
<span data-ttu-id="45980-119">開始：</span><span class="sxs-lookup"><span data-stu-id="45980-119">To begin:</span></span>

1. <span data-ttu-id="45980-120">[下載最新版本的 PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (所需的最低版本為：1.4.0)</span><span class="sxs-lookup"><span data-stu-id="45980-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="45980-121">輸入下列命令，以找到可用的 Azure 備份 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="45980-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="45980-122">PowerShell 可以自動化下列工作：</span><span class="sxs-lookup"><span data-stu-id="45980-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="45980-123">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="45980-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="45980-124">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="45980-124">Back up Azure VMs</span></span>
* <span data-ttu-id="45980-125">觸發備份作業</span><span class="sxs-lookup"><span data-stu-id="45980-125">Trigger a backup job</span></span>
* <span data-ttu-id="45980-126">監視備份作業</span><span class="sxs-lookup"><span data-stu-id="45980-126">Monitor a backup job</span></span>
* <span data-ttu-id="45980-127">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="45980-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="45980-128">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="45980-128">Create a recovery services vault</span></span>
<span data-ttu-id="45980-129">下列步驟將引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="45980-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="45980-130">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="45980-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="45980-131">如果您是第一次使用 Azure 備份，您必須使用 **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** Cmdlet，利用您的訂用帳戶來註冊 Azure 復原服務提供者。</span><span class="sxs-lookup"><span data-stu-id="45980-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="45980-132">復原服務保存庫是一項 Resource Manager 資源，因此您必須將它放在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="45980-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="45980-133">您可以使用現有的資源群組，或使用 **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** Cmdlet 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="45980-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="45980-134">建立資源群組時，請指定資源群組的名稱與位置。</span><span class="sxs-lookup"><span data-stu-id="45980-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="45980-135">使用 **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** Cmdlet 來建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="45980-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="45980-136">請務必為保存庫指定與用於資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="45980-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="45980-137">指定要使用的儲存體備援類型；您可以使用[本地備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) 或[異地備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="45980-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="45980-138">下列範例顯示 testvault 的 -BackupStorageRedundancy 選項設為 GeoRedundant。</span><span class="sxs-lookup"><span data-stu-id="45980-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="45980-139">許多 Azure 備份 Cmdlet 都需要將復原服務保存庫物件當做輸入。</span><span class="sxs-lookup"><span data-stu-id="45980-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="45980-140">基於這個理由，將備份復原服務保存庫物件儲存在變數中會是方便的做法。</span><span class="sxs-lookup"><span data-stu-id="45980-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="45980-141">在訂用帳戶中檢視保存庫</span><span class="sxs-lookup"><span data-stu-id="45980-141">View the vaults in a subscription</span></span>
<span data-ttu-id="45980-142">使用 **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** 來檢視目前訂用帳戶中所有保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="45980-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="45980-143">您可以使用此命令來檢查是否已建立新的保存庫，或查看訂用帳戶中可用的保存庫。</span><span class="sxs-lookup"><span data-stu-id="45980-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="45980-144">執行 Get-AzureRmRecoveryServicesVault 命令來檢視訂用帳戶中的所有保存庫。</span><span class="sxs-lookup"><span data-stu-id="45980-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="45980-145">下列範例顯示每個保存庫所顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="45980-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="45980-146">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="45980-146">Back up Azure VMs</span></span>
<span data-ttu-id="45980-147">使用復原服務保存庫來保護您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45980-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="45980-148">在您套用保護之前，請設定保存庫內容 (保存庫中所保護的資料類型)，並確認保護原則。</span><span class="sxs-lookup"><span data-stu-id="45980-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="45980-149">保護原則是備份工作何時執行，以及每個備份快照之保留時間長度的排程。</span><span class="sxs-lookup"><span data-stu-id="45980-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="45980-150">設定保存庫內容</span><span class="sxs-lookup"><span data-stu-id="45980-150">Set vault context</span></span>
<span data-ttu-id="45980-151">在 VM 上啟用保護之前，請使用 **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  來設定保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="45980-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="45980-152">保存庫內容設定之後就會套用至所有後續的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45980-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="45980-153">下列範例會設定保存庫 *testvault* 的保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="45980-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="45980-154">建立保護原則</span><span class="sxs-lookup"><span data-stu-id="45980-154">Create a protection policy</span></span>
<span data-ttu-id="45980-155">當您建立復原服務保存庫時，它會隨附預設的保護和保留原則。</span><span class="sxs-lookup"><span data-stu-id="45980-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="45980-156">預設保護原則會在每天的指定時間觸發備份作業。</span><span class="sxs-lookup"><span data-stu-id="45980-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="45980-157">預設保留原則會將每日復原點保留 30 天。</span><span class="sxs-lookup"><span data-stu-id="45980-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="45980-158">您可以使用預設原則來快速地保護 VM，並在之後編輯原則的各種詳細資料。</span><span class="sxs-lookup"><span data-stu-id="45980-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="45980-159">使用 **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** 來檢視保存庫中的保護原則。</span><span class="sxs-lookup"><span data-stu-id="45980-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="45980-160">您可以使用此 Cmdlet 來取得特定的原則，或檢視與工作負載類型相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="45980-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="45980-161">下列範例會取得工作負載類型 AzureVM 的原則。</span><span class="sxs-lookup"><span data-stu-id="45980-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="45980-162">PowerShell 中 BackupTime 欄位的時區是 UTC。</span><span class="sxs-lookup"><span data-stu-id="45980-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="45980-163">不過，當備份時間顯示在 Azure 入口網站中時，系統會根據您的當地時區調整時間。</span><span class="sxs-lookup"><span data-stu-id="45980-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="45980-164">備份保護原則至少與一個保留原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="45980-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="45980-165">保留原則會定義復原點在被刪除之前要保留多久。</span><span class="sxs-lookup"><span data-stu-id="45980-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="45980-166">使用 **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** 檢視預設保留原則。</span><span class="sxs-lookup"><span data-stu-id="45980-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="45980-167">同樣地，您可以使用 **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** 取得預設排程原則。</span><span class="sxs-lookup"><span data-stu-id="45980-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="45980-168">**[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** Cmdlet 會建立 PowerShell 物件來保存備份原則資訊。</span><span class="sxs-lookup"><span data-stu-id="45980-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="45980-169">排程和保留原則物件可當作 **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** Cmdlet 的輸入。</span><span class="sxs-lookup"><span data-stu-id="45980-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="45980-170">下列範例會將排程原則和保留原則儲存在變數中。</span><span class="sxs-lookup"><span data-stu-id="45980-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="45980-171">這個範例在建立保護原則 *NewPolicy* 時會使用這些變數來定義參數。</span><span class="sxs-lookup"><span data-stu-id="45980-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="45980-172">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="45980-172">Enable protection</span></span>
<span data-ttu-id="45980-173">在定義備份保護原則之後，您仍然必須對項目啟用此原則。</span><span class="sxs-lookup"><span data-stu-id="45980-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="45980-174">使用 **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** 來啟用保護。</span><span class="sxs-lookup"><span data-stu-id="45980-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="45980-175">啟用保護需要兩個物件：項目和原則。</span><span class="sxs-lookup"><span data-stu-id="45980-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="45980-176">一旦原則與保存庫相關聯，備份工作流程將依照原則排程定義的時間觸發。</span><span class="sxs-lookup"><span data-stu-id="45980-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="45980-177">下列範例會使用原則 NewPolicy 來對項目 V2VM 啟用保護。</span><span class="sxs-lookup"><span data-stu-id="45980-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="45980-178">在非加密 Resource Manager VM 上啟用保護</span><span class="sxs-lookup"><span data-stu-id="45980-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="45980-179">若要在加密的 VM 上 (使用 BEK 與 KEK 加密) 啟用保護，您必須提供權限讓 Azure 備份服務讀取金鑰保存庫中的金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="45980-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="45980-180">若要在加密的 VM 上 (只使用 BEK 加密) 啟用保護，您必須提供權限讓 Azure 備份服務讀取金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="45980-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="45980-181">如果您使用 Azure Government 雲端，請在 [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) Cmdlet 中使用 ff281ffe-705c-4f53-9f37-a40e6f2c68f3 作為 **-ServicePrincipalName** 參數的值。</span><span class="sxs-lookup"><span data-stu-id="45980-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="45980-182">若為傳統 VM</span><span class="sxs-lookup"><span data-stu-id="45980-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="45980-183">修改保護原則</span><span class="sxs-lookup"><span data-stu-id="45980-183">Modify a protection policy</span></span>
<span data-ttu-id="45980-184">若要修改保護原則，請使用 [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) 修改 SchedulePolicy 或 RetentionPolicy 物件。</span><span class="sxs-lookup"><span data-stu-id="45980-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="45980-185">下列範例會將復原點保留變更為 365 天。</span><span class="sxs-lookup"><span data-stu-id="45980-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="45980-186">觸發備份</span><span class="sxs-lookup"><span data-stu-id="45980-186">Trigger a backup</span></span>
<span data-ttu-id="45980-187">您可以使用 **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** 來觸發備份作業。</span><span class="sxs-lookup"><span data-stu-id="45980-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="45980-188">如果是初始備份，則會是完整備份。</span><span class="sxs-lookup"><span data-stu-id="45980-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="45980-189">後續的備份會採用增量複本。</span><span class="sxs-lookup"><span data-stu-id="45980-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="45980-190">在觸發備份作業之前，請務必使用 **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** 來設定保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="45980-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="45980-191">下列範例假設已設定保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="45980-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="45980-192">PowerShell 中 StartTime 和 EndTime 欄位的時區是 UTC。</span><span class="sxs-lookup"><span data-stu-id="45980-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="45980-193">不過，當時間顯示在 Azure 入口網站中時，系統會根據您的當地時區調整時間。</span><span class="sxs-lookup"><span data-stu-id="45980-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="45980-194">監視備份工作</span><span class="sxs-lookup"><span data-stu-id="45980-194">Monitoring a backup job</span></span>
<span data-ttu-id="45980-195">您不必透過 Azure 入口網站就可以監視長時間執行的作業，例如備份作業。</span><span class="sxs-lookup"><span data-stu-id="45980-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="45980-196">若要取得進行中作業的狀態，請使用 **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45980-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="45980-197">此 Cmdlet 會取得特定保存庫 (在保存庫內容中指定) 的備份作業。</span><span class="sxs-lookup"><span data-stu-id="45980-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="45980-198">下列範例會以陣列形式取得進行中作業的狀態，並將狀態儲存在 $joblist 變數中。</span><span class="sxs-lookup"><span data-stu-id="45980-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="45980-199">因為需要額外的程式碼且並非必要，所以不輪詢這些作業是否完成 - 而是改用 **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45980-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="45980-200">此 Cmdlet 會暫停執行，直到工作完成，或達到指定的逾時值為止。</span><span class="sxs-lookup"><span data-stu-id="45980-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="45980-201">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="45980-201">Restore an Azure VM</span></span>
<span data-ttu-id="45980-202">使用 Azure 入口網站還原 VM 和使用 PowerShell 還原 VM 之間有一個主要差異。</span><span class="sxs-lookup"><span data-stu-id="45980-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="45980-203">使用 PowerShell 時，建立磁碟和復原點組態資訊之後，還原作業即完成。</span><span class="sxs-lookup"><span data-stu-id="45980-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="45980-204">還原作業不會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45980-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="45980-205">若要從磁碟建立虛擬機器，請參閱[從預存的磁碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-stored-disks)一節。</span><span class="sxs-lookup"><span data-stu-id="45980-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="45980-206">還原 Azure VM 的基本步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="45980-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="45980-207">選取 VM</span><span class="sxs-lookup"><span data-stu-id="45980-207">Select the VM</span></span>
* <span data-ttu-id="45980-208">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="45980-208">Choose a recovery point</span></span>
* <span data-ttu-id="45980-209">還原磁碟</span><span class="sxs-lookup"><span data-stu-id="45980-209">Restore the disks</span></span>
* <span data-ttu-id="45980-210">從預存的磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="45980-210">Create the VM from stored disks</span></span>

<span data-ttu-id="45980-211">下圖顯示從 RecoveryServicesVault 到 BackupRecoveryPoint 的物件階層。</span><span class="sxs-lookup"><span data-stu-id="45980-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![顯示 BackupContainer 的復原服務物件階層](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="45980-213">若要還原備份資料，請識別已備份的項目和保存時間點資料的復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="45980-214">使用 **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** Cmdlet 將資料從保存庫還原至客戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="45980-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="45980-215">選取 VM</span><span class="sxs-lookup"><span data-stu-id="45980-215">Select the VM</span></span>
<span data-ttu-id="45980-216">若要取得可識別正確備份項目的 PowerShell 物件，請從保存庫中的容器開始，向下深入物件階層。</span><span class="sxs-lookup"><span data-stu-id="45980-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="45980-217">若要選取代表 VM 的容器，請使用 **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** Cmdlet，並透過管道將它傳送到 **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45980-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="45980-218">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="45980-218">Choose a recovery point</span></span>
<span data-ttu-id="45980-219">使用 **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** Cmdlet 來列出備份項目的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="45980-220">接下來選擇要還原的復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="45980-221">如果您不確定要使用哪一個復原點，在清單中選擇最近的 RecoveryPointType = AppConsistent 點是好的做法。</span><span class="sxs-lookup"><span data-stu-id="45980-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="45980-222">在下列指令碼中，變數 **$rp** 是選取的備份項目在過去七天的復原點陣列。</span><span class="sxs-lookup"><span data-stu-id="45980-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="45980-223">陣列是以相反時間順序排序，最新復原點位於索引 0。</span><span class="sxs-lookup"><span data-stu-id="45980-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="45980-224">使用標準 PowerShell 陣列索引來挑選復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="45980-225">在範例中，$rp[0] 會選取最新的復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="45980-226">還原磁碟</span><span class="sxs-lookup"><span data-stu-id="45980-226">Restore the disks</span></span>
<span data-ttu-id="45980-227">使用 **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** Cmdlet 將備份項目的資料和設定還原至復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="45980-228">在您識別復原點之後，請使用它作為 **-RecoveryPoint** 參數的值。</span><span class="sxs-lookup"><span data-stu-id="45980-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="45980-229">在先前的範例程式碼中，**$rp[0]** 是要使用的復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="45980-230">在接下來的範例程式碼中，**$rp[0]** 是要用來還原磁碟的復原點。</span><span class="sxs-lookup"><span data-stu-id="45980-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="45980-231">還原磁碟和設定資訊：</span><span class="sxs-lookup"><span data-stu-id="45980-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="45980-232">使用 **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** Cmdlet 來等候還原作業完成。</span><span class="sxs-lookup"><span data-stu-id="45980-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="45980-233">完成還原作業之後，您可以使用 **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** Cmdlet 來取得還原作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="45980-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="45980-234">JobDetails 屬性具有重建 VM 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="45980-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="45980-235">還原磁碟之後，請繼續下一節來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="45980-236">從還原的磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="45980-236">Create a VM from restored disks</span></span>
<span data-ttu-id="45980-237">在您還原磁碟之後，使用下列步驟來從磁碟建立及設定虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45980-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="45980-238">若要從預存的磁碟建立加密的 VM，您的 Azure 角色必須具備可執行 **Microsoft.KeyVault/vaults/deploy/action** 動作的權限。</span><span class="sxs-lookup"><span data-stu-id="45980-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="45980-239">如果您的角色並沒有此權限，請使用此動作來建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="45980-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="45980-240">如需詳細資訊，請參閱 [Azure RBAC 中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="45980-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="45980-241">查詢工作詳細資料的已還原磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="45980-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="45980-242">設定 Azure 儲存體內容，並還原為 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="45980-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="45980-243">使用 JSON 組態檔來建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="45980-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="45980-244">連接作業系統磁碟與資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="45980-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="45980-245">根據您的 Vm 組態，請按一下以檢視個別的指令程式相關的連結：</span><span class="sxs-lookup"><span data-stu-id="45980-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="45980-246">非管理、 未加密的 Vm</span><span class="sxs-lookup"><span data-stu-id="45980-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="45980-247">非管理、 加密 Vm (只有 BEK)</span><span class="sxs-lookup"><span data-stu-id="45980-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="45980-248">非管理、 加密的 Vm （BEK 和 KEK）</span><span class="sxs-lookup"><span data-stu-id="45980-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="45980-249">受管理、 未加密的 Vm</span><span class="sxs-lookup"><span data-stu-id="45980-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="45980-250">受管理的加密 Vm （BEK 和 KEK）</span><span class="sxs-lookup"><span data-stu-id="45980-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="45980-251">未受管理、未加密的 VM</span><span class="sxs-lookup"><span data-stu-id="45980-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="45980-252">如果是未受管理、未加密的 VM，請使用下列範例。</span><span class="sxs-lookup"><span data-stu-id="45980-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="45980-253">未受管理的已加密 VM (僅限 BEK)</span><span class="sxs-lookup"><span data-stu-id="45980-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="45980-254">如果是未受管理的已加密 VM (只使用 BEK 加密)，您需要先將密碼還原至金鑰保存庫，才可以連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="45980-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="45980-255">如需詳細資訊，請參閱[從 Azure 備份復原點還原已加密的虛擬機器](backup-azure-restore-key-secret.md)一文。</span><span class="sxs-lookup"><span data-stu-id="45980-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="45980-256">下列範例示範如何將 OS 和資料磁碟連結至已加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="45980-257">未受管理的已加密 VM (BEK 和 KEK)</span><span class="sxs-lookup"><span data-stu-id="45980-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="45980-258">如果是未受管理的已加密 VM (使用 BEK 和 KEK 加密)，您需要先將金鑰和密碼還原至金鑰保存庫，才可以連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="45980-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="45980-259">如需詳細資訊，請參閱[從 Azure 備份復原點還原已加密的虛擬機器](backup-azure-restore-key-secret.md)一文。</span><span class="sxs-lookup"><span data-stu-id="45980-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="45980-260">下列範例示範如何將 OS 和資料磁碟連結至已加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="45980-261">受管理、未加密的 VM</span><span class="sxs-lookup"><span data-stu-id="45980-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="45980-262">對於受管理的未加密 VM，您必須從 blob 儲存體建立受控磁碟，然後連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="45980-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="45980-263">如需深入的資訊，請參閱[使用 PowerShell 將資料磁碟連結至 Windows VM](../virtual-machines/windows/attach-disk-ps.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="45980-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="45980-264">下列範例程式碼示範如何將資料磁碟連結至受管理的未加密 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="45980-265">受管理的已加密 VM (BEK 和 KEK)</span><span class="sxs-lookup"><span data-stu-id="45980-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="45980-266">對於受管理的加密 VM (使用 BEK 和 KEK 加密)，您必須從 Blob 儲存體建立受控磁碟，然後連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="45980-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="45980-267">如需深入的資訊，請參閱[使用 PowerShell 將資料磁碟連結至 Windows VM](../virtual-machines/windows/attach-disk-ps.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="45980-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="45980-268">下列範例程式碼示範如何將資料磁碟連結至受管理的加密 VM。</span><span class="sxs-lookup"><span data-stu-id="45980-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="45980-269">設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="45980-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="45980-270">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45980-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="45980-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45980-271">Next steps</span></span>
<span data-ttu-id="45980-272">如果您偏好使用 PowerShell 來與 Azure 資源互動，請參閱 PowerShell 文章：[部署和管理 Windows Server 的備份](backup-client-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="45980-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="45980-273">如果您管理 DPM 備份，請參閱[部署及管理 DPM 的備份](backup-dpm-automation.md)一文。</span><span class="sxs-lookup"><span data-stu-id="45980-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="45980-274">這兩篇文章都有適用於 Resource Manager 部署和傳統部署的版本。</span><span class="sxs-lookup"><span data-stu-id="45980-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
