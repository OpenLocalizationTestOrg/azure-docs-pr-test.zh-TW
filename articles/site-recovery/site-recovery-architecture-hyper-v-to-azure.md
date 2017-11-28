---
title: "在 Azure Site Recovery 中將 Hyper-V 複寫至 Azure 如何運作？ | Microsoft Docs"
description: "本文提供使用 Azure Site Recovery 服務將內部部署 Hyper-V VM 複寫至 Azure 時所用元件和架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 28f775afaf72b11eec0c22f755e4dbd6a485c895
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-hyper-v-replication-to-azure-work-in-site-recovery"></a><span data-ttu-id="59bf0-104">在 Site Recovery 中將 Hyper-V 複寫至 Azure 如何運作？</span><span class="sxs-lookup"><span data-stu-id="59bf0-104">How does Hyper-V replication to Azure work in Site Recovery?</span></span>


<span data-ttu-id="59bf0-105">本文說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 Hyper-V 虛擬機器複寫至 Azure 時的相關元件和程序。</span><span class="sxs-lookup"><span data-stu-id="59bf0-105">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="59bf0-106">Site Recovery 可以在 Hyper-V 叢集和獨立主機上，複寫不論是否使用 System Center Virtual Machine Manager (VMM) 管理的 Hyper-V VM。</span><span class="sxs-lookup"><span data-stu-id="59bf0-106">Site Recovery can replicate Hyper-V VMs on Hyper-V clusters and standalone hosts that are managed with or without System Center Virtual Machine Manager (VMM).</span></span>

<span data-ttu-id="59bf0-107">如有任何意見，請張貼於這篇文章下方或 [Azure 復原服務論壇 (英文)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中。</span><span class="sxs-lookup"><span data-stu-id="59bf0-107">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="59bf0-108">架構元件</span><span class="sxs-lookup"><span data-stu-id="59bf0-108">Architectural components</span></span>

<span data-ttu-id="59bf0-109">將 Hyper-V VM 複寫至 Azure 時，涉及許多元件。</span><span class="sxs-lookup"><span data-stu-id="59bf0-109">There are a number of components involved when replicating Hyper-V VMs to Azure.</span></span>

<span data-ttu-id="59bf0-110">**元件**</span><span class="sxs-lookup"><span data-stu-id="59bf0-110">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="59bf0-112">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="59bf0-112">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="59bf0-113">**Azure**</span><span class="sxs-lookup"><span data-stu-id="59bf0-113">**Azure**</span></span> | <span data-ttu-id="59bf0-114">在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="59bf0-114">In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network.</span></span> | <span data-ttu-id="59bf0-115">所複寫的資料會儲存在儲存體帳戶中，而在從內部部署網站進行容錯移轉時，便會以複寫的資料建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="59bf0-115">Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs.</span></span><br/><br/> <span data-ttu-id="59bf0-116">Azure VM 在建立後會連線到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="59bf0-116">The Azure VMs connect to the Azure virtual network when they're created.</span></span>
<span data-ttu-id="59bf0-117">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="59bf0-117">**VMM server**</span></span> | <span data-ttu-id="59bf0-118">位於 VMM 雲端的 Hyper-V 主機</span><span class="sxs-lookup"><span data-stu-id="59bf0-118">Hyper-V hosts are located in VMM clouds</span></span> | <span data-ttu-id="59bf0-119">如果 Hyper-V 主機是在 VMM 雲端中進行管理，您是在復原服務保存庫中註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="59bf0-119">If Hyper-V hosts are managed in VMM clouds, you register the VMM server in the Recovery Services vault.</span></span><br/><br/> <span data-ttu-id="59bf0-120">在 VMM 伺服器上安裝 Site Recovery Provider，以協調與 Azure 的複寫。</span><span class="sxs-lookup"><span data-stu-id="59bf0-120">On the VMM server you install the Site Recovery Provider to orchestrate replication with Azure.</span></span><br/><br/> <span data-ttu-id="59bf0-121">您需要邏輯和 VM 網路設定以設定網路對應。</span><span class="sxs-lookup"><span data-stu-id="59bf0-121">You need logical and VM networks set up to configure network mapping.</span></span> <span data-ttu-id="59bf0-122">VM 網路應該連結到與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="59bf0-122">A VM network should be linked to a logical network that's associated with the cloud.</span></span>
<span data-ttu-id="59bf0-123">**Hyper-V 主機**</span><span class="sxs-lookup"><span data-stu-id="59bf0-123">**Hyper-V host**</span></span> | <span data-ttu-id="59bf0-124">不論是否具有 VMM 伺服器，可以部署的 Hyper-V 主機和叢集。</span><span class="sxs-lookup"><span data-stu-id="59bf0-124">Hyper-V hosts and clusters can be deployed with or without VMM server.</span></span> | <span data-ttu-id="59bf0-125">如果沒有 VMM 伺服器，Site Recovery Provider 會安裝在主機上，以透過網際網路協調與 Site Recovery 的複寫。</span><span class="sxs-lookup"><span data-stu-id="59bf0-125">If there's no VMM server, the Site Recovery Provider is installed on the host to orchestrate replication with Site Recovery over the internet.</span></span> <span data-ttu-id="59bf0-126">如果有 VMM 伺服器，會在上面安裝 Provider，而不是在主機上安裝。</span><span class="sxs-lookup"><span data-stu-id="59bf0-126">If there's a VMM server, the Provider is installed on it, and not on the host.</span></span><br/><br/> <span data-ttu-id="59bf0-127">復原服務代理程式安裝在主機上以處理資料複寫。</span><span class="sxs-lookup"><span data-stu-id="59bf0-127">The Recovery Services agent is installed on the host to handle data replication.</span></span><br/><br/> <span data-ttu-id="59bf0-128">來自提供者和代理程式的通訊都是安全且加密的。</span><span class="sxs-lookup"><span data-stu-id="59bf0-128">Communications from both the Provider and the agent are secure and encrypted.</span></span> <span data-ttu-id="59bf0-129">Azure 儲存體中的複寫的資料也會加密。</span><span class="sxs-lookup"><span data-stu-id="59bf0-129">Replicated data in Azure storage is also encrypted.</span></span>
<span data-ttu-id="59bf0-130">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="59bf0-130">**Hyper-V VMs**</span></span> | <span data-ttu-id="59bf0-131">您必須有一或多部在 Hyper-V 主機伺服器上執行的 VM。</span><span class="sxs-lookup"><span data-stu-id="59bf0-131">You need one or more VMs running on a Hyper-V host server.</span></span> | <span data-ttu-id="59bf0-132">不需要在 VM 上明確安裝任何項目。</span><span class="sxs-lookup"><span data-stu-id="59bf0-132">Nothing needs to explicitly installed on VMs.</span></span>

<span data-ttu-id="59bf0-133">了解[支援矩陣](site-recovery-support-matrix-to-azure.md)中每個元件的部署必要條件和需求。</span><span class="sxs-lookup"><span data-stu-id="59bf0-133">Learn about the deployment prerequisites and requirements for each of these components in the [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>

<span data-ttu-id="59bf0-134">**圖 1：Hyper-V 網站至 Azure 的複寫**</span><span class="sxs-lookup"><span data-stu-id="59bf0-134">**Figure 1: Hyper-V site to Azure replication**</span></span>

![元件](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

<span data-ttu-id="59bf0-136">**圖 2：VMM 雲端中之 Hyper-V 至 Azure 的複寫**</span><span class="sxs-lookup"><span data-stu-id="59bf0-136">**Figure 2: Hyper-V in VMM clouds to Azure replication**</span></span>

![元件](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a><span data-ttu-id="59bf0-138">複寫程序</span><span class="sxs-lookup"><span data-stu-id="59bf0-138">Replication process</span></span>

<span data-ttu-id="59bf0-139">**圖 3：Hyper-V 複寫至 Azure 的複寫和復原程序**</span><span class="sxs-lookup"><span data-stu-id="59bf0-139">**Figure 3: Replication and recovery process for Hyper-V replication to Azure**</span></span>

![工作流程](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a><span data-ttu-id="59bf0-141">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="59bf0-141">Enable protection</span></span>

1. <span data-ttu-id="59bf0-142">您在 Azure 入口網站或內部部署針對 Hyper-V VM 啟用保護之後，**啟用保護**隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="59bf0-142">After you enable protection for a Hyper-V VM, in the Azure portal or on-premises, the **Enable protection** starts.</span></span>
2. <span data-ttu-id="59bf0-143">作業會檢查符合必要條件的機器，然後叫用 [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx) 方法，以使用您進行的設定來設定複寫。</span><span class="sxs-lookup"><span data-stu-id="59bf0-143">The job checks that the machine complies with prerequisites, before invoking the [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), to set up replication with the settings you've configured.</span></span>
3. <span data-ttu-id="59bf0-144">作業會啟動初始複寫，方法是叫用 [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) 方法，以初始化完整的 VM 複寫，並且將 VM 的虛擬磁碟傳送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="59bf0-144">The job starts initial replication by invoking the [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) method, to initialize a full VM replication, and send the VM's virtual disks to Azure.</span></span>
4. <span data-ttu-id="59bf0-145">您可以在 [作業] 索引標籤中監視作業。</span><span class="sxs-lookup"><span data-stu-id="59bf0-145">You can monitor the job in the **Jobs** tab.</span></span>
        <span data-ttu-id="59bf0-146">![作業清單](media/site-recovery-hyper-v-azure-architecture/image1.png) ![啟用保護向下鑽研](media/site-recovery-hyper-v-azure-architecture/image2.png)</span><span class="sxs-lookup"><span data-stu-id="59bf0-146">![Jobs list](media/site-recovery-hyper-v-azure-architecture/image1.png) ![Enable protection drill down](media/site-recovery-hyper-v-azure-architecture/image2.png)</span></span>

### <a name="replicate-the-initial-data"></a><span data-ttu-id="59bf0-147">複寫初始資料</span><span class="sxs-lookup"><span data-stu-id="59bf0-147">Replicate the initial data</span></span>

1. <span data-ttu-id="59bf0-148">系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-148">A [Hyper-V VM snapshot](https://technet.microsoft.com/library/dd560637.aspx) snapshot is taken when initial replication is triggered.</span></span>
2. <span data-ttu-id="59bf0-149">虛擬硬碟會逐一複寫，直到它們全部複製到 Azure 為止。</span><span class="sxs-lookup"><span data-stu-id="59bf0-149">Virtual hard disks are replicated one by one until they're all copied to Azure.</span></span> <span data-ttu-id="59bf0-150">可能需要一些時間，取決於 VM 大小和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="59bf0-150">It could take a while, depending on the VM size, and network bandwidth.</span></span> <span data-ttu-id="59bf0-151">若要將網路使用量最佳化，請參閱 [如何管理內部部署至 Azure 保護的網路頻寬使用量](https://support.microsoft.com/kb/3056159)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-151">To optimize your network usage, see [How to manage on-premises to Azure protection network bandwidth usage](https://support.microsoft.com/kb/3056159).</span></span>
3. <span data-ttu-id="59bf0-152">如果在初始複寫進行時發生磁碟變更，Hyper-V 複本複寫追蹤器會以 Hyper-V 複寫記錄檔 (.hrl) 的形式追蹤這些變更。</span><span class="sxs-lookup"><span data-stu-id="59bf0-152">If disk changes occur while initial replication is in progress, the Hyper-V Replica Replication Tracker tracks those changes as Hyper-V Replication Logs (.hrl).</span></span> <span data-ttu-id="59bf0-153">這些記錄檔位於與磁碟相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="59bf0-153">These files are located in the same folder as the disks.</span></span> <span data-ttu-id="59bf0-154">每個磁碟都有一個相關聯的.hrl 檔案，將會傳送至次要儲存體。</span><span class="sxs-lookup"><span data-stu-id="59bf0-154">Each disk has an associated .hrl file that will be sent to secondary storage.</span></span>
4. <span data-ttu-id="59bf0-155">當初始複寫正在進行時，快照和記錄檔會取用磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="59bf0-155">The snapshot and log files consume disk resources while initial replication is in progress.</span></span>
5. <span data-ttu-id="59bf0-156">初始複寫完成時，就會刪除 VM 快照集。</span><span class="sxs-lookup"><span data-stu-id="59bf0-156">When the initial replication finishes, the VM snapshot is deleted.</span></span> <span data-ttu-id="59bf0-157">記錄中的差異磁碟變更會同步處理，並合併到父磁碟。</span><span class="sxs-lookup"><span data-stu-id="59bf0-157">Delta disk changes in the log are synchronized and merged to the parent disk.</span></span>


### <a name="finalize-protection"></a><span data-ttu-id="59bf0-158">完成保護</span><span class="sxs-lookup"><span data-stu-id="59bf0-158">Finalize protection</span></span>

1. <span data-ttu-id="59bf0-159">初始複寫完成之後，**在虛擬機器上完成保護**作業會設定網路和其他複寫後設定，如此就能讓虛擬機器受到保護。</span><span class="sxs-lookup"><span data-stu-id="59bf0-159">After the initial replication finishes, the **Finalize protection on the virtual machine** job configures network and other post-replication settings, so that the virtual machine is protected.</span></span>
    <span data-ttu-id="59bf0-160">![完成保護作業](media/site-recovery-hyper-v-azure-architecture/image3.png)</span><span class="sxs-lookup"><span data-stu-id="59bf0-160">![Finalize protection job](media/site-recovery-hyper-v-azure-architecture/image3.png)</span></span>
2. <span data-ttu-id="59bf0-161">如果您要複寫至 Azure，您可能需要調整虛擬機器的設定，使其準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="59bf0-161">If you're replicating to Azure, you might need to tweak the settings for the virtual machine so that it's ready for failover.</span></span> <span data-ttu-id="59bf0-162">此時，您可以執行測試容錯移轉，以確認一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="59bf0-162">At this point you can run a test failover to check everything is working as expected.</span></span>

### <a name="replicate-the-delta"></a><span data-ttu-id="59bf0-163">複寫差異</span><span class="sxs-lookup"><span data-stu-id="59bf0-163">Replicate the delta</span></span>

1. <span data-ttu-id="59bf0-164">在初始複寫之後，會根據複寫設定，開始進行差異同步處理。</span><span class="sxs-lookup"><span data-stu-id="59bf0-164">After the initial replication, delta synchronization begins, in accordance with replication settings.</span></span>
2. <span data-ttu-id="59bf0-165">Hyper-V 複本複寫追蹤器會以 .hrl 檔案格式追蹤虛擬硬碟的變更。</span><span class="sxs-lookup"><span data-stu-id="59bf0-165">The Hyper-V Replica Replication Tracker tracks the changes to a virtual hard disk as .hrl files.</span></span> <span data-ttu-id="59bf0-166">每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。</span><span class="sxs-lookup"><span data-stu-id="59bf0-166">Each disk that's configured for replication has an associated .hrl file.</span></span> <span data-ttu-id="59bf0-167">此記錄檔會在初始複寫完成後，傳送至客戶的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="59bf0-167">This log is sent to the customer's storage account after initial replication is complete.</span></span> <span data-ttu-id="59bf0-168">當記錄傳輸至 Azure 時，將會在同一目錄內的另一個記錄檔中追蹤主要磁碟中的變更。</span><span class="sxs-lookup"><span data-stu-id="59bf0-168">When a log is in transit to Azure, the changes in the primary disk are tracked in another log file, in the same directory.</span></span>
3. <span data-ttu-id="59bf0-169">在初始和差異複寫期間，您可以在 VM 檢視中監視 VM。</span><span class="sxs-lookup"><span data-stu-id="59bf0-169">During initial and delta replication, you can monitor the VM in the VM view.</span></span> <span data-ttu-id="59bf0-170">[深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-170">[Learn more](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span></span>  

### <a name="synchronize-replication"></a><span data-ttu-id="59bf0-171">同步處理複寫</span><span class="sxs-lookup"><span data-stu-id="59bf0-171">Synchronize replication</span></span>

1. <span data-ttu-id="59bf0-172">如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="59bf0-172">If delta replication fails, and a full replication would be costly in terms of bandwidth or time, then a VM is marked for resynchronization.</span></span> <span data-ttu-id="59bf0-173">例如，如果 .hrl 檔案達到磁碟大小的 50%，系統就會標示 VM 以便重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="59bf0-173">For example, if the .hrl files reach 50% of the disk size, then the VM will be marked for resynchronization.</span></span>
2.  <span data-ttu-id="59bf0-174">重新同步處理會計算來源和目標虛擬機器的總和檢查碼，並只傳送差異資料部分，藉此將傳送的資料量降至最低。</span><span class="sxs-lookup"><span data-stu-id="59bf0-174">Resynchronization minimizes the amount of data sent by computing checksums of the source and target virtual machines, and sending only the delta data.</span></span> <span data-ttu-id="59bf0-175">重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。</span><span class="sxs-lookup"><span data-stu-id="59bf0-175">Resynchronization uses a fixed-block chunking algorithm where source and target files are divided into fixed chunks.</span></span> <span data-ttu-id="59bf0-176">系統會產生每個區塊的總和檢查碼並相互比較，以決定需要將來源中的哪些區塊套用至目標。</span><span class="sxs-lookup"><span data-stu-id="59bf0-176">Checksums for each chunk are generated and then compared to determine which blocks from the source need to be applied to the target.</span></span>
3. <span data-ttu-id="59bf0-177">重新同步處理完成之後，應會繼續進行正常的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="59bf0-177">After resynchronization finishes, normal delta replication should resume.</span></span> <span data-ttu-id="59bf0-178">根據預設，重新同步處理會排程在上班時間以外的時間自動執行，但是您可以手動重新同步處理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59bf0-178">By default resynchronization is scheduled to run automatically outside office hours, but you can resynchronize a virtual machine manually.</span></span> <span data-ttu-id="59bf0-179">例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="59bf0-179">For example, you can resume resynchronization if a network outage or another outage occurs.</span></span> <span data-ttu-id="59bf0-180">若要這樣做，請在入口網站中選取 VM > [重新同步處理]。</span><span class="sxs-lookup"><span data-stu-id="59bf0-180">To do this, select the VM in the portal > **Resynchronize**.</span></span>

    ![手動重新同步處理](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a><span data-ttu-id="59bf0-182">重試邏輯</span><span class="sxs-lookup"><span data-stu-id="59bf0-182">Retry logic</span></span>

<span data-ttu-id="59bf0-183">如果發生複寫錯誤，會有內建的重試。</span><span class="sxs-lookup"><span data-stu-id="59bf0-183">If a replication error occurs, there's a built-in retry.</span></span> <span data-ttu-id="59bf0-184">此邏輯可分為以下兩種類別：</span><span class="sxs-lookup"><span data-stu-id="59bf0-184">This logic can be classified into two categories:</span></span>

<span data-ttu-id="59bf0-185">**類別**</span><span class="sxs-lookup"><span data-stu-id="59bf0-185">**Category**</span></span> | <span data-ttu-id="59bf0-186">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="59bf0-186">**Details**</span></span>
--- | ---
<span data-ttu-id="59bf0-187">**無法復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="59bf0-187">**Non-recoverable errors**</span></span> | <span data-ttu-id="59bf0-188">不嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="59bf0-188">No retry is attempted.</span></span> <span data-ttu-id="59bf0-189">VM 狀態為**重大**，需要管理員介入處理。</span><span class="sxs-lookup"><span data-stu-id="59bf0-189">VM status will be **Critical**, and administrator intervention is required.</span></span> <span data-ttu-id="59bf0-190">這些錯誤的範例包括︰中斷 VHD 鏈結；複本 VM 的狀態無效；網路驗證錯誤︰授權錯誤；找不到 VM 錯誤 (適用於獨立 Hyper-V 伺服器)</span><span class="sxs-lookup"><span data-stu-id="59bf0-190">Examples of these errors include: broken VHD chain; Invalid state for the replica VM; Network authentication errors: authorization errors; VM not found errors (for standalone Hyper-V servers)</span></span>
<span data-ttu-id="59bf0-191">**可復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="59bf0-191">**Recoverable errors**</span></span> | <span data-ttu-id="59bf0-192">在每個複寫間隔中進行重試，並採用指數倒退法，從第一次嘗試開始增加重試間隔 (1、2、4、8、10 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-192">Retries occur every replication interval, using an exponential back-off that increases the retry interval from the start of the first attempt by 1, 2, 4, 8, and 10 minutes.</span></span> <span data-ttu-id="59bf0-193">如果錯誤持續發生，會每隔 30 分鐘重試一次。</span><span class="sxs-lookup"><span data-stu-id="59bf0-193">If an error persists, retry every 30 minutes.</span></span> <span data-ttu-id="59bf0-194">範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況</span><span class="sxs-lookup"><span data-stu-id="59bf0-194">Examples include: network errors; low disk  errors; low memory conditions</span></span> |



## <a name="failover-and-failback-process"></a><span data-ttu-id="59bf0-195">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="59bf0-195">Failover and failback process</span></span>

1. <span data-ttu-id="59bf0-196">您可以執行從內部部署 Hyper-V VM 至 Azure 的計劃性或非計劃性[容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-196">You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs to Azure.</span></span> <span data-ttu-id="59bf0-197">如果您執行計劃性容錯移轉，則來源 VM 會關閉以確保不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="59bf0-197">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="59bf0-198">您可以容錯移轉單一機器，或建立[復原計劃](site-recovery-create-recovery-plans.md)來協調多部機器的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="59bf0-198">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="59bf0-199">執行容錯移轉之後，您應該就會在 Azure 中看到所建立的複本 VM。</span><span class="sxs-lookup"><span data-stu-id="59bf0-199">After you run the failover, you should be able to see the created replica VMs in Azure.</span></span> <span data-ttu-id="59bf0-200">如有必要，您可以對 VM 指派公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="59bf0-200">You can assign a public IP address to the VM if required.</span></span>
5. <span data-ttu-id="59bf0-201">然後，您要認可讓容錯移轉開始存取來自複本 Azure VM 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="59bf0-201">You then commit the failover to start accessing the workload from the replica Azure VM.</span></span>
6. <span data-ttu-id="59bf0-202">當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="59bf0-202">When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md).</span></span> <span data-ttu-id="59bf0-203">您可以啟動從 Azure 至主要網站的計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="59bf0-203">You kick off a planned failover from Azure to the primary site.</span></span> <span data-ttu-id="59bf0-204">針對計劃性容錯移轉，您可以選取要容錯回復至相同 VM 或其他位置，並同步處理 Azure 和內部部署之間的變更，以確保不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="59bf0-204">For a planned failover you can select to failback to the same VM or to an alternate location, and synchronize changes between Azure and on-premises, to ensure no data loss.</span></span> <span data-ttu-id="59bf0-205">在內部部署中建立了 VM 後，您就可以認可容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="59bf0-205">When VMs are created on-premises, you commit the failover.</span></span>




## <a name="next-steps"></a><span data-ttu-id="59bf0-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59bf0-206">Next steps</span></span>

<span data-ttu-id="59bf0-207">檢閱[支援矩陣](site-recovery-support-matrix-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="59bf0-207">Review the [support matrix](site-recovery-support-matrix-to-azure.md)</span></span>
