---
title: "HYPER-V 複寫 tooa 次要 VMM 站台與 Azure Site Recovery 的 aaaReview hello 必要條件 |Microsoft 文件"
description: "說明複寫 HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery hello 必要條件。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a><span data-ttu-id="627a2-103">步驟 2： 檢閱 HYPER-V 虛擬機器複寫 tooa 次要 VMM 站台的 hello 必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="627a2-103">Step 2: Review hello prerequisites and limitations for Hyper-V VM replication tooa secondary VMM site</span></span>


<span data-ttu-id="627a2-104">您已檢閱過 hello 之後[案例架構](vmm-to-vmm-walkthrough-architecture.md)，閱讀此文章 toomake 確定當您了解 hello 部署必要條件，在 系統中心虛擬複寫在內部部署 HYPER-V 虛擬機器 (Vm) 管理Machine Manager (VMM) 雲端，tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="627a2-104">After you've reviewed hello [scenario architecture](vmm-to-vmm-walkthrough-architecture.md), read this article toomake sure you understand hello deployment prerequisites, when replicating on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary site using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="627a2-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="627a2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites-and-limitations"></a><span data-ttu-id="627a2-106">必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="627a2-106">Prerequisites and limitations</span></span>

<span data-ttu-id="627a2-107">**需求**</span><span class="sxs-lookup"><span data-stu-id="627a2-107">**Requirement**</span></span> | <span data-ttu-id="627a2-108">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="627a2-108">**Details**</span></span>
--- | ---
<span data-ttu-id="627a2-109">**Azure**</span><span class="sxs-lookup"><span data-stu-id="627a2-109">**Azure**</span></span> | <span data-ttu-id="627a2-110">[Microsoft Azure](http://azure.microsoft.com/) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="627a2-110">A [Microsoft Azure](http://azure.microsoft.com/) subscription.</span></span><br/><br/> <span data-ttu-id="627a2-111">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="627a2-111">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="627a2-112">[深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。</span><span class="sxs-lookup"><span data-stu-id="627a2-112">[Learn more](https://azure.microsoft.com/pricing/details/site-recovery/) about Site Recovery pricing.</span></span><br/><br/> <span data-ttu-id="627a2-113">檢查網站復原，在各地區上市中支援的 hello 區域[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="627a2-113">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
<span data-ttu-id="627a2-114">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="627a2-114">**VMM servers**</span></span> | <span data-ttu-id="627a2-115">我們建議您有兩部 VMM 伺服器在 hello 主要站台，一個次要的 hello 中。</span><span class="sxs-lookup"><span data-stu-id="627a2-115">We recommend you have two VMM servers, one in hello primary site, and one in hello secondary.</span></span><br/><br/> <span data-ttu-id="627a2-116">支援在單一 VMM 伺服器上的雲端之間進行複寫。</span><span class="sxs-lookup"><span data-stu-id="627a2-116">Replicate between clouds on a single VMM server is supported.</span></span><br/><br/> <span data-ttu-id="627a2-117">VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新的更新。</span><span class="sxs-lookup"><span data-stu-id="627a2-117">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="627a2-118">VMM 伺服器需要網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="627a2-118">VMM servers need internet access.</span></span>
<span data-ttu-id="627a2-119">**VMM 雲端**</span><span class="sxs-lookup"><span data-stu-id="627a2-119">**VMM clouds**</span></span> | <span data-ttu-id="627a2-120">每一部 VMM 伺服器必須在一個或多個雲端，而所有雲端必須都具有 hello HYPER-V 容量設定檔集合。</span><span class="sxs-lookup"><span data-stu-id="627a2-120">Each VMM server must have at one or more clouds, and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="627a2-121">雲端必須包含一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="627a2-121">Clouds must contain one or more VMM host groups.</span></span><br/><br/> <span data-ttu-id="627a2-122">如果您只有一部 VMM 伺服器，它需要至少兩個雲端、 tooact 為主要和次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="627a2-122">If you only have one VMM server, it needs at least two clouds, tooact as primary and secondary.</span></span>
<span data-ttu-id="627a2-123">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="627a2-123">**Hyper-V**</span></span> | <span data-ttu-id="627a2-124">HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="627a2-124">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role, and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="627a2-125">Hyper-V 伺服器應該包含一或多部 VM。</span><span class="sxs-lookup"><span data-stu-id="627a2-125">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="627a2-126">HYPER-V 主機伺服器應該位於 hello 主要和次要 VMM 雲端中的主機群組。</span><span class="sxs-lookup"><span data-stu-id="627a2-126">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="627a2-127">如果您在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，請安裝[更新 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="627a2-127">If you run Hyper-V in a cluster on Windows Server 2012 R2, install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="627a2-128">如果您在 Windows Server 2012 上的叢集中執行 Hyper-V，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="627a2-128">If you run Hyper-V in a cluster on Windows Server 2012, cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="627a2-129">手動設定 hello 叢集代理人。</span><span class="sxs-lookup"><span data-stu-id="627a2-129">Configure hello cluster broker manually.</span></span> <span data-ttu-id="627a2-130">[閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。</span><span class="sxs-lookup"><span data-stu-id="627a2-130">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span><br/><br/> <span data-ttu-id="627a2-131">Hyper-V 伺服器需要網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="627a2-131">Hyper-V servers need internet access.</span></span>




## <a name="next-steps"></a><span data-ttu-id="627a2-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="627a2-132">Next steps</span></span>

<span data-ttu-id="627a2-133">跳過[步驟 3： 規劃網路](vmm-to-vmm-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="627a2-133">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>
