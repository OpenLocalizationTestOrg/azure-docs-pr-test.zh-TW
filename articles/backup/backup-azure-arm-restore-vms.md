---
title: "Azure 備份：使用 Azure 入口網站還原虛擬機器 | Microsoft Docs"
description: "使用 Azure 入口網站從復原點還原 Azure 虛擬機器"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "還原備份；如何還原；復原點；"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1fe2b94d462a30f09cb23ab905542aa121ba46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-portal-to-restore-virtual-machines"></a><span data-ttu-id="43597-104">使用 Azure 入口網站來還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="43597-104">Use Azure portal to restore virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43597-105">在傳統入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="43597-105">Restore VMs in Classic portal</span></span>](backup-azure-restore-vms.md)
> * [<span data-ttu-id="43597-106">在 Azure 入口網站中還原 VM</span><span class="sxs-lookup"><span data-stu-id="43597-106">Restore VMs in Azure portal</span></span>](backup-azure-arm-restore-vms.md)
>
>

<span data-ttu-id="43597-107">於定義的間隔進行資料快照，來保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="43597-107">Protect your data by taking snapshots of your data at defined intervals.</span></span> <span data-ttu-id="43597-108">這些快照稱為復原點，而且儲存在復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="43597-108">These snapshots are known as recovery points, and they are stored in recovery services vaults.</span></span> <span data-ttu-id="43597-109">如果或需要修復或重新建立 VM，您可以從任何已儲存的復原點還原 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-109">If or when it is necessary to repair or rebuild a VM, you can restore the VM from any of the saved recovery points.</span></span> <span data-ttu-id="43597-110">當您還原復原點時，您可以建立新的 VM 來代表已備份之 VM 的某個時間點，或還原磁碟並使用它隨附的範本，以自訂已還原的 VM 或執行個別的檔案復原。</span><span class="sxs-lookup"><span data-stu-id="43597-110">When you restore a recovery point, you can create a new VM which is a point-in-time representation of your backed-up VM, or restore disks and use the template that comes along with it to customize the restored VM or do an individual file recovery.</span></span> <span data-ttu-id="43597-111">本文說明如何將 VM 還原至新的 VM，或還原所有已備份的磁碟。</span><span class="sxs-lookup"><span data-stu-id="43597-111">This article explains how to restore a VM to a new VM or restore all backed-up disks.</span></span> <span data-ttu-id="43597-112">關於個別檔案復原，請參閱[從 Azure VM 備份復原檔案](backup-azure-restore-files-from-vm.md)</span><span class="sxs-lookup"><span data-stu-id="43597-112">For individual file recovery, refer to [Recover files from Azure VM backup](backup-azure-restore-files-from-vm.md)</span></span>

![從 VM 備份還原的 3 種方法](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> <span data-ttu-id="43597-114">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="43597-114">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="43597-115">本文提供的資訊和程序可供還原使用 Resource Manager 模型部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-115">This article provides the information and procedures for restoring VMs deployed using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="43597-116">從 VM 備份還原一個 VM 或所有磁碟需要兩個步驟︰</span><span class="sxs-lookup"><span data-stu-id="43597-116">Restoring a VM or all disks from VM backup involves two steps:</span></span>

1. <span data-ttu-id="43597-117">選取要還原的還原點</span><span class="sxs-lookup"><span data-stu-id="43597-117">Select a restore point for restore</span></span>
2. <span data-ttu-id="43597-118">選取還原類型 - 建立新的 VM，或還原磁碟並指定必要的參數。</span><span class="sxs-lookup"><span data-stu-id="43597-118">Selecting the restore type - create a new VM or restore disks and specify required parameters.</span></span> 

## <a name="select-restore-point-for-restore"></a><span data-ttu-id="43597-119">選取要還原的還原點</span><span class="sxs-lookup"><span data-stu-id="43597-119">Select restore point for restore</span></span>
1. <span data-ttu-id="43597-120">登入 [Azure 入口網站](http://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="43597-120">Sign in to the [Azure portal](http://portal.azure.com/)</span></span>
2. <span data-ttu-id="43597-121">在 Azure 功能表上按一下 [瀏覽]，然後在服務清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="43597-121">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span></span> <span data-ttu-id="43597-122">服務清單會調整成您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="43597-122">The list of services adjusts to what you type.</span></span> <span data-ttu-id="43597-123">當您看到 [復原服務保存庫] 時，請選取它。</span><span class="sxs-lookup"><span data-stu-id="43597-123">When you see **Recovery Services vaults**, select it.</span></span>

    ![開啟復原服務保存庫](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    <span data-ttu-id="43597-125">便會顯示訂用帳戶中保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="43597-125">The list of vaults in the subscription is displayed.</span></span>

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. <span data-ttu-id="43597-127">從這份清單，選取與您要還原的 VM 相關聯的保存庫。</span><span class="sxs-lookup"><span data-stu-id="43597-127">From the list, select the vault associated with the VM you want to restore.</span></span> <span data-ttu-id="43597-128">當您按一下保存庫時，其儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="43597-128">When you click the vault, its dashboard opens.</span></span>

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. <span data-ttu-id="43597-130">您現在已在保存庫儀表板中。</span><span class="sxs-lookup"><span data-stu-id="43597-130">Now that you're in the vault dashboard.</span></span> <span data-ttu-id="43597-131">在 [備份項目] 圖格上，按一下 [Azure 虛擬機器] 以顯示與保存庫相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-131">On the **Backup Items** tile, click **Azure Virtual Machines** to display the VMs associated with the vault.</span></span>

    ![保存庫儀表板](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    <span data-ttu-id="43597-133">[備份項目]  刀鋒視窗會開啟並顯示 Azure 虛擬機器的清單。</span><span class="sxs-lookup"><span data-stu-id="43597-133">The **Backup Items** blade opens and displays the list of Azure virtual machines.</span></span>

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. <span data-ttu-id="43597-135">從清單中選取 VM，以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="43597-135">From the list, select a VM to open the dashboard.</span></span> <span data-ttu-id="43597-136">VM 儀表板會開啟至包含 [還原點] 圖格的 [監視] 區域。</span><span class="sxs-lookup"><span data-stu-id="43597-136">The VM dashboard opens to the Monitoring area, which contains the Restore points tile.</span></span>

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. <span data-ttu-id="43597-138">在 VM 的儀表板功能表上，按一下 [還原] </span><span class="sxs-lookup"><span data-stu-id="43597-138">On the VM dashboard menu, click **Restore**</span></span>

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    <span data-ttu-id="43597-140">[還原] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="43597-140">The Restore blade opens.</span></span>

    ![還原刀鋒視窗](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. <span data-ttu-id="43597-142">在 [還原] 刀鋒視窗上，按一下 [還原點] 以開啟 [選取還原點] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43597-142">On the **Restore** blade, click **Restore point** to open the **Select Restore point** blade.</span></span>

    ![還原刀鋒視窗](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    <span data-ttu-id="43597-144">根據預設，對話方塊會顯示過去 30 天內的所有還原點。</span><span class="sxs-lookup"><span data-stu-id="43597-144">By default, the dialog displays all restore points from the last 30 days.</span></span> <span data-ttu-id="43597-145">使用 [篩選]  變更所顯示還原點的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="43597-145">Use the **Filter** to alter the time range of the restore points displayed.</span></span> <span data-ttu-id="43597-146">根據預設，系統會顯示所有一致性的還原點。</span><span class="sxs-lookup"><span data-stu-id="43597-146">By default, restore points of all consistency are displayed.</span></span> <span data-ttu-id="43597-147">修改 [所有還原點]  篩選器，可選取特定還原點的一致性。</span><span class="sxs-lookup"><span data-stu-id="43597-147">Modify **All Restore points** filter to select a specific consistency of restore points.</span></span> <span data-ttu-id="43597-148">如需每種還原點類型的詳細資訊，請參閱 [資料一致性](backup-azure-vms-introduction.md#data-consistency)的說明。</span><span class="sxs-lookup"><span data-stu-id="43597-148">For more information about each type of restoration point, see the explanation of [Data consistency](backup-azure-vms-introduction.md#data-consistency).</span></span>  

   * <span data-ttu-id="43597-149"> 選擇以下清單︰</span><span class="sxs-lookup"><span data-stu-id="43597-149">**Restore point consistency** from this list choose:</span></span>
     * <span data-ttu-id="43597-150">當機時保持一致還原點，</span><span class="sxs-lookup"><span data-stu-id="43597-150">Crash consistent restore points,</span></span>
     * <span data-ttu-id="43597-151">應用程式保持一致還原點，</span><span class="sxs-lookup"><span data-stu-id="43597-151">Application consistent restore points,</span></span>
     * <span data-ttu-id="43597-152">系統檔案保持一致還原點，</span><span class="sxs-lookup"><span data-stu-id="43597-152">File system consistent restore points</span></span>
     * <span data-ttu-id="43597-153">所有還原點。</span><span class="sxs-lookup"><span data-stu-id="43597-153">All restore points.</span></span>  
8. <span data-ttu-id="43597-154">選擇還原點，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="43597-154">Choose a Restore point and click **OK**.</span></span>

    ![選擇還原點](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    <span data-ttu-id="43597-156">[還原]  刀鋒視窗會顯示已設定還原點。</span><span class="sxs-lookup"><span data-stu-id="43597-156">The **Restore** blade shows the Restore point is set.</span></span>

    ![已設定還原點](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. <span data-ttu-id="43597-158">在 [還原] 刀鋒視窗中，[還原組態] 會在設定還原點後自動開啟。</span><span class="sxs-lookup"><span data-stu-id="43597-158">On the **Restore** blade, **Restore configuration** opens automatically after restore point is set.</span></span>

## <a name="choosing-a-vm-restore-configuration"></a><span data-ttu-id="43597-159">選擇 VM 還原組態</span><span class="sxs-lookup"><span data-stu-id="43597-159">Choosing a VM restore configuration</span></span>
<span data-ttu-id="43597-160">既然您已選取還原點，請選擇還原 VM 的組態。</span><span class="sxs-lookup"><span data-stu-id="43597-160">Now that you have selected the restore point, choose a configuration for your restore VM.</span></span> <span data-ttu-id="43597-161">設定還原 VM 的選項包括使用︰Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="43597-161">Your choices for configuring the restored VM are to use: Azure portal or PowerShell.</span></span>

1. <span data-ttu-id="43597-162">如果您尚未到達該位置，請移至 [還原]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43597-162">If you are not already there, go to the **Restore** blade.</span></span> <span data-ttu-id="43597-163">確定[已選取還原點](#select-restore-point-for-restore)，然後按一下 [還原組態] 以開啟 [復原組態] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43597-163">Ensure a [Restore point has been selected](#select-restore-point-for-restore), and click **Restore configuration** to open the **Recovery configuration** blade.</span></span>

    ![已設定復原組態精靈](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. <span data-ttu-id="43597-165">在 [還原組態] 刀鋒視窗上有兩個選擇︰</span><span class="sxs-lookup"><span data-stu-id="43597-165">On the **Restore configuration** blade, you have two choices:</span></span>
   * <span data-ttu-id="43597-166">還原完整虛擬機器</span><span class="sxs-lookup"><span data-stu-id="43597-166">Restore full virtual machine</span></span>
   * <span data-ttu-id="43597-167">還原備份的磁碟</span><span class="sxs-lookup"><span data-stu-id="43597-167">Restore backed up disks</span></span>

<span data-ttu-id="43597-168">入口網站提供還原 VM 專用的「快速建立」選項。</span><span class="sxs-lookup"><span data-stu-id="43597-168">Portal provides a Quick Create option for restored VM.</span></span> <span data-ttu-id="43597-169">如果您想要自訂 VM 組態，或在建立新的 VM 選擇時所建立的資源名稱，請使用 PowerShell 或入口網站來還原備份的磁碟，並使用 PowerShell 命令，將它們連結至所選擇的 VM 組態，或使用還原磁碟隨附的範本來自訂還原的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-169">If you want to customize the VM configuration or names of the resources created as part of create a new VM choice, use PowerShell or portal to restore backed up disks and use PowerShell commands to attach them to choice of VM configuration or use template that comes with restore disks to customize the restored VM.</span></span> <span data-ttu-id="43597-170">有關如何還原具有多個 NIC 或在負載平衡器管理之下的 VM 的詳細資訊，請參閱[還原具有特殊網路組態的 VM](#restoring-vms-with-special-network-configurations)。</span><span class="sxs-lookup"><span data-stu-id="43597-170">See [Restoring a VM with special network configurations](#restoring-vms-with-special-network-configurations) for details on how to restore VM which has multiple NICs or under load balancer.</span></span> <span data-ttu-id="43597-171">如果您的 Windows VM 使用[中樞授權](../virtual-machines/windows/hybrid-use-benefit-licensing.md)，您必須還原磁碟，並且使用以下所述的 PowerShell/範本以建立 VM，以及確定在建立 VM 以獲得已還原 VM 上的中樞優點時，將 LicenseType 指定為 "Windows_Server"。</span><span class="sxs-lookup"><span data-stu-id="43597-171">If your Windows VM uses [HUB licensing](../virtual-machines/windows/hybrid-use-benefit-licensing.md), you need to restore disks and use PowerShell/Template as specified below to create the VM and make sure that you specify LicenseType as "Windows_Server" while creating VM to avail HUB benefits on restored VM.</span></span> 
 
## <a name="create-a-new-vm-from-restore-point"></a><span data-ttu-id="43597-172">從還原點建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-172">Create a new VM from restore point</span></span>
<span data-ttu-id="43597-173">如果您還沒有[選取還原點](#restoring-vms-with-special-network-configurations)，請先選取，再繼續從還原點建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-173">If you are not already there, [select a restore point](#restoring-vms-with-special-network-configurations) before proceeding to creating a new VM from restore point.</span></span> <span data-ttu-id="43597-174">選取還原點之後，在 [還原組態] 刀鋒視窗上，輸入或選取下列各欄位的值︰</span><span class="sxs-lookup"><span data-stu-id="43597-174">Once restore point is selected, on the **Restore configuration** blade, enter or select values for each of the following fields:</span></span>

* <span data-ttu-id="43597-175">**還原類型** - 建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43597-175">**Restore Type** - Create virtual machine.</span></span>
* <span data-ttu-id="43597-176">**虛擬機器名稱** - 提供 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="43597-176">**Virtual machine name** - Provide a name for the VM.</span></span> <span data-ttu-id="43597-177">對資源群組 (適用於資源管理員部署的 VM) 或雲端服務 (適用於傳統型 VM) 來說，名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="43597-177">The name must be unique to the resource group (for a Resource Manager-deployed VM) or cloud service (for a Classic VM).</span></span> <span data-ttu-id="43597-178">如果虛擬機器已經存在於訂用帳戶中，則您無法取代虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43597-178">You cannot replace the virtual machine if it already exists in the subscription.</span></span>
* <span data-ttu-id="43597-179">**資源群組** - 使用現有資源群組，或建立新的群組。</span><span class="sxs-lookup"><span data-stu-id="43597-179">**Resource group** - Use an existing resource group, or create a new one.</span></span> <span data-ttu-id="43597-180">如果您要還原傳統 VM，請使用此欄位來指定新雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="43597-180">If you are restoring a Classic VM, use this field to specify the name of a new cloud service.</span></span> <span data-ttu-id="43597-181">如果您是建立新的資源群組/雲端服務，此名稱必須是全域唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="43597-181">If you are creating a new resource group/cloud service, the name must be globally unique.</span></span> <span data-ttu-id="43597-182">一般來說，雲端服務名稱會與公眾對應 URL 相關聯 - 例如：[cloudservice].cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="43597-182">Typically, the cloud service name is associated with a public-facing URL - for example: [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="43597-183">如果您嘗試使用已經使用的雲端資源群組/雲端服務名稱，Azure 會指派給資源群組/雲端服務與 VM 相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="43597-183">If you attempt to use a name for the cloud resource group/cloud service that has already been used, Azure assigns the resource group/cloud service the same name as the VM.</span></span> <span data-ttu-id="43597-184">Azure 會顯示未與任何同質群組相關聯的資源群組/雲端服務和 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-184">Azure displays resource groups/cloud services and VMs not associated with any affinity groups.</span></span> <span data-ttu-id="43597-185">如需詳細資訊，請參閱 [如何從同質群組移轉至區域虛擬網路 (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="43597-185">For more information, see [How to migrate from Affinity Groups to a Regional Virtual Network (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
* <span data-ttu-id="43597-186">**虛擬網路** -建立 VM 時，請選取虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="43597-186">**Virtual Network** - Select the virtual network (VNET) when creating the VM.</span></span> <span data-ttu-id="43597-187">此欄位提供與訂用帳戶相關聯的所有 VNET。</span><span class="sxs-lookup"><span data-stu-id="43597-187">The field provides all VNETs associated with the subscription.</span></span> <span data-ttu-id="43597-188">顯示的 VM 資源群組會以括號括住。</span><span class="sxs-lookup"><span data-stu-id="43597-188">Resource group of the VM is displayed in parentheses.</span></span>
* <span data-ttu-id="43597-189">**子網路** - 如果 VNET 有子網路，預設會選取第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="43597-189">**Subnet** - If the VNET has subnets, the first subnet is selected by default.</span></span> <span data-ttu-id="43597-190">如果有其他子網路，請選取所需的子網路。</span><span class="sxs-lookup"><span data-stu-id="43597-190">If there are additional subnets, select the desired subnet.</span></span>
* <span data-ttu-id="43597-191">**儲存體帳戶** - 此功能表會列出與復原服務保存庫位於相同位置的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-191">**Storage account** - This menu lists the storage accounts in the same location as the Recovery Services vault.</span></span> <span data-ttu-id="43597-192">不支援區域備援的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-192">Storage accounts that are Zone redundant are not supported.</span></span> <span data-ttu-id="43597-193">如果沒有與復原服務保存庫相同位置的儲存體帳戶，您必須在開始還原作業之前，建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-193">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span></span> <span data-ttu-id="43597-194">儲存體帳戶的複寫類型會使用括號註明。</span><span class="sxs-lookup"><span data-stu-id="43597-194">The storage account's replication type is mentioned in parentheses.</span></span>

![已設定還原組態精靈](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. <span data-ttu-id="43597-196">如果您正在還原資源管理員部署的 VM，您必須識別虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="43597-196">If you are restoring a Resource Manager-deployed VM, you must identify a virtual network (VNET).</span></span> <span data-ttu-id="43597-197">針對傳統型 VM，虛擬網路 (VNET) 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="43597-197">A virtual network (VNET) is optional for a Classic VM.</span></span>
> 2. <span data-ttu-id="43597-198">如果您要還原具有受控磁碟的 VM，請確定所選取的儲存體帳戶未在其存留期內啟用儲存體服務加密 (SSE)。</span><span class="sxs-lookup"><span data-stu-id="43597-198">If you are restoring VMs with managed disks, make sure that storage account selected is not enabled for Storage Service Encryption(SSE) in its lifetime.</span></span>
> 3. <span data-ttu-id="43597-199">根據所選取之儲存體帳戶的儲存體類型 (進階或標準)，所有的還原磁碟將會是進階或標準磁碟的任一種。</span><span class="sxs-lookup"><span data-stu-id="43597-199">Based on the storage type of storage account selected(premium or standard), all disks restored will be either premium or standard disks.</span></span> <span data-ttu-id="43597-200">我們目前不支援在還原時使用混合的磁碟模式。</span><span class="sxs-lookup"><span data-stu-id="43597-200">We currently don't support mixed mode of disks when restoring.</span></span>  
>
>

<span data-ttu-id="43597-201">在 [還原組態] 刀鋒視窗上，按一下 [確定] 完成還原組態。</span><span class="sxs-lookup"><span data-stu-id="43597-201">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span></span> <span data-ttu-id="43597-202">在 [還原] 刀鋒視窗上，按一下 [還原] 以觸發還原作業。</span><span class="sxs-lookup"><span data-stu-id="43597-202">On the **Restore** blade, click **Restore** to trigger the restore operation.</span></span>

## <a name="restore-backed-up-disks"></a><span data-ttu-id="43597-203">還原備份的磁碟</span><span class="sxs-lookup"><span data-stu-id="43597-203">Restore backed up disks</span></span>
<span data-ttu-id="43597-204">如果您想要自訂您從備份的磁碟 (而非還原組態刀鋒視窗中顯示的磁碟) 建立的虛擬機器，請選取 [還原磁碟] 做為 [還原類型] 值。</span><span class="sxs-lookup"><span data-stu-id="43597-204">If you would like to customize the virtual machine you would like to create from backed up disks than what is present in restore configuration blade, select **Restore disks** as value for **Restore Type**.</span></span> <span data-ttu-id="43597-205">此選擇需要儲存體帳戶，以存放從備份複製的磁碟。</span><span class="sxs-lookup"><span data-stu-id="43597-205">This choice asks for a storage account where disks from backups are copied to.</span></span> <span data-ttu-id="43597-206">選擇儲存體帳戶時，請選取與「復原服務」保存庫共用相同位置的帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-206">When choosing a storage account, select an account that shares the same location as the Recovery Services vault.</span></span> <span data-ttu-id="43597-207">不支援區域備援的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-207">Storage accounts that are Zone redundant are not supported.</span></span> <span data-ttu-id="43597-208">如果沒有與復原服務保存庫相同位置的儲存體帳戶，您必須在開始還原作業之前，建立一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43597-208">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span></span> <span data-ttu-id="43597-209">儲存體帳戶的複寫類型會使用括號註明。</span><span class="sxs-lookup"><span data-stu-id="43597-209">The storage account's replication type is mentioned in parentheses.</span></span>

<span data-ttu-id="43597-210">還原作業完成之後，您可以︰</span><span class="sxs-lookup"><span data-stu-id="43597-210">After restore operation is completed, you can:</span></span>
* [<span data-ttu-id="43597-211">使用範本自訂還原的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-211">Use template to customize the restored VM</span></span>](#use-templates-to-customize-restore-vm)
* [<span data-ttu-id="43597-212">使用還原的磁碟連結至現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="43597-212">Use the restored disks to attach to an existing virtual machine</span></span>](../virtual-machines/windows/attach-managed-disk-portal.md)
* [<span data-ttu-id="43597-213">使用 PowerShell 從還原的磁碟建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43597-213">Create a new virtual machine using PowerShell from restored disks.</span></span>](./backup-azure-vms-automation.md#restore-an-azure-vm)

<span data-ttu-id="43597-214">在 [還原組態] 刀鋒視窗上，按一下 [確定] 完成還原組態。</span><span class="sxs-lookup"><span data-stu-id="43597-214">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span></span> <span data-ttu-id="43597-215">在 [還原] 刀鋒視窗上，按一下 [還原] 以觸發還原作業。</span><span class="sxs-lookup"><span data-stu-id="43597-215">On the **Restore** blade, click **Restore** to trigger the restore operation.</span></span>

![已完成復原設定](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-the-restore-operation"></a><span data-ttu-id="43597-217">追蹤還原作業</span><span class="sxs-lookup"><span data-stu-id="43597-217">Track the restore operation</span></span>
<span data-ttu-id="43597-218">一旦觸發還原作業，備份服務會建立一個作業以便追蹤還原作業。</span><span class="sxs-lookup"><span data-stu-id="43597-218">Once you trigger the restore operation, the Backup service creates a job for tracking the restore operation.</span></span> <span data-ttu-id="43597-219">備份服務也會建立，並會在入口網站的 [通知] 區域暫時顯示通知。</span><span class="sxs-lookup"><span data-stu-id="43597-219">The Backup service also creates and temporarily displays the notification in Notifications area of portal.</span></span> <span data-ttu-id="43597-220">如果看不到通知，您隨時可以按一下 [通知] 圖示來檢視您的通知。</span><span class="sxs-lookup"><span data-stu-id="43597-220">If you do not see the notification, you can always click the Notifications icon to view your notifications.</span></span>

![已觸發還原](./media/backup-azure-arm-restore-vms/restore-notification.png)

<span data-ttu-id="43597-222">若要檢視正在處理的作業，或檢視完成的作業，請開啟 [備份作業] 清單。</span><span class="sxs-lookup"><span data-stu-id="43597-222">To view the operation while it is processing, or to view when it completed, open the Backup jobs list.</span></span>

1. <span data-ttu-id="43597-223">在 Azure 功能表上按一下 [瀏覽]，然後在服務清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="43597-223">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span></span> <span data-ttu-id="43597-224">服務清單會調整成您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="43597-224">The list of services adjusts to what you type.</span></span> <span data-ttu-id="43597-225">當您看到 [復原服務保存庫] 時，請選取它。</span><span class="sxs-lookup"><span data-stu-id="43597-225">When you see **Recovery Services vaults**, select it.</span></span>

    ![開啟復原服務保存庫](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    <span data-ttu-id="43597-227">便會顯示訂用帳戶中保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="43597-227">The list of vaults in the subscription is displayed.</span></span>

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. <span data-ttu-id="43597-229">從這份清單，選取與您還原的 VM 相關聯的保存庫。</span><span class="sxs-lookup"><span data-stu-id="43597-229">From the list, select the vault associated with the VM you restored.</span></span> <span data-ttu-id="43597-230">當您按一下保存庫時，其儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="43597-230">When you click the vault, its dashboard opens.</span></span>
3. <span data-ttu-id="43597-231">在保存庫儀表板中的 [備份作業] 圖格上，按一下 [Azure 虛擬機器] 以顯示與保存庫相關聯的作業。</span><span class="sxs-lookup"><span data-stu-id="43597-231">In the vault dashboard on the **Backup Jobs** tile, click **Azure Virtual Machines** to display the jobs associated with the vault.</span></span>

    ![保存庫儀表板](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    <span data-ttu-id="43597-233">[備份作業]  刀鋒視窗會開啟並顯示作業的清單。</span><span class="sxs-lookup"><span data-stu-id="43597-233">The **Backup Jobs** blade opens and displays the list of jobs.</span></span>

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-to-customize-restore-vm"></a><span data-ttu-id="43597-235">使用範本自訂還原的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-235">Use templates to customize restore vm</span></span>
<span data-ttu-id="43597-236">[完成還原磁碟作業](#Track-the-restore-operation)之後，您可以使用還原作業過程所產生的範本，以不同於備份組態的組態來建立新的 VM，或自訂從還原點建立新的 VM 時所建立的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="43597-236">Once [restore disks operation is completed](#Track-the-restore-operation), you can use the template that is generated as part of restore operation to create a new VM with a configuration different from backup configuration or to customize names of resources created as create a new vm from restore point.</span></span> 

> [!NOTE]
> <span data-ttu-id="43597-237">對於 2017年 3 月 1 日之後建立的復原點，範本會新增為還原磁碟的一部分。</span><span class="sxs-lookup"><span data-stu-id="43597-237">Templates will be added as part of Restore Disks for recovery points taken after 1st March, 2017.</span></span> <span data-ttu-id="43597-238">這些範本適用於非加密和非受控磁碟 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-238">They are applicable for non-encrypted and non-managed disk VMs.</span></span> <span data-ttu-id="43597-239">即將發行的版本中支援加密的 VM 和受控磁碟 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-239">Support for encrypted VMs and Managed Disk VMs is coming in upcoming releases.</span></span> 
>
>

<span data-ttu-id="43597-240">若要取得在還原磁碟選項中產生的範本，</span><span class="sxs-lookup"><span data-stu-id="43597-240">To get the template generated as part of restore disks option,</span></span>

1. <span data-ttu-id="43597-241">請移至對應於作業的還原作業詳細資料。</span><span class="sxs-lookup"><span data-stu-id="43597-241">Go to restore job details corresponding to the job.</span></span> 
2. <span data-ttu-id="43597-242">在還原作業詳細資料畫面上，按一下 [部署範本] 按鈕來起始範本部署。</span><span class="sxs-lookup"><span data-stu-id="43597-242">On the restore job details screen, click on *Deploy Template* button to initiate template deployment.</span></span> 

     ![還原作業向下鑽研](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
<span data-ttu-id="43597-244">在自訂部署的 [部署範本] 刀鋒視窗上，使用範本部署來[編輯和部署範本](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template)，或在部署之前[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)以附加更多自訂。</span><span class="sxs-lookup"><span data-stu-id="43597-244">On the Deploy template blade for custom deployment, use template deployment to [edit and deploy the template](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) or append more customizations by [authoring a template](../azure-resource-manager/resource-group-authoring-templates.md) before you deploy.</span></span> 

   ![載入範本部署](./media/backup-azure-arm-restore-vms/loading-template.png)
   
<span data-ttu-id="43597-246">輸入所需的值之後，接受 [條款及條件]，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="43597-246">After entering the required values, accept the *Terms and Conditions* and click on **Purchase**.</span></span>

   ![提交範本部署](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a><span data-ttu-id="43597-248">還原後的步驟</span><span class="sxs-lookup"><span data-stu-id="43597-248">Post-Restore steps</span></span>
* <span data-ttu-id="43597-249">如果您使用 cloud-init 型 Linux 散發套件 (例如 Ubuntu)，基於安全理由，還原後會封鎖密碼。</span><span class="sxs-lookup"><span data-stu-id="43597-249">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password is blocked post restore.</span></span> <span data-ttu-id="43597-250">請在還原的 VM 上使用 VMAccess 擴充功能 [重設密碼](../virtual-machines/linux/classic/reset-access.md)。</span><span class="sxs-lookup"><span data-stu-id="43597-250">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="43597-251">建議您在這些散發套件上使用 SSH 金鑰，以避免在還原後重設密碼。</span><span class="sxs-lookup"><span data-stu-id="43597-251">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span></span>
* <span data-ttu-id="43597-252">出現在備份組態期間的擴充功能，將會安裝但不會啟用。</span><span class="sxs-lookup"><span data-stu-id="43597-252">Extensions present during the backup config will be installed, however they won't be enabled.</span></span> <span data-ttu-id="43597-253">如果您看到任何問題，請重新安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="43597-253">Please reinstall extensions if you see any issue.</span></span> 
* <span data-ttu-id="43597-254">如果備份的 VM 具有靜態 IP，還原後，還原的 VM 將會有動態 IP，以避免在建立還原的 VM 時發生衝突。</span><span class="sxs-lookup"><span data-stu-id="43597-254">If the backed-up VM has static IP, post restore, restored VM will have a dynamic IP to avoid conflict when creating restored VM.</span></span> <span data-ttu-id="43597-255">深入了解如何[將靜態 IP 加入至還原的 VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)</span><span class="sxs-lookup"><span data-stu-id="43597-255">Learn more on how you can [add a static IP to restored VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)</span></span>
* <span data-ttu-id="43597-256">還原的 VM 不會有可用性設定值組。</span><span class="sxs-lookup"><span data-stu-id="43597-256">Restored VM will not have availability value set.</span></span> <span data-ttu-id="43597-257">從 PowerShell 建立 VM 或使用還原的磁碟建立範本時，我們建議使用還原磁碟選項和[新增可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="43597-257">We recommend using restore disks option and [adding availability set](../virtual-machines/windows/tutorial-availability-sets.md) when creating a VM from PowerShell or templates using restored disks.</span></span> 


## <a name="backup-for-restored-vms"></a><span data-ttu-id="43597-258">備份已還原的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-258">Backup for restored VMs</span></span>
<span data-ttu-id="43597-259">如果您已將 VM 還原至相同的資源群組，並使用與原始備份 VM 相同的名稱，則會在還原後於 VM 上繼續進行備份。</span><span class="sxs-lookup"><span data-stu-id="43597-259">If you have restored VM to same Resource Group with the same name as originally backed up VM, backup continues on the VM post restore.</span></span> <span data-ttu-id="43597-260">如果您已將 VM 還原至不同的資源群組，或為還原的 VM 指定不同名稱，系統會將該 VM 視為新 VM，因此您需要為還原 VM 設定備份。</span><span class="sxs-lookup"><span data-stu-id="43597-260">If you have either restored VM to a different Resource group or specified a different name for restored VM, this is treated as a new VM and you need to setup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="43597-261">在 Azure 資料中心發生災害時還原 VM</span><span class="sxs-lookup"><span data-stu-id="43597-261">Restoring a VM during Azure dataCenter disaster</span></span>
<span data-ttu-id="43597-262">如果 VM 執行的主要資料中心發生災害，而您已將備份保存庫設定為異地備援，Azure 備份可讓您將備份 VM 還原至配對的資料中心。</span><span class="sxs-lookup"><span data-stu-id="43597-262">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span></span> <span data-ttu-id="43597-263">在這種情況下，您需要選取配對之資料中心內的儲存體帳戶，其餘的還原程序則保持不變。</span><span class="sxs-lookup"><span data-stu-id="43597-263">During such scenarios, you need to select a storage account, which is present in paired data center and rest of the restore process remains same.</span></span> <span data-ttu-id="43597-264">Azure 備份會使用配對之地理區域的計算服務來建立還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="43597-264">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span></span> <span data-ttu-id="43597-265">深入了解 [Azure 資料中心復原](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span><span class="sxs-lookup"><span data-stu-id="43597-265">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-domain-controller-vms"></a><span data-ttu-id="43597-266">還原網域控制站 VM</span><span class="sxs-lookup"><span data-stu-id="43597-266">Restoring Domain Controller VMs</span></span>
<span data-ttu-id="43597-267">備份網域控制站 (DC) 虛擬機器是 Azure 備份支援的案例。</span><span class="sxs-lookup"><span data-stu-id="43597-267">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span></span> <span data-ttu-id="43597-268">不過，在還原程序進行期間請務必小心。</span><span class="sxs-lookup"><span data-stu-id="43597-268">However, care must be taken during the restore process.</span></span> <span data-ttu-id="43597-269">正確的還原程序取決於網域結構。</span><span class="sxs-lookup"><span data-stu-id="43597-269">The correct restore process depends on the structure of the domain.</span></span> <span data-ttu-id="43597-270">最簡單的情況是您在單一網域中擁有單一 DC。</span><span class="sxs-lookup"><span data-stu-id="43597-270">In the simplest case you have a single DC in a single domain.</span></span> <span data-ttu-id="43597-271">而在生產環境的負載中，較常見的情況是您擁有單一網域且內含多個 DC，其中有些 DC 可能位於內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="43597-271">More commonly for production loads, you will have a single domain with multiple DCs, perhaps with some DCs on premises.</span></span> <span data-ttu-id="43597-272">最後，您也可能擁有內含多個網域的樹系。</span><span class="sxs-lookup"><span data-stu-id="43597-272">Finally, you may have a forest with multiple domains.</span></span> 

<span data-ttu-id="43597-273">從 Active Directory 的觀點來看，Azure VM 就像是位於新式的受支援 Hypervisor 上的其他 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-273">From an Active Directory perspective the Azure VM is like any other VM on a modern supported hypervisor.</span></span> <span data-ttu-id="43597-274">與內部部署 Hypervisor 的主要差異是，Azure 沒有提供 VM 主控台。</span><span class="sxs-lookup"><span data-stu-id="43597-274">The major difference with on-premises hypervisors is that there is no VM console available in Azure.</span></span> <span data-ttu-id="43597-275">在某些情況下，您必須使用主控台，例如使用裸機復原 (BMR) 類型的備份進行復原。</span><span class="sxs-lookup"><span data-stu-id="43597-275">A console is required for certain scenarios such as recovering using a Bare Metal Recovery (BMR) type backup.</span></span> <span data-ttu-id="43597-276">不過，從備份保存庫來還原 VM 可完整取代 BMR。</span><span class="sxs-lookup"><span data-stu-id="43597-276">However, VM restore from the backup vault is a full replacement for BMR.</span></span> <span data-ttu-id="43597-277">我們也提供了 Active Directory 還原模式 (DSRM)，因此，您可以進行所有的 Active Directory 復原案例。</span><span class="sxs-lookup"><span data-stu-id="43597-277">Active Directory Restore Mode (DSRM) is also available, so all Active Directory recovery scenarios are viable.</span></span> <span data-ttu-id="43597-278">如需更多背景資訊，請參閱[虛擬網域控制站的備份和還原考量](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)以及[規劃 Active Directory 樹系復原](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="43597-278">For more background information, please check [Backup and Restore considerations for virtualized Domain Controllers](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) and [Planning for Active Directory Forest Recovery](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).</span></span>

### <a name="single-dc-in-a-single-domain"></a><span data-ttu-id="43597-279">單一網域中的單一 DC</span><span class="sxs-lookup"><span data-stu-id="43597-279">Single DC in a single domain</span></span>
<span data-ttu-id="43597-280">VM 可以從 Azure 入口網站或使用 PowerShell 還原 (就像任何其他 VM)。</span><span class="sxs-lookup"><span data-stu-id="43597-280">The VM can be restored (like any other VM) from the Azure portal or using PowerShell.</span></span>

### <a name="multiple-dcs-in-a-single-domain"></a><span data-ttu-id="43597-281">單一網域中的多個 DC</span><span class="sxs-lookup"><span data-stu-id="43597-281">Multiple DCs in a single domain</span></span>
<span data-ttu-id="43597-282">如果您可以透過網路來連線到相同網域內的其他 DC，您就可以像 VM 一樣地還原 DC。</span><span class="sxs-lookup"><span data-stu-id="43597-282">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="43597-283">如果該 DC 是網域內剩餘的最後一個 DC，或者您是在隔離的網路中進行復原，則您必須遵循樹系的復原程序。</span><span class="sxs-lookup"><span data-stu-id="43597-283">If it is the last remaining DC in the domain, or a recovery in an isolated network is performed, a forest recovery procedure must be followed.</span></span>

### <a name="multiple-domains-in-one-forest"></a><span data-ttu-id="43597-284">單一樹系中的多個網域</span><span class="sxs-lookup"><span data-stu-id="43597-284">Multiple domains in one forest</span></span>
<span data-ttu-id="43597-285">如果您可以透過網路來連線到相同網域內的其他 DC，您就可以像 VM 一樣地還原 DC。</span><span class="sxs-lookup"><span data-stu-id="43597-285">When other DCs of the same domain can be reached over the network, the DC can be restored like any VM.</span></span> <span data-ttu-id="43597-286">不過，若是其他情況，則建議進行樹系復原。</span><span class="sxs-lookup"><span data-stu-id="43597-286">However, in all other cases a forest recovery is recommended.</span></span>

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="43597-287">還原具有特殊網路組態的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-287">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="43597-288">可以備份和還原具有下列特殊網路組態的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-288">It is possible to back up and restore VMs with the following special network configurations.</span></span> <span data-ttu-id="43597-289">不過，進行還原程序時，這些組態需要一些特殊的考量。</span><span class="sxs-lookup"><span data-stu-id="43597-289">However, these configurations require some special consideration while going through the restore process.</span></span>

* <span data-ttu-id="43597-290">負載平衡器底下的 VM (內部與外部)</span><span class="sxs-lookup"><span data-stu-id="43597-290">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="43597-291">具有多個保留的 IP 的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-291">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="43597-292">具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="43597-292">VMs with multiple NICs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43597-293">建立 VM 的特殊網路組態時，您必須使用 PowerShell 從還原的磁碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-293">When creating the special network configuration for VMs, you must use PowerShell to create VMs from the disks restored.</span></span>
>
>

<span data-ttu-id="43597-294">若要在還原至磁碟後，完全重新建立虛擬機器，請依照以下步驟執行：</span><span class="sxs-lookup"><span data-stu-id="43597-294">To fully recreate the virtual machines after restoring to disk, follow these steps:</span></span>

1. <span data-ttu-id="43597-295">使用 [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm) 從復原服務保存庫還原磁碟</span><span class="sxs-lookup"><span data-stu-id="43597-295">Restore the disks from a recovery services vault using [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="43597-296">使用 PowerShell Cmdlet 建立負載平衡器/多個 NIC/多個保留的 IP 所需的 VM 組態，並使用該組態建立具備想要之組態的 VM。</span><span class="sxs-lookup"><span data-stu-id="43597-296">Create the VM configuration required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span></span>

   * <span data-ttu-id="43597-297">使用 [內部負載平衡器 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="43597-297">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="43597-298">建立 VM 來連接至[網際網路面向負載平衡器](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="43597-298">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="43597-299">建立具有 [多個 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="43597-299">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="43597-300">建立具有 [多個保留的 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="43597-300">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="43597-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43597-301">Next steps</span></span>
<span data-ttu-id="43597-302">您現在可以還原您的 VM，請參閱疑難排解文章中有關 VM 常見錯誤的資訊。</span><span class="sxs-lookup"><span data-stu-id="43597-302">Now that you can restore your VMs, see the troubleshooting article for information on common errors with VMs.</span></span> <span data-ttu-id="43597-303">此外，請參閱有關您的 VM 管理工作的文章。</span><span class="sxs-lookup"><span data-stu-id="43597-303">Also, check out the article on managing tasks with your VMs.</span></span>

* [<span data-ttu-id="43597-304">針對錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="43597-304">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="43597-305">管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="43597-305">Manage virtual machines</span></span>](backup-azure-manage-vms.md)
