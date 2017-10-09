---
title: "VMware vm 複寫與 Azure Site Recovery tooAzure aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要使用 hello Azure Site Recovery 服務的 VMware vm 的 tooenable 複寫 tooAzure hello 步驟"
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
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a><span data-ttu-id="fc0aa-103">步驟 11： 啟用複寫的 VMware 虛擬機器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="fc0aa-103">Step 11: Enable replication for VMware virtual machines tooAzure</span></span>


<span data-ttu-id="fc0aa-104">本文說明如何 tooenable 複寫在內部部署 vmware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-104">This article describes how tooenable replication for on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="fc0aa-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="fc0aa-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="fc0aa-106">Before you start</span></span>

- <span data-ttu-id="fc0aa-107">VMware Vm 必須有 hello[安裝行動服務元件](vmware-walkthrough-install-mobility.md)。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-107">VMware VMs must have hello [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="fc0aa-108">-如果 VM 已備妥進行推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-108">- If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="fc0aa-109">您的 Azure 使用者帳戶需要特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)VM tooAzure tooenable 複寫</span><span class="sxs-lookup"><span data-stu-id="fc0aa-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a VM tooAzure</span></span>
- <span data-ttu-id="fc0aa-110">當您加入或修改 Vm 時，可能需要向上 too15 分鐘或更久變更 tootake 效果，以及它們 tooappear hello 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-110">When you add or modify VMs, it can take up too15 minutes or longer for changes tootake effect, and for them tooappear in hello portal.</span></span>
- <span data-ttu-id="fc0aa-111">您可以檢查 hello 上次探索的時間中的 Vm**設定伺服器** > **上次連絡時間**。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-111">You can check hello last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="fc0aa-112">不需等到 hello 已排程的探索，反白顯示 hello 組態伺服器 tooadd Vm （但不要按），然後按一下**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-112">tooadd VMs without waiting for hello scheduled discovery, highlight hello configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="fc0aa-113">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="fc0aa-113">Exclude disks from replication</span></span>

<span data-ttu-id="fc0aa-114">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="fc0aa-115">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-115">You can exclude disks from replication.</span></span> <span data-ttu-id="fc0aa-116">例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-116">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="fc0aa-117">深入了解</span><span class="sxs-lookup"><span data-stu-id="fc0aa-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="fc0aa-118">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="fc0aa-118">Replicate VMs</span></span>

<span data-ttu-id="fc0aa-119">在開始之前，請觀看快速的影片概觀</span><span class="sxs-lookup"><span data-stu-id="fc0aa-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="fc0aa-120">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="fc0aa-121">在**來源**，選取 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-121">In **Source**, select hello configuration server.</span></span>
3. <span data-ttu-id="fc0aa-122">在 [機器類型] 中，選取 [虛擬機器]</span><span class="sxs-lookup"><span data-stu-id="fc0aa-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="fc0aa-123">在**vCenter vSphere Hypervisor**、 選取 hello vCenter 伺服器負責管理 hello vSphere 主機，或選取 hello 的主機。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-123">In **vCenter/vSphere Hypervisor**, select hello vCenter server that manages hello vSphere host, or select hello host.</span></span>
5. <span data-ttu-id="fc0aa-124">選取 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-124">Select hello process server.</span></span> <span data-ttu-id="fc0aa-125">如果您尚未建立任何額外的處理序伺服器，這會是 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-125">If you haven't created any additional process servers this will be hello configuration server.</span></span> <span data-ttu-id="fc0aa-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-126">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="fc0aa-128">在**目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉 Vm 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-128">In **Target**, select hello subscription and hello resource group in which you want toocreate hello failed over VMs.</span></span> <span data-ttu-id="fc0aa-129">選擇要容錯移轉 Vm hello toouse （classic 或資源管理），Azure 中的 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-129">Choose hello deployment model that you want toouse in Azure (classic or resource management), for hello failed over VMs.</span></span>


7. <span data-ttu-id="fc0aa-130">選取要用於複寫資料 toouse hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-130">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="fc0aa-131">如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-131">If you don't want toouse an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="fc0aa-132">在建立時即容錯移轉之後，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-132">Select hello Azure network and subnet toowhich Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="fc0aa-133">選取**現在選取的機器設定**，tooapply hello 網路設定 tooall 您選取的機器進行保護。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-133">Select **Configure now for selected machines**, tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="fc0aa-134">選取**稍後設定**tooselect hello 每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-134">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="fc0aa-135">如果您不想 toouse 現有網路，您可以建立一個。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-135">If you don't want toouse an existing network, you can create one.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="fc0aa-137">在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="fc0aa-138">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="fc0aa-139">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-139">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="fc0aa-141">在**屬性** > **設定屬性**，選取將由 hello 處理序伺服器 tooautomatically 的 hello 帳戶 hello 機器上安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-141">In **Properties** > **Configure properties**, select hello account that will be used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
11. <span data-ttu-id="fc0aa-142">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-142">By default all disks are replicated.</span></span> <span data-ttu-id="fc0aa-143">按一下**所有磁碟**並清除您不想 tooreplicate 任何磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-143">Click **All Disks** and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="fc0aa-144">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-144">Then click **OK**.</span></span> <span data-ttu-id="fc0aa-145">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-145">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="fc0aa-147">在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-147">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="fc0aa-148">如果您修改原則時，將變更套用的 tooreplicating 機器和 toonew 機器。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-148">If you modify a policy, changes will be applied tooreplicating machine, and toonew machines.</span></span>
12. <span data-ttu-id="fc0aa-149">啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-149">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="fc0aa-150">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-150">Then click **OK**.</span></span> <span data-ttu-id="fc0aa-151">請注意：</span><span class="sxs-lookup"><span data-stu-id="fc0aa-151">Note that:</span></span>

    * <span data-ttu-id="fc0aa-152">複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="fc0aa-153">我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="fc0aa-154">啟用多重 VM 一致性可能會影響工作負載的效能，應該只用於如果機器 hello 執行相同的工作負載，且需要一致性。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running hello same workload and you need consistency.</span></span>

    ![啟用複寫](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="fc0aa-156">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-156">Click **Enable Replication**.</span></span> <span data-ttu-id="fc0aa-157">您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.</span><span class="sxs-lookup"><span data-stu-id="fc0aa-157">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="fc0aa-158">之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="fc0aa-158">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc0aa-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc0aa-159">Next steps</span></span>

<span data-ttu-id="fc0aa-160">跳過[步驟 12： 執行測試容錯移轉](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="fc0aa-160">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
