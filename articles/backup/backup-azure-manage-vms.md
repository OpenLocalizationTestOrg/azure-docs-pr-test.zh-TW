---
title: "管理 Resource Manager 部署的虛擬機器備份 | Microsoft Docs"
description: "了解如何管理和監視 Resource Manager 部署的虛擬機器備份"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="04d08-103">管理 Azure 虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="04d08-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04d08-104">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="04d08-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="04d08-105">管理傳統 VM 備份</span><span class="sxs-lookup"><span data-stu-id="04d08-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="04d08-106">本文提供如何管理 VM 備份的指引，並說明入口網站儀表板中提供的備份警示資訊。</span><span class="sxs-lookup"><span data-stu-id="04d08-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="04d08-107">本文中的指引適用於 VM 與復原服務保存庫搭配使用。</span><span class="sxs-lookup"><span data-stu-id="04d08-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="04d08-108">本文並未涵蓋建立虛擬機器，也不說明如何保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04d08-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="04d08-109">有關在 Azure 中以復原服務保存庫來保護 Azure Resource Manager 部署的 VM 的初步解說，請參閱 [搶先目睹︰將 VM 備份至復原服務保存庫](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="04d08-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="04d08-110">管理保存庫與受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04d08-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="04d08-111">在 Azure 入口網站中，復原服務保存庫儀表板可讓您存取保存庫的相關資訊，包括︰</span><span class="sxs-lookup"><span data-stu-id="04d08-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="04d08-112">最近的備份快照，也就是最新的還原點 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="04d08-113">備份原則 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-113">the backup policy <br\></span></span>
* <span data-ttu-id="04d08-114">所有備份快照的大小總計 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="04d08-115">使用保存庫保護的虛擬機器數目 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="04d08-116">虛擬機器備份的許多管理工作都是從儀表板中開啟保存庫開始。</span><span class="sxs-lookup"><span data-stu-id="04d08-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="04d08-117">不過，因為保存庫可以用來保護多個項目 (或多個 VM)，若要檢視特定 VM 的詳細資料，請開啟保存庫項目儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="04d08-118">下列程序示範如何開啟「保存庫儀表板」，然後繼續開啟「保存庫項目儀表板」。</span><span class="sxs-lookup"><span data-stu-id="04d08-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="04d08-119">兩個程序都有「提示」，指出如何使用「釘選到儀表板」命令，將保存庫和保存庫項目新增至 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="04d08-120">「釘選到儀表板」是建立保存庫捷徑或項目捷徑的方法。</span><span class="sxs-lookup"><span data-stu-id="04d08-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="04d08-121">您也可以從捷徑執行常用的命令。</span><span class="sxs-lookup"><span data-stu-id="04d08-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="04d08-122">如果您開啟了多個儀表板和刀鋒視窗，請使用視窗底部的深藍色滑桿，來左右滑動 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![使用滑桿以完整檢視](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="04d08-124">在儀表板中開啟復原服務保存庫︰</span><span class="sxs-lookup"><span data-stu-id="04d08-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="04d08-125">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="04d08-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="04d08-126">在 [中樞] 功能表上按一下 [瀏覽]，然後在資源清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="04d08-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="04d08-127">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="04d08-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="04d08-128">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="04d08-128">Click **Recovery Services vault**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="04d08-130">隨即會顯示 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="04d08-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="04d08-131">復原服務保存庫清單</span><span class="sxs-lookup"><span data-stu-id="04d08-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="04d08-132">如果您將保存庫釘選到 Azure 儀表板，則一開啟 Azure 入口網站就可立即存取該保存庫。</span><span class="sxs-lookup"><span data-stu-id="04d08-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="04d08-133">若要將保存庫釘選到儀表板，請在保存庫清單中以滑鼠右鍵按一下保存庫，然後選取 [釘選到儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="04d08-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="04d08-134">從保存庫清單中，選取保存庫以開啟其儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="04d08-135">選取保存庫時，保存庫儀表板和 [設定] 刀鋒視窗將會開啟。</span><span class="sxs-lookup"><span data-stu-id="04d08-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="04d08-136">下圖中反白顯示 **Contoso-vault** 儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![開啟保存庫儀表板和設定刀鋒視窗](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="04d08-138">開啟保存庫項目儀表板</span><span class="sxs-lookup"><span data-stu-id="04d08-138">Open a vault item dashboard</span></span>
<span data-ttu-id="04d08-139">上一個程序中，您開啟保存庫儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="04d08-140">若要開啟保存庫項目儀表板︰</span><span class="sxs-lookup"><span data-stu-id="04d08-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="04d08-141">在保存庫儀表板的 [備份項目] 圖格上，按一下 [Azure 虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="04d08-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![開啟備份項目備份圖格](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="04d08-143">[備份項目]  刀鋒視窗會列出每個項目的最後一個備份作業。</span><span class="sxs-lookup"><span data-stu-id="04d08-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="04d08-144">在此範例中，有一個受此保存庫保護的虛擬機器：demovm markgal。</span><span class="sxs-lookup"><span data-stu-id="04d08-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="04d08-146">為了方便存取，您可以將保存庫項目釘選到 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="04d08-147">若要釘選保存庫項目，請以滑鼠右鍵按一下項目，然後選取 [釘選到儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="04d08-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="04d08-148">在 [備份項目]  刀鋒視窗中，按一下項目以開啟保存庫項目儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="04d08-150">保存庫項目儀表板及其 [設定]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d08-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![搭配設定刀鋒視窗的備份項目儀表板](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="04d08-152">從保存庫項目儀表板，您可以完成許多重要的管理工作，例如︰</span><span class="sxs-lookup"><span data-stu-id="04d08-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="04d08-153">變更原則或建立新的備份原則 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="04d08-154">檢視還原點並查看其一致性狀態 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="04d08-155">虛擬機器的隨選備份 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="04d08-156">停止保護虛擬機器 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="04d08-157">繼續保護虛擬機器 <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="04d08-158">刪除備份資料 (或復原點) <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="04d08-159">[還原備份磁碟](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="04d08-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="04d08-160">在以下的程序中，起始點是保存庫項目儀表板。</span><span class="sxs-lookup"><span data-stu-id="04d08-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="04d08-161">管理備份原則</span><span class="sxs-lookup"><span data-stu-id="04d08-161">Manage backup policies</span></span>
1. <span data-ttu-id="04d08-162">在[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)中，按一下 [所有設定] 以開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="04d08-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="04d08-164">在 [設定] 刀鋒視窗上，按一下 [備份原則] 以開啟該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="04d08-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="04d08-165">刀鋒視窗上會顯示備份頻率和保留範圍詳細資料。</span><span class="sxs-lookup"><span data-stu-id="04d08-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="04d08-167">從 [選擇備份原則]  功能表︰</span><span class="sxs-lookup"><span data-stu-id="04d08-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="04d08-168">若要變更原則，請選取不同的原則，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="04d08-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="04d08-169">新原則時會立即套用至保存庫。</span><span class="sxs-lookup"><span data-stu-id="04d08-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="04d08-170"><br\></span><span class="sxs-lookup"><span data-stu-id="04d08-170"><br\></span></span>
   * <span data-ttu-id="04d08-171">若要建立原則，請選取 [建立新項目] 。</span><span class="sxs-lookup"><span data-stu-id="04d08-171">To create a policy, select **Create New**.</span></span>

     ![虛擬機器備份](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="04d08-173">如需建立備份原則的指示，請參閱 [定義備份原則](backup-azure-manage-vms.md#defining-a-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="04d08-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="04d08-174">在管理備份原則時，請務必遵循[最佳做法](backup-azure-vms-introduction.md#best-practices)以便獲得最佳備份效能</span><span class="sxs-lookup"><span data-stu-id="04d08-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="04d08-175">虛擬機器的隨選備份</span><span class="sxs-lookup"><span data-stu-id="04d08-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="04d08-176">設定保護後，您可以執行虛擬機器的隨選備份。</span><span class="sxs-lookup"><span data-stu-id="04d08-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="04d08-177">如果初始備份已暫止，則隨選備份會在復原服務保存庫中建立虛擬機器的完整複本。</span><span class="sxs-lookup"><span data-stu-id="04d08-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="04d08-178">如果已完成初始備份，隨選備份只會將前一個備份快照的變更傳送到復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="04d08-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="04d08-179">亦即，後續備份一律是增量備份。</span><span class="sxs-lookup"><span data-stu-id="04d08-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="04d08-180">隨選備份的保留範圍是原則中為「每日」備份點所指定的保留值。</span><span class="sxs-lookup"><span data-stu-id="04d08-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="04d08-181">如果未選取任何「每日」備份點，則會使用每週備份點。</span><span class="sxs-lookup"><span data-stu-id="04d08-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="04d08-182">若要觸發虛擬機器的隨選備份：</span><span class="sxs-lookup"><span data-stu-id="04d08-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="04d08-183">在[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)上，按一下 [立即備份]。</span><span class="sxs-lookup"><span data-stu-id="04d08-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="04d08-185">入口網站會確認您想要啟動隨選備份作業。</span><span class="sxs-lookup"><span data-stu-id="04d08-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="04d08-186">按一下 [是]  啟動備份作業。</span><span class="sxs-lookup"><span data-stu-id="04d08-186">Click **Yes** to start the backup job.</span></span>

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="04d08-188">備份作業會建立復原點。</span><span class="sxs-lookup"><span data-stu-id="04d08-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="04d08-189">復原點的保留範圍與在虛擬機器相關的原則中指定的保留範圍相同。</span><span class="sxs-lookup"><span data-stu-id="04d08-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="04d08-190">若要追蹤作業的進度，請在保存庫儀表板中按一下 [備份作業]  圖格。</span><span class="sxs-lookup"><span data-stu-id="04d08-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="04d08-191">停止保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04d08-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="04d08-192">如果您選擇停止保護虛擬機器，系統會詢問您是否要保留復原點。</span><span class="sxs-lookup"><span data-stu-id="04d08-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="04d08-193">有兩種方式可停止保護虛擬機器︰</span><span class="sxs-lookup"><span data-stu-id="04d08-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="04d08-194">停止所有未來的備份作業並刪除所有復原點，或</span><span class="sxs-lookup"><span data-stu-id="04d08-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="04d08-195">停止所有未來的備份作業但保留復原點 </span><span class="sxs-lookup"><span data-stu-id="04d08-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="04d08-196">在儲存體中保留復原點需要付出相關的成本。</span><span class="sxs-lookup"><span data-stu-id="04d08-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="04d08-197">不過，保留復原點的好處是以後可以在需要時還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04d08-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="04d08-198">如需復原點保留成本的相關資訊，請參閱[價格詳細資料](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="04d08-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="04d08-199">如果您選擇刪除所有復原點，則無法還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04d08-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="04d08-200">若要停止保護虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="04d08-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="04d08-201">在[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)上，按一下 [停止備份]。</span><span class="sxs-lookup"><span data-stu-id="04d08-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![停止備份按鈕](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="04d08-203">[停止備份] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d08-203">The Stop Backup blade opens.</span></span>

    ![停止備份刀鋒視窗](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="04d08-205">在 [停止備份]  刀鋒視窗上，選擇要保留還是刪除備份資料。</span><span class="sxs-lookup"><span data-stu-id="04d08-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="04d08-206">資訊方塊會針對您的選擇提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="04d08-206">The information box provides details about your choice.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="04d08-208">如果您選擇要保留備份資料，請跳至步驟 4。</span><span class="sxs-lookup"><span data-stu-id="04d08-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="04d08-209">如果您選擇要刪除備份資料，請確認您想要停止備份作業，並刪除復原點 - 輸入項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="04d08-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="04d08-211">如果您不確定項目名稱，請以滑鼠暫留在驚嘆號來檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="04d08-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="04d08-212">項目的名稱也會出現在刀鋒視窗頂端的 [停止備份]  下。</span><span class="sxs-lookup"><span data-stu-id="04d08-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="04d08-213">選擇性地提供 [原因] 或 [註解]。</span><span class="sxs-lookup"><span data-stu-id="04d08-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="04d08-214">若要停止目前的項目的備份作業，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="04d08-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="04d08-215">通知訊息可讓您知道備份作業已停止。</span><span class="sxs-lookup"><span data-stu-id="04d08-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![確認停止保護](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="04d08-217">繼續保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04d08-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="04d08-218">如果在停止保護虛擬機器時已選擇 [保留備份資料]  選項，則可以繼續保護。</span><span class="sxs-lookup"><span data-stu-id="04d08-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="04d08-219">如果已選擇 [刪除備份資料]  選項，則無法繼續保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04d08-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="04d08-220">繼續保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04d08-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="04d08-221">在[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)上，按一下 [繼續備份]。</span><span class="sxs-lookup"><span data-stu-id="04d08-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![繼續保護](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="04d08-223">[備份原則] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d08-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04d08-224">重新保護虛擬機器時，您可以選擇與最初用於保護虛擬機器不同的原則。</span><span class="sxs-lookup"><span data-stu-id="04d08-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="04d08-225">請依照[管理備份原則](backup-azure-manage-vms.md#manage-backup-policies)中的步驟，指派虛擬機器的原則。</span><span class="sxs-lookup"><span data-stu-id="04d08-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="04d08-226">備份原則套用至虛擬機器後，您會看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="04d08-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![已成功保護 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="04d08-228">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="04d08-228">Delete Backup data</span></span>
<span data-ttu-id="04d08-229">您可以在 **停止備份** 作業期間，或在備份作業完成之後的任何時間，刪除與虛擬機器相關聯的備份資料。</span><span class="sxs-lookup"><span data-stu-id="04d08-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="04d08-230">先等候幾天或幾週再刪除復原點甚至可能會讓您受益。</span><span class="sxs-lookup"><span data-stu-id="04d08-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="04d08-231">不同於還原復原點，當您刪除備份資料時，您無法選擇刪除特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="04d08-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="04d08-232">如果您選擇刪除備份資料，則會刪除與項目相關聯的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="04d08-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="04d08-233">下列程序假設虛擬機器的備份作業已停止或停用。</span><span class="sxs-lookup"><span data-stu-id="04d08-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="04d08-234">一旦備份作業停用，保存庫項目儀表板便會提供 [繼續備份] 和 [刪除備份] 選項。</span><span class="sxs-lookup"><span data-stu-id="04d08-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![繼續和刪除按鈕](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="04d08-236">若要在「備份已停用」 的情況下刪除虛擬機器上的備份資料：</span><span class="sxs-lookup"><span data-stu-id="04d08-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="04d08-237">在[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)上，按一下 [刪除備份]。</span><span class="sxs-lookup"><span data-stu-id="04d08-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="04d08-239">[刪除備份資料]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="04d08-239">The **Delete Backup Data** blade opens.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="04d08-241">輸入項目的名稱，以確認您想要刪除復原點。</span><span class="sxs-lookup"><span data-stu-id="04d08-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="04d08-243">如果您不確定項目名稱，請以滑鼠暫留在驚嘆號來檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="04d08-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="04d08-244">項目的名稱也出現刀鋒視窗頂端的 [刪除備份資料]  下。</span><span class="sxs-lookup"><span data-stu-id="04d08-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="04d08-245">選擇性地提供 [原因] 或 [註解]。</span><span class="sxs-lookup"><span data-stu-id="04d08-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="04d08-246">若要刪除的備份資料的目前項目，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="04d08-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="04d08-247">通知訊息可讓您知道備份資料已刪除。</span><span class="sxs-lookup"><span data-stu-id="04d08-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d08-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04d08-248">Next steps</span></span>
<span data-ttu-id="04d08-249">如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="04d08-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="04d08-250">如需保護虛擬機器的詳細資訊，請參閱 [搶先目睹︰將 VM 備份至復原服務保存庫](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="04d08-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="04d08-251">如需監視事件的相關資訊，請參閱 [監視 Azure 虛擬機器備份的警示](backup-azure-monitor-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="04d08-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
