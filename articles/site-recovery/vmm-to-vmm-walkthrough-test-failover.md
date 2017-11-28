---
title: "aaaRun 測試容錯移轉的 HYPER-V 虛擬機器複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "說明如何測試容錯移轉的 HYPER-V 虛擬機器複寫 tooa toorun 次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="e5555-103">步驟 10： 執行測試容錯移轉的 HYPER-V 複寫 tooa 次要站台</span><span class="sxs-lookup"><span data-stu-id="e5555-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="e5555-104">使用啟用為 HYPER-V 虛擬機器 (Vm) 的複寫之後[Azure Site Recovery](site-recovery-overview.md)，使用此發行項 toorun 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e5555-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="e5555-105">測試容錯移轉會驗證該複寫是否正常運作，且不會影響您的生產環境。</span><span class="sxs-lookup"><span data-stu-id="e5555-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="e5555-106">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="e5555-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="e5555-107">開始之前</span><span class="sxs-lookup"><span data-stu-id="e5555-107">Before you start</span></span>

- <span data-ttu-id="e5555-108">當您正在觸發測試容錯移轉時，您可以指定 hello 網路 toowhich hello 測試複本 Vm 會連線。</span><span class="sxs-lookup"><span data-stu-id="e5555-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="e5555-109">[進一步了解](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery)需 hello 網路選項。</span><span class="sxs-lookup"><span data-stu-id="e5555-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="e5555-110">我們建議您不要選擇您在網路對應期間選取的網路。</span><span class="sxs-lookup"><span data-stu-id="e5555-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="e5555-111">本文章中的 hello 指示說明如何容錯移轉的單一 VM toofail。</span><span class="sxs-lookup"><span data-stu-id="e5555-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="e5555-112">閱讀有關[建立復原計劃](site-recovery-create-recovery-plans.md)如果您想 toofail 透過多個 Vm 在一起。</span><span class="sxs-lookup"><span data-stu-id="e5555-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="e5555-113">閱讀＜[測試容錯移轉的限制](site-recovery-test-failover-vmm-to-vmm.md#things-to-note)＞。</span><span class="sxs-lookup"><span data-stu-id="e5555-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="e5555-114">hello tooa VM 指定測試容錯移轉期間的 IP 位址為 hello 規劃或未規劃的容錯移轉 （假設 hello IP 位址可供 hello 測試容錯移轉網路中） 將會收到 hello VM 的同一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e5555-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="e5555-115">如果 hello IP 位址不可用在 hello 測試容錯移轉網路，hello VM 將會收到另一個用於 hello 測試容錯移轉網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e5555-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="e5555-116">如果您想 toodo 測試容錯移轉您的生產網路中的端對端網路連線電腦的完整驗證，請注意:</span><span class="sxs-lookup"><span data-stu-id="e5555-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="e5555-117">hello 主要 VM 關機時您所做 hello 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e5555-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="e5555-118">否則，兩個 Vm hello hello 將會執行相同的身分識別與相同網路 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="e5555-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="e5555-119">如果您進行變更 tootest Vm 時，會失去這些變更清除 hello 測試容錯移轉時。</span><span class="sxs-lookup"><span data-stu-id="e5555-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="e5555-120">這些變更不會複寫後 toohello 主要 VM。</span><span class="sxs-lookup"><span data-stu-id="e5555-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="e5555-121">測試生產網路會導致 toodowntime 生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="e5555-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="e5555-122">要求使用者不 toouse hello 應用程式時 hello 災害復原訓練正在進行中。</span><span class="sxs-lookup"><span data-stu-id="e5555-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="e5555-123">執行 VM 的測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="e5555-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="e5555-124">容錯移轉的單一 VM，toofail 中**複寫的項目**，按一下 hello VM >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="e5555-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="e5555-125">在**測試容錯移轉**，指定如何測試 Vm 後，即可連接的 toonetworks hello 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e5555-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="e5555-126">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e5555-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="e5555-127">追蹤進度 hello**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e5555-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="e5555-128">容錯移轉已完成之後，請確認該 hello 測試 Vm 啟動成功。</span><span class="sxs-lookup"><span data-stu-id="e5555-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="e5555-129">當您完成時，按一下**清除測試容錯移轉**hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="e5555-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="e5555-130">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="e5555-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="e5555-131">此步驟會刪除 hello 虛擬機器和測試容錯移轉期間所建立的網路。</span><span class="sxs-lookup"><span data-stu-id="e5555-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5555-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5555-132">Next steps</span></span>

<span data-ttu-id="e5555-133">測試過 hello 部署之後，深入了解其他類型的[容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="e5555-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
