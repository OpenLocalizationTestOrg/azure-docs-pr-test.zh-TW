---
title: "aaaDeploy 及管理 Azure Vm 使用 PowerShell 備份 |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理使用 PowerShell 的 Azure 備份。"
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
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="47679-103">使用虛擬機器 AzureRM.Backup cmdlet tooback</span><span class="sxs-lookup"><span data-stu-id="47679-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47679-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="47679-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="47679-105">傳統</span><span class="sxs-lookup"><span data-stu-id="47679-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="47679-106">本文將說明如何備份及修復 Azure Vm 的 toouse Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="47679-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="47679-107">Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。</span><span class="sxs-lookup"><span data-stu-id="47679-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="47679-108">本文說明如何使用 hello 傳統部署模型 tooback 資料 tooa 備份保存庫註冊。</span><span class="sxs-lookup"><span data-stu-id="47679-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="47679-109">如果您不在您的訂用帳戶中建立備份保存庫，請參閱這篇文章，hello 資源管理員版本[虛擬機器使用 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="47679-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="47679-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="47679-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47679-111">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="47679-112">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="47679-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="47679-113">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="47679-114">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="47679-115">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="47679-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="47679-116">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="47679-117">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="47679-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="47679-118">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47679-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="47679-119">概念</span><span class="sxs-lookup"><span data-stu-id="47679-119">Concepts</span></span>
<span data-ttu-id="47679-120">這篇文章會提供特定 toohello PowerShell cmdlet 使用 tooback 虛擬機器資訊。</span><span class="sxs-lookup"><span data-stu-id="47679-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="47679-121">如需有關保護 Azure VM 的基本資訊，請參閱 [Plan your VM backup infrastructure in Azure (在 Azure 中規劃 VM 備份基礎結構)](backup-azure-vms-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="47679-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47679-122">開始之前，閱讀 hello[必要條件](backup-azure-vms-prepare.md)需要使用 Azure 備份 」 和 「 hello toowork[限制](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)hello 目前 VM 備份解決方案。</span><span class="sxs-lookup"><span data-stu-id="47679-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="47679-123">toouse PowerShell 實際上，需要目前 toounderstand hello 階層的物件和從哪裡 toostart。</span><span class="sxs-lookup"><span data-stu-id="47679-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![物件階層](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="47679-125">hello 兩個最重要的流程會啟用保護的 vm，並從復原點還原資料。</span><span class="sxs-lookup"><span data-stu-id="47679-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="47679-126">這篇文章 hello 重點是 toohelp 您變得家 hello PowerShell cmdlet tooenable 使用這兩種情況。</span><span class="sxs-lookup"><span data-stu-id="47679-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="47679-127">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="47679-127">Setup and Registration</span></span>
<span data-ttu-id="47679-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="47679-128">toobegin:</span></span>

1. <span data-ttu-id="47679-129">[下載最新的 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需最低版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="47679-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="47679-130">輸入下列命令的 hello 尋找可用的 hello Azure 備份的 PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="47679-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="47679-131">hello 下列安裝和註冊工作可以自動化使用 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="47679-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="47679-132">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="47679-132">Create a backup vault</span></span>
* <span data-ttu-id="47679-133">Hello Vm 向 hello Azure 備份服務</span><span class="sxs-lookup"><span data-stu-id="47679-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="47679-134">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="47679-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="47679-135">Hello 第一次使用 Azure Backup 的客戶，您需要 tooregister hello Azure 備份提供者 toobe 搭配您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="47679-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="47679-136">這可藉由執行下列命令的 hello： 暫存器 AzureRmResourceProvider ProviderNamespace"Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="47679-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="47679-137">您可以建立新的備份保存庫使用 hello**新增 AzureRmBackupVault** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="47679-138">hello 備份保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。</span><span class="sxs-lookup"><span data-stu-id="47679-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="47679-139">在提升權限的 Azure PowerShell 主控台中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="47679-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="47679-140">您可以取得一份所有 hello 備份保存庫中指定的訂用帳戶使用 hello **Get AzureRmBackupVault** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="47679-141">它是方便 toostore hello 備份保存庫物件放入變數中。</span><span class="sxs-lookup"><span data-stu-id="47679-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="47679-142">做為輸入，許多 Azure Backup cmdlet 需要 hello 保存庫的物件。</span><span class="sxs-lookup"><span data-stu-id="47679-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="47679-143">註冊 hello Vm</span><span class="sxs-lookup"><span data-stu-id="47679-143">Registering hello VMs</span></span>
<span data-ttu-id="47679-144">hello 第一個步驟設定 Azure backup 備份是 tooregister 電腦或 VM 的 Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="47679-145">hello**暫存器 AzureRmBackupContainer** cmdlet 會採用 hello Azure IaaS 虛擬機器輸入的資訊與 hello 指定保存庫上登錄它。</span><span class="sxs-lookup"><span data-stu-id="47679-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="47679-146">hello 註冊作業會關聯 hello 備份保存庫中的 hello Azure 虛擬機器，並追蹤透過 hello 備份生命週期 hello VM。</span><span class="sxs-lookup"><span data-stu-id="47679-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="47679-147">以 hello Azure 備份服務註冊您的 VM 建立最上層的容器物件。</span><span class="sxs-lookup"><span data-stu-id="47679-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="47679-148">容器通常包含多個項目，可以備份，但是在 hello 案例中的 Vm 會 hello 容器只能有一個備份的項目。</span><span class="sxs-lookup"><span data-stu-id="47679-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="47679-149">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="47679-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="47679-150">建立保護原則</span><span class="sxs-lookup"><span data-stu-id="47679-150">Create a protection policy</span></span>
<span data-ttu-id="47679-151">不強制 toocreate 新 Vm 的保護原則 toostart 備份。</span><span class="sxs-lookup"><span data-stu-id="47679-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="47679-152">hello 保存庫隨附 「 '預設原則' 是使用的 tooquickly 啟用保護，且與 hello 右邊的詳細資料然後稍後編輯。</span><span class="sxs-lookup"><span data-stu-id="47679-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="47679-153">您可以取得一份提供 hello 保存庫中的 hello 原則使用 hello **Get AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="47679-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="47679-154">在 PowerShell 中的 hello BackupTime 欄位的 hello 時區為 UTC。</span><span class="sxs-lookup"><span data-stu-id="47679-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="47679-155">不過，當 hello 備份時間所示為 hello Azure 入口網站，hello 時區是對齊的 tooyour 以及 hello UTC 位移的本機系統。</span><span class="sxs-lookup"><span data-stu-id="47679-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="47679-156">備份原則至少與一個保留原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="47679-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="47679-157">hello 保留原則會定義復原點保留多久向 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="47679-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="47679-158">hello**新增 AzureRmBackupRetentionPolicy** cmdlet 會建立 PowerShell 物件的保留原則資訊。</span><span class="sxs-lookup"><span data-stu-id="47679-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="47679-159">這些保留原則物件會當做輸入 toohello*新增 AzureRmBackupProtectionPolicy* cmdlet，或直接與 hello*啟用 AzureRmBackupProtection* cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="47679-160">備份原則會定義時間和頻率 hello 備份的項目完成。</span><span class="sxs-lookup"><span data-stu-id="47679-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="47679-161">hello**新增 AzureRmBackupProtectionPolicy** cmdlet 會建立保留的備份原則資訊的 PowerShell 物件。</span><span class="sxs-lookup"><span data-stu-id="47679-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="47679-162">hello 備份原則時，會輸入 toohello*啟用 AzureRmBackupProtection* cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="47679-163">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="47679-163">Enable protection</span></span>
<span data-ttu-id="47679-164">啟用保護牽涉到兩個物件-hello 項目和 hello 原則和兩個需要 toobelong toohello 相同保存庫。</span><span class="sxs-lookup"><span data-stu-id="47679-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="47679-165">一旦 hello 原則已與 hello 項目相關聯，hello 備份工作流程會開始運作在 hello 定義的排程。</span><span class="sxs-lookup"><span data-stu-id="47679-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="47679-166">初始備份</span><span class="sxs-lookup"><span data-stu-id="47679-166">Initial backup</span></span>
<span data-ttu-id="47679-167">hello 備份排程會負責種 hello 完整初始複製 hello 項目的 hello 累加複製 hello 後續備份。</span><span class="sxs-lookup"><span data-stu-id="47679-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="47679-168">不過，如果您想 tooforce hello 初始備份 toohappen 在一段時間，或甚至立即然後使用 hello**備份 AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="47679-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="47679-169">hello 時區的 hello StartTime 和 EndTime 欄位顯示在 PowerShell 中為 UTC。</span><span class="sxs-lookup"><span data-stu-id="47679-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="47679-170">不過，當 hello 類似的資訊會顯示 hello Azure 入口網站，hello 時區是對齊的 tooyour 本機系統時鐘。</span><span class="sxs-lookup"><span data-stu-id="47679-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="47679-171">監視備份工作</span><span class="sxs-lookup"><span data-stu-id="47679-171">Monitoring a backup job</span></span>
<span data-ttu-id="47679-172">Azure 備份中長時間執行的大部分作業都模擬成工作。</span><span class="sxs-lookup"><span data-stu-id="47679-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="47679-173">這使得輕鬆 tootrack 進度而不需要隨時都能 tookeep hello Azure 入口網站開啟。</span><span class="sxs-lookup"><span data-stu-id="47679-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="47679-174">tooget hello 的最新狀態為進行中工作時，使用 hello **Get AzureRmBackupJob** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="47679-175">而不是輪詢-這是不需要額外的程式碼-完成這些工作是簡單 toouse hello**等候 AzureRmBackupJob** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="47679-176">指令碼中使用時，hello 指令程式將會暫停 hello 執行，直到 hello 作業完成或 hello 可讓您指定逾時值為止。</span><span class="sxs-lookup"><span data-stu-id="47679-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="47679-177">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="47679-177">Restore an Azure VM</span></span>
<span data-ttu-id="47679-178">在訂單 toorestore 備份資料，您需 tooidentify hello 備份項目和 hello 復原點存 hello 時間點資料。</span><span class="sxs-lookup"><span data-stu-id="47679-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="47679-179">這項資訊是提供的 toohello 還原 AzureRmBackupItem cmdlet tooinitiate hello 保存庫 toohello 客戶的帳戶中的資料的還原。</span><span class="sxs-lookup"><span data-stu-id="47679-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="47679-180">選取 hello VM</span><span class="sxs-lookup"><span data-stu-id="47679-180">Select hello VM</span></span>
<span data-ttu-id="47679-181">tooget hello PowerShell 物件，可識別 hello 正確的備份項目，您需要從 hello 保存庫中的 hello 容器 toostart，由上至下物件階層架構。</span><span class="sxs-lookup"><span data-stu-id="47679-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="47679-182">代表 hello VM，使用 hello tooselect hello 容器**Get AzureRmBackupContainer** cmdlet 並使用管線傳送該 toohello **Get AzureRmBackupItem** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="47679-183">選擇復原點</span><span class="sxs-lookup"><span data-stu-id="47679-183">Choose a recovery point</span></span>
<span data-ttu-id="47679-184">您現在可以列出所有 hello 復原點的 hello 備份項目使用 hello **Get AzureRmBackupRecoveryPoint** cmdlet，然後選擇 hello 復原點 toorestore。</span><span class="sxs-lookup"><span data-stu-id="47679-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="47679-185">使用者通常會選擇最新的 hello *AppConsistent*點 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="47679-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="47679-186">hello 變數```$rp```是陣列的復原點的 hello 選取備份項目，以相反順序排序的時間-hello 最新的復原點是在索引 0。</span><span class="sxs-lookup"><span data-stu-id="47679-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="47679-187">使用標準的 PowerShell 陣列索引 toopick hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="47679-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="47679-188">例如：```$rp[0]```會選取 hello 最新的復原點。</span><span class="sxs-lookup"><span data-stu-id="47679-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="47679-189">還原磁碟</span><span class="sxs-lookup"><span data-stu-id="47679-189">Restoring disks</span></span>
<span data-ttu-id="47679-190">沒有完成透過 hello Azure 入口網站和 Azure PowerShell，hello 還原作業之間的主要差異。</span><span class="sxs-lookup"><span data-stu-id="47679-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="47679-191">使用 PowerShell，hello 還原作業會在還原的 hello 磁碟和組態資訊從 hello 復原點停止。</span><span class="sxs-lookup"><span data-stu-id="47679-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="47679-192">不會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="47679-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="47679-193">hello 還原 AzureRmBackupItem 並不會建立 VM。</span><span class="sxs-lookup"><span data-stu-id="47679-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="47679-194">它只會還原 hello 磁碟 toohello 指定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="47679-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="47679-195">這不是 hello hello Azure 入口網站中，將會經歷相同的行為。</span><span class="sxs-lookup"><span data-stu-id="47679-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="47679-196">您可以取得 hello 詳細資料的 hello 還原作業使用 hello **Get AzureRmBackupJobDetails** cmdlet hello 還原作業完成。</span><span class="sxs-lookup"><span data-stu-id="47679-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="47679-197">hello *ErrorDetails*屬性會有 hello 資訊所需 toorebuild hello VM。</span><span class="sxs-lookup"><span data-stu-id="47679-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="47679-198">建置 hello VM</span><span class="sxs-lookup"><span data-stu-id="47679-198">Build hello VM</span></span>
<span data-ttu-id="47679-199">建置 hello VM 超出 hello 還原磁碟，才可以使用 hello 較舊的 Azure 服務管理 PowerShell cmdlet，hello 新的 Azure 資源管理員範本，或甚至使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="47679-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="47679-200">在簡單的範例，我們將示範如何 tooget 該處使用 hello Azure 服務管理 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="47679-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="47679-201">如需有關如何將 VM 從 hello toobuild 還原磁碟的詳細資訊，請閱讀下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="47679-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="47679-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="47679-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="47679-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="47679-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="47679-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="47679-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="47679-205">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="47679-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="47679-206">1.取得 hello 作業子工作的完成狀態</span><span class="sxs-lookup"><span data-stu-id="47679-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="47679-207">tootrack hello 個別的子工作的完成狀態，您可以使用 hello **Get AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="47679-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="47679-208">2.建立備份作業的每日/每週報表</span><span class="sxs-lookup"><span data-stu-id="47679-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="47679-209">系統管理員通常會想的 tooknow hello 過去 24 小時，有哪些備份作業執行 hello 的這些備份工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="47679-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="47679-210">此外，hello 傳輸的資料量會讓系統管理員的方式 tooestimate 他們每月的資料使用量。</span><span class="sxs-lookup"><span data-stu-id="47679-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="47679-211">下列指令碼 hello 會提取 hello 的 hello Azure 備份服務的未經處理資料，並顯示 hello PowerShell 主控台中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="47679-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
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

<span data-ttu-id="47679-212">如果您想 tooadd 圖表功能 toothis 報表輸出時，了解從 hello TechNet 部落格文章[圖表使用 PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="47679-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="47679-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47679-213">Next steps</span></span>
<span data-ttu-id="47679-214">如果您喜歡使用 PowerShell tooengage 與您的 Azure 資源，請參閱 hello PowerShell 文件保護 Windows Server[部署和管理適用於 Windows Server 的備份](backup-client-automation-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="47679-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="47679-215">另請參閱管理 DPM 備份的 PowerShell 文章：[部署和管理 DPM 的備份](backup-dpm-automation-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="47679-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="47679-216">這兩篇文章都有適用於 Resource Manager 部署以及傳統部署的版本。</span><span class="sxs-lookup"><span data-stu-id="47679-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
