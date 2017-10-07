---
title: "測試容錯移轉的 VMware 複寫 tooAzure aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉，複寫使用 hello Azure Site Recovery 服務 tooAzure VMware vm 的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a><span data-ttu-id="2ce8b-103">步驟 12： 執行測試容錯移轉 tooAzure VMware vm</span><span class="sxs-lookup"><span data-stu-id="2ce8b-103">Step 12: Run a test failover tooAzure for VMware VMs</span></span>

<span data-ttu-id="2ce8b-104">本文說明如何 toorun 測試容錯移轉從內部部署 VMware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-104">This article describes how toorun a test failover from  on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="2ce8b-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="2ce8b-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="2ce8b-106">Before you start</span></span>

<span data-ttu-id="2ce8b-107">執行測試容錯移轉，我們建議您確認 hello VM 屬性，並進行任何變更之前，您需要。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-107">Before you run a test failover we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="2ce8b-108">您可以存取在 hello VM 屬性**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-108">you can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="2ce8b-109">hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-109">hello **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="2ce8b-110">受控磁碟的考量</span><span class="sxs-lookup"><span data-stu-id="2ce8b-110">Managed disk considerations</span></span>

<span data-ttu-id="2ce8b-111">[管理磁碟](../virtual-machines/windows/managed-disks-overview.md)管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure Vm 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing hello storage accounts associated with hello VM disks.</span></span> 

- <span data-ttu-id="2ce8b-112">當您啟用 vm 保護時，VM 資料會複寫 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-112">When you enable protection for a VM, VM data replicates tooa storage account.</span></span> <span data-ttu-id="2ce8b-113">受管理的磁碟建立並附加 toohello VM，只會容錯移轉發生時。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-113">Managed disks are created and attached toohello VM only when failover occurs.</span></span>
- <span data-ttu-id="2ce8b-114">只部署的 Vm 使用 hello 資源管理員的模型，可以建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-114">Managed disks can be created only for VMs deployed using hello Resource Manager model.</span></span>  
- <span data-ttu-id="2ce8b-115">啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="2ce8b-116">受管理的磁碟的 Vm 必須在可用性設定組與**使用受管理磁碟**設定得**是**。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-116">VMs with managed disks must be in availability sets with **Use managed disks** set too**Yes**.</span></span> <span data-ttu-id="2ce8b-117">如果 Vm 未啟用 hello 設定，則可以選取只可用性集資源群組中而不會啟用受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-117">If hello setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="2ce8b-118">[深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)受控磁碟和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="2ce8b-119">如果 hello 複寫所使用的儲存體帳戶與儲存體服務加密已加密，不能在容錯移轉期間建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-119">If hello storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="2ce8b-120">在此情況下可能是不允許使用受管理的磁碟，或停用保護 hello VM，然後將它重新啟用 toouse 沒有加密已啟用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-120">In this case either don't enable use of managed disks, or disable protection for hello VM, and reenable it toouse a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="2ce8b-121">[深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="2ce8b-122">網路考量事項</span><span class="sxs-lookup"><span data-stu-id="2ce8b-122">Network considerations</span></span>

<span data-ttu-id="2ce8b-123">您可以建立容錯移轉後的 Azure vm 中設定 hello 目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-123">You can set hello target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="2ce8b-124">如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-124">If you don't provide an address, hello failed over machine will use DHCP.</span></span>
- <span data-ttu-id="2ce8b-125">如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="2ce8b-126">相同的目標 IP 位址可用於測試容錯移轉，若 hello 位址 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-126">hello same target IP address can be used for test failover, if hello address is available in hello test failover network.</span></span>
- <span data-ttu-id="2ce8b-127">網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：</span><span class="sxs-lookup"><span data-stu-id="2ce8b-127">hello number of network adapters is dictated by hello size you specify for hello target virtual machine:</span></span>

     - <span data-ttu-id="2ce8b-128">如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標必須 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-128">If hello number of network adapters on hello source machine is hello same as, or less than, hello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     - <span data-ttu-id="2ce8b-129">如果 hello hello 來源虛擬機器介面卡的數目超過允許 hello 目標大小，hello 數目 hello 目標大小最大值則會使用。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-129">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size, then hello target size maximum will be used.</span></span>
     - <span data-ttu-id="2ce8b-130">例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-130">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="2ce8b-131">如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-131">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="2ce8b-132">如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-132">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
   - <span data-ttu-id="2ce8b-133">如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-133">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>
 - <span data-ttu-id="2ce8b-134">[深入了解](vmware-walkthrough-network.md) IP 位址指定。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="2ce8b-135">檢視及修改 VM 設定</span><span class="sxs-lookup"><span data-stu-id="2ce8b-135">View and modify VM settings</span></span>

<span data-ttu-id="2ce8b-136">我們建議您執行容錯移轉之前，確認 hello hello 來源機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-136">We recommend that you verify hello properties of hello source machine before you run a failover.</span></span>

1. <span data-ttu-id="2ce8b-137">在**受保護項目**，按一下**複寫的項目**，然後按一下 hello VM。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-137">In **Protected Items**, click **Replicated Items**, and click hello VM.</span></span>
2. <span data-ttu-id="2ce8b-138">在 [hello**複寫項目**] 窗格中，您可以看到 VM 資訊、 健全狀況狀態，以及最新可用的復原點 hello 的摘要。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-138">In hello **Replicated item** pane, you can see a summary of VM information, health status, and hello latest available recovery points.</span></span> <span data-ttu-id="2ce8b-139">按一下**屬性**tooview 更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-139">Click **Properties** tooview more details.</span></span>
3. <span data-ttu-id="2ce8b-140">在 [計算與網路] 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="2ce8b-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="2ce8b-141">修改 hello Azure VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-141">Modify hello Azure VM name.</span></span> <span data-ttu-id="2ce8b-142">hello 名稱必須符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-142">hello name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="2ce8b-143">指定容錯移轉後的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="2ce8b-144">指定 hello Azure VM 的目標大小</span><span class="sxs-lookup"><span data-stu-id="2ce8b-144">Specify a target size for hello Azure VM</span></span>
    - <span data-ttu-id="2ce8b-145">選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="2ce8b-146">指定是否 toouse[管理磁碟](#managed-disk-considerations)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-146">Specify whether toouse [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="2ce8b-147">選取**是**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-147">Select **Yes**, if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span>
    - <span data-ttu-id="2ce8b-148">檢視或修改網路設定，包括 hello 網路/子網路中的 hello Azure VM 將會位於容錯移轉之後，以及要指派 tooit hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-148">View or modify network settings, including hello network/subnet in which hello Azure VM will be located after failover, and hello IP address that will be assigned tooit.</span></span>
4. <span data-ttu-id="2ce8b-149">在**磁碟**、 您可以看到 hello 作業系統的相關資訊和資料磁碟上的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-149">In **Disks**, you can see information about hello operating system and data disks on hello VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="2ce8b-150">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="2ce8b-150">Run a test failover</span></span>

<span data-ttu-id="2ce8b-151">您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-151">After you've set everything up, run a test failover toomake sure everything's working as expected.</span></span>

- <span data-ttu-id="2ce8b-152">如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-152">If you want tooconnect tooAzure VMs using RDP after failover, [prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="2ce8b-153">您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-153">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="2ce8b-154">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="2ce8b-155">如需有關測試容錯移轉的完整資訊，請參閱[這篇文章](site-recovery-test-failover-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="2ce8b-156">在開始之前，請透過影片快速建立概念︰</span><span class="sxs-lookup"><span data-stu-id="2ce8b-156">Get a quick video overview before you start:</span></span>


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


<span data-ttu-id="2ce8b-157">現在，請執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="2ce8b-157">Now, run a failover:</span></span>

1. <span data-ttu-id="2ce8b-158">透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-158">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>

    ![測試容錯移轉](./media/vmware-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="2ce8b-160">toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-160">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="2ce8b-161">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-161">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="2ce8b-162">在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-162">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="2ce8b-163">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-163">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="2ce8b-164">您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-164">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="2ce8b-165">Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-165">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="2ce8b-166">您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-166">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="2ce8b-167">如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-167">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>

7. <span data-ttu-id="2ce8b-168">完成後，按一下**清除測試容錯移轉**hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-168">After you finish, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="2ce8b-169">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-169">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="2ce8b-170">這將刪除測試容錯移轉期間所建立的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-170">This will delete hello VMs that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2ce8b-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ce8b-171">Next steps</span></span>

- <span data-ttu-id="2ce8b-172">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-172">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="2ce8b-173">如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-173">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="2ce8b-174">[閱讀 容錯回復](site-recovery-failback-azure-to-vmware.md)，toofail 回和複寫的 Azure Vm 回 toohello 內部主要站台。</span><span class="sxs-lookup"><span data-stu-id="2ce8b-174">[Read about failback](site-recovery-failback-azure-to-vmware.md), toofail back and replicate Azure VMs back toohello primary on-premises site.</span></span>
