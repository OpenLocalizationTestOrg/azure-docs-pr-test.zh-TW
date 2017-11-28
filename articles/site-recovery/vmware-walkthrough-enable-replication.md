---
title: "使用 Azure Site Recovery 來啟用將 VMware VM 複寫至 Azure 的複寫功能 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務來啟用將 VMware VM 複寫至 Azure 的複寫功能時所需的步驟"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 470b9ddd8df4a4e74ec7174f79020c252323e502
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-to-azure"></a><span data-ttu-id="67452-103">步驟 11：啟用將 VMware 虛擬機器複寫至 Azure 的複寫功能</span><span class="sxs-lookup"><span data-stu-id="67452-103">Step 11: Enable replication for VMware virtual machines to Azure</span></span>


<span data-ttu-id="67452-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，來啟用將內部部署 VMware 虛擬機器複寫至 Azure 的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="67452-104">This article describes how to enable replication for on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="67452-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="67452-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="67452-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="67452-106">Before you start</span></span>

- <span data-ttu-id="67452-107">VMware VM 必須[已安裝行動服務元件](vmware-walkthrough-install-mobility.md)。</span><span class="sxs-lookup"><span data-stu-id="67452-107">VMware VMs must have the [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="67452-108">- 如果 VM 已針對推入安裝做好準備，當您啟用複寫時，處理伺服器就會自動安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="67452-108">- If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="67452-109">您的 Azure 使用者帳戶必須具有特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能將 VM 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="67452-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a VM to Azure</span></span>
- <span data-ttu-id="67452-110">當您新增或修改 VM 時，可能需要 15 分鐘或更久，變更才會生效，也才會出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="67452-110">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>
- <span data-ttu-id="67452-111">您可以在 [設定伺服器] > [上次連絡時間] 中，查看上次探索 VM 的時間。</span><span class="sxs-lookup"><span data-stu-id="67452-111">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="67452-112">若要新增 VM 而不等候已排定的探索，請醒目提示設定伺服器 (不要按一下)，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="67452-112">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="67452-113">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="67452-113">Exclude disks from replication</span></span>

<span data-ttu-id="67452-114">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="67452-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="67452-115">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="67452-115">You can exclude disks from replication.</span></span> <span data-ttu-id="67452-116">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次機器或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="67452-116">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="67452-117">深入了解</span><span class="sxs-lookup"><span data-stu-id="67452-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="67452-118">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="67452-118">Replicate VMs</span></span>

<span data-ttu-id="67452-119">在開始之前，請觀看快速的影片概觀</span><span class="sxs-lookup"><span data-stu-id="67452-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="67452-120">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="67452-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="67452-121">在 [來源] 中，選取設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="67452-121">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="67452-122">在 [機器類型] 中，選取 [虛擬機器]</span><span class="sxs-lookup"><span data-stu-id="67452-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="67452-123">在 [vCenter/vSphere Hypervisor] 中，選取管理 vSphere 主機的 vCenter 伺服器，或選取主機。</span><span class="sxs-lookup"><span data-stu-id="67452-123">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span>
5. <span data-ttu-id="67452-124">選取處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="67452-124">Select the process server.</span></span> <span data-ttu-id="67452-125">如果您尚未建立任何額外的處理序伺服器，則這會成為設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="67452-125">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="67452-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="67452-126">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="67452-128">在 [目標] 中，選取您想要在其中建立容錯移轉 VM 的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="67452-128">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="67452-129">選擇您想要在 Azure (傳統或資源管理) 中，針對容錯移轉 VM 使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="67452-129">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>


7. <span data-ttu-id="67452-130">選取您要用來複寫資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="67452-130">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="67452-131">如果您不想要使用已設定的帳戶，您可以建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="67452-131">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="67452-132">選取 Azure VM 在容錯移轉後啟動時所要建立的 Azure 網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="67452-132">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="67452-133">選取 [立即設定選取的機器]，將網路設定套用至您選取要進行保護的所有機器。</span><span class="sxs-lookup"><span data-stu-id="67452-133">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="67452-134">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="67452-134">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="67452-135">如果您不想使用現有的網路，您可以建立網路。</span><span class="sxs-lookup"><span data-stu-id="67452-135">If you don't want to use an existing network, you can create one.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="67452-137">在 [虛擬機器] > [選取虛擬機器] 中，按一下並選取您要複寫的每部機器。</span><span class="sxs-lookup"><span data-stu-id="67452-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="67452-138">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="67452-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="67452-139">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="67452-139">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="67452-141">在 [名稱]  > 中，選取處理序伺服器將用來在機器上自動安裝行動服務的帳戶。</span><span class="sxs-lookup"><span data-stu-id="67452-141">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="67452-142">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="67452-142">By default all disks are replicated.</span></span> <span data-ttu-id="67452-143">按一下 [所有磁碟]  ，然後將任何您不想要複寫的磁碟取消選取。</span><span class="sxs-lookup"><span data-stu-id="67452-143">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="67452-144">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="67452-144">Then click **OK**.</span></span> <span data-ttu-id="67452-145">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="67452-145">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="67452-147">在 [複寫設定] > [設定複寫設定] 中，確認已選取正確的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="67452-147">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="67452-148">如果您修改原則，變更會套用至複寫電腦及新的電腦。</span><span class="sxs-lookup"><span data-stu-id="67452-148">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="67452-149">如果您想要將機器聚集成一個複寫群組，請啟用 [多部 VM 一致性]  ，並指定群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="67452-149">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="67452-150">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="67452-150">Then click **OK**.</span></span> <span data-ttu-id="67452-151">請注意：</span><span class="sxs-lookup"><span data-stu-id="67452-151">Note that:</span></span>

    * <span data-ttu-id="67452-152">複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="67452-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="67452-153">我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="67452-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="67452-154">啟用多部 VM 一致性可能會影響工作負載的效能，應該只用於機器正在執行相同工作負載，且您需要一致性的情況。</span><span class="sxs-lookup"><span data-stu-id="67452-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="67452-156">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="67452-156">Click **Enable Replication**.</span></span> <span data-ttu-id="67452-157">您可以在 [設定]  >  [作業]  >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="67452-157">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="67452-158">執行 [完成保護]  作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67452-158">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67452-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67452-159">Next steps</span></span>

<span data-ttu-id="67452-160">移至[步驟 12：執行測試容錯移轉](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="67452-160">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
