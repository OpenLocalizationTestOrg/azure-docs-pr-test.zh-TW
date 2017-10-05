---
title: "檢閱 Azure 區域之間的 Azure VM 複寫架構 | Microsoft Docs"
description: "本文概要說明使用 Azure Site Recovery 服務複寫 Azure 區域之間的 Azure VM 時所用的元件和架構。"
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
ms.openlocfilehash: f471add4f4dee26482e2820fb06d010d6c0c0e88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="26893-103">步驟 1：檢閱 Azure 地區之間的 Azure VM 複寫架構</span><span class="sxs-lookup"><span data-stu-id="26893-103">Step 1: Review the architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="26893-104">在檢閱此部署的[概觀步驟](azure-to-azure-walkthrough-overview.md)之後，請閱讀本文以了解使用 [Azure Site Recovery](site-recovery-overview.md) 從一個 Azure 區域將 Azure 虛擬機器 (VM) 複寫及復原到另一個 Azure 區域時所使用的元件和處理。</span><span class="sxs-lookup"><span data-stu-id="26893-104">After reviewing the [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article to understand the components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region to another, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="26893-105">當您完成本文時，應該清楚了解 Azure VM 複寫到另一個區域的運作方式。</span><span class="sxs-lookup"><span data-stu-id="26893-105">When you finish the article, you should have a clear understanding of how Azure VM replication to another region works.</span></span>
- <span data-ttu-id="26893-106">請在本文下方張貼意見，或在 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="26893-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="26893-107">Site Recovery 服務的 Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="26893-107">Azure VM replication with the Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="26893-108">架構元件</span><span class="sxs-lookup"><span data-stu-id="26893-108">Architectural components</span></span>

<span data-ttu-id="26893-109">下圖提供特定區域 (在此範例中為美國東部位置) 之中 Azure VM 環境的高階檢視。</span><span class="sxs-lookup"><span data-stu-id="26893-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="26893-110">在 Azure VM 的環境中：</span><span class="sxs-lookup"><span data-stu-id="26893-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="26893-111">應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26893-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="26893-112">VM 可以包含在虛擬網路內的一個或多個子網路。</span><span class="sxs-lookup"><span data-stu-id="26893-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![客戶環境](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="26893-114">複寫程序</span><span class="sxs-lookup"><span data-stu-id="26893-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="26893-115">步驟 1</span><span class="sxs-lookup"><span data-stu-id="26893-115">Step 1</span></span>

<span data-ttu-id="26893-116">您在 Azure 入口網站中啟用 Azure VM 複寫時，會在目標區域中自動建立下圖和下表所示的資源。</span><span class="sxs-lookup"><span data-stu-id="26893-116">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="26893-117">根據預設，會根據來源地區設定建立資源。</span><span class="sxs-lookup"><span data-stu-id="26893-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="26893-118">您可以視需要自訂目標設定。</span><span class="sxs-lookup"><span data-stu-id="26893-118">You can customize the target settings as required.</span></span> <span data-ttu-id="26893-119">[深入了解](site-recovery-replicate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="26893-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![啟用複寫程序，步驟 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="26893-121">**Resource**</span><span class="sxs-lookup"><span data-stu-id="26893-121">**Resource**</span></span> | <span data-ttu-id="26893-122">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="26893-122">**Details**</span></span>
--- | ---
<span data-ttu-id="26893-123">**目標資源群組**</span><span class="sxs-lookup"><span data-stu-id="26893-123">**Target resource group**</span></span> | <span data-ttu-id="26893-124">在容錯移轉之後複寫的 VM 所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="26893-124">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="26893-125">**目標虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="26893-125">**Target virtual network**</span></span> | <span data-ttu-id="26893-126">在容錯移轉之後複寫的 VM 所在的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26893-126">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="26893-127">在來源和目標的虛擬網路之間會建立網路對應，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="26893-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="26893-128">**快取儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="26893-128">**Cache storage accounts**</span></span> | <span data-ttu-id="26893-129">來源 VM 上的變更複寫到目標儲存體帳戶之前，會受到追蹤並傳送到目標位置中的快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26893-129">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="26893-130">這可確保對於 VM 上執行的生產應用程式所造成的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="26893-130">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="26893-131">**目標儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="26893-131">**Target storage accounts**</span></span>  | <span data-ttu-id="26893-132">將資料複寫至其中的目標位置儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26893-132">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="26893-133">**目標可用性設定組**</span><span class="sxs-lookup"><span data-stu-id="26893-133">**Target availability sets**</span></span>  | <span data-ttu-id="26893-134">在容錯移轉之後複寫的 VM 所在的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="26893-134">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="26893-135">步驟 2</span><span class="sxs-lookup"><span data-stu-id="26893-135">Step 2</span></span>

<span data-ttu-id="26893-136">啟用複寫時，會在 VM 上自動安裝 Site Recovery 擴充行動服務。</span><span class="sxs-lookup"><span data-stu-id="26893-136">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="26893-137">發生的情況如下：</span><span class="sxs-lookup"><span data-stu-id="26893-137">The following occurs:</span></span>

1. <span data-ttu-id="26893-138">向 Site Recovery 註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="26893-138">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="26893-139">對於 VM 設定連續複寫。</span><span class="sxs-lookup"><span data-stu-id="26893-139">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="26893-140">VM 磁碟上的資料寫入持續傳送到來源位置的快取儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="26893-140">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![啟用複寫程序，步驟 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="26893-142">請注意，Site Recovery 永遠不會需要 VM 的輸入連線能力。</span><span class="sxs-lookup"><span data-stu-id="26893-142">Note that Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="26893-143">僅需要 Site Recovery 服務 URL/IP 位址、Office 365 驗證 URL/IP 位址和快取儲存體帳戶 IP 位址的輸出連線能力。</span><span class="sxs-lookup"><span data-stu-id="26893-143">Only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="26893-144">連續複寫程序</span><span class="sxs-lookup"><span data-stu-id="26893-144">Continuous replication process</span></span>

<span data-ttu-id="26893-145">連續複寫進行之後，磁碟寫入會立即傳送至快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26893-145">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="26893-146">Site Recovery 會處理資料，並將資料傳送到目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26893-146">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="26893-147">處理資料之後，目標儲存體帳戶會每隔幾分鐘產生復原點。</span><span class="sxs-lookup"><span data-stu-id="26893-147">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="26893-148">容錯移轉程序</span><span class="sxs-lookup"><span data-stu-id="26893-148">Failover process</span></span>

<span data-ttu-id="26893-149">您起始容錯移轉時，會在目標資源群組、目標虛擬網路，目標子網路和目標可用性設定組中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="26893-149">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="26893-150">在容錯移轉時，您可以使用任何復原點。</span><span class="sxs-lookup"><span data-stu-id="26893-150">During a failover, you can use any recovery point.</span></span>

![容錯移轉程序](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="26893-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26893-152">Next steps</span></span>

<span data-ttu-id="26893-153">移至[步驟 2：確認必要條件和限制](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="26893-153">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
