---
title: "使用 Azure 備份來備份和還原已加密的 VM"
description: "本文討論使用「Azure 磁碟加密」加密之 VM 的備份與還原經驗。"
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
ms.openlocfilehash: 89492cda8eff23509bee7693bb5f7e6ab5eb10d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a><span data-ttu-id="d5c32-103">如何使用 Azure 備份來備份及還原加密的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d5c32-103">How to back up and restore encrypted virtual machines with Azure Backup</span></span>
<span data-ttu-id="d5c32-104">本文討論使用 Azure 備份來備份和還原虛擬機器的步驟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-104">This article talks about steps to backup and restore virtual machines using Azure Backup.</span></span> <span data-ttu-id="d5c32-105">它也提供有關支援的案例、必要條件的詳細資料，以及的錯誤案例的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-105">It also provides details about supported scenarios, pre-requisites, and troubleshooting steps for error cases.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d5c32-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="d5c32-106">Supported scenarios</span></span>
> [!NOTE]
> * <span data-ttu-id="d5c32-107">只有 Resource Manager 部署的虛擬機器支援備份及還原加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-107">Backup and restore of encrypted VMs is supported only for Resource Manager deployed virtual machines.</span></span> <span data-ttu-id="d5c32-108">傳統虛擬機器不提供支援。</span><span class="sxs-lookup"><span data-stu-id="d5c32-108">It is not supported for Classic virtual machines.</span></span> <br>
> * <span data-ttu-id="d5c32-109">使用 Azure 磁碟加密的 Windows 和 Linux 虛擬機器均可提供支援，Azure 磁碟加密會運用業界標準的 Windows BitLocker 功能與 Linux 的 DM-Crypt 功能來提供磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-109">It is supported for both Windows and Linux virtual machines using Azure Disk Encryption, which leverages the industry standard BitLocker feature of Windows and DM-Crypt feature of Linux to provide encryption of disks.</span></span> <br>
> * <span data-ttu-id="d5c32-110">只有使用「BitLocker 加密金鑰」和「金鑰加密金鑰」加密的虛擬機器才提供支援。</span><span class="sxs-lookup"><span data-stu-id="d5c32-110">It is supported only for virtual machines encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span> <span data-ttu-id="d5c32-111">只使用「BitLocker 加密金鑰」加密的虛擬機器不提供支援。</span><span class="sxs-lookup"><span data-stu-id="d5c32-111">It is not supported for virtual machines encrypted using BitLocker Encryption Key only.</span></span> <br>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d5c32-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5c32-112">Prerequisites</span></span>
1. <span data-ttu-id="d5c32-113">虛擬機器已使用 [Azure 磁碟加密](../security/azure-security-disk-encryption.md)進行加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-113">Virtual machine has been encrypted using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span></span> <span data-ttu-id="d5c32-114">應使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-114">It should be encrypted using BitLocker Encryption Key and Key Encryption Key both.</span></span>
2. <span data-ttu-id="d5c32-115">已建立復原服務保存庫，並使用[準備環境以便備份](backup-azure-arm-vms-prepare.md)一文所述的步驟設定儲存體複寫。</span><span class="sxs-lookup"><span data-stu-id="d5c32-115">Recovery services vault has been created and storage replication set using steps mentioned in the article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>
3. <span data-ttu-id="d5c32-116">Azure 備份已獲得[存取金鑰保存庫 (內含已加密 VM 的金鑰、祕密) 的權限](#provide-permissions-to-azure-backup)。</span><span class="sxs-lookup"><span data-stu-id="d5c32-116">Azure Backup has been given [permissions to access key vault](#provide-permissions-to-azure-backup) containing keys, secrets for encrypted VMs.</span></span>

## <a name="backup-encrypted-vm"></a><span data-ttu-id="d5c32-117">備份加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d5c32-117">Backup encrypted VM</span></span>
<span data-ttu-id="d5c32-118">使用下列步驟來設定備份目標、定義原則、設定項目和觸發備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-118">Use the following steps to set backup goal, define policy, configure items and trigger backup.</span></span>

### <a name="configure-backup"></a><span data-ttu-id="d5c32-119">設定備份</span><span class="sxs-lookup"><span data-stu-id="d5c32-119">Configure backup</span></span>
1. <span data-ttu-id="d5c32-120">如果您已開啟復原服務保存庫，請繼續下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-120">If you already have a Recovery Services vault open, proceed to next step.</span></span> <span data-ttu-id="d5c32-121">如果您並未開啟復原服務保存庫，但位於 Azure 入口網站中，請在 [中樞] 功能表上按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="d5c32-121">If you do not have a Recovery Services vault open, but are in the Azure portal, on the Hub menu, click **Browse**.</span></span>

   * <span data-ttu-id="d5c32-122">在資源清單中輸入 **復原服務**。</span><span class="sxs-lookup"><span data-stu-id="d5c32-122">In the list of resources, type **Recovery Services**.</span></span>
   * <span data-ttu-id="d5c32-123">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="d5c32-123">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="d5c32-124">當您看到 [復原服務保存庫] 時，請按一下它。</span><span class="sxs-lookup"><span data-stu-id="d5c32-124">When you see **Recovery Services vaults**, click it.</span></span>

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     <span data-ttu-id="d5c32-126">隨即會出現 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="d5c32-126">The list of Recovery Services vaults appears.</span></span> <span data-ttu-id="d5c32-127">在 [復原服務保存庫] 清單中選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5c32-127">From the list of Recovery Services vaults, select a vault.</span></span>

     <span data-ttu-id="d5c32-128">選取的保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-128">The selected vault dashboard opens.</span></span>
2. <span data-ttu-id="d5c32-129">從出現在保存庫下方的項目清單中，按一下 [備份] 以開啟 [備份] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d5c32-129">From the list of items that appears under vault, click **Backup** to open the Backup blade.</span></span>

      ![開啟 [備份] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup.png)
3. <span data-ttu-id="d5c32-131">在 [備份] 刀鋒視窗中，按一下 [備份目標]  以開啟 [備份目標] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d5c32-131">On the Backup blade, click **Backup goal** to open the Backup Goal blade.</span></span>

      ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. <span data-ttu-id="d5c32-133">在 [備份目標] 刀鋒視窗中，將 [工作負載的執行位置] 設定為 [Azure]，並將 [欲備份的項目] 設定為 [虛擬機器]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-133">On the Backup Goal blade, set **Where is your workload running** to Azure and **What do you want to backup** to Virtual machine, then click **OK**.</span></span>

   <span data-ttu-id="d5c32-134">[備份目標] 刀鋒視窗隨即關閉，然後開啟 [備份原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d5c32-134">The Backup Goal blade closes and the Backup policy blade opens.</span></span>

   ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. <span data-ttu-id="d5c32-136">在 [備份原則] 刀鋒視窗中選取您要套用至保存庫的備份原則，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5c32-136">On the Backup policy blade, select the backup policy you want to apply to the vault and click **OK**.</span></span>

      ![選取備份原則](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    <span data-ttu-id="d5c32-138">預設原則的詳細資料便會列在詳細資料中。</span><span class="sxs-lookup"><span data-stu-id="d5c32-138">The details of the default policy are listed in the details.</span></span> <span data-ttu-id="d5c32-139">如果您想要建立原則，請在下拉式功能表中選取 [建立新的]  。</span><span class="sxs-lookup"><span data-stu-id="d5c32-139">If you want to create a policy, select **Create New** from the drop-down menu.</span></span> <span data-ttu-id="d5c32-140">一旦您按下 [確定] ，備份原則便會與保存庫建立關聯。</span><span class="sxs-lookup"><span data-stu-id="d5c32-140">Once you click **OK**, the backup policy is associated with the vault.</span></span>

    <span data-ttu-id="d5c32-141">接下來選擇要與保存庫建立關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-141">Next choose the VMs to associate with the vault.</span></span>
6. <span data-ttu-id="d5c32-142">選擇要與指定的原則建立關聯的已加密虛擬機器，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-142">Choose the encrypted virtual machines to associate with the specified policy and click **OK**.</span></span>

      ![選取加密的 VM](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. <span data-ttu-id="d5c32-144">此頁面會顯示與所選加密的 VM 相關聯的金鑰保存庫相關訊息。</span><span class="sxs-lookup"><span data-stu-id="d5c32-144">This page shows a message about key vault associated to the encrypted VMs selected.</span></span> <span data-ttu-id="d5c32-145">備份服務需要金鑰保存庫中金鑰和密碼的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="d5c32-145">Backup service requires read-only access to the keys and secrets in the key vault.</span></span> <span data-ttu-id="d5c32-146">它會使用這些權限來備份金鑰和密碼，以及相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-146">It uses these permissions to backup key and secret, along with the associated VMs.</span></span> <span data-ttu-id="d5c32-147">**您必須將金鑰保存庫的存取權限授與備份服務才能進行備份**。</span><span class="sxs-lookup"><span data-stu-id="d5c32-147">**You must give permissions to backup service to access key vault for backups to work**.</span></span> <span data-ttu-id="d5c32-148">您可以使用[下一節所述的步驟](#provide-permissions-to-azure-backup)來提供這些權限。</span><span class="sxs-lookup"><span data-stu-id="d5c32-148">You can provide these permissions using [steps mentioned in the section below](#provide-permissions-to-azure-backup).</span></span>

      ![加密的 VM 訊息](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      <span data-ttu-id="d5c32-150">現在您已定義保存庫的所有設定，接下來在 [備份] 刀鋒視窗中按一下頁面底部的 [啟用備份]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-150">Now that you have defined all settings for the vault, in the Backup blade click Enable Backup at the bottom of the page.</span></span> <span data-ttu-id="d5c32-151">[啟用備份] 可將原則部署到保存庫和 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-151">Enable  Backup deploys the policy to the vault and the VMs.</span></span>
8. <span data-ttu-id="d5c32-152">下一個階段的準備作業是安裝 VM 代理程式，或確定 VM 代理程式已安裝。</span><span class="sxs-lookup"><span data-stu-id="d5c32-152">The next phase in preparation is installing the VM Agent or making sure the VM Agent is installed.</span></span> <span data-ttu-id="d5c32-153">若要執行相同的動作，請使用[準備環境以便備份](backup-azure-arm-vms-prepare.md)一文中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-153">To do the same, use the steps mentioned in the article [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

### <a name="triggering-backup-job"></a><span data-ttu-id="d5c32-154">觸發備份作業</span><span class="sxs-lookup"><span data-stu-id="d5c32-154">Triggering backup job</span></span>
<span data-ttu-id="d5c32-155">使用[將 Azure VM 備份至復原服務保存庫](backup-azure-arm-vms.md)一文中所述的步驟來觸發備份作業。</span><span class="sxs-lookup"><span data-stu-id="d5c32-155">Use the steps mentioned in the article [Backup Azure VMs to recovery services vault](backup-azure-arm-vms.md) to trigger backup job.</span></span>

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a><span data-ttu-id="d5c32-156">將啟用加密之已備份 VM 繼續備份</span><span class="sxs-lookup"><span data-stu-id="d5c32-156">Continue backups of already backed up VMs with encryption enabled</span></span>  
<span data-ttu-id="d5c32-157">如果您的 VM 已在復原服務保存庫中進行備份，並於稍後已啟用加密，您必須將備份服務的權限提供給金鑰保存庫，才可繼續進行備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-157">If you have VMs already being backup up in recovery services vault and have been enabled for encryption at a later point, you must give permissions to backup service to access key vault for backups to continue.</span></span> <span data-ttu-id="d5c32-158">您可以使用[下一節的步驟](#provide-permissions-to-azure-backup)或使用 [PowerShell 文件](backup-azure-vms-automation.md)的**啟用備份**一節中所述的 PowerShell 步驟，來提供這些權限。</span><span class="sxs-lookup"><span data-stu-id="d5c32-158">You can provide these permissions using [steps in the section below](#provide-permissions-to-azure-backup) or using PowerShell steps mentioned in **Enable Backup** section of [PowerShell documentation](backup-azure-vms-automation.md).</span></span> 

## <a name="provide-permissions-to-azure-backup"></a><span data-ttu-id="d5c32-159">對 Azure 備份提供權限</span><span class="sxs-lookup"><span data-stu-id="d5c32-159">Provide permissions to Azure Backup</span></span>
<span data-ttu-id="d5c32-160">使用下列步驟來提供相關權限給 Azure 備份，以供其存取金鑰保存庫並執行已加密 VM 的備份：</span><span class="sxs-lookup"><span data-stu-id="d5c32-160">Use the following steps to provide relevant permissions to Azure Backup to access key vault and perform backup of encrypted VMs:</span></span>
1. <span data-ttu-id="d5c32-161">選取 [更多服務]，然後搜尋 [金鑰保存庫]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-161">Select **More Services** and search for **Key vaults**.</span></span>

    ![搜尋金鑰保存庫](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. <span data-ttu-id="d5c32-163">從金鑰保存庫清單中選取與已加密之 VM 相關聯的金鑰保存庫，以讓其進行備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-163">From the list of key vaults, select the key vault associated with encrypted VM, which needs to be backed up.</span></span>

     ![選取金鑰保存庫](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. <span data-ttu-id="d5c32-165">按一下 [存取原則] 然後 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-165">Click **Access policies** and then **Add new**.</span></span>

    ![新增存取原則](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. <span data-ttu-id="d5c32-167">按一下 [選取主體]，然後在搜尋列中輸入**備份管理服務**。</span><span class="sxs-lookup"><span data-stu-id="d5c32-167">Click **Select principal** and type **Backup Management Service** in the search bar.</span></span> 

    ![搜尋備份服務](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. <span data-ttu-id="d5c32-169">選取 [備份管理服務]，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5c32-169">Select **Backup Management Service** and click Select button.</span></span>

    ![選取備份服務](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. <span data-ttu-id="d5c32-171">在 [從範本設定] 下拉式功能表中選取 [Azure 備份]。</span><span class="sxs-lookup"><span data-stu-id="d5c32-171">Select **Azure Backup** in Configure from template drop down.</span></span> <span data-ttu-id="d5c32-172">該備份會在 [金鑰權限和祕密權限] 下拉式清單中預先填入必要的權限。</span><span class="sxs-lookup"><span data-stu-id="d5c32-172">It pre-fills the required permissions in Key permissions and Secret permissions drop down.</span></span> 

    ![選取 Azure 備份](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. <span data-ttu-id="d5c32-174">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5c32-174">Click **OK**.</span></span> <span data-ttu-id="d5c32-175">請注意「備份管理服務」會新增到 [存取原則] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d5c32-175">Notice that Backup Management Service gets added in Access Policies blade.</span></span> 

    ![備份服務存取原則](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. <span data-ttu-id="d5c32-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d5c32-177">Click **Save**.</span></span> <span data-ttu-id="d5c32-178">這會對 Azure 備份提供必要權限。</span><span class="sxs-lookup"><span data-stu-id="d5c32-178">This will give the required permissions to Azure Backup.</span></span>

    ![備份服務存取原則](./media/backup-azure-vms-encryption/save-access-policy.png)

<span data-ttu-id="d5c32-180">順利提供權限後，您可以繼續為已加密的 VM 啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-180">Once permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span></span>

## <a name="restore-encrypted-vm"></a><span data-ttu-id="d5c32-181">還原已加密的 VM</span><span class="sxs-lookup"><span data-stu-id="d5c32-181">Restore encrypted VM</span></span>
<span data-ttu-id="d5c32-182">若要還原加密的 VM，請先使用[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)的＜還原備份的磁碟＞一節中所述的步驟來還原磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-182">To restore encrypted VM, first Restore Disks using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="d5c32-183">之後，您可以使用下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="d5c32-183">After that, you can use one of the following options:</span></span>
* <span data-ttu-id="d5c32-184">使用[從還原的磁碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) 中所述的 PowerShell 步驟，從還原的磁碟建立完整的 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-184">Use the PowerShell steps mentioned in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create full VM from restored disks.</span></span>
* <span data-ttu-id="d5c32-185">或者，[使用產生作為還原磁碟一部分的範本](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm)，從還原的磁碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="d5c32-185">OR, [Use template generated as part of Restore Disks](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) to create VMs from restored disks.</span></span> <span data-ttu-id="d5c32-186">只可將範本用於 2017 年 4 月 26 日之後建立的復原點。</span><span class="sxs-lookup"><span data-stu-id="d5c32-186">Templates can be used only for recovery points created after 26 April 2017.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="d5c32-187">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="d5c32-187">Troubleshooting errors</span></span>
| <span data-ttu-id="d5c32-188">作業</span><span class="sxs-lookup"><span data-stu-id="d5c32-188">Operation</span></span> | <span data-ttu-id="d5c32-189">錯誤詳細資料</span><span class="sxs-lookup"><span data-stu-id="d5c32-189">Error details</span></span> | <span data-ttu-id="d5c32-190">解決方案</span><span class="sxs-lookup"><span data-stu-id="d5c32-190">Resolution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5c32-191">備份</span><span class="sxs-lookup"><span data-stu-id="d5c32-191">Backup</span></span> |<span data-ttu-id="d5c32-192">驗證失敗，因為虛擬機器單獨以 BEK 進行加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-192">Validation failed as virtual machine is encrypted with BEK alone.</span></span> <span data-ttu-id="d5c32-193">只會對同時使用 BEK 和 KEK 加密的虛擬機器啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-193">Backups can be enabled only for virtual machines encrypted with both BEK and KEK.</span></span> |<span data-ttu-id="d5c32-194">應該使用 BEK 和 KEK 來加密虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5c32-194">Virtual machine should be encrypted using BEK and KEK.</span></span> <span data-ttu-id="d5c32-195">先解密 VM，再使用 BEK 和 KEK 將它加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-195">First decrypt the VM and encrypt it using both BEK and KEK.</span></span> <span data-ttu-id="d5c32-196">使用 BEK 和 KEK 加密 VM 之後，啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-196">Enable backup once VM is encrypted using both BEK and KEK.</span></span> <span data-ttu-id="d5c32-197">了解如何[解密及加密 VM](../security/azure-security-disk-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="d5c32-197">Learn more on how you can [decrypt and encrypt the VM](../security/azure-security-disk-encryption.md)</span></span>  |
| <span data-ttu-id="d5c32-198">還原</span><span class="sxs-lookup"><span data-stu-id="d5c32-198">Restore</span></span> |<span data-ttu-id="d5c32-199">您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰保存庫不存在。</span><span class="sxs-lookup"><span data-stu-id="d5c32-199">You cannot restore this encrypted VM since key vault associated with this VM does not exist.</span></span> |<span data-ttu-id="d5c32-200">利用[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)，建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5c32-200">Create key vault using [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span> <span data-ttu-id="d5c32-201">請參閱[使用 Azure 備份來還原金鑰保存庫金鑰和密碼](backup-azure-restore-key-secret.md)文章來還原金鑰和密碼 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="d5c32-201">Refer the article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) to restore key and secret if they are not present.</span></span> |
| <span data-ttu-id="d5c32-202">還原</span><span class="sxs-lookup"><span data-stu-id="d5c32-202">Restore</span></span> |<span data-ttu-id="d5c32-203">您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰和密碼不存在。</span><span class="sxs-lookup"><span data-stu-id="d5c32-203">You cannot restore this encrypted VM since key and secret associated with this VM do not exist.</span></span> |<span data-ttu-id="d5c32-204">請參閱[使用 Azure 備份來還原金鑰保存庫金鑰和密碼](backup-azure-restore-key-secret.md)文章來還原金鑰和密碼 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="d5c32-204">Refer the article [Restore key vault key and secret using Azure Backup](backup-azure-restore-key-secret.md) to restore key and secret if they are not present.</span></span> |
| <span data-ttu-id="d5c32-205">還原</span><span class="sxs-lookup"><span data-stu-id="d5c32-205">Restore</span></span> |<span data-ttu-id="d5c32-206">備份服務無權存取您訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="d5c32-206">Backup Service does not have authorization to access resources in your subscription.</span></span> |<span data-ttu-id="d5c32-207">如前所述，請先使用[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)的＜還原備份的磁碟＞一節中所述的步驟來還原磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5c32-207">As mentioned above, Restore Disks first, using steps mentioned in section **Restore backed up disks** in [Choosing VM restore configuration](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration).</span></span> <span data-ttu-id="d5c32-208">之後，使用 PowerShell 來[從還原的磁碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)。</span><span class="sxs-lookup"><span data-stu-id="d5c32-208">After that, user PowerShell to [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span></span> |
|<span data-ttu-id="d5c32-209">備份</span><span class="sxs-lookup"><span data-stu-id="d5c32-209">Backup</span></span> | <span data-ttu-id="d5c32-210">Azure 備份服務沒有足夠的 Key Vault權限可備份加密的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d5c32-210">Azure Backup Service does not have sufficient permissions to Key Vault for Backup of Encrypted Virtual Machines</span></span> | <span data-ttu-id="d5c32-211">虛擬機器應該使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。</span><span class="sxs-lookup"><span data-stu-id="d5c32-211">Virtual machine should be encrypted using both BitLocker Encryption Key and Key Encryption Key.</span></span> <span data-ttu-id="d5c32-212">之後，應該啟用備份。</span><span class="sxs-lookup"><span data-stu-id="d5c32-212">After that, backup should be enabled.</span></span>  <span data-ttu-id="d5c32-213">您應該使用[上一節所述步驟](#provide-permissions-to-azure-backup)或[使用 AzureRM.RecoveryServices.Backup Cmdlet 備份虛擬機器](backup-azure-vms-automation.md#back-up-azure-vms)的 PowerShell 文件中的**啟用保護**一節所提到的 PowerShell 步驟，為備份服務提供這些權限。</span><span class="sxs-lookup"><span data-stu-id="d5c32-213">Backup service should be provided these permissions using [steps mentioned in the section above](#provide-permissions-to-azure-backup) or by using PowerShell steps mentioned in the **Enable protection** section of the PowerShell documentation at [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md#back-up-azure-vms).</span></span> |  
