---
title: "HYPER-V 與 Azure Site Recovery 的複寫 （而不使用 System Center VMM) tooAzure aaaReview hello 架構 |Microsoft 文件"
description: "本文提供元件和複寫在內部部署 （無 VMM) 的 HYPER-V Vm tooAzure hello Azure Site Recovery 服務時使用的架構的概觀。"
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
ms.openlocfilehash: ec148e87ab2fa17485001ee447ad9f9bf795840e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooazure"></a><span data-ttu-id="1b89a-103">步驟 1： 檢閱 HYPER-V 複寫 tooAzure hello 架構</span><span class="sxs-lookup"><span data-stu-id="1b89a-103">Step 1: Review hello architecture for Hyper-V replication tooAzure</span></span>


<span data-ttu-id="1b89a-104">這篇文章描述 hello 元件和處理程序涉及複寫時在內部部署 HYPER-V 虛擬機器 （不由 System Center VMM 管理），使用 hello tooAzure [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="1b89a-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (that aren't managed by System Center VMM), tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="1b89a-105">在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="1b89a-106">架構元件</span><span class="sxs-lookup"><span data-stu-id="1b89a-106">Architectural components</span></span>

<span data-ttu-id="1b89a-107">有多個元件所涉及複寫無 VMM 的 HYPER-V Vm tooAzure 時。</span><span class="sxs-lookup"><span data-stu-id="1b89a-107">There are a number of components involved when replicating Hyper-V VMs tooAzure without VMM.</span></span>

<span data-ttu-id="1b89a-108">**元件**</span><span class="sxs-lookup"><span data-stu-id="1b89a-108">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="1b89a-110">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="1b89a-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="1b89a-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="1b89a-111">**Azure**</span></span> | <span data-ttu-id="1b89a-112">在 Azure 中，您需要 Microsoft Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="1b89a-112">In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network.</span></span> | <span data-ttu-id="1b89a-113">複寫的資料會儲存在 hello 儲存體帳戶，並從您的內部部署站台容錯移轉發生時，將會建立與 hello 複寫資料的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="1b89a-113">Replicated data is stored in hello storage account, and Azure VMs are created with hello replicated data when failover from your on-premises site occurs.</span></span><br/><br/> <span data-ttu-id="1b89a-114">在建立時即 hello Azure Vm 會連線 toohello Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1b89a-114">hello Azure VMs connect toohello Azure virtual network when they're created.</span></span>
<span data-ttu-id="1b89a-115">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1b89a-115">**Hyper-V**</span></span> | <span data-ttu-id="1b89a-116">Hyper-V 主機和叢集會蒐集到 Hyper-V 網站中。</span><span class="sxs-lookup"><span data-stu-id="1b89a-116">Hyper-V hosts and clusters are gathered into Hyper-V sites.</span></span> <span data-ttu-id="1b89a-117">hello Azure Site Recovery Provider 和復原服務代理程式安裝在每個 HYPER-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="1b89a-117">hello Azure Site Recovery Provider and Recovery Services agent is installed on each Hyper-V host.</span></span> | <span data-ttu-id="1b89a-118">hello 提供者會協調複寫與站台復原 hello 透過網際網路。</span><span class="sxs-lookup"><span data-stu-id="1b89a-118">hello Provider orchestrates replication with Site Recovery over hello internet.</span></span> <span data-ttu-id="1b89a-119">hello 復原服務代理程式處理資料的複寫。</span><span class="sxs-lookup"><span data-stu-id="1b89a-119">hello Recovery Services agent handles data replication.</span></span><br/><br/> <span data-ttu-id="1b89a-120">從提供者 hello 和 hello 代理程式的通訊是安全而且會加密。</span><span class="sxs-lookup"><span data-stu-id="1b89a-120">Communications from both hello Provider and hello agent are secure and encrypted.</span></span> <span data-ttu-id="1b89a-121">Azure 儲存體中的複寫的資料也會加密。</span><span class="sxs-lookup"><span data-stu-id="1b89a-121">Replicated data in Azure storage is also encrypted.</span></span>
<span data-ttu-id="1b89a-122">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="1b89a-122">**Hyper-V VMs**</span></span> | <span data-ttu-id="1b89a-123">您必須有一或多部在 Hyper-V 主機伺服器上執行的 VM。</span><span class="sxs-lookup"><span data-stu-id="1b89a-123">You need one or more VMs running on a Hyper-V host server.</span></span> | <span data-ttu-id="1b89a-124">Tooexplicitly Vm 上安裝，不需要。</span><span class="sxs-lookup"><span data-stu-id="1b89a-124">Nothing needs tooexplicitly installed on VMs.</span></span>

<span data-ttu-id="1b89a-125">深入了解 hello 部署先決條件和需求的每個元件在 hello[支援矩陣](site-recovery-support-matrix-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-125">Learn about hello deployment prerequisites and requirements for each of these components in hello [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>

<span data-ttu-id="1b89a-126">**圖 1： 使用 HYPER-V 站台 tooAzure 複寫**</span><span class="sxs-lookup"><span data-stu-id="1b89a-126">**Figure 1: Hyper-V site tooAzure replication**</span></span>

![元件](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a><span data-ttu-id="1b89a-128">複寫程序</span><span class="sxs-lookup"><span data-stu-id="1b89a-128">Replication process</span></span>

<span data-ttu-id="1b89a-129">**HYPER-V 複寫 tooAzure 如圖 2： 複寫和復原程序**</span><span class="sxs-lookup"><span data-stu-id="1b89a-129">**Figure 2: Replication and recovery process for Hyper-V replication tooAzure**</span></span>

![工作流程](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a><span data-ttu-id="1b89a-131">啟用保護。</span><span class="sxs-lookup"><span data-stu-id="1b89a-131">Enable protection</span></span>

1. <span data-ttu-id="1b89a-132">您針對 HYPER-V 虛擬機器啟用保護之後，在 hello Azure 入口網站或內部部署，hello**啟用保護**啟動。</span><span class="sxs-lookup"><span data-stu-id="1b89a-132">After you enable protection for a Hyper-V VM, in hello Azure portal or on-premises, hello **Enable protection** starts.</span></span>
2. <span data-ttu-id="1b89a-133">hello 工作會檢查該 hello 機器符合必要條件，再叫用 hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)，tooset hello 設定已設定的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="1b89a-133">hello job checks that hello machine complies with prerequisites, before invoking hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset up replication with hello settings you've configured.</span></span>
3. <span data-ttu-id="1b89a-134">hello 工作所叫用 hello 啟動初始複寫[StartReplication](https://msdn.microsoft.com/library/hh850303.aspx)方法、 tooinitialize 完整的 VM 複寫，以及傳送嗨 VM 的虛擬磁碟 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1b89a-134">hello job starts initial replication by invoking hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) method, tooinitialize a full VM replication, and send hello VM's virtual disks tooAzure.</span></span>
4. <span data-ttu-id="1b89a-135">您可以監視 hello 作業在 hello**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1b89a-135">You can monitor hello job in hello **Jobs** tab.</span></span>
 
### <a name="replicate-hello-initial-data"></a><span data-ttu-id="1b89a-136">Hello 初始資料複寫</span><span class="sxs-lookup"><span data-stu-id="1b89a-136">Replicate hello initial data</span></span>

1. <span data-ttu-id="1b89a-137">系統會在初始複寫觸發時擷取 [Hyper-V VM 快照集](https://technet.microsoft.com/library/dd560637.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-137">A [Hyper-V VM snapshot](https://technet.microsoft.com/library/dd560637.aspx) snapshot is taken when initial replication is triggered.</span></span>
2. <span data-ttu-id="1b89a-138">虛擬硬碟才是所有的複製的 tooAzure 複寫的一個。</span><span class="sxs-lookup"><span data-stu-id="1b89a-138">Virtual hard disks are replicated one by one until they're all copied tooAzure.</span></span> <span data-ttu-id="1b89a-139">它可能需要一些時間，視 hello VM 大小和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="1b89a-139">It could take a while, depending on hello VM size, and network bandwidth.</span></span> <span data-ttu-id="1b89a-140">toooptimize 網路使用量，請參閱[如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-140">toooptimize your network usage, see [How toomanage on-premises tooAzure protection network bandwidth usage](https://support.microsoft.com/kb/3056159).</span></span>
3. <span data-ttu-id="1b89a-141">如果磁碟上的變更會發生初始複寫正在進行時，hello HYPER-V 複本複寫追蹤器會追蹤這些變更為 HYPER-V 複寫記錄檔 (.hrl)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-141">If disk changes occur while initial replication is in progress, hello Hyper-V Replica Replication Tracker tracks those changes as Hyper-V Replication Logs (.hrl).</span></span> <span data-ttu-id="1b89a-142">這些檔案位在 hello 與 hello 磁碟相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1b89a-142">These files are located in hello same folder as hello disks.</span></span> <span data-ttu-id="1b89a-143">每個磁碟具有相關聯的.hrl 檔案傳送 toosecondary 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1b89a-143">Each disk has an associated .hrl file that will be sent toosecondary storage.</span></span>
4. <span data-ttu-id="1b89a-144">初始複寫正在進行時，hello 快照集和記錄檔會消耗磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="1b89a-144">hello snapshot and log files consume disk resources while initial replication is in progress.</span></span>
5. <span data-ttu-id="1b89a-145">Hello 初始複寫完成時，會刪除 hello VM 快照集。</span><span class="sxs-lookup"><span data-stu-id="1b89a-145">When hello initial replication finishes, hello VM snapshot is deleted.</span></span> <span data-ttu-id="1b89a-146">Hello 記錄檔中的差異磁碟變更為已同步處理和合併 toohello 父系磁碟。</span><span class="sxs-lookup"><span data-stu-id="1b89a-146">Delta disk changes in hello log are synchronized and merged toohello parent disk.</span></span>


### <a name="finalize-protection"></a><span data-ttu-id="1b89a-147">完成保護</span><span class="sxs-lookup"><span data-stu-id="1b89a-147">Finalize protection</span></span>

1. <span data-ttu-id="1b89a-148">Hello 初始複寫完成，hello 之後**完成 hello 虛擬機器上的保護**作業設定網路和其他複寫後續設定，以便 hello 虛擬機器時保護。</span><span class="sxs-lookup"><span data-stu-id="1b89a-148">After hello initial replication finishes, hello **Finalize protection on hello virtual machine** job configures network and other post-replication settings, so that hello virtual machine is protected.</span></span>
2. <span data-ttu-id="1b89a-149">如果您要複寫 tooAzure，您可能需要 tootweak hello 設定 hello 虛擬機器，讓它準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1b89a-149">If you're replicating tooAzure, you might need tootweak hello settings for hello virtual machine so that it's ready for failover.</span></span> <span data-ttu-id="1b89a-150">此時，您可以執行測試容錯移轉 toocheck 一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="1b89a-150">At this point you can run a test failover toocheck everything is working as expected.</span></span>

### <a name="replicate-hello-delta"></a><span data-ttu-id="1b89a-151">複寫 hello 差異</span><span class="sxs-lookup"><span data-stu-id="1b89a-151">Replicate hello delta</span></span>

1. <span data-ttu-id="1b89a-152">Hello 初始複寫之後，差異同步處理開始時，根據複寫設定。</span><span class="sxs-lookup"><span data-stu-id="1b89a-152">After hello initial replication, delta synchronization begins, in accordance with replication settings.</span></span>
2. <span data-ttu-id="1b89a-153">hello HYPER-V 複本複寫追蹤器會為.hrl 檔案追蹤 hello 變更 tooa 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="1b89a-153">hello Hyper-V Replica Replication Tracker tracks hello changes tooa virtual hard disk as .hrl files.</span></span> <span data-ttu-id="1b89a-154">每個設定用於複寫的磁碟都會有相關聯的 .hrl 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b89a-154">Each disk that's configured for replication has an associated .hrl file.</span></span> <span data-ttu-id="1b89a-155">此記錄檔會在初始複寫完成之後傳送 toohello 客戶儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b89a-155">This log is sent toohello customer's storage account after initial replication is complete.</span></span> <span data-ttu-id="1b89a-156">在另一個記錄檔，在 hello 傳輸 tooAzure 記錄時，會追蹤 hello 變更 hello 主要磁碟相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b89a-156">When a log is in transit tooAzure, hello changes in hello primary disk are tracked in another log file, in hello same directory.</span></span>
3. <span data-ttu-id="1b89a-157">初始和差異在複寫期間，您可以監視 hello VM 檢視中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1b89a-157">During initial and delta replication, you can monitor hello VM in hello VM view.</span></span> <span data-ttu-id="1b89a-158">[深入了解](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-158">[Learn more](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span></span>  

### <a name="synchronize-replication"></a><span data-ttu-id="1b89a-159">同步處理複寫</span><span class="sxs-lookup"><span data-stu-id="1b89a-159">Synchronize replication</span></span>

1. <span data-ttu-id="1b89a-160">如果差異複寫失敗且完整複寫因為頻寬或時間需要大量成本，就會將 VM 標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="1b89a-160">If delta replication fails, and a full replication would be costly in terms of bandwidth or time, then a VM is marked for resynchronization.</span></span> <span data-ttu-id="1b89a-161">例如，如果 hello.hrl 檔案到達 hello 磁碟大小的 50%，然後 hello VM 將會標示為重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="1b89a-161">For example, if hello .hrl files reach 50% of hello disk size, then hello VM will be marked for resynchronization.</span></span>
2.  <span data-ttu-id="1b89a-162">重新同步處理將 hello 會計算總和檢查碼的 hello 的來源和目標虛擬機器，並傳送 hello 差異資料傳送的資料量降到最低。</span><span class="sxs-lookup"><span data-stu-id="1b89a-162">Resynchronization minimizes hello amount of data sent by computing checksums of hello source and target virtual machines, and sending only hello delta data.</span></span> <span data-ttu-id="1b89a-163">重新同步處理會使用固定區塊的區塊處理演算法，將來源和目標檔案分成固定區塊。</span><span class="sxs-lookup"><span data-stu-id="1b89a-163">Resynchronization uses a fixed-block chunking algorithm where source and target files are divided into fixed chunks.</span></span> <span data-ttu-id="1b89a-164">總和檢查碼的每個區塊產生，則會比較，它會封鎖從 hello 來源需要 toobe 套用的 toohello 目標 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="1b89a-164">Checksums for each chunk are generated and then compared toodetermine which blocks from hello source need toobe applied toohello target.</span></span>
3. <span data-ttu-id="1b89a-165">重新同步處理完成之後，應會繼續進行正常的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="1b89a-165">After resynchronization finishes, normal delta replication should resume.</span></span> <span data-ttu-id="1b89a-166">預設重新同步處理排程的 toorun 自動外上班時間時，但是您可以手動重新同步虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1b89a-166">By default resynchronization is scheduled toorun automatically outside office hours, but you can resynchronize a virtual machine manually.</span></span> <span data-ttu-id="1b89a-167">例如，若發生網路中斷或其他中斷情形，您可以繼續重新同步處理。</span><span class="sxs-lookup"><span data-stu-id="1b89a-167">For example, you can resume resynchronization if a network outage or another outage occurs.</span></span> <span data-ttu-id="1b89a-168">toodo hello 入口網站中的，選取 hello VM >**重新同步處理**。</span><span class="sxs-lookup"><span data-stu-id="1b89a-168">toodo this, select hello VM in hello portal > **Resynchronize**.</span></span>

    ![手動重新同步處理](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a><span data-ttu-id="1b89a-170">重試邏輯</span><span class="sxs-lookup"><span data-stu-id="1b89a-170">Retry logic</span></span>

<span data-ttu-id="1b89a-171">如果發生複寫錯誤，會有內建的重試。</span><span class="sxs-lookup"><span data-stu-id="1b89a-171">If a replication error occurs, there's a built-in retry.</span></span> <span data-ttu-id="1b89a-172">此邏輯可分為以下兩種類別：</span><span class="sxs-lookup"><span data-stu-id="1b89a-172">This logic can be classified into two categories:</span></span>

<span data-ttu-id="1b89a-173">**類別**</span><span class="sxs-lookup"><span data-stu-id="1b89a-173">**Category**</span></span> | <span data-ttu-id="1b89a-174">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="1b89a-174">**Details**</span></span>
--- | ---
<span data-ttu-id="1b89a-175">**無法復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="1b89a-175">**Non-recoverable errors**</span></span> | <span data-ttu-id="1b89a-176">不嘗試重試。</span><span class="sxs-lookup"><span data-stu-id="1b89a-176">No retry is attempted.</span></span> <span data-ttu-id="1b89a-177">VM 狀態為**重大**，需要管理員介入處理。</span><span class="sxs-lookup"><span data-stu-id="1b89a-177">VM status will be **Critical**, and administrator intervention is required.</span></span> <span data-ttu-id="1b89a-178">這些錯誤的範例包括： 中斷 VHD 鏈結。Hello 複本 VM; 無效的狀態網路驗證錯誤： 授權錯誤。找不到錯誤 （適用於獨立 HYPER-V 伺服器） 的 VM</span><span class="sxs-lookup"><span data-stu-id="1b89a-178">Examples of these errors include: broken VHD chain; Invalid state for hello replica VM; Network authentication errors: authorization errors; VM not found errors (for standalone Hyper-V servers)</span></span>
<span data-ttu-id="1b89a-179">**可復原的錯誤**</span><span class="sxs-lookup"><span data-stu-id="1b89a-179">**Recoverable errors**</span></span> | <span data-ttu-id="1b89a-180">產生每個複寫間隔，使用指數型撤退，從而 hello 從 hello 開頭的 1、 2、 4、 8、 hello 第一次嘗試的重試間隔和 10 分鐘重試作業。</span><span class="sxs-lookup"><span data-stu-id="1b89a-180">Retries occur every replication interval, using an exponential back-off that increases hello retry interval from hello start of hello first attempt by 1, 2, 4, 8, and 10 minutes.</span></span> <span data-ttu-id="1b89a-181">如果錯誤持續發生，會每隔 30 分鐘重試一次。</span><span class="sxs-lookup"><span data-stu-id="1b89a-181">If an error persists, retry every 30 minutes.</span></span> <span data-ttu-id="1b89a-182">範例包括：網路錯誤；磁碟空間不足錯誤；記憶體不足情況</span><span class="sxs-lookup"><span data-stu-id="1b89a-182">Examples include: network errors; low disk  errors; low memory conditions</span></span> |



## <a name="failover-and-failback-process"></a><span data-ttu-id="1b89a-183">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="1b89a-183">Failover and failback process</span></span>

1. <span data-ttu-id="1b89a-184">您可以執行的已規劃或未規劃[容錯移轉](site-recovery-failover.md)從內部部署 HYPER-V Vm tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1b89a-184">You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs tooAzure.</span></span> <span data-ttu-id="1b89a-185">如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="1b89a-185">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="1b89a-186">您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。</span><span class="sxs-lookup"><span data-stu-id="1b89a-186">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="1b89a-187">執行 hello 容錯移轉之後，您應該在 Azure 中建立複本 Vm 可以 toosee hello。</span><span class="sxs-lookup"><span data-stu-id="1b89a-187">After you run hello failover, you should be able toosee hello created replica VMs in Azure.</span></span> <span data-ttu-id="1b89a-188">如果需要，您可以指定公用 IP 位址 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1b89a-188">You can assign a public IP address toohello VM if required.</span></span>
5. <span data-ttu-id="1b89a-189">然後，您就會認可 hello 容錯移轉 toostart 從 hello 複本 Azure VM 存取 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="1b89a-189">You then commit hello failover toostart accessing hello workload from hello replica Azure VM.</span></span>
6. <span data-ttu-id="1b89a-190">當主要的內部部署網站恢復可用狀態時，您就可以[容錯回復](site-recovery-failback-from-azure-to-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="1b89a-190">When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md).</span></span> <span data-ttu-id="1b89a-191">您開始進行規劃的容錯移轉，從 Azure toohello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="1b89a-191">You kick off a planned failover from Azure toohello primary site.</span></span> <span data-ttu-id="1b89a-192">規劃的容錯移轉，您可以選取 toofailback toohello 相同 VM 或 tooan 替代位置，並同步處理變更 Azure 和內部部署、 tooensure 之間不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="1b89a-192">For a planned failover you can select toofailback toohello same VM or tooan alternate location, and synchronize changes between Azure and on-premises, tooensure no data loss.</span></span> <span data-ttu-id="1b89a-193">Vm 建立時在內部部署，您就會認可 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1b89a-193">When VMs are created on-premises, you commit hello failover.</span></span>




## <a name="next-steps"></a><span data-ttu-id="1b89a-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b89a-194">Next steps</span></span>

<span data-ttu-id="1b89a-195">跳過[步驟 2： 檢閱 hello 部署必要條件](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1b89a-195">Go too[Step 2: Review hello deployment prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>
