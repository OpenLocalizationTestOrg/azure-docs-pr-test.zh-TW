---
title: "從備份虛擬機器的 aaaRestore |Microsoft 文件"
description: "了解如何 toorestore Azure 虛擬機器的復原點"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "還原備份;如何 toorestore;復原點。"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a><span data-ttu-id="bf5c0-104">還原 Azure 中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bf5c0-104">Restore virtual machines in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf5c0-105">在 Azure 入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-105">Restore VMs in Azure portal</span></span>](backup-azure-arm-restore-vms.md)
> * [<span data-ttu-id="bf5c0-106">在傳統入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-106">Restore VMs in Classic portal</span></span>](backup-azure-restore-vms.md)
>
>

<span data-ttu-id="bf5c0-107">還原虛擬機器 tooa hello 遵循與儲存在 Azure 備份保存庫中的 hello 備份中的新 VM 的步驟。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-107">Restore a virtual machine tooa new VM from hello backups stored in an Azure Backup vault with hello following steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf5c0-108">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="bf5c0-109">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="bf5c0-110">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="bf5c0-111">**2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="bf5c0-112">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="bf5c0-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="bf5c0-113">任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="bf5c0-114">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="bf5c0-115">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="restore-workflow"></a><span data-ttu-id="bf5c0-116">還原工作流程</span><span class="sxs-lookup"><span data-stu-id="bf5c0-116">Restore workflow</span></span>
### <a name="step-1-choose-an-item-toorestore"></a><span data-ttu-id="bf5c0-117">步驟 1： 選擇的項目 toorestore</span><span class="sxs-lookup"><span data-stu-id="bf5c0-117">Step 1: Choose an item toorestore</span></span>
1. <span data-ttu-id="bf5c0-118">瀏覽 toohello**受保護項目** 索引標籤，然後選取 hello 想 toorestore tooa 虛擬機器新的 VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-118">Navigate toohello **Protected Items** tab and select hello virtual machine you want toorestore tooa new VM.</span></span>

    ![受保護項目](./media/backup-azure-restore-vms/protected-items.png)

    <span data-ttu-id="bf5c0-120">hello**復原點**hello 中的資料行**受保護項目**頁面會告訴您 hello 的虛擬機器的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-120">hello **Recovery Point** column in hello **Protected Items** page will tell you hello number of recovery points for a virtual machine.</span></span> <span data-ttu-id="bf5c0-121">hello **Newest 復原點**資料行告訴您 hello hello 在還原虛擬機器的最新備份的時間。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-121">hello **Newest Recovery Point** column tells you hello time of hello most recent backup from which a virtual machine can be restored.</span></span>
2. <span data-ttu-id="bf5c0-122">按一下**還原**tooopen hello**還原的項目**精靈。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-122">Click **Restore** tooopen hello **Restore an Item** wizard.</span></span>

    ![還原項目](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a><span data-ttu-id="bf5c0-124">步驟 2：挑選復原點</span><span class="sxs-lookup"><span data-stu-id="bf5c0-124">Step 2: Pick a recovery point</span></span>
1. <span data-ttu-id="bf5c0-125">在 [hello**選取的復原點**] 畫面上，您可以還原從 hello 最新復原點，或從先前的點的時間。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-125">In hello **select a recovery point** screen, you can restore from hello newest recovery point, or from a previous point in time.</span></span> <span data-ttu-id="bf5c0-126">hello 選取當精靈開啟時的預設選項是*Newest 復原點*。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-126">hello default option selected when wizard opens is *Newest Recovery Point*.</span></span>

    ![選取復原點](./media/backup-azure-restore-vms/select-recovery-point.png)
2. <span data-ttu-id="bf5c0-128">較早的時間點 toopick 選擇 hello**選取日期**hello 下拉式清單中的選項和 hello 月曆控制項中選取日期，按一下 hello**行事曆圖示**。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-128">toopick an earlier point in time, choose hello **Select Date** option in hello dropdown and select a date in hello calendar control by clicking on hello **calendar icon**.</span></span> <span data-ttu-id="bf5c0-129">Hello 控制項中所有復原點的日期會以淺灰色陰影填滿，並選取 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-129">In hello control, all dates that have recovery points are filled with a light gray shade and are selectable by hello user.</span></span>

    ![選取日期](./media/backup-azure-restore-vms/select-date.png)

    <span data-ttu-id="bf5c0-131">一旦您按一下 hello 月曆控制項中的日期的 hello 復原點可以使用上表的復原點中，將會顯示日期。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-131">Once you click a date in hello calendar control, hello recovery points available on that date will be shown in recovery points table below.</span></span> <span data-ttu-id="bf5c0-132">hello**時間**資料行會指出 hello 的 hello 在擷取快照當時的時間。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-132">hello **Time** column indicates hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="bf5c0-133">hello**類型**資料行會顯示 hello[一致性](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points)hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-133">hello **Type** column displays hello [consistency](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) of hello recovery point.</span></span> <span data-ttu-id="bf5c0-134">hello 資料表標頭會顯示在括號括住的那一天的 hello 可用的復原點的數目。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-134">hello table header shows hello number of recovery points available on that day in parentheses.</span></span>

    ![復原點](./media/backup-azure-restore-vms/recovery-points.png)
3. <span data-ttu-id="bf5c0-136">選取 hello 復原點從 hello**復原點**資料表，並按一下 hello 下一步 箭號 toogo toohello 下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-136">Select hello recovery point from hello **Recovery Points** table and click hello Next arrow toogo toohello next screen.</span></span>

### <a name="step-3-specify-a-destination-location"></a><span data-ttu-id="bf5c0-137">步驟 3：指定目的地位置</span><span class="sxs-lookup"><span data-stu-id="bf5c0-137">Step 3: Specify a destination location</span></span>
1. <span data-ttu-id="bf5c0-138">在 hello**選取還原執行個體**螢幕指定 toorestore hello 虛擬機器的位置詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-138">In hello **Select restore instance** screen specify details of where toorestore hello virtual machine.</span></span>

   * <span data-ttu-id="bf5c0-139">指定 hello 虛擬機器名稱： 在指定的雲端服務中，hello 虛擬機器名稱應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-139">Specify hello virtual machine name: In a given cloud service, hello virtual machine name should be unique.</span></span> <span data-ttu-id="bf5c0-140">我們不支援覆寫現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-140">We don't support over-writing existing VM.</span></span>
   * <span data-ttu-id="bf5c0-141">選取 hello VM 的雲端服務： 這是必要的用於建立 VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-141">Select a cloud service for hello VM: This is mandatory for creating a VM.</span></span> <span data-ttu-id="bf5c0-142">您可以選擇 tooeither 使用現有的雲端服務，或建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-142">You can choose tooeither use an existing cloud service or create a new cloud service.</span></span>

        <span data-ttu-id="bf5c0-143">挑選的雲端服務名稱應具有全域唯一性。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-143">Whatever cloud service name is picked should be globally unique.</span></span> <span data-ttu-id="bf5c0-144">通常，hello 雲端服務名稱會取得 [cloudservice] hello 形式公開 URL 相關聯。.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-144">Typically, hello cloud service name gets associated with a public-facing URL in hello form of [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="bf5c0-145">Azure 不允許您 toocreate 新的雲端服務如果 hello 名稱已經使用。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-145">Azure will not allow you toocreate a new cloud service if hello name has already been used.</span></span> <span data-ttu-id="bf5c0-146">如果您選擇 toocreate 新的雲端服務，它會指定為 hello 虛擬機器 – 在哪一個案例的 hello VM 名稱相同的 hello 挑選的名稱應該是唯一不足，無法套用的 toobe toohello 相關聯雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-146">If you choose toocreate a new cloud service, it will be given hello same name as hello virtual machine – in which case hello VM name picked should be unique enough toobe applied toohello associated cloud service.</span></span>

        <span data-ttu-id="bf5c0-147">我們只會顯示雲端服務和虛擬網路不在 hello 任何同質群組相關聯的還原執行個體詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-147">We only display cloud services and virtual networks that are not associated with any affinity groups in hello restore instance details.</span></span> <span data-ttu-id="bf5c0-148">[深入了解](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-148">[Learn More](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
2. <span data-ttu-id="bf5c0-149">選取 hello VM 的存放裝置帳戶： 這是必要的建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-149">Select a storage account for hello VM: This is mandatory for creating hello VM.</span></span> <span data-ttu-id="bf5c0-150">您可以選擇從現有的儲存體帳戶 hello 相同 hello Azure 備份保存庫與區域。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-150">You can select from existing storage accounts in hello same region as hello Azure Backup vault.</span></span> <span data-ttu-id="bf5c0-151">我們不支援區域備援或進階儲存體類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-151">We don’t support storage accounts that are Zone redundant or of Premium storage type.</span></span>

    <span data-ttu-id="bf5c0-152">如果有任何儲存體帳戶，以支援的組態，請建立儲存體帳戶的支援的設定先前 toostarting 還原作業。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-152">If there are no storage accounts with supported configuration, please create a storage account of supported configuration prior toostarting restore operation.</span></span>

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-sa.png)
3. <span data-ttu-id="bf5c0-154">選取虛擬網路： hello 虛擬網路 (VNET) 的 hello 虛擬機器應建立的 hello 次選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-154">Select a Virtual Network: hello virtual network (VNET) for hello virtual machine should be selected at hello time of creating hello VM.</span></span> <span data-ttu-id="bf5c0-155">hello 還原 UI 會顯示可以使用此訂用帳戶內的所有 hello Vnet。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-155">hello restore UI shows all hello VNETs within this subscription that can be used.</span></span> <span data-ttu-id="bf5c0-156">不是強制性 tooselect VNET 的 hello 還原 VM – 您可以 tooconnect toohello 還原虛擬機器可透過 hello 網際網路即使 hello VNET 不會套用。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-156">It is not mandatory tooselect a VNET for hello restored VM – you will be able tooconnect toohello restored virtual machine over hello internet even if hello VNET is not applied.</span></span>

    <span data-ttu-id="bf5c0-157">如果 hello 雲端服務選取是相關聯的虛擬網路，您無法變更 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-157">If hello cloud service selected is associated with a virtual network, then you cannot change hello virtual network.</span></span>

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. <span data-ttu-id="bf5c0-159">選取子網路： hello VNET 有子網路，以免預設 hello 第一個子網路會選取。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-159">Select a subnet: In case hello VNET has subnets, by default hello first subnet will be selected.</span></span> <span data-ttu-id="bf5c0-160">從 hello 下拉式清單選項中選擇您所選擇的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-160">Choose hello subnet of your choice from hello dropdown options.</span></span> <span data-ttu-id="bf5c0-161">子網路的詳細資訊，請在 hello tooNetworks 延伸模組[入口網站首頁](https://manage.windowsazure.com/)，跳過**虛擬網路**選取 hello 虛擬網路和向下切入至 設定 toosee 子網路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-161">For subnet details, go tooNetworks extension in hello [portal home page](https://manage.windowsazure.com/), go too**Virtual Networks** and select hello virtual network and drill down into Configure toosee subnet details.</span></span>

    ![選取子網路](./media/backup-azure-restore-vms/select-subnet.png)
5. <span data-ttu-id="bf5c0-163">按一下 hello**送出**圖示 hello 精靈 toosubmit hello 詳細資料，並建立還原工作。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-163">Click hello **Submit** icon in hello wizard toosubmit hello details and create a restore job.</span></span>

## <a name="track-hello-restore-operation"></a><span data-ttu-id="bf5c0-164">追蹤 hello 還原作業</span><span class="sxs-lookup"><span data-stu-id="bf5c0-164">Track hello Restore operation</span></span>
<span data-ttu-id="bf5c0-165">一旦您已輸入到 hello 還原精靈的所有 hello 資訊並將它提交 Azure 備份將會嘗試 toocreate 作業 tootrack hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-165">Once you have input all hello information into hello restore wizard and submitted it Azure Backup will try toocreate a job tootrack hello restore operation.</span></span>

![正在建立還原工作](./media/backup-azure-restore-vms/create-restore-job.png)

<span data-ttu-id="bf5c0-167">如果建立 hello 工作成功時，您會看到快顯通知，表示該 hello 作業已建立。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-167">If hello job creation is successful, you will see a toast notification indicating that hello job is created.</span></span> <span data-ttu-id="bf5c0-168">您可以取得更多詳細資料，只要按一下 hello**檢視工作**按鈕會引導您太**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-168">You can get more details by clicking hello **View Job** button that will take you too**Jobs** tab.</span></span>

![已建立還原工作](./media/backup-azure-restore-vms/restore-job-created.png)

<span data-ttu-id="bf5c0-170">在 hello 還原作業完成時，它將會標示為已完成在**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-170">Once hello restore operation is finished, it will be marked as completed in **Jobs** tab.</span></span>

![已完成還原工作](./media/backup-azure-restore-vms/restore-job-complete.png)

<span data-ttu-id="bf5c0-172">還原 hello 您可能需要 toore 安裝 hello 擴充功能上的現有虛擬機器之後 hello 原始 VM 和[修改 hello 端點](../virtual-machines/windows/classic/setup-endpoints.md)hello hello Azure 入口網站中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-172">After restoring hello virtual machine you may need toore-install hello extensions existing on hello original VM and [modify hello endpoints](../virtual-machines/windows/classic/setup-endpoints.md) for hello virtual machine in hello Azure portal.</span></span>

## <a name="post-restore-steps"></a><span data-ttu-id="bf5c0-173">還原後的步驟</span><span class="sxs-lookup"><span data-stu-id="bf5c0-173">Post-Restore steps</span></span>
<span data-ttu-id="bf5c0-174">如果您使用 cloud-init 型 Linux 散發套件 (例如 Ubuntu)，為求安全，還原後將會封鎖密碼。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-174">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password will be blocked post restore.</span></span> <span data-ttu-id="bf5c0-175">請使用 VMAccess 擴充功能上 hello 還原 VM 太[重設 hello 密碼](../virtual-machines/linux/classic/reset-access.md)。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-175">Please use VMAccess extension on hello restored VM too[reset hello password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="bf5c0-176">我們建議使用重設密碼後還原這些散發 tooavoid 上的 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-176">We recommend using SSH keys on these distributions tooavoid resetting password post restore.</span></span>

## <a name="backup-for-restored-vms"></a><span data-ttu-id="bf5c0-177">備份還原 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-177">Backup for Restored VMs</span></span>
<span data-ttu-id="bf5c0-178">如果您已還原為原始備份 VM 名稱相同的 hello 與 VM toosame 雲端服務，VM 後還原 hello 會繼續備份。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-178">If you have restored VM toosame cloud service with hello same name as originally backed up VM, backup will continue on hello VM post restore.</span></span> <span data-ttu-id="bf5c0-179">如果您有還原 VM tooa 不同雲端服務，或指定不同的名稱還原的 VM，這將會被視為新的 VM，以及您還原的 VM 需要 toosetup 備份。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-179">If you have either restored VM tooa different cloud service or specified a different name for restored VM, this will be treated as a new VM and you need toosetup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="bf5c0-180">在 Azure 資料中心發生災害時還原 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-180">Restoring a VM during Azure DataCenter Disaster</span></span>
<span data-ttu-id="bf5c0-181">Azure Backup 可讓以防 hello 主要資料中心 Vm 正在執行體驗災害而設定備份保存庫 toobe 異地備援，還原備份 Vm toohello 成對的資料中心。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-181">Azure Backup allows restoring backed up VMs toohello paired data center in case hello primary data center where VMs are running experiences disaster and you configured Backup vault toobe geo-redundant.</span></span> <span data-ttu-id="bf5c0-182">在這種情況下，您需要 tooselect 成對的資料中心內提供的儲存體帳戶與 hello 還原程序的其餘部分會保持相同。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-182">During such scenarios, you need tooselect a storage account which is present in paired data center and rest of hello restore process remains same.</span></span> <span data-ttu-id="bf5c0-183">Azure Backup 使用從配對的地理 toocreate hello 還原虛擬機器的計算服務。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-183">Azure Backup uses Compute service from paired geo toocreate hello restored virtual machine.</span></span> <span data-ttu-id="bf5c0-184">深入了解 [Azure 資料中心復原](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-184">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-domain-controller-vms"></a><span data-ttu-id="bf5c0-185">還原網域控制站 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-185">Restoring Domain Controller VMs</span></span>
<span data-ttu-id="bf5c0-186">備份網域控制站 (DC) 虛擬機器是 Azure 備份支援的案例。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-186">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span></span> <span data-ttu-id="bf5c0-187">不過，必須小心 hello 還原程序。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-187">However, care must be taken during hello restore process.</span></span> <span data-ttu-id="bf5c0-188">hello 正確的還原程序取決於 hello hello 網域結構。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-188">hello correct restore process depends on hello structure of hello domain.</span></span> <span data-ttu-id="bf5c0-189">在 hello 簡單的案例中，您會有單一 DC 在單一網域。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-189">In hello simplest case you have a single DC in a single domain.</span></span> <span data-ttu-id="bf5c0-190">而在生產環境的負載中，較常見的情況是您擁有單一網域且內含多個 DC，其中有些 DC 可能位於內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-190">More commonly for production loads, you will have a single domain with multiple DCs, perhaps with some DCs on premises.</span></span> <span data-ttu-id="bf5c0-191">最後，您也可能擁有內含多個網域的樹系。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-191">Finally, you may have a forest with multiple domains.</span></span>

<span data-ttu-id="bf5c0-192">從 Active Directory 的觀點來看 hello Azure VM 是像現代支援的 hypervisor 上的其他 VM。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-192">From an Active Directory perspective hello Azure VM is like any other VM on a modern supported hypervisor.</span></span> <span data-ttu-id="bf5c0-193">hello 與內部 hypervisor 的主要差異是，沒有任何 VM 主控台在 Azure 中可用。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-193">hello major difference with on-premises hypervisors is that there is no VM console available in Azure.</span></span> <span data-ttu-id="bf5c0-194">在某些情況下，您必須使用主控台，例如使用裸機復原 (BMR) 類型的備份進行復原。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-194">A console is required for certain scenarios such as recovering using a Bare Metal Recovery (BMR) type backup.</span></span> <span data-ttu-id="bf5c0-195">不過，hello 備份保存庫中的 VM 還原是完整取代用於執行 BMR。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-195">However, VM restore from hello backup vault is a full replacement for BMR.</span></span> <span data-ttu-id="bf5c0-196">我們也提供了 Active Directory 還原模式 (DSRM)，因此，您可以進行所有的 Active Directory 復原案例。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-196">Active Directory Restore Mode (DSRM) is also available, so all Active Directory recovery scenarios are viable.</span></span> <span data-ttu-id="bf5c0-197">如需更多背景資訊，請參閱[虛擬網域控制站的備份和還原考量](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)以及[規劃 Active Directory 樹系復原](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-197">For more background information, please check [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) and [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).</span></span>

### <a name="single-dc-in-a-single-domain"></a><span data-ttu-id="bf5c0-198">單一網域中的單一 DC</span><span class="sxs-lookup"><span data-stu-id="bf5c0-198">Single DC in a single domain</span></span>
<span data-ttu-id="bf5c0-199">hello VM 可以還原 （就像任何其他 VM) 從 hello Azure 入口網站或使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-199">hello VM can be restored (like any other VM) from hello Azure portal or using PowerShell.</span></span>

### <a name="multiple-dcs-in-a-single-domain"></a><span data-ttu-id="bf5c0-200">單一網域中的多個 DC</span><span class="sxs-lookup"><span data-stu-id="bf5c0-200">Multiple DCs in a single domain</span></span>
<span data-ttu-id="bf5c0-201">當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-201">When other DCs of hello same domain can be reached over hello network, hello DC can be restored like any VM.</span></span> <span data-ttu-id="bf5c0-202">如果它是 hello hello 網域中最後一個剩餘的 DC，或執行在隔離網路中的復原時，必須遵循的樹系修復程序。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-202">If it is hello last remaining DC in hello domain, or a recovery in an isolated network is performed, a forest recovery procedure must be followed.</span></span>

### <a name="multiple-domains-in-one-forest"></a><span data-ttu-id="bf5c0-203">單一樹系中的多個網域</span><span class="sxs-lookup"><span data-stu-id="bf5c0-203">Multiple domains in one forest</span></span>
<span data-ttu-id="bf5c0-204">當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-204">When other DCs of hello same domain can be reached over hello network, hello DC can be restored like any VM.</span></span> <span data-ttu-id="bf5c0-205">不過，若是其他情況，則建議進行樹系復原。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-205">However, in all other cases a forest recovery is recommended.</span></span>

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="bf5c0-206">還原具有特殊網路組態的 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-206">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="bf5c0-207">Azure 備份支援備份虛擬機器的以下特殊網路組態。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-207">Azure Backup supports backup for following special network configurations of virtual machines.</span></span>

* <span data-ttu-id="bf5c0-208">負載平衡器底下的 VM (內部與外部)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-208">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="bf5c0-209">具有多個保留的 IP 的 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-209">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="bf5c0-210">具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="bf5c0-210">VMs with multiple NICs</span></span>

<span data-ttu-id="bf5c0-211">這些組態可在還原組態時授權以下考量項目。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-211">These configurations mandate following considerations while restoring them.</span></span>

> [!TIP]
> <span data-ttu-id="bf5c0-212">請使用 PowerShell 還原流程 toorecreate hello 特殊的網路組態的 Vm 後還原。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-212">Please use PowerShell based restore flow toorecreate hello special network configuration of VMs post restore.</span></span>
>
>

### <a name="restoring-from-hello-ui"></a><span data-ttu-id="bf5c0-213">還原從 hello UI:</span><span class="sxs-lookup"><span data-stu-id="bf5c0-213">Restoring from hello UI:</span></span>
<span data-ttu-id="bf5c0-214">從 UI 還原時，請 **一律選擇新的雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-214">While restoring from UI, **always choose a new cloud service**.</span></span> <span data-ttu-id="bf5c0-215">請注意，由於入口網站只使用強制參數期間還原流程，使用 UI 來還原的 Vm 將會遺失他們擁有 hello 特殊的網路組態。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-215">Please note that since portal only takes mandatory parameters during restore flow, VMs restored using UI will lose hello special network configuration they possess.</span></span> <span data-ttu-id="bf5c0-216">也就是說，還原後的 VM 將會是一般的 VM，不具有負載平衡器組態、多個 NIC 或多個保留的 IP。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-216">In other words, restore VMs will be normal VMs without configuration of load balancer or multi NIC or multiple reserved IP.</span></span>

### <a name="restoring-from-powershell"></a><span data-ttu-id="bf5c0-217">從 PowerShell 還原：</span><span class="sxs-lookup"><span data-stu-id="bf5c0-217">Restoring from PowerShell:</span></span>
<span data-ttu-id="bf5c0-218">PowerShell 的 hello 能力 toojust 從備份還原 hello VM 磁碟，並建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-218">PowerShell has hello ability toojust restore hello VM disks from backup and not create hello virtual machine.</span></span> <span data-ttu-id="bf5c0-219">在還原需要上述特殊網路組態的虛擬機器時，這很有用。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-219">This is helpful when restoring virtual machines which require special network configurations mentioned above.</span></span>

<span data-ttu-id="bf5c0-220">順序 toofully 重新建立 hello 還原磁碟的虛擬機器後，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bf5c0-220">In order toofully recreate hello virtual machine post restoring disks, follow these steps:</span></span>

1. <span data-ttu-id="bf5c0-221">從備份保存庫使用還原 hello 磁碟[Azure 備份的 PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-221">Restore hello disks from backup vault using [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="bf5c0-222">建立 hello VM 組態所需的負載平衡器/多個 NIC 或多個保留 IP 使用 hello PowerShell 指令程式，並用它 toocreate hello VM 所需的組態。</span><span class="sxs-lookup"><span data-stu-id="bf5c0-222">Create hello VM config required for load balancer/multiple NIC/multiple reserved IP using hello PowerShell cmdlets and use it toocreate hello VM of desired configuration.</span></span>

   * <span data-ttu-id="bf5c0-223">使用 [內部負載平衡器 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-223">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="bf5c0-224">建立 VM tooconnect 太[網際網路對向負載平衡器](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-224">Create VM tooconnect too[Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="bf5c0-225">建立具有 [多個 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-225">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="bf5c0-226">建立具有 [多個保留的 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="bf5c0-226">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf5c0-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf5c0-227">Next steps</span></span>
* [<span data-ttu-id="bf5c0-228">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="bf5c0-228">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="bf5c0-229">管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bf5c0-229">Manage virtual machines</span></span>](backup-azure-manage-vms.md)
