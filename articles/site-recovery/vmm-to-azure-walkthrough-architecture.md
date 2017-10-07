---
title: "HYPER-V 與 Azure Site Recovery 的複寫 （搭配 System Center VMM) tooAzure aaaReview hello 架構 |Microsoft 文件"
description: "這篇文章提供元件的概觀，並複寫時使用的架構在內部部署 HYPER-V Vm 的 VMM 雲端 tooAzure hello Azure Site Recovery 服務。"
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
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: ee1f2775b0c929894933b639464176d7a0441519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture"></a><span data-ttu-id="9558f-103">步驟 1： 檢閱 hello 架構</span><span class="sxs-lookup"><span data-stu-id="9558f-103">Step 1: Review hello architecture</span></span>


<span data-ttu-id="9558f-104">本文說明 hello 元件和複寫在內部使用 hello tooAzure System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器時使用的處理序[Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="9558f-104">This article describes hello components and processes used when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="9558f-105">在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="9558f-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="9558f-106">架構元件</span><span class="sxs-lookup"><span data-stu-id="9558f-106">Architectural components</span></span>

<span data-ttu-id="9558f-107">有多個元件在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時。</span><span class="sxs-lookup"><span data-stu-id="9558f-107">There are a number of components involved when replicating Hyper-V VMs in VMM clouds tooAzure.</span></span>

<span data-ttu-id="9558f-108">**元件**</span><span class="sxs-lookup"><span data-stu-id="9558f-108">**Component**</span></span> | <span data-ttu-id="9558f-109">**需求**</span><span class="sxs-lookup"><span data-stu-id="9558f-109">**Requirement**</span></span> | <span data-ttu-id="9558f-110">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="9558f-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="9558f-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="9558f-111">**Azure**</span></span> | <span data-ttu-id="9558f-112">在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="9558f-112">In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network.</span></span> | <span data-ttu-id="9558f-113">複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="9558f-113">Replicated data is stored in hello storage account, and Azure VMs are created with hello replicated data when failover from your on-premises site occurs.</span></span><br/><br/> <span data-ttu-id="9558f-114">在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9558f-114">hello Azure VMs connect toohello Azure virtual network when they're created.</span></span>
<span data-ttu-id="9558f-115">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="9558f-115">**VMM server**</span></span> | <span data-ttu-id="9558f-116">hello VMM 伺服器包含 HYPER-V 主機的一或多個雲端。</span><span class="sxs-lookup"><span data-stu-id="9558f-116">hello VMM server has one or more clouds containing Hyper-V hosts.</span></span> | <span data-ttu-id="9558f-117">Hello VMM 伺服器上安裝與 Site Recovery 的 hello Site Recovery Provider tooorchestrate 複寫，並在 hello 復原服務保存庫中註冊 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9558f-117">On hello VMM server you install hello Site Recovery Provider tooorchestrate replication with Site Recovery, and register hello server in hello Recovery Services vault.</span></span>
<span data-ttu-id="9558f-118">**Hyper-V 主機**</span><span class="sxs-lookup"><span data-stu-id="9558f-118">**Hyper-V host**</span></span> | <span data-ttu-id="9558f-119">一或多個由 VMM 管理的 Hyper-V 主機/叢集。</span><span class="sxs-lookup"><span data-stu-id="9558f-119">One or more Hyper-V hosts/clusters managed by VMM.</span></span> |  <span data-ttu-id="9558f-120">您每個主機或叢集成員上安裝 hello 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="9558f-120">You install hello Recovery Services agent on each host or cluster member.</span></span>
<span data-ttu-id="9558f-121">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="9558f-121">**Hyper-V VMs**</span></span> | <span data-ttu-id="9558f-122">一或多個在 Hyper-V 主機伺服器上執行的 VM。</span><span class="sxs-lookup"><span data-stu-id="9558f-122">One or VMs running on a Hyper-V host server.</span></span> | <span data-ttu-id="9558f-123">Tooexplicitly Vm 上安裝，不需要。</span><span class="sxs-lookup"><span data-stu-id="9558f-123">Nothing needs tooexplicitly installed on VMs.</span></span>
<span data-ttu-id="9558f-124">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="9558f-124">**Networking**</span></span> |<span data-ttu-id="9558f-125">邏輯和 VM 網路設定 hello VMM 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9558f-125">Logical and VM networks set up on hello VMM server.</span></span> <span data-ttu-id="9558f-126">VM 網路應連結的 tooa hello 雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="9558f-126">A VM network should be linked tooa logical network that's associated with hello cloud.</span></span> | <span data-ttu-id="9558f-127">VM 網路會對應的 tooAzure 虛擬網路，Azure Vm 位在網路中，當建立容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="9558f-127">VM networks are mapped tooAzure virtual networks, so that Azure VMs are located in a network when they're created after failover.</span></span>

<span data-ttu-id="9558f-128">深入了解 hello 部署先決條件和需求的每個元件在 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="9558f-128">Learn about hello deployment prerequisites and requirements for each of these components in hello [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>


<span data-ttu-id="9558f-129">**圖 1： 在 VMM 雲端 tooAzure 的 HYPER-V 主機上的複寫 Vm**</span><span class="sxs-lookup"><span data-stu-id="9558f-129">**Figure 1: Replicate VMs on Hyper-V hosts in VMM clouds tooAzure**</span></span>

![元件](./media/vmm-to-azure-walkthrough-architecture/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a><span data-ttu-id="9558f-131">複寫程序</span><span class="sxs-lookup"><span data-stu-id="9558f-131">Replication process</span></span>

<span data-ttu-id="9558f-132">**HYPER-V 複寫 tooAzure 如圖 2： 複寫和復原程序**</span><span class="sxs-lookup"><span data-stu-id="9558f-132">**Figure 2: Replication and recovery process for Hyper-V replication tooAzure**</span></span>

![工作流程](./media/vmm-to-azure-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a><span data-ttu-id="9558f-134">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="9558f-134">Enable protection</span></span>

1. <span data-ttu-id="9558f-135">您針對 HYPER-V 虛擬機器啟用保護之後，在 hello Azure 入口網站或內部部署，hello**啟用保護**啟動。</span><span class="sxs-lookup"><span data-stu-id="9558f-135">After you enable protection for a Hyper-V VM, in hello Azure portal or on-premises, hello **Enable protection** starts.</span></span>
2. <span data-ttu-id="9558f-136">hello 工作會檢查該 hello 機器符合必要條件，再叫用 hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)，tooset hello 設定已設定的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="9558f-136">hello job checks that hello machine complies with prerequisites, before invoking hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset up replication with hello settings you've configured.</span></span>
3. <span data-ttu-id="9558f-137">hello 工作所叫用 hello 啟動初始複寫[StartReplication](https://msdn.microsoft.com/library/hh850303.aspx)方法、 tooinitialize 完整的 VM 複寫，以及傳送嗨 VM 的虛擬磁碟 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9558f-137">hello job starts initial replication by invoking hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) method, tooinitialize a full VM replication, and send hello VM's virtual disks tooAzure.</span></span>
4. <span data-ttu-id="9558f-138">您可以監視 hello 作業在 hello**作業** 索引標籤。    ![作業清單](media/vmm-to-azure-walkthrough-architecture/image1.png) ![啟用保護向下鑽研](media/vmm-to-azure-walkthrough-architecture/image2.png)</span><span class="sxs-lookup"><span data-stu-id="9558f-138">You can monitor hello job in hello **Jobs** tab.      ![Jobs list](media/vmm-to-azure-walkthrough-architecture/image1.png) ![Enable protection drill down](media/vmm-to-azure-walkthrough-architecture/image2.png)</span></span>

### <a name="replicate-hello-initial-data"></a><span data-ttu-id="9558f-139">Hello 初始資料複寫</span><span class="sxs-lookup"><span data-stu-id="9558f-139">Replicate hello initial data</span></span>

1. <span data-ttu-id="9558f-140">系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9558f-140">A [Hyper-V VM snapshot](https://technet.microsoft.com/library/dd560637.aspx) snapshot is taken when initial replication is triggered.</span></span>
2. <span data-ttu-id="9558f-141">虛擬硬碟才是所有的複製的 tooAzure 複寫的一個。</span><span class="sxs-lookup"><span data-stu-id="9558f-141">Virtual hard disks are replicated one by one until they're all copied tooAzure.</span></span> <span data-ttu-id="9558f-142">它可能需要一些時間，視 hello VM 大小和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="9558f-142">It could take a while, depending on hello VM size, and network bandwidth.</span></span> <span data-ttu-id="9558f-143">toooptimize 網路使用量，請參閱[如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)。</span><span class="sxs-lookup"><span data-stu-id="9558f-143">toooptimize your network usage, see [How toomanage on-premises tooAzure protection network bandwidth usage](https://support.microsoft.com/kb/3056159).</span></span>
3. <span data-ttu-id="9558f-144">如果磁碟上的變更會發生初始複寫正在進行時，hello HYPER-V 複本複寫追蹤器會追蹤這些變更為 HYPER-V 複寫記錄檔 (.hrl)。</span><span class="sxs-lookup"><span data-stu-id="9558f-144">If disk changes occur while initial replication is in progress, hello Hyper-V Replica Replication Tracker tracks those changes as Hyper-V Replication Logs (.hrl).</span></span> <span data-ttu-id="9558f-145">這些檔案位在 hello 與 hello 磁碟相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="9558f-145">These files are located in hello same folder as hello disks.</span></span> <span data-ttu-id="9558f-146">每個磁碟具有相關聯的.hrl 檔案傳送 toosecondary 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9558f-146">Each disk has an associated .hrl file that will be sent toosecondary storage.</span></span>
4. <span data-ttu-id="9558f-147">初始複寫正在進行時，hello 快照集和記錄檔會消耗磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="9558f-147">hello snapshot and log files consume disk resources while initial replication is in progress.</span></span>
5. <span data-ttu-id="9558f-148">Hello 初始複寫完成時，會刪除 hello VM 快照集。</span><span class="sxs-lookup"><span data-stu-id="9558f-148">When hello initial replication finishes, hello VM snapshot is deleted.</span></span> <span data-ttu-id="9558f-149">Hello 記錄檔中的差異磁碟變更為已同步處理和合併 toohello 父系磁碟。</span><span class="sxs-lookup"><span data-stu-id="9558f-149">Delta disk changes in hello log are synchronized and merged toohello parent disk.</span></span>


### <a name="finalize-protection"></a><span data-ttu-id="9558f-150">完成保護</span><span class="sxs-lookup"><span data-stu-id="9558f-150">Finalize protection</span></span>

1. <span data-ttu-id="9558f-151">Hello 初始複寫完成，hello 之後**完成 hello 虛擬機器上的保護**作業設定網路和其他複寫後續設定，以便 hello 虛擬機器時保護。</span><span class="sxs-lookup"><span data-stu-id="9558f-151">After hello initial replication finishes, hello **Finalize protection on hello virtual machine** job configures network and other post-replication settings, so that hello virtual machine is protected.</span></span>
    <span data-ttu-id="9558f-152">![完成保護作業](media/vmm-to-azure-walkthrough-architecture/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9558f-152">![Finalize protection job](media/vmm-to-azure-walkthrough-architecture/image3.png)</span></span>
2. <span data-ttu-id="9558f-153">如果您要複寫 tooAzure，您可能需要 tootweak hello 設定 hello 虛擬機器，讓它準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="9558f-153">If you're replicating tooAzure, you might need tootweak hello settings for hello virtual machine so that it's ready for failover.</span></span> <span data-ttu-id="9558f-154">此時，您可以執行測試容錯移轉 toocheck 一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="9558f-154">At this point you can run a test failover toocheck everything is working as expected.</span></span>

### <a name="replicate-hello-delta"></a><span data-ttu-id="9558f-155">複寫 hello 差異</span><span class="sxs-lookup"><span data-stu-id="9558f-155">Replicate hello delta</span></span>

1. <span data-ttu-id="9558f-156">Hello 初始複寫之後，差異同步處理開始時，根據複寫設定。</span><span class="sxs-lookup"><span data-stu-id="9558f-156">After hello initial replication, delta synchronization begins, in accordance with replication settings.</span></span>
2. <span data-ttu-id="9558f-157">hello HYPER-V 複本複寫追蹤器會為.hrl 檔案追蹤 hello 變更 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="9558f-157">hello Hyper-V Replica Replication Tracker tracks hello changes tooa virtual hard disk as .hrl files.</span></span> <span data-ttu-id="9558f-158">每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。</span><span class="sxs-lookup"><span data-stu-id="9558f-158">Each disk that's configured for replication has an associated .hrl file.</span></span> <span data-ttu-id="9558f-159">此記錄檔會在初始複寫完成之後傳送 toohello 客戶儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9558f-159">This log is sent toohello customer's storage account after initial replication is complete.</span></span> <span data-ttu-id="9558f-160">在另一個記錄檔，在 hello 傳輸 tooAzure 記錄時，會追蹤 hello 變更 hello 主要磁碟相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="9558f-160">When a log is in transit tooAzure, hello changes in hello primary disk are tracked in another log file, in hello same directory.</span></span>
3. <span data-ttu-id="9558f-161">初始和差異在複寫期間，您可以監視 hello VM 檢視中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="9558f-161">During initial and delta replication, you can monitor hello VM in hello VM view.</span></span> <span data-ttu-id="9558f-162">[深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="9558f-162">[Learn more](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span></span>  

### <a name="synchronize-replication"></a><span data-ttu-id="9558f-163">同步處理複寫</span><span class="sxs-lookup"><span data-stu-id="9558f-163">Synchronize replication</span></span>

1. <span data-ttu-id="9558f-164">如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="9558f-164">If delta replication fails, and a full replication would be costly in terms of bandwidth or time, then a VM is marked for resynchronization.</span></span> <span data-ttu-id="9558f-165">例如，如果 hello.hrl 檔案到達 hello 磁碟大小的 50%，然後 hello VM 將會標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="9558f-165">For example, if hello .hrl files reach 50% of hello disk size, then hello VM will be marked for resynchronization.</span></span>
2.  <span data-ttu-id="9558f-166">重新同步處理將 hello 會計算總和檢查碼的 hello 的來源和目標虛擬機器，並傳送 hello 差異資料傳送的資料量降到最低。</span><span class="sxs-lookup"><span data-stu-id="9558f-166">Resynchronization minimizes hello amount of data sent by computing checksums of hello source and target virtual machines, and sending only hello delta data.</span></span> <span data-ttu-id="9558f-167">重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。</span><span class="sxs-lookup"><span data-stu-id="9558f-167">Resynchronization uses a fixed-block chunking algorithm where source and target files are divided into fixed chunks.</span></span> <span data-ttu-id="9558f-168">總和檢查碼的每個區塊產生，則會比較，它會封鎖從 hello 來源需要 toobe 套用的 toohello 目標 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="9558f-168">Checksums for each chunk are generated and then compared toodetermine which blocks from hello source need toobe applied toohello target.</span></span>
3. <span data-ttu-id="9558f-169">重新同步處理完成之後，應會繼續進行正常的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="9558f-169">After resynchronization finishes, normal delta replication should resume.</span></span> <span data-ttu-id="9558f-170">預設重新同步處理排程的 toorun 自動外上班時間時，但是您可以手動重新同步虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9558f-170">By default resynchronization is scheduled toorun automatically outside office hours, but you can resynchronize a virtual machine manually.</span></span> <span data-ttu-id="9558f-171">例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="9558f-171">For example, you can resume resynchronization if a network outage or another outage occurs.</span></span> <span data-ttu-id="9558f-172">toodo hello 入口網站中的，選取 hello VM >**重新同步處理**。</span><span class="sxs-lookup"><span data-stu-id="9558f-172">toodo this, select hello VM in hello portal > **Resynchronize**.</span></span>

    ![手動重新同步處理](media/vmm-to-azure-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a><span data-ttu-id="9558f-174">重試邏輯</span><span class="sxs-lookup"><span data-stu-id="9558f-174">Retry logic</span></span>

<span data-ttu-id="9558f-175">如果發生複寫錯誤，會有內建的重試。</span><span class="sxs-lookup"><span data-stu-id="9558f-175">If a replication error occurs, there's a built-in retry.</span></span> <span data-ttu-id="9558f-176">此邏輯可分為以下兩種類別：</span><span class="sxs-lookup"><span data-stu-id="9558f-176">This logic can be classified into two categories:</span></span>

<span data-ttu-id="9558f-177">**類別**</span><span class="sxs-lookup"><span data-stu-id="9558f-177">**Category**</span></span> | <span data-ttu-id="9558f-178">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="9558f-178">**Details**</span></span>
--- | ---
<span data-ttu-id="9558f-179">**無法復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="9558f-179">**Non-recoverable errors**</span></span> | <span data-ttu-id="9558f-180">不嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="9558f-180">No retry is attempted.</span></span> <span data-ttu-id="9558f-181">VM 狀態為**重大**，需要管理員介入處理。</span><span class="sxs-lookup"><span data-stu-id="9558f-181">VM status will be **Critical**, and administrator intervention is required.</span></span> <span data-ttu-id="9558f-182">這些錯誤的範例包括： 中斷 VHD 鏈結。Hello 複本 VM; 無效的狀態網路驗證錯誤： 授權錯誤。找不到錯誤 （適用於獨立 HYPER-V 伺服器） 的 VM</span><span class="sxs-lookup"><span data-stu-id="9558f-182">Examples of these errors include: broken VHD chain; Invalid state for hello replica VM; Network authentication errors: authorization errors; VM not found errors (for standalone Hyper-V servers)</span></span>
<span data-ttu-id="9558f-183">**可復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="9558f-183">**Recoverable errors**</span></span> | <span data-ttu-id="9558f-184">產生每個複寫間隔，使用指數型撤退，從而 hello 從 hello 開頭的 1、 2、 4、 8、 hello 第一次嘗試的重試間隔和 10 分鐘重試作業。</span><span class="sxs-lookup"><span data-stu-id="9558f-184">Retries occur every replication interval, using an exponential back-off that increases hello retry interval from hello start of hello first attempt by 1, 2, 4, 8, and 10 minutes.</span></span> <span data-ttu-id="9558f-185">如果錯誤持續發生，會每隔 30 分鐘重試一次。</span><span class="sxs-lookup"><span data-stu-id="9558f-185">If an error persists, retry every 30 minutes.</span></span> <span data-ttu-id="9558f-186">範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況</span><span class="sxs-lookup"><span data-stu-id="9558f-186">Examples include: network errors; low disk  errors; low memory conditions</span></span> |



## <a name="failover-and-failback-process"></a><span data-ttu-id="9558f-187">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="9558f-187">Failover and failback process</span></span>

1. <span data-ttu-id="9558f-188">您可以執行的已規劃或未規劃[容錯移轉](site-recovery-failover.md)從內部部署 HYPER-V Vm tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9558f-188">You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs tooAzure.</span></span> <span data-ttu-id="9558f-189">如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="9558f-189">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="9558f-190">您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。</span><span class="sxs-lookup"><span data-stu-id="9558f-190">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="9558f-191">執行 hello 容錯移轉之後，您應該在 Azure 中建立複本 Vm 可以 toosee hello。</span><span class="sxs-lookup"><span data-stu-id="9558f-191">After you run hello failover, you should be able toosee hello created replica VMs in Azure.</span></span> <span data-ttu-id="9558f-192">如果需要，您可以指定公用 IP 位址 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="9558f-192">You can assign a public IP address toohello VM if required.</span></span>
5. <span data-ttu-id="9558f-193">然後，您就會認可 hello 容錯移轉 toostart 從 hello 複本 Azure VM 存取 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="9558f-193">You then commit hello failover toostart accessing hello workload from hello replica Azure VM.</span></span>
6. <span data-ttu-id="9558f-194">當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="9558f-194">When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md).</span></span> <span data-ttu-id="9558f-195">您開始進行規劃的容錯移轉，從 Azure toohello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="9558f-195">You kick off a planned failover from Azure toohello primary site.</span></span> <span data-ttu-id="9558f-196">規劃的容錯移轉，您可以選取 toofailback toohello 相同 VM 或 tooan 替代位置，並同步處理變更 Azure 和內部部署、 tooensure 之間不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="9558f-196">For a planned failover you can select toofailback toohello same VM or tooan alternate location, and synchronize changes between Azure and on-premises, tooensure no data loss.</span></span> <span data-ttu-id="9558f-197">Vm 建立時在內部部署，您就會認可 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="9558f-197">When VMs are created on-premises, you commit hello failover.</span></span>




## <a name="next-steps"></a><span data-ttu-id="9558f-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9558f-198">Next steps</span></span>

<span data-ttu-id="9558f-199">跳過[步驟 2： 檢閱 hello 部署必要條件](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="9558f-199">Go too[Step 2: Review hello deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md)</span></span>
