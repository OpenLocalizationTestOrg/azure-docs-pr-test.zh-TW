---
title: "aaaHow 未在 Azure Site Recovery 的 Azure 區域工作之間的 Azure 虛擬機器複寫嗎？  | Microsoft Docs"
description: "本文提供元件和複寫使用 hello Azure Site Recovery 服務的 Azure 區域之間的 Azure Vm 時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="ae27f-104">Azure VM 複寫如何在 Site Recovery 中運作？</span><span class="sxs-lookup"><span data-stu-id="ae27f-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="ae27f-105">本文說明 hello 元件和處理序中複製及復原 Azure 虛擬機器 (Vm) 從一個區域 tooanother 涉及使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="ae27f-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="ae27f-106">Azure VM 複寫以 hello Site Recovery 服務目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ae27f-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="ae27f-107">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="ae27f-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="ae27f-108">架構元件</span><span class="sxs-lookup"><span data-stu-id="ae27f-108">Architectural components</span></span>

<span data-ttu-id="ae27f-109">下列圖表中的 hello 提供 Azure VM 中的環境 （在此範例中，hello 美國東部位置） 的特定區域的高層級檢視。</span><span class="sxs-lookup"><span data-stu-id="ae27f-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="ae27f-110">在 Azure VM 的環境中：</span><span class="sxs-lookup"><span data-stu-id="ae27f-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="ae27f-111">應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae27f-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="ae27f-112">hello Vm 可以包含在虛擬網路內的一個或多個子網路。</span><span class="sxs-lookup"><span data-stu-id="ae27f-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![客戶環境](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="ae27f-114">深入了解 hello 部署必要條件和需求 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ae27f-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="ae27f-115">複寫程序</span><span class="sxs-lookup"><span data-stu-id="ae27f-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="ae27f-116">步驟 1</span><span class="sxs-lookup"><span data-stu-id="ae27f-116">Step 1</span></span>

<span data-ttu-id="ae27f-117">當您啟用 Azure VM 複寫 hello Azure 入口網站中的時，hello 示 hello 下列圖表和資料表會自動建立 hello 目標區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="ae27f-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="ae27f-118">根據預設，會根據來源地區設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="ae27f-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="ae27f-119">您可以自訂所需的 hello 目標設定。</span><span class="sxs-lookup"><span data-stu-id="ae27f-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="ae27f-120">[深入了解](site-recovery-replicate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ae27f-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![啟用複寫程序，步驟 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="ae27f-122">**Resource**</span><span class="sxs-lookup"><span data-stu-id="ae27f-122">**Resource**</span></span> | <span data-ttu-id="ae27f-123">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="ae27f-123">**Details**</span></span>
--- | ---
<span data-ttu-id="ae27f-124">**目標資源群組**</span><span class="sxs-lookup"><span data-stu-id="ae27f-124">**Target resource group**</span></span> | <span data-ttu-id="ae27f-125">hello 複寫的 Vm 屬於容錯移轉之後的資源群組 toowhich。</span><span class="sxs-lookup"><span data-stu-id="ae27f-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="ae27f-126">**目標虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="ae27f-126">**Target virtual network**</span></span> | <span data-ttu-id="ae27f-127">在其中複寫的 Vm 位於容錯移轉之後 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ae27f-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="ae27f-128">在來源和目標的虛擬網路之間會建立網路對應，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ae27f-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="ae27f-129">**快取儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="ae27f-129">**Cache storage accounts**</span></span> | <span data-ttu-id="ae27f-130">來源的 vm 上的變更複寫 toohello 目標儲存體帳戶之前，它們會追蹤並傳送嗨目標位置中 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae27f-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="ae27f-131">這可確保在 hello VM 上執行的實際執行應用程式的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="ae27f-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="ae27f-132">**目標儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="ae27f-132">**Target storage accounts**</span></span>  | <span data-ttu-id="ae27f-133">在 hello 目標位置 toowhich hello 資料的儲存體帳戶會被複寫。</span><span class="sxs-lookup"><span data-stu-id="ae27f-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="ae27f-134">**目標可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="ae27f-134">**Target availability sets**</span></span>  | <span data-ttu-id="ae27f-135">可用性設定組中的 hello 複寫 Vm 位於容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="ae27f-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="ae27f-136">步驟 2</span><span class="sxs-lookup"><span data-stu-id="ae27f-136">Step 2</span></span>

<span data-ttu-id="ae27f-137">因為已啟用複寫，hello Site Recovery 擴充行動服務會自動安裝在 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="ae27f-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="ae27f-138">發生 hello 下列情況：</span><span class="sxs-lookup"><span data-stu-id="ae27f-138">hello following occurs:</span></span>

1. <span data-ttu-id="ae27f-139">hello VM 已向站台復原。</span><span class="sxs-lookup"><span data-stu-id="ae27f-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="ae27f-140">Hello VM 設定連續複寫。</span><span class="sxs-lookup"><span data-stu-id="ae27f-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="ae27f-141">資料寫入 hello VM 磁碟是持續傳送嗨來源位置中的 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae27f-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![啟用複寫程序，步驟 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="ae27f-143">站台復原永遠不需要輸入的連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="ae27f-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="ae27f-144">hello VM 需要的傳出連線 tooSite 復原服務 Url/IP 位址、 Office 365 驗證 Url/IP 位址，並快取儲存體帳戶的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ae27f-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="ae27f-145">如需詳細資訊，請參閱 hello[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ae27f-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="ae27f-146">連續複寫程序</span><span class="sxs-lookup"><span data-stu-id="ae27f-146">Continuous replication process</span></span>

<span data-ttu-id="ae27f-147">連續的複寫運作正常之後，磁碟寫入會立即傳送 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae27f-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="ae27f-148">站台復原處理 hello 資料，並將它傳送 toohello 目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae27f-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="ae27f-149">處理 hello 資料之後，每隔幾分鐘 hello 目標儲存體帳戶會產生復原點。</span><span class="sxs-lookup"><span data-stu-id="ae27f-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="ae27f-150">容錯移轉程序</span><span class="sxs-lookup"><span data-stu-id="ae27f-150">Failover process</span></span>

<span data-ttu-id="ae27f-151">當您起始容錯移轉時，Vm 建立 hello 目標資源群組、 目標虛擬網路、 目標子網路中的 hello 與 hello 目標可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="ae27f-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="ae27f-152">在容錯移轉時，您可以使用任何復原點。</span><span class="sxs-lookup"><span data-stu-id="ae27f-152">During a failover, you can use any recovery point.</span></span>

![容錯移轉程序](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="ae27f-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae27f-154">Next steps</span></span>

- <span data-ttu-id="ae27f-155">深入了解 Azure VM 複寫的[網路](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="ae27f-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="ae27f-156">依照逐步解說太[複寫 Azure Vm。](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="ae27f-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
