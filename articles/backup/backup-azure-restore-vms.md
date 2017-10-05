---
title: "從備份還原虛擬機器 | Microsoft Docs"
description: "了解如何從復原點還原 Azure 虛擬機器"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "還原備份；如何還原；復原點；"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: fc52c909df5e91741ec1fa21fb911487be039fdc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="restore-virtual-machines-in-azure"></a><span data-ttu-id="0d417-104">還原 Azure 中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0d417-104">Restore virtual machines in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d417-105">在 Azure 入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-105">Restore VMs in Azure portal</span></span>](backup-azure-arm-restore-vms.md)
> * [<span data-ttu-id="0d417-106">在傳統入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-106">Restore VMs in Classic portal</span></span>](backup-azure-restore-vms.md)
>
>

<span data-ttu-id="0d417-107">使用下列步驟，利用 Azure 備份保存庫中儲存的備份，將虛擬機器還原到新的 VM。</span><span class="sxs-lookup"><span data-stu-id="0d417-107">Restore a virtual machine to a new VM from the backups stored in an Azure Backup vault with the following steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d417-108">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0d417-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="0d417-109">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="0d417-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0d417-110">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0d417-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="0d417-111">在 **2017 年 10 月 15 日**之後，您就無法使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="0d417-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="0d417-112">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="0d417-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="0d417-113">任何其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0d417-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="0d417-114">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="0d417-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="0d417-115">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="0d417-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="restore-workflow"></a><span data-ttu-id="0d417-116">還原工作流程</span><span class="sxs-lookup"><span data-stu-id="0d417-116">Restore workflow</span></span>
### <a name="step-1-choose-an-item-to-restore"></a><span data-ttu-id="0d417-117">步驟 1：選擇要還原的項目</span><span class="sxs-lookup"><span data-stu-id="0d417-117">Step 1: Choose an item to restore</span></span>
1. <span data-ttu-id="0d417-118">瀏覽至 [ **受保護項目** ] 索引標籤，然後選取您想要還原至新 VM 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0d417-118">Navigate to the **Protected Items** tab and select the virtual machine you want to restore to a new VM.</span></span>

    ![受保護項目](./media/backup-azure-restore-vms/protected-items.png)

    <span data-ttu-id="0d417-120">[受保護項目] 頁面中的 [復原點] 欄會告訴您虛擬機器的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="0d417-120">The **Recovery Point** column in the **Protected Items** page will tell you the number of recovery points for a virtual machine.</span></span> <span data-ttu-id="0d417-121">[ **最新復原點** ] 欄位會告訴您虛擬機器可還原的最近備份時間。</span><span class="sxs-lookup"><span data-stu-id="0d417-121">The **Newest Recovery Point** column tells you the time of the most recent backup from which a virtual machine can be restored.</span></span>
2. <span data-ttu-id="0d417-122">按一下 [還原] 以開啟 [還原項目] 精靈。</span><span class="sxs-lookup"><span data-stu-id="0d417-122">Click **Restore** to open the **Restore an Item** wizard.</span></span>

    ![還原項目](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a><span data-ttu-id="0d417-124">步驟 2：挑選復原點</span><span class="sxs-lookup"><span data-stu-id="0d417-124">Step 2: Pick a recovery point</span></span>
1. <span data-ttu-id="0d417-125">在 [ **選取復原點** ] 畫面中，您可以從最新的復原點或較舊的復原點進行還原。</span><span class="sxs-lookup"><span data-stu-id="0d417-125">In the **select a recovery point** screen, you can restore from the newest recovery point, or from a previous point in time.</span></span> <span data-ttu-id="0d417-126">精靈開啟時預設選取的選項是 [最新復原點] 。</span><span class="sxs-lookup"><span data-stu-id="0d417-126">The default option selected when wizard opens is *Newest Recovery Point*.</span></span>

    ![選取復原點](./media/backup-azure-restore-vms/select-recovery-point.png)
2. <span data-ttu-id="0d417-128">若要挑選較舊的時間，請選擇下拉式清單中的 [選取日期] 選項，然後按一下**行事曆圖示**，在行事曆控制項中選取一個日期。</span><span class="sxs-lookup"><span data-stu-id="0d417-128">To pick an earlier point in time, choose the **Select Date** option in the dropdown and select a date in the calendar control by clicking on the **calendar icon**.</span></span> <span data-ttu-id="0d417-129">在控制項中，所有擁有復原點的日期會以淺灰色陰影填滿，並可供使用者選取。</span><span class="sxs-lookup"><span data-stu-id="0d417-129">In the control, all dates that have recovery points are filled with a light gray shade and are selectable by the user.</span></span>

    ![選取日期](./media/backup-azure-restore-vms/select-date.png)

    <span data-ttu-id="0d417-131">一旦您按一下行事曆控制項中的日期時，該日可用的復原點將會顯示在下方的復原點資料表中。</span><span class="sxs-lookup"><span data-stu-id="0d417-131">Once you click a date in the calendar control, the recovery points available on that date will be shown in recovery points table below.</span></span> <span data-ttu-id="0d417-132">[ **時間** ] 欄位會指出擷取快照集的時間。</span><span class="sxs-lookup"><span data-stu-id="0d417-132">The **Time** column indicates the time at which the snapshot was taken.</span></span> <span data-ttu-id="0d417-133">[ **類型** ] 欄位會顯示復原點的 [一致性](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) 。</span><span class="sxs-lookup"><span data-stu-id="0d417-133">The **Type** column displays the [consistency](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) of the recovery point.</span></span> <span data-ttu-id="0d417-134">資料表標頭會在括號裡顯示該日可用的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="0d417-134">The table header shows the number of recovery points available on that day in parentheses.</span></span>

    ![復原點](./media/backup-azure-restore-vms/recovery-points.png)
3. <span data-ttu-id="0d417-136">從 [復原點]  資料表中選取復原點，然後按一下 [下一步] 箭號以移至下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="0d417-136">Select the recovery point from the **Recovery Points** table and click the Next arrow to go to the next screen.</span></span>

### <a name="step-3-specify-a-destination-location"></a><span data-ttu-id="0d417-137">步驟 3：指定目的地位置</span><span class="sxs-lookup"><span data-stu-id="0d417-137">Step 3: Specify a destination location</span></span>
1. <span data-ttu-id="0d417-138">在 [ **選取還原執行個體** ] 畫面中，指定要將虛擬機器還原至何處的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d417-138">In the **Select restore instance** screen specify details of where to restore the virtual machine.</span></span>

   * <span data-ttu-id="0d417-139">指定虛擬機器名稱：在指定的雲端服務中，虛擬機器名稱應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0d417-139">Specify the virtual machine name: In a given cloud service, the virtual machine name should be unique.</span></span> <span data-ttu-id="0d417-140">我們不支援覆寫現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="0d417-140">We don't support over-writing existing VM.</span></span>
   * <span data-ttu-id="0d417-141">選取 VM 的雲端服務：這是建立 VM 的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="0d417-141">Select a cloud service for the VM: This is mandatory for creating a VM.</span></span> <span data-ttu-id="0d417-142">您可以選擇使用現有的雲端服務，或建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0d417-142">You can choose to either use an existing cloud service or create a new cloud service.</span></span>

        <span data-ttu-id="0d417-143">挑選的雲端服務名稱應具有全域唯一性。</span><span class="sxs-lookup"><span data-stu-id="0d417-143">Whatever cloud service name is picked should be globally unique.</span></span> <span data-ttu-id="0d417-144">一般來說，雲端服務名稱會以 [cloudservice].cloudapp.net 的形式來與公眾對應 URL 產生相關。</span><span class="sxs-lookup"><span data-stu-id="0d417-144">Typically, the cloud service name gets associated with a public-facing URL in the form of [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="0d417-145">如果名稱已在使用中，Azure 將不允許您建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0d417-145">Azure will not allow you to create a new cloud service if the name has already been used.</span></span> <span data-ttu-id="0d417-146">如果您選擇建立新的雲端服務，系統將會為該服務提供與虛擬機器相同的名稱 - 在此情況下，所挑選的 VM 名稱應該具備足以套用至相關雲端服務的唯一性。</span><span class="sxs-lookup"><span data-stu-id="0d417-146">If you choose to create a new cloud service, it will be given the same name as the virtual machine – in which case the VM name picked should be unique enough to be applied to the associated cloud service.</span></span>

        <span data-ttu-id="0d417-147">我們只會顯示與還原執行個體詳細資料中的任何同質群組不關聯的雲端服務和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0d417-147">We only display cloud services and virtual networks that are not associated with any affinity groups in the restore instance details.</span></span> <span data-ttu-id="0d417-148">[深入了解](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="0d417-148">[Learn More](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
2. <span data-ttu-id="0d417-149">選取 VM 的儲存體帳戶：這是建立 VM 的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="0d417-149">Select a storage account for the VM: This is mandatory for creating the VM.</span></span> <span data-ttu-id="0d417-150">您可以選取與 Azure 備份保存庫位於相同區域的現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d417-150">You can select from existing storage accounts in the same region as the Azure Backup vault.</span></span> <span data-ttu-id="0d417-151">我們不支援區域備援或進階儲存體類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d417-151">We don’t support storage accounts that are Zone redundant or of Premium storage type.</span></span>

    <span data-ttu-id="0d417-152">如果沒有支援組態的儲存體帳戶，請在啟動還原作業之前建立一個支援組態的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d417-152">If there are no storage accounts with supported configuration, please create a storage account of supported configuration prior to starting restore operation.</span></span>

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-sa.png)
3. <span data-ttu-id="0d417-154">選取虛擬網路：在建立 VM 時應該已經選取虛擬機器的虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="0d417-154">Select a Virtual Network: The virtual network (VNET) for the virtual machine should be selected at the time of creating the VM.</span></span> <span data-ttu-id="0d417-155">還原 UI 會顯示此訂用帳戶內所有可以使用的 VNET。</span><span class="sxs-lookup"><span data-stu-id="0d417-155">The restore UI shows all the VNETs within this subscription that can be used.</span></span> <span data-ttu-id="0d417-156">為已還原的 VM 選取 VNET 並非必要步驟 – 即使不套用 VNET，您仍然可透過網際網路連接到已還原的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0d417-156">It is not mandatory to select a VNET for the restored VM – you will be able to connect to the restored virtual machine over the internet even if the VNET is not applied.</span></span>

    <span data-ttu-id="0d417-157">如果選取的雲端服務與虛擬網路相關聯，則您無法變更虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0d417-157">If the cloud service selected is associated with a virtual network, then you cannot change the virtual network.</span></span>

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. <span data-ttu-id="0d417-159">選取子網路：如果 VNET 有子網路，預設選取的選項為第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="0d417-159">Select a subnet: In case the VNET has subnets, by default the first subnet will be selected.</span></span> <span data-ttu-id="0d417-160">從下拉式清單選項中選擇您想要的子網路。</span><span class="sxs-lookup"><span data-stu-id="0d417-160">Choose the subnet of your choice from the dropdown options.</span></span> <span data-ttu-id="0d417-161">若需子網路的詳細資訊，請移至[入口網站首頁](https://manage.windowsazure.com/)中的 [網路] 擴充功能，然後移至 [虛擬網路]，並在選取虛擬網路後，向下切入至 [設定] 以查看子網路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d417-161">For subnet details, go to Networks extension in the [portal home page](https://manage.windowsazure.com/), go to **Virtual Networks** and select the virtual network and drill down into Configure to see subnet details.</span></span>

    ![選取子網路](./media/backup-azure-restore-vms/select-subnet.png)
5. <span data-ttu-id="0d417-163">按一下精靈中的 [提交]  圖示以提交詳細資料和建立還原工作。</span><span class="sxs-lookup"><span data-stu-id="0d417-163">Click the **Submit** icon in the wizard to submit the details and create a restore job.</span></span>

## <a name="track-the-restore-operation"></a><span data-ttu-id="0d417-164">追蹤還原作業</span><span class="sxs-lookup"><span data-stu-id="0d417-164">Track the Restore operation</span></span>
<span data-ttu-id="0d417-165">一旦您輸入還原精靈中的所有資訊和提交，Azure 備份將會嘗試建立一項工作以追蹤還原作業。</span><span class="sxs-lookup"><span data-stu-id="0d417-165">Once you have input all the information into the restore wizard and submitted it Azure Backup will try to create a job to track the restore operation.</span></span>

![正在建立還原工作](./media/backup-azure-restore-vms/create-restore-job.png)

<span data-ttu-id="0d417-167">如果成功建立工作，您會看到快顯通知指出工作已建立。</span><span class="sxs-lookup"><span data-stu-id="0d417-167">If the job creation is successful, you will see a toast notification indicating that the job is created.</span></span> <span data-ttu-id="0d417-168">您可以按一下 [檢視工作] 按鈕進入 [工作] 索引標籤，以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d417-168">You can get more details by clicking the **View Job** button that will take you to **Jobs** tab.</span></span>

![已建立還原工作](./media/backup-azure-restore-vms/restore-job-created.png)

<span data-ttu-id="0d417-170">在還原作業完成時，系統會在 **工作**  索引標籤中將其標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="0d417-170">Once the restore operation is finished, it will be marked as completed in **Jobs** tab.</span></span>

![已完成還原工作](./media/backup-azure-restore-vms/restore-job-complete.png)

<span data-ttu-id="0d417-172">還原虛擬機器後，您可能需要重新安裝原始虛擬機器 (VM) 上現有的擴充功能，並為 Azure 入口網站中的虛擬機器 [修改端點](../virtual-machines/windows/classic/setup-endpoints.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d417-172">After restoring the virtual machine you may need to re-install the extensions existing on the original VM and [modify the endpoints](../virtual-machines/windows/classic/setup-endpoints.md) for the virtual machine in the Azure portal.</span></span>

## <a name="post-restore-steps"></a><span data-ttu-id="0d417-173">還原後的步驟</span><span class="sxs-lookup"><span data-stu-id="0d417-173">Post-Restore steps</span></span>
<span data-ttu-id="0d417-174">如果您使用 cloud-init 型 Linux 散發套件 (例如 Ubuntu)，為求安全，還原後將會封鎖密碼。</span><span class="sxs-lookup"><span data-stu-id="0d417-174">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password will be blocked post restore.</span></span> <span data-ttu-id="0d417-175">請在還原的 VM 上使用 VMAccess 擴充功能 [重設密碼](../virtual-machines/linux/classic/reset-access.md)。</span><span class="sxs-lookup"><span data-stu-id="0d417-175">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="0d417-176">建議您在這些散發套件上使用 SSH 金鑰，以避免在還原後重設密碼。</span><span class="sxs-lookup"><span data-stu-id="0d417-176">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span></span>

## <a name="backup-for-restored-vms"></a><span data-ttu-id="0d417-177">備份還原 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-177">Backup for Restored VMs</span></span>
<span data-ttu-id="0d417-178">如果您已將 VM 還原至相同的雲端服務，並使用與原始備份 VM 相同的名稱，備份將會在還原後繼續進行。</span><span class="sxs-lookup"><span data-stu-id="0d417-178">If you have restored VM to same cloud service with the same name as originally backed up VM, backup will continue on the VM post restore.</span></span> <span data-ttu-id="0d417-179">如果您已將 VM 還原至不同的雲端服務，或為還原 VM 指定不同名稱，系統會將該 VM 視為新 VM，因此您需要為還原 VM 設定備份。</span><span class="sxs-lookup"><span data-stu-id="0d417-179">If you have either restored VM to a different cloud service or specified a different name for restored VM, this will be treated as a new VM and you need to setup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="0d417-180">在 Azure 資料中心發生災害時還原 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-180">Restoring a VM during Azure DataCenter Disaster</span></span>
<span data-ttu-id="0d417-181">如果 VM 執行的主要資料中心發生災害，而您已將備份保存庫設定為異地備援，Azure 備份可讓您將備份 VM 還原至配對的資料中心。</span><span class="sxs-lookup"><span data-stu-id="0d417-181">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span></span> <span data-ttu-id="0d417-182">在這種情況下，您需要選取配對之資料中心內的儲存體帳戶，其餘的還原程序則保持不變。</span><span class="sxs-lookup"><span data-stu-id="0d417-182">During such scenarios, you need to select a storage account which is present in paired data center and rest of the restore process remains same.</span></span> <span data-ttu-id="0d417-183">Azure 備份會使用配對之地理區域的計算服務來建立還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0d417-183">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span></span> <span data-ttu-id="0d417-184">深入了解 [Azure 資料中心復原](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span><span class="sxs-lookup"><span data-stu-id="0d417-184">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-domain-controller-vms"></a><span data-ttu-id="0d417-185">還原網域控制站 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-185">Restoring Domain Controller VMs</span></span>
<span data-ttu-id="0d417-186">備份網域控制站 (DC) 虛擬機器是 Azure 備份支援的案例。</span><span class="sxs-lookup"><span data-stu-id="0d417-186">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span></span> <span data-ttu-id="0d417-187">不過，在還原程序進行期間請務必小心。</span><span class="sxs-lookup"><span data-stu-id="0d417-187">However, care must be taken during the restore process.</span></span> <span data-ttu-id="0d417-188">正確的還原程序取決於網域結構。</span><span class="sxs-lookup"><span data-stu-id="0d417-188">The correct restore process depends on the structure of the domain.</span></span> <span data-ttu-id="0d417-189">最簡單的情況是您在單一網域中擁有單一 DC。</span><span class="sxs-lookup"><span data-stu-id="0d417-189">In the simplest case you have a single DC in a single domain.</span></span> <span data-ttu-id="0d417-190">而在生產環境的負載中，較常見的情況是您擁有單一網域且內含多個 DC，其中有些 DC 可能位於內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="0d417-190">More commonly for production loads, you will have a single domain with multiple DCs, perhaps with some DCs on premises.</span></span> <span data-ttu-id="0d417-191">最後，您也可能擁有內含多個網域的樹系。</span><span class="sxs-lookup"><span data-stu-id="0d417-191">Finally, you may have a forest with multiple domains.</span></span>

<span data-ttu-id="0d417-192">從 Active Directory 的觀點來看，Azure VM 就像是位於新式的受支援 Hypervisor 上的其他 VM。</span><span class="sxs-lookup"><span data-stu-id="0d417-192">From an Active Directory perspective the Azure VM is like any other VM on a modern supported hypervisor.</span></span> <span data-ttu-id="0d417-193">與內部部署 Hypervisor 的主要差異是，Azure 沒有提供 VM 主控台。</span><span class="sxs-lookup"><span data-stu-id="0d417-193">The major difference with on-premises hypervisors is that there is no VM console available in Azure.</span></span> <span data-ttu-id="0d417-194">在某些情況下，您必須使用主控台，例如使用裸機復原 (BMR) 類型的備份進行復原。</span><span class="sxs-lookup"><span data-stu-id="0d417-194">A console is required for certain scenarios such as recovering using a Bare Metal Recovery (BMR) type backup.</span></span> <span data-ttu-id="0d417-195">不過，從備份保存庫來還原 VM 可完整取代 BMR。</span><span class="sxs-lookup"><span data-stu-id="0d417-195">However, VM restore from the backup vault is a full replacement for BMR.</span></span> <span data-ttu-id="0d417-196">我們也提供了 Active Directory 還原模式 (DSRM)，因此，您可以進行所有的 Active Directory 復原案例。</span><span class="sxs-lookup"><span data-stu-id="0d417-196">Active Directory Restore Mode (DSRM) is also available, so all Active Directory recovery scenarios are viable.</span></span> <span data-ttu-id="0d417-197">如需更多背景資訊，請參閱[虛擬網域控制站的備份和還原考量](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)以及[規劃 Active Directory 樹系復原](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="0d417-197">For more background information, please check [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) and [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).</span></span>

### <a name="single-dc-in-a-single-domain"></a><span data-ttu-id="0d417-198">單一網域中的單一 DC</span><span class="sxs-lookup"><span data-stu-id="0d417-198">Single DC in a single domain</span></span>
<span data-ttu-id="0d417-199">VM 可以從 Azure 入口網站或使用 PowerShell 還原 (就像任何其他 VM)。</span><span class="sxs-lookup"><span data-stu-id="0d417-199">The VM can be restored (like any other VM) from the Azure portal or using PowerShell.</span></span>

### <a name="multiple-dcs-in-a-single-domain"></a><span data-ttu-id="0d417-200">單一網域中的多個 DC</span><span class="sxs-lookup"><span data-stu-id="0d417-200">Multiple DCs in a single domain</span></span>
<span data-ttu-id="0d417-201">如果您可以透過網路來連線到相同網域內的其他 DC，您就可以像 VM 一樣地還原 DC。</span><span class="sxs-lookup"><span data-stu-id="0d417-201">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="0d417-202">如果該 DC 是網域內剩餘的最後一個 DC，或者您是在隔離的網路中進行復原，則您必須遵循樹系的復原程序。</span><span class="sxs-lookup"><span data-stu-id="0d417-202">If it is the last remaining DC in the domain, or a recovery in an isolated network is performed, a forest recovery procedure must be followed.</span></span>

### <a name="multiple-domains-in-one-forest"></a><span data-ttu-id="0d417-203">單一樹系中的多個網域</span><span class="sxs-lookup"><span data-stu-id="0d417-203">Multiple domains in one forest</span></span>
<span data-ttu-id="0d417-204">如果您可以透過網路來連線到相同網域內的其他 DC，您就可以像 VM 一樣地還原 DC。</span><span class="sxs-lookup"><span data-stu-id="0d417-204">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="0d417-205">不過，若是其他情況，則建議進行樹系復原。</span><span class="sxs-lookup"><span data-stu-id="0d417-205">However, in all other cases a forest recovery is recommended.</span></span>

<!--- WK: this following original supportability statement is incorrect, taking it out.
The challenge arises because DSRM mode is not present in Azure. So to restore such a VM, you cannot use the Azure portal. The only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use the Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about the [USN rollback problem](https://technet.microsoft.com/library/dd363553) and the strategies suggested to fix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="0d417-206">還原具有特殊網路組態的 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-206">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="0d417-207">Azure 備份支援備份虛擬機器的以下特殊網路組態。</span><span class="sxs-lookup"><span data-stu-id="0d417-207">Azure Backup supports backup for following special network configurations of virtual machines.</span></span>

* <span data-ttu-id="0d417-208">負載平衡器底下的 VM (內部與外部)</span><span class="sxs-lookup"><span data-stu-id="0d417-208">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="0d417-209">具有多個保留的 IP 的 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-209">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="0d417-210">具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="0d417-210">VMs with multiple NICs</span></span>

<span data-ttu-id="0d417-211">這些組態可在還原組態時授權以下考量項目。</span><span class="sxs-lookup"><span data-stu-id="0d417-211">These configurations mandate following considerations while restoring them.</span></span>

> [!TIP]
> <span data-ttu-id="0d417-212">請使用 PowerShell 型還原流程重新建立 VM 後續還原的特殊網路組態。</span><span class="sxs-lookup"><span data-stu-id="0d417-212">Please use PowerShell based restore flow to recreate the special network configuration of VMs post restore.</span></span>
>
>

### <a name="restoring-from-the-ui"></a><span data-ttu-id="0d417-213">從 UI 還原：</span><span class="sxs-lookup"><span data-stu-id="0d417-213">Restoring from the UI:</span></span>
<span data-ttu-id="0d417-214">從 UI 還原時，請 **一律選擇新的雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="0d417-214">While restoring from UI, **always choose a new cloud service**.</span></span> <span data-ttu-id="0d417-215">請注意，入口網站在還原流程中只接受強制參數，使用 UI 還原的 VM 將會失去它們擁有的特殊網路組態。</span><span class="sxs-lookup"><span data-stu-id="0d417-215">Please note that since portal only takes mandatory parameters during restore flow, VMs restored using UI will lose the special network configuration they possess.</span></span> <span data-ttu-id="0d417-216">也就是說，還原後的 VM 將會是一般的 VM，不具有負載平衡器組態、多個 NIC 或多個保留的 IP。</span><span class="sxs-lookup"><span data-stu-id="0d417-216">In other words, restore VMs will be normal VMs without configuration of load balancer or multi NIC or multiple reserved IP.</span></span>

### <a name="restoring-from-powershell"></a><span data-ttu-id="0d417-217">從 PowerShell 還原：</span><span class="sxs-lookup"><span data-stu-id="0d417-217">Restoring from PowerShell:</span></span>
<span data-ttu-id="0d417-218">PowerShell 能夠只從備份還原 VM 磁碟，而不建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0d417-218">PowerShell has the ability to just restore the VM disks from backup and not create the virtual machine.</span></span> <span data-ttu-id="0d417-219">在還原需要上述特殊網路組態的虛擬機器時，這很有用。</span><span class="sxs-lookup"><span data-stu-id="0d417-219">This is helpful when restoring virtual machines which require special network configurations mentioned above.</span></span>

<span data-ttu-id="0d417-220">為了完整重新建立虛擬機器後續還原磁碟，請依照以下步驟執行：</span><span class="sxs-lookup"><span data-stu-id="0d417-220">In order to fully recreate the virtual machine post restoring disks, follow these steps:</span></span>

1. <span data-ttu-id="0d417-221">使用 [Azure 備份 PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="0d417-221">Restore the disks from backup vault using [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="0d417-222">使用 PowerShell Cmdlet 建立負載平衡器/多個 NIC/多個保留的 IP 所需的 VM 組態，並使用該組態建立具備想要之組態的 VM。</span><span class="sxs-lookup"><span data-stu-id="0d417-222">Create the VM config required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span></span>

   * <span data-ttu-id="0d417-223">使用 [內部負載平衡器 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="0d417-223">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="0d417-224">建立 VM 來連接至[網際網路面向負載平衡器](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="0d417-224">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="0d417-225">建立具有 [多個 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="0d417-225">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="0d417-226">建立具有 [多個保留的 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="0d417-226">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d417-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d417-227">Next steps</span></span>
* [<span data-ttu-id="0d417-228">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="0d417-228">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="0d417-229">管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0d417-229">Manage virtual machines</span></span>](backup-azure-manage-vms.md)
