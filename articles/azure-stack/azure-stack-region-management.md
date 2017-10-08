---
title: "aaaRegion 管理 Azure 堆疊中的 |Microsoft 文件"
description: "Azure Stack 中的區域管理概觀。"
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="71bce-103">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="71bce-103">Region management in Azure Stack</span></span>
<span data-ttu-id="71bce-104">Azure 的堆疊已 hello 概念的區域，也就是組成 hello hello Azure 堆疊基礎結構所組成的硬體資源的邏輯實體。</span><span class="sxs-lookup"><span data-stu-id="71bce-104">Azure Stack has hello concept of regions, which are logical entities comprised of hello hardware resources that make up hello Azure Stack infrastructure.</span></span> <span data-ttu-id="71bce-105">內部區域管理中，您可以找到所有資源的必要的 toosuccessfully 都運作 hello Azure 堆疊基礎結構的生命週期。</span><span class="sxs-lookup"><span data-stu-id="71bce-105">Inside Region management, you can find all resources that are required toosuccessfully operate hello Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="71bce-106">hello Azure 堆疊開發套件是以單一節點部署，而且等於一個區域。</span><span class="sxs-lookup"><span data-stu-id="71bce-106">hello Azure Stack Development Kit is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="71bce-107">如果您設定不同的硬體上 Azure 堆疊開發套件的另一個執行個體，這個執行個體是 hello 的不同的區域。</span><span class="sxs-lookup"><span data-stu-id="71bce-107">If you set up another instance of hello Azure Stack Development Kit on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-hello-region-management-tile"></a><span data-ttu-id="71bce-108">可透過 hello 區域管理並排顯示的資訊</span><span class="sxs-lookup"><span data-stu-id="71bce-108">Information available through hello Region Management tile</span></span>
<span data-ttu-id="71bce-109">Azure 堆疊都有可用的 hello 的區域管理功能的一組**區域管理**磚。</span><span class="sxs-lookup"><span data-stu-id="71bce-109">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="71bce-110">此磚是可用 tooa hello hello 管理員入口網站中的預設儀表板上的雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="71bce-110">This tile is available tooa cloud administrator on hello default dashboard in hello administrator portal.</span></span> <span data-ttu-id="71bce-111">您可以透過此磚來監視和更新特定區域的 Azure Stack 區域及其元件。</span><span class="sxs-lookup"><span data-stu-id="71bce-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![hello 區域管理圖格](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="71bce-113">如果您按一下 hello 區域管理磚中的區域，您可以存取 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="71bce-113">If you click a region in hello Region management tile, you can access hello following information:</span></span>

  ![描述窗格在 hello 區域管理刀鋒視窗上的](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="71bce-115">**hello 資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="71bce-115">**hello resource menu**.</span></span> <span data-ttu-id="71bce-116">您可以在這裡存取特定的基礎結構管理領域，以及檢視和管理租用戶資源，例如儲存體帳戶和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="71bce-116">Here, you can access specific infrastructure management areas, and view and manage tenant resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="71bce-117">**警示**。</span><span class="sxs-lookup"><span data-stu-id="71bce-117">**Alerts**.</span></span> <span data-ttu-id="71bce-118">此磚會列出全系統警示，並提供每個警示的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="71bce-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="71bce-119">**更新**。</span><span class="sxs-lookup"><span data-stu-id="71bce-119">**Updates**.</span></span> <span data-ttu-id="71bce-120">在此磚，您可以檢視 hello Azure 堆疊基礎結構的目前版本。</span><span class="sxs-lookup"><span data-stu-id="71bce-120">In this tile, you can view hello current version of your Azure Stack infrastructure.</span></span>

4. <span data-ttu-id="71bce-121">**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="71bce-121">**Resource providers**.</span></span> <span data-ttu-id="71bce-122">資源提供者是 hello 位置 toomanage hello 租用戶提供的功能 hello 元件需要 toorun Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="71bce-122">Resource providers is hello place toomanage hello tenant functionality offered by hello components required toorun Azure Stack.</span></span> <span data-ttu-id="71bce-123">每個資源提供者皆隨附系統管理體驗。</span><span class="sxs-lookup"><span data-stu-id="71bce-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="71bce-124">這項體驗可以包含 hello 特定提供者、 度量和其他管理功能特定 toohello 資源提供者的警示。</span><span class="sxs-lookup"><span data-stu-id="71bce-124">This experience can include alerts for hello specific provider, metrics, and other management capabilities specific toohello resource provider.</span></span>
 
5. <span data-ttu-id="71bce-125">**基礎結構角色**。</span><span class="sxs-lookup"><span data-stu-id="71bce-125">**Infrastructure roles**.</span></span> <span data-ttu-id="71bce-126">基礎結構角色是 hello 元件需要 toorun Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="71bce-126">Infrastructure roles are hello components necessary toorun Azure Stack.</span></span> <span data-ttu-id="71bce-127">列出報告警示的唯一 hello 基礎結構角色。</span><span class="sxs-lookup"><span data-stu-id="71bce-127">Only hello infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="71bce-128">按一下角色，您可以檢視 hello 與 hello 特定角色，此角色執行所在的 hello 角色執行個體相關聯的警示。</span><span class="sxs-lookup"><span data-stu-id="71bce-128">By clicking a role, you can view hello alerts associated with hello specific role and hello role instances where this role is running.</span></span> <span data-ttu-id="71bce-129">雖然 hello 功能 toostart，重新啟動，或關閉基礎結構角色執行個體，執行**不**開發套件環境中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="71bce-129">Although there is hello capability toostart, restart, or shut down an infrastructure role instance, do **not** do this in a development kit environment.</span></span> <span data-ttu-id="71bce-130">這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。</span><span class="sxs-lookup"><span data-stu-id="71bce-130">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="71bce-131">Hello 開發套件中重新啟動角色執行個體 (特別是 Xrp01 AzS) 會導致系統不穩定。</span><span class="sxs-lookup"><span data-stu-id="71bce-131">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71bce-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71bce-132">Next steps</span></span>
[<span data-ttu-id="71bce-133">在 Azure Stack 中監視健康情況和警示</span><span class="sxs-lookup"><span data-stu-id="71bce-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="71bce-134">在 Azure Stack 中管理更新</span><span class="sxs-lookup"><span data-stu-id="71bce-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)






