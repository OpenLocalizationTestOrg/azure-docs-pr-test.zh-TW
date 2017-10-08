---
title: "aaaBackup] 和 [還原加密使用 Azure Backup 的 Vm"
description: "這篇文章討論關於 hello 備份和還原 Vm 經驗加密使用 Azure 磁碟加密。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a><span data-ttu-id="d0f0a-103">向上 tooback 與還原加密使用 Azure 備份的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d0f0a-103">How tooback up and restore encrypted virtual machines with Azure Backup</span></span>
<span data-ttu-id="d0f0a-104">這篇文章討論有關步驟 toobackup 和還原虛擬機器使用 Azure Backup。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-104">This article talks about steps toobackup and restore virtual machines using Azure Backup.</span></span> <span data-ttu-id="d0f0a-105">它也提供有關支援的案例、必要條件的詳細資料，以及的錯誤案例的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-105">It also provides details about supported scenarios, pre-requisites, and troubleshooting steps for error cases.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d0f0a-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="d0f0a-106">Supported scenarios</span></span>
> [!NOTE]
> * <span data-ttu-id="d0f0a-107">只有 Resource Manager 部署的虛擬機器支援備份及還原加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-107">Backup and restore of encrypted VMs is supported only for Resource Manager deployed virtual machines.</span></span> <span data-ttu-id="d0f0a-108">傳統虛擬機器不提供支援。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-108">It is not supported for Classic virtual machines.</span></span> <br>
> * <span data-ttu-id="d0f0a-109">它支援使用 Azure 磁碟加密，此方法運用 hello 業界標準 BitLocker 功能的 Windows 和 Linux tooprovide 加密的磁碟的 DM Crypt 功能的 Windows 和 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-109">It is supported for both Windows and Linux virtual machines using Azure Disk Encryption, which leverages hello industry standard BitLocker feature of Windows and DM-Crypt feature of Linux tooprovide encryption of disks.</span></span> <br>
> * <span data-ttu-id="d0f0a-110">只有使用「BitLocker 加密金鑰」和「金鑰加密金鑰」加密的虛擬機器才提供支援。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-110">It is supported only for virtual machines encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span> <span data-ttu-id="d0f0a-111">只使用「BitLocker 加密金鑰」加密的虛擬機器不提供支援。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-111">It is not supported for virtual machines encrypted using BitLocker Encryption Key only.</span></span> <br>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d0f0a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="d0f0a-112">Prerequisites</span></span>
1. <span data-ttu-id="d0f0a-113">虛擬機器已使用 [Azure 磁碟加密](../security/azure-security-disk-encryption.md)進行加密。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-113">Virtual machine has been encrypted using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span></span> <span data-ttu-id="d0f0a-114">應使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-114">It should be encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span>
2. <span data-ttu-id="d0f0a-115">復原服務保存庫已建立及使用設定的儲存體複寫的步驟 hello 文章中提及[準備環境以使用備份](backup-azure-arm-vms-prepare.md)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-115">Recovery services vault has been created and storage replication set using steps mentioned in hello article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>
3. <span data-ttu-id="d0f0a-116">Azure 備份具有[權限 tooaccess 金鑰保存庫](#provide-permissions-to-azure-backup)包含索引鍵，為機密資料加密的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-116">Azure Backup has been given [permissions tooaccess key vault](#provide-permissions-to-azure-backup) containing keys, secrets for encrypted VMs.</span></span>

## <a name="backup-encrypted-vm"></a><span data-ttu-id="d0f0a-117">備份加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d0f0a-117">Backup encrypted VM</span></span>
<span data-ttu-id="d0f0a-118">使用下列步驟 tooset 備份目標的 hello、 定義原則、 設定項目和觸發程序備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-118">Use hello following steps tooset backup goal, define policy, configure items and trigger backup.</span></span>

### <a name="configure-backup"></a><span data-ttu-id="d0f0a-119">設定備份</span><span class="sxs-lookup"><span data-stu-id="d0f0a-119">Configure backup</span></span>
1. <span data-ttu-id="d0f0a-120">如果您已經開啟的復原服務保存庫，請繼續執行 toonext 步驟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-120">If you already have a Recovery Services vault open, proceed toonext step.</span></span> <span data-ttu-id="d0f0a-121">如果您不需要復原服務保存庫開啟之後，但在 hello hello 中樞功能表中，在 Azure 入口網站中按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-121">If you do not have a Recovery Services vault open, but are in hello Azure portal, on hello Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="d0f0a-122">在 [hello] 清單中的資源，輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-122">In hello list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="d0f0a-123">當您開始輸入 hello 清單會篩選根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-123">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="d0f0a-124">當您看到 [復原服務保存庫] 時，請按一下它。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-124">When you see **Recovery Services vaults**, click it.</span></span>

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="d0f0a-126">復原服務保存庫 hello 清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-126">hello list of Recovery Services vaults appears.</span></span> <span data-ttu-id="d0f0a-127">從 hello 清單的 復原服務保存庫中，選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-127">From hello list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="d0f0a-128">hello 選取保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-128">hello selected vault dashboard opens.</span></span>
2. <span data-ttu-id="d0f0a-129">從 hello 的項目清單會出現在保存庫下，按一下 **備份**tooopen hello 備份刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-129">From hello list of items that appears under vault, click **Backup** tooopen hello Backup blade.</span></span>

      ![開啟 [備份] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup.png)
3. <span data-ttu-id="d0f0a-131">在 hello 備份刀鋒視窗中，按一下 **備份目標**tooopen hello 備份目標刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-131">On hello Backup blade, click **Backup goal** tooopen hello Backup Goal blade.</span></span>

      ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. <span data-ttu-id="d0f0a-133">在 hello 備份目標刀鋒視窗中，設定**您的工作負載執行**tooAzure 和**怎麼辦想 toobackup** tooVirtual 機器，然後按一下  **確定**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-133">On hello Backup Goal blade, set **Where is your workload running** tooAzure and **What do you want toobackup** tooVirtual machine, then click **OK**.</span></span>

   <span data-ttu-id="d0f0a-134">hello 備份目標刀鋒視窗關閉，並 hello 備份原則 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-134">hello Backup Goal blade closes and hello Backup policy blade opens.</span></span>

   ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. <span data-ttu-id="d0f0a-136">Hello 備份原則 刀鋒視窗，選取您想 tooapply toohello 保存庫，然後按一下 hello 備份原則**確定**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-136">On hello Backup policy blade, select hello backup policy you want tooapply toohello vault and click **OK**.</span></span>

      ![選取備份原則](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    <span data-ttu-id="d0f0a-138">hello 的 hello 預設原則的詳細資料會列在 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-138">hello details of hello default policy are listed in hello details.</span></span> <span data-ttu-id="d0f0a-139">如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-139">If you want toocreate a policy, select **Create New** from hello drop-down menu.</span></span> <span data-ttu-id="d0f0a-140">一旦您按一下**確定**，hello 備份原則是 hello 保存庫相關聯。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-140">Once you click **OK**, hello backup policy is associated with hello vault.</span></span>

    <span data-ttu-id="d0f0a-141">接下來選擇 hello Vm tooassociate hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-141">Next choose hello VMs tooassociate with hello vault.</span></span>
6. <span data-ttu-id="d0f0a-142">選擇 hello 加密以 hello tooassociate 指定原則，按一下 虛擬機器**確定**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-142">Choose hello encrypted virtual machines tooassociate with hello specified policy and click **OK**.</span></span>

      ![選取加密的 VM](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. <span data-ttu-id="d0f0a-144">此頁面會顯示有關加密的相關聯的 toohello Vm 選取金鑰保存庫的訊息。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-144">This page shows a message about key vault associated toohello encrypted VMs selected.</span></span> <span data-ttu-id="d0f0a-145">備份服務需要唯讀存取 toohello 金鑰和 hello 金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-145">Backup service requires read-only access toohello keys and secrets in hello key vault.</span></span> <span data-ttu-id="d0f0a-146">它會使用這些權限 toobackup 金鑰和密碼，以及 hello 相關聯的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-146">It uses these permissions toobackup key and secret, along with hello associated VMs.</span></span> <span data-ttu-id="d0f0a-147">**您必須提供權限 toobackup 服務 tooaccess 金鑰保存庫的備份 toowork**。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-147">**You must give permissions toobackup service tooaccess key vault for backups toowork**.</span></span> <span data-ttu-id="d0f0a-148">您可以提供使用這些權限[hello 一節所述步驟](#provide-permissions-to-azure-backup)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-148">You can provide these permissions using [steps mentioned in hello section below](#provide-permissions-to-azure-backup).</span></span>

      ![加密的 VM 訊息](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      <span data-ttu-id="d0f0a-150">既然您已定義 hello 保存庫，在 hello 備份刀鋒視窗中的所有設定都按一下 啟用在 hello hello 頁面底部的備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-150">Now that you have defined all settings for hello vault, in hello Backup blade click Enable Backup at hello bottom of hello page.</span></span> <span data-ttu-id="d0f0a-151">啟用備份部署 hello 原則 toohello 保存庫和 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-151">Enable  Backup deploys hello policy toohello vault and hello VMs.</span></span>
8. <span data-ttu-id="d0f0a-152">hello 準備中的下一個階段安裝 hello VM 代理程式或進行確定 hello VM 代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-152">hello next phase in preparation is installing hello VM Agent or making sure hello VM Agent is installed.</span></span> <span data-ttu-id="d0f0a-153">toodo hello 相同，請使用 hello 文章中提及的 hello 步驟[準備環境以使用備份](backup-azure-arm-vms-prepare.md)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-153">toodo hello same, use hello steps mentioned in hello article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

### <a name="triggering-backup-job"></a><span data-ttu-id="d0f0a-154">觸發備份作業</span><span class="sxs-lookup"><span data-stu-id="d0f0a-154">Triggering backup job</span></span>
<span data-ttu-id="d0f0a-155">使用 hello 文章中提及的 hello 步驟[備份的 Azure Vm toorecovery 服務保存庫](backup-azure-arm-vms.md)tootrigger 備份工作。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-155">Use hello steps mentioned in hello article [Backup Azure VMs toorecovery services vault](backup-azure-arm-vms.md) tootrigger backup job.</span></span>

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a><span data-ttu-id="d0f0a-156">將啟用加密之已備份 VM 繼續備份</span><span class="sxs-lookup"><span data-stu-id="d0f0a-156">Continue backups of already backed up VMs with encryption enabled</span></span>  
<span data-ttu-id="d0f0a-157">如果您有已正在備份復原服務保存庫中的 Vm，並在稍後的加密已啟用，您必須針對備份 toocontinue 給予權限 toobackup 服務 tooaccess 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-157">If you have VMs already being backup up in recovery services vault and have been enabled for encryption at a later point, you must give permissions toobackup service tooaccess key vault for backups toocontinue.</span></span> <span data-ttu-id="d0f0a-158">您可以提供使用這些權限[hello 一節中的步驟](#provide-permissions-to-azure-backup)或使用 PowerShell 步驟中所述**啟用備份**區段[PowerShell 文件](backup-azure-vms-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-158">You can provide these permissions using [steps in hello section below](#provide-permissions-to-azure-backup) or using PowerShell steps mentioned in **Enable Backup** section of [PowerShell documentation](backup-azure-vms-automation.md).</span></span> 

## <a name="provide-permissions-tooazure-backup"></a><span data-ttu-id="d0f0a-159">提供的權限 tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="d0f0a-159">Provide permissions tooAzure Backup</span></span>
<span data-ttu-id="d0f0a-160">使用下列步驟 tooprovide 相關的權限 tooAzure 備份 tooaccess 金鑰保存庫的 hello 和執行備份的加密 Vm:</span><span class="sxs-lookup"><span data-stu-id="d0f0a-160">Use hello following steps tooprovide relevant permissions tooAzure Backup tooaccess key vault and perform backup of encrypted VMs:</span></span>
1. <span data-ttu-id="d0f0a-161">選取 [更多服務]，然後搜尋 [金鑰保存庫]。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-161">Select **More Services** and search for **Key vaults**.</span></span>

    ![搜尋金鑰保存庫](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. <span data-ttu-id="d0f0a-163">從金鑰保存庫的 hello 清單中選取 hello 與加密的 VM，必須備份 toobe 相關聯的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-163">From hello list of key vaults, select hello key vault associated with encrypted VM, which needs toobe backed up.</span></span>

     ![選取金鑰保存庫](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. <span data-ttu-id="d0f0a-165">按一下 [存取原則] 然後 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-165">Click **Access policies** and then **Add new**.</span></span>

    ![新增存取原則](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. <span data-ttu-id="d0f0a-167">按一下**選取主體**和型別**備份管理服務**hello 搜尋列中。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-167">Click **Select principal** and type **Backup Management Service** in hello search bar.</span></span> 

    ![搜尋備份服務](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. <span data-ttu-id="d0f0a-169">選取 [備份管理服務]，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-169">Select **Backup Management Service** and click Select button.</span></span>

    ![選取備份服務](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. <span data-ttu-id="d0f0a-171">在 [從範本設定] 下拉式功能表中選取 [Azure 備份]。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-171">Select **Azure Backup** in Configure from template drop down.</span></span> <span data-ttu-id="d0f0a-172">預先填入機碼權限中的 hello 所需權限和密碼的權限下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-172">It pre-fills hello required permissions in Key permissions and Secret permissions drop down.</span></span> 

    ![選取 Azure 備份](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. <span data-ttu-id="d0f0a-174">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-174">Click **OK**.</span></span> <span data-ttu-id="d0f0a-175">請注意「備份管理服務」會新增到 [存取原則] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-175">Notice that Backup Management Service gets added in Access Policies blade.</span></span> 

    ![備份服務存取原則](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. <span data-ttu-id="d0f0a-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-177">Click **Save**.</span></span> <span data-ttu-id="d0f0a-178">這可讓 hello 所需的權限 tooAzure 備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-178">This will give hello required permissions tooAzure Backup.</span></span>

    ![備份服務存取原則](./media/backup-azure-vms-encryption/save-access-policy.png)

<span data-ttu-id="d0f0a-180">順利提供權限後，您可以繼續為已加密的 VM 啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-180">Once permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span></span>

## <a name="restore-encrypted-vm"></a><span data-ttu-id="d0f0a-181">還原已加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d0f0a-181">Restore encrypted VM</span></span>
<span data-ttu-id="d0f0a-182">toorestore 加密 VM，第一個還原的磁碟使用一個步驟中所述的章節**磁碟備份還原**中[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-182">toorestore encrypted VM, first Restore Disks using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="d0f0a-183">之後，您可以使用其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="d0f0a-183">After that, you can use one of hello following options:</span></span>
* <span data-ttu-id="d0f0a-184">使用所述的 hello PowerShell 步驟[從還原的硬碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 完整 VM 從還原的磁碟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-184">Use hello PowerShell steps mentioned in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate full VM from restored disks.</span></span>
* <span data-ttu-id="d0f0a-185">OR[產生做為還原的磁碟的一部分使用範本](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm)toocreate Vm 從還原的磁碟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-185">OR, [Use template generated as part of Restore Disks](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate VMs from restored disks.</span></span> <span data-ttu-id="d0f0a-186">只可將範本用於 2017 年 4 月 26 日之後建立的復原點。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-186">Templates can be used only for recovery points created after 26 April 2017.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="d0f0a-187">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="d0f0a-187">Troubleshooting errors</span></span>
| <span data-ttu-id="d0f0a-188">作業</span><span class="sxs-lookup"><span data-stu-id="d0f0a-188">Operation</span></span> | <span data-ttu-id="d0f0a-189">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="d0f0a-189">Error details</span></span> | <span data-ttu-id="d0f0a-190">解決方案</span><span class="sxs-lookup"><span data-stu-id="d0f0a-190">Resolution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d0f0a-191">備份</span><span class="sxs-lookup"><span data-stu-id="d0f0a-191">Backup</span></span> |<span data-ttu-id="d0f0a-192">驗證失敗，因為虛擬機器單獨以 BEK 進行加密。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-192">Validation failed as virtual machine is encrypted with BEK alone.</span></span> <span data-ttu-id="d0f0a-193">只會對同時使用 BEK 和 KEK 加密的虛擬機器啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-193">Backups can be enabled only for virtual machines encrypted with both BEK and KEK.</span></span> |<span data-ttu-id="d0f0a-194">應該使用 BEK 和 KEK 來加密虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-194">Virtual machine should be encrypted using BEK and KEK.</span></span> <span data-ttu-id="d0f0a-195">第一次解密 hello VM，並使用 BEK 和 KEK 將其加密。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-195">First decrypt hello VM and encrypt it using both BEK and KEK.</span></span> <span data-ttu-id="d0f0a-196">使用 BEK 和 KEK 加密 VM 之後，啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-196">Enable backup once VM is encrypted using both BEK and KEK.</span></span> <span data-ttu-id="d0f0a-197">進一步了解如何在[解密和加密 hello VM](../security/azure-security-disk-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="d0f0a-197">Learn more on how you can [decrypt and encrypt hello VM](../security/azure-security-disk-encryption.md)</span></span>  |
| <span data-ttu-id="d0f0a-198">還原</span><span class="sxs-lookup"><span data-stu-id="d0f0a-198">Restore</span></span> |<span data-ttu-id="d0f0a-199">您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰保存庫不存在。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-199">You cannot restore this encrypted VM since key vault associated with this VM does not exist.</span></span> |<span data-ttu-id="d0f0a-200">利用[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)，建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-200">Create key vault using [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span> <span data-ttu-id="d0f0a-201">Hello 發行項，請參閱[還原金鑰保存庫金鑰和密碼使用 Azure Backup](backup-azure-restore-key-secret.md) toorestore 金鑰和密碼是否不存在。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-201">Refer hello article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) toorestore key and secret if they are not present.</span></span> |
| <span data-ttu-id="d0f0a-202">還原</span><span class="sxs-lookup"><span data-stu-id="d0f0a-202">Restore</span></span> |<span data-ttu-id="d0f0a-203">您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰和密碼不存在。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-203">You cannot restore this encrypted VM since key and secret associated with this VM do not exist.</span></span> |<span data-ttu-id="d0f0a-204">Hello 發行項，請參閱[還原金鑰保存庫金鑰和密碼使用 Azure Backup](backup-azure-restore-key-secret.md) toorestore 金鑰和密碼是否不存在。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-204">Refer hello article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) toorestore key and secret if they are not present.</span></span> |
| <span data-ttu-id="d0f0a-205">還原</span><span class="sxs-lookup"><span data-stu-id="d0f0a-205">Restore</span></span> |<span data-ttu-id="d0f0a-206">備份服務您的訂用帳戶中沒有授權 tooaccess 資源。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-206">Backup Service does not have authorization tooaccess resources in your subscription.</span></span> |<span data-ttu-id="d0f0a-207">如前所述，請先使用[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)的＜還原備份的磁碟＞一節中所述的步驟來還原磁碟。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-207">As mentioned above, Restore Disks first, using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="d0f0a-208">之後，使用者 PowerShell 太[從還原的硬碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-208">After that, user PowerShell too[Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span></span> |
|<span data-ttu-id="d0f0a-209">備份</span><span class="sxs-lookup"><span data-stu-id="d0f0a-209">Backup</span></span> | <span data-ttu-id="d0f0a-210">Azure 備份服務沒有足夠的權限 tooKey 保存庫適用於備份的加密虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d0f0a-210">Azure Backup Service does not have sufficient permissions tooKey Vault for Backup of Encrypted Virtual Machines</span></span> | <span data-ttu-id="d0f0a-211">虛擬機器應該使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-211">Virtual machine should be encrypted using both BitLocker Encryption Key and Key Encryption Key.</span></span> <span data-ttu-id="d0f0a-212">之後，應該啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-212">After that, backup should be enabled.</span></span>  <span data-ttu-id="d0f0a-213">備份服務應提供使用這些權限[hello 的上一節所述步驟](#provide-permissions-to-azure-backup)或使用 PowerShell 步驟所述 hello**啟用保護**hello PowerShell 區段文件，網址[虛擬機器使用 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md#back-up-azure-vms)。</span><span class="sxs-lookup"><span data-stu-id="d0f0a-213">Backup service should be provided these permissions using [steps mentioned in hello section above](#provide-permissions-to-azure-backup) or by using PowerShell steps mentioned in hello **Enable protection** section of hello PowerShell documentation at [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md#back-up-azure-vms).</span></span> |  
