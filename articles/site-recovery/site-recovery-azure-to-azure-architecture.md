---
title: "Azure 區域之間的 Azure 虛擬機器複寫如何在 Azure Site Recovery 中運作？  | Microsoft Docs"
description: "本文概要說明使用 Azure Site Recovery 服務複寫 Azure 區域之間的 Azure VM 時所用的元件和架構。"
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="636d1-104">Azure VM 複寫如何在 Site Recovery 中運作？</span><span class="sxs-lookup"><span data-stu-id="636d1-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="636d1-105">本文說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務從一個區域複寫 Azure 虛擬機器 (VM) 並復原到另一個區域時的相關元件和程序。</span><span class="sxs-lookup"><span data-stu-id="636d1-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="636d1-106">Site Recovery 服務的 Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="636d1-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="636d1-107">請在本文下方張貼意見，或在 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="636d1-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="636d1-108">架構元件</span><span class="sxs-lookup"><span data-stu-id="636d1-108">Architectural components</span></span>

<span data-ttu-id="636d1-109">下圖提供特定區域 (在此範例中為美國東部位置) 之中 Azure VM 環境的高階檢視。</span><span class="sxs-lookup"><span data-stu-id="636d1-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="636d1-110">在 Azure VM 的環境中：</span><span class="sxs-lookup"><span data-stu-id="636d1-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="636d1-111">應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="636d1-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="636d1-112">VM 可以包含在虛擬網路內的一個或多個子網路。</span><span class="sxs-lookup"><span data-stu-id="636d1-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![客戶環境](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="636d1-114">了解[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)中的部署必要條件和需求。</span><span class="sxs-lookup"><span data-stu-id="636d1-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="636d1-115">複寫程序</span><span class="sxs-lookup"><span data-stu-id="636d1-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="636d1-116">步驟 1</span><span class="sxs-lookup"><span data-stu-id="636d1-116">Step 1</span></span>

<span data-ttu-id="636d1-117">您在 Azure 入口網站中啟用 Azure VM 複寫時，會在目標區域中自動建立下圖和下表所示的資源。</span><span class="sxs-lookup"><span data-stu-id="636d1-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="636d1-118">根據預設，會根據來源地區設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="636d1-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="636d1-119">您可以視需要自訂目標設定。</span><span class="sxs-lookup"><span data-stu-id="636d1-119">You can customize the target settings as required.</span></span> <span data-ttu-id="636d1-120">[深入了解](site-recovery-replicate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="636d1-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![啟用複寫程序，步驟 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="636d1-122">**Resource**</span><span class="sxs-lookup"><span data-stu-id="636d1-122">**Resource**</span></span> | <span data-ttu-id="636d1-123">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="636d1-123">**Details**</span></span>
--- | ---
<span data-ttu-id="636d1-124">**目標資源群組**</span><span class="sxs-lookup"><span data-stu-id="636d1-124">**Target resource group**</span></span> | <span data-ttu-id="636d1-125">在容錯移轉之後複寫的 VM 所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="636d1-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="636d1-126">**目標虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="636d1-126">**Target virtual network**</span></span> | <span data-ttu-id="636d1-127">在容錯移轉之後複寫的 VM 所在的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="636d1-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="636d1-128">在來源和目標的虛擬網路之間會建立網路對應，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="636d1-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="636d1-129">**快取儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="636d1-129">**Cache storage accounts**</span></span> | <span data-ttu-id="636d1-130">來源 VM 上的變更複寫到目標儲存體帳戶之前，會受到追蹤並傳送到目標位置中的快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="636d1-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="636d1-131">這可確保對於 VM 上執行的生產應用程式所造成的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="636d1-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="636d1-132">**目標儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="636d1-132">**Target storage accounts**</span></span>  | <span data-ttu-id="636d1-133">將資料複寫至其中的目標位置儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="636d1-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="636d1-134">**目標可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="636d1-134">**Target availability sets**</span></span>  | <span data-ttu-id="636d1-135">在容錯移轉之後複寫的 VM 所在的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="636d1-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="636d1-136">步驟 2</span><span class="sxs-lookup"><span data-stu-id="636d1-136">Step 2</span></span>

<span data-ttu-id="636d1-137">啟用複寫時，會在 VM 上自動安裝 Site Recovery 擴充行動服務。</span><span class="sxs-lookup"><span data-stu-id="636d1-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="636d1-138">發生的情況如下：</span><span class="sxs-lookup"><span data-stu-id="636d1-138">The following occurs:</span></span>

1. <span data-ttu-id="636d1-139">向 Site Recovery 註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="636d1-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="636d1-140">對於 VM 設定連續複寫。</span><span class="sxs-lookup"><span data-stu-id="636d1-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="636d1-141">VM 磁碟上的資料寫入持續傳送到來源位置的快取儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="636d1-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![啟用複寫程序，步驟 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="636d1-143">Site Recovery 永遠不會需要 VM 的輸入連線能力。</span><span class="sxs-lookup"><span data-stu-id="636d1-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="636d1-144">VM 僅需要 Site Recovery 服務 URL/IP 位址、Office 365 驗證 URL/IP 位址和快取儲存體帳戶 IP 位址的輸出連線能力。</span><span class="sxs-lookup"><span data-stu-id="636d1-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="636d1-145">如需詳細資訊，請參閱[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)文章。</span><span class="sxs-lookup"><span data-stu-id="636d1-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="636d1-146">連續複寫程序</span><span class="sxs-lookup"><span data-stu-id="636d1-146">Continuous replication process</span></span>

<span data-ttu-id="636d1-147">連續複寫進行之後，磁碟寫入會立即傳送至快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="636d1-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="636d1-148">Site Recovery 會處理資料，並將資料傳送到目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="636d1-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="636d1-149">處理資料之後，目標儲存體帳戶會每隔幾分鐘產生復原點。</span><span class="sxs-lookup"><span data-stu-id="636d1-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="636d1-150">容錯移轉程序</span><span class="sxs-lookup"><span data-stu-id="636d1-150">Failover process</span></span>

<span data-ttu-id="636d1-151">您起始容錯移轉時，會在目標資源群組、目標虛擬網路，目標子網路和目標可用性設定組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="636d1-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="636d1-152">在容錯移轉時，您可以使用任何復原點。</span><span class="sxs-lookup"><span data-stu-id="636d1-152">During a failover, you can use any recovery point.</span></span>

![容錯移轉程序](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="636d1-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="636d1-154">Next steps</span></span>

- <span data-ttu-id="636d1-155">深入了解 Azure VM 複寫的[網路](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="636d1-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="636d1-156">依照逐步解說[複寫 Azure VM。](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="636d1-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
