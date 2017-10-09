---
title: "HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 的 aaaReview hello 架構 |Microsoft 文件"
description: "本文章會提供用來複寫在內部部署 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery hello 架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="40a5a-103">步驟 1： 檢閱 HYPER-V 複寫 tooa 次要站台的 hello 架構</span><span class="sxs-lookup"><span data-stu-id="40a5a-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="40a5a-104">本文說明 hello 元件和複寫時所涉及程序內部使用 hello tooa 次要 VMM 站台 System Center Virtual Machine Manager (VMM) 雲端中的 HYPER-V 虛擬機器 (Vm) [Azure Site Recovery](site-recovery-overview.md)hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="40a5a-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="40a5a-105">在本文中，或在 hello hello 下方張貼的任何註解[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="40a5a-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="40a5a-106">架構元件</span><span class="sxs-lookup"><span data-stu-id="40a5a-106">Architectural components</span></span>

<span data-ttu-id="40a5a-107">以下是您需要複寫 HYPER-V Vm tooa 次要 VMM 站台。</span><span class="sxs-lookup"><span data-stu-id="40a5a-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="40a5a-108">**元件**</span><span class="sxs-lookup"><span data-stu-id="40a5a-108">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="40a5a-110">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="40a5a-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="40a5a-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="40a5a-111">**Azure**</span></span> | <span data-ttu-id="40a5a-112">Azure 中的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="40a5a-112">Subscription in Azure.</span></span> | <span data-ttu-id="40a5a-113">您在 hello Azure 訂用帳戶，tooorchestrate 中建立的復原服務保存庫和管理 VMM 位置之間的複寫。</span><span class="sxs-lookup"><span data-stu-id="40a5a-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="40a5a-114">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="40a5a-114">**VMM server**</span></span> | <span data-ttu-id="40a5a-115">您需要 VMM 主要和次要位置。</span><span class="sxs-lookup"><span data-stu-id="40a5a-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="40a5a-116">我們建議您在 hello 主要站台 VMM 伺服器，一個在 hello 次要站台</span><span class="sxs-lookup"><span data-stu-id="40a5a-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="40a5a-117">**Hyper-V 伺服器**</span><span class="sxs-lookup"><span data-stu-id="40a5a-117">**Hyper-V server**</span></span> |  <span data-ttu-id="40a5a-118">一或多個 HYPER-V 主機伺服器 hello 主要和次要 VMM 雲端中。</span><span class="sxs-lookup"><span data-stu-id="40a5a-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="40a5a-119">Hello LAN 或 VPN，使用 Kerberos 或憑證驗證的 hello 主要和次要 HYPER-V 主機伺服器之間複寫資料。</span><span class="sxs-lookup"><span data-stu-id="40a5a-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="40a5a-120">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="40a5a-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="40a5a-121">在 Hyper-V 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="40a5a-121">On Hyper-V host server.</span></span> | <span data-ttu-id="40a5a-122">hello 來源主機伺服器應該有至少一個 VM 的 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="40a5a-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="40a5a-123">複寫程序</span><span class="sxs-lookup"><span data-stu-id="40a5a-123">Replication process</span></span>

1. <span data-ttu-id="40a5a-124">您設定 hello Azure 帳戶、 建立復原服務保存庫，並指定您想要 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="40a5a-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="40a5a-125">您設定 hello 來源和目標複寫設定，包括 hello Azure Site Recovery Provider 安裝 VMM 伺服器和每個 HYPER-V 主機上的 hello Microsoft Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="40a5a-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="40a5a-126">您建立 hello 來源 VMM 雲端的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="40a5a-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="40a5a-127">hello 原則會套用的 tooall 位於 hello 雲端中的主機上的 Vm。</span><span class="sxs-lookup"><span data-stu-id="40a5a-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="40a5a-128">您為每個 VMM 中啟用，並會依據您選擇的 hello 設定的 VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="40a5a-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="40a5a-129">初始複寫之後，就會開始複寫差異變更。</span><span class="sxs-lookup"><span data-stu-id="40a5a-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="40a5a-130">項目的追蹤變更會保存在 .hrl 檔案中。</span><span class="sxs-lookup"><span data-stu-id="40a5a-130">Tracked changes for an item are held in a .hrl file.</span></span>


![在內部部署內部部署 tooon](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="40a5a-132">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="40a5a-132">Failover and failback process</span></span>

1. <span data-ttu-id="40a5a-133">您可以在內部部署網站間執行計劃性或非計劃性的[容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="40a5a-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="40a5a-134">如果您執行規劃的容錯移轉，則來源 Vm 會關閉 tooensure 遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="40a5a-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="40a5a-135">您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)tooorchestrate 容錯移轉的多部電腦。</span><span class="sxs-lookup"><span data-stu-id="40a5a-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="40a5a-136">如果您執行未規劃的容錯移轉 tooa 次要站台之後在 hello 次要位置中的 hello 容錯移轉機器未啟用保護或複寫。</span><span class="sxs-lookup"><span data-stu-id="40a5a-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="40a5a-137">如果您已規劃的容錯移轉，執行 hello 容錯移轉之後，會受到保護 hello 次要位置中的機器。</span><span class="sxs-lookup"><span data-stu-id="40a5a-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="40a5a-138">然後，您會從 hello 複本 VM 認可 hello 容錯移轉 toostart 存取 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="40a5a-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="40a5a-139">您的主要站台再次可用時，會起始反向複寫 tooreplicate 從 hello 次要站台 toohello 主要。</span><span class="sxs-lookup"><span data-stu-id="40a5a-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="40a5a-140">反轉複寫方向將 hello 虛擬機器放置到受保護的狀態，但 hello 次要資料中心仍然是 hello 作用中的位置。</span><span class="sxs-lookup"><span data-stu-id="40a5a-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="40a5a-141">toomake hello 主要站台到 hello 作用中的位置，您起始規劃的容錯移轉，從次要 tooprimary，後面接著另一個的反向複寫。</span><span class="sxs-lookup"><span data-stu-id="40a5a-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="40a5a-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40a5a-142">Next steps</span></span>

<span data-ttu-id="40a5a-143">跳過[步驟 2： 檢閱 hello 必要條件和限制](vmm-to-vmm-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="40a5a-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
