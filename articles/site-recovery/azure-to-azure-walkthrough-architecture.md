---
title: "Azure Vm 的 Azure 區域間的複寫 aaaReview hello 架構 |Microsoft 文件"
description: "本文提供元件和複寫使用 hello Azure Site Recovery 服務的 Azure 區域之間的 Azure Vm 時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="12abd-103">步驟 1： 檢閱 Azure VM 之間的複寫的 Azure 地區的 hello 架構</span><span class="sxs-lookup"><span data-stu-id="12abd-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="12abd-104">檢閱 hello 之後[概觀步驟](azure-to-azure-walkthrough-overview.md)閱讀此文章 toounderstand hello 元件和複寫，並從一個 Azure 區域 tooanother，復原 Azure 虛擬機器 (Vm) 時所使用的處理序使用針對此部署，[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="12abd-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="12abd-105">當您完成 hello 發行項時，您應該清楚了解 Azure VM 複寫 tooanother 區域的運作方式。</span><span class="sxs-lookup"><span data-stu-id="12abd-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="12abd-106">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="12abd-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="12abd-107">Azure VM 複寫以 hello Site Recovery 服務目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="12abd-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="12abd-108">架構元件</span><span class="sxs-lookup"><span data-stu-id="12abd-108">Architectural components</span></span>

<span data-ttu-id="12abd-109">下列圖表中的 hello 提供 Azure VM 中的環境 （在此範例中，hello 美國東部位置） 的特定區域的高層級檢視。</span><span class="sxs-lookup"><span data-stu-id="12abd-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="12abd-110">在 Azure VM 的環境中：</span><span class="sxs-lookup"><span data-stu-id="12abd-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="12abd-111">應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12abd-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="12abd-112">hello Vm 可以包含在虛擬網路內的一個或多個子網路。</span><span class="sxs-lookup"><span data-stu-id="12abd-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![客戶環境](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="12abd-114">複寫程序</span><span class="sxs-lookup"><span data-stu-id="12abd-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="12abd-115">步驟 1</span><span class="sxs-lookup"><span data-stu-id="12abd-115">Step 1</span></span>

<span data-ttu-id="12abd-116">當您啟用 Azure VM 複寫 hello Azure 入口網站中的時，hello 示 hello 下列圖表和資料表會自動建立 hello 目標區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="12abd-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="12abd-117">根據預設，會根據來源地區設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="12abd-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="12abd-118">您可以自訂所需的 hello 目標設定。</span><span class="sxs-lookup"><span data-stu-id="12abd-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="12abd-119">[深入了解](site-recovery-replicate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="12abd-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![啟用複寫程序，步驟 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="12abd-121">**Resource**</span><span class="sxs-lookup"><span data-stu-id="12abd-121">**Resource**</span></span> | <span data-ttu-id="12abd-122">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="12abd-122">**Details**</span></span>
--- | ---
<span data-ttu-id="12abd-123">**目標資源群組**</span><span class="sxs-lookup"><span data-stu-id="12abd-123">**Target resource group**</span></span> | <span data-ttu-id="12abd-124">hello 複寫的 Vm 屬於容錯移轉之後的資源群組 toowhich。</span><span class="sxs-lookup"><span data-stu-id="12abd-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="12abd-125">**目標虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="12abd-125">**Target virtual network**</span></span> | <span data-ttu-id="12abd-126">在其中複寫的 Vm 位於容錯移轉之後 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="12abd-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="12abd-127">在來源和目標的虛擬網路之間會建立網路對應，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="12abd-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="12abd-128">**快取儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="12abd-128">**Cache storage accounts**</span></span> | <span data-ttu-id="12abd-129">來源的 vm 上的變更複寫 toohello 目標儲存體帳戶之前，它們會追蹤並傳送嗨目標位置中 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12abd-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="12abd-130">這可確保在 hello VM 上執行的實際執行應用程式的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="12abd-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="12abd-131">**目標儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="12abd-131">**Target storage accounts**</span></span>  | <span data-ttu-id="12abd-132">在 hello 目標位置 toowhich hello 資料的儲存體帳戶會被複寫。</span><span class="sxs-lookup"><span data-stu-id="12abd-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="12abd-133">**目標可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="12abd-133">**Target availability sets**</span></span>  | <span data-ttu-id="12abd-134">可用性設定組中的 hello 複寫 Vm 位於容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="12abd-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="12abd-135">步驟 2</span><span class="sxs-lookup"><span data-stu-id="12abd-135">Step 2</span></span>

<span data-ttu-id="12abd-136">因為已啟用複寫，hello Site Recovery 擴充行動服務會自動安裝在 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="12abd-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="12abd-137">發生 hello 下列情況：</span><span class="sxs-lookup"><span data-stu-id="12abd-137">hello following occurs:</span></span>

1. <span data-ttu-id="12abd-138">hello VM 已向站台復原。</span><span class="sxs-lookup"><span data-stu-id="12abd-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="12abd-139">Hello VM 設定連續複寫。</span><span class="sxs-lookup"><span data-stu-id="12abd-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="12abd-140">資料寫入 hello VM 磁碟是持續傳送嗨來源位置中的 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12abd-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![啟用複寫程序，步驟 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="12abd-142">請注意，站台復原永遠不需要輸入連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="12abd-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="12abd-143">僅輸出連接 tooSite 復原服務 Url/IP 位址、 Office 365 驗證 Url/IP 位址，以及需要快取儲存體帳戶的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="12abd-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="12abd-144">連續複寫程序</span><span class="sxs-lookup"><span data-stu-id="12abd-144">Continuous replication process</span></span>

<span data-ttu-id="12abd-145">連續的複寫運作正常之後，磁碟寫入會立即傳送 toohello 快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12abd-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="12abd-146">站台復原處理 hello 資料，並將它傳送 toohello 目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="12abd-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="12abd-147">處理 hello 資料之後，每隔幾分鐘 hello 目標儲存體帳戶會產生復原點。</span><span class="sxs-lookup"><span data-stu-id="12abd-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="12abd-148">容錯移轉程序</span><span class="sxs-lookup"><span data-stu-id="12abd-148">Failover process</span></span>

<span data-ttu-id="12abd-149">當您起始容錯移轉時，Vm 建立 hello 目標資源群組、 目標虛擬網路、 目標子網路中的 hello 與 hello 目標可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="12abd-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="12abd-150">在容錯移轉時，您可以使用任何復原點。</span><span class="sxs-lookup"><span data-stu-id="12abd-150">During a failover, you can use any recovery point.</span></span>

![容錯移轉程序](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="12abd-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12abd-152">Next steps</span></span>

<span data-ttu-id="12abd-153">跳過[步驟 2： 確認必要條件和限制](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="12abd-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
