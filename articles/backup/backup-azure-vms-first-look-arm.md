---
title: "初步了解：使用復原服務保存庫保護 Azure VM | Microsoft Docs"
description: "使用復原服務保存庫保護 Azure VM。 使用資源管理員部署的 Vm、 傳統部署 Vm 和 Premium 儲存體的 Vm，加密的 Vm，Vm 上管理磁碟 tooprotect 備份您的資料。 建立和註冊復原服務保存庫。 在 Azure 中註冊 VM、建立原則和保護 VM。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a><span data-ttu-id="7268b-106">備份 Azure 虛擬機器 tooRecovery 服務保存庫</span><span class="sxs-lookup"><span data-stu-id="7268b-106">Back up Azure virtual machines tooRecovery Services vaults</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7268b-107">使用復原服務保存庫保護 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-107">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="7268b-108">使用備份保存庫保護 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-108">Protect VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="7268b-109">本教學課程會帶領您完成建立復原服務保存庫，以及備份 Azure 虛擬機器 (VM) 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7268b-109">This tutorial takes you through hello steps for creating a recovery services vault and backing up an Azure virtual machine (VM).</span></span> <span data-ttu-id="7268b-110">復原服務保存庫可保護︰</span><span class="sxs-lookup"><span data-stu-id="7268b-110">Recovery services vaults protect:</span></span>

* <span data-ttu-id="7268b-111">Azure Resource Manager 部署的 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-111">Azure Resource Manager-deployed VMs</span></span>
* <span data-ttu-id="7268b-112">傳統 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-112">Classic VMs</span></span>
* <span data-ttu-id="7268b-113">標準儲存體 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-113">Standard storage VMs</span></span>
* <span data-ttu-id="7268b-114">進階儲存體 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-114">Premium storage VMs</span></span>
* <span data-ttu-id="7268b-115">在受控磁碟上執行的 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-115">VMs running on Managed Disks</span></span>
* <span data-ttu-id="7268b-116">使用 Azure 磁碟加密，搭配 BEK 與 KEK 來加密的 VM</span><span class="sxs-lookup"><span data-stu-id="7268b-116">VMs encrypted using Azure Disk Encryption, with BEK and KEK</span></span>
* <span data-ttu-id="7268b-117">使用 VSS 之 Windows VM 和使用自訂快照前與快照後指令碼之 Linux VM 的應用程式一致備份</span><span class="sxs-lookup"><span data-stu-id="7268b-117">Application consistent backup of Windows VMs using VSS and Linux VMs using custom pre-snapshot and post-snapshot scripts</span></span>

<span data-ttu-id="7268b-118">如需有關保護進階儲存體 Vm 的詳細資訊，請參閱 hello 文件，[備份和還原 Premium 儲存體 Vm](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup)。</span><span class="sxs-lookup"><span data-stu-id="7268b-118">For more information on protecting Premium storage VMs, see hello article, [Back up and Restore Premium Storage VMs](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup).</span></span> <span data-ttu-id="7268b-119">如需受控磁碟 VM 支援的詳細資訊，請參閱[備份及還原受控磁碟上的 VM](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。</span><span class="sxs-lookup"><span data-stu-id="7268b-119">For more information on support for managed disk VMs, see [Back up and restore VMs on managed disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).</span></span> <span data-ttu-id="7268b-120">如需有關 Linux VM 備份之前置和後置指令碼架構的詳細資訊，請參閱 [使用前置指令碼和後置指令碼的應用程式一致 Linux VM 備份] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。</span><span class="sxs-lookup"><span data-stu-id="7268b-120">For more information on pre and post-script framework for Linux VM backup see [Application consistent Linux VM backup using pre-script and post-script] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span>

<span data-ttu-id="7268b-121">toofind 出更多有關您備份也不能請參閱[這裡](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span><span class="sxs-lookup"><span data-stu-id="7268b-121">toofind out more about what can you backup and what you can't, refer [here](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span></span>

> [!NOTE]
> <span data-ttu-id="7268b-122">本教學課程假設您的 Azure 訂用帳戶中已有 VM，並採取措施 tooallow hello 備份服務 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="7268b-122">This tutorial assumes you already have a VM in your Azure subscription and that you have taken measures tooallow hello backup service tooaccess hello VM.</span></span>
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="7268b-123">Hello 的虛擬機器的數目視您想 tooprotect，您就可以開始從不同的起始點。</span><span class="sxs-lookup"><span data-stu-id="7268b-123">Depending on hello number of virtual machines you want tooprotect, you can begin from different starting points.</span></span> <span data-ttu-id="7268b-124">如果您想 tooback 多個虛擬機器在一個作業中，請移至 toohello 復原服務保存庫和[起始 hello 備份工作，從 hello 保存庫儀表板](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault)。</span><span class="sxs-lookup"><span data-stu-id="7268b-124">If you want tooback up multiple virtual machines in one operation, go toohello Recovery Services vault and [initiate hello backup job from hello vault dashboard](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault).</span></span> <span data-ttu-id="7268b-125">如果您想 tooback 單一的虛擬機器，您可以起始 hello 備份作業從 VM 管理刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7268b-125">If you want tooback up a single virtual machine, you can initiate hello backup job from VM management blade.</span></span>

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a><span data-ttu-id="7268b-126">設定從 hello VM 管理刀鋒視窗的 hello 備份工作</span><span class="sxs-lookup"><span data-stu-id="7268b-126">Configure hello backup job from hello VM management blade</span></span>

<span data-ttu-id="7268b-127">使用 hello hello hello Azure 入口網站中虛擬機器管理刀鋒視窗中的下列步驟 tooconfigure hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="7268b-127">Use hello following steps tooconfigure hello backup job from hello virtual machine management blade in hello Azure portal.</span></span> <span data-ttu-id="7268b-128">這些步驟不會套用 toohello hello 傳統入口網站中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7268b-128">These steps do not apply toohello virtual machines in hello classic portal.</span></span>

1. <span data-ttu-id="7268b-129">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7268b-129">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7268b-130">在 hello 中樞功能表中，按一下 **更服務**在 hello 篩選對話方塊中，輸入**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="7268b-130">On hello Hub menu, click **More Services** and in hello Filter dialog, type **Virtual machines**.</span></span> <span data-ttu-id="7268b-131">當您輸入時，篩選 hello 的資源清單。</span><span class="sxs-lookup"><span data-stu-id="7268b-131">As you type, hello list of resources filters.</span></span> <span data-ttu-id="7268b-132">當您看到虛擬機器時，請選取它。</span><span class="sxs-lookup"><span data-stu-id="7268b-132">When you see Virtual machines, select it.</span></span>

  ![在中樞功能表中，按一下 [更多服務 tooopen 文字] 對話方塊，然後輸入虛擬機器](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  <span data-ttu-id="7268b-134">中的虛擬機器 (VM) hello 訂閱 hello 清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7268b-134">hello list of virtual machines (VM) in hello subscription, appears.</span></span>

  ![Vm 的 hello 訂用帳戶中的 hello 清單隨即出現。](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. <span data-ttu-id="7268b-136">從 hello 清單中，選取 VM tooback。</span><span class="sxs-lookup"><span data-stu-id="7268b-136">From hello list, select a VM tooback up.</span></span>

  ![Vm 的 hello 訂用帳戶中的 hello 清單隨即出現。](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  <span data-ttu-id="7268b-138">當您選取 hello VM 時，hello 清單中的虛擬機器會進入 toohello 左和 hello 虛擬機器管理刀鋒視窗，hello 虛擬機器儀表板中，開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-138">When you select hello VM, hello list of virtual machines shifts toohello left, and hello virtual machine management blade and hello virtual machine dashboard, open.</span></span> </br><span data-ttu-id="7268b-139">
 ![VM 管理刀鋒視窗](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span><span class="sxs-lookup"><span data-stu-id="7268b-139">
![VM Management blade](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span></span>

4. <span data-ttu-id="7268b-140">在 hello VM 管理刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="7268b-140">On hello VM management blade, in hello **Settings** section, click **Backup**.</span></span> </br>

  ![VM 管理刀鋒視窗中的備份選項](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  <span data-ttu-id="7268b-142">hello 啟用備份刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-142">hello Enable backup blade opens.</span></span>

  ![VM 管理刀鋒視窗中的備份選項](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. <span data-ttu-id="7268b-144">Hello 復原服務保存庫中，按一下 **選取現有**hello 下拉式清單中選擇 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-144">For hello Recovery Services vault, click **Select existing** and choose hello vault from hello drop-down list.</span></span>

  ![啟用備份精靈](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  <span data-ttu-id="7268b-146">如果沒有復原服務保存庫，或您想要 toouse 新的保存庫，請按一下**建立新**並提供 hello hello 新的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="7268b-146">If there are no Recovery Services vaults, or you want toouse a new vault, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="7268b-147">新的保存庫中建立 hello 相同資源群組，而且與 hello 虛擬機器相同的位置。</span><span class="sxs-lookup"><span data-stu-id="7268b-147">A new vault is created in hello same Resource Group and same location as hello virtual machine.</span></span> <span data-ttu-id="7268b-148">如果您想 toocreate 復原服務保存庫使用不同的值，請參閱 hello 一節有關太[建立復原服務保存庫](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="7268b-148">If you want toocreate a Recovery Services vault with different values, see hello section on how too[create a recovery services vault](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).</span></span>

6. <span data-ttu-id="7268b-149">按一下 tooview hello hello 備份原則詳細資料**備份原則**。</span><span class="sxs-lookup"><span data-stu-id="7268b-149">tooview hello details of hello Backup policy, click **Backup policy**.</span></span>

  <span data-ttu-id="7268b-150">hello**備份原則**刀鋒視窗會開啟，並提供 hello 選取原則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7268b-150">hello **Backup policy** blade opens and provides hello details of hello selected policy.</span></span> <span data-ttu-id="7268b-151">如果其他原則存在，請使用 hello 下拉式功能表 toochoose 不同的備份原則。</span><span class="sxs-lookup"><span data-stu-id="7268b-151">If other policies exist, use hello drop-down menu toochoose a different backup policy.</span></span> <span data-ttu-id="7268b-152">如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="7268b-152">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="7268b-153">如需定義備份原則的指示，請參閱 [定義備份原則](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="7268b-153">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span> <span data-ttu-id="7268b-154">toosave hello 變更 toohello 備份原則，並傳回 toohello 啟用備份刀鋒視窗中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7268b-154">toosave hello changes toohello backup policy and return toohello Enable backup blade, click **OK**.</span></span>

  ![選取備份原則](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. <span data-ttu-id="7268b-156">在 hello 啟用備份刀鋒視窗中，按一下 **啟用備份**toodeploy hello 原則。</span><span class="sxs-lookup"><span data-stu-id="7268b-156">On hello Enable backup blade, click **Enable Backup** toodeploy hello policy.</span></span> <span data-ttu-id="7268b-157">部署的 hello 原則與 hello 保存庫和 hello 虛擬機器關聯。</span><span class="sxs-lookup"><span data-stu-id="7268b-157">Deploying hello policy associates it with hello vault and hello virtual machines.</span></span>

  ![啟用備份按鈕](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. <span data-ttu-id="7268b-159">您可以追蹤 hello 通知 hello 入口網站中的 hello 設定進行。</span><span class="sxs-lookup"><span data-stu-id="7268b-159">You can track hello configuration progress through hello notifications that appear in hello portal.</span></span> <span data-ttu-id="7268b-160">下列範例中的 hello 顯示部署的開始。</span><span class="sxs-lookup"><span data-stu-id="7268b-160">hello following example shows that Deployment started.</span></span>

  ![啟用備份通知](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. <span data-ttu-id="7268b-162">Hello 組態進度完成後，請在 hello VM 管理刀鋒視窗中，按一下**備份**tooopen hello 備份項目刀鋒視窗，然後檢視 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7268b-162">Once hello configuration progress has completed, on hello VM management blade, click **Backup** tooopen hello Backup Item blade and view hello details.</span></span>

  ![VM 備份項目檢視](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  <span data-ttu-id="7268b-164">Hello 初始備份完成為止，**上次備份狀態**顯示為**警告 （暫止的初始備份）**。</span><span class="sxs-lookup"><span data-stu-id="7268b-164">Until hello initial backup has completed, **Last backup status** shows as **Warning(Initial backup pending)**.</span></span> <span data-ttu-id="7268b-165">toosee hello 下一個排程的備份工作時，就會發生，在**備份原則**按一下 hello hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="7268b-165">toosee when hello next scheduled backup job occurs, under **Backup policy** click hello name of hello policy.</span></span> <span data-ttu-id="7268b-166">hello 備份原則 刀鋒視窗隨即開啟，並顯示 hello hello 排程備份的時間。</span><span class="sxs-lookup"><span data-stu-id="7268b-166">hello Backup Policy blade opens and shows hello time of hello scheduled backup.</span></span>

10. <span data-ttu-id="7268b-167">toorun 備份工作並建立 hello 初始的復原點，請在 hello 備份保存庫刀鋒視窗中按一下**備份現在**。</span><span class="sxs-lookup"><span data-stu-id="7268b-167">toorun a Backup job and create hello initial recovery point, on hello Backup vault blade click **Backup now**.</span></span>

  ![按一下 備份現在 toorun hello 初始備份](./media/backup-azure-vms-first-look-arm/backup-now.png)

  <span data-ttu-id="7268b-169">hello 立即備份 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-169">hello Backup Now blade opens.</span></span>

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. <span data-ttu-id="7268b-171">Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="7268b-171">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="7268b-173">部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。</span><span class="sxs-lookup"><span data-stu-id="7268b-173">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span>

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a><span data-ttu-id="7268b-174">設定從 復原服務保存庫的 hello hello 備份工作</span><span class="sxs-lookup"><span data-stu-id="7268b-174">Configure hello backup job from hello Recovery Services vault</span></span>
<span data-ttu-id="7268b-175">tooconfigure hello 備份工作，您完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="7268b-175">tooconfigure hello backup job, you complete hello following steps.</span></span>  

1. <span data-ttu-id="7268b-176">建立虛擬機器的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-176">Create a Recovery Services vault for a virtual machine.</span></span>
2. <span data-ttu-id="7268b-177">使用 hello Azure 入口網站 tooselect 案例中，設定備份原則，並找出項目 tooprotect。</span><span class="sxs-lookup"><span data-stu-id="7268b-177">Use hello Azure portal tooselect a Scenario, set a Backup policy, and identify items tooprotect.</span></span>
3. <span data-ttu-id="7268b-178">執行 hello 初始備份。</span><span class="sxs-lookup"><span data-stu-id="7268b-178">Run hello initial backup.</span></span>

## <a name="create-a-recovery-services-vault-for-a-vm"></a><span data-ttu-id="7268b-179">建立 VM 的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-179">Create a recovery services vault for a VM</span></span>
<span data-ttu-id="7268b-180">復原服務保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。</span><span class="sxs-lookup"><span data-stu-id="7268b-180">A Recovery Services vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="7268b-181">hello 復原服務保存庫也包含 hello 備份原則套用 toohello 受保護 Vm。</span><span class="sxs-lookup"><span data-stu-id="7268b-181">hello Recovery Services vault also contains hello backup policy applied toohello protected VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="7268b-182">備份 VM 是本機程序。</span><span class="sxs-lookup"><span data-stu-id="7268b-182">Backing up VMs is a local process.</span></span> <span data-ttu-id="7268b-183">您無法從一個位置 tooa 復原服務保存庫，在另一個位置來備份 Vm。</span><span class="sxs-lookup"><span data-stu-id="7268b-183">You cannot back up VMs from one location tooa Recovery Services vault in another location.</span></span> <span data-ttu-id="7268b-184">因此，對於每個已備份的 Vm toobe 的 Azure 位置，至少一個復原服務保存庫必須存在於該位置。</span><span class="sxs-lookup"><span data-stu-id="7268b-184">So, for every Azure location that has VMs toobe backed up, at least one Recovery Services vault must exist in that location.</span></span>
>
>

<span data-ttu-id="7268b-185">toocreate 復原服務保存庫：</span><span class="sxs-lookup"><span data-stu-id="7268b-185">toocreate a Recovery Services vault:</span></span>

1. <span data-ttu-id="7268b-186">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7268b-186">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="7268b-187">在 hello 中樞功能表中，按一下 **更多服務**在 hello 篩選對話方塊類型**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="7268b-187">On hello Hub menu, click **More services** and in hello Filter dialog type **Recovery Services**.</span></span> <span data-ttu-id="7268b-188">當您輸入時，篩選 hello 的資源清單。</span><span class="sxs-lookup"><span data-stu-id="7268b-188">As you type, hello list of resources filters.</span></span> <span data-ttu-id="7268b-189">當您看到 復原服務保存庫 hello 清單中的時，按一下它。</span><span class="sxs-lookup"><span data-stu-id="7268b-189">When you see Recovery Services vaults in hello list, click it.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7268b-191">如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-191">If there are Recovery Services vaults in hello subscription, hello vaults are listed.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. <span data-ttu-id="7268b-193">在 hello**復原服務保存庫**功能表上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="7268b-193">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="7268b-195">hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。</span><span class="sxs-lookup"><span data-stu-id="7268b-195">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="7268b-197">如**名稱**，輸入好記名稱 tooidentify hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-197">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="7268b-198">hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7268b-198">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="7268b-199">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="7268b-199">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="7268b-200">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="7268b-200">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="7268b-201">在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7268b-201">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="7268b-202">如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7268b-202">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="7268b-203">如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7268b-203">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="7268b-204">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="7268b-204">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="7268b-205">在 hello**資源群組**> 一節：</span><span class="sxs-lookup"><span data-stu-id="7268b-205">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="7268b-206">選取**建立新**如果您想 toocreate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="7268b-206">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="7268b-207">或</span><span class="sxs-lookup"><span data-stu-id="7268b-207">Or</span></span>
    * <span data-ttu-id="7268b-208">選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="7268b-208">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="7268b-209">完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7268b-209">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="7268b-210">按一下**位置**hello 保存庫的 tooselect hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="7268b-210">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="7268b-211">這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="7268b-211">This choice determines hello geographic region where your backup data is sent.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7268b-212">如果您不確定的 hello 您 VM 所在的位置，退出 hello 保存庫建立對話方塊，並移 hello 入口網站中的虛擬機器 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="7268b-212">If you are unsure of hello location in which your VM exists, close out of hello vault creation dialog, and go toohello list of Virtual Machines in hello portal.</span></span> <span data-ttu-id="7268b-213">如果您在多個區域中有虛擬機器，請在每個區域中建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-213">If you have virtual machines in multiple regions, create a Recovery Services vault in each region.</span></span> <span data-ttu-id="7268b-214">建立 hello 第一個位置中的 hello 保存庫，再繼續 toohello 下一個位置。</span><span class="sxs-lookup"><span data-stu-id="7268b-214">Create hello vault in hello first location before going toohello next location.</span></span> <span data-ttu-id="7268b-215">沒有任何需要 toospecify hello 使用儲存體帳戶 toostore hello 備份資料--hello 復原服務保存庫，而且 hello Azure 備份服務會自動處理 hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7268b-215">There is no need toospecify hello storage accounts used toostore hello backup data--hello Recovery Services vault and hello Azure Backup service automatically handle hello storage.</span></span>
  >

8. <span data-ttu-id="7268b-216">在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="7268b-216">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="7268b-217">可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="7268b-217">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="7268b-218">監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。</span><span class="sxs-lookup"><span data-stu-id="7268b-218">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="7268b-219">一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-219">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="7268b-220">在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="7268b-220">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="7268b-222">一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。</span><span class="sxs-lookup"><span data-stu-id="7268b-222">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

<span data-ttu-id="7268b-223">既然您已建立您的保存庫，了解如何 tooset hello 儲存體複寫。</span><span class="sxs-lookup"><span data-stu-id="7268b-223">Now that you've created your vault, learn how tooset hello storage replication.</span></span>

### <a name="set-storage-replication"></a><span data-ttu-id="7268b-224">設定儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="7268b-224">Set Storage Replication</span></span>
<span data-ttu-id="7268b-225">hello 儲存體複寫選項可讓您 toochoose 地理備援儲存體和本機備援儲存體之間。</span><span class="sxs-lookup"><span data-stu-id="7268b-225">hello storage replication option allows you toochoose between geo-redundant storage and locally redundant storage.</span></span> <span data-ttu-id="7268b-226">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7268b-226">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7268b-227">如果您主要的備份復原服務保存庫的 hello，保留 hello 儲存體複寫選項集 toogeo 備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7268b-227">If hello Recovery Services vault is your primary backup, leave hello storage replication option set toogeo-redundant storage.</span></span> <span data-ttu-id="7268b-228">如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7268b-228">Choose locally redundant storage if you want a cheaper option that isn't as durable.</span></span> <span data-ttu-id="7268b-229">深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本機備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存選項的 hello [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="7268b-229">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in hello [Azure Storage replication overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="7268b-230">tooedit hello 儲存體複寫設定：</span><span class="sxs-lookup"><span data-stu-id="7268b-230">tooedit hello storage replication setting:</span></span>

1. <span data-ttu-id="7268b-231">從 hello**復原服務保存庫**刀鋒視窗中，選取 hello 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-231">From hello **Recovery Services vaults** blade, select hello new vault.</span></span>

  ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  <span data-ttu-id="7268b-233">當您選取 hello 保存庫時，hello 設定 刀鋒視窗 (*hello 頂端具有 hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-233">When you select hello vault, hello Settings blade (*which has hello vault's name at hello top*) and hello vault details blade open.</span></span>

  ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="7268b-235">在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="7268b-235">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="7268b-236">hello 備份基礎結構刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-236">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="7268b-237">在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7268b-237">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="7268b-239">選擇您的保存庫的 hello 適當的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="7268b-239">Choose hello appropriate storage replication option for your vault.</span></span>

    ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="7268b-241">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7268b-241">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7268b-242">如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。</span><span class="sxs-lookup"><span data-stu-id="7268b-242">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="7268b-243">如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="7268b-243">If you don't use Azure as a primary backup storage endpoint, then choose **Locally redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="7268b-244">在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="7268b-244">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a><span data-ttu-id="7268b-245">選取備份目標、 設定原則，並定義項目 tooprotect</span><span class="sxs-lookup"><span data-stu-id="7268b-245">Select a backup goal, set policy and define items tooprotect</span></span>
<span data-ttu-id="7268b-246">向保存庫註冊的 VM，之前請先執行 hello 探索程序 tooensure toohello 訂用帳戶已加入任何新虛擬機器所識別。</span><span class="sxs-lookup"><span data-stu-id="7268b-246">Before registering a VM with a vault, run hello discovery process tooensure that any new virtual machines that have been added toohello subscription are identified.</span></span> <span data-ttu-id="7268b-247">hello 處理序會查詢 Azure hello hello 訂用帳戶，以及其他資訊中的虛擬機器清單，例如 hello 雲端服務名稱與 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="7268b-247">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span> <span data-ttu-id="7268b-248">在 hello Azure 入口網站，案例是指 toowhat 要 tooput 到 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-248">In hello Azure portal, scenario refers toowhat you are going tooput into hello recovery services vault.</span></span> <span data-ttu-id="7268b-249">原則是 hello 排程的頻率如何及何時建立復原點。</span><span class="sxs-lookup"><span data-stu-id="7268b-249">Policy is hello schedule for how often and when recovery points are taken.</span></span> <span data-ttu-id="7268b-250">原則也包括 hello hello 的復原點的保留範圍。</span><span class="sxs-lookup"><span data-stu-id="7268b-250">Policy also includes hello retention range for hello recovery points.</span></span>

1. <span data-ttu-id="7268b-251">如果您已經開啟保存庫復原服務，繼續 toostep 2。</span><span class="sxs-lookup"><span data-stu-id="7268b-251">If you already have a recovery services vault open, proceed toostep 2.</span></span> <span data-ttu-id="7268b-252">否則，請在 [hello 中樞功能表中，按一下**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="7268b-252">Otherwise, on hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7268b-254">復原服務保存庫 hello 清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7268b-254">hello list of recovery services vaults appears.</span></span>

    ![檢視的 hello 復原服務保存庫清單](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    <span data-ttu-id="7268b-256">從 hello 清單中的 復原服務保存庫，請選取保存庫 tooopen 其儀表板。</span><span class="sxs-lookup"><span data-stu-id="7268b-256">From hello list of recovery services vaults, select a vault tooopen its dashboard.</span></span>

     ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. <span data-ttu-id="7268b-258">Hello 保存庫儀表板功能表上，按一下**備份**tooopen hello 備份刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7268b-258">On hello vault dashboard menu, click **Backup** tooopen hello Backup blade.</span></span>

    ![開啟 [備份] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/backup-button.png)

    <span data-ttu-id="7268b-260">hello 備份及備份目標刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-260">hello Backup and Backup Goal blades open.</span></span>

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. <span data-ttu-id="7268b-262">在 hello 備份目標刀鋒視窗中，從 hello**您的工作負載執行**下拉式選單中，選擇 Azure。</span><span class="sxs-lookup"><span data-stu-id="7268b-262">On hello Backup Goal blade, from hello **Where is your workload running** drop-down menu, choose Azure.</span></span> <span data-ttu-id="7268b-263">從 hello**您該怎麼想 toobackup**下拉式清單，請選擇虛擬機器，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7268b-263">From hello **What do you want toobackup** drop-down, choose Virtual machine, then click **OK**.</span></span>

    <span data-ttu-id="7268b-264">這些動作 hello 保存庫中註冊 hello VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7268b-264">These actions register hello VM extension with hello vault.</span></span> <span data-ttu-id="7268b-265">hello 關閉刀鋒視窗中的備份目標和 hello**備份原則**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-265">hello Backup Goal blade closes and hello **Backup policy** blade opens.</span></span>

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. <span data-ttu-id="7268b-267">在 hello 備份原則 刀鋒視窗，選取您想 tooapply toohello 保存庫的 hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="7268b-267">On hello Backup policy blade, select hello backup policy you want tooapply toohello vault.</span></span>

    ![選取備份原則](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    <span data-ttu-id="7268b-269">hello 的 hello 預設原則的詳細資料列在 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="7268b-269">hello details of hello default policy are listed under hello drop-down menu.</span></span> <span data-ttu-id="7268b-270">如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="7268b-270">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="7268b-271">如需定義備份原則的指示，請參閱 [定義備份原則](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="7268b-271">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span>
    <span data-ttu-id="7268b-272">按一下**確定**tooassociate hello 備份原則與 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-272">Click **OK** tooassociate hello backup policy with hello vault.</span></span>

    <span data-ttu-id="7268b-273">備份原則 刀鋒視窗關閉和 hello hello**選取虛擬機器**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-273">hello Backup policy blade closes and hello **Select virtual machines** blade opens.</span></span>
5. <span data-ttu-id="7268b-274">在 hello**選取虛擬機器**刀鋒視窗中，選擇將虛擬機器 tooassociate hello 以 hello 指定原則，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7268b-274">In hello **Select virtual machines** blade, choose hello virtual machines tooassociate with hello specified policy and click **OK**.</span></span>

    ![選取工作負載](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    <span data-ttu-id="7268b-276">hello 選取虛擬機器會進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7268b-276">hello selected virtual machine is validated.</span></span> <span data-ttu-id="7268b-277">如果您沒有看到 hello 虛擬機器的預期 toosee，存在於的核取 hello 相同的 Azure 位置，如 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7268b-277">If you do not see hello virtual machines that you expected toosee, check that they exist in hello same Azure location as hello Recovery Services vault.</span></span> <span data-ttu-id="7268b-278">hello 保存庫儀表板上顯示的 復原服務保存庫的 hello 的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="7268b-278">hello location of hello Recovery Services vault is shown on hello vault dashboard.</span></span>

6. <span data-ttu-id="7268b-279">既然您已經定義 hello 保存庫的所有設定在 hello 備份刀鋒視窗中，按一下**啟用備份**toodeploy hello 原則 toohello 保存庫和 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="7268b-279">Now that you have defined all settings for hello vault, in hello Backup blade, click **Enable Backup** toodeploy hello policy toohello vault and hello VMs.</span></span> <span data-ttu-id="7268b-280">部署的 hello 備份原則不會建立 hello hello 虛擬機器的初始的復原點。</span><span class="sxs-lookup"><span data-stu-id="7268b-280">Deploying hello backup policy does not create hello initial recovery point for hello virtual machine.</span></span>

    ![啟用備份](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

<span data-ttu-id="7268b-282">已成功啟用 hello 備份之後，您的備份原則也會執行排程。</span><span class="sxs-lookup"><span data-stu-id="7268b-282">After successfully enabling hello backup, your backup policy will execute on schedule.</span></span> <span data-ttu-id="7268b-283">不過，繼續 tooinitiate hello 的第一個備份工作。</span><span class="sxs-lookup"><span data-stu-id="7268b-283">However, proceed tooinitiate hello first backup job.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="7268b-284">初始備份</span><span class="sxs-lookup"><span data-stu-id="7268b-284">Initial backup</span></span>
<span data-ttu-id="7268b-285">一旦備份原則已部署在 hello 虛擬機器，並不表示 hello 已備份的資料。</span><span class="sxs-lookup"><span data-stu-id="7268b-285">Once a backup policy has been deployed on hello virtual machine, that does not mean hello data has been backed up.</span></span> <span data-ttu-id="7268b-286">根據預設，hello 第一個排定的備份 （如 hello 備份原則中所定義） 是 hello 初始備份。</span><span class="sxs-lookup"><span data-stu-id="7268b-286">By default, hello first scheduled backup (as defined in hello backup policy) is hello initial backup.</span></span> <span data-ttu-id="7268b-287">Hello 初始備份，就會發生，直到 hello 上次備份的狀態上 hello**備份工作**刀鋒視窗中顯示為**警告 （已暫止的初始備份）**。</span><span class="sxs-lookup"><span data-stu-id="7268b-287">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![待備份](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="7268b-289">除非您初始的備份是到期 toobegin 過期，建議您執行**立即備份**。</span><span class="sxs-lookup"><span data-stu-id="7268b-289">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span>

<span data-ttu-id="7268b-290">toorun hello 初始備份作業：</span><span class="sxs-lookup"><span data-stu-id="7268b-290">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="7268b-291">Hello 保存庫儀表板上按一下下的 hello 號碼**備份項目**，或按一下 hello**備份項目**磚。</span><span class="sxs-lookup"><span data-stu-id="7268b-291">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="7268b-292">
  ![設定圖示](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="7268b-292">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="7268b-293">hello**備份項目**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-293">hello **Backup Items** blade opens.</span></span>

  ![備份項目](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="7268b-295">在 hello**備份項目**刀鋒視窗中，選取 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="7268b-295">On hello **Backup Items** blade, select hello item.</span></span>

  ![設定圖示](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="7268b-297">hello**備份項目**清單隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-297">hello **Backup Items** list opens.</span></span> <br/>

  ![備份作業已觸發](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="7268b-299">在 hello**備份項目**清單中，按一下 hello 省略符號**...** tooopen hello 操作功能表。</span><span class="sxs-lookup"><span data-stu-id="7268b-299">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="7268b-301">hello 操作功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7268b-301">hello Context menu appears.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="7268b-303">Hello 操作功能表上，按一下 **備份現在**。</span><span class="sxs-lookup"><span data-stu-id="7268b-303">On hello Context menu, click **Backup now**.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="7268b-305">hello 立即備份 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-305">hello Backup Now blade opens.</span></span>

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="7268b-307">Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="7268b-307">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="7268b-309">部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。</span><span class="sxs-lookup"><span data-stu-id="7268b-309">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="7268b-310">根據您的 VM hello 大小，建立 hello 初始備份可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="7268b-310">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="7268b-311">hello 初始備份，hello 保存庫儀表板上，在 hello tooview 或追蹤 hello 狀態**備份工作**磚按一下**正在**。</span><span class="sxs-lookup"><span data-stu-id="7268b-311">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="7268b-313">hello 備份作業 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="7268b-313">hello Backup Jobs blade opens.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="7268b-315">在 hello**備份作業**刀鋒視窗中，您可以查看所有工作的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="7268b-315">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="7268b-316">請檢查 VM 的 hello 備份工作是否仍在進行中，或若它已完成。</span><span class="sxs-lookup"><span data-stu-id="7268b-316">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="7268b-317">Hello 狀態的備份工作完成時，是*已完成*。</span><span class="sxs-lookup"><span data-stu-id="7268b-317">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7268b-318">Hello 備份作業的一部分 hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個 VM tooflush 所有寫入，並採取一致的快照集。</span><span class="sxs-lookup"><span data-stu-id="7268b-318">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="7268b-319">Hello 虛擬機器上安裝 VM 代理程式 hello</span><span class="sxs-lookup"><span data-stu-id="7268b-319">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="7268b-320">如果需要便會提供此資訊。</span><span class="sxs-lookup"><span data-stu-id="7268b-320">This information is provided in case it is needed.</span></span> <span data-ttu-id="7268b-321">hello Azure VM 代理程式必須安裝在 Azure 虛擬機器以 hello 備份副檔名 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="7268b-321">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="7268b-322">不過，如果您的 VM 建立從 hello Azure 組件庫，然後 hello VM 代理程式已經存在於 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7268b-322">However, if your VM was created from hello Azure gallery, then hello VM Agent is already present on hello virtual machine.</span></span> <span data-ttu-id="7268b-323">從移轉內部部署資料中心會沒有 hello VM 代理程式安裝的 Vm。</span><span class="sxs-lookup"><span data-stu-id="7268b-323">VMs that are migrated from on-premises datacenters would not have hello VM Agent installed.</span></span> <span data-ttu-id="7268b-324">在這種情況下，hello VM 代理程式需要安裝 toobe。</span><span class="sxs-lookup"><span data-stu-id="7268b-324">In such a case, hello VM Agent needs toobe installed.</span></span> <span data-ttu-id="7268b-325">如果您有備份 hello Azure VM 的問題，確認 hello Azure VM 代理程式已正確安裝 hello 虛擬機器上 （請參閱下表中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="7268b-325">If you have problems backing up hello Azure VM, check that hello Azure VM Agent is correctly installed on hello virtual machine (see hello following table).</span></span> <span data-ttu-id="7268b-326">如果您建立自訂的 VM，[確保 hello**安裝 hello VM 代理程式**核取方塊已選取](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)hello 虛擬機器已佈建之前。</span><span class="sxs-lookup"><span data-stu-id="7268b-326">If you create a custom VM, [ensure hello **Install hello VM Agent** check box is selected](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) before hello virtual machine is provisioned.</span></span>

<span data-ttu-id="7268b-327">深入了解 hello [VM 代理程式](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409)和[如何 tooinstall 它](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7268b-327">Learn about hello [VM Agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how tooinstall it](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="7268b-328">下表中的 hello 提供 hello VM 代理程式用於 Windows 及 Linux Vm 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="7268b-328">hello following table provides additional information about hello VM Agent for Windows and Linux VMs.</span></span>

| <span data-ttu-id="7268b-329">**作業**</span><span class="sxs-lookup"><span data-stu-id="7268b-329">**Operation**</span></span> | <span data-ttu-id="7268b-330">**Windows**</span><span class="sxs-lookup"><span data-stu-id="7268b-330">**Windows**</span></span> | <span data-ttu-id="7268b-331">**Linux**</span><span class="sxs-lookup"><span data-stu-id="7268b-331">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7268b-332">安裝 VM 代理程式 hello</span><span class="sxs-lookup"><span data-stu-id="7268b-332">Installing hello VM Agent</span></span> |<li><span data-ttu-id="7268b-333">下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="7268b-333">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="7268b-334">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="7268b-334">You need Administrator privileges toocomplete hello installation.</span></span> <li><span data-ttu-id="7268b-335">[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="7268b-335">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |<li> <span data-ttu-id="7268b-336">安裝最新的 hello [Linux 代理程式](https://github.com/Azure/WALinuxAgent)從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="7268b-336">Install hello latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="7268b-337">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="7268b-337">You need Administrator privileges toocomplete hello installation.</span></span> <li> <span data-ttu-id="7268b-338">[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="7268b-338">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |
| <span data-ttu-id="7268b-339">更新 hello VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="7268b-339">Updating hello VM Agent</span></span> |<span data-ttu-id="7268b-340">更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="7268b-340">Updating hello VM Agent is as simple as reinstalling hello [VM Agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><span data-ttu-id="7268b-341">請確認在 hello VM 代理程式在更新時，執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="7268b-341">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |<span data-ttu-id="7268b-342">依 hello 指示[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7268b-342">Follow hello instructions on [updating hello Linux VM Agent](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><span data-ttu-id="7268b-343">確定沒有備份作業正在執行時 hello VM 代理程式正在更新。</span><span class="sxs-lookup"><span data-stu-id="7268b-343">Ensure that no backup operation is running while hello VM Agent is being updated.</span></span> |
| <span data-ttu-id="7268b-344">正在驗證 hello VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="7268b-344">Validating hello VM Agent installation</span></span> |<li><span data-ttu-id="7268b-345">瀏覽 toohello *C:\WindowsAzure\Packages* hello Azure VM 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7268b-345">Navigate toohello *C:\WindowsAzure\Packages* folder in hello Azure VM.</span></span> <li><span data-ttu-id="7268b-346">您應該尋找 hello WaAppAgent.exe 檔案存在。</span><span class="sxs-lookup"><span data-stu-id="7268b-346">You should find hello WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="7268b-347">以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="7268b-347">Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="7268b-348">N/A</span><span class="sxs-lookup"><span data-stu-id="7268b-348">N/A</span></span> |

### <a name="backup-extension"></a><span data-ttu-id="7268b-349">備份擴充功能</span><span class="sxs-lookup"><span data-stu-id="7268b-349">Backup extension</span></span>
<span data-ttu-id="7268b-350">一次 hello hello Azure 備份服務 hello 虛擬機器安裝 VM 代理程式會安裝 hello 備用分機號碼 toohello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="7268b-350">Once hello VM Agent is installed on hello virtual machine, hello Azure Backup service installs hello backup extension toohello VM Agent.</span></span> <span data-ttu-id="7268b-351">hello Azure 備份服務順暢地升級和修補程式不需要額外的使用者介入的 hello 備用分機號碼。</span><span class="sxs-lookup"><span data-stu-id="7268b-351">hello Azure Backup service seamlessly upgrades and patches hello backup extension without additional user intervention.</span></span>

<span data-ttu-id="7268b-352">hello 備份服務會安裝 hello 備用分機號碼，即使 hello VM 未執行。</span><span class="sxs-lookup"><span data-stu-id="7268b-352">hello Backup service installs hello backup extension, even if hello VM is not running.</span></span> <span data-ttu-id="7268b-353">執行中的 VM 提供 hello 取得應用程式一致復原點的最大的機會。</span><span class="sxs-lookup"><span data-stu-id="7268b-353">A running VM provides hello greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="7268b-354">不過，hello Azure 備份服務會繼續向上 hello VM tooback 即使它已關閉，而且 hello 擴充功能無法安裝。</span><span class="sxs-lookup"><span data-stu-id="7268b-354">However, hello Azure Backup service continues tooback up hello VM even if it is turned off, and hello extension could not be installed.</span></span> <span data-ttu-id="7268b-355">這種類型的備份也就是離線的 VM，並且 hello 的復原點*絕對一致*。</span><span class="sxs-lookup"><span data-stu-id="7268b-355">This type of backup is known as Offline VM, and hello recovery point is *crash consistent*.</span></span>

## <a name="troubleshooting-information"></a><span data-ttu-id="7268b-356">疑難排解資訊</span><span class="sxs-lookup"><span data-stu-id="7268b-356">Troubleshooting information</span></span>
<span data-ttu-id="7268b-357">如果您有一些在這篇文章中的 hello 工作完成的問題，請參閱[疑難排解指引](backup-azure-vms-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="7268b-357">If you have issues accomplishing some of hello tasks in this article, consult the [Troubleshooting guidance](backup-azure-vms-troubleshoot.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="7268b-358">價格</span><span class="sxs-lookup"><span data-stu-id="7268b-358">Pricing</span></span>
<span data-ttu-id="7268b-359">備份 Azure Vm 的 hello 成本根據 hello 受保護的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="7268b-359">hello cost of backing up Azure VMs is based on hello number of protected instances.</span></span> <span data-ttu-id="7268b-360">如需受保護執行個體的定義，請參閱[什麼是受保護執行個體](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)。</span><span class="sxs-lookup"><span data-stu-id="7268b-360">For a definition of a protected instance, see [What is a protected instance](backup-introduction-to-azure-backup.md#what-is-a-protected-instance).</span></span> <span data-ttu-id="7268b-361">如需計算備份虛擬機器的 hello 成本的範例，請參閱[如何計算受保護的執行個體](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances)。</span><span class="sxs-lookup"><span data-stu-id="7268b-361">For an example of calculating hello cost of backing up a virtual machine, see [How are protected instances calculated](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances).</span></span> <span data-ttu-id="7268b-362">請參閱 hello Azure 備份定價頁面的相關資訊[備份定價](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="7268b-362">See hello Azure Backup Pricing page for information about [Backup Pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>

## <a name="questions"></a><span data-ttu-id="7268b-363">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="7268b-363">Questions?</span></span>
<span data-ttu-id="7268b-364">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="7268b-364">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
