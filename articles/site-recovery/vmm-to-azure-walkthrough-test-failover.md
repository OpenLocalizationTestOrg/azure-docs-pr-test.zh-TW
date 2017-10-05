---
title: "執行 Hyper-V 複寫至 Azure 的測試容錯移轉 (含 System Center VMM) | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務將 VMM 雲端中的 Hyper-V VM 複寫至 Azure 時，執行測試容錯移轉所需的步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7b562a23-7ba7-48ee-905d-c22b4b5d6466
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 4688fc4bc74a9e0e04487cfbe965006070fd9a7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="96ae2-103">步驟 11：執行 Hyper-V (含 VMM) 複寫至 Azure 的測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="96ae2-103">Step 11: Run a test failover for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="96ae2-104">啟用 [Hyper-V VM 的複寫](vmm-to-azure-walkthrough-enable-replication.md)後，請使用本文來執行測試容錯移轉，以在 Azure 入口網站中，使用 [Azure Site Recovery](site-recovery-overview.md) 服務從 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V 虛擬機器容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="96ae2-104">After you [enable replication for Hyper-V VMs](vmm-to-azure-walkthrough-enable-replication.md), use this article to run a test failover from  on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="96ae2-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="96ae2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="96ae2-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="96ae2-106">Before you start</span></span>

<span data-ttu-id="96ae2-107">在您執行測試容錯移轉之前，建議您確認 VM 屬性，並進行任何需要的變更。</span><span class="sxs-lookup"><span data-stu-id="96ae2-107">Before you run a test failover we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="96ae2-108">您可以在 [複寫的項目] 中存取 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="96ae2-108">you can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="96ae2-109">[程式集]  刀鋒視窗會顯示機器設定與狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="96ae2-109">The **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="96ae2-110">受控磁碟的考量</span><span class="sxs-lookup"><span data-stu-id="96ae2-110">Managed disk considerations</span></span>

<span data-ttu-id="96ae2-111">[受控磁碟](../virtual-machines/windows/managed-disks-overview.md)會管理與 VM 磁碟相關聯的儲存體帳戶，從而簡化 Azure VM 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="96ae2-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing the storage accounts associated with the VM disks.</span></span> 

- <span data-ttu-id="96ae2-112">只有當容錯移轉至 Azure 時，受控磁碟會加以建立並連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="96ae2-112">Managed disks are created and attached to the VM only when a failover to Azure occurs.</span></span> <span data-ttu-id="96ae2-113">當您啟用保護時，來自內部部署 VM 的資料會複寫到儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="96ae2-113">When you enable protection, data from on-premises VMs replicates to storage accounts.</span></span>
- <span data-ttu-id="96ae2-114">只有使用 Resource Manager 部署模型部署的 VM 才能建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="96ae2-114">Managed disks can be created only for VMs that are deployed using the Resource manager deployment model.</span></span>
- <span data-ttu-id="96ae2-115">具有受控磁碟的電腦目前不支援從 Azure 容錯回復到內部部署 Hyper-V 環境。</span><span class="sxs-lookup"><span data-stu-id="96ae2-115">Failback from Azure to an on-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="96ae2-116">若您只要進行移轉 (容錯移轉至 Azure 不含容錯回復)，應該只將 [使用受控磁碟] 設定為 [是]</span><span class="sxs-lookup"><span data-stu-id="96ae2-116">You should only set **Use managed disks** to **Yes** if you're doing a migration only (failover to Azure without failback)</span></span>
- <span data-ttu-id="96ae2-117">啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。</span><span class="sxs-lookup"><span data-stu-id="96ae2-117">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="96ae2-118">具有受控磁碟的 VM 必須位於 [使用受控磁碟] 設定為 [是] 的可用性群組中。</span><span class="sxs-lookup"><span data-stu-id="96ae2-118">VMs with managed disks must be in availability sets with **Use managed disks** set to **Yes**.</span></span> <span data-ttu-id="96ae2-119">若 VM 未啟用此設定，則只有未啟用受控磁碟的資源群組之可用性設定組可供選取。</span><span class="sxs-lookup"><span data-stu-id="96ae2-119">If the setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span> <span data-ttu-id="96ae2-120">[深入了解](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-120">[Learn more](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).</span></span>
- - <span data-ttu-id="96ae2-121">如果您用來複寫的儲存體帳戶已使用「儲存體服務加密」進行加密，就不能在容錯移轉期間建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="96ae2-121">If the storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="96ae2-122">在此情況下，請不要啟用使用受控磁碟的功能，或是停用 VM 保護，然後再將它重新啟用，以使用未啟用加密的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="96ae2-122">In this case either don't enable use of managed disks, or disable protection for the VM, and reenable it to use a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="96ae2-123">[深入了解](../virtual-machines/windows/managed-disks-overview.md#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-123">[Learn more](../virtual-machines/windows/managed-disks-overview.md#managed-disks-and-encryption).</span></span>

 
## <a name="network-considerations"></a><span data-ttu-id="96ae2-124">網路考量事項</span><span class="sxs-lookup"><span data-stu-id="96ae2-124">Network considerations</span></span>
    
- <span data-ttu-id="96ae2-125">您可以將目標 IP 位址設定為要在容錯移轉之後用於 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="96ae2-125">You can set the target IP address to be used for the Azure VM after failover.</span></span> <span data-ttu-id="96ae2-126">如果您未提供地址，則容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="96ae2-126">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="96ae2-127">如果您設定無法用於容錯移轉的位址，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="96ae2-127">If you set an address that isn't available at failover, the failover will fail.</span></span> <span data-ttu-id="96ae2-128">如果位址可用於測試容錯移轉網路，則相同的目標 IP 位址可用於測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="96ae2-128">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>
- <span data-ttu-id="96ae2-129">網路介面卡的數目會視您指定給目標虛擬機器的大小而有所不同，如下所示：</span><span class="sxs-lookup"><span data-stu-id="96ae2-129">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>
    - <span data-ttu-id="96ae2-130">如果來源電腦上的網路介面卡數目小於或等於針對目標機器大小所允許的介面卡數目，則目標將具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="96ae2-130">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
    - <span data-ttu-id="96ae2-131">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則將使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="96ae2-131">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
    - <span data-ttu-id="96ae2-132">例如，如果來源機器具有兩張網路介面卡，而目標機器大小支援四張，則目標機器將會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="96ae2-132">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="96ae2-133">如果來源機器具有兩張介面卡，但支援的目標大小僅支援一張，則目標機器將只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="96ae2-133">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
- <span data-ttu-id="96ae2-134">如果 VM 有多張網路介面卡，則全部會連接至相同的網路。</span><span class="sxs-lookup"><span data-stu-id="96ae2-134">If the VM has multiple network adapters they will all connect to the same network.</span></span>
- <span data-ttu-id="96ae2-135">如果虛擬機器具有多個網路介面卡，則清單中顯示的第一個會變成 Azure 虛擬機器中的*預設*網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="96ae2-135">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>


## <a name="view-and-manage-vm-settings"></a><span data-ttu-id="96ae2-136">檢視及管理 VM 設定</span><span class="sxs-lookup"><span data-stu-id="96ae2-136">View and manage VM settings</span></span>

<span data-ttu-id="96ae2-137">建議您在執行容錯移轉之前，確認來源機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="96ae2-137">We recommend that you verify the properties of the source machine before you run a failover.</span></span>

1. <span data-ttu-id="96ae2-138">在 [受保護的項目] 中，按一下 [複寫的項目]，然後按一下 [VM]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-138">In **Protected Items**, click **Replicated Items**, and click the VM.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-test-failover/test-failover1.png)
2. <span data-ttu-id="96ae2-140">在 [複寫的項目] 窗格中，您可以看到 VM 資訊、健康情況狀態，以及最新可用復原點的摘要。</span><span class="sxs-lookup"><span data-stu-id="96ae2-140">In the **Replicated item** pane, you can see a summary of VM information, health status, and the latest available recovery points.</span></span> <span data-ttu-id="96ae2-141">如需檢視詳細資訊，請按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-141">Click **Properties** to view more details.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-test-failover/test-failover2.png)
3. <span data-ttu-id="96ae2-143">在 [計算與網路] 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="96ae2-143">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="96ae2-144">修改 Azure VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="96ae2-144">Modify the Azure VM name.</span></span> <span data-ttu-id="96ae2-145">名稱必須符合 [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-145">The name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="96ae2-146">指定容錯移轉後的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-146">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="96ae2-147">指定 Azure VM 的目標大小</span><span class="sxs-lookup"><span data-stu-id="96ae2-147">Specify a target size for the Azure VM</span></span>
    - <span data-ttu-id="96ae2-148">選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-148">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="96ae2-149">指定是否要使用[受控磁碟](#managed-disk-considerations)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-149">Specify whether to use [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="96ae2-150">如果您想要將受控磁碟連結到您移轉至 Azure 的機器上，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-150">Select **Yes**, if you want to attach managed disks to your machine on migration to Azure.</span></span>
    - <span data-ttu-id="96ae2-151">檢視或修改網路設定，包括在容錯移轉後 Azure VM 所在的網路/子網路，以及要指派給它的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="96ae2-151">View or modify network settings, including the network/subnet in which the Azure VM will be located after failover, and the IP address that will be assigned to it.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-test-failover/test-failover4.png)
4. <span data-ttu-id="96ae2-153">在 [磁碟] 中，您可以看見 VM 上作業系統和資料磁碟的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="96ae2-153">In **Disks**, you can see information about the operating system and data disks on the VM.</span></span>


## <a name="run-a-test-failover"></a><span data-ttu-id="96ae2-154">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="96ae2-154">Run a test failover</span></span>

<span data-ttu-id="96ae2-155">現在，執行測試容錯移轉，確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="96ae2-155">Now, run a test failover to make sure everything's working as expected.</span></span>

- <span data-ttu-id="96ae2-156">如果您想要在容錯移轉後使用 RDP 連線到 Azure VM，請[準備連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-156">If you want to connect to Azure VMs using RDP after failover, [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="96ae2-157">若要完整測試，您需要在測試環境中將 Active Directory 和 DNS 進行複製。</span><span class="sxs-lookup"><span data-stu-id="96ae2-157">To fully test you need to copy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="96ae2-158">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-158">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="96ae2-159">如需關於測試容錯移轉的完整資訊，請參閱[本文](site-recovery-test-failover-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-159">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
 
 <span data-ttu-id="96ae2-160">立即執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="96ae2-160">Now run a failover:</span></span>

1. <span data-ttu-id="96ae2-161">若要容錯移轉單一機器，請在 [複寫的項目] 中，按一下 VM > [+測試容錯移轉] 圖示。</span><span class="sxs-lookup"><span data-stu-id="96ae2-161">To fail over a single machine, in **Replicated Items**, click the VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="96ae2-162">若要容錯移轉復原方案，請在 [復原方案] 中，以滑鼠右鍵按一下方案 > [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-162">To fail over a recovery plan, in **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="96ae2-163">若要建立復原方案，請[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="96ae2-163">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="96ae2-164">在 [測試容錯移轉] 中，選取 Azure VM 在容錯移轉之後要連接的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="96ae2-164">In **Test Failover**, select the Azure network to which Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="96ae2-165">按一下 [確定]  即可開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="96ae2-165">Click **OK** to begin the failover.</span></span> <span data-ttu-id="96ae2-166">您可以按一下 VM 以開啟其屬性，或在保存庫名稱 > [作業]  > [Site Recovery 作業] 中的 [測試容錯移轉] 作業上按一下，來追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="96ae2-166">You can track progress by clicking on the VM to open its properties, or on the **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="96ae2-167">容錯移轉完成之後，您應該也會看到複本 Azure 機器出現在 Azure 入口網站 > [虛擬機器]中。</span><span class="sxs-lookup"><span data-stu-id="96ae2-167">After the failover completes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="96ae2-168">您應該確定 VM 為適當的大小、已連接到適當的網路，而且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="96ae2-168">You should make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="96ae2-169">如果您已準備好在容錯移轉後進行連線，應該能夠連線到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="96ae2-169">If you prepared for connections after failover, you should be able to connect to the Azure VM.</span></span>
7. <span data-ttu-id="96ae2-170">完成後，在復原方案上按一下 [清除測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="96ae2-170">After you finish, click on **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="96ae2-171">在 [記事]  中，記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="96ae2-171">In **Notes** record and save any observations associated with the test failover.</span></span> <span data-ttu-id="96ae2-172">這將刪除在測試容錯移轉期間所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="96ae2-172">This will delete the virtual machines that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="96ae2-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96ae2-173">Next steps</span></span>

- <span data-ttu-id="96ae2-174">[深入了解](site-recovery-failover.md)不同類型的容錯移轉及如何執行。</span><span class="sxs-lookup"><span data-stu-id="96ae2-174">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="96ae2-175">[深入了解容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)，以便將 Azure VM 容錯回復和複寫回到主要內部部署 VMM 雲端。</span><span class="sxs-lookup"><span data-stu-id="96ae2-175">[Read about failback](site-recovery-failback-from-azure-to-hyper-v.md), to fail back and replicate Azure VMs back to the primary on-premises VMM cloud.</span></span>

