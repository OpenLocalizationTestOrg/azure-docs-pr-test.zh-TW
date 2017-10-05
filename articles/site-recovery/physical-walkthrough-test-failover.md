---
title: "使用 Azure Site Recovery 來執行將實體伺服器複寫至 Azure 的測試容錯移轉 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務來執行將實體伺服器複寫至 Azure 之測試容錯移轉所需的步驟。"
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
ms.openlocfilehash: 94aa3bfc700cad3de9fc5516c0c9a4d86ade3fed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-to-azure"></a><span data-ttu-id="98b3c-103">步驟 11：執行實體伺服器至 Azure 的測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="98b3c-103">Step 11: Run a test failover of physical servers to Azure</span></span>

<span data-ttu-id="98b3c-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，來執行從內部部署實體伺服器至 Azure 的測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="98b3c-104">This article describes how to run a test failover from on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="98b3c-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="98b3c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="98b3c-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="98b3c-106">Before you start</span></span>

<span data-ttu-id="98b3c-107">在您執行測試容錯移轉之前，建議您確認伺服器屬性，並進行任何需要的變更。</span><span class="sxs-lookup"><span data-stu-id="98b3c-107">Before you run a test failover we recommend that you verify the server properties, and make any changes you need to.</span></span> <span data-ttu-id="98b3c-108">您可以在 [複寫的項目] 中存取 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="98b3c-108">you can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="98b3c-109">[程式集] 刀鋒視窗會顯示機器設定與狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="98b3c-109">The **Essentials** blade shows information about machine settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="98b3c-110">受控磁碟的考量</span><span class="sxs-lookup"><span data-stu-id="98b3c-110">Managed disk considerations</span></span>

<span data-ttu-id="98b3c-111">[受控磁碟](../virtual-machines/windows/managed-disks-overview.md)可透過管理與 VM 磁碟關聯的儲存體帳戶，來簡化 Azure VM 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="98b3c-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing the storage accounts associated with the VM disks.</span></span> 

- <span data-ttu-id="98b3c-112">當您為伺服器啟用保護時，VM 資料會複寫到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="98b3c-112">When you enable protection for a server, VM data replicates to a storage account.</span></span> <span data-ttu-id="98b3c-113">只有在發生容錯移轉時，才會建立受控磁碟並將它們連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="98b3c-113">Managed disks are created and attached to the VM only when failover occurs.</span></span>
- <span data-ttu-id="98b3c-114">只有針對使用 Resource Manager 模型來部署的 Azure VM，才能建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="98b3c-114">Managed disks can be created only for Azure VMs deployed using the Resource Manager model.</span></span>  
- <span data-ttu-id="98b3c-115">在啟用此設定的情況下，只能選取「資源群組」中已啟用 [使用受控磁碟] 的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="98b3c-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="98b3c-116">具有受控磁碟的 VM 必須位於 [使用受控磁碟] 設定為 [是] 的可用性群組中。</span><span class="sxs-lookup"><span data-stu-id="98b3c-116">VMs with managed disks must be in availability sets with **Use managed disks** set to **Yes**.</span></span> <span data-ttu-id="98b3c-117">如果沒有為 VM 啟用此設定，則只能選取「資源群組」中未啟用受控磁碟的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="98b3c-117">If the setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="98b3c-118">[深入了解](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)受控磁碟和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="98b3c-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="98b3c-119">如果您用於複寫的儲存體帳戶已使用「儲存體服務加密」進行加密，在容錯移轉期間便無法建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="98b3c-119">If the storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="98b3c-120">在此情況下，請不要啟用使用受控磁碟的功能，或是停用 VM 保護，然後再將它重新啟用，以使用未啟用加密的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="98b3c-120">In this case either don't enable use of managed disks, or disable protection for the VM, and reenable it to use a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="98b3c-121">[深入了解](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="98b3c-122">網路考量</span><span class="sxs-lookup"><span data-stu-id="98b3c-122">Network considerations</span></span>

<span data-ttu-id="98b3c-123">您可以為在容錯移轉後建立的 Azure VM 設定目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="98b3c-123">You can set the target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="98b3c-124">如果您未提供地址，則容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="98b3c-124">If you don't provide an address, the failed over machine will use DHCP.</span></span>
- <span data-ttu-id="98b3c-125">如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="98b3c-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="98b3c-126">如果相同的目標 IP 位址在測試容錯移轉網路中可用，則此位址可用於測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="98b3c-126">The same target IP address can be used for test failover, if the address is available in the test failover network.</span></span>
- <span data-ttu-id="98b3c-127">網路介面卡的數目會視您指定給目標虛擬機器的大小而有所不同：</span><span class="sxs-lookup"><span data-stu-id="98b3c-127">The number of network adapters is dictated by the size you specify for the target virtual machine:</span></span>

     - <span data-ttu-id="98b3c-128">如果來源電腦上的網路介面卡數目等於或小於針對目標電腦大小所允許的介面卡數目，則目標將具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="98b3c-128">If the number of network adapters on the source machine is the same as, or less than, the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
     - <span data-ttu-id="98b3c-129">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則將使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="98b3c-129">If the number of adapters for the source virtual machine exceeds the number allowed for the target size, then the target size maximum will be used.</span></span>
     - <span data-ttu-id="98b3c-130">例如，如果來源機器具有兩張網路介面卡，而目標機器大小支援四張，則目標機器將會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="98b3c-130">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="98b3c-131">如果來源機器具有兩張介面卡，但支援的目標大小僅支援一張，則目標機器將只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="98b3c-131">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="98b3c-132">如果虛擬機器有多張網路介面卡，則全部會連接至相同的網路。</span><span class="sxs-lookup"><span data-stu-id="98b3c-132">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
   - <span data-ttu-id="98b3c-133">如果虛擬機器具有多個網路介面卡，則清單中顯示的第一個會變成 Azure 虛擬機器中的*預設*網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="98b3c-133">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>
 - <span data-ttu-id="98b3c-134">[深入了解](vmware-walkthrough-network.md) IP 位址指定。</span><span class="sxs-lookup"><span data-stu-id="98b3c-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="98b3c-135">檢視及修改 VM 設定</span><span class="sxs-lookup"><span data-stu-id="98b3c-135">View and modify VM settings</span></span>

<span data-ttu-id="98b3c-136">建議您在執行容錯移轉之前，先確認來源伺服器的屬性。</span><span class="sxs-lookup"><span data-stu-id="98b3c-136">We recommend that you verify the properties of the source server before you run a failover.</span></span>

1. <span data-ttu-id="98b3c-137">在 [受保護的項目] 中，按一下 [複寫的項目]，然後按一下機器。</span><span class="sxs-lookup"><span data-stu-id="98b3c-137">In **Protected Items**, click **Replicated Items**, and click the machine.</span></span>
2. <span data-ttu-id="98b3c-138">在 [複寫的項目] 窗格中，您可以看到機器資訊、健康情況狀態及最新可用復原點的摘要。</span><span class="sxs-lookup"><span data-stu-id="98b3c-138">In the **Replicated item** pane, you can see a summary of machine information, health status, and the latest available recovery points.</span></span> <span data-ttu-id="98b3c-139">若要檢視其他詳細資料，請按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="98b3c-139">Click **Properties** to view more details.</span></span>
3. <span data-ttu-id="98b3c-140">在 [計算與網路] 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="98b3c-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="98b3c-141">修改 Azure VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="98b3c-141">Modify the Azure VM name.</span></span> <span data-ttu-id="98b3c-142">名稱必須符合 [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-142">The name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="98b3c-143">指定容錯移轉後的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="98b3c-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="98b3c-144">指定 Azure VM 的目標大小</span><span class="sxs-lookup"><span data-stu-id="98b3c-144">Specify a target size for the Azure VM</span></span>
    - <span data-ttu-id="98b3c-145">選取[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="98b3c-146">指定是否要使用[受控磁碟](#managed-disk-considerations)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-146">Specify whether to use [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="98b3c-147">如果您想要將受控磁碟連結到您移轉至 Azure 的機器上，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="98b3c-147">Select **Yes**, if you want to attach managed disks to your machine on migration to Azure.</span></span>
    - <span data-ttu-id="98b3c-148">檢視或修改網路設定，包括在容錯移轉後 Azure VM 將位於的網路/子網路，以及要指派給它的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="98b3c-148">View or modify network settings, including the network/subnet in which the Azure VM will be located after failover, and the IP address that will be assigned to it.</span></span>
4. <span data-ttu-id="98b3c-149">在 [磁碟] 中，您可以看見有關 VM 上作業系統和資料磁碟的資訊。</span><span class="sxs-lookup"><span data-stu-id="98b3c-149">In **Disks**, you can see information about the operating system and data disks on the VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="98b3c-150">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="98b3c-150">Run a test failover</span></span>

<span data-ttu-id="98b3c-151">一切就緒後，執行測試容錯移轉，確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="98b3c-151">After you've set everything up, run a test failover to make sure everything's working as expected.</span></span>

- <span data-ttu-id="98b3c-152">如果您想要在容錯移轉後使用 RDP 來連線到 Azure VM，請[準備連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-152">If you want to connect to Azure VMs using RDP after failover, [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="98b3c-153">若要完整測試，您需要在測試環境中將 Active Directory 和 DNS 進行複製。</span><span class="sxs-lookup"><span data-stu-id="98b3c-153">To fully test you need to copy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="98b3c-154">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="98b3c-155">如需有關測試容錯移轉的完整資訊，請參閱[這篇文章](site-recovery-test-failover-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="98b3c-156">在開始之前，請透過影片快速建立概念︰</span><span class="sxs-lookup"><span data-stu-id="98b3c-156">Get a quick video overview before you start:</span></span>

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

<span data-ttu-id="98b3c-157">現在，請執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="98b3c-157">Now, run a failover:</span></span>

1. <span data-ttu-id="98b3c-158">若要容錯移轉單一機器，請在 [設定] > [複寫的項目] 中，按一下該機器 > [+測試容錯移轉] 圖示。</span><span class="sxs-lookup"><span data-stu-id="98b3c-158">To fail over a single machine, in **Settings** > **Replicated Items**, click the machine > **+Test Failover** icon.</span></span>

    ![測試容錯移轉](./media/physical-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="98b3c-160">若要容錯移轉復原方案，請在 [設定]  >  [復原方案] 中，以滑鼠右鍵按一下方案 > [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="98b3c-160">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="98b3c-161">若要建立復原方案，請[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-161">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="98b3c-162">在 [測試容錯移轉] 中，選取 Azure VM 在容錯移轉之後要連接的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="98b3c-162">In **Test Failover**, select the Azure network to which Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="98b3c-163">按一下 [確定]  即可開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="98b3c-163">Click **OK** to begin the failover.</span></span> <span data-ttu-id="98b3c-164">您可以按一下機器來開啟其屬性，或在保存庫名稱 > [設定] > [作業] > [Site Recovery 作業] 中的 [測試容錯移轉] 作業上按一下，來追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="98b3c-164">You can track progress by clicking on the machine to open its properties, or on the **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="98b3c-165">容錯移轉完成之後，您應該也會看到複本 Azure VM 出現在 Azure 入口網站 > [虛擬機器] 中。</span><span class="sxs-lookup"><span data-stu-id="98b3c-165">After the failover completes, you should also be able to see the replica Azure VM appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="98b3c-166">您應該確定 VM 為適當的大小、已連接到適當的網路，而且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="98b3c-166">You should make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="98b3c-167">如果您已準備好在容錯移轉後進行連線，應該能夠連線到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="98b3c-167">If you prepared for connections after failover, you should be able to connect to the Azure VM.</span></span>

### <a name="delete-test-failover-vms"></a><span data-ttu-id="98b3c-168">刪除測試容錯移轉 VM</span><span class="sxs-lookup"><span data-stu-id="98b3c-168">Delete test failover VMs</span></span>

1. <span data-ttu-id="98b3c-169">完成之後，在復原方案或機器上按一下 [清除測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="98b3c-169">After you finish, click on **Cleanup test failover** on the recovery plan or machine.</span></span>
2. <span data-ttu-id="98b3c-170">在 [記事] 中，記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="98b3c-170">In **Notes**, record and save any observations associated with the test failover.</span></span>
3. <span data-ttu-id="98b3c-171">此清除動作會刪除在測試容錯移轉期間建立的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="98b3c-171">The cleanup action deletes Azure VMs that were created during test failover.</span></span>

## <a name="summary"></a><span data-ttu-id="98b3c-172">摘要</span><span class="sxs-lookup"><span data-stu-id="98b3c-172">Summary</span></span>

<span data-ttu-id="98b3c-173">如果您已成功完成測試容錯移轉，即表示您的實體伺服器正在複寫，且您已確認它們能夠容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="98b3c-173">If you completed the test failover successfully, your physical servers are replicating and you've checked that they can fail over to Azure.</span></span> <span data-ttu-id="98b3c-174">現在，您可以根據您的組織需求來執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="98b3c-174">Now, you can run failovers in accordance with your organizational requirements.</span></span> 

<span data-ttu-id="98b3c-175">請記住，您目前無法從 Azure 容錯回復到實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="98b3c-175">Remember that you can't currently fail back from Azure to a physical server.</span></span> <span data-ttu-id="98b3c-176">您必須容錯回復到 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="98b3c-176">You have to fail back to a VMware VM.</span></span> <span data-ttu-id="98b3c-177">這意謂著您必須要有內部部署 VMware VM 基礎結構，才能容錯回復。</span><span class="sxs-lookup"><span data-stu-id="98b3c-177">This means you need an on-premises VMware infrastructure in order to fail back.</span></span> <span data-ttu-id="98b3c-178">[深入了解](site-recovery-failback-azure-to-vmware.md)將 Azure VM 容錯回復到 VMware。</span><span class="sxs-lookup"><span data-stu-id="98b3c-178">[Learn more](site-recovery-failback-azure-to-vmware.md) about failing back Azure VMs to VMware.</span></span>


## <a name="next-steps"></a><span data-ttu-id="98b3c-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98b3c-179">Next steps</span></span>

- <span data-ttu-id="98b3c-180">視需要[執行容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="98b3c-180">[Run failovers](site-recovery-failover.md) as needed.</span></span>
