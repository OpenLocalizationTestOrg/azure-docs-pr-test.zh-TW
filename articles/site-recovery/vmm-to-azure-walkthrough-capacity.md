---
title: "aaaPlan 容量與縮放比例為 HYPER-V 虛擬機器與 Azure Site Recovery 的複寫 （VMM) tooAzure |Microsoft 文件"
description: "複寫在 VMM 中的 HYPER-V Vm 雲端 tooAzure，與 Azure Site Recovery 時，使用此發行項 tooplan 容量和小數位數"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="2536d-103">步驟 3： 規劃容量與縮放比例 （使用 VMM) 的 HYPER-V tooAzure 複寫</span><span class="sxs-lookup"><span data-stu-id="2536d-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="2536d-104">您已檢閱過 hello 之後[部署必要條件](vmm-to-azure-walkthrough-prerequisites.md)、 使用容量規劃出此發行項 toofigure 和縮放比例，複寫時在內部部署 HYPER-V Vm 的 System Center Virtual Machine Manager (VMM) 雲端 tooAzure，與[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2536d-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="2536d-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="2536d-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="2536d-106">如何開始容量規劃？</span><span class="sxs-lookup"><span data-stu-id="2536d-106">How do I start capacity planning?</span></span>


<span data-ttu-id="2536d-107">您收集有關您複寫環境，然後使用 hello 的資料與 hello 考量這篇文章中反白顯示的計劃容量資訊。</span><span class="sxs-lookup"><span data-stu-id="2536d-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="2536d-108">收集資訊</span><span class="sxs-lookup"><span data-stu-id="2536d-108">Gather information</span></span>

1. <span data-ttu-id="2536d-109">收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。</span><span class="sxs-lookup"><span data-stu-id="2536d-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="2536d-110">識別複寫資料的每日變更 (流失) 率。</span><span class="sxs-lookup"><span data-stu-id="2536d-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="2536d-111">下載 hello [HYPER-V 容量規劃工具](https://www.microsoft.com/download/details.aspx?id=39057)tooget hello 變更率。</span><span class="sxs-lookup"><span data-stu-id="2536d-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="2536d-112">我們建議您執行此工具透過週 toocapture 平均值。</span><span class="sxs-lookup"><span data-stu-id="2536d-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="2536d-113">找出產能</span><span class="sxs-lookup"><span data-stu-id="2536d-113">Figure out capacity</span></span>

<span data-ttu-id="2536d-114">根據已收集的 hello 資訊，您執行 hello[站台復原產能規劃工具](http://aka.ms/asr-capacity-planner-excel)tooanalyze 您的來源環境和工作負載，估計頻寬需求和伺服器 hello 來源位置，資源和 hello資源 （虛擬機器和存放裝置等等），您需要在 hello 目標位置。</span><span class="sxs-lookup"><span data-stu-id="2536d-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="2536d-115">您可以透過幾種模式來執行 hello 工具：</span><span class="sxs-lookup"><span data-stu-id="2536d-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="2536d-116">快速的計劃： hello 工具以此模式執行的 tooget 網路和伺服器投影根據 Vm、 磁碟、 存放裝置和變更速率平均數目。</span><span class="sxs-lookup"><span data-stu-id="2536d-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="2536d-117">詳細的規劃： 在此模式中，執行 hello 工具，並提供每個工作負載在 VM 層級的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2536d-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="2536d-118">分析 VM 相容性，並取得網路和伺服器預測。</span><span class="sxs-lookup"><span data-stu-id="2536d-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="2536d-119">現在執行 hello 工具：</span><span class="sxs-lookup"><span data-stu-id="2536d-119">Now run hello tool:</span></span>

1. <span data-ttu-id="2536d-120">下載 hello[工具](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="2536d-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="2536d-121">toorun hello 快速規劃中，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-quick-planner)，並選取 hello 案例**HYPER-V tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="2536d-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="2536d-122">toorun hello 詳細的規劃，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-detailed-planner)，並選取 hello 案例**HYPER-V tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="2536d-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="2536d-123">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="2536d-123">Control network bandwidth</span></span>

<span data-ttu-id="2536d-124">您需要的導出的 hello 頻寬之後，您會有幾個選項用於複寫的頻寬控制 hello 量：</span><span class="sxs-lookup"><span data-stu-id="2536d-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="2536d-125">**節流的頻寬**: HYPER-V 複寫 tooAzure 流量透過特定的 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="2536d-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="2536d-126">您可以節流處理 hello 主機伺服器上的頻寬。</span><span class="sxs-lookup"><span data-stu-id="2536d-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="2536d-127">**影響頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="2536d-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="2536d-128">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="2536d-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="2536d-129">開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="2536d-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="2536d-130">依預設 Microsoft Azure 備份的捷徑。 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin</span><span class="sxs-lookup"><span data-stu-id="2536d-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="2536d-131">在 [hello] 嵌入式管理單元中按一下**變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="2536d-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="2536d-132">在 hello**節流**索引標籤上選取**啟用網際網路頻寬使用節流設定的備份操作**，並設定工作的 hello 限制和非工作小時。</span><span class="sxs-lookup"><span data-stu-id="2536d-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="2536d-133">有效範圍是從每秒 512 Kbps too102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="2536d-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![節流頻寬](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="2536d-135">您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。</span><span class="sxs-lookup"><span data-stu-id="2536d-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="2536d-136">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="2536d-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="2536d-137">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="2536d-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="2536d-138">影響網路頻寬</span><span class="sxs-lookup"><span data-stu-id="2536d-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="2536d-139">Hello 登錄中瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="2536d-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="2536d-140">tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值 hello **UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="2536d-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="2536d-141">從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。</span><span class="sxs-lookup"><span data-stu-id="2536d-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="2536d-142">hello 預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="2536d-142">hello default value is 4.</span></span> <span data-ttu-id="2536d-143">在 「 超量佈建 」 的網路中，應該從 hello 預設值變更這些登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="2536d-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="2536d-144">hello 上限為 32。</span><span class="sxs-lookup"><span data-stu-id="2536d-144">hello maximum is 32.</span></span> <span data-ttu-id="2536d-145">監視流量 toooptimize hello 值。</span><span class="sxs-lookup"><span data-stu-id="2536d-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2536d-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2536d-146">Next steps</span></span>

<span data-ttu-id="2536d-147">跳過[步驟 4： 規劃網路](vmm-to-azure-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="2536d-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
