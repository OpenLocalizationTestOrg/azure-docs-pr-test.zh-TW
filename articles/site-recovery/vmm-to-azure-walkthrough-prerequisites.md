---
title: "使用 Azure Site Recovery 檢閱 Hyper-V 對 Azure 複寫的必要條件 (含 System Center VMM) | Microsoft Docs"
description: "描述使用 Azure Site Recovery 來設定將 VMM 雲端中的內部部署 Hyper-V VM 複寫、容錯移轉和復原至 Azure 的必要條件"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: 47c178c66ec98fe5d333edd725b64465026e73ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="7180a-103">步驟 2：檢閱 Hyper-V (含 VMM) 對 Azure 複寫的必要條件</span><span class="sxs-lookup"><span data-stu-id="7180a-103">Step 2: Review the prerequisites for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="7180a-104">在檢閱[情節架構](vmm-to-azure-walkthrough-architecture.md)之後，請閱讀本文以確定您了解部署必要條件。</span><span class="sxs-lookup"><span data-stu-id="7180a-104">After you're reviewed the [scenario architecture](vmm-to-azure-walkthrough-architecture.md), read this article to make sure you understand the deployment prerequisites.</span></span> 

## <a name="prerequisites-and-limitations"></a><span data-ttu-id="7180a-105">必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="7180a-105">Prerequisites and limitations</span></span>

<span data-ttu-id="7180a-106">**需求**</span><span class="sxs-lookup"><span data-stu-id="7180a-106">**Requirement**</span></span> | <span data-ttu-id="7180a-107">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7180a-107">**Details**</span></span>
--- | ---
<span data-ttu-id="7180a-108">**Azure 帳戶**</span><span class="sxs-lookup"><span data-stu-id="7180a-108">**Azure account**</span></span> | <span data-ttu-id="7180a-109">您需要 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="7180a-109">You need a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
<span data-ttu-id="7180a-110">**Azure 儲存體**</span><span class="sxs-lookup"><span data-stu-id="7180a-110">**Azure storage**</span></span> | <span data-ttu-id="7180a-111">您需要 Azure 儲存體帳戶來儲存複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="7180a-111">You need an Azure storage account to store replicated data.</span></span><br/><br/> <span data-ttu-id="7180a-112">儲存體帳戶必須位於與 Azure 復原服務保存庫相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="7180a-112">The storage account must be in the same region as the Azure Recovery Services vault.</span></span><br/><br/><span data-ttu-id="7180a-113">您可以使用[異地備援儲存體](../storage/common/storage-redundancy.md#geo-redundant-storage)或本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7180a-113">You can use [geo-redundant storage](../storage/common/storage-redundancy.md#geo-redundant-storage) or locally redundant storage.</span></span> <span data-ttu-id="7180a-114">建議使用異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="7180a-114">We recommend geo-redundant storage.</span></span> <span data-ttu-id="7180a-115">使用異地備援儲存體時，如果發生區域性停電或無法復原主要區域，就能夠恢復資料。</span><span class="sxs-lookup"><span data-stu-id="7180a-115">With geo-redundant storage, data is resilient if a regional outage occurs, or if the primary region can't be recovered.</span></span><br/><br/> <span data-ttu-id="7180a-116">您可以使用標準的 Azure 儲存體帳戶，或使用 Azure [進階儲存體](../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="7180a-116">You can use a standard Azure storage account, or you can use Azure [premium storage](../storage/common/storage-premium-storage.md).</span></span> <span data-ttu-id="7180a-117">進階儲存體可以裝載需要大量 I/O 的工作負載，且通常用於需要持續有高 I/O 效能和低延遲的 VM。</span><span class="sxs-lookup"><span data-stu-id="7180a-117">Premium storage can host I/O intensive workloads, and is typically is used for VMs that need a consistently high I/O performance and low latency.</span></span> <span data-ttu-id="7180a-118">如果您使用進階儲存體來存放複寫的資料，您也需要標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7180a-118">If you use premium storage for replicated data, you also need a standard storage account.</span></span> <span data-ttu-id="7180a-119">標準儲存體帳戶可儲存複寫記錄，這些記錄會擷取內部部署資料不斷發生的變更。</span><span class="sxs-lookup"><span data-stu-id="7180a-119">A standard storage account stores replication logs that capture ongoing changes to on-premises data.</span></span>
<span data-ttu-id="7180a-120">**Azure 網路**</span><span class="sxs-lookup"><span data-stu-id="7180a-120">**Azure network**</span></span> | <span data-ttu-id="7180a-121">您需要 [Azure 網路](../virtual-network/virtual-network-get-started-vnet-subnet.md)，供 Azure VM 在容錯移轉之後連線。</span><span class="sxs-lookup"><span data-stu-id="7180a-121">You need an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md), to which Azure VMs connect after failover.</span></span> <span data-ttu-id="7180a-122">此 Azure 網路必須位於與復原服務保存庫相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="7180a-122">The Azure network must be in the same region as the Recovery Services vault.</span></span>
<span data-ttu-id="7180a-123">**內部部署 VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="7180a-123">**On-premises VMM servers**</span></span> | <span data-ttu-id="7180a-124">您需要一或多部執行 System Center 2012 R2 或更新版本的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7180a-124">You need one or more VMM servers running System Center 2012 R2 or later.</span></span><br/><br/> <span data-ttu-id="7180a-125">每一部 VMM 伺服器必須有一或多個私人雲端。</span><span class="sxs-lookup"><span data-stu-id="7180a-125">Each VMM server must have one or more private clouds.</span></span> <span data-ttu-id="7180a-126">每一個雲端需要一或多個主機群組。</span><span class="sxs-lookup"><span data-stu-id="7180a-126">Each cloud needs one or most host groups.</span></span><br/><br/> <span data-ttu-id="7180a-127">VMM 伺服器需要存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="7180a-127">The VMM server needs internet access.</span></span>
<span data-ttu-id="7180a-128">**內部部署 Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7180a-128">**On-premises Hyper-V**</span></span> | <span data-ttu-id="7180a-129">Hyper-V 主機伺服器必須至少執行 Windows Server 2012 R2 (已啟用 Hyper-V 角色) 或 Microsoft Hyper-V Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="7180a-129">Hyper-V host servers must be running at least Windows Server 2012 R2 with the Hyper-V role enabled, or Microsoft Hyper-V Server 2012 R2.</span></span> <span data-ttu-id="7180a-130">必須安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="7180a-130">The latest updates must be installed.</span></span><br/><br/> <span data-ttu-id="7180a-131">Hyper-V 伺服器必須位於 VMM 主機群組中 (位於 VMM 雲端)。</span><span class="sxs-lookup"><span data-stu-id="7180a-131">The Hyper-V host must be located in a VMM host group (located in a VMM cloud).</span></span><br/><br/> <span data-ttu-id="7180a-132">主機必須具有您想要複寫的一或多個 VM。</span><span class="sxs-lookup"><span data-stu-id="7180a-132">A host must have one or more VMs that you want to replicated.</span></span><br/><br/> <span data-ttu-id="7180a-133">Hyper-V 主機必須連線至網際網路，才能直接或透過 proxy 來複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7180a-133">Hyper-V hosts must be connected to the internet for replication to Azure, directly or with a proxy.</span></span> <span data-ttu-id="7180a-134">Hyper-V 伺服器必須具有 [2961977](https://support.microsoft.com/kb/2961977) 文章所述的修正程式。</span><span class="sxs-lookup"><span data-stu-id="7180a-134">Hyper-V servers must have the fixes described in article [2961977](https://support.microsoft.com/kb/2961977).</span></span>
<span data-ttu-id="7180a-135">**內部部署 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="7180a-135">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="7180a-136">您想要複寫的 VM 應該執行[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，也要符合 [Azure 必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="7180a-136">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span> <span data-ttu-id="7180a-137">啟用複寫之後，可以修改 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="7180a-137">The VM name can be modified after replication is enabled.</span></span> 




## <a name="next-steps"></a><span data-ttu-id="7180a-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7180a-138">Next steps</span></span>

<span data-ttu-id="7180a-139">移至[步驟 3：規劃容量](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="7180a-139">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>