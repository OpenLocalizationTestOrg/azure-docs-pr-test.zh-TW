---
title: "測試容錯移轉的 HYPER-V 複寫 （而不使用 System Center VMM) tooAzure aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉的 HYPER-V Vm 複寫 tooAzure 使用 hello Azure Site Recovery 服務的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a><span data-ttu-id="4c783-103">步驟 11： 執行測試容錯移轉的 HYPER-V 複寫 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4c783-103">Step 11: Run a test failover for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="4c783-104">本文說明如何 toorun 測試容錯移轉從內部部署 HYPER-V 虛擬機器 （不受 System Center VMM） tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="4c783-104">This article describes how toorun a test failover from  on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="4c783-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="4c783-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4c783-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="4c783-106">Before you start</span></span>

<span data-ttu-id="4c783-107">執行測試容錯移轉，我們建議您確認 hello VM 屬性，並進行任何變更之前，您需要。</span><span class="sxs-lookup"><span data-stu-id="4c783-107">Before you run a test failover we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="4c783-108">您可以存取在 hello VM 屬性**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="4c783-108">you can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="4c783-109">hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="4c783-109">hello **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="4c783-110">受控磁碟的考量</span><span class="sxs-lookup"><span data-stu-id="4c783-110">Managed disk considerations</span></span>

<span data-ttu-id="4c783-111">[管理磁碟](../virtual-machines/windows/managed-disks-overview.md)管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure Vm 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="4c783-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing hello storage accounts associated with hello VM disks.</span></span> 

- <span data-ttu-id="4c783-112">受管理的磁碟建立並附加 toohello VM，只會發生容錯移轉 tooAzure 時。</span><span class="sxs-lookup"><span data-stu-id="4c783-112">Managed disks are created and attached toohello VM only when a failover tooAzure occurs.</span></span> <span data-ttu-id="4c783-113">當您啟用保護時，在內部部署的 Vm 所傳來的資料會複寫 toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c783-113">When you enable protection, data from on-premises VMs replicates toostorage accounts.</span></span>
- <span data-ttu-id="4c783-114">受管理的磁碟只可以建立使用 hello 資源管理員部署模型所部署的 Vm。</span><span class="sxs-lookup"><span data-stu-id="4c783-114">Managed disks can be created only for VMs that are deployed using hello Resource manager deployment model.</span></span>
- <span data-ttu-id="4c783-115">從 Azure tooan 容錯回復內部部署 HYPER-V 環境目前不支援受管理的磁碟使用的機器。</span><span class="sxs-lookup"><span data-stu-id="4c783-115">Failback from Azure tooan on-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="4c783-116">您應該只設定**使用受管理磁碟**太**是**若您正在進行移轉唯一 (容錯移轉 tooAzure 容錯回復不)</span><span class="sxs-lookup"><span data-stu-id="4c783-116">You should only set **Use managed disks** too**Yes** if you're doing a migration only (failover tooAzure without failback)</span></span>
- <span data-ttu-id="4c783-117">啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。</span><span class="sxs-lookup"><span data-stu-id="4c783-117">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="4c783-118">受管理的磁碟的 Vm 必須在可用性設定組與**使用受管理磁碟**設定得**是**。</span><span class="sxs-lookup"><span data-stu-id="4c783-118">VMs with managed disks must be in availability sets with **Use managed disks** set too**Yes**.</span></span> <span data-ttu-id="4c783-119">如果 Vm 未啟用 hello 設定，則可以選取只可用性集資源群組中而不會啟用受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="4c783-119">If hello setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span> <span data-ttu-id="4c783-120">[深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="4c783-120">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span></span>
- - <span data-ttu-id="4c783-121">如果 hello 複寫所使用的儲存體帳戶與儲存體服務加密已加密，不能在容錯移轉期間建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="4c783-121">If hello storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="4c783-122">在此情況下可能是不允許使用受管理的磁碟，或停用保護 hello VM，然後將它重新啟用 toouse 沒有加密已啟用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c783-122">In this case either don't enable use of managed disks, or disable protection for hello VM, and reenable it toouse a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="4c783-123">[深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="4c783-123">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>

 
## <a name="network-considerations"></a><span data-ttu-id="4c783-124">網路考量事項</span><span class="sxs-lookup"><span data-stu-id="4c783-124">Network considerations</span></span>
    
- <span data-ttu-id="4c783-125">您可以設定用於容錯移轉之後的 hello Azure VM 的 hello 目標 IP 位址 toobe。</span><span class="sxs-lookup"><span data-stu-id="4c783-125">You can set hello target IP address toobe used for hello Azure VM after failover.</span></span> <span data-ttu-id="4c783-126">如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="4c783-126">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="4c783-127">如果您將無法使用在容錯移轉的位址，hello 容錯移轉將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4c783-127">If you set an address that isn't available at failover, hello failover will fail.</span></span> <span data-ttu-id="4c783-128">相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4c783-128">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>
- <span data-ttu-id="4c783-129">hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：</span><span class="sxs-lookup"><span data-stu-id="4c783-129">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>
    - <span data-ttu-id="4c783-130">如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="4c783-130">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
    - <span data-ttu-id="4c783-131">如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="4c783-131">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
    - <span data-ttu-id="4c783-132">例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="4c783-132">For example if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="4c783-133">如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。</span><span class="sxs-lookup"><span data-stu-id="4c783-133">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
- <span data-ttu-id="4c783-134">如果 hello VM 有多張網路介面卡將所有連線 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="4c783-134">If hello VM has multiple network adapters they will all connect toohello same network.</span></span>
- <span data-ttu-id="4c783-135">如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="4c783-135">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>


## <a name="view-and-manage-vm-settings"></a><span data-ttu-id="4c783-136">檢視及管理 VM 設定</span><span class="sxs-lookup"><span data-stu-id="4c783-136">View and manage VM settings</span></span>

<span data-ttu-id="4c783-137">我們建議您執行容錯移轉之前，確認 hello hello 來源機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="4c783-137">We recommend that you verify hello properties of hello source machine before you run a failover.</span></span>

1. <span data-ttu-id="4c783-138">在**受保護項目**，按一下**複寫的項目**，然後按一下 hello VM。</span><span class="sxs-lookup"><span data-stu-id="4c783-138">In **Protected Items**, click **Replicated Items**, and click hello VM.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. <span data-ttu-id="4c783-140">在 [hello**複寫項目**] 窗格中，您可以看到 VM 資訊、 健全狀況狀態，以及最新可用的復原點 hello 的摘要。</span><span class="sxs-lookup"><span data-stu-id="4c783-140">In hello **Replicated item** pane, you can see a summary of VM information, health status, and hello latest available recovery points.</span></span> <span data-ttu-id="4c783-141">按一下**屬性**tooview 更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4c783-141">Click **Properties** tooview more details.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. <span data-ttu-id="4c783-143">在 [計算與網路] 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="4c783-143">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="4c783-144">修改 hello Azure VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="4c783-144">Modify hello Azure VM name.</span></span> <span data-ttu-id="4c783-145">hello 名稱必須符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="4c783-145">hello name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="4c783-146">指定容錯移轉後的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="4c783-146">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="4c783-147">指定 hello Azure VM 的目標大小</span><span class="sxs-lookup"><span data-stu-id="4c783-147">Specify a target size for hello Azure VM</span></span>
    - <span data-ttu-id="4c783-148">選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="4c783-148">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="4c783-149">指定是否 toouse[管理磁碟](#managed-disk-considerations)。</span><span class="sxs-lookup"><span data-stu-id="4c783-149">Specify whether toouse [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="4c783-150">選取**是**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="4c783-150">Select **Yes**, if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span>
    - <span data-ttu-id="4c783-151">檢視或修改網路設定，包括 hello 網路/子網路中的 hello Azure VM 將會位於容錯移轉之後，以及要指派 tooit hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4c783-151">View or modify network settings, including hello network/subnet in which hello Azure VM will be located after failover, and hello IP address that will be assigned tooit.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. <span data-ttu-id="4c783-153">在**磁碟**、 您可以看到 hello 作業系統的相關資訊和資料磁碟上的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="4c783-153">In **Disks**, you can see information about hello operating system and data disks on hello VM.</span></span>


## <a name="run-a-test-failover"></a><span data-ttu-id="4c783-154">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4c783-154">Run a test failover</span></span>

<span data-ttu-id="4c783-155">現在，執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="4c783-155">Now, run a test failover toomake sure everything's working as expected.</span></span>

- <span data-ttu-id="4c783-156">如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="4c783-156">If you want tooconnect tooAzure VMs using RDP after failover, [prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="4c783-157">您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。</span><span class="sxs-lookup"><span data-stu-id="4c783-157">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="4c783-158">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="4c783-158">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="4c783-159">如需關於測試容錯移轉的完整資訊，請參閱[本文](site-recovery-test-failover-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="4c783-159">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
 
 <span data-ttu-id="4c783-160">立即執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="4c783-160">Now run a failover:</span></span>

1. <span data-ttu-id="4c783-161">透過單一電腦、 toofail 中**複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="4c783-161">toofail over a single machine, in **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="4c783-162">toofail 透過復原計劃，在**復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="4c783-162">toofail over a recovery plan, in **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="4c783-163">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="4c783-163">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="4c783-164">在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="4c783-164">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="4c783-165">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4c783-165">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="4c783-166">您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="4c783-166">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="4c783-167">Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="4c783-167">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="4c783-168">您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="4c783-168">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="4c783-169">如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="4c783-169">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>
7. <span data-ttu-id="4c783-170">完成後，按一下**清除測試容錯移轉**hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4c783-170">After you finish, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="4c783-171">在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="4c783-171">In **Notes** record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="4c783-172">這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4c783-172">This will delete hello virtual machines that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4c783-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c783-173">Next steps</span></span>

- <span data-ttu-id="4c783-174">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="4c783-174">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="4c783-175">[閱讀 容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)，toofail 回和複寫的 Azure Vm 回 toohello 主要內部部署 HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="4c783-175">[Read about failback](site-recovery-failback-from-azure-to-hyper-v.md), toofail back and replicate Azure VMs back toohello primary on-premises Hyper-V site.</span></span>

