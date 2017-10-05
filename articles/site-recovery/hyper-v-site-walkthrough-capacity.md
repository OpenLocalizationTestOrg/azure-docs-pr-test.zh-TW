---
title: "使用 Azure Site Recovery 規劃產能並調整 Hyper-V VM 複寫 (不含 VMM) 至 Azure | Microsoft Docs"
description: "使用 Azure Site Recovery 將 Hyper-V VM 複寫至 Azure 時，請使用本文規劃產能和調整"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="3a448-103">步驟 3：規劃產能並調整 Hyper-V 對 Azure 的複寫</span><span class="sxs-lookup"><span data-stu-id="3a448-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="3a448-104">使用這份文件找出在將內部部署 Hyper-V VM (不含 System Center VMM) 複寫至 Azure 時，使用 [Azure Site Recovery](site-recovery-overview.md) 規劃產能和調整的方法。</span><span class="sxs-lookup"><span data-stu-id="3a448-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="3a448-105">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="3a448-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="3a448-106">如何開始容量規劃？</span><span class="sxs-lookup"><span data-stu-id="3a448-106">How do I start capacity planning?</span></span>


<span data-ttu-id="3a448-107">您需收集複寫環境的相關資訊，然後使用此資訊搭配本文中強調的考量事項來規劃容量。</span><span class="sxs-lookup"><span data-stu-id="3a448-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="3a448-108">收集資訊</span><span class="sxs-lookup"><span data-stu-id="3a448-108">Gather information</span></span>

1. <span data-ttu-id="3a448-109">收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。</span><span class="sxs-lookup"><span data-stu-id="3a448-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="3a448-110">識別複寫資料的每日變更 (流失) 率。</span><span class="sxs-lookup"><span data-stu-id="3a448-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="3a448-111">請下載 [Hyper-V 容量規劃工具](https://www.microsoft.com/download/details.aspx?id=39057)來取得變更率。</span><span class="sxs-lookup"><span data-stu-id="3a448-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="3a448-112">我們建議您執行此工具一週以上的時間來擷取平均值。</span><span class="sxs-lookup"><span data-stu-id="3a448-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="3a448-113">找出產能</span><span class="sxs-lookup"><span data-stu-id="3a448-113">Figure out capacity</span></span>

<span data-ttu-id="3a448-114">以您所收集的資訊作為基礎，執行 [Site Recovery Capacity Planner 工具](http://aka.ms/asr-capacity-planner-excel)來分析您的來源環境和工作負載，並且評估來源位置的頻寬需求和伺服器資源，以及在目標位置所需的資源 (虛擬機器和儲存體等等)。</span><span class="sxs-lookup"><span data-stu-id="3a448-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="3a448-115">有幾種模式可讓您執行工具：</span><span class="sxs-lookup"><span data-stu-id="3a448-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="3a448-116">快速規劃：在此模式中執行工具，以 VM、磁碟、儲存體及變更率的平均數作為基礎，取得網路與伺服器的預測。</span><span class="sxs-lookup"><span data-stu-id="3a448-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="3a448-117">詳細規劃：在此模式中執行工具，提供每個工作負載的 VM 層級詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3a448-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="3a448-118">分析 VM 相容性，並取得網路和伺服器預測。</span><span class="sxs-lookup"><span data-stu-id="3a448-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="3a448-119">現在執行工具：</span><span class="sxs-lookup"><span data-stu-id="3a448-119">Now run the tool:</span></span>

1. <span data-ttu-id="3a448-120">下載[工具](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="3a448-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="3a448-121">若要執行快速規劃，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-quick-planner)，並選取 **Hyper-V 至 Azure** 情節。</span><span class="sxs-lookup"><span data-stu-id="3a448-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="3a448-122">若要執行詳細規劃，請遵循[這些指示](site-recovery-capacity-planner.md#run-the-detailed-planner)，並選取 **Hyper-V 至 Azure** 情節。</span><span class="sxs-lookup"><span data-stu-id="3a448-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="3a448-123">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="3a448-123">Control network bandwidth</span></span>

<span data-ttu-id="3a448-124">在計算您所需要的頻寬之後，您會有幾個選項可控制用於複寫的頻寬數量：</span><span class="sxs-lookup"><span data-stu-id="3a448-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="3a448-125">**節流頻寬**︰複寫至 Azure 的 Hyper-V 流量會經過特定的 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="3a448-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="3a448-126">您可以在主機伺服器上進行頻寬節流。</span><span class="sxs-lookup"><span data-stu-id="3a448-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="3a448-127">**影響頻寬**︰您可以使用幾個登錄機碼來影響用於複寫的頻寬。</span><span class="sxs-lookup"><span data-stu-id="3a448-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="3a448-128">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="3a448-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="3a448-129">在 Hyper-V 主機伺服器上開啟 Microsoft Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="3a448-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="3a448-130">根據預設，Microsoft Azure 備份的捷徑位於桌面上或在 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin 中。</span><span class="sxs-lookup"><span data-stu-id="3a448-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="3a448-131">在嵌入式管理單元中，按一下 [變更屬性] 。</span><span class="sxs-lookup"><span data-stu-id="3a448-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="3a448-132">在 [節流] 索引標籤上，選取 [啟用備份操作的網際網路頻寬使用節流設定]，然後設定工作和非工作時數的限制。</span><span class="sxs-lookup"><span data-stu-id="3a448-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="3a448-133">有效範圍是每秒 512 Kbps 到 102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="3a448-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![節流頻寬](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="3a448-135">您也可以使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) Cmdlet 來設定節流。</span><span class="sxs-lookup"><span data-stu-id="3a448-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="3a448-136">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="3a448-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="3a448-137">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="3a448-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="3a448-138">影響網路頻寬</span><span class="sxs-lookup"><span data-stu-id="3a448-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="3a448-139">在登錄中瀏覽至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="3a448-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="3a448-140">若要影響複製磁碟上的頻寬流量，請修改 **UploadThreadsPerVM**的值，如果不存在則請建立機碼。</span><span class="sxs-lookup"><span data-stu-id="3a448-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="3a448-141">若要影響從 Azure 容錯回復流量的頻寬，請修改 **DownloadThreadsPerVM**的值。</span><span class="sxs-lookup"><span data-stu-id="3a448-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="3a448-142">預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="3a448-142">The default value is 4.</span></span> <span data-ttu-id="3a448-143">在 “overprovisioned” 網路中，這些登錄機碼必須變更自其預設值。</span><span class="sxs-lookup"><span data-stu-id="3a448-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="3a448-144">最大值為 32。</span><span class="sxs-lookup"><span data-stu-id="3a448-144">The maximum is 32.</span></span> <span data-ttu-id="3a448-145">監視流量，將此值最佳化。</span><span class="sxs-lookup"><span data-stu-id="3a448-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a448-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a448-146">Next steps</span></span>

<span data-ttu-id="3a448-147">移至[步驟 4：規劃網路](hyper-v-site-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="3a448-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
