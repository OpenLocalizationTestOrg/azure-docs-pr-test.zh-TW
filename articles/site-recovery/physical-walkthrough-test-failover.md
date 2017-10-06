---
title: "測試容錯移轉的 Azure Site recovery 的實體伺服器複寫 tooAzure aaaRun |Microsoft 文件"
description: "摘要說明 hello 步驟，您需要執行測試容錯移轉 [實體伺服器複寫 tooAzure 使用 hello Azure Site Recovery 服務。"
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
ms.openlocfilehash: f8ed5ce585c5574be3018ce15339c4fd3b527eaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-tooazure"></a><span data-ttu-id="6b702-103">步驟 11： 執行測試容錯移轉的實體伺服器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b702-103">Step 11: Run a test failover of physical servers tooAzure</span></span>

<span data-ttu-id="6b702-104">本文說明如何 toorun 測試容錯移轉從內部部署實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="6b702-104">This article describes how toorun a test failover from on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="6b702-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="6b702-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="6b702-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="6b702-106">Before you start</span></span>

<span data-ttu-id="6b702-107">執行測試容錯移轉，我們建議您確認 hello 伺服器屬性，並進行任何變更之前，您需要。</span><span class="sxs-lookup"><span data-stu-id="6b702-107">Before you run a test failover we recommend that you verify hello server properties, and make any changes you need to.</span></span> <span data-ttu-id="6b702-108">您可以存取在 hello VM 屬性**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="6b702-108">you can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="6b702-109">hello **Essentials**刀鋒視窗會顯示電腦的設定狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="6b702-109">hello **Essentials** blade shows information about machine settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="6b702-110">受控磁碟的考量</span><span class="sxs-lookup"><span data-stu-id="6b702-110">Managed disk considerations</span></span>

<span data-ttu-id="6b702-111">[管理磁碟](../virtual-machines/windows/managed-disks-overview.md)管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure Vm 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="6b702-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing hello storage accounts associated with hello VM disks.</span></span> 

- <span data-ttu-id="6b702-112">當您啟用保護的伺服器時，VM 資料會複寫 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b702-112">When you enable protection for a server, VM data replicates tooa storage account.</span></span> <span data-ttu-id="6b702-113">受管理的磁碟建立並附加 toohello VM，只會容錯移轉發生時。</span><span class="sxs-lookup"><span data-stu-id="6b702-113">Managed disks are created and attached toohello VM only when failover occurs.</span></span>
- <span data-ttu-id="6b702-114">受管理的磁碟只可以建立 Azure Vm 部署使用 hello 資源管理員模型。</span><span class="sxs-lookup"><span data-stu-id="6b702-114">Managed disks can be created only for Azure VMs deployed using hello Resource Manager model.</span></span>  
- <span data-ttu-id="6b702-115">啟用此設定時，只有將 [使用受控磁碟] 啟用的資源群組之可用性設定組可供選取。</span><span class="sxs-lookup"><span data-stu-id="6b702-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="6b702-116">受管理的磁碟的 Vm 必須在可用性設定組與**使用受管理磁碟**設定得**是**。</span><span class="sxs-lookup"><span data-stu-id="6b702-116">VMs with managed disks must be in availability sets with **Use managed disks** set too**Yes**.</span></span> <span data-ttu-id="6b702-117">如果 Vm 未啟用 hello 設定，則可以選取只可用性集資源群組中而不會啟用受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6b702-117">If hello setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="6b702-118">[深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)受控磁碟和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="6b702-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="6b702-119">如果 hello 複寫所使用的儲存體帳戶與儲存體服務加密已加密，不能在容錯移轉期間建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6b702-119">If hello storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="6b702-120">在此情況下可能是不允許使用受管理的磁碟，或停用保護 hello VM，然後將它重新啟用 toouse 沒有加密已啟用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b702-120">In this case either don't enable use of managed disks, or disable protection for hello VM, and reenable it toouse a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="6b702-121">[深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="6b702-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="6b702-122">網路考量事項</span><span class="sxs-lookup"><span data-stu-id="6b702-122">Network considerations</span></span>

<span data-ttu-id="6b702-123">您可以建立容錯移轉後的 Azure vm 中設定 hello 目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b702-123">You can set hello target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="6b702-124">如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="6b702-124">If you don't provide an address, hello failed over machine will use DHCP.</span></span>
- <span data-ttu-id="6b702-125">如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="6b702-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="6b702-126">相同的目標 IP 位址可用於測試容錯移轉，若 hello 位址 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="6b702-126">hello same target IP address can be used for test failover, if hello address is available in hello test failover network.</span></span>
- <span data-ttu-id="6b702-127">網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：</span><span class="sxs-lookup"><span data-stu-id="6b702-127">hello number of network adapters is dictated by hello size you specify for hello target virtual machine:</span></span>

     - <span data-ttu-id="6b702-128">如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標必須 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="6b702-128">If hello number of network adapters on hello source machine is hello same as, or less than, hello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     - <span data-ttu-id="6b702-129">如果 hello hello 來源虛擬機器介面卡的數目超過允許 hello 目標大小，hello 數目 hello 目標大小最大值則會使用。</span><span class="sxs-lookup"><span data-stu-id="6b702-129">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size, then hello target size maximum will be used.</span></span>
     - <span data-ttu-id="6b702-130">例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="6b702-130">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="6b702-131">如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。</span><span class="sxs-lookup"><span data-stu-id="6b702-131">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="6b702-132">如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="6b702-132">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
   - <span data-ttu-id="6b702-133">如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="6b702-133">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>
 - <span data-ttu-id="6b702-134">[深入了解](vmware-walkthrough-network.md) IP 位址指定。</span><span class="sxs-lookup"><span data-stu-id="6b702-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="6b702-135">檢視及修改 VM 設定</span><span class="sxs-lookup"><span data-stu-id="6b702-135">View and modify VM settings</span></span>

<span data-ttu-id="6b702-136">我們建議您執行容錯移轉之前，確認 hello 來源伺服器的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6b702-136">We recommend that you verify hello properties of hello source server before you run a failover.</span></span>

1. <span data-ttu-id="6b702-137">在**受保護項目**，按一下 **複寫的項目**，，按一下 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="6b702-137">In **Protected Items**, click **Replicated Items**, and click hello machine.</span></span>
2. <span data-ttu-id="6b702-138">在 [hello**複寫項目**] 窗格中，您可以看到電腦資訊、 健全狀況狀態，以及最新可用的復原點 hello 的摘要。</span><span class="sxs-lookup"><span data-stu-id="6b702-138">In hello **Replicated item** pane, you can see a summary of machine information, health status, and hello latest available recovery points.</span></span> <span data-ttu-id="6b702-139">按一下**屬性**tooview 更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6b702-139">Click **Properties** tooview more details.</span></span>
3. <span data-ttu-id="6b702-140">在 [計算與網路] 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="6b702-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="6b702-141">修改 hello Azure VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6b702-141">Modify hello Azure VM name.</span></span> <span data-ttu-id="6b702-142">hello 名稱必須符合[Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="6b702-142">hello name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="6b702-143">指定容錯移轉後的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="6b702-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="6b702-144">指定 hello Azure VM 的目標大小</span><span class="sxs-lookup"><span data-stu-id="6b702-144">Specify a target size for hello Azure VM</span></span>
    - <span data-ttu-id="6b702-145">選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="6b702-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="6b702-146">指定是否 toouse[管理磁碟](#managed-disk-considerations)。</span><span class="sxs-lookup"><span data-stu-id="6b702-146">Specify whether toouse [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="6b702-147">選取**是**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="6b702-147">Select **Yes**, if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span>
    - <span data-ttu-id="6b702-148">檢視或修改網路設定，包括 hello 網路/子網路中的 hello Azure VM 將會位於容錯移轉之後，以及要指派 tooit hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b702-148">View or modify network settings, including hello network/subnet in which hello Azure VM will be located after failover, and hello IP address that will be assigned tooit.</span></span>
4. <span data-ttu-id="6b702-149">在**磁碟**、 您可以看到 hello 作業系統的相關資訊和資料磁碟上的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="6b702-149">In **Disks**, you can see information about hello operating system and data disks on hello VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="6b702-150">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="6b702-150">Run a test failover</span></span>

<span data-ttu-id="6b702-151">您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="6b702-151">After you've set everything up, run a test failover toomake sure everything's working as expected.</span></span>

- <span data-ttu-id="6b702-152">如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="6b702-152">If you want tooconnect tooAzure VMs using RDP after failover, [prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="6b702-153">您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。</span><span class="sxs-lookup"><span data-stu-id="6b702-153">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="6b702-154">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="6b702-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="6b702-155">如需有關測試容錯移轉的完整資訊，請參閱[這篇文章](site-recovery-test-failover-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="6b702-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="6b702-156">在開始之前，請透過影片快速建立概念︰</span><span class="sxs-lookup"><span data-stu-id="6b702-156">Get a quick video overview before you start:</span></span>

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

<span data-ttu-id="6b702-157">現在，請執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="6b702-157">Now, run a failover:</span></span>

1. <span data-ttu-id="6b702-158">透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello 機器 > **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="6b702-158">toofail over a single machine, in **Settings** > **Replicated Items**, click hello machine > **+Test Failover** icon.</span></span>

    ![測試容錯移轉](./media/physical-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="6b702-160">toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="6b702-160">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="6b702-161">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="6b702-161">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="6b702-162">在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="6b702-162">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="6b702-163">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6b702-163">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="6b702-164">您可以追蹤進度，藉由按 hello 機器 tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="6b702-164">You can track progress by clicking on hello machine tooopen its properties, or on hello **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="6b702-165">Hello 容錯移轉完成之後，您也應該要能夠 toosee hello 複本 hello Azure 入口網站中出現的 Azure VM >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="6b702-165">After hello failover completes, you should also be able toosee hello replica Azure VM appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="6b702-166">您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="6b702-166">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="6b702-167">如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="6b702-167">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>

### <a name="delete-test-failover-vms"></a><span data-ttu-id="6b702-168">刪除測試容錯移轉 VM</span><span class="sxs-lookup"><span data-stu-id="6b702-168">Delete test failover VMs</span></span>

1. <span data-ttu-id="6b702-169">完成後，按一下**清除測試容錯移轉**hello 復原計劃或電腦上。</span><span class="sxs-lookup"><span data-stu-id="6b702-169">After you finish, click on **Cleanup test failover** on hello recovery plan or machine.</span></span>
2. <span data-ttu-id="6b702-170">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="6b702-170">In **Notes**, record and save any observations associated with hello test failover.</span></span>
3. <span data-ttu-id="6b702-171">hello 清理動作會刪除在測試容錯移轉期間所建立的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="6b702-171">hello cleanup action deletes Azure VMs that were created during test failover.</span></span>

## <a name="summary"></a><span data-ttu-id="6b702-172">摘要</span><span class="sxs-lookup"><span data-stu-id="6b702-172">Summary</span></span>

<span data-ttu-id="6b702-173">如果您已成功完成 hello 測試容錯移轉，複寫您的實體伺服器，並在您檢查，可以在容錯移轉 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6b702-173">If you completed hello test failover successfully, your physical servers are replicating and you've checked that they can fail over tooAzure.</span></span> <span data-ttu-id="6b702-174">現在，您可以根據您的組織需求來執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6b702-174">Now, you can run failovers in accordance with your organizational requirements.</span></span> 

<span data-ttu-id="6b702-175">請記住，您目前無法無法從 Azure tooa 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="6b702-175">Remember that you can't currently fail back from Azure tooa physical server.</span></span> <span data-ttu-id="6b702-176">您有 toofail 回 tooa VMware VM。</span><span class="sxs-lookup"><span data-stu-id="6b702-176">You have toofail back tooa VMware VM.</span></span> <span data-ttu-id="6b702-177">這表示您需要在順序 toofail 回在內部部署 VMware 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="6b702-177">This means you need an on-premises VMware infrastructure in order toofail back.</span></span> <span data-ttu-id="6b702-178">[進一步了解](site-recovery-failback-azure-to-vmware.md)有關失敗後的 Azure Vm tooVMware。</span><span class="sxs-lookup"><span data-stu-id="6b702-178">[Learn more](site-recovery-failback-azure-to-vmware.md) about failing back Azure VMs tooVMware.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b702-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b702-179">Next steps</span></span>

- <span data-ttu-id="6b702-180">視需要[執行容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="6b702-180">[Run failovers](site-recovery-failover.md) as needed.</span></span>
