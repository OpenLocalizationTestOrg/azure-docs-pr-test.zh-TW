---
title: "使用 Azure Site Recovery 複寫至 Azure 的必要條件 | Microsoft Docs"
description: "本文摘要說明使用 Azure Site Recovery 服務將 VM 和實體機器複寫至 Azure 的必要條件。"
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: fb5b8c9ac96ac44d0112919664a177f33ef392da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-to-another-region-by-using-azure-site-recovery"></a><span data-ttu-id="b093f-103">使用 Azure Site Recovery 將 Azure 虛擬機器複寫至另一個區域的必要條件</span><span class="sxs-lookup"><span data-stu-id="b093f-103">Prerequisites for replicating Azure virtual machines to another region by using Azure Site Recovery</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b093f-104">從 Azure 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="b093f-104">Replicate from Azure to Azure</span></span>](site-recovery-azure-to-azure-prereq.md)
> * [<span data-ttu-id="b093f-105">從內部部署複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="b093f-105">Replicate from on-premises to Azure</span></span>](site-recovery-prereq.md)

<span data-ttu-id="b093f-106">Azure Site Recovery 是一項有助於建立商務持續性和災害復原 (BCDR) 策略的服務，可協調：</span><span class="sxs-lookup"><span data-stu-id="b093f-106">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating:</span></span>
* <span data-ttu-id="b093f-107">將 Azure 虛擬機器複寫到另一個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b093f-107">Replication of Azure virtual machines to another Azure region.</span></span>
* <span data-ttu-id="b093f-108">將內部部署實體伺服器與虛擬機器複寫至 Azure 或次要資料中心。</span><span class="sxs-lookup"><span data-stu-id="b093f-108">Replication of on-premises physical servers and virtual machines to Azure or to a secondary datacenter.</span></span> 

<span data-ttu-id="b093f-109">當主要位置運作中斷時，您可以容錯移轉至次要位置，讓應用程式和工作負載保持可用。</span><span class="sxs-lookup"><span data-stu-id="b093f-109">When outages occur in your primary location, you can fail over to a secondary location to keep apps and workloads available.</span></span> <span data-ttu-id="b093f-110">當主要位置恢復正常作業時，您即可容錯回復至該位置。</span><span class="sxs-lookup"><span data-stu-id="b093f-110">You can fail back to your primary location when it returns to normal operations.</span></span> <span data-ttu-id="b093f-111">如需有關 Site Recovery 的詳細資訊，請參閱[什麼是 Site Recovery？](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b093f-111">For more about Site Recovery, see [What is Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="b093f-112">本文摘要說明開始進行從內部部署到 Azure 的 Site Recovery 複寫的必要條件。</span><span class="sxs-lookup"><span data-stu-id="b093f-112">This article summarizes the prerequisites required to begin Site Recovery replication from on-premises to Azure.</span></span>

<span data-ttu-id="b093f-113">在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="b093f-113">Post any comments at the bottom of the article, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="azure-requirements"></a><span data-ttu-id="b093f-114">Azure 需求</span><span class="sxs-lookup"><span data-stu-id="b093f-114">Azure requirements</span></span>

<span data-ttu-id="b093f-115">**需求**</span><span class="sxs-lookup"><span data-stu-id="b093f-115">**Requirement**</span></span> | <span data-ttu-id="b093f-116">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="b093f-116">**Details**</span></span>
--- | ---
<span data-ttu-id="b093f-117">**Azure 帳戶**</span><span class="sxs-lookup"><span data-stu-id="b093f-117">**Azure account**</span></span> | <span data-ttu-id="b093f-118">[Microsoft Azure](http://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b093f-118">A [Microsoft Azure](http://azure.microsoft.com/) account.</span></span><br/><br/> <span data-ttu-id="b093f-119">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="b093f-119">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
<span data-ttu-id="b093f-120">**Site Recovery 服務**</span><span class="sxs-lookup"><span data-stu-id="b093f-120">**Site Recovery service**</span></span> | <span data-ttu-id="b093f-121">如需有關 Site Recovery 價格的詳細資訊，請參閱 [Site Recovery 價格](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="b093f-121">For more about Site Recovery pricing, see [Site Recovery pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span> <span data-ttu-id="b093f-122">建議您在想要做為災害復原位置的目標 Azure 區域中建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="b093f-122">We recommend that you create a Recovery Services vault in the target Azure region that you want to use as a disaster recovery location.</span></span> <span data-ttu-id="b093f-123">例如，如果來源 VM 是在美國東部運作，而且您想要複寫到美國中部，建議您在美國中部建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="b093f-123">For example, if your source VMs are running in East US, and you want to replicate to Central US, we recommend that you create the vault in Central US.</span></span>|
<span data-ttu-id="b093f-124">**Azure 容量**</span><span class="sxs-lookup"><span data-stu-id="b093f-124">**Azure capacity**</span></span> | <span data-ttu-id="b093f-125">對於您想要做為災害復原位置的目標 Azure 區域，您需要有足夠容量可容納虛擬機器、儲存體帳戶和網路元件的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b093f-125">For the target Azure region that you want to use as your disaster recovery location, you need to have a subscription with sufficient capacity for virtual machines, storage accounts, and network components.</span></span> <span data-ttu-id="b093f-126">您可以連絡支援人員增加容量。</span><span class="sxs-lookup"><span data-stu-id="b093f-126">You can contact support to add more capacity.</span></span>
<span data-ttu-id="b093f-127">**儲存體指引**</span><span class="sxs-lookup"><span data-stu-id="b093f-127">**Storage guidance**</span></span> | <span data-ttu-id="b093f-128">請確定您遵循來源 Azure 虛擬機器的[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)，以避免任何效能問題。</span><span class="sxs-lookup"><span data-stu-id="b093f-128">Ensure that you follow the [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure virtual machines to avoid any performance issues.</span></span> <span data-ttu-id="b093f-129">如果您遵循預設設定，Site Recovery 會根據來源組態建立所需的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b093f-129">If you follow the default settings, Site Recovery creates the required storage accounts based on the source configuration.</span></span> <span data-ttu-id="b093f-130">如果您自訂並選取您自己的設定，請確定您按照[虛擬機器磁碟的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)進行。</span><span class="sxs-lookup"><span data-stu-id="b093f-130">If you customize and select your own settings, ensure that you follow the [scalability targets for virtual machine disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="b093f-131">**網路服務指南**</span><span class="sxs-lookup"><span data-stu-id="b093f-131">**Networking guidance**</span></span> | <span data-ttu-id="b093f-132">您需要將 Azure VM 對於特定 URL 或 IP 範圍的輸出連線能力列入白名單。</span><span class="sxs-lookup"><span data-stu-id="b093f-132">You need to whitelist the outbound connectivity from your Azure VM for specific URLs or IP ranges.</span></span> <span data-ttu-id="b093f-133">如需詳細資料，請參閱[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)文章。</span><span class="sxs-lookup"><span data-stu-id="b093f-133">For more details, refer to the [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>
<span data-ttu-id="b093f-134">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="b093f-134">**Azure VM**</span></span> | <span data-ttu-id="b093f-135">確定 Windows 或 Linux VM 上有全部最新的根憑證。</span><span class="sxs-lookup"><span data-stu-id="b093f-135">Ensure that all the latest root certificates are present on the Windows or Linux VM.</span></span> <span data-ttu-id="b093f-136">如果沒有最新的根憑證，VM 會因安全性條件限制而無法註冊至 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="b093f-136">If the latest root certificates are not present, the VM cannot be registered to Site Recovery due to security constraints.</span></span>

>[!NOTE]
><span data-ttu-id="b093f-137">如需特定設定支援的詳細資料，請參閱[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="b093f-137">For more details about support for specific configurations, read the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b093f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b093f-138">Next steps</span></span>
- <span data-ttu-id="b093f-139">深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="b093f-139">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
- <span data-ttu-id="b093f-140">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="b093f-140">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
