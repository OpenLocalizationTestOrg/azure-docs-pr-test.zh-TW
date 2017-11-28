---
title: "使用 Azure Site Recovery 的複寫 tooAzure 的 aaaPrerequisites |Microsoft 文件"
description: "本文摘要說明使用 hello Azure Site Recovery 服務複寫 Vm 和實體機器 tooAzure 的必要條件。"
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
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a><span data-ttu-id="e80cb-103">用來複寫使用 Azure Site Recovery 的 Azure 虛擬機器 tooanother 區域的必要條件</span><span class="sxs-lookup"><span data-stu-id="e80cb-103">Prerequisites for replicating Azure virtual machines tooanother region by using Azure Site Recovery</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e80cb-104">從 Azure tooAzure 複寫</span><span class="sxs-lookup"><span data-stu-id="e80cb-104">Replicate from Azure tooAzure</span></span>](site-recovery-azure-to-azure-prereq.md)
> * [<span data-ttu-id="e80cb-105">從內部部署 tooAzure 複寫</span><span class="sxs-lookup"><span data-stu-id="e80cb-105">Replicate from on-premises tooAzure</span></span>](site-recovery-prereq.md)

<span data-ttu-id="e80cb-106">hello Azure Site Recovery 服務作為 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調：</span><span class="sxs-lookup"><span data-stu-id="e80cb-106">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating:</span></span>
* <span data-ttu-id="e80cb-107">Azure 虛擬機器 tooanother Azure 區域資料複寫。</span><span class="sxs-lookup"><span data-stu-id="e80cb-107">Replication of Azure virtual machines tooanother Azure region.</span></span>
* <span data-ttu-id="e80cb-108">在內部部署實體伺服器和虛擬機器 tooAzure 或 tooa 次要資料中心複寫。</span><span class="sxs-lookup"><span data-stu-id="e80cb-108">Replication of on-premises physical servers and virtual machines tooAzure or tooa secondary datacenter.</span></span> 

<span data-ttu-id="e80cb-109">當您的主要位置發生中斷時，您可以容錯移轉 tooa 次要位置 tookeep 應用程式和可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="e80cb-109">When outages occur in your primary location, you can fail over tooa secondary location tookeep apps and workloads available.</span></span> <span data-ttu-id="e80cb-110">當它傳回 toonormal 作業，您可以容錯回復 tooyour 主要位置。</span><span class="sxs-lookup"><span data-stu-id="e80cb-110">You can fail back tooyour primary location when it returns toonormal operations.</span></span> <span data-ttu-id="e80cb-111">如需有關 Site Recovery 的詳細資訊，請參閱[什麼是 Site Recovery？](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-111">For more about Site Recovery, see [What is Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="e80cb-112">本文摘要說明 hello 必要條件需要的 toobegin 內部 tooAzure 從站台復原複寫。</span><span class="sxs-lookup"><span data-stu-id="e80cb-112">This article summarizes hello prerequisites required toobegin Site Recovery replication from on-premises tooAzure.</span></span>

<span data-ttu-id="e80cb-113">張貼在 hello hello 文章底部的任何註解或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-113">Post any comments at hello bottom of hello article, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="azure-requirements"></a><span data-ttu-id="e80cb-114">Azure 需求</span><span class="sxs-lookup"><span data-stu-id="e80cb-114">Azure requirements</span></span>

<span data-ttu-id="e80cb-115">**需求**</span><span class="sxs-lookup"><span data-stu-id="e80cb-115">**Requirement**</span></span> | <span data-ttu-id="e80cb-116">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="e80cb-116">**Details**</span></span>
--- | ---
<span data-ttu-id="e80cb-117">**Azure 帳戶**</span><span class="sxs-lookup"><span data-stu-id="e80cb-117">**Azure account**</span></span> | <span data-ttu-id="e80cb-118">[Microsoft Azure](http://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e80cb-118">A [Microsoft Azure](http://azure.microsoft.com/) account.</span></span><br/><br/> <span data-ttu-id="e80cb-119">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="e80cb-119">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
<span data-ttu-id="e80cb-120">**Site Recovery 服務**</span><span class="sxs-lookup"><span data-stu-id="e80cb-120">**Site Recovery service**</span></span> | <span data-ttu-id="e80cb-121">如需有關 Site Recovery 價格的詳細資訊，請參閱 [Site Recovery 價格](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-121">For more about Site Recovery pricing, see [Site Recovery pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span> <span data-ttu-id="e80cb-122">我們建議您復原服務保存庫中建立 hello 目標 Azure 地區的 toouse 做為災害復原位置。</span><span class="sxs-lookup"><span data-stu-id="e80cb-122">We recommend that you create a Recovery Services vault in hello target Azure region that you want toouse as a disaster recovery location.</span></span> <span data-ttu-id="e80cb-123">比方說，如果在美國東部、 執行您的來源 Vm，而且您希望 tooreplicate tooCentral 我們，我們建議您在美國中部建立 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="e80cb-123">For example, if your source VMs are running in East US, and you want tooreplicate tooCentral US, we recommend that you create hello vault in Central US.</span></span>|
<span data-ttu-id="e80cb-124">**Azure 容量**</span><span class="sxs-lookup"><span data-stu-id="e80cb-124">**Azure capacity**</span></span> | <span data-ttu-id="e80cb-125">Hello 目標 Azure 地區的 toouse 做為災害復原位置，您需要 toohave 足夠容量的虛擬機器、 儲存體帳戶和網路元件的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e80cb-125">For hello target Azure region that you want toouse as your disaster recovery location, you need toohave a subscription with sufficient capacity for virtual machines, storage accounts, and network components.</span></span> <span data-ttu-id="e80cb-126">您可以連絡支援 tooadd 容量。</span><span class="sxs-lookup"><span data-stu-id="e80cb-126">You can contact support tooadd more capacity.</span></span>
<span data-ttu-id="e80cb-127">**儲存體指引**</span><span class="sxs-lookup"><span data-stu-id="e80cb-127">**Storage guidance**</span></span> | <span data-ttu-id="e80cb-128">請確定您遵循 hello[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)針對您的來源 Azure 虛擬機器 tooavoid 任何效能問題。</span><span class="sxs-lookup"><span data-stu-id="e80cb-128">Ensure that you follow hello [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure virtual machines tooavoid any performance issues.</span></span> <span data-ttu-id="e80cb-129">如果您遵循 hello 預設設定，站台復原就會建立所需的 hello hello 來源設定為基礎的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e80cb-129">If you follow hello default settings, Site Recovery creates hello required storage accounts based on hello source configuration.</span></span> <span data-ttu-id="e80cb-130">如果您自訂，並選取您自己的設定，請確定您遵循 hello[虛擬機器磁碟的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-130">If you customize and select your own settings, ensure that you follow hello [scalability targets for virtual machine disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="e80cb-131">**網路服務指南**</span><span class="sxs-lookup"><span data-stu-id="e80cb-131">**Networking guidance**</span></span> | <span data-ttu-id="e80cb-132">針對特定的 Url 或 IP 範圍，您需要從 Azure VM toowhitelist hello 的傳出連線。</span><span class="sxs-lookup"><span data-stu-id="e80cb-132">You need toowhitelist hello outbound connectivity from your Azure VM for specific URLs or IP ranges.</span></span> <span data-ttu-id="e80cb-133">如需詳細資訊，請參閱 toohello[網路複寫 Azure 虛擬機器的指引](site-recovery-azure-to-azure-networking-guidance.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="e80cb-133">For more details, refer toohello [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>
<span data-ttu-id="e80cb-134">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="e80cb-134">**Azure VM**</span></span> | <span data-ttu-id="e80cb-135">確認所有 hello 最新的根憑證都會出現在 hello Windows 或 Linux VM 上。</span><span class="sxs-lookup"><span data-stu-id="e80cb-135">Ensure that all hello latest root certificates are present on hello Windows or Linux VM.</span></span> <span data-ttu-id="e80cb-136">如果 hello 最新的根憑證不存在，hello VM 不能註冊的 tooSite 復原，因為 toosecurity 條件約束。</span><span class="sxs-lookup"><span data-stu-id="e80cb-136">If hello latest root certificates are not present, hello VM cannot be registered tooSite Recovery due toosecurity constraints.</span></span>

>[!NOTE]
><span data-ttu-id="e80cb-137">如需支援的特定設定的詳細資訊，請參閱 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-137">For more details about support for specific configurations, read hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e80cb-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e80cb-138">Next steps</span></span>
- <span data-ttu-id="e80cb-139">深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="e80cb-139">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
- <span data-ttu-id="e80cb-140">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="e80cb-140">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
