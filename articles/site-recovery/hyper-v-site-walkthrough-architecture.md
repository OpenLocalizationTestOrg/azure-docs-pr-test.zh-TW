---
title: "檢閱使用 Azure Site Recovery 將 Hyper-V (不含 System Center VMM) 複寫至 Azure 的架構 | Microsoft Docs"
description: "本文提供使用 Azure Site Recovery 服務將內部部署 Hyper-V VM (不含 VMM) 複寫至 Azure 時所用元件和架構的概觀。"
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
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: d57cbc5b205cfb020070d567097f3bb648ce5300
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-azure"></a><span data-ttu-id="dc4ee-103">步驟 1：檢閱 Hyper-V 複寫至 Azure 的架構</span><span class="sxs-lookup"><span data-stu-id="dc4ee-103">Step 1: Review the architecture for Hyper-V replication to Azure</span></span>


<span data-ttu-id="dc4ee-104">本文說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 Hyper-V 虛擬機器 (不是由系統中心 VMM 管理) 複寫至 Azure 時的相關元件和程序。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (that aren't managed by System Center VMM), to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="dc4ee-105">如有任何意見，請張貼於這篇文章下方或 [Azure 復原服務論壇 (英文)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="dc4ee-106">架構元件</span><span class="sxs-lookup"><span data-stu-id="dc4ee-106">Architectural components</span></span>

<span data-ttu-id="dc4ee-107">將 Hyper-V VM 複寫至 Azure (不含 VMM) 時，會涉及許多元件。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-107">There are a number of components involved when replicating Hyper-V VMs to Azure without VMM.</span></span>

<span data-ttu-id="dc4ee-108">**元件**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-108">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="dc4ee-110">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="dc4ee-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-111">**Azure**</span></span> | <span data-ttu-id="dc4ee-112">在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-112">In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network.</span></span> | <span data-ttu-id="dc4ee-113">所複寫的資料會儲存在儲存體帳戶中，而在從內部部署網站進行容錯移轉時，便會以複寫的資料建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-113">Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs.</span></span><br/><br/> <span data-ttu-id="dc4ee-114">Azure VM 在建立後會連線到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-114">The Azure VMs connect to the Azure virtual network when they're created.</span></span>
<span data-ttu-id="dc4ee-115">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-115">**Hyper-V**</span></span> | <span data-ttu-id="dc4ee-116">Hyper-V 主機和叢集會蒐集到 Hyper-V 網站中。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-116">Hyper-V hosts and clusters are gathered into Hyper-V sites.</span></span> <span data-ttu-id="dc4ee-117">Azure Site Recovery 提供者和復原服務代理程式會安裝在每部 Hyper-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-117">The Azure Site Recovery Provider and Recovery Services agent is installed on each Hyper-V host.</span></span> | <span data-ttu-id="dc4ee-118">此提供者會透過網際網路與 Site Recovery 協調複寫作業。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-118">The Provider orchestrates replication with Site Recovery over the internet.</span></span> <span data-ttu-id="dc4ee-119">復原服務代理程式會處理資料複寫。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-119">The Recovery Services agent handles data replication.</span></span><br/><br/> <span data-ttu-id="dc4ee-120">來自提供者和代理程式的通訊都是安全且加密的。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-120">Communications from both the Provider and the agent are secure and encrypted.</span></span> <span data-ttu-id="dc4ee-121">Azure 儲存體中的複寫的資料也會加密。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-121">Replicated data in Azure storage is also encrypted.</span></span>
<span data-ttu-id="dc4ee-122">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-122">**Hyper-V VMs**</span></span> | <span data-ttu-id="dc4ee-123">您必須有一或多部在 Hyper-V 主機伺服器上執行的 VM。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-123">You need one or more VMs running on a Hyper-V host server.</span></span> | <span data-ttu-id="dc4ee-124">不需要在 VM 上明確安裝任何項目。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-124">Nothing needs to explicitly installed on VMs.</span></span>

<span data-ttu-id="dc4ee-125">了解[支援矩陣](site-recovery-support-matrix-to-azure.md)中每個元件的部署必要條件和需求。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-125">Learn about the deployment prerequisites and requirements for each of these components in the [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>

<span data-ttu-id="dc4ee-126">**圖 1：Hyper-V 網站至 Azure 的複寫**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-126">**Figure 1: Hyper-V site to Azure replication**</span></span>

![元件](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a><span data-ttu-id="dc4ee-128">複寫程序</span><span class="sxs-lookup"><span data-stu-id="dc4ee-128">Replication process</span></span>

<span data-ttu-id="dc4ee-129">**圖 2：將 Hyper-V 複寫至 Azure 的複寫和復原程序**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-129">**Figure 2: Replication and recovery process for Hyper-V replication to Azure**</span></span>

![工作流程](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a><span data-ttu-id="dc4ee-131">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-131">Enable protection</span></span>

1. <span data-ttu-id="dc4ee-132">您在 Azure 入口網站或內部部署針對 Hyper-V VM 啟用保護之後，**啟用保護**隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-132">After you enable protection for a Hyper-V VM, in the Azure portal or on-premises, the **Enable protection** starts.</span></span>
2. <span data-ttu-id="dc4ee-133">作業會檢查符合必要條件的機器，然後叫用 [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx) 方法，以使用您進行的設定來設定複寫。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-133">The job checks that the machine complies with prerequisites, before invoking the [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), to set up replication with the settings you've configured.</span></span>
3. <span data-ttu-id="dc4ee-134">作業會啟動初始複寫，方法是叫用 [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) 方法，以初始化完整的 VM 複寫，並且將 VM 的虛擬磁碟傳送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-134">The job starts initial replication by invoking the [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) method, to initialize a full VM replication, and send the VM's virtual disks to Azure.</span></span>
4. <span data-ttu-id="dc4ee-135">您可以在 [作業] 索引標籤中監視作業。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-135">You can monitor the job in the **Jobs** tab.</span></span>
 
### <a name="replicate-the-initial-data"></a><span data-ttu-id="dc4ee-136">複寫初始資料</span><span class="sxs-lookup"><span data-stu-id="dc4ee-136">Replicate the initial data</span></span>

1. <span data-ttu-id="dc4ee-137">系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-137">A [Hyper-V VM snapshot](https://technet.microsoft.com/library/dd560637.aspx) snapshot is taken when initial replication is triggered.</span></span>
2. <span data-ttu-id="dc4ee-138">虛擬硬碟會逐一複寫，直到它們全部複製到 Azure 為止。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-138">Virtual hard disks are replicated one by one until they're all copied to Azure.</span></span> <span data-ttu-id="dc4ee-139">可能需要一些時間，取決於 VM 大小和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-139">It could take a while, depending on the VM size, and network bandwidth.</span></span> <span data-ttu-id="dc4ee-140">若要將網路使用量最佳化，請參閱 [如何管理內部部署至 Azure 保護的網路頻寬使用量](https://support.microsoft.com/kb/3056159)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-140">To optimize your network usage, see [How to manage on-premises to Azure protection network bandwidth usage](https://support.microsoft.com/kb/3056159).</span></span>
3. <span data-ttu-id="dc4ee-141">如果在初始複寫進行時發生磁碟變更，Hyper-V 複本複寫追蹤器會以 Hyper-V 複寫記錄檔 (.hrl) 的形式追蹤這些變更。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-141">If disk changes occur while initial replication is in progress, the Hyper-V Replica Replication Tracker tracks those changes as Hyper-V Replication Logs (.hrl).</span></span> <span data-ttu-id="dc4ee-142">這些記錄檔位於與磁碟相同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-142">These files are located in the same folder as the disks.</span></span> <span data-ttu-id="dc4ee-143">每個磁碟都有一個相關聯的.hrl 檔案，將會傳送至次要儲存體。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-143">Each disk has an associated .hrl file that will be sent to secondary storage.</span></span>
4. <span data-ttu-id="dc4ee-144">當初始複寫正在進行時，快照和記錄檔會取用磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-144">The snapshot and log files consume disk resources while initial replication is in progress.</span></span>
5. <span data-ttu-id="dc4ee-145">初始複寫完成時，就會刪除 VM 快照集。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-145">When the initial replication finishes, the VM snapshot is deleted.</span></span> <span data-ttu-id="dc4ee-146">記錄中的差異磁碟變更會同步處理，並合併到父磁碟。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-146">Delta disk changes in the log are synchronized and merged to the parent disk.</span></span>


### <a name="finalize-protection"></a><span data-ttu-id="dc4ee-147">完成保護</span><span class="sxs-lookup"><span data-stu-id="dc4ee-147">Finalize protection</span></span>

1. <span data-ttu-id="dc4ee-148">初始複寫完成之後，**在虛擬機器上完成保護**作業會設定網路和其他複寫後設定，如此就能讓虛擬機器受到保護。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-148">After the initial replication finishes, the **Finalize protection on the virtual machine** job configures network and other post-replication settings, so that the virtual machine is protected.</span></span>
2. <span data-ttu-id="dc4ee-149">如果您要複寫至 Azure，您可能需要調整虛擬機器的設定，使其準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-149">If you're replicating to Azure, you might need to tweak the settings for the virtual machine so that it's ready for failover.</span></span> <span data-ttu-id="dc4ee-150">此時，您可以執行測試容錯移轉，以確認一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-150">At this point you can run a test failover to check everything is working as expected.</span></span>

### <a name="replicate-the-delta"></a><span data-ttu-id="dc4ee-151">複寫差異</span><span class="sxs-lookup"><span data-stu-id="dc4ee-151">Replicate the delta</span></span>

1. <span data-ttu-id="dc4ee-152">在初始複寫之後，會根據複寫設定，開始進行差異同步處理。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-152">After the initial replication, delta synchronization begins, in accordance with replication settings.</span></span>
2. <span data-ttu-id="dc4ee-153">Hyper-V 複本複寫追蹤器會以 .hrl 檔案格式追蹤虛擬硬碟的變更。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-153">The Hyper-V Replica Replication Tracker tracks the changes to a virtual hard disk as .hrl files.</span></span> <span data-ttu-id="dc4ee-154">每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-154">Each disk that's configured for replication has an associated .hrl file.</span></span> <span data-ttu-id="dc4ee-155">此記錄檔會在初始複寫完成後，傳送至客戶的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-155">This log is sent to the customer's storage account after initial replication is complete.</span></span> <span data-ttu-id="dc4ee-156">當記錄傳輸至 Azure 時，將會在同一目錄內的另一個記錄檔中追蹤主要磁碟中的變更。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-156">When a log is in transit to Azure, the changes in the primary disk are tracked in another log file, in the same directory.</span></span>
3. <span data-ttu-id="dc4ee-157">在初始和差異複寫期間，您可以在 VM 檢視中監視 VM。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-157">During initial and delta replication, you can monitor the VM in the VM view.</span></span> <span data-ttu-id="dc4ee-158">[深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-158">[Learn more](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span></span>  

### <a name="synchronize-replication"></a><span data-ttu-id="dc4ee-159">同步處理複寫</span><span class="sxs-lookup"><span data-stu-id="dc4ee-159">Synchronize replication</span></span>

1. <span data-ttu-id="dc4ee-160">如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-160">If delta replication fails, and a full replication would be costly in terms of bandwidth or time, then a VM is marked for resynchronization.</span></span> <span data-ttu-id="dc4ee-161">例如，如果 .hrl 檔案達到磁碟大小的 50%，系統就會標示 VM 以便重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-161">For example, if the .hrl files reach 50% of the disk size, then the VM will be marked for resynchronization.</span></span>
2.  <span data-ttu-id="dc4ee-162">重新同步處理會計算來源和目標虛擬機器的總和檢查碼，並只傳送差異資料部分，藉此將傳送的資料量降至最低。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-162">Resynchronization minimizes the amount of data sent by computing checksums of the source and target virtual machines, and sending only the delta data.</span></span> <span data-ttu-id="dc4ee-163">重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-163">Resynchronization uses a fixed-block chunking algorithm where source and target files are divided into fixed chunks.</span></span> <span data-ttu-id="dc4ee-164">系統會產生每個區塊的總和檢查碼並相互比較，以決定需要將來源中的哪些區塊套用至目標。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-164">Checksums for each chunk are generated and then compared to determine which blocks from the source need to be applied to the target.</span></span>
3. <span data-ttu-id="dc4ee-165">重新同步處理完成之後，應會繼續進行正常的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-165">After resynchronization finishes, normal delta replication should resume.</span></span> <span data-ttu-id="dc4ee-166">根據預設，重新同步處理會排程在上班時間以外的時間自動執行，但是您可以手動重新同步處理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-166">By default resynchronization is scheduled to run automatically outside office hours, but you can resynchronize a virtual machine manually.</span></span> <span data-ttu-id="dc4ee-167">例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-167">For example, you can resume resynchronization if a network outage or another outage occurs.</span></span> <span data-ttu-id="dc4ee-168">若要這樣做，請在入口網站中選取 VM > [重新同步處理]。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-168">To do this, select the VM in the portal > **Resynchronize**.</span></span>

    ![手動重新同步處理](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a><span data-ttu-id="dc4ee-170">重試邏輯</span><span class="sxs-lookup"><span data-stu-id="dc4ee-170">Retry logic</span></span>

<span data-ttu-id="dc4ee-171">如果發生複寫錯誤，會有內建的重試。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-171">If a replication error occurs, there's a built-in retry.</span></span> <span data-ttu-id="dc4ee-172">此邏輯可分為以下兩種類別：</span><span class="sxs-lookup"><span data-stu-id="dc4ee-172">This logic can be classified into two categories:</span></span>

<span data-ttu-id="dc4ee-173">**類別**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-173">**Category**</span></span> | <span data-ttu-id="dc4ee-174">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-174">**Details**</span></span>
--- | ---
<span data-ttu-id="dc4ee-175">**無法復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-175">**Non-recoverable errors**</span></span> | <span data-ttu-id="dc4ee-176">不嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-176">No retry is attempted.</span></span> <span data-ttu-id="dc4ee-177">VM 狀態為**重大**，需要管理員介入處理。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-177">VM status will be **Critical**, and administrator intervention is required.</span></span> <span data-ttu-id="dc4ee-178">這些錯誤的範例包括︰中斷 VHD 鏈結；複本 VM 的狀態無效；網路驗證錯誤︰授權錯誤；找不到 VM 錯誤 (適用於獨立 Hyper-V 伺服器)</span><span class="sxs-lookup"><span data-stu-id="dc4ee-178">Examples of these errors include: broken VHD chain; Invalid state for the replica VM; Network authentication errors: authorization errors; VM not found errors (for standalone Hyper-V servers)</span></span>
<span data-ttu-id="dc4ee-179">**可復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="dc4ee-179">**Recoverable errors**</span></span> | <span data-ttu-id="dc4ee-180">在每個複寫間隔中進行重試，並採用指數倒退法，從第一次嘗試開始增加重試間隔 (1、2、4、8、10 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-180">Retries occur every replication interval, using an exponential back-off that increases the retry interval from the start of the first attempt by 1, 2, 4, 8, and 10 minutes.</span></span> <span data-ttu-id="dc4ee-181">如果錯誤持續發生，會每隔 30 分鐘重試一次。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-181">If an error persists, retry every 30 minutes.</span></span> <span data-ttu-id="dc4ee-182">範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況</span><span class="sxs-lookup"><span data-stu-id="dc4ee-182">Examples include: network errors; low disk  errors; low memory conditions</span></span> |



## <a name="failover-and-failback-process"></a><span data-ttu-id="dc4ee-183">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="dc4ee-183">Failover and failback process</span></span>

1. <span data-ttu-id="dc4ee-184">您可以執行從內部部署 Hyper-V VM 至 Azure 的計劃性或非計劃性[容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-184">You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs to Azure.</span></span> <span data-ttu-id="dc4ee-185">如果您執行計劃性容錯移轉，則來源 VM 會關閉以確保不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-185">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="dc4ee-186">您可以容錯移轉單一機器，或建立[復原計劃](site-recovery-create-recovery-plans.md)來協調多部機器的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-186">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="dc4ee-187">執行容錯移轉之後，您應該就會在 Azure 中看到所建立的複本 VM。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-187">After you run the failover, you should be able to see the created replica VMs in Azure.</span></span> <span data-ttu-id="dc4ee-188">如有必要，您可以對 VM 指派公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-188">You can assign a public IP address to the VM if required.</span></span>
5. <span data-ttu-id="dc4ee-189">然後，您要認可讓容錯移轉開始存取來自複本 Azure VM 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-189">You then commit the failover to start accessing the workload from the replica Azure VM.</span></span>
6. <span data-ttu-id="dc4ee-190">當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-190">When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md).</span></span> <span data-ttu-id="dc4ee-191">您可以啟動從 Azure 至主要網站的計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-191">You kick off a planned failover from Azure to the primary site.</span></span> <span data-ttu-id="dc4ee-192">針對計劃性容錯移轉，您可以選取要容錯回復至相同 VM 或其他位置，並同步處理 Azure 和內部部署之間的變更，以確保不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-192">For a planned failover you can select to failback to the same VM or to an alternate location, and synchronize changes between Azure and on-premises, to ensure no data loss.</span></span> <span data-ttu-id="dc4ee-193">在內部部署中建立了 VM 後，您就可以認可容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dc4ee-193">When VMs are created on-premises, you commit the failover.</span></span>




## <a name="next-steps"></a><span data-ttu-id="dc4ee-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc4ee-194">Next steps</span></span>

<span data-ttu-id="dc4ee-195">移至[步驟 2：檢閱部署先決條件](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="dc4ee-195">Go to [Step 2: Review the deployment prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>
