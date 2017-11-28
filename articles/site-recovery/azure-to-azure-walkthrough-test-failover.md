---
title: "測試容錯移轉與 Azure Site Recovery 的 Azure VM 複寫 aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉的 Azure Vm 複寫 tooanother Azure 區域使用 hello Azure Site Recovery 服務的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="f3128-103">步驟 6：執行 Azure VM 複寫的測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f3128-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="f3128-104">您已啟用的 Azure 虛擬機器 (Vm) 複寫之後，請依照本文中，從一個 Azure 區域 tooanother，使用 hello toorun 測試容錯移轉中的 hello 步驟[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="f3128-104">After you've enabled replication for Azure virtual machine (VMs), follow hello steps in this article, toorun test failover from one Azure region tooanother, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="f3128-105">當您完成 hello 發行項時，您應該已經確認與測試容錯移轉時，至少一個 Azure VM 可以容錯移轉 tooyour 次要 Azure 地區。</span><span class="sxs-lookup"><span data-stu-id="f3128-105">When you finish hello article, you should have verified with a test failover, that at least one Azure VM can fail over tooyour secondary Azure region.</span></span> 
- <span data-ttu-id="f3128-106">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="f3128-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="f3128-107">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="f3128-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="f3128-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="f3128-108">Before you start</span></span>

- <span data-ttu-id="f3128-109">在執行測試容錯移轉之前，我們建議您確認 hello VM 內容，然後進行您需要的任何變更。</span><span class="sxs-lookup"><span data-stu-id="f3128-109">Before you run a test failover, we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="f3128-110">您可以存取在 hello VM 屬性**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="f3128-110">You can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="f3128-111">hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="f3128-111">hello **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="f3128-112">建議您針對 hello 測試容錯移轉，而且不要 hello 網路使用不同的 Azure VM 網路 （預設或自訂），設定為實際執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f3128-112">We recommend you use a separate Azure VM network for hello test failover, and not hello network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="f3128-113">hello 測試容錯移轉容錯移轉 Azure Vm （和其存放裝置） toohello 次要 Azure 地區。</span><span class="sxs-lookup"><span data-stu-id="f3128-113">hello test failover fails over Azure VMs (and their storage) toohello secondary Azure region.</span></span> <span data-ttu-id="f3128-114">它不會複寫任何相依的應用程式或資源。</span><span class="sxs-lookup"><span data-stu-id="f3128-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="f3128-115">如果上執行應用程式失敗的 Vm 上有相依於其他資源，例如 Active Directory 或 DNS，您需要 tooreplicate 這些，如果它們不提供次要區域中。</span><span class="sxs-lookup"><span data-stu-id="f3128-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need tooreplicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="f3128-116">深入了解</span><span class="sxs-lookup"><span data-stu-id="f3128-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="f3128-117">如果您想要將 tooaccess 複寫 Vm 從內部部署站台的容錯移轉之後，您需要太[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese Vm。</span><span class="sxs-lookup"><span data-stu-id="f3128-117">If you want tooaccess replicated VMs after failover from an on-premises site, you need too[prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="f3128-118">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f3128-118">Run a test failover</span></span>

1. <span data-ttu-id="f3128-119">在**設定** > **複寫的項目**，按一下 hello VM **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="f3128-119">In **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="f3128-120">在**測試容錯移轉**，選取復原點 toouse hello 容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="f3128-120">In **Test Failover**, Select a recovery point toouse for hello failover:</span></span>

    - <span data-ttu-id="f3128-121">**最新版處理**： 失敗 hello VM toohello 最新復原點上方 hello Site Recovery 服務所處理。</span><span class="sxs-lookup"><span data-stu-id="f3128-121">**Latest processed**: Fails hello VM over toohello latest recovery point that was processed by hello Site Recovery service.</span></span> <span data-ttu-id="f3128-122">會顯示 hello 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="f3128-122">hello time stamp is shown.</span></span> <span data-ttu-id="f3128-123">使用此選項時，無須花費時間處理資料，因此它會提供低 RTO (復原時間目標)。</span><span class="sxs-lookup"><span data-stu-id="f3128-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="f3128-124">**最新的應用程式一致**： 容錯移轉所有 Vm toohello 最新的應用程式一致復原點的這個選項。</span><span class="sxs-lookup"><span data-stu-id="f3128-124">**Latest app-consistent**: This option fails over all VMs toohello latest app-consistent recovery point.</span></span> <span data-ttu-id="f3128-125">會顯示 hello 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="f3128-125">hello time stamp is shown.</span></span> 
    - <span data-ttu-id="f3128-126">**自訂**：選取任何復原點。</span><span class="sxs-lookup"><span data-stu-id="f3128-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="f3128-127">Hello 容錯移轉發生後，將會連接選取 hello 目標 Azure 虛擬網路 toowhich hello 次要區域中的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="f3128-127">Select hello target Azure virtual network toowhich Azure VMs in hello secondary region will be connected, after hello failover occurs.</span></span>
4. <span data-ttu-id="f3128-128">toostart hello 容錯移轉，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f3128-128">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="f3128-129">tootrack 進度，請按一下 hello VM tooopen 其屬性。</span><span class="sxs-lookup"><span data-stu-id="f3128-129">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="f3128-130">或者，您可以按一下 hello**測試容錯移轉**作業在 hello 保存庫名稱 >**設定** > **作業** > **的站台復原工作**.</span><span class="sxs-lookup"><span data-stu-id="f3128-130">Or, you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="f3128-131">Hello 之後容錯移轉完成時，Azure VM 的 hello 複本會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="f3128-131">After hello failover finishes, hello replica Azure VM appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="f3128-132">請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="f3128-132">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="f3128-133">按一下 toodelete hello hello 測試容錯移轉期間所建立的 Vm**清除測試容錯移轉**hello 上複寫項目或 hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="f3128-133">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="f3128-134">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="f3128-134">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="f3128-135">[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f3128-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3128-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3128-136">Next steps</span></span>

<span data-ttu-id="f3128-137">測試容錯移轉之後，即完成本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f3128-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="f3128-138">現在，深入了解在生產環境中執行容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="f3128-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="f3128-139">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="f3128-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="f3128-140">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)容錯移轉多個 VM。</span><span class="sxs-lookup"><span data-stu-id="f3128-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="f3128-141">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="f3128-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="f3128-142">深入了解容錯移轉之後[重新保護 Azure VM](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="f3128-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

